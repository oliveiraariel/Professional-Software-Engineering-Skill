# ORCHESTRATOR — PROJECT MANAGEMENT

**Projeto:** Adaptive AI Orchestrator  
**Capacidade:** Project Management  
**Versão:** v0.1 — definição conceitual inicial  
**Status:** Definição conceitual  
**Base:** `PROJECT-DEFINITION.md`, `ORCHESTRATOR-CAPABILITIES.md`, `ORCHESTRATOR-PROJECT-AWARENESS.md` e conhecimento reutilizável do projeto legado

---

## 1. Propósito

Project Management é a capacidade do Orchestrator de transformar o conhecimento atual do projeto em um plano de trabalho executável, controlando prioridades, dependências, sequência, paralelismo, bloqueios, progresso, mudanças e replanejamento.

O objetivo não é produzir um cronograma rígido. O objetivo é manter uma representação operacional do trabalho que permita ao Orchestrator determinar:

- o que precisa ser feito;
- o que precisa ser feito primeiro;
- o que pode ser executado em paralelo;
- o que ainda não pode começar;
- quais recursos devem ser alocados;
- quando uma unidade de trabalho está pronta;
- quando um resultado exige correção;
- quando o plano deve ser alterado.

Project Management opera sobre o conhecimento mantido por Project Awareness e transforma esse conhecimento em decisões de execução.

---

## 2. Responsabilidade central

A responsabilidade central é manter o projeto em um estado de execução controlado, no qual cada unidade de trabalho possua contexto, objetivo, dependências e condições suficientes para ser executada com baixo risco de retrabalho.

O Orchestrator deve buscar continuamente:

```text
estado atual
    ↓
trabalho necessário
    ↓
dependências
    ↓
prioridade
    ↓
unidades liberáveis
    ↓
alocação de recursos
    ↓
execução
    ↓
resultado
    ↓
atualização do estado
    ↓
replanejamento
```

---

## 3. Limite da capacidade

Project Management não executa diretamente as responsabilidades técnicas dos agentes especialistas.

O Orchestrator deve gerenciar o trabalho, enquanto os agentes especialistas executam as unidades que lhes forem atribuídas.

```text
Orchestrator
    ↓
planeja e coordena
    ↓
Work Unit
    ↓
Agent + Skill + Model
    ↓
execução especializada
```

O Orchestrator pode possuir conhecimento profundo sobre a área relacionada à unidade de trabalho para planejar e avaliar sua execução, sem assumir a responsabilidade operacional de executá-la diretamente.

---

## 4. Relação com Project Awareness

Project Management depende diretamente de Project Awareness.

```text
Project Awareness
    ↓
"qual é o estado atual?"
    ↓
Project Management
    ↓
"o que deve acontecer agora?"
```

Project Awareness mantém a representação do projeto.

Project Management utiliza essa representação para determinar trabalho, prioridade, sequência, dependências, estado operacional e próxima ação.

Uma mudança relevante no Project Knowledge pode provocar replanejamento.

---

## 5. Modelo de trabalho

O projeto deve ser representado como um conjunto de unidades de trabalho relacionadas por dependências, objetivos, resultados e critérios de conclusão.

A divisão não deve ser arbitrária.

Uma unidade deve existir quando sua separação trouxer benefício real para pelo menos uma das seguintes funções:

- execução;
- validação;
- decisão;
- rastreabilidade;
- controle de risco;
- especialização;
- paralelismo controlado.

O conhecimento legado já estabelece que a granularidade deve ser proporcional ao benefício e que o projeto não deve ser fragmentado arbitrariamente.

---

## 6. Unidade de trabalho

A unidade operacional básica do Project Management deverá ser a **Work Unit**.

Uma Work Unit deve possuir, conforme aplicável:

```text
WORK UNIT
├── identificador
├── objetivo
├── descrição
├── escopo
├── entradas
├── saídas esperadas
├── artefatos relacionados
├── conhecimento necessário
├── Skill necessária
├── agentes elegíveis
├── modelos elegíveis
├── dependências
├── pré-condições
├── prioridade
├── criticidade
├── impacto esperado
├── risco
├── estado
├── critério de início
├── critério de conclusão
├── resultado observado
└── histórico
```

Nem todos os atributos precisam ser preenchidos para toda unidade. A profundidade deve ser proporcional à complexidade, risco, impacto e necessidade de controle.

---

## 7. Identificação do trabalho

O Orchestrator deve identificar o trabalho necessário a partir de:

