# ORCHESTRATOR-REPLANNING

**Projeto:** Adaptive AI Orchestrator  
**Capacidade:** Replanning  
**Versão:** v0.1 — definição inicial  
**Status:** Em desenvolvimento

---

## 1. Propósito

A capacidade **Replanning** permite ao Orchestrator revisar e atualizar o plano de trabalho quando novas informações, resultados, falhas, mudanças, dependências, riscos ou avaliações modificarem as condições do projeto.

Seu objetivo é garantir que o plano permaneça:

- coerente;
- executável;
- atualizado;
- proporcional;
- economicamente adequado;
- alinhado ao estado real do projeto.

Replanning não significa reiniciar o projeto sempre que algo muda.

Seu princípio é:

> **preservar o máximo de trabalho válido e modificar somente o que o novo estado exige.**

---

## 2. Papel dentro do Orchestrator

Replanning responde:

> **"Dado o novo estado do projeto, o plano atual ainda é válido? Se não, qual é o menor conjunto de alterações necessário para continuar com segurança e eficiência?"**

Recebe:

- Project State;
- resultados avaliados;
- mudanças;
- novas dependências;
- riscos;
- bloqueios;
- Work Units;
- baselines;
- evidências;
- informações de custos e desempenho;
- decisões humanas;
- eventos do ecossistema.

Produz:

- plano atualizado;
- Work Units criadas, alteradas, bloqueadas, reabertas ou canceladas;
- novas dependências;
- alterações de prioridade;
- alterações de sequência;
- novas necessidades de agentes/Skills/modelos;
- necessidade de revisão humana;
- justificativas e impacto das mudanças.

---

## 3. Papel no ciclo adaptativo

O ciclo é:

```text
PLAN
 ↓
EXECUTE
 ↓
EVALUATE
 ↓
NEW INFORMATION
 ↓
REPLAN
 ↓
NEW PLAN
 ↓
EXECUTE
 ↺
```

O projeto não possui necessariamente um único planejamento inicial.

Ele possui:

```text
baseline inicial
+
atualizações controladas
```

---

## 4. Princípio de continuidade

Uma mudança não deve provocar reinicialização desnecessária do projeto inteiro.

O Orchestrator deve preservar:

- artefatos válidos;
- decisões válidas;
- Work Units concluídas;
- resultados aceitos;
- dependências ainda válidas;
- contexto relevante;
- histórico.

Isso aproveita diretamente o princípio existente no legado de que mudanças devem atingir somente o conjunto afetado quando possível.

---

## 5. Trigger de replanejamento

Replanning pode ser acionado por:

### Resultado de agente

```text
novo conhecimento
contradição
falha
nova dependência
nova lacuna
```

### Mudança de projeto

```text
requisito alterado
escopo alterado
prioridade alterada
decisão humana
```

### Mudança de ambiente

```text
modelo indisponível
Skill alterada
ferramenta indisponível
custo alterado
runtime alterado
```

### Avaliação

```text
resultado rejeitado
resultado condicionado
risco descoberto
qualidade insuficiente
```

### Continuidade

```text
informação histórica relevante
novo padrão
evidência de desempenho
```

---

## 6. Replanning não é sinônimo de correção

Correção trata um problema localizado.

Replanning revisa o plano de trabalho em razão do problema.

Exemplo:

```text
resultado incorreto
 ↓
correção
```

pode ser suficiente.

Mas:

```text
resultado incorreto
 ↓
descoberta de que duas Work Units dependem de uma decisão inexistente
```

pode exigir:

```text
replanejamento
```

---

## 7. Replanning não deve ocorrer por qualquer alteração

Uma mudança deve ser classificada antes de replanejar.

Categorias conceituais:

```text
LOCAL
CONTEXTUAL
STRUCTURAL
CRITICAL
UNKNOWN IMPACT
```

Essa classificação reutiliza diretamente o modelo de impacto do legado.

---

## 8. Mudança local

Exemplo:

```text
correção documental
```

Impacto restrito.

Tratamento:

```text
corrigir
→ validar
→ continuar
```

Sem replanejamento global.

---

## 9. Mudança contextual

