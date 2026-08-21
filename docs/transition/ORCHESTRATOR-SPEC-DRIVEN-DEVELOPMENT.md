# ORCHESTRATOR-SPEC-DRIVEN-DEVELOPMENT

**Projeto:** Adaptive AI Orchestrator  
**Versão:** v0.1 — disciplina formal de desenvolvimento  
**Status:** Em desenvolvimento  
**Aplicação:** transversal a requisitos, arquitetura, design, implementação, validação, Evals e evolução

---

# 1. Propósito

Este documento formaliza **Specification-Driven Development (SDD)** como disciplina de desenvolvimento do Adaptive AI Orchestrator.

O objetivo é garantir que, em um sistema desenvolvido com forte participação de agentes de IA:

```text
intenção
→ especificação explícita
→ arquitetura
→ design
→ plano
→ implementação
→ verificação
→ evidência
```

permaneça coerente ao longo de todo o ciclo.

O risco que esta disciplina busca controlar é a perda progressiva de intenção entre:

```text
necessidade
→ requisito
→ arquitetura
→ design
→ código
→ comportamento observado
```

Esse risco é particularmente relevante em desenvolvimento assistido por IA porque um agente pode produzir rapidamente uma implementação aparentemente funcional a partir de instruções incompletas. Microsoft descreve SDD justamente como uma abordagem para manter requisitos, design, implementação e validação alinhados, evitando que a velocidade de geração esconda perda de intenção. citeturn430705search5

---

# 2. Por que SDD é especialmente relevante neste projeto

O Orchestrator que estamos construindo não será apenas um software convencional.

Ele próprio deverá:

- interpretar especificações;
- estruturar projetos;
- decompor trabalho;
- delegar implementação;
- avaliar resultados;
- replanejar.

Portanto, a disciplina usada para construir o Orchestrator também precisa ser compatível com a disciplina que ele futuramente aplicará aos projetos.

Temos dois níveis:

```text
NÍVEL A — construção do Orchestrator

Specification
→ Design
→ Code
→ Verification
```

e:

```text
NÍVEL B — trabalho futuro gerenciado pelo Orchestrator

Project Specification
→ Architecture
→ Design
→ Implementation
→ Verification
→ Evaluation
```

O primeiro garante a qualidade do próprio sistema.

O segundo define parte de seu comportamento operacional.

---

# 3. Estado da prática atual

O termo **Spec-Driven Development** ainda não possui uma definição única e rígida no mercado.

Literatura e ferramentas recentes usam pelo menos três níveis de rigor:

```text
SPEC-FIRST
SPEC-ANCHORED
SPEC-AS-SOURCE
```

Uma análise de 2026 descreve essas três formas como níveis de rigor distintos, enquanto IBM diferencia abordagens em que a especificação ancora a implementação daquelas em que ela assume posição ainda mais normativa. citeturn430705academia35turn430705search0

Thoughtworks também observa que o termo ainda está evoluindo, mas identifica como característica central o uso de uma especificação escrita antes do código e tratada como fonte de verdade compartilhada entre humano e IA. citeturn430705search12

Este projeto adotará conscientemente uma postura **mais forte que spec-anchored** para as partes críticas:

> **a especificação é a fonte normativa da intenção e do comportamento; código é uma implementação dessa intenção, não sua autoridade superior.**

Essa escolha não implica que todo detalhe técnico precise existir na especificação funcional.

---

# 4. O que "fonte de verdade" significa aqui

A expressão não significa:

> "um único arquivo contém absolutamente tudo."

A fonte de verdade é um **sistema de especificações relacionadas**.

Exemplo:

```text
Project Definition
       ↓
Requirements
       ↓
Architecture
       ↓
Design
       ↓
Implementation Plan
       ↓
Code
       ↓
Verification / Evals
```

Cada nível possui uma responsabilidade.

A fonte de verdade deve responder:

```text
O que precisa existir?
Por que existe?
Quais restrições são obrigatórias?
Como sabemos que foi atendido?
```

Enquanto o design responde principalmente:

```text
Como materializar?
```

E o código responde:

```text
Qual implementação concreta foi executada?
```

---

# 5. Não é "documentação antes do código" apenas

SDD não deve ser reduzido a:

```text
escrever documentos
→ depois programar
```

O princípio é mais forte:

```text
especificar
→ revisar
→ derivar
→ implementar
→ verificar
→ manter alinhado
```

A especificação permanece viva durante a evolução.

A própria comunidade atual de SDD descreve o fluxo como uma cadeia contínua entre intenção, especificação explícita, implementação e evidência, e não como documentação descartável criada somente no início. citeturn430705search2turn430705search8

---

# 6. Hierarquia de artefatos

O projeto deve distinguir:

```text
NÍVEL 1 — INTENÇÃO
Project Definition / Objectives / Scope

NÍVEL 2 — ESPECIFICAÇÃO
Requirements / Rules / Constraints / Acceptance Criteria

NÍVEL 3 — ARQUITETURA
System Architecture / Boundaries / Responsibilities

NÍVEL 4 — DESIGN
Domain Model / Contracts / Interfaces / State / Data Structures

NÍVEL 5 — IMPLEMENTATION PLAN
Tasks / Work Units / Sequence / Dependencies

NÍVEL 6 — IMPLEMENTAÇÃO
Source Code / Configuration

NÍVEL 7 — VERIFICAÇÃO
Tests / Evals / Reviews

NÍVEL 8 — EVIDÊNCIA
Results / Telemetry / Acceptance / Operational Feedback
```

---

# 7. Relação entre níveis

A relação não é simplesmente linear.

Ela é:

```text
Intention
   ↓
Specification
   ↓
Architecture
   ↓
Design
   ↓
Plan
   ↓
Implementation
   ↓
Verification
   ↓
Evidence
   ↓
Feedback
   └──────────────→ Specification / Design / Plan
```

Feedback pode voltar ao menor nível necessário.

---

# 8. Princípio SD-001 — Especificação como fonte normativa

Uma especificação aprovada é a referência normativa para a implementação do comportamento que ela define.

Quando existir conflito:

```text
Specification
vs
Code
```

o conflito precisa ser analisado.

Não se assume automaticamente:

```text
Code = truth
```

nem:

```text
Specification = infalível
```

A especificação pode estar errada.

Mas a correção deve ser explícita e governada.

---

# 9. Princípio SD-002 — Código não corrige silenciosamente a especificação

Um desenvolvedor ou agente pode descobrir durante a implementação que:

```text
a especificação está incompleta
```

Nesse caso:

```text
descoberta
→ análise
→ atualização de especificação
→ revalidação
→ implementação
```

e não:

```text
descoberta
→ código inventa comportamento
```

---

# 10. Princípio SD-003 — Mudanças começam no nível adequado

Uma alteração deve ser registrada no menor artefato normativo capaz de expressar sua causa.

Exemplo:

```text
mudança de objetivo
→ Project Definition

mudança de comportamento
→ Requirement

mudança de estrutura
→ Architecture

mudança de contrato interno
→ Design

mudança somente de algoritmo interno
→ Design/Implementation
```

Nem toda mudança precisa subir até o nível de requisito.

---

# 11. Princípio SD-004 — Design não deve inventar comportamento

Design pode decidir:

```text
como
```

mas não deve inventar:

```text
o que
```

fora dos limites estabelecidos pela especificação.

Exemplo:

```text
Requirement:
"o sistema deve registrar uma decisão."

Design:
"DecisionRepository persistirá a decisão."
```

Está correto.

Mas:

```text
Design:
"o sistema apagará decisões após 30 dias."
```

é comportamento novo.

Se não estiver especificado e tiver impacto relevante, deve retornar à especificação.

---

# 12. Princípio SD-005 — Implementação deve ser derivável

Uma implementação deve ser justificável a partir de:

```text
Requirements
+
Architecture
+
Design
+
Implementation Plan
```

Se um trecho significativo não puder ser justificado por esses artefatos, deve existir uma análise de lacuna.

---

# 13. Princípio SD-006 — Nenhum requisito silencioso

Um requisito silencioso é comportamento implementado sem representação normativa suficiente.

Exemplo:

```text
código:
"se o custo passar de X, troca automaticamente de modelo."

mas:
não existe regra correspondente.
```

Isso é um problema de especificação.

Tratamento:

```text
detect
→ classify
→ specify
→ validate
→ implement
```

---

# 14. Princípio SD-007 — Verificação é contra a especificação

Um teste não deve perguntar somente:

> "o código funciona?"

Deve perguntar:

> **"o código implementa o comportamento especificado?"**

Assim:

```text
Requirement
→ Acceptance Criteria
→ Verification
```

Isso preserva o conceito já consolidado no projeto legado de separar requisito, critério e teste.

---

# 15. Princípio SD-008 — Evals verificam comportamento agentic

Para capacidades do Orchestrator que envolvam LLMs, testes convencionais não são suficientes.

Também precisamos de Evals para verificar:

- qualidade da decomposição;
- seleção de agente;
- seleção de modelo;
- qualidade da delegação;
- avaliação de resultado;
- replanejamento;
- respeito a políticas.

Portanto:

```text
Software Tests
+
Agent Evals
```

formam a estratégia de verificação do sistema.

---

# 16. Princípio SD-009 — Prompt não é especificação

Prompt é um mecanismo de instrução.

Especificação é um artefato persistente do projeto.

A relação é:

```text
Specification
→ Prompt Design
```

e não:

```text
Prompt
→ Specification
```

Um prompt pode conter apenas uma fração da especificação.

---

# 17. Princípio SD-010 — Skill não é especificação do projeto

Uma Skill representa conhecimento/procedimento reutilizável.

Ela pode implementar comportamentos exigidos pela especificação, mas:

```text
Skill ≠ Project Specification
```

Exemplo:

```text
Requirement:
"o sistema deve preservar dependências."

Skill:
procedimento para análise de dependências.
```

---

# 18. Princípio SD-011 — Policy não é prompt

Uma política crítica de segurança ou autorização não deve depender exclusivamente de uma instrução ao modelo.

Deve existir enforcement de software.

```text
Prompt
→ orientação

Policy
→ restrição aplicável

Software Enforcement
→ garantia operacional
```

---

# 19. Princípio SD-012 — Teste não substitui especificação

Um teste pode demonstrar:

```text
"para este exemplo, o sistema fez X."
```

Mas não necessariamente representa:

```text
"o sistema deve fazer X em todas as condições relevantes."
```

Portanto:

```text
Test
≠
Specification
```

Testes verificam a especificação.

---

# 20. Princípio SD-013 — Código pode revelar lacunas

SDD não significa que a especificação seja produzida uma única vez e congelada.

Durante implementação, pode surgir:

```text
edge case
contradição
ambiguidade
restrição não percebida
falha arquitetural
```

Isso produz feedback.

Fluxo:

```text
Implementation
→ discovery
→ specification/design feedback
→ controlled update
```

---

# 21. Princípio SD-014 — Especificação é evolutiva

Uma especificação pode mudar.

O que não pode acontecer é:

```text
spec v1
+
code v2
+
ninguém sabe por quê
```

A mudança deve possuir:

```text
motivo
impacto
versão
rastreabilidade
```

---

# 22. Princípio SD-015 — Versionamento

Todos os artefatos normativos relevantes devem ser versionáveis:

```text
Requirements
Architecture
Design
Policies
Skills
Prompts
Implementation Plans
```

O nível de formalidade deve ser proporcional ao impacto.

---

# 23. Princípio SD-016 — Baseline

Uma especificação aprovada pode constituir uma baseline.

Depois:

```text
baseline
→ implementation
```

e alterações relevantes exigem:

```text
change
→ impact analysis
→ updated baseline
```

Isso reutiliza diretamente o conceito de baseline do legado.

---

# 24. Princípio SD-017 — Baseline não é imutável

Baseline representa um compromisso válido em determinado estado.

Não representa verdade eterna.

---

# 25. Princípio SD-018 — Mudança tem impacto

Uma mudança de especificação deve considerar:

- Work Units afetadas;
- arquitetura afetada;
- design afetado;
- código afetado;
- testes afetados;
- Skills/prompt afetados;
- agentes afetados;
- dados afetados;
- documentação afetada.

O nível de análise deve ser proporcional.

---

# 26. Princípio SD-019 — Impacto não depende de tamanho textual

Uma alteração de uma linha pode alterar uma regra crítica.

Uma alteração de dezenas de linhas pode ser apenas reorganização.

Portanto:

```text
textual size
≠
semantic impact
```

Esse princípio já existe no Master e deve ser reutilizado diretamente.

---

# 27. Princípio SD-020 — Rastreabilidade bidirecional

A rastreabilidade deve permitir:

```text
Requirement
→ Design
→ Code
→ Test
→ Evidence
```

e:

```text
Evidence
→ Test
→ Code
→ Design
→ Requirement
```

Quando a profundidade justificar o custo.

---

# 28. Matriz de rastreabilidade

A estrutura conceitual:

| Requirement | Architecture | Design | Work Unit | Code | Test/Eval | Evidence |
|---|---|---|---|---|---|---|
| RF-001 | C-001 | ProjectState | WU-001 | ... | ... | ... |
| RF-027 | C-009/C-015 | DelegateWork | WU-027 | ... | ... | ... |
| RF-031 | C-010 | EvaluateResult | WU-031 | ... | ... | ... |

A matriz física poderá ser arquivo, banco, ferramenta ou sistema de links.

---

# 29. Critérios de qualidade de uma especificação

Uma especificação útil deve ser:

```text
clara
consistente
necessária
rastreável
verificável
suficiente
versionável
compreensível
```

Também deve evitar:

```text
ambiguidade
contradição
solução prematura
detalhe irrelevante
requisito implícito
```

IBM destaca que uma boa especificação deve ser clara e testável, conter entradas/saídas, casos de borda e critérios de sucesso quando necessários, mas permanecer leve o suficiente para evoluir conforme o problema fica mais compreendido. citeturn430705search0

---

# 30. Especificação deve evitar prescrição prematura

Sempre que possível:

```text
WHAT
```

antes de:

```text
HOW
```

Exemplo:

```text
Requirement:
"o sistema deve preservar o histórico relevante."

Design:
"usar Event Store."

Implementation:
"PostgreSQL..."
```

A decisão tecnológica deve aparecer no nível apropriado.

---

# 31. Exceção — requisitos técnicos legítimos

Às vezes o requisito pode ser técnico:

```text
"deve suportar TLS 1.3"
```

Isso é legítimo quando a origem for uma política, restrição ou necessidade real.

SDD não proíbe especificar tecnologia.

Ele proíbe antecipar tecnologia sem razão normativa.

---

# 32. Specification Units

Uma especificação não precisa ser um único arquivo.

Pode ser composta por:

```text
Project Definition
Requirements
Business Rules
Acceptance Criteria
Architecture Constraints
Security Requirements
API Contracts
Data Contracts
```

O importante é que suas relações sejam claras.

---

# 33. Living Specification

Uma especificação relevante deve ser tratada como **living specification** enquanto o projeto evolui.

Isso significa:

```text
read
→ review
→ update
→ validate
→ baseline
```

e não:

```text
write once
→ archive
→ code independently
```

---

# 34. Spec Change Workflow

Fluxo padrão:

```text
Change Request / Discovery
          ↓
Impact Analysis
          ↓
Specification Update
          ↓
Validation
          ↓
Architecture Review
          ↓
Design Update
          ↓
Plan Update
          ↓
Implementation
          ↓
Verification
```

Nem toda mudança precisa percorrer todos os níveis.

O fluxo é adaptativo.

---

# 35. Small Change Workflow

```text
small change
→ update spec
→ update code
→ focused verification
```

---

# 36. Medium Change Workflow

```text
medium change
→ impact
→ requirement/design update
→ affected Work Units
→ implementation
→ affected verification
```

---

# 37. Structural Change Workflow

```text
structural change
→ global/contextual impact
→ architecture update
→ design update
→ plan revision
→ implementation
→ broad verification
```

---

# 38. Critical Change Workflow

```text
critical change
→ stop affected work
→ impact analysis
→ human governance
→ updated specification
→ architecture/design review
→ controlled implementation
→ validation
```