- objetivos do projeto;
- requisitos;
- estrutura aprovada;
- lacunas identificadas;
- decisões;
- resultados de agentes;
- problemas encontrados;
- mudanças solicitadas;
- dependências descobertas;
- resultados de validação.

A identificação do trabalho não deve ser feita apenas uma vez.

Novas unidades podem surgir durante a execução quando novas informações, dependências ou problemas forem descobertos.

---

## 8. Decomposição

A decomposição deve transformar o trabalho em unidades suficientemente pequenas para permitir execução e controle, mas suficientemente grandes para evitar fragmentação e coordenação excessivas.

```text
Projeto
  ↓
estrutura aprovada
  ↓
etapas
  ↓
subetapas
  ↓
atividades / Work Units
```

A decomposição deve preservar a relação entre:

```text
objetivo
→ trabalho
→ resultado
→ dependência
→ validação
```

A unidade deve possuir fronteira funcional suficiente para permitir atribuição e avaliação.

---

## 9. Dependências

O Project Management deve representar dependências entre unidades de trabalho.

Uma dependência significa que determinada unidade requer algum resultado, decisão, artefato, informação ou condição antes de poder avançar em uma determinada extensão.

Exemplo:

```text
Requisitos
    ↓
Modelagem
    ↓
Arquitetura
    ↓
Implementação
    ↓
Testes
```

Mas dependências também podem ser parciais:

```text
A ─────→ B
│
└──────→ C
```

onde B depende de A, mas C pode começar com uma parte diferente das informações de A.

O Orchestrator não deve assumir dependência total quando a dependência for parcial.

---

## 10. Estados de disponibilidade

Uma Work Unit deve possuir um estado operacional suficiente para que o Orchestrator saiba se ela pode ou não ser executada.

Estados conceituais mínimos:

```text
NÃO_INICIADA
    ↓
EM_ANÁLISE
    ↓
BLOQUEADA / PARCIALMENTE_LIBERADA / LIBERADA
    ↓
EM_EXECUÇÃO
    ↓
EM_REVISÃO
    ↓
EM_CORREÇÃO
    ↓
VALIDADA
    ↓
CONCLUÍDA
```

Estados adicionais podem existir quando necessários:

- concluída com pendências;
- reaberta;
- cancelada;
- obsoleta.

O uso de estados deve ser consistente com a finalidade operacional.

---

## 11. Critério de início

Uma unidade só deve ser iniciada quando suas condições mínimas de execução forem atendidas.

Essas condições podem incluir:

- dependências necessárias validadas;
- entradas disponíveis;
- decisões necessárias estabelecidas;
- Skill apropriada disponível;
- agente elegível disponível;
- modelo elegível disponível;
- contexto suficiente;
- critérios de sucesso compreendidos;
- ausência de bloqueio relevante.

Uma unidade pode permanecer bloqueada mesmo que um agente esteja disponível.

Disponibilidade do agente não significa prontidão da unidade.

---

## 12. Dependência como controle de retrabalho

Uma das responsabilidades críticas do Orchestrator é reduzir retrabalho causado por execução prematura.

Exemplo problemático:

```text
A ainda não produziu decisão estrutural
        ↓
B começa usando premissas
        ↓
A termina
        ↓
premissas de B tornam-se inválidas
        ↓
B precisa ser refeito
```

O Project Management deve procurar evitar esse padrão mediante análise de dependências e critérios de prontidão.

A execução deve ser sequencial por dependência, mesmo quando várias unidades puderem ser executadas simultaneamente em termos de calendário.

---

## 13. Priorização

Prioridade representa a necessidade relativa de tratar uma unidade em determinado momento.

Ela não deve ser confundida com impacto.

```text
Impacto
→ qual o tamanho das consequências se estiver errado?

Prioridade
→ quão necessário é tratar isso agora?
```

Fatores de priorização podem incluir:

- bloqueio de outras unidades;
- criticidade;
- impacto;
- urgência;
- risco;
- dependências;
- valor para o projeto;
- necessidade de informação para decisões futuras;
- custo de atraso;
- custo de retrabalho;
- disponibilidade de recursos.

Uma unidade de alto impacto pode possuir prioridade futura.
Uma unidade de impacto moderado pode ser imediatamente bloqueadora.

---

## 14. Classes de prioridade

Como representação inicial:

```text
BLOQUEADORA
URGENTE
IMPORTANTE
NORMAL
FUTURA
```

Essa classificação é operacional e poderá ser refinada posteriormente.

A prioridade deve poder mudar durante o projeto.

