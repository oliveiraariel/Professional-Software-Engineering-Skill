# ORCHESTRATOR-DELEGATION-AND-COORDINATION

**Projeto:** Adaptive AI Orchestrator  
**Capacidade:** Delegation & Coordination  
**Versão:** v0.1 — definição inicial  
**Status:** Em desenvolvimento

---

## 1. Propósito

A capacidade **Delegation & Coordination** transforma uma decisão de alocação em uma execução coordenada.

Seu objetivo é permitir que o Orchestrator:

- prepare corretamente o trabalho;
- forneça o contexto necessário ao agente;
- envie a unidade de trabalho ao recurso selecionado;
- acompanhe o estado da execução;
- receba o resultado;
- trate falhas;
- integre os resultados ao projeto;
- preserve dependências e consistência;
- acione revisões quando necessário;
- devolva controle ao ciclo de planejamento e avaliação.

A capacidade deve impedir que o Orchestrator confunda:

```text
selecionar um recurso
```

com:

```text
executar corretamente o trabalho com esse recurso
```

---

## 2. Papel dentro do Orchestrator

A pergunta central desta capacidade é:

> **"Como executar a Work Unit selecionada de forma controlada, transmitindo contexto suficiente, evitando contexto desnecessário, preservando dependências e garantindo que o resultado possa retornar ao projeto?"**

Ela recebe principalmente:

- Work Unit;
- configuração selecionada;
- dependências;
- contexto do projeto;
- critérios de sucesso;
- restrições;
- políticas;
- informações de integração.

Ela produz:

- Task Package;
- estado de execução;
- Result Package;
- eventos de execução;
- informações de falha;
- informações de integração;
- sinais para avaliação;
- sinais para replanejamento.

---

## 3. Posição no ciclo do Orchestrator

A cadeia principal é:

```text
Project Management
        ↓
Work Unit
        ↓
Agent & Skill Analysis
        ↓
Resource / Model Selection
        ↓
Delegation & Coordination
        ↓
Execution
        ↓
Result Evaluation
        ↓
Continuity & Learning
        ↓
Replanning
```

Delegation & Coordination é, portanto, a ponte entre:

```text
decisão
```

e:

```text
execução observável
```

---

## 4. Princípio fundamental

A delegação deve ser tratada como **contrato de trabalho**, e não como simples envio de texto para outro agente.

O Orchestrator deve fornecer:

```text
objetivo
+
contexto
+
restrições
+
entradas
+
dependências
+
resultado esperado
+
critérios de conclusão
```

O agente executa dentro desse contrato.

O resultado retorna por meio de uma estrutura suficientemente organizada para que o Orchestrator possa avaliá-lo.

---

## 5. Separação entre plano, delegação e execução

São etapas distintas:

```text
PLANEJAMENTO
→ o que precisa ser feito?

SELEÇÃO
→ quem/com o quê fará?

DELEGAÇÃO
→ como o trabalho será transferido?

EXECUÇÃO
→ o agente realiza o trabalho

RETORNO
→ resultado e evidências

AVALIAÇÃO
→ o resultado atende?

REPLANEJAMENTO
→ o que fazer agora?
```

Essa separação impede que uma decisão de alocação seja automaticamente tratada como conclusão do trabalho.

---

## 6. Work Unit como unidade de delegação

A Work Unit é a unidade mínima de trabalho que o Orchestrator pode delegar.

Ela deve possuir, conforme aplicável:

```text
id
objetivo
escopo
entradas
saídas
dependências
pré-condições
prioridade
criticidade
restrições
Skill necessária
agente selecionado
modelo selecionado
critério de conclusão
estado
```

A delegação não deve alterar silenciosamente a definição da Work Unit.

Qualquer alteração significativa deve retornar ao processo de planejamento.

---

## 7. Task Package

Antes da execução, o Orchestrator deve montar um **Task Package**.

Estrutura conceitual:

```text
TASK PACKAGE
├── task_id
├── project_id
├── work_unit
├── objective
├── scope
├── context
├── required_inputs
├── available_artifacts
├── relevant_decisions
├── dependencies
├── constraints
├── selected_skill(s)
├── selected_agent
├── selected_model
├── expected_output
├── success_criteria
├── validation_requirements
├── authority
└── execution_metadata
```

Nem todo campo precisa ser transmitido ao agente na íntegra.

O pacote lógico pode ser maior que o contexto efetivamente enviado.

---

## 8. Contexto completo versus contexto necessário

O Orchestrator deve distinguir:

```text
Project Context
```

de:

```text
Task Context
```

Nem todo agente precisa receber todo o projeto.

A transmissão deve seguir o princípio:

> **fornecer o máximo de contexto necessário e o mínimo de contexto desnecessário.**

Isso reduz:

- custo;
- latência;
- confusão;
- carga cognitiva;
- risco de inconsistência.

---

## 9. Context Package

O contexto efetivamente enviado ao agente pode ser composto por:

```text
CONTEXTO ESSENCIAL
+
ARTEFATOS NECESSÁRIOS
+
DECISÕES RELEVANTES
+
DEPENDÊNCIAS
+
RESTRIÇÕES
+
CRITÉRIOS
```

Informações irrelevantes não devem ser transferidas simplesmente porque estão disponíveis.

---

## 10. Proveniência do contexto

Quando possível, o Task Package deve indicar de onde veio a informação:

```text
Project Definition
Requirement
Decision
Artifact
Previous Result
External Evidence
Inference
```

Isso permite ao agente diferenciar:

```text
fato
```

de:

```text
hipótese
```

e:

```text
decisão ainda pendente
```

Esse princípio é diretamente compatível com o modelo de evidência do projeto legado.

---

## 11. Contexto mínimo seguro

"Contexto mínimo" não significa contexto insuficiente.

Antes de delegar, o Orchestrator deve garantir:

```text
informação necessária
+
pré-condições
+
objetivo
+
critérios
```

Se faltar uma informação essencial:

```text
não delegar ainda
```

ou:

```text
delegar parcialmente
```

caso a parte liberada possa avançar de forma segura.

---

## 12. Dependências antes da delegação

Uma Work Unit somente deve ser delegada quando suas dependências estiverem em estado compatível com o início.

Exemplo:

```text
A → B → C
```

B não deve ser iniciado antes de A produzir o conhecimento/artefato necessário.

Possíveis estados:

```text
BLOCKED
PARTIALLY_RELEASED
READY
```

A definição de estados e dependências deve permanecer compatível com os mecanismos existentes no legado.

---

## 13. Delegação parcial

Uma Work Unit pode, quando seguro, ser parcialmente delegada.

Exemplo:

```text
Work Unit
├── parte independente → READY
└── parte dependente → BLOCKED
```

O Orchestrator pode encaminhar apenas a parte liberada, desde que:

- o escopo esteja claro;
- o resultado seja útil;
- não seja criado retrabalho evitável.

---

## 14. Pré-condições

Antes de iniciar, o Orchestrator deve verificar:

```text
Skill disponível
Agent disponível
Model disponível
Ferramentas disponíveis
Contexto suficiente
Dependências satisfeitas
Permissões válidas
Restrições atendidas
Critérios definidos
```

Se uma pré-condição essencial não estiver satisfeita:

```text
não iniciar
```

---

## 15. Handoff

O **handoff** é a transferência formal do trabalho do Orchestrator para o agente.

O handoff deve representar:

```text
quem delega
+
quem recebe
+
o que será realizado
+
com quais entradas
+
em quais limites
+
qual resultado deve retornar
```

A execução somente deve ser considerada iniciada quando o handoff estiver concluído.

---

## 16. Estado da delegação

A delegação pode assumir estados como:

```text
PREPARING
READY_TO_SEND
SENT
ACCEPTED
RUNNING
WAITING
BLOCKED
RETRYING
RETURNING
COMPLETED
FAILED
CANCELLED
REOPENED
```

Nem todos precisam ser materializados no primeiro runtime, mas a semântica deve existir.

---

## 17. Acompanhamento

O Orchestrator deve distinguir:

