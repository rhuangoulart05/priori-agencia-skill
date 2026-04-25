# Fluxo: Criar Arte

Transforma copy + brief visual em peças finais exportadas.

## Três vias visuais — quando usar cada uma

| Situação | Via |
|---|---|
| Instagram **carrossel** (múltiplos slides, copy denso) | **G4 Editorial** (belt + Pillow) |
| Instagram **post único** com composição visual rica (flyer, evento, save the date, lançamento) | **ChatGPT** (GPT-4o image generation) |
| LinkedIn, Facebook, Stories, formatos variados | **Canva MCP** |
| Post simples só texto, sem foto | **Canva MCP** puro |
| Reel cover | **Canva** com imagem de apoio |

**Regra geral:**
- Carrossel → G4 Editorial (controle total do copy slide a slide)
- Post único com identidade visual forte / composição artística → ChatGPT (aceita logo como input, gera composição completa de uma vez)
- Outros formatos → Canva

---

## Via ChatGPT — Post único (flyer, evento, save the date)

Melhor opção para posts únicos com composição visual rica. O GPT-4o aceita a logo do cliente como imagem de input e gera a arte completa — ilustração, tipografia, elementos decorativos e foto fundidos em uma só geração.

### Como usar

1. **Abra o ChatGPT** (GPT-4o com geração de imagem ativa)
2. **Suba a logo do cliente** como imagem no chat
3. **Descreva a arte** com:
   - O que é (flyer de evento, save the date, post de lançamento...)
   - Textos que devem aparecer (título, data, subtítulo, CTA)
   - Paleta de cores (HEX ou descrição)
   - Estilo visual (moderno, orgânico, minimalista, religioso, corporativo...)
   - Formato: 1080×1350px (4:5 Instagram)
4. **Instrução obrigatória:** diga explicitamente "use a logo que enviei, não acrescente nada além do que pedi"
5. **Itere** se precisar — peça ajustes mantendo o mesmo chat

### O que funciona bem no ChatGPT
- Composições completas com texto integrado à imagem
- Elementos decorativos coerentes com o tema (folhas, formas, texturas)
- Fusão de foto + ilustração + tipografia em uma geração
- Uso correto de logo fornecida como referência

### O que NÃO delegar ao ChatGPT
- Carrosseis (copy denso, múltiplos slides) → G4 Editorial
- Quando precisar de controle preciso de tipografia/brand kit → Canva

---

## Via 1 — G4 Editorial (Instagram 1080×1350 carrossel)

Método validado com a Lupa Gestão (abr/2026). Resultado: qualidade de capa de revista, controle total do layout, sem depender de templates genéricos.

### Etapa 1.A — Gerar Backgrounds com IA

**Ferramenta:** `belt app run google/gemini-2-5-flash-image`

**Paralelismo:** `ThreadPoolExecutor(max_workers=2)` — 4 workers causa rate limiting na API.

**Skip-if-exists:** sempre verificar se o arquivo já existe antes de gerar. Não regera o que já está pronto.

**Estrutura de output:**
```
clientes/<cliente>/artes-geradas/<data>-<slug>/
├── editorial_bg/     ← backgrounds gerados pela IA
└── final_g4/         ← PNGs compostos finais
```

**Modelo de prompt para os backgrounds:**
```
Editorial magazine cover photograph, 1080x1350px portrait.

SCENE: [descrição específica da cena — pessoa, ambiente, ação concreta]
COMPOSITION: [como o frame está organizado, onde fica espaço para texto]
LIGHTING: [tipo de iluminação — natural, dramática, editorial]
STYLE: Forbes/Exame/Valor Econômico magazine cover. Sharp, premium, Brazilian corporate.

PHOTOGRAPHY REQUIREMENTS — MANDATORY:
• SHARP editorial photography — zero motion blur, zero background blur at the top
• Magazine cover quality — like Forbes, Exame, or Valor Econômico
• Strong, clear composition with an obvious subject
• Professional studio or real-world lighting
• Bottom 35% of the image should naturally be slightly darker — text overlay area
• NO text, NO logos, NO UI elements, NO watermarks anywhere
• Format: 1080x1350px portrait (4:5)
```

**Blur obrigatório:** qualquer background que mostre calendário, relógio ou data recebe `GaussianBlur` na composição:
- Calendário principal: `radius=18`
- Elemento secundário com data/relógio: `radius=8`

Motivo: datas na foto conflitam com datas reais do post e confundem o público.

---

### Etapa 1.B — Compor com Pillow

**Canvas:** `W, H = 1080, 1350`

**Safe Zone (área de texto):**
```python
SAFE_X0, SAFE_X1 = 200, 880   # margem lateral: 200px cada lado
SAFE_Y0, SAFE_Y1 = 400, 950   # faixa vertical: 550px de altura útil
SAFE_W, SAFE_H   = 680, 550
```

**Gradiente de contraste (REGRA CRÍTICA):**
```python
bottom_gradient(img, start_y_pct=0.42)
```
Cobre ~58% inferior da imagem. `0.42` = começa um pouco acima da metade.
**Nunca usar valor abaixo de 0.38** — textos centrais perdem contraste.

**Fonte:** Montserrat Variable Font (`Montserrat-Variable.ttf`)
```python
ExtraBold  → set_variation_by_axes([800])
Regular    → set_variation_by_axes([400])
SemiBold   → set_variation_by_axes([600])
```

**Cálculo de altura de texto — BUG CRÍTICO em variable fonts:**
```python
def th(d, text, fnt):
    bb = d.textbbox((0, 0), text, font=fnt)
    return bb[3]   # NUNCA bb[3] - bb[1]
```
Variable fonts têm `bb[1] > 0` (distância âncora-topo do glifo). Usar `bb[3] - bb[1]` dá advance errado e causa sobreposição de textos.
Após cada `draw` call, rastrear o bottom real: `d.textbbox((x, y), text, font=fnt)[3]`.

