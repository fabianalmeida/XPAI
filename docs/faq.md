# FAQ — Perguntas Frequentes

---

**A XPAI funciona com qualquer LLM?**

Sim. A metodologia é agnóstica ao modelo. O contexto está nos artefatos markdown — qualquer agente que consiga ler markdown e seguir instruções pode executar as tasks. A qualidade do output varia com a capacidade do modelo, mas a estrutura funciona com Claude, GPT, Gemini, Llama local, e outros.

---

**Preciso usar o IDE Antigravity?**

Não. Antigravity é o ambiente em que a metodologia foi desenvolvida, mas qualquer IDE ou interface de chat com suporte a anexar arquivos funciona. O que importa é que você consiga injetar os arquivos de contexto no início de cada sessão.

---

**Posso usar com modelos locais (Ollama, LM Studio)?**

Sim. A XPAI foi desenhada para ser compatível com execução local. Modelos locais menores têm janela de contexto menor — ajuste o número de arquivos injetados por sessão conforme a capacidade do modelo. A seção 3.4 (contexto calibrado por task) é especialmente importante nesse cenário.

---

**Quanto tempo leva para configurar um projeto XPAI do zero?**

As Fases F0 a F3 (do bootstrap até o task breakdown) levam entre 6 e 10 horas num projeto de complexidade média. Esse investimento inicial é recuperado nas primeiras tasks de implementação.

---

**O que é uma "Non-Delegation Zone"?**

São as áreas do projeto onde a revisão humana é obrigatória antes de qualquer merge — independente de o agente ter "gerado código funcionando". Segurança, lógica de negócio crítica, infraestrutura de produção. O agente pode propor a implementação; o humano valida antes de commitar.

---

**Qual a diferença entre WALKTHROUGH.md e CONTEXT_PLAYBOOK.md?**

O WALKTHROUGH.md é o histórico detalhado de execução de cada task — específico, granular, cronológico. O CONTEXT_PLAYBOOK.md contém apenas padrões recorrentes abstraídos do walkthrough — o que vale para qualquer agente, em qualquer sessão futura. O walkthrough é memória local; o playbook é conhecimento do projeto.

---

**E se um acceptance test quebrar durante uma refactoring?**

Acceptance tests nunca são "evolução de contrato". Se um acceptance test quebra, a implementação está errada — não o teste. Corrija a implementação. Veja a seção 5.3.1 da metodologia para a distinção completa entre regressão acidental e evolução de contrato.

---

**A metodologia funciona para projetos pequenos?**

Sim, com adaptação. Para projetos pequenos ou protótipos, você pode simplificar: CONSTITUTION.md + CONTEXT_PLAYBOOK.md são sempre obrigatórios; os demais artefatos são opcionais conforme a complexidade. O princípio fundamental — spec antes de código, contexto explícito — continua valendo em qualquer escala.
