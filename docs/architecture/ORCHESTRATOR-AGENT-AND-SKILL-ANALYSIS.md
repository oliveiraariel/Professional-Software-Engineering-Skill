# ORCHESTRATOR-AGENT-AND-SKILL-ANALYSIS

**Projeto:** Adaptive AI Orchestrator  
**Capacidade:** Agent & Skill Analysis  
**Versão:** v0.1 — definição inicial  
**Status:** Em desenvolvimento

---

## 1. Propósito

A capacidade **Agent & Skill Analysis** permite ao Orchestrator determinar quais capacidades especializadas são necessárias para executar cada unidade de trabalho e quais agentes são tecnicamente adequados para fornecê-las.

Seu objetivo é estabelecer a relação entre:

```text
necessidade do projeto
        ↓
capacidade necessária
        ↓
Skill necessária
        ↓
agentes elegíveis
        ↓
configurações possíveis
```

A capacidade não executa a tarefa especializada.

Ela realiza a **análise necessária para que o Orchestrator possa decidir como a tarefa deverá ser alocada**.

---

## 2. Papel dentro do Orchestrator

A pergunta central desta capacidade é:

> **"Qual capacidade especializada esta unidade de trabalho exige e quais agentes disponíveis conseguem fornecê-la?"**

Ela recebe:

- conhecimento sobre o projeto;
- estrutura aprovada;
- Work Units;
- estado das dependências;
- catálogo do ecossistema.

E produz:

- capacidades requeridas;
- Skills necessárias;
- agentes elegíveis;
- incompatibilidades;
- lacunas de capacidade;
- combinações candidatas;
- justificativas;
- informações para seleção de recursos.

### Relação com as demais capacidades

```text
Project Awareness
        ↓
entende o problema e o estado

Project Management
        ↓
define a unidade de trabalho e suas condições

Ecosystem Awareness
        ↓
conhece recursos disponíveis

Agent & Skill Analysis
        ↓
determina capacidade necessária e elegibilidade

Resource / Model Selection
        ↓
seleciona configuração de execução

Delegation & Coordination
        ↓
executa a alocação

Result Evaluation
        ↓
verifica o resultado
```

---

## 3. Princípio fundamental

O Orchestrator não deve partir de:

> "Tenho estes agentes; qual tarefa posso dar a eles?"

Ele deve partir de:

> **"Tenho esta necessidade; qual capacidade ela exige e qual recurso disponível é capaz de atender a essa necessidade?"**

A direção do raciocínio deve ser:

```text
necessidade
→ capacidade
→ Skill
→ agente
```

e não:

```text
agente
→ procurar uma tarefa
```

Isso reduz encaixes artificiais e uso inadequado de agentes.

---

## 4. Separação entre tarefa, capacidade, Skill e agente

Esses conceitos devem permanecer distintos.

### Tarefa / Work Unit

O que precisa ser realizado.

### Capacidade

O tipo de competência necessária para realizar a tarefa.

### Skill

Conhecimento ou procedimento especializado que fornece ou amplia uma capacidade.

### Agente

Unidade responsável por executar a tarefa utilizando suas capacidades, Skills, ferramentas e modelo.

### Modelo

Recurso de inteligência utilizado pelo agente.

A cadeia conceitual é:

```text
WORK UNIT
    ↓
REQUIRED CAPABILITY
    ↓
REQUIRED SKILL(S)
    ↓
ELIGIBLE AGENT(S)
    ↓
ELIGIBLE MODEL(S)
```

A última etapa pertence principalmente à capacidade de **Resource / Model Selection**, embora as informações de elegibilidade sejam produzidas aqui.

---

## 5. Entrada principal: Work Unit

A análise deve utilizar uma Work Unit já suficientemente definida.

Uma Work Unit deve possuir, conforme aplicável:

```text
objetivo
escopo
entradas
saídas
dependências
pré-condições
criticidade
complexidade
prioridade
restrições
critério de conclusão
```

Se a Work Unit não estiver suficientemente definida para permitir uma análise responsável, o Orchestrator deve tratar isso como lacuna.

Não deve inventar requisitos ou capacidades apenas para conseguir atribuir a tarefa.

---

## 6. Identificação da capacidade necessária

O primeiro passo é determinar:

> **"O que precisa ser feito para produzir o resultado esperado?"**

Exemplo:

```text
Work Unit:
"Definir a arquitetura lógica do sistema."

        ↓

Capacidades requeridas:
- arquitetura de software
- modelagem estrutural
- análise de trade-offs
- definição de responsabilidades
- avaliação de dependências
```