Afeta uma Work Unit ou suas dependências próximas.

Tratamento:

```text
identificar conjunto afetado
→ atualizar
→ revalidar
→ continuar
```

---

## 10. Mudança estrutural

Afeta:

- arquitetura;
- divisão do projeto;
- dependências fundamentais;
- requisitos centrais;
- baseline.

Pode exigir:

```text
replanejamento significativo
+
nova validação
+
possível nova baseline
```

---

## 11. Impacto desconhecido

Se o Orchestrator não conseguir determinar o impacto com confiança suficiente:

```text
IMPACT_UNKNOWN
```

Deve:

- ampliar análise;
- consultar agente especialista;
- solicitar informação;
- escalar ao desenvolvedor quando necessário.

O legado já estabelece que impacto desconhecido exige atenção antes de ação potencialmente relevante.

---

## 12. Estado necessário para replanejamento

O Orchestrator deve manter uma visão suficientemente atualizada de:

```text
Project State
├── objetivos
├── escopo
├── requisitos
├── decisões
├── Work Units
├── dependências
├── estados
├── artefatos
├── riscos
├── resultados
├── pendências
├── baselines
└── histórico
```

Sem estado confiável, o replanejamento pode produzir um plano incorreto.

---

## 13. Replanning como delta

Preferir:

```text
PLANO ATUAL
+
MUDANÇA
=
PLANO ATUALIZADO
```

em vez de:

```text
PLANO ATUAL
→ apagar
→ reconstruir tudo
```

O delta deve identificar:

- o que mudou;
- por que mudou;
- quais elementos são afetados;
- quais permanecem válidos.

---

## 14. Identificação do conjunto afetado

O Orchestrator deve localizar:

```text
elemento alterado
↓
dependências diretas
↓
dependências indiretas relevantes
↓
Work Units afetadas
↓
artefatos afetados
```

A análise deve ser proporcional ao impacto.

Isso reutiliza diretamente os mecanismos de impacto e coerência global do legado.

---

## 15. Work Units afetadas

Uma Work Unit pode ser classificada como:

```text
UNCHANGED
ADJUSTED
BLOCKED
REOPENED
CANCELLED
REPLACED
NEW
```

Exemplo:

```text
Requisito R1 mudou
        ↓
Work Unit A → REOPENED
Work Unit B → ADJUSTED
Work Unit C → BLOCKED
Work Unit D → UNCHANGED
```

---

## 16. Preservação do trabalho válido

O Orchestrator não deve reabrir automaticamente tudo que está relacionado ao elemento alterado.

Deve determinar:

```text
o que realmente depende da alteração
```

Se uma Work Unit permanece válida:

```text
não reabrir
```

Isso reduz retrabalho.

---

## 17. Replanejamento por impacto

Uma pequena alteração textual pode produzir grande impacto semântico.

Da mesma forma, uma grande alteração textual pode ter baixo impacto.

Portanto:

> **Tamanho da alteração não determina a extensão do replanejamento.**

Esse princípio já existe no legado e deve ser reutilizado diretamente.

---

## 18. Revisão da baseline

Quando uma alteração afeta significativamente a estrutura:

```text
baseline atual
 ↓
análise
 ↓
nova proposta
 ↓
aprovação
 ↓
nova baseline
```

A baseline anterior deve permanecer no histórico.

---

## 19. Replanning e aprovação

Nem toda atualização exige decisão humana.

Pode ocorrer:

```text
baixo impacto
+
autoridade disponível
+
evidência suficiente
```

→ Orchestrator atualiza.

Pode exigir:

```text
alto impacto
ou
decisão estratégica
ou
regra de negócio
```

→ consulta ao desenvolvedor.

Isso reutiliza a governança existente do legado.

---

## 20. Repriorização

Mudanças podem alterar a prioridade das Work Units.

Exemplo:

```text
Tarefa C
prioridade normal
```

após nova informação:

```text
C → BLOCKER
```

O Orchestrator deve recalcular a fila de trabalho.

---

## 21. Reordenação

Uma nova dependência pode alterar a ordem:

```text
A → B → C
```

