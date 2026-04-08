# XPAI — Metodologia de Desenvolvimento Assistido por IA
**Versão:** 3.0  
**Status:** Revisado — Ativo  
**Base:** Spec-Driven Development · Extreme Programming · Agentic Context Engineering  
**Última Revisão:** Abril 2026

---

## Nota de Versão

A v3.0 corrige o principal desvio da v2.2: **a metodologia havia absorvido implementação**. Detalhes de stack, constraints de LOC, pipelines de CI e diagramas de infraestrutura pertencem à **especificação do projeto** (CONSTITUTION.md, ARCHITECTURE.md), não à metodologia. A metodologia define **como trabalhar** — a especificação define **o que construir e com quê**.

Esta versão também incorpora o conceito de **skills reutilizáveis para LLMs** e reduz a prescritividade técnica, tornando a metodologia aplicável a qualquer domínio, linguagem ou tamanho de projeto.

---

## 1. Fundamentos

### 1.1. Lei de Ouro

```
┌─────────────────────────────────────────────────────────┐
│ HUMANO: decide O QUÊ e O PORQUÊ                         │
│ AGENTE: decide O COMO (implementação)                   │
│                                                         │
│ Você é o Navigator — o agente é o Driver                │
│ Inverta isso e o resultado piora dramaticamente, sempre │
└─────────────────────────────────────────────────────────┘
```

### 1.2. As Três Correntes Fundadoras

| Corrente | Contribuição para XPAI |
|----------|------------------------|
| **Extreme Programming (XP)** | Pair programming humano-agente, TDD, small releases, refactoring contínuo |
| **Spec-Driven Development (SDD)** | Spec como fonte da verdade. Artefatos vivos antes do código |
| **Agentic Context Engineering (ACE)** | Playbook evolutivo com delta updates, prevenção de context collapse |

### 1.3. Os 6 Princípios Operacionais

| # | Princípio | Descrição |
|---|-----------|-----------|
| **1** | **Spec como Fonte da Verdade** | Código deriva da spec, nunca o contrário. Specs evoluem com o projeto — não são waterfall |
| **2** | **Pair Programming Humano-Agente** | Humano navega (quê/porquê), agente pilota (como). Intervenção ativa quando o agente sobre-engenheira |
| **3** | **TDD é Mais Importante com IA** | Agente escreve testes *antes* da implementação. Testes são o contrato da spec |
| **4** | **Contexto Evolutivo** | Playbook dinâmico que acumula estratégias. Delta updates incrementais — nunca reescritas |
| **5** | **Small Releases Contínuas** | Cada commit deve ser production-ready. CI é o árbitro, não a revisão manual |
| **6** | **Human-in-the-Loop nas Non-Delegation Zones** | Segurança, arquitetura, domínio crítico e infraestrutura exigem revisão humana obrigatória |

---

## 2. Os Artefatos Vivos

A XPAI opera sobre um conjunto mínimo de artefatos que vivem no repositório e evoluem ao longo do projeto. Eles são o **contexto primário** do agente — não devem ser fornecidos via prompt ad-hoc, mas mantidos como arquivos rastreáveis.

### 2.1. Artefatos Obrigatórios

| Artefato | Propósito | Mutabilidade |
|----------|-----------|--------------|
| **CONSTITUTION.md** | Princípios não-negociáveis do projeto: visão, stack escolhida, regras de segurança, limites de complexidade, padrões de qualidade | Raramente muda; exige gate formal para alteração |
| **SPEC.md** (ou equivalente) | Problem statement, user stories, acceptance criteria em Gherkin/BDD, non-goals explícitos | Evolui a cada feature |
| **ARCHITECTURE.md** | Decisões arquiteturais, bounded contexts, diagramas de fluxo, padrões de integração | Evolui com decisões de design |
| **TASKS.md** | Decomposição atômica das features em tarefas INVEST-compliant | Evolui por sprint/ciclo |
| **CONTEXT_PLAYBOOK.md** | Playbook evolutivo: estratégias, pitfalls, domain knowledge acumulado | Atualizado após cada sessão (delta updates) |

> **Nota:** O conteúdo técnico de cada artefato (linguagem, framework, ferramentas) pertence à **especificação do projeto**, não à metodologia. A XPAI define que esses artefatos devem existir e como usá-los — não o que deve estar dentro deles.