A análise deve ser realizada no nível necessário, evitando decomposição excessiva.

---

## 7. Uma Work Unit pode exigir múltiplas capacidades

Não existe obrigação de uma relação:

```text
1 Work Unit → 1 Skill
```

Pode existir:

```text
1 Work Unit
    ↓
Skill A
+
Skill B
+
Skill C
```

Exemplo:

```text
Segurança arquitetural

→ Architecture
→ Security
→ Risk Analysis
```

Nesse caso, o Orchestrator deverá determinar se:

- um único agente possui todas as competências;
- um agente principal possui uma competência e outra Skill complementar;
- são necessários múltiplos agentes;
- uma etapa deve ser decomposta.

Essa decisão deverá considerar o custo e o risco da coordenação.

---

## 8. Especialização necessária

Cada capacidade requerida deve possuir um nível de profundidade suficiente para orientar a seleção.

Pode ser representada conceitualmente por:

```text
básica
intermediária
avançada
especialista
crítica/especialista
```

A classificação não deve ser absoluta.

Deve considerar:

- complexidade;
- criticidade;
- impacto;
- incerteza;
- grau de especialização exigido;
- necessidade de revisão.

---

## 9. Skill necessária

Depois de identificar a capacidade, o Orchestrator deve procurar Skills que forneçam essa capacidade.

Exemplo:

```text
Required Capability:
"Domain Modeling"

        ↓

Candidate Skills:
- Domain Modeling
- DDD
- Entity Modeling
```

A análise deve verificar:

- cobertura;
- especialização;
- pré-condições;
- dependências;
- versão;
- compatibilidade;
- restrições;
- evidências de adequação.

---

## 10. Skill suficiente versus Skill complementar

A Skill pode ser:

### Suficiente

Sozinha cobre a capacidade necessária.

### Parcial

Cobre apenas parte da necessidade.

### Complementar

Aumenta a capacidade de uma Skill principal.

### Inadequada

Não cobre de forma suficiente a necessidade.

Exemplo:

```text
Architecture Skill
+
Security Skill
```

pode ser mais apropriado do que uma única Skill genérica.

---

## 11. Dependências entre Skills

Skills podem depender de outras Skills ou de conhecimentos prévios.

Exemplo:

```text
Architecture Review
      ↓
Requires:
Architecture Knowledge
+
Quality Attributes
+
Project Context
```

O Orchestrator deve detectar pré-condições.

Uma Skill disponível mas sem suas dependências necessárias não deve ser considerada plenamente elegível.

---

## 12. Análise de agentes

Depois das Skills requeridas serem identificadas, o Orchestrator avalia os agentes disponíveis.

Para cada agente, deve poder analisar:

```text
responsabilidade
especialização
Skills
ferramentas
contexto
autonomia
restrições
modelos elegíveis
histórico
qualidade observada
custo relativo
disponibilidade
```

Isso utiliza diretamente o conhecimento produzido por **Ecosystem Awareness**.

---

## 13. Agent Profile

O perfil conceitual de um agente pode conter:

```text
AGENT PROFILE
├── id
├── role
├── responsibilities
├── capabilities
├── skills
├── tools
├── eligible models
├── context requirements
├── autonomy limits
├── restrictions
├── dependencies
├── performance history
└── status
```

A representação física será definida na arquitetura de implementação.

---

## 14. Elegibilidade do agente

O fato de um agente existir não significa que ele seja adequado.

Para uma determinada Work Unit, o agente deve ser classificado, conforme aplicável, como:

```text
ELEGIBLE
PARTIALLY_ELIGIBLE
INELIGIBLE
UNKNOWN
```

A elegibilidade deve considerar pelo menos:

- cobertura da capacidade;
- Skills;
- ferramentas;
- contexto;
- dependências;
- restrições;
- criticidade;
- disponibilidade;
- política de uso.

---

## 15. Elegibilidade técnica

Um agente é tecnicamente elegível quando possui capacidade suficiente para realizar a tarefa dentro das restrições conhecidas.

Exemplo:

```text
Task:
Modelar banco de dados

Agent A:
+ Data Modeling Skill
+ SQL Tool
+ contexto suficiente

→ TECNICAMENTE ELEGÍVEL
```

---

## 16. Elegibilidade operacional

Além da capacidade técnica, o agente deve ser operacionalmente utilizável.

Exemplo:

```text
Agent B
+ Skill correta
+ modelo adequado

mas:

sem acesso à ferramenta necessária

→ NÃO ELEGÍVEL OPERACIONALMENTE
```

