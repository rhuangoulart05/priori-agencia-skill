# Catálogo de Nichos

Mapa dos templates de nicho disponíveis e como escolher.

## Nichos ativos

### contabilidade
Contabilidades em geral, incluindo nichadas (para salão, saúde, restaurante, etc.).
- Pilares: autoridade fiscal, dor operacional, gestão, calendário fiscal, bastidor
- Compliance: CFC — sem conselho individual, sem promessa de economia específica
- Calendário fiscal é fonte recorrente de pauta

**Clientes Lupa Gestão, contabilidades do Rhuan se encaixam aqui.**

### saude-estetica
Clínicas, dentistas, médicos estéticos, transplante capilar, tratamentos.
- Pilares: educação sobre procedimento, desmistificação, bastidor, resultados (com consentimento)
- Compliance: CFM/CRO/CFF — **sem promessa de resultado**, sem alarmismo, cuidado com antes/depois

**Cliente Lorena (transplante), dentista de implantes se encaixam aqui.**

### b2b-tecnico
B2B com produto físico ou técnico (peças, equipamentos, máquinas).
- Pilares: specs, compatibilidade, caso de uso, manutenção preventiva, sazonalidade setorial
- Compliance: afirmações técnicas sempre com fonte (catálogo oficial, manual)

**Distribuidora de peças do agro, terceirização de DP se encaixam aqui.**

### info-produto
Mentor, consultor, criador de conteúdo autoral vendendo curso/mentoria/consultoria.
- Pilares: autoridade, storytelling, prova social, desconstrução de crenças, método
- Compliance: se for área regulada (ex: vendas, finanças), não prometer resultado

**Mentor de vendas pra contabilidade (Thiago Concer-style) se encaixa aqui.**

## Como escolher

Se o cliente tem **mais de um nicho possível**, escolha pelo:

1. **Discurso principal** — sobre o que ele fala?
2. **Compliance mais restritivo** — se tiver saúde envolvida, é saúde-estética
3. **Modelo de venda** — info-produto é sempre info-produto, mesmo que fale de outro tema

## Criando nicho novo (qualquer segmento)

Não existe segmento que não possa virar nicho. Se o cliente não se encaixa nos existentes, o usuário descreve o negócio e o nicho é criado na hora.

**O que pedir ao usuário:**
- O que o cliente vende / faz (produto, serviço, área)
- Para quem vende (perfil do comprador final)
- Existe regulamentação ou restrição legal no setor? (ex: CRM, CREA, ANVISA, Banco Central)
- Qual o tom de voz da marca (formal, técnico, descontraído, inspiracional)

**Com essas informações, criar automaticamente:**

1. `nichos/<novo-nicho>/pilares-padrao.md` — 4-6 pilares temáticos derivados do negócio
2. `nichos/<novo-nicho>/datas-setoriais.md` — datas relevantes do setor (feiras, sazonalidade, deadlines)
3. `nichos/<novo-nicho>/tom-guardrails.md` — tom de voz + o que pode/não pode dizer (incluindo restrições regulatórias se houver)

Após criar, adicionar entrada neste catálogo e confirmar com o usuário:
> "Criei o nicho `<novo>` com os 3 arquivos base. Quer revisar antes de seguir para o onboarding?"

**Exemplos de nichos que podem surgir:**
- `juridico` — advocacia, compliance
- `educacao` — escola, curso técnico, faculdade
- `imobiliario` — imobiliária, construtora, loteadora
- `gastronomia` — restaurante, delivery, food service
- `moda` — loja de roupas, moda autoral, e-commerce
- `financeiro-pessoal` — planejador financeiro, corretora
- (qualquer outro que o usuário descrever)