```text
executando
```

de:

```text
executando corretamente
```

A capacidade de acompanhamento pode considerar:

- estado;
- progresso observável;
- eventos;
- tempo;
- erros;
- bloqueios;
- ausência de resposta;
- mudanças de escopo.

---

## 18. Não interferir sem motivo

O Orchestrator não deve interromper ou alterar uma execução apenas porque o agente está demorando.

Intervenção deve ser motivada por:

- timeout relevante;
- erro;
- violação de escopo;
- nova informação;
- mudança de prioridade;
- custo inesperado;
- risco;
- bloqueio.

---

## 19. Result Package

O agente deve retornar um pacote de resultado estruturado.

Estrutura conceitual:

```text
RESULT PACKAGE
├── task_id
├── status
├── summary
├── result
├── artifacts
├── decisions
├── assumptions
├── evidence
├── discovered_dependencies
├── discovered_issues
├── uncertainty
├── unresolved_questions
├── validation performed
├── recommendations
└── execution_metadata
```

O resultado principal pode ser textual, documental, estruturado ou composto por artefatos.

---

## 20. Resultado não é conclusão

Receber:

```text
RESULT PACKAGE
```

não significa:

```text
Work Unit = COMPLETED
```

O estado correto é:

```text
RESULT RECEIVED
        ↓
RESULT EVALUATION
        ↓
ACCEPTED / RETURNED / BLOCKED / REOPENED
```

A conclusão depende da avaliação posterior.

---

## 21. Preservação de decisões do agente

Se o agente tomou uma decisão durante a execução, o retorno deve distingui-la de:

```text
fato encontrado
```

e de:

```text
hipótese
```

e de:

```text
recomendação
```

Isso permite que o Orchestrator saiba o que pode integrar diretamente e o que precisa ser revisado.

---

## 22. Assumptions

O agente deve informar premissas relevantes.

Exemplo:

```text
Assumption:
"Foi assumido que o módulo X será independente."
```

Isso é importante porque uma premissa incorreta pode afetar várias Work Units posteriores.

---

## 23. Novas dependências descobertas

Um resultado pode revelar:

```text
nova dependência
```

Exemplo:

```text
Agent A
→ descobriu que B depende de C
```

O Orchestrator deve:

1. registrar a dependência;
2. avaliar impacto;
3. atualizar o grafo;
4. bloquear/desbloquear unidades quando necessário;
5. replanejar.

---

## 24. Novas lacunas descobertas

O agente também pode descobrir:

```text
informação ausente
```

Essa informação não deve ser preenchida automaticamente.

O Orchestrator deve classificar:

```text
não bloqueadora
bloqueadora
crítica
desconhecida
```

e agir conforme a classificação.

---

## 25. Falhas de execução

Quando a execução falhar:

```text
FAILURE
↓
CLASSIFICATION
↓
RECOVERY DECISION
```

Possíveis causas:

```text
contexto insuficiente
ferramenta indisponível
modelo inadequado
Skill inadequada
erro do agente
dependência não satisfeita
restrição violada
timeout
falha externa
```

A causa deve ser registrada quando puder ser determinada.

---

## 26. Retry

Retry não deve ser automático em qualquer situação.

Pode ser adequado quando:

- falha transitória;
- ferramenta temporariamente indisponível;
- timeout;
- erro operacional recuperável.

Não deve ser repetido indefinidamente quando a causa for:

```text
Skill inadequada
Contexto insuficiente
Planejamento incorreto
Modelo inadequado
```

Nesses casos, deve ocorrer reavaliação.

---

## 27. Escalonamento

Quando a delegação não puder ser resolvida autonomamente:

```text
Orchestrator
    ↓
escalation
```

A escalada pode ocorrer para:

- outro agente;
- agente revisor;
- outro modelo;
- desenvolvedor.

O nível de escalonamento deve ser proporcional ao impacto.

---

## 28. Mudança de agente durante execução

Pode ser necessário substituir o agente quando:

- ele ficar indisponível;
- a capacidade necessária mudar;
- a qualidade estiver inadequada;
- uma especialização adicional for descoberta;
- houver falha persistente.