Portanto:

```text
capacidade técnica
+
condições operacionais
=
elegibilidade
```

---

## 17. Adequação não é o mesmo que elegibilidade

Pode haver vários agentes elegíveis.

Exemplo:

```text
Agent A → elegível
Agent B → elegível
Agent C → elegível
```

A análise então fornece candidatos.

A seleção final considerará:

- custo;
- qualidade;
- latência;
- criticidade;
- histórico;
- disponibilidade;
- risco;
- contexto.

Essa etapa pertence principalmente a **Resource / Model Selection**.

---

## 18. Agentes generalistas versus especialistas

Um agente generalista pode ser tecnicamente elegível para várias tarefas.

Isso não significa que seja a melhor opção.

O Orchestrator deve considerar o custo-benefício da especialização.

Exemplo:

```text
General Agent
→ faz tudo razoavelmente bem

Specialist Agent
→ faz uma classe específica de tarefas melhor
```

A seleção deve considerar:

```text
ganho de especialização
vs.
custo de coordenação
```

---

## 19. Um agente pode usar múltiplas Skills

Um agente pode ser configurado com:

```text
Agent
├── Skill A
├── Skill B
└── Skill C
```

Nesse caso, uma Work Unit pode ser realizada por um único agente quando isso reduzir:

- transferência de contexto;
- coordenação;
- custo;
- latência;
- risco de inconsistência.

Esse princípio evita fragmentação artificial.

---

## 20. Mais agentes não significa melhor arquitetura

A análise deve considerar a pergunta:

> **"Adicionar outro agente realmente produz benefício?"**

O Master já estabelece que a Skill não deve fragmentar arbitrariamente e que a divisão deve trazer benefício para execução, validação, rastreabilidade, decisão ou controle de risco.

Esse princípio deve ser reutilizado diretamente.

Portanto:

```text
mais agentes
≠
mais qualidade
```

Pode ocorrer:

```text
mais agentes
→ mais contexto
→ mais coordenação
→ mais custo
→ mais pontos de falha
→ mais retrabalho
```

---

## 21. Fronteira para a divisão de agentes

Uma Work Unit deve ser dividida entre agentes quando a separação produzir benefício suficiente em pelo menos uma dimensão:

```text
especialização
independência
validação
risco
paralelismo
qualidade
isolamento de contexto
```

e o benefício compensar a coordenação adicional.

---

## 22. Divisão por conhecimento especializado

Pode haver casos em que o ganho esteja principalmente na especialização.

Exemplo:

```text
Arquitetura geral
     ↓
Security Review
     ↓
Performance Review
```

O Orchestrator pode manter um agente principal e chamar especialistas para revisões específicas.

---

## 23. Divisão por independência

Quando duas partes são pouco acopladas, diferentes agentes podem executar em paralelo.

Exemplo:

```text
Documentation
        │
        └── independent

Test Design
        │
        └── independent
```

Mas isso só deve ocorrer quando as dependências relevantes estiverem satisfeitas.

O princípio legado de paralelismo controlado deve ser preservado.

---

## 24. Divisão por validação

Um agente pode produzir e outro revisar.

Exemplo:

```text
Architecture Agent
        ↓
Architecture Reviewer
```

Essa estratégia é especialmente relevante para:

- decisões críticas;
- artefatos de alto impacto;
- segurança;
- arquitetura;
- mudanças estruturais;
- resultados com alta incerteza.

---

## 25. Divisão por continuidade

O Orchestrator também deve considerar se separar a execução exige transferir uma quantidade de contexto que anule o benefício.

Se:

```text
Agent A
→ já possui todo o contexto
```

e:

```text
Agent B
→ exigiria reconstruir quase todo o contexto
```

a transferência pode ser economicamente e cognitivamente desvantajosa.

---

## 26. Análise de cobertura

Antes de escolher um agente, o Orchestrator deve conseguir responder:

```text
required capabilities
        ↓
        ?
covered by candidate?
```

Uma matriz conceitual:

| Necessidade | Skill | Agent | Cobertura |
|---|---|---|---|
| Arquitetura | Architecture | Agent A | Completa |
| Segurança | Security | Agent A | Parcial |
| Modelagem | Data Modeling | Agent B | Completa |

Isso pode revelar:

```text
Agent A → suficiente para estrutura
Agent A → insuficiente para segurança
Agent B → adequado para dados
```

---

## 27. Lacuna de capacidade

Se nenhuma combinação conhecida atender ao trabalho:

```text
Required Capability
        ↓
nenhum agente adequado
        ↓
CAPABILITY GAP
```

O Orchestrator não deve inventar uma capacidade inexistente.

Deve:

1. registrar a lacuna;
2. verificar se uma Skill adicional resolve;
3. verificar se outro modelo melhora a capacidade;
4. verificar se outro agente disponível é elegível;
5. considerar decomposição;
6. solicitar intervenção humana quando necessário.

---

## 28. Criação versus seleção

Nesta fase, o Orchestrator deve distinguir:

```text
selecionar recurso existente
```

de:

```text
criar/adicionar nova capacidade
```

A criação de uma nova Skill ou agente não deve ocorrer automaticamente apenas porque uma tarefa atual não encontrou um encaixe perfeito.

Essa decisão pode representar mudança estrutural no ecossistema.

---

## 29. Composição de capacidades

O Orchestrator pode combinar recursos:

```text
Agent A
+ Skill X
+ Skill Y
```

ou:

```text
Agent A
→ produz parte 1

Agent B
→ produz parte 2

Agent C
→ integra/revisa
```

A composição deve considerar dependências e interfaces de saída.

---

## 30. Compatibilidade de saída

Um agente só deve ser considerado uma boa escolha se sua saída puder ser consumida adequadamente pelo próximo estágio.

Exemplo:

```text
Agent A
→ produz arquitetura em formato esperado
        ↓
Agent B
→ consegue interpretar a arquitetura
```

Se a forma de saída exigir transformação excessiva:

```text
Agent A
→ resultado incompatível
→ conversão
→ risco
→ custo
```

o Orchestrator deve considerar isso na análise.

---

## 31. Contexto como requisito de elegibilidade

Alguns agentes podem exigir contexto maior ou diferente.

A análise deve considerar:

```text
contexto necessário
vs.
contexto acessível
```

Um agente tecnicamente excelente pode ser inadequado se não conseguir receber o contexto necessário de forma confiável e economicamente aceitável.

---

## 32. Conhecimento do agente versus contexto do projeto

O Orchestrator deve distinguir:

```text
Agent Knowledge
```

de:

```text
Project Knowledge
```

Um agente pode saber profundamente como fazer arquitetura, mas não conhecer:

```text
as regras específicas do projeto
```

Isso deve ser suprido pelo contexto da Work Unit.

---

## 33. Model independence

Agent & Skill Analysis não deve prender um agente a um modelo específico.

Exemplo:

```text
Architecture Agent
├── Architecture Skill
├── eligible models:
│   ├── Model A
│   ├── Model B
│   └── Model C
```

A seleção do modelo ocorrerá posteriormente.

Isso preserva o princípio definido no `PROJECT-DEFINITION`:

> modelo não é sinônimo de agente.

---

## 34. Histórico como evidência de elegibilidade

Quando houver dados históricos, o Orchestrator pode considerar:

```text
Agent + Skill + Model + Task Type
```

e observar:

- qualidade;
- retrabalho;
- tempo;
- falhas;
- necessidade de intervenção;
- estabilidade.

Um histórico real pode fornecer evidência melhor do que uma simples descrição declarada.

Mas histórico não deve ser tratado como verdade universal.

---

## 35. Confiança

A análise deve produzir, quando possível:

```text
elegibilidade
+
nível de confiança
```

Exemplo:

```text
Architecture Agent
→ elegível
→ confiança alta
```

ou:

```text
Agent C
→ potencialmente elegível
→ confiança baixa
→ pouca evidência histórica
```

Isso permite que outras capacidades tratem incerteza adequadamente.

---

## 36. Evidência usada

A justificativa da análise deve poder apontar para:

```text
Skill configuration
Agent configuration
Tool availability
Model capability
Historical performance
Project requirements
Runtime constraints
```

Quando possível, o Orchestrator deve registrar a origem.

Esse princípio é diretamente aproveitável da seção de evidência do legado.

---

## 37. Saída da análise

A saída conceitual deve possuir estrutura semelhante a:

```text
AGENT-SKILL ANALYSIS
├── work_unit
├── required_capabilities
├── required_skills
├── candidate_agents
├── eligibility
├── capability_gaps
├── compatibility
├── dependencies
├── confidence
├── evidence
└── recommendation_inputs
```

A recomendação final de recurso não precisa ser decidida aqui.

---

## 38. Exemplo completo

### Work Unit

```text
"Projetar arquitetura do sistema."
```

### Capacidades

```text
Architecture
Domain Modeling
Quality Attributes
Trade-off Analysis
```