---

## 15. Paralelismo

O Orchestrator deve detectar oportunidades de execução paralela, mas o paralelismo deve ser controlado.

Uma execução paralela é apropriada quando:

- as dependências necessárias estão satisfeitas;
- as unidades possuem baixo acoplamento;
- os dados necessários estão suficientemente estáveis;
- o risco de retrabalho é aceitável;
- existe benefício real de tempo ou throughput;
- a coordenação adicional não supera esse benefício.

O paralelismo não deve ser usado apenas para aumentar o número de agentes ativos.

```text
mais agentes ativos
≠
mais eficiência
```

---

## 16. Economicidade da execução

Project Management deve considerar o custo total de executar um conjunto de unidades, e não apenas o custo individual de cada chamada.

Devem ser considerados, quando possível:

- custo do modelo;
- quantidade de agentes;
- número de chamadas;
- tamanho do contexto;
- custo de compartilhamento de contexto;
- latência;
- coordenação;
- revisões;
- retrabalho;
- necessidade de sincronização.

O objetivo é buscar uma combinação adequada entre:

```text
capacidade
qualidade
risco
tempo
custo
```

Não existe uma regra de minimizar apenas o número de agentes ou apenas o custo.

---

## 17. Alocação de recursos

Project Management identifica que uma unidade está pronta para execução.

A seleção de agente, Skill e modelo pertence às capacidades relacionadas de Agent & Skill Analysis e Resource / Model Selection.

O fluxo conceitual é:

```text
Project Management
    ↓
Work Unit READY
    ↓
Agent & Skill Analysis
    ↓
Resource / Model Selection
    ↓
Delegation & Coordination
```

Project Management deve fornecer contexto suficiente para que essa seleção seja feita corretamente.

---

## 18. Fila de trabalho

O Orchestrator deve manter uma fila de trabalho lógica baseada no estado das Work Units.

Uma fila pode conter:

```text
READY
BLOCKED
PARTIALLY_RELEASED
RUNNING
WAITING_REVIEW
WAITING_DEPENDENCY
```

A fila não é necessariamente uma lista simples.

Ela representa o conjunto de trabalho e suas relações de dependência, prioridade e disponibilidade.

---

## 19. Seleção da próxima unidade

A seleção da próxima unidade deve considerar simultaneamente:

1. prontidão;
2. prioridade;
3. dependências que serão desbloqueadas;
4. impacto;
5. risco;
6. criticidade;
7. custo;
8. benefício do paralelismo;
9. disponibilidade de recursos;
10. risco de retrabalho.

A decisão deve buscar maximizar o progresso útil, não simplesmente o número de tarefas concluídas.

---

## 20. Execução e acompanhamento

Depois de uma unidade ser liberada e delegada, o Orchestrator deve acompanhar seu estado.

```text
READY
 ↓
ASSIGNED
 ↓
RUNNING
 ↓
RESULT_RECEIVED
 ↓
EVALUATION
```

A execução não deve ser considerada concluída apenas porque o agente retornou uma resposta.

O resultado precisa passar pelo processo de avaliação aplicável.

---

## 21. Tratamento de bloqueios

Quando uma unidade não puder prosseguir, o Orchestrator deve identificar:

- qual dependência bloqueia;
- qual informação falta;
- qual decisão falta;
- qual agente ou Skill está indisponível;
- se existe alternativa segura;
- se a unidade deve permanecer bloqueada;
- se outra unidade pode avançar.

O bloqueio de uma unidade não deve necessariamente bloquear o projeto inteiro.

```text
Projeto
├── Unidade A → CONCLUÍDA
├── Unidade B → BLOQUEADA
├── Unidade C → LIBERADA
└── Unidade D → FUTURA
```

O Orchestrator deve continuar trabalho seguro e não dependente quando isso trouxer benefício.

---

## 22. Dependências parciais

Uma unidade pode avançar parcialmente quando apenas parte de suas dependências estiver disponível e a parte liberada puder ser realizada sem transformar hipótese em fundamento consolidado.

Estados possíveis:

```text
LIBERADA
PARCIALMENTE_LIBERADA
BLOQUEADA
```

A utilização de informação inferida pode servir para exploração e preparação, mas não deve ser confundida com conhecimento validado.

---

## 23. Mudanças durante a execução

O projeto deve aceitar mudanças sem perder controle do planejamento.

Quando uma mudança surgir, o Orchestrator deve:

```text
receber mudança
    ↓
interpretar
    ↓
analisar impacto
    ↓
identificar unidades afetadas
    ↓
verificar dependências
    ↓
recalcular estado quando necessário
    ↓
replanejar somente o necessário
```

A mudança não deve provocar reinicialização desnecessária do projeto inteiro.

---

## 24. Replanejamento

Replanejamento é uma função contínua do Project Management.

Pode ser provocado por:

- nova informação;
- alteração de requisito;
- resultado inesperado;
- falha de agente;
- resultado abaixo do esperado;
- descoberta de dependência;
- mudança de prioridade;
- indisponibilidade de recurso;
- mudança de modelo;
- mudança de custo;
- mudança de risco;
- alteração arquitetural.

O replanejamento deve ser proporcional ao impacto.

```text
mudança pequena
→ ajuste local

mudança média
→ replanejamento parcial

mudança estrutural
→ revisão da baseline
```

---

## 25. Baseline operacional

Depois que uma estrutura de trabalho for aprovada, ela poderá constituir uma baseline operacional.

A baseline fornece um ponto estável para comparar mudanças posteriores.

Uma mudança significativa não deve simplesmente apagar a baseline anterior.

Deve ser possível identificar:

```text
baseline anterior
→ mudança
→ justificativa
→ impacto
→ nova estrutura
```

---

## 26. Reabertura

Uma unidade validada pode ser reaberta quando uma mudança posterior afetar suas premissas, resultado ou dependências.

A reabertura deve ser proporcional ao conjunto afetado.

```text
mudança
 ↓
impacto
 ↓
unidades afetadas
 ↓
reabertura seletiva
 ↓
revalidação
```

Não se deve reabrir o projeto inteiro sem evidência de impacto global.

---

## 27. Critério de conclusão da unidade

Uma Work Unit deve ser considerada concluída quando:

- o trabalho definido foi executado;
- o resultado esperado foi produzido;
- as validações aplicáveis foram realizadas;
- as dependências produzidas estão registradas;
- problemas relevantes foram tratados ou explicitamente registrados como pendências;
- o resultado foi integrado ao estado do projeto.

`RESULT_RECEIVED` não equivale automaticamente a `COMPLETED`.

---

## 28. Critério de conclusão do conjunto de trabalho

Uma etapa ou conjunto de unidades pode ser considerado concluído quando:

- suas unidades necessárias foram concluídas;
- suas dependências relevantes foram satisfeitas;
- seus resultados foram integrados;
- pendências remanescentes são conhecidas e aceitáveis;
- os critérios de gate aplicáveis foram atendidos;
- não existe trabalho bloqueador conhecido sem tratamento.

---

## 29. Integração com Result Evaluation

Project Management produz o contexto operacional para a avaliação.

```text
Work Unit
   ↓
Agent
   ↓
Result
   ↓
Result Evaluation
   ↓
resultado da avaliação
   ↓
Project Management
```

A avaliação pode resultar em:

```text
VALIDADO
REPROVADO
BLOQUEADO
VALIDADO_COM_PENDÊNCIAS
```

O significado operacional exato desses estados será consolidado na capacidade de Result Evaluation.

---

## 30. Integração com Replanning

O Project Management mantém o plano.

Replanning modifica o plano quando as condições mudarem.

```text
Project Management
      ↕
Replanning
      ↕
Project Awareness
```

A separação permite distinguir:

- estado atual do projeto;
- plano atual;
- motivo da mudança do plano.

---

## 31. Intervenção humana

O Orchestrator deve escalar decisões quando:

- uma mudança ultrapassar sua autoridade;
- o impacto for desconhecido;
- houver risco elevado ou crítico;
- uma decisão estratégica estiver em jogo;
- houver implicações importantes de segurança, privacidade ou conformidade;
- a mudança alterar políticas ou governança;
- não houver base suficiente para continuar com segurança.

O agente deve preparar a decisão antes de solicitar intervenção humana sempre que possível.

---

## 32. Telemetria operacional

O Project Management deve produzir ou permitir o registro de informações úteis para avaliação posterior.

Quando disponível, registrar:

- unidade executada;
- agente utilizado;
- Skill utilizada;
- modelo utilizado;
- tempo de execução;
- custo;
- número de revisões;
- falhas;
- bloqueios;
- retrabalho;
- intervenção humana;
- resultado da avaliação;
- motivo de replanejamento.

Esses dados serão fundamentais para a futura avaliação de eficiência e economicidade do Orchestrator.

---

## 33. Conhecimento reutilizável do projeto legado

