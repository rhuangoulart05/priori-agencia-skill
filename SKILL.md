---
name: agencia
description: Sistema completo de produção de conteúdo para agência de marketing com múltiplos clientes. Use SEMPRE que o usuário pedir para planejar conteúdo (semana, quinzena ou mês inteiro), produzir post, criar carrossel, criar arte, gerar legenda ou roteiro de vídeo para qualquer cliente da agência (Lupa Gestão, Contabilizei, G4, Jhon Deere, Lorena, Mobs, Samsung, Thales Laray, Thiago Concer e outros). Também dispara quando o usuário mencionar "pauta", "calendário editorial", "planejar o mês", "conteúdo da semana", "arte do post", "carrossel", ou citar qualquer cliente por nome. Orquestra três fluxos: planejar-conteúdo (pauta via pesquisa + calendário setorial, em qualquer período), produzir (copy + roteiro + brief visual) e criar-arte (Canva MCP + Nano Banana). Herda tom e guardrails por nicho (contabilidade, saúde-estética, b2b-técnico, info-produto).
---

# Agência — Produção de Conteúdo para Clientes

## O que essa skill resolve

O Rhuan toca uma agência com ~7 clientes de nichos variados, produzindo 2-4 posts/semana cada + vídeos. A dor é volume × qualidade simultâneos. Essa skill é um **amplificador**: entrega 90% pronto, ele revisa e aprova.

Três fluxos. Nunca misture.

| Fluxo | Quando usar | Reference |
|---|---|---|
| **Planejar conteúdo** | "planejar semana/quinzena/mês de X", "pautas da semana", "calendário editorial do mês", "conteúdo de abril" | `references/planejar-conteudo.md` |
| **Produzir pauta** | "produzir post X", "escrever carrossel Y", "roteiro de vídeo Z" | `references/produzir-pauta.md` |
| **Criar arte** | "fazer a arte", "gerar carrossel visual", "montar no Canva" | `references/criar-arte.md` |

**Planejar conteúdo suporta 3 modos:** semana (2–4 pautas, padrão), quinzena (4–8) ou mês (8–16, agrupadas por semana). Se o usuário não especificar, pergunte. Detalhes em `references/planejar-conteudo.md`.

## Mental model — por que a skill é estruturada assim

1. **Separação por fluxo** — planejamento, copy e arte são competências distintas. Um prompt grandão degrada todas. Cada fluxo lê só o que precisa.

2. **Herança por nicho** — um cliente de contabilidade herda calendário fiscal, pilares e tom do template `nichos/contabilidade/`, e sobrescreve o que é próprio dele em `clientes/<cliente>/`. Novo cliente no mesmo nicho = 30min, não do zero.

3. **Compliance embutido por nicho** — saúde não promete resultado, contabilidade cita legislação correta, agro fala specs. Os guardrails são parte do nicho, não do cliente.

4. **Memória do que foi publicado** — `clientes/<cliente>/ja-publicado/` é consultado antes de propor pauta, pra não repetir e pra aprender o que performou.

5. **Dupla via visual** — Para Instagram 1080×1350 (formato principal dos clientes): **G4 Editorial** (belt + Gemini para backgrounds IA + Pillow para composição tipográfica). Para outros formatos (LinkedIn, Stories, etc.): **Canva MCP** + Nano Banana para imagem de apoio. O G4 Editorial foi validado com a Lupa Gestão (abr/2026) — safe zone 200/880, gradiente 0.42, sem linhas separadoras, blur em calendários. Detalhes completos em `references/criar-arte.md`.

## Achar a raiz do workspace (crítico)

Todos os caminhos abaixo são **relativos à raiz do workspace** — a pasta onde vivem `nichos/`, `clientes/` e as pastas de `Referencias visuais...`. Essa raiz **não é** necessariamente o working directory atual do shell; é a pasta-mãe onde estão os arquivos da agência.

Regra de descoberta (faça na ordem, para na primeira que funcionar):

1. Procure `nichos/` e `clientes/` a partir do CWD subindo níveis com `Glob` (pattern `**/nichos/` e `**/clientes/`). Se achar ambos no mesmo parent, **esse é o workspace**.
2. Caso ainda não tenha achado, tente o path canônico: `/Users/rhuancarlos/Documents/PROJETOS/Rhuan/`.
3. Sempre que ler um arquivo do cliente ou do nicho, use o caminho **absoluto** (ex: `/Users/rhuancarlos/Documents/PROJETOS/Rhuan/clientes/lupa-gestao/brand.md`), não o relativo. Isso previne o bug do eval onde o agent não achou os arquivos porque o CWD estava em outro lugar.

Se a raiz não existe ou está incompleta (falta `clientes/<cliente>/brand.md` etc), **pare e avise** — não invente conteúdo pra cliente desconhecido.

## Arquitetura de arquivos