---

# 39. Contradiction Workflow

Quando duas especificações conflitarem:

```text
Conflict
↓
Classify source
↓
Authority
↓
Evidence
↓
Impact
↓
Decision
↓
Update
↓
Revalidate
```

Não escolher silenciosamente.

---

# 40. Ambiguity Workflow

Quando um requisito for ambíguo:

```text
Ambiguity
↓
identify interpretations
↓
impact
↓
ask/decide if needed
↓
specification refinement
↓
validation
```

---

# 41. Missing Specification Workflow

Quando implementação exigir informação ausente:

```text
Missing Spec
↓
classify
↓
low impact?
    ├── yes → safe assumption only if authorized
    └── no → decision required
↓
record
↓
update spec
```

---

# 42. Spec Review

Antes de implementação, revisar:

```text
complete enough?
consistent?
verifiable?
traceable?
feasible?
within scope?
no hidden behavior?
```

---

# 43. Architecture Conformance

A arquitetura deve ser verificável contra a especificação.

Exemplo:

```text
Requirement:
runtime independent

Architecture:
Runtime Adapter
```

A arquitetura atende à restrição.

---

# 44. Design Conformance

O design deve ser verificável contra a arquitetura.

Exemplo:

```text
Architecture:
Domain independent from runtime

Design:
Domain imports no runtime packages
```

---

# 45. Code Conformance

O código deve ser verificável contra o design.

Exemplo:

```text
Design:
Delegation depends on AgentRuntime port

Code:
DelegationUseCase → AgentRuntime
```

Não:

```text
DelegationUseCase → OpenClaw SDK
```

---

# 46. Test Conformance

Os testes devem verificar os critérios relevantes.

```text
Requirement
→ Acceptance Criterion
→ Test / Eval
```

---

# 47. Evidence Conformance

A evidência deve permitir determinar:

```text
what was implemented
what was verified
under which configuration
with what result
```

---

# 48. Agent-Assisted Implementation

No desenvolvimento com agentes de IA:

```text
Agent receives:
specification
+
design
+
implementation task
+
constraints
+
acceptance criteria
```

Não deve receber apenas:

```text
"faça a funcionalidade X"
```

---

# 49. Context Package para desenvolvimento

Uma Work Unit de implementação deve possuir:

```text
TaskPackage
├── requirement references
├── design references
├── affected components
├── constraints
├── acceptance criteria
├── dependencies
├── expected artifacts
└── verification instructions
```

---

# 50. Agent Implementation Contract

O agente implementador deve retornar:

```text
ResultPackage
├── implemented changes
├── files/components changed
├── tests added/changed
├── assumptions
├── unresolved issues
├── specification deviations
└── verification results
```

---

# 51. Specification Deviation

Se o agente não conseguir seguir integralmente a especificação:

```text
DEVIATION
├── requirement
├── reason
├── impact
├── workaround
└── recommendation
```

A divergência não deve ficar escondida no código.

---

# 52. No Unauthorized Expansion

O agente de implementação não deve adicionar:

```text
feature
behavior
policy
integration
```

fora do escopo sem registrar a necessidade.

Isso controla scope creep.

---

# 53. No Unauthorized Simplification

Também não deve remover:

```text
requirement
validation
security constraint
```

simplesmente para facilitar implementação.

Se impossível:

```text
surface conflict
```

---

# 54. Implementation Plan

O plano de implementação deve ser derivado:

```text
Requirement
+
Architecture
+
Design
→
Work Units
```

As Work Units devem possuir dependências.

---

# 55. Dependency-Ordered Implementation

Exemplo:

```text
Domain Model
↓
Application Contract
↓
Adapter
↓
Integration
```

Não:

```text
OpenClaw Adapter
antes
de existir contrato interno
```

---

# 56. Spec-Driven Definition of Done

Uma Work Unit de implementação não será concluída apenas porque o código foi escrito.

Critério mínimo:

```text
specified
+
implemented
+
verified
+
reviewed
+
traceable
```

Quando aplicável:

```text
+
architecture conformance
+
tests/evals
+
documentation update
```

---

# 57. Code Review under SDD

Code Review deve perguntar:

```text
1. Está correto?
2. Atende à especificação?
3. Respeita o design?
4. Respeita arquitetura?
5. Há comportamento não especificado?
6. Há comportamento especificado que não foi implementado?
```

---

# 58. Specification Review under SDD

Review deve perguntar:

```text
1. O que queremos está claro?
2. Está suficientemente preciso?
3. Há ambiguidade?
4. Há dependências ocultas?
5. É verificável?
6. Está alinhado ao objetivo?
7. Está dentro do escopo?
```

---

# 59. Drift Detection

O sistema deverá ser capaz de detectar:

```text
Specification
≠
Implementation
```

em níveis diferentes:

```text
requirements drift
architecture drift
design drift
code drift
test drift
documentation drift
```

---

# 60. Types of Drift

### Requirement Drift

Código implementa comportamento não desejado.

### Design Drift

Código contradiz design aprovado.

### Architecture Drift

Implementação viola fronteiras arquiteturais.

### Test Drift

Testes deixam de representar critérios válidos.

### Documentation Drift

Documentação diverge do comportamento aprovado.

---

# 61. Drift Resolution

```text
Drift
↓
classify
↓
find source of change
↓
authority
↓
impact
↓
update correct artifact
↓
align downstream artifacts
```

---

# 62. Code as Evidence

Código não é a especificação.

Código é:

> **evidência da implementação de uma especificação.**

A equipe pode inspecionar o código para determinar o que foi realmente construído, mas a intenção continua sendo definida pelos artefatos normativos válidos.

---

# 63. Tests as Evidence

Testes também são evidência:

```text
Criterion
→ Test
→ Result
```

Um teste passando demonstra o resultado daquele teste.

Não prova sozinho que todo o sistema atende à intenção.

---

# 64. Runtime Results as Evidence

No sistema agentic:

```text
Execution
→ Outcome
→ Evaluation
→ Evidence
```

Isso é especialmente importante para escolhas de:

```text
Agent
Skill
Model
Delegation Strategy
```

---

# 65. Evals como evidence of agentic behavior

Evals podem demonstrar:

```text
Orchestrator chose reasonable agent
Orchestrator respected dependency
Orchestrator detected failure
Orchestrator replanned
```

A evidência deve estar vinculada à especificação do comportamento esperado.

---

# 66. Spec-driven versus test-driven

SDD e TDD não são concorrentes.

Relação:

```text
Specification
      ↓
Acceptance Criteria
      ↓
Tests
      ↓
Implementation
```

Em desenvolvimento de código:

```text
SDD
+
TDD where appropriate
```

é compatível.

---

# 67. Spec-driven versus BDD

BDD pode fornecer uma forma de especificação executável para comportamentos:

```text
Given
When
Then
```

Mas nem toda especificação precisa usar BDD.

O formato deve ser proporcional à necessidade.

---

# 68. Spec-driven versus API contracts

OpenAPI, schemas, interface contracts e outros contratos formais podem ser **subespecificações** dentro do sistema SDD.

Exemplo:

```text
Requirement
→ API Contract
→ Code
→ Integration Test
```

---

# 69. Spec-driven versus ADR

ADR documenta:

```text
why a design decision was made
```

Não substitui requisito.

Relação:

```text
Requirement
→ Architectural alternatives
→ ADR
→ Design
```

---

# 70. Spec-driven versus prompts

Prompt é uma instrução de execução.

Pode ser derivado de:

```text
requirements
design
role
policy
skill
task
```

Portanto:

```text
Specification
→ Prompt
```

e não o inverso como regra normativa.

---

# 71. Spec-driven versus Skills

Skill é um mecanismo de especialização.

Pode conter:

```text
procedures
rules
references
examples
templates
```

e ser usada para implementar uma parte da especificação.

---

# 72. Spec-driven versus AGENTS / system instructions

Arquivos como:

```text
AGENTS.md
system instructions
```

podem carregar instruções persistentes de operação do agente.

Mas não devem substituir a especificação específica do projeto.

---

# 73. Specification scope

Existem pelo menos:

