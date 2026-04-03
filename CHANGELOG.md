# Changelog — XPAI

Todas as mudanças significativas nesta metodologia são documentadas aqui.

Formato baseado em [Keep a Changelog](https://keepachangelog.com/pt-BR/1.0.0/).

---

## [2.2.2] — Abril 2026

### Adicionado
- **Seção 5.3.1** — Distinção formal entre Regressão Acidental e Evolução de Contrato
- Invariante absoluta: acceptance tests nunca são classificados como "evolução de contrato"
- Protocolo de 5 passos para tratamento de quebras por evolução de contrato
- Alerta explícito sobre comportamento do LLM de atualizar testes para "fazer o CI passar"

### Motivação
Necessidade prática identificada durante o projeto DT-e/CIOT: mudanças estruturais legítimas
(extração de Value Objects, refactoring de API interna) quebravam testes corretos de tasks
anteriores. A regra "CI verde antes de avançar" precisava de distinção mais fina.

---

## [2.2.1] — Abril 2026

### Adicionado
- **WALKTHROUGH.md** como artefato obrigatório (seção 3.1, 3.3, template 7.3)
- **Seção 3.4** — Contexto calibrado por task: mapa de quais arquivos incluir em cada tipo de task
- **Seção 3.5** — Estrutura de arquivos explícita em cada prompt (convenção Java e Python)
- **Princípio P8** — A Lei (ou Domínio) como Especificação Formal
- **Princípio P9** — Proibição Explícita supera Instrução Positiva
- **Princípio P10** — Resultado proporcional ao contexto fornecido
- Retroalimentação em dois níveis no loop de execução (WALKTHROUGH + CONTEXT_PLAYBOOK)
- Frequência "por task" no ciclo de melhoria contínua
- Critério explícito de promoção: o que vai ao WALKTHROUGH vs o que vai ao CONTEXT_PLAYBOOK

### Motivação
Experiência acumulada no projeto DT-e/CIOT (TASK-001 a TASK-009). Os três princípios novos
emergiram da prática em domínio regulatório (MP 1.343/2026). O WALKTHROUGH.md foi adicionado
após identificar que o histórico de execução ficava preso no IDE e não viajava com o repositório.

---

## [2.2] — Março 2026

### Adicionado
- Versão inicial publicada
- 7 princípios operacionais
- 6 fases de implementação (F0 a F6)
- Artefatos obrigatórios: CONSTITUTION.md, PROJECT_SPEC.md, ACCEPTANCE_TESTS.md,
  ARCHITECTURE.md, TASK_BREAKDOWN.md, CONTEXT_PLAYBOOK.md, SECURITY_CHECKLIST.md
- Templates de artefatos (seção 7)
- Checklists operacionais: início de sessão, por tarefa, antes do deploy
- Métricas de saúde do projeto (seção 5.1)
- Constraints arquiteturais explícitas (seção 2.3)

### Base
- Extreme Programming (Kent Beck, 1999)
- Spec-Driven Development (GitHub Spec-Kit, 2025)
- Agentic Context Engineering (Stanford/SambaNova, ICLR 2026)