```
<working-dir>/
├── nichos/                        # Templates herdáveis por categoria
│   ├── contabilidade/
│   │   ├── pilares-padrao.md      # Temas base (fiscal, gestão, autoridade)
│   │   ├── calendario-fiscal.md   # Datas-chave do ano
│   │   └── tom-guardrails.md      # Tom de voz + CFC + o que pode/não pode
│   ├── saude-estetica/
│   ├── b2b-tecnico/
│   └── info-produto/
│
├── clientes/
│   └── <cliente>/
│       ├── brand.md               # Nicho herdado, cores, tipografia, posicionamento
│       ├── icp.md                 # Público-alvo, dores, linguagem deles
│       ├── pilares.md             # Pilares próprios (sobrescreve/acrescenta ao nicho)
│       ├── logos/                 # Arquivos de logo (PNG/SVG)
│       ├── ja-publicado/          # Posts passados + performance
│       ├── calendario/            # Pautas do mês (YYYY-MM.md)
│       └── artes-geradas/         # Outputs finais
│
└── Referencias visuais para posts:carrosseis/   # Moodboards por marca (existente)
    ├── Contabilizei/              # Ref visual Lupa Gestão (nicho próximo)
    ├── G4/
    └── ...
```

## Princípios anti-genérico

Todo output passa por esses filtros. Se falhar, refaça.

1. **Hook específico** — nada de "Você sabia que..." ou "3 dicas para...". Hook deve carregar dado, número, data, regra ou contradição.
2. **Ancoragem em fato** — sempre citar legislação, procedimento, spec, data ou fonte real. Para contabilidade: IN, LC, data de vencimento, portaria. Para saúde: estudo, protocolo, limite legal.
3. **Voz do ICP** — usar vocabulário que o cliente do cliente usa. Se o ICP fala "faturamento", não escreva "receita bruta" só porque é mais técnico.
4. **Nada de filler visual** — toda arte tem um motivo de existir (dado, pessoa, contraste, metáfora concreta). Imagem decorativa genérica é reprovada.
5. **CTA único e claro** — um CTA por post. Nada de "segue a gente, comenta e compartilha" junto.

## Como o usuário aprova

**Ele aprova tudo.** Cada fluxo gera um output em markdown que ele revisa antes do próximo passo:

- `planejar-conteudo` → `clientes/<cliente>/calendario/YYYY-MM.md` (pautas propostas, agrupadas por semana se for quinzena/mês)
- `produzir-pauta` → arquivo por pauta: `calendario/YYYY-MM-dd-<slug>.md` (copy + roteiro)
- `criar-arte` → arquivos finais em `clientes/<cliente>/artes-geradas/`

Entre cada etapa, **pare e mostre**. Não vá pro próximo passo sem aprovação explícita.

## Como identificar o cliente e o nicho

Quando o usuário mencionar um nome (ex: "Lupa Gestão"):

1. Normalize: lowercase, sem acento, troca espaço por hífen → `lupa-gestao`
2. Leia `clientes/lupa-gestao/brand.md` — primeira linha do frontmatter diz o nicho
3. Leia os arquivos do nicho correspondente em `nichos/<nicho>/`
4. Agora você tem contexto pra executar o fluxo

Se o cliente não existe ainda: use o skill-creator interno pra onboarding (ver `references/onboarding-cliente.md`).

## Sobre o G4 Editorial (Instagram 1080×1350)

Via principal para Instagram. Usa `belt app run google/gemini-2-5-flash-image` para gerar backgrounds editoriais (estilo capa de revista) e Pillow para compor tipografia sobre a foto com gradiente e safe zone. Regras inegociáveis: `start_y_pct=0.42`, sem `d.line()`, `th()` usando `bb[3]`, blur em calendários/datas, logo discreta só no slide 1. Ver `references/criar-arte.md`.

## Sobre o Canva MCP

O Canva MCP está disponível (tools com prefixo `mcp__0e0417f3...__*`). **Use para formatos além do Instagram** (LinkedIn, Stories, banners, etc.) e para carrosseis onde o texto domina sobre a imagem.

- `list-brand-kits` — pega brand kit do cliente
- `generate-design-structured` — gera carrossel/post com estrutura
- `perform-editing-operations` — edita texto/imagem em design existente
- `upload-asset-from-url` — sobe imagem do Nano Banana pro Canva
- `export-design` — exporta PNG/PDF final

Fluxo canônico em `references/criar-arte.md`.

## Sobre o Nano Banana / ai-image-generation

Use a skill `ai-image-generation` (já disponível). Nano Banana é ideal para:
- Gerar imagem de apoio única (hero do post/slide 1 do carrossel)
- Compor logo do cliente com cenário/produto
- Editar imagem (remover fundo, trocar contexto)

**Não use** pra gerar carrossel inteiro em uma imagem só — o texto vira ilegível. Use pra gerar UMA imagem e compor no Canva.

## Sobre pesquisa de pauta

Use `mcp__perplexity__perplexity_research` para:
- Novidades regulatórias do nicho (últimos 30 dias)
- Tendências setoriais
- Datas comemorativas filtradas pelo nicho

Sempre peça citação de fontes. Pautas precisam ser **ancoradas** em algo real.

## Primeiro passo quando o usuário invocar

1. Identifique o fluxo (planejar, produzir, criar-arte) pela intenção dele
2. Leia a reference correspondente
3. Identifique o cliente e carregue `brand.md` + nicho
4. Execute

Se o usuário for vago ("cria um post"), pergunte: **qual cliente, qual formato (post único/carrossel/reels), e tem pauta específica ou gera nova?**