```text
Project Specification
Feature Specification
Work Unit Specification
API Specification
Data Specification
Security Specification
Operational Specification
```

A hierarquia deve ser explícita.

---

# 74. Specification precedence

Quando múltiplas especificações existirem:

```text
Higher-level constraints
        ↓
Project requirements
        ↓
Feature/work-unit specification
        ↓
Design
        ↓
Implementation
```

Detalhes específicos não devem violar restrições superiores.

---

# 75. Conflict resolution across specs

Quando:

```text
Feature Spec
contradiz
Project Requirement
```

a especificação inferior não pode simplesmente prevalecer.

Fluxo:

```text
conflict
→ identify authority
→ impact
→ reconcile
→ update
```

---

# 76. Specification completeness

Não buscar completude absoluta.

Usar:

```text
sufficient completeness
```

perguntando:

```text
Há informação suficiente para implementar e verificar
sem inventar decisões críticas?
```

Isso é coerente com o princípio de suficiência do legado.

---

# 77. Specification granularity

Não criar especificações para cada microdetalhe.

Uma unidade de especificação deve existir quando melhora:

- clareza;
- execução;
- validação;
- rastreabilidade;
- decisão.

Isso também reaproveita diretamente a regra de granularidade do Master.

---

# 78. Specification lifecycle

```text
DRAFT
↓
REVIEW
↓
APPROVED
↓
BASELINED
↓
IMPLEMENTED
↓
VERIFIED
↓
ACTIVE
↓
CHANGED
↓
SUPERSEDED / UPDATED
```

---

# 79. Specification states

Estados conceituais:

```text
PROPOSED
UNDER_REVIEW
APPROVED
BASELINED
IMPLEMENTED
VERIFIED
SUPERSEDED
REJECTED
BLOCKED
```

Nem todos precisam existir no primeiro runtime.

---

# 80. Approval

Aprovação significa:

```text
suficiente para avançar
```

não:

```text
perfeito para sempre
```

---

# 81. Baseline management

Uma baseline aprovada deve registrar:

```text
version
scope
date
authority
affected artifacts
```

---

# 82. Specification update

Atualizações relevantes devem preservar:

```text
old version
new version
change reason
impact
decision
```

---

# 83. Regeneration mindset

Em uma abordagem fortemente spec-driven, partes do sistema podem ser reconstruídas a partir da especificação e do design.

Não significa que:

```text
todo código = gerado automaticamente
```

Significa que:

```text
specification remains the durable intent
```

mesmo quando implementação for artesanal.

GitHub Spec Kit descreve essa inversão de forma forte: especificação e planos tornam-se artefatos que dirigem a implementação, enquanto o código é expressão concreta em uma linguagem/framework. citeturn430705search1

---

# 84. Spec as software medium

A prática contemporânea de SDD trata especificações como artefatos técnicos que podem guiar pessoas, agentes, implementação e verificação, não apenas como documentos administrativos. citeturn430705search2

Para este projeto, isso significa que nossas especificações precisam ser:

```text
estruturadas
versionadas
rastreáveis
consultáveis
verificáveis
```

---

# 85. AI-friendly specification

Uma especificação destinada também a agentes deve:

- evitar ambiguidades;
- definir termos;
- explicitar restrições;
- definir entradas;
- definir saídas;
- indicar critérios;
- indicar dependências;
- separar fatos de hipóteses;
- apontar referências.

Isso melhora a capacidade do agente de agir sem reconstruir intenção de conversas dispersas. Microsoft identifica justamente a perda de significado entre handoffs como um problema central em desenvolvimento com IA. citeturn430705search5

---

# 86. Context package for an AI coder

Antes de delegar implementação:

```text
Implementation Context
├── relevant specification
├── relevant architecture
├── relevant design
├── relevant Work Unit
├── constraints
├── acceptance criteria
├── tests/evals
└── references
```

Isso é uma aplicação direta do SDD ao nosso futuro Orchestrator.

---

# 87. Minimal implementation context

Não mandar:

```text
todo o projeto
```

por padrão.

Enviar:

```text
necessário para a Work Unit
+
referências
```

mantendo acesso ao restante quando necessário.

---

# 88. Agent output under SDD

Todo agente implementador deverá distinguir:

```text
implemented
verified
assumed
deviated
blocked
recommended
```

Isso facilita avaliação.

---

# 89. Deviation approval

Quando houver desvio:

```text
Deviation
→ impact
→ recommendation
→ decision
→ spec/design update
```

O código não deve ser considerado final enquanto a divergência relevante não estiver resolvida.

---

# 90. Spec-driven debugging

Quando houver bug:

```text
Observed Failure
↓
Does spec require this behavior?
├── yes → implementation defect
└── no → specification/design question
```

Isso muda a qualidade do diagnóstico.

---

# 91. Spec-driven refactoring

Refatoração deve preservar o comportamento especificado.

```text
refactor
→ same specification
→ same acceptance criteria
→ new implementation
```

Se o comportamento mudar:

```text
not merely refactoring
→ change
```

---

# 92. Spec-driven feature development

Fluxo:

```text
Need
↓
Specification
↓
Review
↓
Architecture impact
↓
Design
↓
Implementation Plan
↓
Implementation
↓
Verification
↓
Evidence
```

---

# 93. Spec-driven bug fixing

Fluxo:

```text
Failure
↓
Reproduce
↓
Check specification
↓
Classify
↓
Implementation fix
or
Specification fix
↓
Verification
```

---

# 94. Spec-driven architecture evolution

Fluxo:

```text
New requirement
↓
Impact
↓
Architecture decision
↓
ADR
↓
Design update
↓
Implementation
↓
Verification
```

---

# 95. Spec-driven model change

No nosso projeto:

```text
Model X
→ Model Y
```

não é necessariamente uma simples configuração.

Se a mudança alterar:

- qualidade esperada;
- contexto;
- custo;
- comportamento;
- segurança;

a especificação operacional ou de recursos pode precisar de atualização.

---

# 96. Spec-driven Skill change

Se uma Skill for modificada:

```text
Skill v1
→ Skill v2
```

deve ser possível avaliar:

```text
quais agentes
quais Work Units
quais resultados
```

foram afetados.

---

# 97. Spec-driven prompt change

Prompts também podem ser versionados.

Exemplo:

```text
Orchestrator Prompt v1
→ v2
```

e a mudança pode ser avaliada por Evals.

---

# 98. Prompt experiment

Um experimento pode comparar:

```text
Prompt A
vs.
Prompt B
```

contra a mesma especificação e conjunto de Evals.

O objetivo é melhorar implementação sem alterar a intenção especificada.

---

# 99. Spec-driven agent selection

A escolha do agente deve derivar da Work Unit especificada:

```text
Work Unit Specification
→ required capability
→ Skill
→ Agent
```

Não:

```text
Agent available
→ invent Work Unit
```

---

# 100. Spec-driven model selection

O modelo também deve ser derivado de requisitos:

```text
Requirement / Work Unit
→ quality/complexity/context constraints
→ eligible models
→ selection
```

---

# 101. Spec-driven evaluation

A avaliação deve usar:

```text
Specification
+
Acceptance Criteria
+
Evidence
```

e não apenas:

```text
"o resultado parece bom."
```

---

# 102. Spec-driven replanning

Uma mudança no plano deve continuar vinculada à intenção:

```text
spec
→ current architecture/design
→ current plan
→ new constraints
→ revised plan
```

Replanning não pode criar um objetivo novo sem especificação correspondente.

---

# 103. Spec-driven learning

Learning pode sugerir:

```text
"this pattern should become a rule"
```

mas a promoção segue:

```text
candidate
→ specification/methodology review
→ approval
→ new rule/Skill/prompt
```

---

# 104. Spec-driven governance

Governança deve proteger:

```text
specification
architecture constraints
policies
approval thresholds
security
traceability
```

O agente não pode "aprender" para contornar esses elementos.

---

# 105. Human role

Com SDD, o papel humano sobe de:

```text
line-by-line coding
```

para:

```text
intent
constraints
architecture
trade-offs
approval
evaluation
```

Isso não elimina a necessidade de revisão humana.

---