### 2.2. Hierarquia de Confiança dos Artefatos

```
CONSTITUTION.md    ← mais estável, define o que nunca muda
    │
    ▼
ARCHITECTURE.md    ← decisões de design ratificadas
    │
    ▼
SPEC.md            ← features e critérios de aceitação
    │
    ▼
TASKS.md           ← implementação atômica
    │
    ▼
CONTEXT_PLAYBOOK   ← conhecimento tático acumulado
```

Quando houver conflito entre artefatos, o artefato **mais alto** na hierarquia prevalece.

---

## 3. Fluxo de Implementação

O ciclo de desenvolvimento segue **5 Fases**, iteradas a cada feature ou sprint.

### 3.1. Visão Geral

```
┌──────────────────────────────────────┐
│  FASE 0: Bootstrap                   │
│  Output: artefatos iniciais          │
│  Quem: humano + agente (co-autoria)  │
└────────────┬─────────────────────────┘
             ▼
┌──────────────────────────────────────┐
│  FASE 1: Specification               │
│  Output: SPEC.md com Gherkin         │
│  Quem: humano decide, agente escreve │
└────────────┬─────────────────────────┘
             ▼
┌──────────────────────────────────────┐
│  FASE 2: Task Breakdown              │
│  Output: TASKS.md com critérios      │
│  Quem: agente propõe, humano valida  │
└────────────┬─────────────────────────┘
             ▼
┌──────────────────────────────────────┐
│  FASE 3: TDD Cycle (por tarefa)      │
│  Output: código testado + CI verde   │
│  Quem: agente pilota, humano navega  │
└────────────┬─────────────────────────┘
             ▼
┌──────────────────────────────────────┐
│  FASE 4: Refactoring & Playbook      │
│  Output: código saudável + playbook  │
│  Trigger: a cada 5-10 commits        │
└──────────────────────────────────────┘
```

### 3.2. Fase 0 — Bootstrap

O objetivo é criar os artefatos iniciais do projeto em co-autoria com o agente, com revisão humana obrigatória antes do primeiro commit.

**Ações:**
1. Humano define visão, domínio, tecnologias e restrições de negócio
2. Agente gera rascunho de CONSTITUTION.md, ARCHITECTURE.md e SPEC.md
3. Humano revisa e aprova os artefatos (Gate 0)
4. Commit inicial com artefatos ratificados

> **Regra do Bootstrap:** Nunca inicie o código sem que CONSTITUTION.md e SPEC.md estejam aprovados pelo humano. Todo código gerado antes de uma spec é código sem contrato.

### 3.3. Fase 1 — Specification

A spec é escrita em linguagem que a LLM possa usar como *guardrail* de geração — não como documentação passiva.

**Critérios de uma boa spec para LLMs:**
- **Goals expressados em verbos testáveis**: "o sistema deve emitir CIOT automaticamente quando...", não "gerenciar CIOT"
- **Non-goals explícitos**: o que está fora do escopo é tão importante quanto o que está dentro
- **Acceptance criteria em Gherkin** (Given/When/Then): cada critério é um test case candidato
- **Edge cases nomeados**: comportamentos esperados em falhas, timeouts, dados inválidos

**Gate 1 — checklist de spec:**
- [ ] Cada goal pode ser verificado por um teste automatizado?
- [ ] Non-goals estão explícitos?
- [ ] Acceptance criteria cobrem happy path e pelo menos 2 error paths?
- [ ] Regras de domínio críticas estão documentadas com suas fontes?

### 3.4. Fase 2 — Task Breakdown

O agente decompõe a spec em tarefas atômicas, validadas pelo critério **INVEST**:

| Letra | Significado | Verificação |
|-------|-------------|-------------|
| **I** | Independent | Pode ser implementada sem depender de outra task não-concluída? |
| **N** | Negotiable | O escopo pode ser ajustado sem quebrar o valor? |
| **V** | Valuable | Entrega valor observável ao usuário ou ao sistema? |
| **E** | Estimable | O esforço pode ser estimado em horas? |
| **S** | Small | Pode ser concluída em uma sessão de 30–60 min? |
| **T** | Testable | Existe critério claro de "done"? |