### Skills candidatas

```text
Architecture
DDD
Architecture Decision Analysis
```

### Agentes

```text
Architecture Agent
Architecture Review Agent
General Engineering Agent
```

### Resultado da análise

```text
Architecture Agent
→ elegível
→ cobertura alta

General Engineering Agent
→ elegível
→ cobertura média

Architecture Review Agent
→ elegível para revisão
→ não substitui o agente de produção
```

### Plano candidato

```text
Architecture Agent
        ↓
produz arquitetura
        ↓
Architecture Review Agent
        ↓
revisão
```

O Orchestrator então poderá encaminhar essas alternativas para seleção e planejamento.

---

## 39. Quando a análise deve parar

A análise não precisa atingir conhecimento absoluto.

Ela deve parar quando houver:

```text
cobertura suficiente
+
elegibilidade suficiente
+
dependências identificadas
+
incerteza explicitada
```

e houver base suficiente para a próxima capacidade tomar sua decisão.

Isso segue o princípio de suficiência já consolidado no legado.

---

## 40. Critérios de sucesso

A capacidade estará suficientemente desenvolvida quando o Orchestrator puder:

1. inferir corretamente as capacidades necessárias de uma Work Unit;
2. identificar Skills adequadas;
3. analisar agentes disponíveis;
4. determinar elegibilidade;
5. detectar lacunas;
6. avaliar combinações de Skills;
7. reconhecer quando um único agente é suficiente;
8. reconhecer quando múltiplos agentes trazem benefício;
9. preservar separação entre agente e modelo;
10. considerar contexto e dependências;
11. justificar suas análises;
12. explicitar incertezas;
13. fornecer candidatos adequados para seleção de recursos;
14. evitar fragmentação desnecessária.

---

## 41. Relação com o conhecimento legado

O legado fornece uma base forte e reutilizável para:

- separação conceitual;
- compreensão da unidade de trabalho;
- granularidade;
- dependências;
- paralelismo;
- impacto;
- evidência;
- estados;
- suficiência;
- validação;
- coerência global.

Em especial, a regra de que uma divisão deve existir quando trouxer benefício para execução, validação, rastreabilidade, decisão ou controle de risco é diretamente aplicável a esta capacidade.

A parte nova é a modelagem explícita de:

- catálogo de agentes;
- catálogo de Skills;
- elegibilidade;
- composição de capacidades;
- lacunas de capacidade;
- compatibilidade entre recursos;
- histórico agente/Skill/tarefa.

---

## 42. Limites

Agent & Skill Analysis não deve:

- escolher definitivamente o modelo;
- executar o trabalho;
- revisar profundamente o resultado;
- alterar o plano por conta própria;
- criar agentes indiscriminadamente;
- inventar capacidades;
- ignorar políticas do ecossistema;
- assumir que especialização sempre justifica um agente adicional.

---

## 43. Integração com as próximas capacidades

### Entrada

```text
Project Management
+
Ecosystem Awareness
+
Project Awareness
```

### Saída

```text
Resource / Model Selection
+
Delegation & Coordination
```

Fluxo:

```text
Work Unit
    ↓
Agent & Skill Analysis
    ↓
required skills
    ↓
eligible agents
    ↓
Resource / Model Selection
    ↓
configuration
    ↓
Delegation & Coordination
```

---

## 44. Princípio operacional consolidado

> **O Orchestrator deve selecionar a responsabilidade antes de selecionar o recurso.**

Em termos práticos:

```text
1. compreender o trabalho;
2. identificar a capacidade necessária;
3. identificar Skills adequadas;
4. identificar agentes elegíveis;
5. avaliar composição;
6. encaminhar candidatos para seleção de recursos;
7. delegar somente após as condições estarem satisfeitas.
```

---

## 45. Estado

**Status:** Definição inicial concluída.

### Artefatos relacionados

- `PROJECT-DEFINITION.md`
- `ORCHESTRATOR-CAPABILITIES.md`
- `ORCHESTRATOR-KNOWLEDGE-MAP.md`
- `ORCHESTRATOR-PROJECT-AWARENESS.md`
- `ORCHESTRATOR-PROJECT-MANAGEMENT.md`
- `ORCHESTRATOR-ECOSYSTEM-AWARENESS.md`

### Próxima capacidade

**Resource / Model Selection**

Pergunta central:

> **"Entre os recursos elegíveis, qual combinação de agente, Skill e modelo oferece a melhor relação entre capacidade, qualidade, custo, latência, risco e contexto para esta Work Unit?"**
