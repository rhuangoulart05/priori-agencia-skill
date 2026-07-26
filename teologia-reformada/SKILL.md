---
name: teologia-reformada
description: Sistema de produção de liturgias para o culto reformado. Use SEMPRE que o usuário pedir para criar/montar uma liturgia, ordem de culto, "culto de domingo", "liturgia de domingo", liturgia de Ceia, liturgia de Natal/Páscoa/Reforma, ou pedir oração de adoração/confissão/iluminação/pastoral, leitura responsiva, confissão de fé, ou bênção apostólica. Monta o culto seguindo o princípio dialógico (Deus chama, o povo responde) e o princípio regulador do culto, ancorando cada elemento na Escritura e nas confissões reformadas (Westminster, Heidelberg, Belga, Dort). Padrão IPB/presbiteriano com hinário Novo Cântico + Saltério, mas parametrizável por tradição reformada.
---

# Teologia Reformada — Produção de Liturgia para o Culto

## O que essa skill resolve

Montar a **ordem do culto** (liturgia) de um domingo (ou data especial) demanda tempo
e cuidado teológico: cada elemento precisa de base bíblica, os textos precisam
conversar entre si, as orações não podem ser genéricas e a estrutura precisa
respeitar a tradição reformada. Essa skill entrega a liturgia **90% pronta** —
estruturada, ancorada na Escritura e nas confissões — para o pastor/presbítero
revisar, ajustar a pregação e aprovar.

Ela **não** substitui o ministro: o sermão, a escolha final dos hinos e as decisões
pastorais são dele. A skill prepara o andaime e preenche o que é repetível.

## Dois princípios inegociáveis (a skill obedece sempre)

1. **Princípio regulador do culto (RPW)** — só entra na liturgia o que a Escritura
   ordena ou autoriza por bom e necessário consequente. Nada de elemento "porque é
   bonito". Ref.: Confissão de Fé de Westminster (CFW) XXI.1.

2. **Princípio dialógico** — o culto é diálogo de aliança: **Deus fala, o povo responde.**
   - *Deus fala:* chamado à adoração, lei, garantia do perdão, leitura e pregação da
     Palavra, sacramentos, bênção.
   - *O povo responde:* louvor, confissão de pecados, confissão de fé, orações,
     ofertas, votos.
   Toda liturgia gerada deve deixar claro **quem está falando** em cada momento.

## Estrutura canônica (4 movimentos)

A skill organiza o culto em quatro movimentos. Detalhe de cada elemento, propósito,
base bíblica e exemplos em `references/estrutura-liturgica.md`.

| Movimento | O que acontece | Quem fala |
|---|---|---|
| **1. Preparação / Adoração** | Chamado à adoração, invocação, cântico de adoração | Deus chama → povo louva |
| **2. Contrição** | Lei de Deus, confissão de pecados, garantia do perdão | Deus convence → povo confessa → Deus perdoa |
| **3. Edificação / Consagração** | Confissão de fé, oração pastoral, ofertas, oração de iluminação, **duas leituras** (a 2ª é a principal) | povo professa → Deus fala na Palavra |
| **4. Comunhão / Despedida** | **Louvor de resposta**, **Santa Ceia** (quando há), **bênção apostólica** | povo responde → Deus envia e abençoa |

> **Formato padrão deste usuário: culto SEM pregação.** A Palavra é ministrada por **duas
> leituras**; a **segunda é a principal** (o texto-tema do culto) e vem **logo antes do
> louvor de resposta**. A skill **não escreve sermão** e não inclui item de pregação,
> salvo pedido explícito.

## Mental model — por que é estruturada assim

1. **Diálogo, não programa** — a ordem não é uma lista de "atrações"; é a lógica da
   aliança. Por isso cada elemento é rotulado com *Deus fala* ou *povo responde*.

2. **Tudo ancorado** — todo chamado, garantia de perdão e bênção é **texto bíblico
   citado** (não paráfrase solta). Confissão de fé vem de um símbolo reformado real.
   Ver princípios anti-genérico abaixo.

3. **Coerência temática** — chamado, salmo, hinos, confissão e leituras devem
   convergir com o **texto da pregação**. A skill pede o texto/tema do sermão *antes*
   de montar, e escolhe os demais elementos para conversar com ele.

4. **Confessionalismo como repertório** — Westminster (Confissão, Catecismo Maior e
   Breve), Catecismo de Heidelberg, Confissão Belga e Cânones de Dort são fonte de
   leituras responsivas e confissões de fé. Catálogo em
   `references/confissoes-e-catecismos.md`.

5. **Parametrizável por tradição** — padrão é IPB (Westminster + Novo Cântico), mas
   suporta outras igrejas reformadas/presbiterianas. Pergunte a tradição se não for óbvia.

## Princípios anti-genérico (todo output passa por esses filtros)

1. **Sem oração-clichê** — nada de "Senhor, te agradecemos por mais um dia". Orações
   carregam conteúdo bíblico-teológico concreto (atributo de Deus, ato redentor, promessa).
2. **Chamado e garantia são Escritura citada** — com referência (livro, cap., verso).
3. **Confissão de fé é símbolo real** — Credo Apostólico, Niceno, ou pergunta/resposta
   de catecismo, transcrita corretamente.
4. **Coerência com o texto-tema** — se a leitura principal é sobre graça, o culto inteiro respira graça.
5. **Hinos por tema, não por hábito** — escolha pelo conteúdo doutrinário que serve ao
   movimento (adoração ≠ gratidão ≠ consagração). Cite por título; confirme o número no
   hinário local (não invente número de hino).

## Primeiro passo quando o usuário invocar

Antes de montar, confirme (pergunte só o que faltar):

1. **Tradição/igreja** — IPB? Outra presbiteriana/reformada? (padrão: IPB)
2. **Data e ocasião** — domingo comum? Ceia? Data especial (Reforma, Natal, Páscoa, Pentecostes)?
3. **Texto-tema (leitura principal)** — qual passagem? É a **segunda leitura**, lida antes
   do louvor, e define a coerência de todo o culto. *(Padrão sem pregação; peça o texto da
   1ª leitura complementar ou proponha um coerente.)*
4. **Tem Santa Ceia?** — se sim, inclui o movimento sacramental (instituição, convite, oração).
5. **Hinário** — Novo Cântico? Saltério? Outro?

Com isso, leia `references/estrutura-liturgica.md` e monte. Para orações e seleção de
hinos/salmos, use `references/oracoes-e-hinos.md`. Para confissões/catecismos, use
`references/confissoes-e-catecismos.md`.

## Onde salvar o output

A liturgia final vai em `liturgias/AAAA-MM-DD-<ocasiao>.md` (ex:
`liturgias/2026-06-28-domingo.md`), pronta para impressão/projeção. Mostre ao usuário
e **pare para aprovação** antes de considerar concluído.

## O que a skill NÃO faz

- **Não inclui pregação/sermão** (formato padrão). A ministração da Palavra são as duas
  leituras. Só monta pregação se o usuário pedir explicitamente.
- Não inventa número de hino nem texto de confissão — se não tiver certeza, cita por
  título/referência e marca para conferência.
- Não impõe calendário litúrgico onde a igreja não observa; pergunta antes.
