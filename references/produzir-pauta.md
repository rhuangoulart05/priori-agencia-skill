# Fluxo: Produzir Pauta

Dada UMA pauta aprovada em `clientes/<cliente>/calendario/YYYY-MM.md`, produz o pacote completo: copy + (se aplicável) roteiro de carrossel + (se aplicável) roteiro de vídeo + brief visual pra próxima etapa.

## Input esperado

- Cliente
- Slug da pauta (ex: `simples-nacional-limite-2026`)
- Formato (se não especificado, usa o definido no calendário)

## Regras inegociáveis (aprendidas no eval)

Antes de qualquer coisa, fixe essas 3 regras — elas são a diferença entre "output da Lupa" e "output genérico":

1. **Paleta literal do brand.md.** Copie os HEX exatos (ex: Lupa = `#2C111F` + `#FBF2AD`). **Não invente** marinho, azul corporativo, dourado, amarelo-mostarda. Se o `brand.md` define 2 cores, use essas 2. Se precisa de terceira cor de apoio, tira do moodboard em `Referencias visuais para posts:carrosseis/<marca>/`, nunca inventa.
2. **Nome literal do pilar.** Copie do `pilares.md` do cliente (ex: "Dicas Práticas / Descomplica", não "Educativo"). Pilar "inventado" é sinal de que não leu o arquivo.
3. **Dado verificado, não lembrado.** Toda data, número, legislação que aparece no copy **tem que vir de uma chamada Perplexity ou leitura de fonte oficial na mesma sessão** — não da memória. Anote a fonte no final do arquivo.

## Passo a passo

### 1. Carregue contexto

- `<workspace>/clientes/<cliente>/brand.md`, `pilares.md`, `icp.md`
- `<workspace>/nichos/<nicho>/tom-guardrails.md` — **crítico** pra evitar quebra de compliance
- A pauta específica no calendário
- Use `copywriting` skill em paralelo se quiser refinar o copy depois

### 2. Validação de ângulo (passo 0 de reframe)

Antes de escrever, bata a pauta contra o ICP do cliente:

- **O ângulo faz sentido pro público real?** Exemplo: "IRPF para PME" não casa — IRPF é PF. O ângulo correto vira "sócio-dono da PME, como PF, precisa declarar IRPF por causa de pró-labore / distribuição de lucros".
- **Se o briefing original está tecnicamente errado, reframe ANTES de produzir** e deixe nota explícita no topo do output pro Rhuan validar. Produzir algo tecnicamente errado pra "seguir o briefing" é pior que pausar e reframe.
- **Se o ângulo está ok, segue direto pro passo 3.**

### 3. Expanda a pesquisa da pauta

A pauta já veio com ancoragem, mas antes de escrever use `perplexity_search` ou `perplexity_ask` pra:
- Confirmar dado/legislação citada (não confie na memória)
- Pegar 1-2 exemplos concretos pra usar no texto
- Conferir se nada mudou depois da pauta ser gerada
- **Confirmar datas específicas em fonte oficial** (ex: Receita Federal, gov.br) — não reuse a data do briefing sem validar

### 4. Produza por formato

#### Formato: POST ÚNICO (estático)

Gere:
- **Headline** (texto grande da arte): max 8 palavras, impacto
- **Sub-headline** (opcional): 1 linha de contexto
- **Legenda**:
  - Linha 1 (hook): copia/adapta o hook da pauta
  - 2-4 parágrafos curtos (2-4 linhas cada) — desenvolvimento
  - CTA final único
  - Hashtags: 5-8, mix de nicho (3-4 específicas) + geral (2-4)
- **Brief visual** (vai pra `criar-arte`): direção visual em 3-5 bullets

#### Formato: CARROSSEL

Antes de escrever, defina arco narrativo:
1. **Slide 1 — Hook**: pergunta, dado chocante ou afirmação contra-intuitiva. Zero enrolação.
2. **Slide 2 — Promessa/Problema**: por que o leitor deve continuar
3. **Slides 3 a N-2 — Desenvolvimento**: um conceito por slide. Sem misturar.
4. **Slide N-1 — Síntese/ação**: o que fazer com isso
5. **Slide N — CTA**: único, direto. Pode ter também "salve pra consultar depois".