# 106. Orchestrator role

O futuro Orchestrator deverá atuar como:

```text
specification interpreter
+
planner
+
delegator
+
evaluator
+
governor
```

e não apenas:

```text
prompt router
```

---

# 107. Specification as shared context

A mesma especificação pode ser consumida por:

```text
Orchestrator
Architecture Agent
Requirements Agent
Implementation Agent
Testing Agent
Documentation Agent
Reviewer
```

Isso reduz a quantidade de interpretação independente.

---

# 108. Shared vocabulary

O sistema deve manter terminologia consistente.

Exemplo:

```text
Work Unit
```

não deve ser chamada alternativamente de:

```text
task
job
activity
subtask
```

sem definir a diferença.

---

# 109. Specification references

Os artefatos podem referenciar uns aos outros:

```text
RF-ORC-027
→ UC-ORC-006
→ DelegateWork
→ AgentRuntime
→ OpenClawAdapter
```

Isso transforma a documentação em uma rede coerente.

---

# 110. Specification graph

Conceitualmente:

```text
Specification Graph
├── Objectives
├── Requirements
├── Constraints
├── Decisions
├── Architecture
├── Design
├── Work Units
├── Tests
├── Evals
└── Evidence
```

Esse grafo será importante para o Orchestrator futuramente.

---

# 111. Dependency graph versus specification graph

São diferentes.

### Dependency Graph

Representa:

```text
A depends on B
```

### Specification Graph

Representa:

```text
A specifies B
B implemented by C
C verified by D
```

Podem se relacionar, mas não são o mesmo modelo.

---

# 112. Change propagation

Quando:

```text
Requirement R1
```

muda, o sistema deve conseguir identificar:

```text
Architecture A
Design D
Work Units W
Code C
Tests T
Evals E
```

afetados.

Essa é uma das aplicações mais importantes da rastreabilidade.

A literatura recente destaca justamente a importância de conectar requisitos ao produto final e observa que ferramentas de rastreabilidade ainda possuem lacunas de cobertura ao longo do ciclo. citeturn430705search9

---

# 113. Impact propagation

Nem todo elemento ligado diretamente é necessariamente afetado.

O Orchestrator deve analisar:

```text
relation
+
semantic dependency
```

e não apenas grafo textual.

---

# 114. Change review

Antes de aceitar uma mudança relevante:

```text
what changes?
why?
what breaks?
what must be rebuilt?
what remains valid?
```

---

# 115. Partial implementation

Se apenas parte da especificação estiver implementada:

```text
Requirement
→ partial coverage
```

o sistema deve representar o estado.

Não marcar como totalmente concluído.

---

# 116. Partial verification

Pode existir:

```text
implemented
but not fully verified
```

Isso deve ser diferente de:

```text
verified
```

---

# 117. Completion hierarchy

```text
Requirement
→ Implementation
→ Verification
→ Acceptance
→ Complete
```

Essa estrutura é consistente com o modelo de conclusão já estabelecido no legado.

---

# 118. No false completion

O Orchestrator não deve afirmar:

```text
"feature complete"
```

quando:

```text
implementation exists
but acceptance not verified
```

---

# 119. Specification debt

Uma nova categoria útil é:

```text
Specification Debt
```

quando:

- comportamento importante está implícito;
- decisão não documentada;
- critérios ausentes;
- requisitos ambíguos.

Specification debt deve ser tratada como fonte de risco e retrabalho.

---

# 120. Technical debt versus specification debt

```text
Specification Debt
→ falta de clareza/intenção formalizada

Technical Debt
→ custo de uma decisão/implementação técnica
```

Podem existir independentemente.

---

# 121. Specification quality metrics

Possíveis métricas:

```text
unresolved ambiguities
requirements without acceptance criteria
requirements without traceability
implementation deviations
verification coverage
change frequency
rework caused by missing spec
```

Esses indicadores devem servir para melhoria, não como métricas absolutas de qualidade.

---

# 122. Verification coverage

Uma métrica conceitual:

```text
requirements with verification
/
requirements requiring verification
```

---

# 123. Traceability coverage

```text
requirements linked to implementation
+
verification
/
requirements requiring traceability
```

---

# 124. Drift rate

Pode ser observado:

```text
specification changes
vs.
unexpected implementation behavior
```

Não deve ser tratado como métrica universal.

---

# 125. Rework caused by specification

Registrar:

```text
rework
→ root cause
→ specification issue?
```

Isso alimenta aprendizado.

---

# 126. Specification lifecycle with agents

O Orchestrator pode gerenciar:

```text
Draft
→ Review
→ Approval
→ Baseline
→ Implementation
→ Verification
→ Evolution
```

Isso se torna parte do próprio domínio de Project Management.

---

# 127. Specialist specification agents

Futuras Skills/agentes podem atuar sobre partes:

```text
Requirements Agent
→ requirement specification

Architecture Agent
→ architectural specification

API Agent
→ contract specification

Testing Agent
→ verification specification
```

O Orchestrator integra essas partes.

---

# 128. Specification reviewer

Um agente revisor pode comparar:

```text
Specification
vs.
Design
vs.
Implementation
```

e gerar:

```text
Conformance Report
```

---

# 129. Conformance Report

Estrutura conceitual:

```text
Requirement
├── expected
├── implementation
├── verification
├── evidence
├── conformance
└── deviation
```

---

# 130. Specification acceptance

Uma specification pode possuir critérios de aceitação próprios:

```text
clear
consistent
traceable
verifiable
sufficient
approved
```

---

# 131. Architecture acceptance

Architecture também:

```text
requirements covered
boundaries coherent
trade-offs explicit
constraints respected
```

---

# 132. Design acceptance

Design:

```text
architecture respected
contracts defined
state defined
testable
implementable
```

---

# 133. Implementation acceptance

Implementation:

```text
requirements covered
tests pass
evals pass where applicable
no unresolved critical deviations
```

---

# 134. Release acceptance

Release:

```text
specified
implemented
verified
operationally observed
known risks documented
```

---

# 135. Operational feedback loop

Depois do uso real:

```text
Operation
→ Quality
→ Efficiency
→ Incidents
→ Rework
→ Learning
→ Specification / Skill / Prompt updates
```

Isso conecta diretamente a decisão que já tomamos sobre o pós-integração real do Orchestrator.

---

# 136. SDD e o ciclo operacional do nosso projeto

A partir da Fase 10:

```text
Integrated System
        ↓
Real Service
        ↓
Observed Outcome
        ↓
Evaluation
        ↓
Evidence
        ↓
Learning Candidate
        ↓
Possible Spec / Skill / Prompt improvement
```

Isso torna a especificação viva também depois da implementação.

---

# 137. SDD e versionamento Git

Git não serve apenas para guardar código.

Deve versionar:

```text
specification
architecture
design
Skills
prompts
tests/evals
implementation
```

Cada alteração relevante deve poder ser relacionada.

---

# 138. Commit discipline

Mudanças de comportamento devem evitar:

```text
code-only commit
```

quando a mudança exigir atualização da especificação.

Preferir commits semanticamente agrupados:

```text
spec:
docs:
feat:
test:
```

conforme a natureza da alteração e o workflow do projeto.

---

# 139. Review hierarchy

Uma Pull Request relevante pode ser revisada em:

```text
Specification Review
Architecture Review
Design Review
Code Review
Verification Review
```

Nem toda mudança exige todos os níveis.

---

# 140. SDD and CI/CD

Futuramente a pipeline poderá verificar:

```text
architecture tests
unit tests
integration tests
evals
traceability checks
spec validation
```

antes da promoção de uma versão.

---

# 141. SDD and automated agents

Um agente de implementação deverá receber como contexto mínimo:

```text
spec fragment
design fragment
work unit
criteria
```

e não apenas o prompt textual do usuário.

---

# 142. SDD and model selection

Modelos diferentes podem ser escolhidos para diferentes etapas:

```text
Requirements Agent
→ model suitable for analysis

Architecture Agent
→ high reasoning capability

Implementation Agent
→ coding optimized

Review Agent
→ independent evaluation
```

O critério continua sendo a especificação e a Work Unit.

---

# 143. SDD and economicity

