# Os 10 Princípios — Aprofundamento

Este documento expande cada princípio com a motivação concreta que o originou.

---

## P1 — Spec como Fonte da Verdade

O código deriva da spec, não o contrário. Specs evoluem com o projeto — não são waterfall.

**Por que importa com IA:** O agente implementa o que você especificou. Se a spec é vaga, o agente preenche as lacunas com suposições plausíveis — que podem estar erradas para o seu domínio. Uma spec precisa não elimina bugs, mas elimina a categoria de bugs causada por mal-entendido do requisito.

---

## P2 — Pair Programming Humano-Agente

Humano navega (quê/porquê), agente pilota (como). Interrupção ativa quando o agente sobre-engenheira.

**Por que importa:** O agente não tem custo de complexidade. Ele adiciona abstrações, camadas e patterns sem sentir o peso da manutenção futura. O humano precisa interromper ativamente quando o agente propõe uma solução mais complexa do que o problema exige.

---

## P3 — TDD é Mais Importante com IA

Agente escreve testes ANTES da implementação. Ratio teste/código ≥ 1.5x.

**Por que importa:** O agente não tem medo de subir código quebrado. TDD força a especificação do comportamento antes da implementação — e o teste é o contrato que impede que o agente "resolva" um problema de um jeito que passa no CI mas viola o requisito.

---

## P4 — Contexto Evolutivo (ACE)

Playbook dinâmico com delta updates. NUNCA reescrever — apenas acrescentar com IDs únicos.

**Por que importa:** LLMs não têm memória entre sessões. O CONTEXT_PLAYBOOK.md é a memória explícita do projeto. A regra de nunca reescrever garante que o histórico seja preservado e rastreável.

---

## P5 — Small Releases + CI/CD

Cada commit é production-ready. Pipeline: lint → security → tests → deploy.

**Por que importa:** O agente gera código rápido. Sem CI obrigatório, acumula-se dívida técnica silenciosa. Commits pequenos e frequentes com CI mantêm o projeto saudável continuamente.

---

## P6 — Refactoring Contínuo

O agente empilha código com velocidade. Alguém precisa podar periodicamente.

**Por que importa:** Velocidade de geração sem poda cria sistemas que funcionam mas são impossíveis de manter. Refactoring a cada 5-10 commits mantém a complexidade controlada.

---

## P7 — Human-in-the-Loop para Non-Delegation Zones

Segurança, arquitetura, regras de domínio e infraestrutura exigem revisão humana obrigatória.

**Por que importa:** Quando o agente erra nessas áreas, o post mortem vai ter o nome do humano responsável — não o nome do modelo. A responsabilidade não é delegável.

---

## P8 — O Domínio como Especificação Formal *(v2.2.1)*

Em domínios regulados, a legislação já é uma especificação. Cada decisão técnica tem âncora no documento normativo.

**Por que importa:** O agente não conhece a lei. Mas consegue implementar fielmente quando você traduz cada artigo em regra executável. Inspirado no OpenFisca: tradução fiel, não interpretação criativa.

**Exemplo prático:** "Event Sourcing porque Art. 9º-D §1º Res. 6.077/2026 exige evidências imutáveis para processos administrativos" é uma decisão técnica ancorada na lei — não uma preferência arquitetural.

---

## P9 — Proibição Explícita supera Instrução Positiva *(v2.2.1)*

"NUNCA use float — float(1306.14) pode ser 1306.1399999 e causar multa de R$ 10.500 por operação" é mais eficaz que "use BigDecimal".

**Por que importa:** O agente consegue raciocinar sobre consequências quando você as explicita. A razão concreta da proibição é parte da regra — não um comentário opcional.

---

## P10 — Resultado Proporcional ao Contexto *(v2.2.1)*

A diferença entre um dev júnior e um arquiteto sênior usando IA não é a ferramenta — é a profundidade e precisão do contexto que cada um constrói.

**Por que importa:** A IA multiplica o que você traz. Não inventa o que você não tem. Vinte anos de experiência em domínio vira contexto — e contexto é o que determina a qualidade do output.