Para cada slide gere:
```markdown
### Slide X

- **Headline:** (max 8 palavras)
- **Sub-texto** (se couber, max 15 palavras)
- **Elemento visual central:** (dado, ícone, foto, ilustração)
- **Notas pro designer:** (o que precisa dar destaque)
```

Escreva a **legenda** separada — 3-6 linhas. Ela vende o carrossel: hook, promessa, CTA "arrasta pro lado" ou "salva pra consultar".

#### Formato: REELS / VÍDEO CURTO

Gere roteiro:
```markdown
### Roteiro vídeo — [slug]

- **Duração alvo:** 30-45s (Instagram) ou 60-90s (LinkedIn)
- **Gancho (0-3s):** (primeira frase, enquadramento, cenário)
- **Desenvolvimento (3-30s):** bullets do que falar, em ordem
- **CTA (últimos 3-5s):**
- **Legenda do reels:** (texto do post)
- **Texto on-screen (se aplicável):** ponto a ponto com timestamps aproximados
- **Notas de gravação:** (ambiente, figurino, props, b-roll se precisar)
```

**Pra vídeo, sempre inclua notas de gravação.** O Rhuan grava tudo em batch, as notas economizam tempo dele no dia da gravação.

### 5. Aplicar guardrails do nicho

Antes de entregar, rode mental checklist do `nichos/<nicho>/tom-guardrails.md`. Exemplos:

- **Contabilidade:** não dê conselho fiscal individual — sempre "consulte seu contador"/"consulte a Lupa"
- **Saúde-estética:** não prometa resultado, não use linguagem alarmista, sem "antes e depois" sem consentimento
- **B2B técnico:** não afirme compatibilidade de peça sem fonte oficial

### 6. Brief visual pra próxima etapa

Todo output termina com um **Brief Visual** estruturado, pra `criar-arte`:

```markdown
## Brief Visual

- **Formato final:** post 1080x1350 | carrossel 1080x1350 × N | reels cover
- **Tom visual:** (sério | clean | vibrante | técnico | orgânico)
- **Cor dominante:** HEX literal do brand.md (ex: `#2C111F` + `#FBF2AD` pra Lupa — não descreva como "vinho + champagne", cole os HEX)
- **Elementos essenciais:** logo, headline, [dado específico], CTA
- **Imagem de apoio necessária:** (descrição pra Nano Banana) OR (não precisa, só texto)
- **Inspiração do moodboard:** (referência arquivos em "Referencias visuais para posts:carrosseis/<marca>/")
- **Anti-padrão:** (o que NÃO queremos — ex: "stock photo genérica de reunião")
```

### 7. Salvar

Crie/atualize: `<workspace>/clientes/<cliente>/calendario/YYYY-MM-DD-<slug>.md` com todo o pacote acima.

Atualize o `calendario/YYYY-MM.md` mudando status da pauta de `proposta` para `copy-pronto`.

### 8. Entrega

Mostre pro usuário. Pergunte:

> "Aqui está a pauta completa. Me diz: manda direto pra arte ou quer ajustar texto antes?"

## Qualidade — checklist final

- [ ] Hook específico (dado/data/regra/contradição)
- [ ] Ancoragem factual concreta, verificada
- [ ] Tom coerente com `brand.md`
- [ ] Zero quebra de guardrail do nicho
- [ ] CTA único
- [ ] Linguagem do ICP (não do cliente)
- [ ] Brief visual permite próxima etapa sem voltar

## Anti-padrões comuns

1. "7 dicas para X" — raramente tem ângulo próprio. Prefira "A dica de X que quase ninguém fala", se tiver substância.
2. Texto "de consultoria" que não aponta nada específico ("É importante estar atento...").
3. CTA vago ("me segue pra mais conteúdo!"). Prefira "salva esse post pra quando fechar o mês" ou "comenta ABC se já passou por isso".
4. Hashtag genérica demais (#marketing #negocios) sem as 3-4 específicas do nicho.