Fluxo:

```text
RUNNING
 ↓
PROBLEM
 ↓
REASSESS
 ↓
NEW CONFIGURATION
 ↓
CONTINUE / RESTART / SPLIT
```

A decisão deve preservar o máximo possível do trabalho já realizado.

---

## 29. Mudança de modelo durante execução

O modelo também pode ser alterado quando:

- o recurso ficar indisponível;
- a complexidade aumentar;
- o resultado exigir maior capacidade;
- a tarefa se mostrar simples demais;
- custo/latência fugir do planejado.

A mudança deve ser registrada.

---

## 30. Preservação do trabalho parcial

Quando uma execução falhar depois de produzir resultados úteis:

```text
não descartar automaticamente
```

O Orchestrator deve identificar:

```text
parte válida
parte inválida
parte desconhecida
```

e decidir se pode reutilizar o trabalho parcial.

Isso reduz retrabalho.

---

## 31. Integração de resultados

O resultado de um agente pode produzir:

```text
artefato
decisão
conhecimento
dependência
risco
nova Work Unit
```

O Orchestrator deve determinar o impacto da integração.

Nem todo resultado deve alterar imediatamente o estado global.

---

## 32. Merge de resultados paralelos

Quando múltiplos agentes trabalham em paralelo:

```text
Agent A → Result A
Agent B → Result B
Agent C → Result C
```

os resultados devem ser:

```text
integrados
+
comparados
+
validados
```

antes de serem tratados como um único estado consolidado.

---

## 33. Conflito entre resultados

Pode ocorrer:

```text
Agent A → decisão X
Agent B → decisão Y
```

O Orchestrator não deve escolher arbitrariamente.

Deve:

1. detectar conflito;
2. identificar a origem;
3. comparar evidências;
4. verificar dependências;
5. solicitar revisão ou decisão quando necessário;
6. registrar a resolução.

---

## 34. Resultado redundante

Múltiplos agentes podem produzir essencialmente o mesmo resultado.

Nesse caso, o Orchestrator deve evitar armazenar duplicação como conhecimento independente.

Pode comparar:

```text
convergência
divergência
qualidade
custo
```

e usar a convergência como evidência complementar.

---

## 35. Coordenação entre agentes

A coordenação deve ocorrer principalmente através do Orchestrator e dos contratos definidos.

Evitar:

```text
Agent A
   ↕
Agent B
   ↕
Agent C
   ↕
Agent D
```

sem controle.

Preferir:

```text
           ORCHESTRATOR
            /    |    \
           ↓     ↓     ↓
        Agent A Agent B Agent C
```

salvo quando o runtime ou a natureza da tarefa justificarem comunicação direta.

---

## 36. Contexto compartilhado

Quando múltiplos agentes participarem do mesmo projeto, o Orchestrator deve definir:

```text
shared project state
```

mas não necessariamente compartilhar todo o conteúdo bruto entre eles.

Cada agente recebe:

```text
subset of project state
```

necessário para seu trabalho.

---

## 37. Coordenação por dependência

A coordenação deve utilizar explicitamente o grafo de dependências:

```text
A
├── B
├── C
└── D

B
└── E

C
└── E
```

E só liberar:

```text
E
```

quando:

```text
B + C
```

estiverem em estados compatíveis.

---

## 38. Paralelismo

A coordenação deve aproveitar paralelismo quando:

- tarefas independentes;
- baixo acoplamento;
- contexto estável;
- dependências satisfeitas;
- benefício real.

Evitar manter muitos agentes ativos simultaneamente apenas para parecer mais rápido.

O legado estabelece explicitamente que o processo é sequencial por dependência e que o paralelismo deve ser controlado para evitar retrabalho.

---

## 39. Contexto crescente

Conforme o projeto evolui, o contexto pode crescer.

O Orchestrator deve evitar:

```text
enviar tudo novamente
```

em cada delegação.

Preferir:

```text
estado atual
+
delta relevante
+
referências
```

quando o runtime suportar.

---

## 40. Controle de contexto