O `MASTER-SPECIFICATION.md` já possui uma base significativa para esta capacidade.

### Reaproveitamento direto

- granularidade proporcional ao benefício;
- dependências;
- paralelismo controlado;
- execução sequencial por dependência;
- dependências parciais;
- estados de execução;
- ciclo de execução;
- análise de impacto;
- prioridade;
- baseline;
- reabertura;
- validação e revalidação.

A especificação legada explicita que o processo é sequencial por dependência e não necessariamente por calendário, permite paralelismo quando houver benefício real e orienta evitar muitas tarefas abertas quando isso aumentar retrabalho.

### Reaproveitamento com adaptação

- fila de trabalho;
- classificação de prioridades;
- estrutura metodológica;
- mudança estrutural, média, pequena e crítica;
- gates;
- critérios de conclusão;
- aprendizagem pós-projeto.

### Conhecimento novo do Orchestrator

- gerenciamento simultâneo de múltiplos agentes;
- alocação de agentes como recursos cognitivos;
- custo de coordenação multiagente;
- custo de contexto compartilhado;
- gestão de disponibilidade de agentes e modelos;
- combinação entre especialização, custo e disponibilidade;
- priorização considerando capacidade cognitiva disponível;
- decisões de quando delegar e quando não delegar;
- gerenciamento de execução distribuída em runtime de agentes.

---

## 34. O que Project Management não deve decidir sozinho

A capacidade não deve absorver responsabilidades das demais capacidades.

Ela não deve, isoladamente:

- escolher detalhes técnicos de arquitetura;
- determinar qual modelo específico será usado sem utilizar Resource / Model Selection;
- determinar qual Skill é adequada sem Agent & Skill Analysis;
- aceitar definitivamente um resultado sem Result Evaluation;
- modificar políticas fundamentais do sistema;
- inventar requisitos ou decisões de negócio.

Ela deve fornecer o contexto e o estado necessários para essas decisões.

---

## 35. Critérios de sucesso

Project Management será considerada suficientemente definida quando o Orchestrator puder:

1. transformar um projeto compreendido em unidades de trabalho coerentes;
2. representar dependências relevantes;
3. controlar estados de disponibilidade;
4. evitar execução prematura;
5. priorizar trabalho de forma justificável;
6. identificar paralelismo seguro;
7. controlar bloqueios;
8. administrar mudanças sem reinicialização desnecessária;
9. replanejar proporcionalmente ao impacto;
10. integrar resultados e atualizar o plano;
11. registrar informações úteis sobre eficiência, custo e retrabalho;
12. preparar contexto adequado para as capacidades de seleção e delegação.

---

## 36. Dependências com outras capacidades

```text
Project Awareness
       ↓
Project Management
       ├── Structural Analysis
       ├── Agent & Skill Analysis
       ├── Resource / Model Selection
       ├── Delegation & Coordination
       ├── Result Evaluation
       └── Replanning
```

Project Management funciona como capacidade de coordenação entre conhecimento do projeto e execução distribuída.

---

## 37. Princípios operacionais consolidados

1. **Planejar não é executar.** O plano deve orientar a execução, mas pode mudar diante de evidências.
2. **Disponibilidade não é prontidão.** Uma unidade só deve começar quando suas pré-condições estiverem satisfeitas.
3. **Dependência determina sequência.** Calendário não deve prevalecer sobre dependências técnicas ou semânticas.
4. **Paralelismo exige benefício.** Não manter unidades simultâneas apenas para aumentar atividade aparente.
5. **Granularidade deve ter propósito.** Não fragmentar sem benefício operacional.
6. **Retrabalho é um custo de primeira classe.** A decisão de executar agora deve considerar o risco de ter de refazer depois.
7. **Mudanças não implicam reinicialização global.** O impacto deve determinar a abrangência do replanejamento.
8. **Resultados alteram o plano.** A devolutiva dos agentes é informação de gestão, não apenas produto final.
9. **O plano precisa de memória.** Mudanças, decisões e razões de replanejamento devem ser rastreáveis.
10. **Autonomia é condicionada por evidência, impacto, risco e autoridade.**

---

## 38. Estado atual

**Definição conceitual:** consolidada para continuidade.

A capacidade Project Management possui agora uma definição suficientemente detalhada para servir de base ao desenvolvimento das capacidades subsequentes.

### Próximo passo

Detalhar **Ecosystem Awareness**, incluindo o modelo de representação do ecossistema de agentes, Skills, modelos, providers, ferramentas, regras de elegibilidade e limitações de execução.
