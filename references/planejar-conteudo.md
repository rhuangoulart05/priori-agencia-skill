# Fluxo: Planejar Conteúdo

Gera o calendário editorial para UM cliente específico, no período pedido — **semana, quinzena ou mês inteiro**. Rhuan aprova as pautas em bloco, depois cada uma vai pra `produzir-pauta`.

## Modos de planejamento

| Modo | Volume típico | Quando usar |
|---|---|---|
| **Semana** | 2–4 pautas | Padrão. Mantém o feed adaptativo a notícias da semana. |
| **Quinzena** | 4–8 pautas | Quando Rhuan quer planejar 2 semanas de uma vez e o nicho está estável. |
| **Mês** | 8–16 pautas | Lote grande no início do mês — ideal quando calendário fiscal é o eixo dominante (ex: abril IRPF, março DEFIS, outubro Outubro Rosa). |

**Regra que muda por modo:**
- **Semana:** 1 único bloco linear de pautas.
- **Quinzena / Mês:** **agrupe por semana** dentro do markdown (H2 "Semana 1 — DD/MM a DD/MM", etc.). Cada semana segue o mix de pilares do cliente. Isso mantém a rotação saudável (veja `pilares.md` do cliente) e evita dar 4 Autoridade Fiscal seguidas só porque o mês tem muita data.
- **Mês:** a pesquisa Perplexity pode ficar mais antiga até a semana 3–4 — marque cada pauta com **confiança** (alta / revisar-na-semana), pra Rhuan saber o que re-checar.

## Input esperado

- Cliente (ex: "Lupa Gestão")
- Período — se não especificado, pergunte: "semana, quinzena ou mês?"
- Quantidade de pautas — padrão vem de `clientes/<cliente>/brand.md` → `posts_por_semana`. Multiplique por nº de semanas do período.

## Passo a passo

### 1. Contexto do cliente

Leia, nessa ordem (use caminhos **absolutos a partir da raiz do workspace** — veja "Achar a raiz do workspace" no SKILL.md):

1. `<workspace>/clientes/<cliente>/brand.md` — identifica o **nicho** e posicionamento
2. `<workspace>/nichos/<nicho>/pilares-padrao.md` — pilares herdados
3. `<workspace>/nichos/<nicho>/calendario-fiscal.md` (ou equivalente) — datas do período
4. `<workspace>/nichos/<nicho>/tom-guardrails.md` — regras de tom e compliance
5. `<workspace>/clientes/<cliente>/pilares.md` — pilares próprios (sobrescreve/acrescenta)
6. `<workspace>/clientes/<cliente>/icp.md` — público-alvo
7. **Últimos 10–15 posts publicados** em `<workspace>/clientes/<cliente>/ja-publicado/` — o que já foi falado e o que performou

**Se `ja-publicado/` estiver vazio** (primeiro mês do cliente), pule o passo 5 abaixo e siga a rotação de pilares do `pilares.md` direto.

### 2. Pesquisa de contexto atual

Use `mcp__perplexity__perplexity_research` (ou `_search` se for só cross-check rápido) com prompt estruturado:

```
Pesquise, nos últimos 30 dias, novidades relevantes para [NICHO] que interessam a [ICP]:
1. Mudanças regulatórias, portarias, instruções normativas
2. Tendências de mercado do setor
3. Datas importantes no período [DATA_INICIO]–[DATA_FIM]
4. Discussões correntes (fóruns, LinkedIn, mídia especializada)

Retorne com data, fonte e link de cada item.
```

**Para contabilidade:** cruze com `nichos/contabilidade/calendario-fiscal.md` — datas de vencimento são pauta automática. Sempre **confirme a data de vencimento na fonte oficial** (gov.br, Receita Federal) antes de usar no hook — o eval mostrou que prazos podem ter diferença de 1 dia do que está no briefing.

**Para saúde-estética:** filtre Outubro Rosa, Novembro Azul, Dia Mundial do X.

### 3. Seleção e rotação de pautas

Respeite a **rotação do `pilares.md` do cliente**. Se o cliente tem ciclo de 4 semanas (como a Lupa), olhe em que semana do ciclo está a próxima publicação e use o mix previsto.