**Formato de task:**
```
TASK-[ID]: [Título curto e ativo]
Spec: [referência ao critério de aceitação na SPEC.md]
Done when: [critério testável de conclusão]
Skill sugerida: [se houver skill reutilizável aplicável — ver Seção 5]
```

### 3.5. Fase 3 — TDD Cycle

Este é o coração da metodologia. Para cada task, o ciclo é:

```
1. CONTEXTO       → Injetar spec da task + domain knowledge relevante
2. TESTES PRIMEIRO → Agente escreve testes que falham (Red)
3. GATE HUMANO    → Humano valida se os testes cobrem o comportamento esperado
4. IMPLEMENTAÇÃO  → Agente implementa o mínimo para os testes passarem (Green)
5. CI             → Pipeline roda automaticamente
6. REFACTOR       → Agente melhora legibilidade sem quebrar testes (Refactor)
7. COMMIT         → Commit semântico production-ready
8. PLAYBOOK       → Documentar hurdles via delta update
```

**Regra do Red-Green-Refactor com agente:**
> O agente nunca deve escrever implementação antes dos testes. Se o agente produzir implementação sem testes, interrompa e solicite os testes primeiro. Testes são o contrato — a implementação é a consequência.

**Anatomia de um commit production-ready:**
```
[x] CI verde (lint + security + tests)
[x] Nenhum arquivo de debug ou código comentado
[x] Testes cobrem o comportamento novo (happy path + error paths)
[x] CONTEXT_PLAYBOOK.md atualizado com hurdles descobertos
[x] Spec atualizada se comportamento mudou
```

### 3.6. Fase 4 — Refactoring & Playbook Update

Refactoring contínuo é parte do método, não uma fase separada. A cada 5–10 commits, o agente (como Reflector) analisa a codebase recente em busca de duplicações, responsabilidades difusas e complexidade acidental.

**Regras de refactoring com agente:**
- Testes devem permanecer verdes durante o refactor
- Refactors pequenos e frequentes, nunca grandes reescritas
- O CONTEXT_PLAYBOOK.md deve registrar o *porquê* de cada decisão de design

---

## 4. Non-Delegation Zones

Algumas decisões **nunca podem ser delegadas totalmente ao agente**. Revisão humana é obrigatória.

| Zona | Por que não delegar |
|------|---------------------|
| **Segurança** | Autenticação, autorização, sanitização, gestão de secrets, rate limiting — falhas aqui têm consequências irreversíveis |
| **Arquitetura** | Isolamento de contextos, contratos entre serviços, decisões de backward compatibility |
| **Domínio crítico** | Regras de negócio com impacto legal, fiscal ou financeiro — o agente não conhece o domínio sem que você o ensine |
| **Infraestrutura** | Configurações de produção, backup/recovery, alertas e logging estruturado |

```
┌─────────────────────────────────────────────────────────┐
│ ⚠️  Regra de Violação                                   │
│                                                         │
│ Quando o agente violar um princípio da CONSTITUTION.md: │
│ "Para. Isso viola [princípio]. Corrija antes de         │
│ continuar."                                             │
│                                                         │
│ NUNCA deixe uma violação passar para o próximo commit   │
└─────────────────────────────────────────────────────────┘
```

---

## 5. Skills Reutilizáveis para LLMs

### 5.1. O que são Skills

