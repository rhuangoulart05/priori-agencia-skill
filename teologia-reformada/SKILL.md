---
name: teologia-reformada
description: Monta a LITURGIA que o pastor/pregador vai conduzir sobre um texto bíblico. Use SEMPRE que o usuário pedir "liturgia", "monta uma liturgia", "liturgia sobre o texto X", "liturgia do Salmo/capítulo Y". NÃO escreve sermão nem transcreve o texto bíblico (o usuário lê da própria Bíblia) e NÃO escolhe hinos. Entrega duas coisas: (A) a CONTEXTUALIZAÇÃO do texto — contexto histórico, situação do autor, gênero, imagens, estrutura e analogias com outras passagens, explicada para o usuário entender — e (B) o ROTEIRO em dois momentos, com o que o usuário LÊ e o que ele FALA (roteiro em primeira pessoa, pronto para conduzir). ENTREGA FINAL EM PDF, com as partes que ele não pode deixar de falar destacadas em cor (amarelo).
---

# Teologia Reformada — Liturgia sobre um texto

## O que o usuário quer (leia isto e obedeça — já erramos aqui antes)

Quando ele pede "liturgia", ele **NÃO** quer um culto reformado completo com orações,
confissões, ofertas e bênção. Ele quer um material enxuto para **conduzir sobre um texto**:

1. **Contextualização do texto — para ELE entender.** Contexto histórico, situação do
   autor no momento em que escreveu, gênero, sentido das imagens, estrutura do texto e
   **analogias com outras passagens**. É estudo, explicado de forma clara.
2. **Roteiro em dois momentos** — o que ele **lê** e o que ele **fala** (as palavras dele,
   em primeira pessoa, prontas para falar).

### Regras inegociáveis
- **NÃO escrever o texto bíblico.** Ele lê da própria Bíblia. Você dá a referência.
- **NÃO escrever sermão.** Você dá a *fala* dele — comentário/contextualização falada, curta.
- **NÃO escolher hinos.** O hino é escolhido por eles. No roteiro, marque `→ HINO (vocês escolhem)`.
- **Você entrega o que ELE fala**, não um texto teológico impessoal. Roteiro em 1ª pessoa,
  linguagem falada, para ele ler/conduzir.

## A estrutura fixa dos dois momentos

Sempre a mesma. Não invente etapas.

| | O que acontece | Quem faz |
|---|---|---|
| **Momento 1 — Abertura** | Ele **lê um versículo** de abertura + faz um **comentário rápido** (~30s) | usuário lê + fala |
| **→ HINO** | Cântico de entrada | *vocês escolhem (não sugerir)* |
| **Momento 2 — Texto principal** | Ele **lê o texto-tema** (ex.: Salmo 1) + **fala sobre o texto**, usando a contextualização | usuário lê + fala |

O **texto principal do Momento 2** é o texto que o usuário deu. O **versículo do Momento 1**
é um versículo curto que "puxa" o tema do texto principal — sugira um, mas deixe claro que
ele pode trocar.

## O formato de entrega (sempre duas partes)

O output é **um arquivo em duas partes**:

- **PARTE A — Contexto (para você entender):** as seções de contextualização (ver checklist
  em `references/contexto-e-roteiro.md`). É onde vão o histórico, o autor, a estrutura e as
  analogias — explicados **para o usuário**, não para a congregação.
- **PARTE B — Roteiro do culto:** Momento 1 (versículo + fala) → HINO → Momento 2 (leitura +
  fala). A **fala** do Momento 2 destila a Parte A em linguagem falada, em 1ª pessoa.

Modelo completo e checklist em `references/contexto-e-roteiro.md`.

## Entrega final: PDF com destaques (padrão)

A entrega final é sempre um **PDF**, e **as partes que o usuário não pode deixar de falar vêm
destacadas com cor de fundo (amarelo)**. Destaque com parcimônia — só as frases-chave das
falas (e uns poucos fatos essenciais do contexto); se destacar tudo, nada se destaca.

Método (HTML → PDF, mantém o destaque colorido):
1. Escreva o conteúdo em **HTML** com CSS de impressão (A4), usando `<mark>` nas frases
   essenciais. Modelo de HTML/CSS: veja o exemplo em `assets/liturgia-template.html`.
2. Converta com **WeasyPrint**: `weasyprint entrada.html liturgias/AAAA-MM-DD-<tema>.pdf`
   (ou `python3 -c "import weasyprint; weasyprint.HTML('in.html').write_pdf('out.pdf')"`).
   Se o WeasyPrint faltar, `pip install weasyprint`. Alternativa: Chromium headless
   `--print-to-pdf`.
3. Salve o PDF em `liturgias/`, confira o render (1 página por vez) e **entregue o PDF ao usuário**.
Mantenha também o `.md` fonte no repositório para edições futuras.

## Como construir a contextualização (Parte A)

Cobrir, na medida em que o texto permite (não force o que não há):
1. **Onde o texto está** e sua função no livro.
2. **Autor e situação histórica** — quem escreveu (ou a leitura mais aceita, se anônimo) e em
   que circunstância. Seja honesto sobre incerteza (ex.: salmo sem título → dizer que é anônimo).
3. **Gênero** — narrativa, poesia, sabedoria, carta, profecia… muda o jeito de ler.
4. **Imagens e pano de fundo cultural** — o sentido concreto das figuras na época.
5. **Estrutura** — o "mapa" dos versículos (blocos e virada).
6. **Analogias com outros textos** — 3 a 5 passagens que iluminam o texto (ecos verbais,
   temas gêmeos, cumprimento no NT).
7. **Leitura em Cristo** — como o texto aponta para o evangelho (chave reformada).

## Precisão (importante)
- **Não invente** autoria, data ou fato histórico. Se a datação/autoria é discutida, diga
  isso e apresente a leitura majoritária.
- **Não invente** número de versículo nem cita errado. Confira as referências.
- Mantenha a teologia **reformada** (soberania de Deus, graça, Cristo no centro), mas o foco
  é servir a exposição do texto, não empurrar jargão.

## Primeiro passo quando o usuário invocar
1. **Qual o texto?** (o texto-tema do Momento 2). Se não veio, pergunte só isso.
2. **Versículo de abertura:** ele já tem um, ou quer que eu sugira? (sugira um coerente).
3. Monte **Parte A (contexto)** + **Parte B (roteiro)**, salve o `.md` fonte em
   `liturgias/AAAA-MM-DD-<tema>.md` e **gere o PDF com destaques** em
   `liturgias/AAAA-MM-DD-<tema>.pdf` (ver "Entrega final: PDF com destaques").
4. **Entregue o PDF** ao usuário e **pare para aprovação**.

## O que a skill NÃO faz
- Não escreve sermão, não transcreve o texto bíblico, não escolhe hinos.
- Não monta culto reformado completo (orações, confissões, ofertas, Ceia, bênção) — a menos
  que o usuário peça explicitamente por "culto completo".