Regra de ouro: **nunca 2 pautas consecutivas no mesmo pilar**, mesmo se o período for muito específico (ex: abril com 5 datas fiscais). Intercale com um pilar leve (Dicas Práticas, Bastidor).

**Feriado / data não-útil:** se o dia de postagem cai em feriado nacional sem ângulo editorial do nicho, desloque pro dia útil anterior ou posterior. Documente o desvio ("Originalmente 01/05, deslocado pra 03/05 por ser feriado").

### 4. Proposta estruturada

Crie/atualize o arquivo `<workspace>/clientes/<cliente>/calendario/YYYY-MM.md`.

**Para modo SEMANA** — 1 H1, pautas em H2 direto.

**Para modo QUINZENA / MÊS** — 1 H1 com o mês, 1 H2 por semana ("Semana 1 — 01/MM a 07/MM"), pautas em H3.

Formato por pauta:

```markdown
## [Data] — [Slug curto]

- **Tipo:** autoridade | dor-icp | educativa | data-especial | dicas-praticas | bastidor | calendario-fiscal
- **Formato:** post único | carrossel 5 slides | carrossel 10 slides | reels | linkedin-artigo
- **Pilar:** [nome LITERAL do pilar, copiado de pilares.md do cliente]
- **Hook candidato:** [primeira frase forte, com dado/fato]
- **Ângulo:** [1–2 linhas explicando o ângulo não-óbvio]
- **Ancoragem:** [LC 123/2006 art. 13 | estudo X | portaria Y] — com fonte verificada
- **CTA:** [chamada única]
- **Fonte da pesquisa:** [link/referência consultada]
- **Por que agora:** [conexão com o momento]
- **Confiança** (só modo mês): alta | revisar-na-semana
- **Status:** proposta
```

**Regra de nomenclatura dos pilares:** use o nome **EXATO** como aparece em `pilares.md` do cliente (ex: "Dicas Práticas / Descomplica", não "Educativo"). O eval mostrou que inventar nomes de pilar é o erro mais comum do baseline.

### 5. Anti-repetição (se tem histórico em ja-publicado/)

Antes de finalizar, compare cada pauta proposta com os últimos 30 posts em `ja-publicado/`. Se o ângulo é muito parecido, refaça.

Critério: se mais de 2 bullets principais coincidem com um post recente, é repetição.

### 6. Entrega e aprovação

Imprima o calendário pro usuário em formato legível. Pergunte:

> "Revisei as pautas. Me diz: quais aprovam, quais querem repitching, e se alguma pauta precisa ser adicionada? Quando confirmar, parto pra produção."

**Não comece a produzir** sem aprovação explícita.

## Heurísticas para pauta forte (checklist)

- [ ] Hook tem número, data, regra ou contradição
- [ ] Há uma ancoragem factual (fonte ou legislação) **verificada**, não da memória
- [ ] Não repete ângulo dos últimos 30 dias
- [ ] Pilar está claro e usa nome literal do `pilares.md`
- [ ] CTA é único e acionável
- [ ] Ângulo é não-óbvio (um concorrente postaria igual? então refaça)
- [ ] Se é mês/quinzena: rotação respeitada, não tem 2 pautas do mesmo pilar em sequência

## Quando pesquisar mais fundo

Se o nicho tem movimento intenso (contabilidade — sempre tem) ou o cliente pediu pauta sobre evento recente: use `perplexity_research` em vez de `perplexity_ask`. Demora 60s+ mas retorna material muito melhor.

## Pegadinhas aprendidas no eval

- **Data oficial ≠ briefing:** o briefing de IRPF dizia 30/05, Receita dizia 29/05. Sempre confira com fonte oficial antes de colocar a data no hook.
- **Ângulo precisa casar com ICP real:** "IRPF para PME" é armadilha — IRPF é PF. O ângulo correto é "sócio-dono da PME, como PF, precisa declarar por causa de pró-labore / distribuição de lucros". Quando a pauta original não casa com o ICP, faça **reframe** antes de produzir, não force.
