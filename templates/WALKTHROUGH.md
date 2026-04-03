# WALKTHROUGH.md — [Nome do Projeto]
# Histórico de execução de tasks por sessão de agente
#
# ⚠️ INSTRUÇÃO PARA O AGENTE:
# Ao finalizar uma task, crie uma entrada com o formato abaixo.
# Nunca apague entradas anteriores — apenas adicione ao final.
# Este arquivo viaja com o repositório e é lido por todos os agentes subsequentes.

---

## Como usar

Para cada task executada, o agente deve criar uma seção com:
- O que foi feito (decisões técnicas e implementação)
- Bugs encontrados e como foram resolvidos
- Desvios do plano original (e por quê)
- Status final do build
- O que ficou pendente para a próxima sessão
- O que foi promovido ao CONTEXT_PLAYBOOK.md (e o que não foi, e por quê)

---

<!-- Exemplo de entrada — remova antes de usar -->
<!--
## TASK-001 — [Nome da Task]
**Data:** [data]
**Agente:** [modelo/IDE utilizado]
**Status:** BUILD SUCCESS | BUILD FAILURE | PARCIAL

### O que foi implementado
[decisões técnicas e o que foi entregue]

### Bugs encontrados e resolvidos
[descrição do bug, causa raiz, solução aplicada]

### Desvios do plano original
[o que mudou em relação ao prompt inicial e por quê]

### Status do build
`mvn test` / `pytest` — [PASSOU / FALHOU / PARCIAL]

### Promovido ao CONTEXT_PLAYBOOK.md
- [ts-00001] [descrição] — promovido porque outro agente repetiria
- NÃO promovido: [bug X] — específico deste ambiente local

### Pendências para a próxima sessão
- [ ] [item 1]
- [ ] [item 2]
-->
