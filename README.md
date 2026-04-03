# XPAI — Spec-Driven Vibe Coding

**eXtreme Prompt-Aided Implementation** · v2.2 · Abril 2026

> *"O LLM não conhece seu domínio. Você conhece. O resultado é proporcional ao que você traz para a conversa."*

---

## O que é a XPAI

XPAI é uma metodologia de desenvolvimento de software assistido por IA para equipes e engenheiros que trabalham em domínios com **regras de negócio críticas, conformidade legal ou invariantes que não podem ser violadas**.

Não é vibe coding. É **spec-driven vibe coding**: você especifica com precisão, o agente implementa com velocidade.

A premissa central:

```
HUMANO: decide O QUÊ e O PORQUÊ
AGENTE: decide O COMO (implementação)

Você é o Navigator — o agente é o Driver.
Inverta isso e o resultado piora dramaticamente, sempre.
```

---

## Por que existe

Em 2026, construí a fundação de um sistema regulatório complexo em **2 dias, sem escrever uma linha de código**:

- 67 arquivos gerados e testados
- 26 use cases em Gherkin com cobertura de CI
- Cada decisão arquitetural com referência ao artigo de lei correspondente
- Descoberta de um GAP técnico que parecia exigir meses de negociação — e não existia

A XPAI foi a metodologia que tornou isso possível. Este repositório é a documentação pública dessa metodologia para que outros possam usá-la.

---

## A Metodologia

📄 **[XPAI-v2.2.md](./XPAI-v2.2.md)** — Documentação completa da metodologia v2.2

Inclui:
- Os 10 princípios operacionais
- As 6 fases de implementação (F0 a F6)
- Os artefatos obrigatórios com templates prontos
- Checklists operacionais (início de sessão, por tarefa, antes do deploy)
- Protocolo de handoff entre agentes
- Distinção entre regressão acidental e evolução de contrato

---

## Os 10 Princípios em 30 Segundos

| # | Princípio | Núcleo |
|---|-----------|--------|
| 1 | Spec como fonte da verdade | Código deriva da spec — nunca o contrário |
| 2 | Pair programming humano-agente | Humano navega, agente pilota |
| 3 | TDD é mais importante com IA | Agente não tem medo de subir código quebrado. Você deveria ter |
| 4 | Contexto evolutivo (ACE) | Playbook dinâmico — delta updates, nunca rewrite |
| 5 | Small releases + CI/CD | Cada commit é production-ready, sem exceção |
| 6 | Refactoring contínuo | O agente empilha rápido. Alguém precisa podar |
| 7 | Human-in-the-loop | Responsabilidade legal não é delegável ao modelo |
| 8 | O domínio como especificação formal | Legislação e regras de negócio são specs executáveis |
| 9 | Proibição explícita supera instrução positiva | "NUNCA X porque Y causa Z" é mais eficaz que "use X" |
| 10 | Resultado proporcional ao contexto | Sênior com XPAI ≠ júnior com XPAI |

---

## As 6 Fases

```
F0  Bootstrap & Constitution    — regras invioláveis antes de qualquer código     (1–2h)
F1  Specification               — use cases em Gherkin, o "o quê" sem o "como"   (2–4h)
F2  Technical Plan              — arquitetura com justificativa por decisão        (1–2h)
F3  Task Breakdown              — tasks INVEST com prompt e contexto calibrado     (1h)
F4  TDD Cycle                   — testes antes da implementação, CI obrigatório    (30–60min/task)
F5  Refactoring & Hardening     — poda periódica, safety net de testes             (a cada 5–10 commits)
F6  ACE Playbook Update         — memória explícita acumulada entre sessões         (por sessão)
```

---

## Os Artefatos

Cada projeto XPAI tem estes arquivos na raiz:

