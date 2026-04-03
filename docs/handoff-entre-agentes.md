# Protocolo de Handoff Entre Agentes

Este documento define o procedimento obrigatório ao trocar de agente (modelo, IDE ou instância) no meio de um projeto XPAI.

---

## Por que este protocolo existe

Durante o projeto DT-e/CIOT, a instância Claude expirou após a TASK-009. O projeto continuou com agentes alternativos sem o protocolo correto de migração de contexto. Resultado: bugs introduzidos silenciosamente entre a TASK-010 e TASK-012, testes que quebraram, e dias de trabalho para reconstituir o estado correto após renovação da instância.

O problema não era o agente alternativo. Era o contexto incompleto fornecido a ele.

---

## Quando executar

- Troca de modelo (ex: Claude → Gemini → Claude)
- Troca de IDE ou plataforma
- Expiração e renovação de instância
- Início de sessão após pausa longa (> 48h)
- Onboarding de novo desenvolvedor no projeto

---

## O Checklist

### Antes de encerrar a sessão atual

- [ ] WALKTHROUGH.md atualizado com o estado atual da task em andamento
- [ ] Status de build documentado (passou / falhou / o que está pendente)
- [ ] CONTEXT_PLAYBOOK.md atualizado com hurdles descobertos nesta sessão
- [ ] Qualquer decisão técnica tomada nas últimas horas documentada no WALKTHROUGH.md
- [ ] Branch commitado com mensagem semântica descritiva

### Ao iniciar com o novo agente

Sempre fornecer **todos** estes arquivos no início da sessão, sem exceção:

```
Arquivos obrigatórios (sempre):
- CONTEXT.md ou CONSTITUTION.md   ← regras invioláveis
- CONTEXT_PLAYBOOK.md              ← hurdles e padrões acumulados
- WALKTHROUGH.md                   ← estado atual do projeto

Arquivos específicos por tipo de task:
- ACCEPTANCE_TESTS.md              ← se a task envolve comportamento externo
- ARCHITECTURE.md                  ← se a task é estrutural
- SECURITY_CHECKLIST.md            ← se a task tem superfície de segurança
- PROJECT_SPEC.md                  ← se a task envolve regras de domínio
```

### Instrução de onboarding para o novo agente

Cole este bloco no início da primeira sessão com o novo agente:

```
Leia os seguintes arquivos antes de qualquer ação:
1. CONSTITUTION.md — regras invioláveis deste projeto
2. CONTEXT_PLAYBOOK.md — problemas conhecidos e padrões estabelecidos
3. WALKTHROUGH.md — histórico de execução e estado atual

Só comece a trabalhar após confirmar que leu e entendeu os três arquivos.
```

---

## Sinais de que o handoff foi incompleto

- O agente sugere uma solução que o CONTEXT_PLAYBOOK.md já descartou
- O agente usa um tipo de dado que a CONSTITUTION.md proíbe (ex: `float` em vez de `BigDecimal`)
- O agente não sabe qual é o estado atual das tasks
- Testes que passavam começam a quebrar sem mudança aparente
- O agente propõe uma arquitetura diferente da já decidida

Se qualquer um desses sinais aparecer: **pare, forneça os arquivos de contexto completos, e reinicie a sessão.**

---

## A regra de ouro do handoff

> Os artefatos XPAI (CONSTITUTION.md, CONTEXT_PLAYBOOK.md, WALKTHROUGH.md) são a memória do projeto. O agente é substituível. A memória, não.
>
> A instância pode expirar. O contexto não pode ser perdido.
