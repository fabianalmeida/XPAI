# CONSTITUTION: [Nome do Projeto]

> **Versão:** 1.0 | **Data:** [data] | **Status:** Definitivo
> Alterações neste arquivo requerem revisão formal humana (gate obrigatório).

---

## Visão e Objetivo

[1 parágrafo com critério de sucesso testável — sem floreios]

**Critério de sucesso testável:** [descreva o que "funcionando" significa de forma verificável]

---

## Stack Tecnológico (imutável sem revisão formal)

| Camada | Tecnologia | Alternativa |
|--------|-----------|-------------|
| Linguagem/runtime | [ex: Java 21] | [ex: Python 3.12] |
| Framework API | [ex: Spring Boot 3] | [ex: FastAPI] |
| Database | [ex: PostgreSQL 16] | — |
| Testes | [ex: JUnit 5 + Testcontainers] | [ex: pytest] |
| CI/CD | [ex: GitHub Actions] | — |

---

## Princípios de Arquitetura (Non-Delegation Zones)

1. [Regra inviolável 1 — ex: "Event store é append-only. NUNCA UPDATE ou DELETE em eventos."]
2. [Regra inviolável 2]
3. [Regra inviolável 3]

---

## Regras de Segurança

- [ ] [Regra de segurança 1 — ex: "SQL injection prevention: ORM parametrizado em todas as queries"]
- [ ] [Regra de segurança 2]
- [ ] Secrets via variáveis de ambiente — NUNCA hardcoded, NUNCA em logs

---

## Regras de Testes (Non-Negotiable)

- **Coverage mínima:** ≥80% line, ≥70% branch por serviço
- **Test ratio:** ≥1.5x (linhas de teste / linhas de código de produção)
- **TDD obrigatório:** testes escritos ANTES da implementação
- **Acceptance tests em Gherkin** do `ACCEPTANCE_TESTS.md` devem passar antes de qualquer merge em `main`
- **Lógica crítica:** revisão humana obrigatória antes de merge

### Distinção Obrigatória: Regressão Acidental vs Evolução de Contrato

| Tipo | Diagnóstico | Protocolo |
|------|-------------|-----------|
| **Regressão acidental** | Bug introduzido — comportamento correto foi quebrado | Corrigir a implementação. Não atualizar o teste. |
| **Evolução de contrato** | Mudança estrutural intencional — contrato interno evoluiu | Atualizar o teste. Revisão humana obrigatória. Documentar no WALKTHROUGH.md. |

**Invariante absoluta:** acceptance tests do `ACCEPTANCE_TESTS.md` NUNCA são "evolução de contrato".

---

## Limites de Complexidade

- Máx. **200 LOC** por arquivo de produção
- Máx. **5 parâmetros** por função/método
- Máx. **3 níveis de indentação** em métodos de negócio
- Máx. **complexidade ciclomática 10** por método

---

## Non-Delegation Zones: Revisão Humana Obrigatória

| Área | Itens críticos |
|------|---------------|
| Regras de negócio | [listar regras críticas do domínio] |
| Segurança | Autenticação, autorização, rate limiting |
| Infraestrutura | docker-compose, CI/CD, configurações de produção |