Skills são instruções estruturadas (geralmente arquivos Markdown) que ensinam a LLM a executar uma tarefa específica com precisão e consistência — formatação de documentos, geração de diagramas, criação de planilhas, leitura de PDFs, entre outras. Repositórios públicos como [antigravity-awesome-skills](https://github.com/sickn33/antigravity-awesome-skills), [anthropics/skills](https://github.com/anthropics/skills) e [awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills) concentram centenas de skills battle-tested.

### 5.2. Onde Skills se Encaixam na XPAI

A XPAI recomenda o uso de skills em **dois pontos do fluxo**:

#### A) Na Especificação (Bootstrap)

Skills de geração de artefatos podem ser usadas durante a Fase 0 para produzir os documentos fundacionais do projeto com maior qualidade e consistência:

| Artefato | Skill sugerida |
|----------|---------------|
| `CONSTITUTION.md` | skill de geração de constitution / project charter |
| `ARCHITECTURE.md` | skill de diagramas Mermaid / arquitetura hexagonal |
| `TASKS.md` | skill de task breakdown / user story mapping |
| Documentação técnica (.docx, .pdf) | skill de geração de documentos |

> **Como referenciar na spec:**
> ```markdown
> ## Bootstrap
> Para gerar CONSTITUTION.md: utilize a skill `constitution-generator` do repositório 
> antigravity-awesome-skills antes de preencher os campos do projeto.
> ```

#### B) Nas Tasks (Fase 3)

Skills de implementação podem ser referenciadas diretamente em tasks específicas, como guardrails de execução:

```
TASK-042: Gerar relatório de auditoria em PDF
Spec: RF-18 — exportação de registros para fins regulatórios
Done when: PDF gerado com todos os campos obrigatórios e assinatura digital válida
Skill: use skill `pdf-generator` para garantir estrutura e metadados corretos
```

Isso cria um **padrão de execução replicável**: a LLM que executar essa task seguirá a skill como receita, não como improviso.

### 5.3. Critérios para Usar uma Skill

Nem toda tarefa precisa de skill. Use quando:

- A tarefa tem **saída com formato bem definido** (PDFs, planilhas, diagramas, documentos Word)
- A tarefa é **recorrente** no projeto (ex: geração de relatórios, criação de migrations)
- Existe uma skill pública **testada e mantida** que cobre o caso
- O custo de não usar a skill é **inconsistência ou retrabalho**

Não use quando:
- A tarefa é de **lógica de negócio** — skills não substituem spec de domínio
- A skill disponível é genérica demais para o contexto específico do projeto
- A skill cria **dependência de um repositório externo sem versionamento** claro

### 5.4. Onde Documentar Skills no Projeto

```
project-root/
├── CONSTITUTION.md          ← referenciar skills usadas no bootstrap
├── TASKS.md                 ← referenciar skills por task quando aplicável
├── .skills/                 ← (opcional) copiar skills externas para o repositório
│   ├── pdf-generator.md
│   └── architecture-diagram.md
```

> **Recomendação:** Se uma skill externa for crítica para o projeto, faça uma cópia versionada no repositório (`.skills/`). Dependência de URL externa pode quebrar silenciosamente.

---

## 6. Checklists Operacionais

### Checklist: Início de Sessão
- [ ] Leia as últimas entradas do CONTEXT_PLAYBOOK.md
- [ ] Instrua o agente: *"Leia CONTEXT_PLAYBOOK.md e CONSTITUTION.md antes de qualquer ação"*
- [ ] Escolha a próxima task do TASKS.md
- [ ] Confirme que o CI está verde no último commit
- [ ] Defina o objetivo claro da sessão

### Checklist: Por Tarefa (TDD Cycle)
- [ ] O agente tem o contexto de domínio específico para esta task?
- [ ] O agente escreveu os testes *antes* da implementação?
- [ ] Os testes cobrem happy path + error paths + edge cases?
- [ ] O código implementado é simples (sem over-engineering)?
- [ ] CI rodou e está verde?
- [ ] Revisei o diff antes de confirmar o commit?
- [ ] Há algum hurdle novo para documentar no CONTEXT_PLAYBOOK.md?

### Checklist: Antes do Deploy
- [ ] Todos os commits do branch com CI verde?
- [ ] Critérios de aceitação da SPEC.md satisfeitos?
- [ ] Security scan limpo?
- [ ] CONTEXT_PLAYBOOK.md atualizado com lições desta feature?
- [ ] Variáveis de ambiente de produção configuradas e validadas?
- [ ] Rollback procedure documentado?

---

## 7. Loop de Melhoria Contínua

| Período | Atividades |
|---------|------------|
| **Por sessão** | Atualizar CONTEXT_PLAYBOOK.md com delta updates |
| **Semanal** | Revisar métricas de saúde, priorizar refactors pendentes, validar non-delegation zones |
| **Por feature** | Atualizar SPEC.md se comportamento mudou, revisar TASKS.md concluídas |
| **Mensal** | Revisar CONSTITUTION.md, auditar checklist de segurança, avaliar novas skills disponíveis |

---

## 8. Templates de Artefatos

### 8.1. Template: CONSTITUTION.md

```markdown
# CONSTITUTION: [Nome do Projeto]

## Visão & Objetivo
[1 parágrafo testável, sem floreios — o que o sistema faz e para quem]

## Stack Tecnológica (imutável sem revisão formal)
- Linguagem/Framework: [especificar]
- Banco de dados: [especificar]
- Deploy: [especificar]
- CI/CD: [especificar]
- Testing: [especificar framework e coverage mínima]

## Princípios de Arquitetura
[Padrões arquiteturais escolhidos e suas justificativas — ex: hexagonal, event-driven, etc.]

## Regras de Segurança
[Checklist de segurança específico do domínio]

## Limites de Complexidade
[Métricas de qualidade de código acordadas para o projeto]

## Skills Utilizadas no Bootstrap
[Lista de skills externas usadas para gerar os artefatos iniciais]
```

### 8.2. Template: TASKS.md (task individual)

```markdown
## TASK-[ID]: [Título curto e ativo]

**Spec de referência:** [link para critério em SPEC.md]
**Done when:** [critério testável e observável de conclusão]
**Skill sugerida:** [skill reutilizável, se aplicável]
**Non-delegation:** [marcar se esta task toca uma Non-Delegation Zone]

### Acceptance Criteria
- Given [contexto], When [ação], Then [resultado esperado]
- Given [contexto de falha], When [ação], Then [comportamento de erro esperado]
```

### 8.3. Template: CONTEXT_PLAYBOOK.md

```markdown
# [NOME DO PROJETO] — Agent Playbook
# ⚠️ NUNCA reescreva este arquivo — use delta updates com IDs únicos

## PROJECT OVERVIEW
[1 parágrafo: o que é, stack, objetivo final]

## STRATEGIES & HARD RULES [shr-xxxxx]
[shr-00001] :: [Padrão ou decisão importante com contexto]

## TROUBLESHOOTING & PITFALLS [ts-xxxxx]
[ts-00001] :: [Problema] | [Solução] | [Como testar que foi resolvido]

## DOMAIN KNOWLEDGE [dk-xxxxx]
[dk-00001] :: [Conhecimento de domínio crítico que o agente precisa para não errar]

## HURDLES [hurdle-xxx]
[hurdle-001] Data: [data] | Problema: [descrição] | Solução: [descrição] | Status: [resolvido/aberto]
```

---

## 9. Reflexão: Arquitetura Complexa e DDD

### Deve a XPAI prescrever Hexagonal, DDD, CI/CD e mocks?

**Não.** Esses são padrões excelentes — mas pertencem à **especificação do projeto**, não à metodologia.

A XPAI opera em um nível de abstração acima: ela define *como trabalhar com a LLM*, não *o que construir*. Um projeto pode adotar arquitetura hexagonal, DDD e mocks detalhados — e isso deve estar no CONSTITUTION.md e ARCHITECTURE.md daquele projeto específico. A metodologia deve ser aplicável a um microserviço simples ou a um ecossistema complexo como o DT-e sem mudar uma linha.

**O que a XPAI garante universalmente:**
- Spec antes do código
- Testes antes da implementação
- Contexto evolutivo (playbook)
- Revisão humana nas zonas críticas
- Small releases com CI verde

**O que vai na especificação do projeto:**
- Stack tecnológica e versões
- Padrões arquiteturais (hexagonal, CQRS, event-driven)
- Estratégias de mock e testes de integração
- Regras de domínio (DDD: bounded contexts, aggregates, domain events)
- Configuração de CI/CD e pipelines específicos
- Métricas de coverage e complexity targets

---

## 10. Lembrete Final

```
"Use o mínimo de especificação necessário para remover ambiguidade 
no seu contexto.

Spec-first para desenvolvimento assistido por IA;
Spec-anchored para sistemas em produção de longa vida;
Spec-as-source apenas quando a geração é madura e confiável."
```

```
"A IA é seu espelho: revela mais rápido quem você é.
Se for incompetente, vai produzir coisas ruins mais rápido.
Se for competente, vai produzir coisas boas mais rápido."
— AkitaOnRails
```

---

**Baseado em:** XPAI v2.2 (2026) · AkitaOnRails "Do Zero à Pós-Produção em 1 Semana" · GitHub Spec-Kit · ACE (Stanford/SambaNova, ICLR 2026) · antigravity-awesome-skills · anthropics/skills · awesome-claude-skills (travisvn)