**Separadores horizontais: PROIBIDO**
Nunca usar `d.line()` ou qualquer `hline()`. Linhas sobrepõem elementos numéricos e ficam mal alinhadas. Espaçamento é feito exclusivamente via constantes `BG` (gap base), `LG` (gap grande), `IG` (gap interno).

**Logo nos slides hook:**
```python
paste_logo_small(img, logo_file, width=130, opacity=130, x=SAFE_X0, y=80)
```
Discreta, só para constar. Presente apenas no slide 1 (hook/capa) de cada post.
Nunca nos slides internos do carrossel.

---

### Tipos de slide

**Hook (slide 1 — capa do post):**
- Foto editorial + `top_vignette` sutil + `bottom_gradient(0.42)`
- Logo pequena no canto superior esquerdo
- Título ExtraBold grande + subtítulo Regular na safe zone inferior

**Carousel dark (slides de conteúdo com fundo escuro):**
- Foto editorial + mesmo gradiente
- Texto claro (WHITE) sobre gradiente
- Sem card overlay

**Carousel light (slides de conteúdo com fundo claro):**
- Card branco semi-transparente sobre a foto:
  ```python
  fill=(255, 255, 255, 215), radius=12
  # Cobre a safe zone: (SAFE_X0-20, SAFE_Y0-20) → (SAFE_X1+20, SAFE_Y1+20)
  ```
- Texto escuro (DARK) sobre o card

**CTA (último slide):**
- Foto editorial premium (pessoa ou ambiente)
- Logo centralizada no rodapé (width=200px)
- Texto CTA acima da logo

---

### Paleta de cores padrão (adaptar por cliente)

Exemplo Lupa Gestão:
```python
GOLD     = (191, 155, 67)
WHITE    = (255, 255, 255)
OFF_WHITE = (235, 228, 210)
DARK     = (15, 22, 40)
```

Para novo cliente: substituir estas constantes pelas cores do `brand.md` do cliente.

---

### Checklist G4 antes de entregar

- [ ] Safe zone respeitada (nenhum texto saindo das bordas 200px / 400-950px)
- [ ] Gradiente iniciando em `0.42` — texto legível em todos os slides
- [ ] Nenhum separador horizontal (`d.line`) no código
- [ ] `th()` usando `bb[3]` (nunca `bb[3] - bb[1]`)
- [ ] Nenhum texto sobrepondo outro (rastrear bottom real após cada draw)
- [ ] Calendários/datas com GaussianBlur aplicado
- [ ] Logo só no slide 1, discreta (opacity 130, width 130px)
- [ ] Paleta correta do cliente (não GOLD/DARK da Lupa se for outro cliente)
- [ ] Arquivos em `clientes/<cliente>/artes-geradas/<slug>/final_g4/`

---

## Via 2 — Canva MCP (LinkedIn, Stories, formatos variados)

### 1. Ler brief visual

Carregue `clientes/<cliente>/calendario/YYYY-MM-DD-<slug>.md` → seção `## Brief Visual`.

### 2. Gerar imagens de apoio (Gemini / NanoBanana)

Se o brief pedir imagem: use a skill `ai-image-generation`.

Prompts bem feitos:
```
[Descrição visual específica do brief, não genérico]
Estilo: [fotorrealista | ilustração vetorial minimalista | 3D render limpo]
Paleta: [cores do brand kit do cliente]
Composição: [rule of thirds | centralizada | com espaço negativo à direita/esquerda]
Negative: stock photo look, generic business imagery, logos, watermarks, text
```

Regras para não ficar genérico:
- **Seja específico.** "Mesa de contador com DARF impresso e cafezinho" > "pessoa trabalhando"
- **Peça espaço negativo** onde vai entrar texto/logo no Canva
- **Nunca peça para inserir logo** — modelos erram logos. Logo vai sempre via Canva

Salve em `clientes/<cliente>/artes-geradas/YYYY-MM-DD-<slug>/imagens-base/`.

### 3. Consultar brand kit no Canva

```
list-brand-kits → encontrar o do cliente
```

Se não existir brand kit no Canva, use dados de `clientes/<cliente>/brand.md` manualmente.

### 4. Criar design no Canva

Use `generate-design-structured`:
- Tipo: formato adequado ao canal (LinkedIn 1200×1500, Stories 1080×1920, etc.)
- Brand kit do cliente
- Conteúdo estruturado slide a slide

### 5. Refinamento visual

Se o output ficar "quadrado":
- `perform-editing-operations` — ajuste tipografia, kerning, hierarquia
- `upload-asset-from-url` — sobe imagem gerada e insere
- Headline grande no hook (80-120pt quebra tudo)
- Um slide com foto full-bleed + texto overlay

### 6. Exportar

`export-design` → PNG ou PDF.

Salve em `clientes/<cliente>/artes-geradas/YYYY-MM-DD-<slug>/final/`.

---

### Como fugir do "quadrado do Canva"

Sintomas:
- Fundo chapado + headline centralizada + ícone vetorial padrão
- Mesma paleta em todos os slides sem contraste
- Tipografia em um único peso

Contramedidas:
1. Headline MUITO grande no slide 1 (80-120pt)
2. Um slide com foto full-bleed + texto overlay
3. Paleta com acento: 80% neutro + 20% cor de destaque em 1-2 slides
4. Tipografia hierárquica real: display + corpo, pesos diferentes

---

## Entrega (ambas as vias)

Mostre caminhos ou miniaturas dos arquivos. Pergunte:

> "Arte pronta. Quer ajustar algo ou libera pra publicar?"

Atualize o calendário: status → `arte-pronta`.
