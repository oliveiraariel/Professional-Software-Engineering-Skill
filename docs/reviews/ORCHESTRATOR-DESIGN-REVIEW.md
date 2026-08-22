# ORCHESTRATOR-DESIGN-REVIEW

**Projeto:** Adaptive AI Orchestrator  
**Documento revisado:** `ORCHESTRATOR-SYSTEM-DESIGN(1).md`  
**Resultado:** revisão arquitetural profunda  
**Versão proposta:** Design v0.2

---

# 1. Objetivo da revisão

Revisar o Design v0.1 contra:

- Clean Architecture;
- DDD;
- SOLID / Clean Code;
- Ports-and-Adapters;
- Specification-Driven Development;
- princípios de Deep Modules;
- Seam Discipline;
- Design It Twice;
- linguagem ubíqua;
- requisitos e capacidades já consolidados;
- conhecimento reutilizável do projeto legado.

A revisão não altera a arquitetura macro já aprovada. Ela procura principalmente **reduzir abstrações artificiais e aumentar a profundidade dos módulos**.

---

# 2. Resultado executivo

O Design v0.1 possui boa separação macro entre:

```text
Interface
→ Application
→ Domain
→ Infrastructure
```

Também estabelece independência de runtime, SDD, contratos, testes, observabilidade e integração com OpenClaw/Hermes. fileciteturn11file0L15-L25 fileciteturn11file4L791-L860

O principal problema identificado não está na arquitetura macro.

Está no risco de **excesso de abstrações e módulos rasos**.

O documento v0.1 lista numerosos ports e abstrações — repositórios, catálogos, runtime, conhecimento, ferramentas, clock e geração de IDs — antes de existir uma prova de que cada seam seja necessário. fileciteturn11file7L1588-L1627

A revisão portanto muda a regra de:

```text
"abstrair para manter flexível"
```

para:

```text
"abstrair quando um seam real produzir leverage, locality ou isolamento relevante."
```

---

# 3. Achado crítico — ports especulativos

## Problema

O v0.1 tratava `ProjectRepository`, `WorkUnitRepository`, `DecisionRepository`, `EvaluationRepository`, `LearningRepository`, `EventStore`, `ModelCatalog`, `SkillCatalog`, `AgentCatalog`, `KnowledgeProvider`, `ToolGateway`, `Clock` e `IdGenerator` como abstrações candidatas muito cedo. fileciteturn11file7L1596-L1627

Isso é compatível com Clean Architecture em intenção, mas pode produzir uma implementação excessivamente indireta.

## Decisão

Classificar as dependências antes de criar seams:

```text
in-process
local-substitutable
remote but owned
true external
```

A existência de dois adapters ou de uma necessidade real de isolamento deve orientar a criação do port.

## Resultado

- `AgentRuntime`: seam real.
- OpenClaw/Hermes: adapters reais.
- `ModelCatalog`: módulo interno inicialmente.
- `SkillCatalog`: módulo interno inicialmente.
- `AgentCatalog`: módulo interno inicialmente.
- `Clock`: dependência simples inicialmente.
- `IdGenerator`: dependência simples inicialmente.

---

# 4. Achado crítico — módulos potencialmente rasos

O v0.1 descreve pipelines com diversos elementos auxiliares. Em `Resource Selection`, por exemplo, aparecem `CapabilityResolver`, `AgentCandidates`, `SkillCandidates`, `ModelCandidates`, `PolicyFilter` e `MultiObjectiveEvaluator`. fileciteturn11file2L220-L252

Esses nomes são úteis para explicar a lógica, mas não devem ser interpretados automaticamente como módulos públicos.

## Decisão

Tratar esses elementos como **implementação interna potencial** de um módulo profundo:

```text
ResourceSelection
        ↓
select(requirement, context)
        ↓
ResourceConfiguration / SelectionDecision
```

O chamador não deve reconstruir o pipeline interno.

---

# 5. Módulo crítico — Delegation

`AgentRuntime` é o melhor candidato a seam real porque o projeto explicitamente pretende manter o núcleo independente do runtime e suportar OpenClaw primeiro, com possibilidade de Hermes/outro runtime. O v0.1 já estabelece essa independência. fileciteturn11file4L791-L811

## Decisão

Manter:

```text
Application
→ AgentRuntime
→ OpenClawAdapter / HermesAdapter
```

Mas impedir que a interface copie a API do runtime.

O módulo de delegação deve esconder:

- montagem do handoff;
- lifecycle necessário;
- correlação da execução;
- normalização do resultado;
- tratamento de falhas técnicas.

---

# 6. Módulo crítico — Result Evaluation

O v0.1 apresenta um pipeline explícito:

```text
CriteriaResolver
→ EvidenceResolver
→ Evaluator
→ Verdict
→ StateUpdate
```

Isso é bom como visão interna, mas seria uma interface ruim se todos esses estágios fossem expostos aos chamadores.

## Decisão

Preferir:

