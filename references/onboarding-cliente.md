# Fluxo: Onboarding de Cliente Novo

Quando o Rhuan disser "vamos cadastrar o cliente X" ou pedir pra gerar conteúdo pra um cliente que ainda não existe na pasta `clientes/`.

## Passo a passo

### 1. Descobrir o nicho

Pergunte: "Em qual nicho esse cliente se encaixa? Pode ser um dos existentes ou me descreva o negócio e eu crio um template novo."

Nichos já prontos (herdáveis imediatamente):
- `contabilidade` — escritórios contábeis, compliance CFC
- `saude-estetica` — clínicas, estética, compliance CFM/CRO
- `b2b-tecnico` — produto físico/técnico, agro, B2B
- `info-produto` — mentor, consultor, criador de conteúdo

**Se o cliente não se encaixa em nenhum dos acima**, peça ao usuário que descreva:
- O que o cliente vende / faz
- Para quem (perfil do cliente final)
- Se existe alguma restrição legal ou regulatória no setor
- O tom que o cliente usa (formal, descontraído, técnico, inspiracional)

Com essa descrição, crie automaticamente `nichos/<novo-nicho>/` com os 3 arquivos obrigatórios baseados no que foi informado. Não precisa esperar — gere o template na hora e confirme com o usuário antes de usar.

### 2. Criar a pasta do cliente

Slug: lowercase, sem acento, espaços viram hífen. Ex: "Lupa Gestão" → `lupa-gestao`.

```
clientes/<slug>/
├── brand.md          # copia do template
├── icp.md            # copia do template
├── pilares.md        # copia do template
├── logos/
├── ja-publicado/
├── calendario/
└── artes-geradas/
```

Use os templates da Lupa Gestão como ponto de partida (`clientes/lupa-gestao/*.md`) — eles já são genéricos o suficiente.

### 3. Preenchimento mínimo pra destravar

Pra começar a gerar pautas e conteúdo, preciso no mínimo:

**brand.md:**
- Posicionamento (1 frase)
- 3 diferenciais
- Cores (HEX)
- Tom de voz (3 bullets como E como NÃO)

**icp.md:**
- Perfil (porte, segmento, regime)
- 3-5 dores principais
- Vocabulário do ICP (4-5 termos)

**pilares.md:**
- Pode começar com os herdados do nicho e ajustar depois

**Logo:** pelo menos uma versão PNG transparent na pasta `logos/`.

### 4. Moodboard

Pergunte se já existe pasta em `Referencias visuais para posts:carrosseis/<Nome>/`. Se não, crie e peça 5-10 imagens de referência.

### 5. Confirmar e seguir

Quando o mínimo estiver preenchido, confirme com o Rhuan:

> "Setup da [cliente] pronto. Já posso planejar a primeira semana de pautas. Quer que eu comece agora?"

## Importante

**Não force o Rhuan a preencher tudo.** Setup pode ser incremental — começa com o mínimo, a cada ciclo de conteúdo refina. O brand kit fica mais rico com o tempo.