| Arquivo | Função | Frequência |
|---------|--------|------------|
| `CONSTITUTION.md` | Regras invioláveis — lido em toda sessão | Raramente |
| `PROJECT_SPEC.md` | Problem statement + acceptance criteria em Gherkin | Por feature |
| `ACCEPTANCE_TESTS.md` | Use cases executáveis — viram testes de integração | Por feature |
| `ARCHITECTURE.md` | Decisões técnicas com justificativa | Por decisão |
| `TASK_BREAKDOWN.md` | Tasks com prompt pronto e contexto calibrado | Por feature |
| `CONTEXT_PLAYBOOK.md` | Playbook evolutivo — delta updates, nunca rewrite | Por hurdle |
| `WALKTHROUGH.md` | Histórico de execução por task — viaja com o git | Por task |
| `SECURITY_CHECKLIST.md` | Gates de segurança por feature | Por feature |

Templates prontos para uso em [`/templates`](./templates/).

---

## Início Rápido

```bash
# 1. Clone o repositório
git clone https://github.com/[SEU_USUARIO]/xpai.git
cd xpai

# 2. Copie os templates para o seu projeto
cp templates/CONSTITUTION.md   meu-projeto/
cp templates/CONTEXT_PLAYBOOK.md  meu-projeto/
cp templates/WALKTHROUGH.md    meu-projeto/
cp templates/SECURITY_CHECKLIST.md meu-projeto/

# 3. Abra CONSTITUTION.md e personalize:
#    - Stack tecnológico
#    - Regras invioláveis do domínio
#    - Non-Delegation Zones
#    - Limites de complexidade

# 4. Siga as 6 fases documentadas em XPAI-v2.2.md
```

---

## Para Quem é

✅ Engenheiros e arquitetos sêniors desenvolvendo em domínios com **regras críticas ou conformidade legal**

✅ Times que precisam de **rastreabilidade** entre requisito de negócio e implementação

✅ Projetos onde um erro tem **consequência mensurável** — financeira, legal ou operacional

✅ Qualquer desenvolvedor que quer usar IA **sem perder o controle** do que está sendo construído

## O Que Não É

❌ Uma receita para substituir engenheiros por LLMs

❌ Uma solução para quem não tem conhecimento de domínio

❌ Agnóstica ao esforço — a spec é o produto principal e exige experiência para ser escrita bem

---

## Caso de Uso de Referência

A metodologia foi desenvolvida e validada para o backend de um projeto — sistema de conformidade regulatória.



---

## Estrutura do Repositório

```
xpai/
├── README.md                    ← este arquivo
├── XPAI-v2.2.md                 ← documentação completa da metodologia
├── CHANGELOG.md                 ← histórico de versões
├── CONTRIBUTING.md              ← como contribuir
├── LICENSE                      ← MIT
│
├── templates/                   ← templates prontos para uso
│   ├── CONSTITUTION.md
│   ├── CONTEXT_PLAYBOOK.md
│   ├── WALKTHROUGH.md
│   └── SECURITY_CHECKLIST.md
│
├── docs/                        ← documentação complementar
│   ├── principios.md            ← aprofundamento dos 10 princípios
│   ├── faq.md                   ← perguntas frequentes
│   └── handoff-entre-agentes.md ← protocolo de troca de agente/modelo
│
└── examples/                    ← projetos de referência
    └── dte-ciot/
        └── README.md            ← resumo do caso DT-e/CIOT
```

---

## Histórico de Versões

| Versão | Data | Principais mudanças |
|--------|------|---------------------|
| 2.2.2 | Abr 2026 | Seção 5.3.1 — distinção regressão acidental vs evolução de contrato |
| 2.2.1 | Abr 2026 | WALKTHROUGH.md, contexto calibrado por task (3.4), estrutura explícita (3.5), P8/P9/P10 |
| 2.2 | Mar 2026 | Versão inicial publicada |

Histórico completo: [CHANGELOG.md](./CHANGELOG.md)

---

## Licença

MIT — use, adapte, contribua. Ver [LICENSE](./LICENSE).

---

*Construído a partir de prática real, não de teoria. Cada princípio foi adicionado porque, sem ele, algo quebrou de um jeito que custou tempo ou dinheiro.*