e depois:

```text
A → D
D → B
```

O plano deve ser atualizado sem eliminar o que já estiver concluído.

---

## 22. Paralelismo dinâmico

Replanning pode:

```text
aumentar paralelismo
```

quando novas informações provarem independência.

Ou:

```text
reduzir paralelismo
```

quando uma nova dependência surgir.

Exemplo:

```text
antes:
A || B || C

depois:
A
↓
B || C
```

---

## 23. Bloqueios

Quando uma dependência é perdida:

```text
Work Unit
→ BLOCKED
```

O Orchestrator deve determinar:

- causa;
- dependência;
- trabalho alternativo;
- necessidade de resolução;
- impacto no restante do plano.

---

## 24. Work Around

Quando uma tarefa está bloqueada, o Orchestrator pode procurar trabalho não bloqueado.

Exemplo:

```text
B bloqueada
```

mas:

```text
C independente
```

Então:

```text
executar C
```

em vez de deixar o sistema inativo.

Isso aproveita o princípio legado de continuar trabalho não bloqueador quando apropriado.

---

## 25. Criação de novas Work Units

Replanning pode descobrir trabalho não previsto.

Exemplo:

```text
Agent A
→ descoberta:
"é necessária análise de segurança"
```

Então:

```text
NEW WORK UNIT
"Security Analysis"
```

A nova unidade deve possuir:

- objetivo;
- escopo;
- prioridade;
- dependências;
- critérios;
- responsável futuro.

---

## 26. Cancelamento

Uma Work Unit pode deixar de ser necessária.

O Orchestrator pode marcá-la:

```text
CANCELLED
```

quando:

- requisito removido;
- estratégia alterada;
- trabalho substituído;
- resultado torna a tarefa desnecessária.

O histórico deve preservar a razão.

---

## 27. Substituição

Uma Work Unit pode ser substituída por outra estratégia.

Exemplo:

```text
implementação manual
```

substituída por:

```text
integração existente
```

Nesse caso:

```text
WORK UNIT A → SUPERSEDED
WORK UNIT B → NEW
```

---

## 28. Reabertura

Uma Work Unit concluída pode ser reaberta quando:

- dependência relevante mudou;
- resultado posterior contradiz o trabalho;
- requisito alterado;
- defeito detectado;
- decisão estrutural afetada.

O legado já estabelece a lógica de reabertura seletiva e revalidação do conjunto afetado.

---

## 29. Replanning após rejeição

Quando Result Evaluation retorna:

```text
RETURNED_FOR_REVISION
```

o Orchestrator pode:

```text
devolver ao mesmo agente
```

ou:

```text
selecionar outro agente
```

ou:

```text
alterar Skill
```

ou:

```text
alterar modelo
```

ou:

```text
decompor a tarefa
```

A escolha depende da causa da rejeição.

---

## 30. Replanning após conflito entre agentes

Se:

```text
Agent A → opção X
Agent B → opção Y
```

o Orchestrator deve decidir se:

- uma alternativa prevalece;
- é necessária nova análise;
- é necessária revisão independente;
- é necessária decisão humana.

O conflito deve alimentar o replanejamento quando alterar dependências ou decisões.

---

## 31. Replanning após falha do agente

Uma falha pode indicar:

```text
retry
```

ou:

```text
selecionar outro modelo
```

ou:

```text
selecionar outro agente
```

ou:

```text
alterar contexto
```

ou:

```text
dividir a Work Unit
```

ou:

```text
replanejar
```

A causa precisa ser considerada antes de repetir.

---

## 32. Replanning após falha de modelo

Quando o modelo não entregar qualidade suficiente:

```text
modelo atual
 ↓
evidência de insuficiência
 ↓
Resource / Model Selection
 ↓
novo modelo
 ↓
retry/reexecution
```

A mudança precisa ser registrada para gerar evidência histórica.

---

## 33. Replanning por custo

O custo observado pode ser diferente do previsto.

Exemplo:

```text
custo estimado = baixo
custo real = alto
```

O Orchestrator pode:

- trocar modelo;
- reduzir contexto;
- reduzir número de agentes;
- simplificar plano;
- alterar estratégia.