Spec-driven não significa especificação infinita.

Uma especificação excessivamente detalhada pode aumentar custo sem produzir benefício.

Princípio:

```text
specification detail
∝
risk + complexity + impact + need for verification
```

Isso combina diretamente com o princípio de suficiência do nosso legado.

---

# 144. SDD and autonomy

Quanto mais crítica a mudança:

```text
mais explícita
mais verificável
mais governada
```

deve ser a especificação.

Isso permite manter autonomia em mudanças simples sem sacrificar controle em mudanças críticas.

---

# 145. SDD and human intervention

Quando existir ambiguidade material:

```text
specification ambiguity
→ decision request
```

O Orchestrator deve preparar:

```text
question
context
alternatives
impact
recommendation
```

---

# 146. SDD and unknown impact

Se uma mudança não puder ser avaliada:

```text
IMPACT UNKNOWN
```

não deve ser implementada automaticamente quando o risco for relevante.

---

# 147. SDD and reversibility

Quando possível:

```text
spec version
→ implementation version
→ verification evidence
```

deve permitir rollback ou reconstrução.

---

# 148. SDD and architecture fitness

A arquitetura deve continuar atendendo às especificações ao longo do tempo.

Não basta passar testes funcionais.

Também pode ser necessário:

```text
architecture conformance
```

---

# 149. SDD and code cleanliness

Código limpo não é objetivo independente da especificação.

A combinação correta é:

```text
Correct behavior
+
Correct architecture
+
Clean implementation
```

O código deve ser bem estruturado dentro das restrições especificadas.

---

# 150. SDD and SOLID

SOLID atua no nível de design/código.

SDD atua principalmente na relação:

```text
intention
→ specification
→ implementation
→ verification
```

Eles são complementares.

---

# 151. SDD and Clean Architecture

Clean Architecture define:

```text
como organizar dependências
```

SDD define:

```text
como manter intenção alinhada à implementação
```

Combinação:

```text
SDD
+
Clean Architecture
```

é apropriada para este projeto.

---

# 152. SDD and DDD

DDD ajuda a definir:

```text
linguagem
modelo
limites
regras
```

SDD ajuda a tornar essas decisões explícitas, versionadas e rastreáveis ao longo da implementação.

---

# 153. SDD and Testing

TDD pode ser aplicado dentro de Work Units específicas:

```text
Specification
→ Acceptance
→ Test
→ Implementation
```

Não há conflito.

---

# 154. SDD and documentation

Documentação deve ser derivada ou ancorada na especificação quando representar comportamento atual.

Evitar documentação independente que possa divergir silenciosamente.

---

# 155. SDD and API documentation

Contratos como OpenAPI podem ser tratados como especificações técnicas executáveis/verificáveis.

Fluxo:

```text
API Requirement
→ API Contract
→ Implementation
→ Contract Test
```

---

# 156. SDD and Data

Da mesma forma:

```text
Data Requirement
→ Data Model
→ Persistence Model
→ Migration
→ Verification
```

---

# 157. SDD and Security

Segurança deve ser especificada de modo explícito quando relevante:

```text
Security Requirement
→ Architecture Constraint
→ Design
→ Code
→ Security Test
```

---

# 158. SDD and Observability

Requisitos de observabilidade:

```text
Requirement
→ telemetry contract
→ instrumentation
→ monitoring
→ operational evidence
```

---

# 159. SDD and failures

Falhas também podem produzir atualização da especificação.

Exemplo:

```text
production failure
→ requirement gap?
→ architecture gap?
→ implementation defect?
```

A análise deve identificar a raiz.

---

# 160. SDD and root cause

Não assumir:

```text
bug
→ developer mistake
```

Pode ser:

```text
ambiguous spec
wrong design
missing constraint
bad model choice
bad context
implementation defect
```

Esse diagnóstico é central para a aprendizagem do Orchestrator.

---

# 161. SDD and postmortem

Após incidente:

```text
Incident
→ Root Cause
→ Specification impact
→ Design impact
→ Implementation impact
→ Corrective action
```

---

# 162. SDD and learning candidate

Se uma falha revelar um padrão:

```text
pattern
→ LearningCandidate
```

Depois:

```text
validation
→ possible specification/rule update
```

---

# 163. SDD and multi-agent consistency

Todos os agentes que trabalham sobre um projeto devem receber uma referência comum à especificação relevante.

Isso reduz:

```text
Agent A understands X
Agent B understands Y
```

quando ambos deveriam executar a mesma intenção.

---

# 164. Shared project specification

A especificação do projeto deve funcionar como:

```text
shared contract
```

entre:

```text
Orchestrator
Agents
Reviewers
Human
```

---

# 165. Specialist autonomy under SDD

Um especialista pode decidir:

```text
como executar
```

desde que respeite:

```text
specified behavior
constraints
architecture
policies
```

Essa é a fronteira adequada entre autonomia e governança.

---

# 166. Agent creativity under SDD

SDD não deve eliminar criatividade do agente.

Pode existir:

```text
specification constrains intent
agent explores implementation
```

O agente pode descobrir uma solução melhor, mas quando ela alterar o comportamento ou decisões arquiteturais relevantes:

```text
propose
→ review
→ update
```

---

# 167. Spec-driven experimentation

Experimentos podem ocorrer sem alterar a baseline:

```text
baseline spec
        ↓
experimental branch / hypothesis
        ↓
test
        ↓
evidence
        ↓
accept / reject
```

Isso permite evolução sem contaminar imediatamente o estado oficial.

---

# 168. Experimental versus normative

Distinguir:

```text
NORMATIVE
```

de:

```text
EXPERIMENTAL
```

Conhecimento experimental não deve ser tratado como regra oficial.

---

# 169. Specification branching

Para mudanças importantes, pode existir:

```text
Baseline v1
   ├── Experiment A
   └── Experiment B
```

Depois:

```text
A accepted
→ baseline v2
```

---

# 170. Spec merge

Quando experimentos convergirem:

```text
compare
→ evidence
→ choose
→ consolidate
```

---

# 171. Specification archival

Quando uma especificação deixar de ser válida:

```text
SUPERSEDED
```

não:

```text
deleted
```

quando o histórico justificar preservação.

---

# 172. Specification lineage

Manter:

```text
v1
↓
v2
↓
v3
```

permite saber como o comportamento evoluiu.

---

# 173. Specification ownership

Cada especificação relevante deve possuir:

```text
owner
authority
scope
version
status
```

---

# 174. Specification authority

Nem toda documentação possui a mesma autoridade.

Exemplo:

```text
Approved Requirement
>
draft note
```

O sistema deve distinguir.

---

# 175. Spec confidence

Uma especificação pode possuir confiança diferente conforme o nível:

```text
Confirmed
Proposed
Draft
Experimental
```

---

# 176. Spec and uncertainty

Se algo permanece desconhecido:

```text
UNKNOWN
```

não transformar em requisito inventado.

Se for necessário avançar:

```text
assumption
+
impact
+
owner
+
validation plan
```

---

# 177. Assumption handling

Uma premissa utilizada para implementação deve ser registrada.

Se tornar-se falsa:

```text
replan
```

---

# 178. Specification gates

Podem existir gates:

```text
Spec Gate
Architecture Gate
Design Gate
Implementation Gate
Verification Gate
Release Gate
```

Não precisam ser universais.

O rigor deve ser proporcional.

---

# 179. Spec gate criteria

Uma specification gate pode exigir:

```text
clarity
consistency
traceability
verifiability
authority
sufficiency
```

---

# 180. Architecture gate

Pode exigir:

```text
requirements covered
constraints respected
boundaries clear
major trade-offs recorded
```

---

# 181. Design gate

Pode exigir:

```text
components defined
contracts defined
state defined
persistence strategy defined
test strategy defined
```

---

# 182. Implementation gate

Pode exigir:

```text
code exists
requirements covered
tests pass
architecture tests pass
no critical deviation
```

---

# 183. Verification gate

Pode exigir:

```text
acceptance criteria met
tests/evals sufficient
known risks recorded
```

---

# 184. Release gate

Pode exigir:

```text
implementation
verification
documentation
operational readiness
rollback
observability
```