A coordenação deve acompanhar:

```text
contexto necessário
contexto enviado
contexto reutilizado
contexto redundante
```

Isso é importante porque contexto é simultaneamente:

```text
recurso cognitivo
e
recurso econômico
```

---

## 41. Timeout

A definição de timeout deve ser proporcional ao trabalho.

Um timeout deve considerar:

- complexidade;
- modelo;
- ferramenta;
- volume;
- histórico.

Timeout não deve ser interpretado automaticamente como erro lógico.

---

## 42. Cancelamento

O Orchestrator pode cancelar uma tarefa quando:

- ela deixou de ser necessária;
- a dependência mudou;
- o projeto foi replanejado;
- o custo ficou injustificável;
- surgiu uma solução superior;
- houve risco relevante.

O cancelamento deve preservar o histórico da decisão.

---

## 43. Reabertura

Uma Work Unit concluída pode ser reaberta quando:

- nova descoberta a afeta;
- dependência mudou;
- resultado posterior contradiz a decisão;
- requisito mudou;
- defeito foi encontrado.

Isso reutiliza diretamente o modelo de reabertura do legado.

---

## 44. Replanejamento após retorno

O retorno de uma execução deve poder causar:

```text
nenhuma alteração
```

ou:

```text
ajuste local
```

ou:

```text
mudança estrutural
```

ou:

```text
replanejamento global
```

O nível deve ser proporcional ao impacto.

---

## 45. Telemetria da execução

Cada delegação deve registrar, quando possível:

```text
task_id
agent
skill
model
start_time
end_time
status
cost
tokens/usage
latency
retry
failure
human intervention
result quality
rework
```

Isso alimentará as futuras capacidades de avaliação e aprendizagem.

---

## 46. Custo de coordenação

A própria Delegation & Coordination pode gerar custo.

Registrar, quando disponível:

```text
número de handoffs
quantidade de contexto transferido
mensagens
retries
revisões
tempo de coordenação
```

Esses dados são úteis para verificar se uma arquitetura multiagente realmente trouxe benefício.

---

## 47. Qualidade do handoff

Um handoff deve poder ser avaliado posteriormente por:

```text
contexto suficiente?
objetivo claro?
restrições claras?
dependências claras?
saída esperada clara?
```

Um resultado ruim pode ter origem no trabalho do agente ou no próprio handoff.

Essa distinção é importante para aprendizado.

---

## 48. Diagnóstico de causa

Quando o resultado falhar, o Orchestrator deve tentar distinguir:

```text
PLANNING ERROR
SELECTION ERROR
DELEGATION ERROR
CONTEXT ERROR
SKILL ERROR
AGENT ERROR
MODEL ERROR
TOOL ERROR
INTEGRATION ERROR
EVALUATION ERROR
```

Essa classificação permite melhorar o componente correto.

---

## 49. Interface com Result Evaluation

Delegation & Coordination entrega o resultado.

Result Evaluation decide:

```text
aceitar
rejeitar
revisar
reabrir
```

Não deve haver aprovação implícita.

Fluxo:

```text
Execution
 ↓
Result Package
 ↓
Result Evaluation
 ↓
decision
```

---

## 50. Interface com Continuity & Learning

A execução produz evidência.

O conhecimento histórico deve poder registrar:

```text
configuration
+
task type
+
context
+
result
+
quality
+
cost
+
rework
```

Esse histórico permitirá posteriormente melhorar:

- seleção;
- Skills;
- prompts;
- agentes;
- modelos;
- estratégias de delegação.

---

## 51. Conhecimento legado reutilizado

Esta capacidade reaproveita fortemente o projeto anterior:

### Dependências e paralelismo

O legado estabelece execução sequencial por dependência, paralelismo controlado e estados de liberação/bloqueio.

### Ciclo de execução

Já existe:

```text
decisão
→ planejamento
→ execução
→ teste
→ validação
→ análise de efeitos
→ conclusão
```

e, em falha:

```text
problema
→ análise
→ correção
→ revalidação
```

### Estados

O legado já possui estados de execução e reabertura.

