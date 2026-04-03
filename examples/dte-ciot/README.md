# Caso de Uso: DT-e/CIOT — Sistema Regulatório de Transporte de Cargas

## Contexto

O projeto DT-e/CIOT é a infraestrutura de conformidade do transporte rodoviário de cargas brasileiro, implementada a partir da MP 1.343/2026. O sistema registra toda operação via CIOT (Código Identificador da Operação de Transporte) e bloqueia preventivamente fretes abaixo do piso mínimo legal.

## Por que é um bom caso de referência para a XPAI

É um domínio com invariantes legais rígidas, múltiplos atores com interesses conflitantes, conformidade regulatória verificável, e consequências financeiras mensuráveis por erro (R$ 10.500/operação).

## Resultado

- **2 dias** do zero à fundação funcional
- **67 arquivos** gerados e testados
- **26 use cases** em Gherkin com cobertura de CI
- **0 linhas** escritas manualmente
- Cada decisão arquitetural com referência ao artigo de lei correspondente

## Stack

Java 21 / Spring Boot 3 · Kafka · PostgreSQL 16 · OPA · Kong · Temporal.io · Docker

## Descoberta crítica via XPAI

Na proposta técnica v9, havia um GAP documentado: "A inclusão do campo CIOT no MDF-e requer alteração no SINIEF — processo que envolve as 27 SEFAZes."

Após análise de 213 páginas de legislação com o agente, a descoberta: o campo `infCIOT.CIOT` já existe no schema do MDF-e desde o Ajuste SINIEF 09/2007. A MP 1.343/2026 não cria um campo novo — torna obrigatório um campo que existia há anos e não estava sendo usado corretamente.

O GAP que parecia exigir meses de negociação institucional não existia.

## Lição sobre handoff entre agentes

A instância Claude expirou após a TASK-009. O projeto continuou com agentes alternativos sem o protocolo correto de migração de contexto. Resultado: bugs introduzidos entre as TASK-010 e TASK-012, testes quebrados, dias de trabalho de recuperação.

Isso originou o [Protocolo de Handoff Entre Agentes](../../docs/handoff-entre-agentes.md) e o artefato WALKTHROUGH.md.

## Princípios ilustrados

- **P8** (Domínio como spec formal): cada padrão arquitetural tem âncora num artigo de lei
- **P9** (Proibição explícita): "NUNCA use float — pode gerar multa de R$ 10.500 por operação"
- **P10** (Resultado proporcional): experiência prévia em domínio de frete virou contexto determinante