---

# 185. SDD quality gate

Antes de qualquer implementação significativa:

```text
Specification usable?
```

Se não:

```text
do not code yet
```

salvo trabalho exploratório explicitamente classificado.

---

# 186. Discovery exception

Pode haver prototipagem antes da especificação final.

Isso deve ser classificado como:

```text
spike / exploration
```

e não tratado como implementação normativa.

---

# 187. Spike workflow

```text
Unknown
→ Spike
→ Evidence
→ Decision
→ Specification
→ Real implementation
```

Isso permite explorar sem quebrar SDD.

---

# 188. Research exception

Pesquisa técnica também pode preceder especificação final quando necessária para reduzir incerteza.

Fluxo:

```text
Question
→ Research
→ Evidence
→ Decision
→ Spec
```

---

# 189. Prototype versus production

Protótipo:

```text
exploratory
```

Produção:

```text
specification-backed
```

A passagem deve ser explícita.

---

# 190. SDD and legacy knowledge

O projeto legado já possui elementos que se encaixam diretamente:

```text
requirements
acceptance criteria
traceability
validation
baseline
impact
reopening
evidence
governance
```

Esses componentes serão reaproveitados como fundamentos.

A diferença é que o novo projeto os conecta explicitamente ao ciclo de agentes de IA e à implementação assistida por agentes.

---

# 191. SDD and current project artifacts

Nossa sequência atual já pode ser interpretada como:

```text
PROJECT-DEFINITION
        ↓
CAPABILITIES
        ↓
KNOWLEDGE MAP
        ↓
REQUIREMENTS
        ↓
SYSTEM ARCHITECTURE
        ↓
SYSTEM DESIGN
```

O que faltava era tornar explícito que:

```text
esses artefatos são normativos
```

e que a implementação será derivada deles.

---

# 192. New artifact hierarchy

A estrutura conceitual atual passa a ser:

```text
PROJECT-DEFINITION.md
        ↓
ORCHESTRATOR-CAPABILITIES.md
        ↓
ORCHESTRATOR-KNOWLEDGE-MAP.md
        ↓
ORCHESTRATOR-REQUIREMENTS.md
        ↓
ORCHESTRATOR-SYSTEM-ARCHITECTURE.md
        ↓
ORCHESTRATOR-SYSTEM-DESIGN.md
        ↓
ORCHESTRATOR-SPEC-DRIVEN-DEVELOPMENT.md
        ↓
Implementation Plan / Work Units
        ↓
Code
        ↓
Tests / Evals
        ↓
Evidence
```

---

# 193. SDD artifact status

Os artefatos normativos devem possuir:

```text
Draft
Review
Approved
Baselined
Superseded
```

---

# 194. Specification repository

O conhecimento normativo deve permanecer:

```text
version controlled
searchable
referenceable
auditable
```

Git é adequado para isso no contexto atual.

---

# 195. Specification identifiers

Elementos importantes devem ter IDs estáveis.

Exemplo:

```text
RF-ORC-027
RNF-ORC-005
RO-014
UC-ORC-006
```

Isso permite rastreabilidade.

---

# 196. Stable IDs

IDs devem permanecer estáveis mesmo quando o texto for refinado, salvo quando o significado do requisito mudar completamente.

---

# 197. Requirement splitting

Quando um requisito se tornar grande demais:

```text
RF-001
→ RF-001A
→ RF-001B
```

ou novos IDs, conforme o sistema de versionamento adotado.

A relação histórica deve ser preservada.

---

# 198. Requirement merging

Quando dois requisitos forem consolidáveis:

```text
RF-010
RF-011
→ RF-020
```

preservar histórico da consolidação.

---

# 199. Deletion

Um requisito removido deve ser marcado como:

```text
SUPERSEDED
```

ou outro estado histórico apropriado, quando rastreabilidade exigir.

---

# 200. Traceability automation

No futuro, ferramentas podem validar:

```text
Requirement has design?
Requirement has Work Unit?
Work Unit has implementation?
Implementation has verification?
```

Isso será especialmente útil para o Orchestrator.

---

# 201. Spec linting

Pode existir validação automatizada de:

- IDs;
- links;
- referências;
- campos obrigatórios;
- inconsistências;
- duplicações.

---

# 202. Spec schema

No futuro, partes da especificação poderão possuir schema estruturado.

Exemplo:

```yaml
id:
type:
statement:
source:
priority:
constraints:
acceptance:
status:
```

A forma final dependerá da ferramenta escolhida.

---

# 203. Natural language plus structure

A melhor abordagem para este projeto provavelmente será híbrida:

```text
Markdown
+
structured metadata
+
schemas where needed
```

Isso preserva legibilidade humana e processamento por agentes.

---

# 204. Executable specification

Alguns requisitos podem ser transformados em checks executáveis.

Exemplo:

```text
Requirement:
"Domain must not depend on Infrastructure."

Executable architecture test:
fail if forbidden import exists.
```

---

# 205. Executable acceptance criteria

Quando possível:

```text
Acceptance Criterion
→ automated test
```

Isso cria uma ponte muito forte entre intenção e verificação.

---

# 206. Human-readable and machine-readable

Uma boa especificação deve ser:

```text
compreensível para humanos
```

e, quando justificável:

```text
estruturada para agentes / ferramentas
```

---

# 207. Agent-readable specification

Agentes devem conseguir encontrar:

```text
requirements
constraints
decisions
references
```

sem depender de uma conversa antiga.

---

# 208. Prompt assembly from spec

No futuro:

```text
Spec Fragment
+
Design Fragment
+
Work Unit
+
Skill
+
Policy
→
Agent Context
```

O prompt não precisa conter toda a especificação.

---

# 209. Spec retrieval

O Orchestrator deve recuperar apenas a parte relevante:

```text
Work Unit
→ affected requirements
→ design references
→ constraints
```

Isso reduz contexto.

---

# 210. Specification access control

Nem todo agente precisa acessar todo o projeto.

O acesso deve ser proporcional à tarefa e política.

---

# 211. Spec freshness

Antes de executar, o agente deve verificar se está usando:

```text
current approved version
```

e não um documento obsoleto.

---

# 212. Spec lock

Durante uma execução crítica, pode ser necessário registrar:

```text
spec version used for execution
```

Assim o resultado pode ser interpretado corretamente.

---

# 213. Reproducibility package

Uma execução relevante pode preservar:

```text
spec version
architecture version
design version
Skill version
prompt version
model version
runtime
configuration
result
evaluation
```

Isso é valioso para diagnóstico.

---

# 214. Operational SDD

Depois do release:

```text
runtime behavior
→ evidence
→ spec conformance
→ improvement
```

A especificação continua viva.

---

# 215. SDD and observability

Telemetry deve ser capaz de ligar:

```text
Execution
→ Work Unit
→ Specification
```

---

# 216. SDD and cost optimization

Uma melhoria de custo não deve reduzir comportamento especificado sem decisão explícita.

Exemplo:

```text
cheaper model
→ same spec?
```

Se não:

```text
trade-off must be evaluated
```

---

# 217. SDD and model substitution

Trocar modelo é permitido quando:

```text
specification still satisfied
```

ou:

```text
change approved
```

---

# 218. SDD and runtime substitution

Trocar OpenClaw por Hermes:

```text
same project specification
+
same domain/application behavior
+
different adapter
```

é um dos benefícios da arquitetura definida.

---

# 219. SDD and portability

A portabilidade não significa que os runtimes sejam funcionalmente idênticos.

Significa:

```text
same core intent
+
adapter-specific implementation
```

---

# 220. SDD and future Skills

Uma nova Skill deve responder:

```text
qual necessidade resolve?
qual capacidade acrescenta?
qual especificação utiliza?
como será avaliada?
```

---

# 221. SDD and Skill versioning

Quando Skill mudar:

```text
Skill v1
→ Skill v2
```

deve ser possível avaliar impacto sobre agentes e Work Units.

---

# 222. SDD and prompt versioning

O mesmo vale para prompt.

Uma mudança de prompt é uma mudança de comportamento potencial e deve possuir avaliação correspondente.

---

# 223. SDD and model versioning