A qualidade mínima deve permanecer protegida.

---

## 34. Replanning por qualidade

Se a qualidade observada estiver abaixo do esperado:

```text
qualidade insuficiente
```

o Orchestrator pode:

```text
revisar
+
trocar configuração
+
adicionar especialista
+
adicionar revisão
```

Não deve aumentar recursos automaticamente sem analisar causa.

---

## 35. Replanning por descoberta de conhecimento

Um agente pode descobrir:

```text
nova regra
nova dependência
nova restrição
novo risco
```

O Orchestrator deve determinar se a descoberta é:

```text
local
contextual
estrutural
```

e planejar a resposta proporcionalmente.

---

## 36. Replanning por mudança do ecossistema

O ecossistema pode mudar durante o projeto:

```text
modelo removido
Skill atualizada
provider indisponível
ferramenta alterada
runtime atualizado
```

O Orchestrator deve verificar se a alteração afeta:

```text
tarefas futuras
tarefas em execução
resultados aceitos
```

e replanejar somente o necessário.

---

## 37. Replanning e estabilidade

Após uma mudança importante, o Orchestrator deve evitar alterar tudo novamente em reação imediata a pequenas oscilações.

Pode ser necessário utilizar:

```text
stability window
```

ou outro mecanismo futuro para evitar instabilidade excessiva.

A implementação exata será definida posteriormente.

---

## 38. Replanning em cascata

Uma alteração pode causar:

```text
A muda
 ↓
B é afetado
 ↓
C depende de B
 ↓
D depende de C
```

O Orchestrator precisa diferenciar:

```text
impacto direto
```

de:

```text
impacto indireto
```

e avaliar a propagação de forma controlada.

---

## 39. Limite da propagação

Não é necessário abrir todo o projeto automaticamente.

O Orchestrator deve usar:

```text
impact analysis
+
dependency graph
+
risk
```

para determinar até onde a propagação deve ser analisada.

Isso reutiliza diretamente o diagnóstico adaptativo do legado:

```text
local
→ contextual
→ global
```

quando necessário.

---

## 40. Replanning e documentação

Quando o plano mudar de forma relevante, o Orchestrator deve atualizar os artefatos de estado apropriados.

A documentação não deve registrar apenas o estado final.

Deve preservar, conforme a importância:

```text
mudança
+
motivo
+
impacto
+
decisão
+
novo estado
```

---

## 41. Justificativa de mudança

Uma mudança relevante deve poder ser representada por:

```text
Change
├── trigger
├── current_state
├── proposed_change
├── reason
├── evidence
├── impact
├── risks
├── affected_units
├── decision
└── resulting_state
```

Essa estrutura deriva diretamente do modelo de decisão e impacto do conhecimento legado.

---

## 42. Replanning e autoridade

Quando o replanejamento atingir uma decisão de negócio:

```text
não decidir autonomamente
```

O Orchestrator deve preparar:

```text
questão
+
contexto
+
alternativas
+
impacto
+
riscos
+
recomendação
```

e escalar.

---

## 43. Replanning e reversibilidade

Alterações de plano devem ser preferencialmente:

- rastreáveis;
- auditáveis;
- reversíveis quando possível.

Isso é coerente com o princípio de reversibilidade do legado.

---

## 44. Replanning e histórico

Cada versão relevante do plano deve possuir histórico suficiente para responder:

```text
qual era o plano?
o que mudou?
por que mudou?
quem/qual mecanismo decidiu?
qual evidência existia?
```

Não é necessário preservar cada microajuste se ele não possuir relevância operacional ou histórica.

---

## 45. Replanning e aprendizado

Um padrão recorrente pode revelar:

```text
"esta categoria de Work Unit sempre exige revisão de segurança"
```

Isso gera:

```text
conhecimento candidato
```

Não deve alterar automaticamente a metodologia ou política do Orchestrator.

Essa regra aproveita diretamente o princípio de aprendizagem pós-projeto do legado.

---

## 46. Replanning e seleção de recursos

Quando o plano muda, as escolhas anteriores de agentes/Skills/modelos podem deixar de ser válidas.