```text
EvaluationRequest
→ Evaluation
```

com pipeline interna privada.

---

# 7. Módulo crítico — Replanning

O v0.1 apresenta:

```text
ImpactAssessment
→ AffectedSetResolver
→ PlanUpdater
→ ResourceReassessment
→ PlanValidator
```

Isso é uma implementação possível, não uma API obrigatória. fileciteturn11file2L220-L252

## Decisão

Preferir:

```text
replan(projectState, trigger)
→ PlanRevision
```

com locality da lógica de impacto e propagação dentro do módulo.

---

# 8. Módulo crítico — Knowledge / Context

O v0.1 já distingue Knowledge de Context. fileciteturn11file3L103-L140

Isso permanece correto.

O ajuste é evitar transformar cada backend de retrieval em uma abstração pública antes de existir necessidade real.

## Decisão

O contexto será montado por um módulo de aplicação que pode consultar fontes por meio de um seam quando houver dependência externa real.

---

# 9. Módulo crítico — Skill Catalog

O `SkillProfile` atual já contempla dependencies, compatibilidade e versionamento. fileciteturn11file7L1454-L1468

A revisão baseada no material externo acrescenta:

```text
invocationPolicy
skill composition
provenance
runtime-specific metadata
```

Isso deverá ser desenvolvido em uma futura **Skill Architecture**, não transformado diretamente em código neste momento.

---

# 10. Interface como superfície de teste

O Design v0.1 já possui uma estratégia de testes por camada. fileciteturn11file4L162-L203

A revisão adiciona uma regra mais forte:

> testes de comportamento devem atravessar preferencialmente a interface externa do módulo.

Isso evita testes que conheçam a implementação interna e torna refatorações mais seguras.

---

# 11. Replace, don't layer

Ao aprofundar um módulo, testes específicos dos módulos rasos anteriores não devem ser mantidos indefinidamente se se tornarem redundantes.

O objetivo é:

```text
old shallow modules
→ deep module
→ interface tests
→ remove redundant tests
```

Isso reduz duplicação de testes e acoplamento histórico.

---

# 12. Design It Twice

Foram escolhidos quatro candidatos principais:

```text
Resource Selection
Delegation
Result Evaluation
Replanning
```

Para cada um, o Design v0.2 registra alternativas de interface e uma recomendação baseada em:

```text
depth
leverage
locality
seam placement
```

A escolha não significa que os contratos estejam congelados no nível de código; significa que o design já foi comparado antes da implementação.

---

# 13. Ubiquitous Language

O projeto ainda deve criar um `CONTEXT.md` próprio, de maneira incremental, para consolidar termos canônicos.

Esse arquivo deverá ser distinto de:

```text
Requirements
Architecture
Design
```

A finalidade será controlar linguagem, sinônimos e ambiguidades.

---

# 14. Confronto com o legado

O legado foi reutilizado em princípios de:

- separação de responsabilidades;
- dependências;
- estados;
- baseline;
- validação;
- impacto;
- rastreabilidade;
- suficiência;
- evolução governada.

O novo conhecimento de Deep Modules não é uma substituição desses princípios; ele os complementa com um critério de qualidade para a forma dos módulos e interfaces.

---

# 15. Decisões preservadas

A revisão **não altera** estas decisões:

```text
Clean Architecture
DDD como ferramenta de modelagem
modular monolith inicialmente
OpenClaw como primeiro runtime
possibilidade de Hermes/outros runtimes
SDD como disciplina transversal
Project State explícito
Work Unit como unidade de execução
TaskPackage / ResultPackage
Evaluation antes de conclusão
Replanning adaptativo
Continuity & Learning
```

---

# 16. Decisões modificadas

Foram modificadas estas interpretações:

```text
ports para tudo
        ↓
ports somente para seams justificados

pipelines públicos
        ↓
pipelines internas de módulos profundos

service por responsabilidade nominal
        ↓
módulo/coesa unidade por razão de mudança e profundidade

flexibilidade antecipada
        ↓
YAGNI + seam real
```

---

# 17. Resultado da revisão

O Design v0.2 é considerado adequado para avançar ao **Implementation Plan**, mas não diretamente ao código.

Ainda é necessário transformar o design em Work Units ordenadas por dependência, com critérios de aceitação e verificação.

---

# 18. Próximo gate

```text
Design v0.2
    ↓
Implementation Plan
    ↓
Work Units
    ↓
Dependency ordering
    ↓
Acceptance criteria
    ↓
Verification strategy
    ↓
Implementation
```

---

# 19. Conclusão

A principal melhoria desta revisão é evitar que a intenção de Clean Architecture produza um sistema excessivamente abstrato.

O princípio final é:

> **módulos coesos e profundos, interfaces pequenas, seams reais, adapters justificáveis e testes atravessando as interfaces relevantes.**

Isso reduz acoplamento, aumenta locality e leverage e melhora a navegabilidade do código para humanos e agentes de IA.