O resultado pode variar com versão do modelo.

Portanto:

```text
Model Version
```

faz parte da evidência operacional.

---

# 224. SDD and knowledge versioning

Conhecimento normativo:

```text
Knowledge v1
→ v2
```

deve permitir verificar quais execuções foram realizadas com qual versão.

---

# 225. SDD and learning promotion

Uma aprendizagem pode mudar:

```text
Skill
Prompt
Policy
Selection heuristic
```

mas a promoção deve ser explícita.

---

# 226. SDD and self-improving Orchestrator

O Orchestrator poderá melhorar-se, mas:

```text
learning
≠
automatic self-modification
```

O ciclo seguro é:

```text
observe
→ propose
→ evaluate
→ approve if required
→ version
→ deploy
→ monitor
```

---

# 227. SDD and protected core

Mudanças no núcleo protegido:

```text
security
authority
audit
traceability
policy
```

devem exigir governança específica.

---

# 228. SDD and autonomous coding

Autonomous coding deve significar:

```text
autonomous within approved specification
```

não:

```text
autonomous definition of what the system should become
```

---

# 229. SDD and human creativity

O humano continua responsável por:

```text
goals
trade-offs
authority
acceptance
strategic choices
```

A IA acelera:

```text
analysis
design exploration
implementation
testing
documentation
```

---

# 230. SDD and agent collaboration

Múltiplos agentes compartilham:

```text
Specification
+
Project State
+
relevant Context
```

para reduzir divergência.

---

# 231. Specification conflict between agents

Se agentes propuserem interpretações diferentes:

```text
compare against spec
```

A especificação é o ponto de referência antes de escolher a implementação.

---

# 232. Agent disagreement can reveal spec weakness

Quando dois agentes igualmente competentes interpretam algo de formas incompatíveis:

```text
disagreement
→ ambiguity signal
```

Pode ser necessário melhorar a especificação.

---

# 233. SDD and review agent

Um Review Agent pode verificar:

```text
spec conformance
architecture conformance
design conformance
implementation conformance
```

Isso cria uma especialização futura muito útil.

---

# 234. SDD and documentation agent

O agente de documentação pode produzir documentos derivados de:

```text
approved specification
+
architecture
+
current state
```

reduzindo divergência.

---

# 235. SDD and requirements agent

Requirements Agent pode manter:

```text
needs
requirements
acceptance
traceability
```

mas não deve alterar decisões estratégicas sem autoridade.

---

# 236. SDD and architecture agent

Architecture Agent recebe:

```text
requirements
constraints
quality attributes
```

e produz:

```text
architecture
trade-offs
ADRs
```

---

# 237. SDD and implementation agent

Implementation Agent recebe:

```text
spec
design
work unit
acceptance criteria
```

e produz:

```text
code
tests
evidence
```

---

# 238. SDD and testing agent

Testing Agent deriva:

```text
requirements
→ verification strategy
→ tests/evals
```

---

# 239. SDD and orchestrator

O Orchestrator assegura:

```text
spec
→ right specialist
→ right sequence
→ right context
→ right verification
```

---

# 240. Final Operating Model

O modelo que adotaremos será:

```text
              INTENT
                ↓
         SPECIFICATION
                ↓
          SPEC REVIEW
                ↓
          ARCHITECTURE
                ↓
             DESIGN
                ↓
       IMPLEMENTATION PLAN
                ↓
        AGENT DELEGATION
                ↓
          IMPLEMENTATION
                ↓
       TESTS + EVALS
                ↓
             EVIDENCE
                ↓
          ACCEPTANCE
                ↓
          OPERATION
                ↓
          FEEDBACK
                ↓
        LEARNING CANDIDATE
                ↓
       GOVERNED EVOLUTION
                ↺
```

---

# 241. Definition of SDD for this project

Para este projeto, **Specification-Driven Development** será definido como:

> **Uma disciplina de engenharia na qual a intenção validada do projeto é mantida em especificações explícitas, versionadas, rastreáveis e verificáveis, utilizadas para derivar arquitetura, design, planejamento e implementação; código, testes e resultados operacionais são tratados como implementações e evidências dessa intenção, e mudanças relevantes retornam ao nível apropriado da especificação antes de serem consolidadas.**

---

# 242. SDD Core Rules

As regras resumidas são:

```text
SD-001  Specification is normative
SD-002  Code does not silently redefine behavior
SD-003  Changes start at the appropriate specification level
SD-004  Design derives from specification
SD-005  Verification is against specification
SD-006  Traceability is bidirectional when justified
SD-007  No silent requirements
SD-008  Prompt is not specification
SD-009  Policy is not prompt
SD-010  Experience does not become rule automatically
SD-011  Baselines are versioned
SD-012  Impact controls propagation
SD-013  Specification remains evolvable
SD-014  AI agents operate within approved specification
SD-015  Experimental work is explicitly classified
SD-016  Evidence closes the loop
```

---

# 243. Acceptance Criteria of this Discipline

SDD estará adequadamente incorporado ao projeto quando:

```text
specifications are explicit
+
requirements are testable
+
architecture traces to requirements
+
design traces to architecture
+
implementation tasks trace to design/spec
+
tests/evals trace to criteria
+
results preserve evidence
+
changes propagate through the correct level
+
drift can be detected
+
learning is governed
```

---

# 244. Relation to Existing Project

A estrutura atual do projeto já contém grande parte dessa disciplina:

```text
PROJECT-DEFINITION
→ intent

ORCHESTRATOR-REQUIREMENTS
→ formal requirements

ORCHESTRATOR-SYSTEM-ARCHITECTURE
→ architectural constraints

ORCHESTRATOR-SYSTEM-DESIGN
→ implementation design
```

Este documento torna explícita a regra que conecta esses artefatos ao código futuro.

---

# 245. Relationship to Legacy

O projeto legado contribuiu diretamente com:

- separação entre problema, necessidade, requisito e solução;
- critérios de aceitação;
- rastreabilidade;
- validação da especificação;
- baseline;
- impacto;
- evidência;
- suficiência;
- governança;
- reabertura;
- evolução controlada.

Esses conceitos são compatíveis com a disciplina SDD e serão usados como fundamentos, não simplesmente copiados como estrutura física.

---

# 246. Decision

**Decisão:** O Adaptive AI Orchestrator adotará **Specification-Driven Development como disciplina transversal oficial de desenvolvimento e operação**, em uma forma forte de **spec-as-source-of-truth para intenção e comportamento**, adaptada à natureza evolutiva e agentic do sistema.

---

# 247. Limites da decisão

Esta decisão não significa:

```text
every implementation detail must be specified
```

nem:

```text
all code must be generated from specs automatically
```

nem:

```text
spec can never change
```

Significa:

```text
important intent must be explicit,
versioned,
reviewable,
traceable,
and verifiable.
```

---

# 248. Próximos impactos

A decisão deverá ser refletida posteriormente em:

```text
Implementation Plan
Agent contracts
Developer workflow
Git workflow
Testing
Evals
Prompt design
Skill design
Change management
Repository structure
CI/CD
```

---

# 249. Próximo passo

Antes de escrever código, deverá ser elaborado o:

**Implementation Plan**

que transformará:

```text
Requirements
+
Architecture
+
Design
+
SDD rules
```

em Work Units de implementação ordenadas por dependência.

---

# 250. Fechamento

O sistema passa a possuir quatro níveis complementares de disciplina:

```text
CLEAN ARCHITECTURE
→ protege dependências

DDD
→ protege o modelo do domínio

SOLID / CLEAN CODE
→ protege a qualidade interna do código

SPEC-DRIVEN DEVELOPMENT
→ protege a relação entre intenção e implementação
```

Juntos:

```text
INTENÇÃO
   ↓
SPECIFICATION
   ↓
ARCHITECTURE
   ↓
DESIGN
   ↓
IMPLEMENTATION
   ↓
VERIFICATION
   ↓
EVIDENCE
   ↓
LEARNING
   ↺
```

Esse ciclo será a base disciplinar para a implementação do Orchestrator e, posteriormente, para o próprio comportamento de desenvolvimento que o Orchestrator deverá supervisionar.