O Orchestrator deve reexecutar, conforme necessário:

```text
Agent & Skill Analysis
+
Resource / Model Selection
```

somente para as partes afetadas.

---

## 47. Replanning e delegação

Quando o plano muda durante uma execução, o Orchestrator deve decidir:

```text
deixar execução continuar
cancelar
pausar
alterar configuração
reexecutar
```

A decisão depende do impacto e do custo de interromper.

---

## 48. Replanning e trabalho em andamento

Uma Work Unit em execução pode ficar:

```text
CONTINUE
PAUSE
CANCEL
RESTART
RECONFIGURE
```

O Orchestrator deve evitar cancelar trabalho útil sem motivo.

---

## 49. Critério de estabilidade do novo plano

Depois de replanejar, o Orchestrator deve verificar:

```text
coerência
+
dependências
+
recursos
+
critérios
+
custos
+
riscos
+
continuidade
```

Só então o novo plano deve voltar a ser considerado operacional.

---

## 50. Mini-baseline

Nem todo replanejamento precisa produzir nova baseline global.

Pode haver:

```text
baseline global
+
baseline local
```

quando uma mudança estiver contida em determinado subconjunto.

Essa possibilidade reduz burocracia.

A política exata será definida posteriormente.

---

## 51. Replanning e eficiência

O objetivo não é replanejar com frequência.

O objetivo é:

> **replanejar quando o plano atual deixou de ser suficientemente confiável ou eficiente.**

Replanejamento excessivo também é custo.

---

## 52. Sinais de replanejamento excessivo

Indicadores possíveis:

```text
mudanças muito frequentes
work units reabertas repetidamente
ciclos sem progresso
trocas constantes de agentes
trocas constantes de modelos
oscilações de prioridade
```

Esses sinais podem indicar:

```text
planejamento inicial insuficiente
```

ou:

```text
ambiente excessivamente instável
```

---

## 53. Sinais de replanejamento insuficiente

Também existem sinais opostos:

```text
retrabalho crescente
tarefas executadas com dependências faltantes
muitos resultados rejeitados
bloqueios não tratados
agentes aguardando contexto
```

Nesse caso, o Orchestrator pode estar tolerando um plano inadequado por tempo excessivo.

---

## 54. Decisão adaptativa

Uma decisão de replanejamento deve considerar:

```text
benefício esperado da mudança
vs.
custo da mudança
```

Quando o benefício não justificar o custo, pode ser melhor concluir a unidade atual e ajustar apenas a próxima.

---

## 55. Saída do Replanning

O resultado conceitual pode ser:

```text
REPLAN RESULT
├── trigger
├── impact
├── current_plan
├── proposed_changes
├── affected_units
├── new_units
├── reordered_units
├── blocked_units
├── reopened_units
├── cancelled_units
├── resource_changes
├── rationale
├── approvals
├── new_plan
└── version/history metadata
```

---

## 56. Exemplo completo

### Estado

```text
A → B → C
```

A conclui.

B começa e descobre que existe uma nova regra de negócio.

### Avaliação

A nova regra é confirmada e altera o modelo de domínio.

### Replanning

```text
B → REOPENED
C → BLOCKED
D → NEW WORK UNIT
```

O Orchestrator:

```text
1. atualiza Project State
2. registra mudança
3. analisa impacto
4. cria D
5. ajusta dependências
6. reavalia agentes/Skills
7. atualiza fila
8. retoma o trabalho liberado
```

Não reinicia A porque A permanece válido.

---

## 57. Exemplo de mudança de modelo

```text
Work Unit
→ Architecture Review

Configuração:
Agent A + Skill Architecture + Model X
```

Durante execução:

```text
Model X
→ qualidade insuficiente
```

Replanning local:

```text
Resource / Model Selection
→ Model Y

mesma Work Unit
→ nova execução
```

A estrutura do projeto permanece.

---

## 58. Exemplo de nova dependência

```text
Agent Architecture
→ descobre:
"Deployment depende de decisão de infraestrutura."
```

Replanning:

```text
Deployment Work Unit
→ BLOCKED

Infrastructure Decision
→ NEW

Deployment
→ depende de Infrastructure Decision
```

Outras Work Units independentes continuam normalmente.

---

## 59. Exemplo de mudança estrutural

```text
Requisito central alterado
```

Impacto:

```text
alto
```

Então:

```text
parar avanço de unidades afetadas
↓
analisar impacto global
↓
consultar especialista
↓
revisar baseline
↓
aprovar novo plano
↓
retomar
```

---

## 60. Integração com Continuity & Learning

Toda alteração relevante do plano deve poder gerar:

```text
historical event
```

e potencialmente:

```text
learning candidate
```

O aprendizado deve ser avaliado posteriormente.

---

## 61. Conhecimento legado reutilizado

Esta capacidade aproveita diretamente:

- análise de impacto;
- dependências;
- paralelismo;
- granularidade;
- estados;
- baseline;
- reabertura;
- reversibilidade;
- evidência;
- modelo de decisão;
- suficiência;
- diagnóstico adaptativo;
- evolução governada;
- aprendizagem pós-projeto.

O legado já estabelece que mudanças relevantes devem ser avaliadas quanto ao impacto e que uma unidade validada pode ser reaberta quando alteração posterior a afetar.

---

## 62. Conhecimento novo

O novo conhecimento específico inclui:

- gatilhos de replanejamento;
- replanejamento incremental;
- atualização da fila de trabalho;
- mutação controlada de Work Units;
- substituição de recursos;
- replanejamento durante execução;
- reconfiguração após feedback operacional;
- controle de oscilação de planos;
- distinção entre mudança local e estrutural no contexto multiagente.

---

## 63. Limites

Replanning não deve:

- reiniciar o projeto sem necessidade;
- reabrir todo o trabalho por qualquer alteração;
- alterar políticas do desenvolvedor;
- cancelar trabalho útil sem justificativa;
- trocar agentes/modelos sem analisar impacto;
- transformar uma descoberta não confirmada em requisito;
- ignorar baselines e decisões existentes;
- mascarar instabilidade do planejamento.

---

## 64. Critérios de sucesso

Replanning estará suficientemente desenvolvido quando o Orchestrator puder:

1. detectar gatilhos relevantes;
2. classificar impacto;
3. localizar o conjunto afetado;
4. preservar trabalho válido;
5. atualizar Work Units;
6. criar novas Work Units quando necessário;
7. reordenar tarefas;
8. bloquear/desbloquear;
9. reabrir unidades afetadas;
10. cancelar trabalho obsoleto;
11. reavaliar recursos quando necessário;
12. controlar paralelismo;
13. evitar reinicialização global;
14. justificar mudanças;
15. preservar histórico;
16. escalar decisões fora da autoridade;
17. retornar a um plano operacional estável.

---

## 65. Princípio operacional consolidado

> **Replanning deve adaptar o plano ao estado real do projeto preservando o máximo de trabalho válido e alterando somente o conjunto necessário, com análise proporcional de impacto, dependências, risco, custo e autoridade.**

---

## 66. Fluxo completo

```text
EVENT / RESULT / CHANGE
        ↓
DETECT
        ↓
CLASSIFY IMPACT
        ↓
IDENTIFY AFFECTED SET
        ↓
PRESERVE VALID WORK
        ↓
UPDATE DEPENDENCIES / STATES
        ↓
CREATE / ADJUST / BLOCK / REOPEN / CANCEL
        ↓
REASSESS AGENTS / SKILLS / MODELS
        ↓
BUILD UPDATED PLAN
        ↓
VALIDATE PLAN
        ↓
APPROVE IF REQUIRED
        ↓
EXECUTE
        ↺
```

---

## 67. Estado

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
- `ORCHESTRATOR-DELEGATION-AND-COORDINATION.md`
- `ORCHESTRATOR-RESULT-EVALUATION.md`

### Próxima capacidade

**Continuity & Learning**

Pergunta central:

> **"O que o Orchestrator deve preservar, aprender e reutilizar depois de cada execução, decisão, avaliação e projeto, sem transformar automaticamente qualquer experiência em regra?"**