### Impacto

Alterações devem considerar dependências e impacto antes de propagá-las.

### Evidência

Resultados e decisões devem preservar origem, confiança e estado.

Esses elementos são aproveitados como fundamentos metodológicos do mecanismo de delegação.

---

## 52. Conhecimento novo

A capacidade precisa desenvolver conhecimento adicional sobre:

- Task Package;
- Result Package;
- handoff;
- contexto mínimo seguro;
- transferência de contexto;
- isolamento de agentes;
- retries;
- fallback operacional;
- cancelamento;
- merge;
- conflitos entre agentes;
- telemetria;
- custo de coordenação;
- diagnóstico de falha de delegação.

---

## 53. Não acoplar o conceito ao runtime

O modelo conceitual deve funcionar independentemente da plataforma.

Por exemplo:

```text
Task Package
Result Package
Work Unit
Delegation State
```

são conceitos próprios do projeto.

OpenClaw/Hermes ou outro runtime devem fornecer os mecanismos concretos para implementar esses conceitos.

---

## 54. Adaptação à plataforma

Na fase de integração, cada conceito será mapeado para mecanismos reais:

```text
Project concept
      ↓
Runtime mechanism
```

Exemplo conceitual:

```text
Subagent Session
→ execução isolada

Skill
→ conhecimento operacional

Workspace
→ contexto persistente

Model selection
→ configuração de execução
```

O mapeamento concreto será definido na arquitetura de implementação.

---

## 55. Critérios de sucesso

Delegation & Coordination estará suficientemente desenvolvida quando o Orchestrator puder:

1. montar uma Work Unit delegável;
2. preparar um Task Package;
3. fornecer contexto suficiente;
4. respeitar dependências;
5. iniciar a execução no recurso selecionado;
6. acompanhar o estado;
7. receber um Result Package;
8. preservar decisões, premissas e evidências;
9. registrar falhas;
10. executar retries controlados;
11. acionar fallback quando autorizado;
12. substituir recursos quando necessário;
13. integrar resultados;
14. tratar conflitos;
15. controlar paralelismo;
16. atualizar o estado do projeto;
17. fornecer dados para avaliação e aprendizagem;
18. evitar delegações e transferências de contexto desnecessárias.

---

## 56. Princípio operacional consolidado

> **Toda delegação deve ser uma transferência controlada de uma Work Unit, com contexto, dependências, autoridade, resultado esperado e critérios de conclusão explicitamente definidos, seguida por retorno estruturado e integração supervisionada ao estado do projeto.**

---

## 57. Fluxo completo

```text
Work Unit
    ↓
Agent & Skill Analysis
    ↓
Resource / Model Selection
    ↓
Task Package
    ↓
Precondition Check
    ↓
Handoff
    ↓
Execution
    ↓
Monitoring
    ↓
Result Package
    ↓
Result Evaluation
    ↓
┌──────────────────────────────┐
│                              │
ACCEPTED                    RETURNED
│                              │
↓                              ↓
Integration                 Review/Retry
│                              │
└──────────────┬───────────────┘
               ↓
         Project State
               ↓
          Replanning
               ↓
          Next Work Unit
```

---

## 58. Estado

**Status:** Definição inicial concluída.

### Artefatos relacionados

- `PROJECT-DEFINITION.md`
- `ORCHESTRATOR-CAPABILITIES.md`
- `ORCHESTRATOR-KNOWLEDGE-MAP.md`
- `ORCHESTRATOR-PROJECT-AWARENESS.md`
- `ORCHESTRATOR-PROJECT-MANAGEMENT.md`
- `ORCHESTRATOR-ECOSYSTEM-AWARENESS.md`
- `ORCHESTRATOR-AGENT-AND-SKILL-ANALYSIS.md`
- `ORCHESTRATOR-RESOURCE-MODEL-SELECTION.md`

### Próxima capacidade

**Result Evaluation**

Pergunta central:

> **"O resultado produzido pelo agente é correto, suficiente, consistente, rastreável e adequado ao objetivo, às restrições e ao estado do projeto?"**
