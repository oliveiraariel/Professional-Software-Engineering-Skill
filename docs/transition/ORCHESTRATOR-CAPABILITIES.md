# ORCHESTRATOR-CAPABILITIES

**Projeto:** Adaptive AI Orchestrator  
**Versão:** v0.1 — definição inicial  
**Status:** Em desenvolvimento  
**Dependência:** `PROJECT-DEFINITION.md`

---

## 1. Propósito

Este documento define as capacidades centrais que o **Adaptive AI Orchestrator** deverá possuir para cumprir a visão estabelecida em `PROJECT-DEFINITION.md`.

O objetivo não é definir ainda a implementação técnica dessas capacidades, nem determinar de antemão quais ferramentas, frameworks, modelos ou fornecedores serão utilizados.

O objetivo é estabelecer **o que o Orchestrator precisa ser capaz de compreender, decidir, coordenar, avaliar e preservar**.

A implementação poderá utilizar a infraestrutura de ecossistemas de agentes existente, como OpenClaw, Hermes ou outra plataforma compatível. O diferencial pretendido deste projeto está no conhecimento, nas políticas, no raciocínio operacional e nas instruções que orientam o comportamento do Orchestrator.

---

## 2. Princípio central

O Orchestrator deverá possuir conhecimento suficientemente aprofundado sobre o projeto e sobre o ecossistema no qual opera para decidir **quando executar, quando delegar, para quem delegar, qual capacidade especializada utilizar, em que condições iniciar uma unidade de trabalho e como avaliar o resultado recebido**.

Possuir conhecimento sobre uma área não implica executar diretamente essa área.

O Orchestrator deve poder conhecer profundamente determinada disciplina e, ainda assim, delegar sua execução a um agente especialista com Skill e modelo adequados.

---

# 3. Capacidades Fundamentais

## 3.1 Project Awareness

### Objetivo

Construir e manter uma representação global e suficientemente profunda do projeto em execução.

### Deve compreender, conforme aplicável

- problema e contexto;
- objetivos;
- escopo;
- necessidades;
- requisitos;
- domínio;
- restrições;
- decisões;
- artefatos;
- dependências;
- riscos;
- estado atual;
- lacunas e incertezas;
- impactos de mudanças.

### Resultado esperado

O Orchestrator deve saber **onde o projeto está, o que já foi estabelecido, o que falta e quais condições limitam o próximo trabalho**.

---

## 3.2 Project Management

### Objetivo

Gerenciar o trabalho necessário para levar o projeto de seu estado atual ao estado pretendido.

### Capacidades

- identificar trabalho necessário;
- decompor trabalho;
- estabelecer prioridades;
- controlar dependências;
- sequenciar unidades de trabalho;
- identificar possibilidades de paralelismo;
- controlar bloqueios;
- liberar trabalho quando suas pré-condições forem satisfeitas;
- acompanhar progresso;
- detectar retrabalho potencial;
- replanejar quando necessário.

### Princípio

O processo deve ser **sequencial por dependência**, não necessariamente por calendário.

O Orchestrator não deve iniciar uma unidade apenas porque ela está disponível se suas dependências ainda não estiverem suficientemente estabelecidas.

---

## 3.3 Ecosystem Awareness

### Objetivo

Conhecer o ecossistema operacional no qual o Orchestrator está integrado.

### Deve representar, conforme disponível

- agentes;
- responsabilidades dos agentes;
- Skills;
- capacidades fornecidas pelas Skills;
- modelos;
- providers;
- ferramentas;
- mecanismos de delegação;
- memória e contexto;
- limites de execução;
- restrições definidas pelo desenvolvedor.

### Resultado esperado

O Orchestrator deve saber **quais recursos existem, o que cada recurso pode fazer, quais combinações são permitidas e quais são suas limitações relevantes**.

---

## 3.4 Structural Analysis

### Objetivo

Analisar e validar a estrutura necessária para transformar o projeto em trabalho executável.

### Comportamento esperado

O Orchestrator pode delegar a construção da estrutura a um agente especializado.

Fluxo esperado:

```text
Orchestrator
→ solicita estruturação
→ agente especialista produz estrutura
→ Orchestrator analisa
→ aprova ou devolve observações
→ agente corrige
→ Orchestrator revalida
→ estrutura aprovada
```

### A análise deve considerar, conforme aplicável

- cobertura;
- coerência;
- granularidade;
- dependências;
- sequência;
- paralelismo;
- lacunas;
- duplicações;
- riscos;
- custo de coordenação;
- potencial de retrabalho;
- critérios de conclusão.

A aprovação da estrutura deve preceder a execução estruturada quando a estrutura for relevante para o projeto.

---

## 3.5 Agent & Skill Analysis

### Objetivo

Relacionar cada unidade de trabalho às capacidades especializadas necessárias para sua execução.

### Deve responder

- qual capacidade é necessária;
- qual Skill fornece essa capacidade;
- quais agentes possuem ou podem utilizar essa Skill;
- quais são as limitações do agente;
- quais entradas o agente necessita;
- quais resultados o agente deve produzir;
- quais dependências existem;
- qual nível de especialização é necessário.

### Princípio

O Orchestrator não deve escolher agentes apenas por nome ou disponibilidade. A escolha deve ser baseada na relação entre **responsabilidade, capacidade, Skill, contexto e requisitos da unidade de trabalho**.

---

## 3.6 Resource and Model Selection

### Objetivo

Selecionar recursos de execução adequados à unidade de trabalho dentro das políticas e limites definidos pelo desenvolvedor.

A decisão poderá envolver:

```text
unidade de trabalho
→ Skill necessária
→ agentes elegíveis
→ modelos elegíveis
→ seleção de recursos
```

### Fatores possíveis

- capacidade requerida;
- complexidade;
- criticidade;
- qualidade esperada;
- especialização;
- custo;
- latência;
- contexto disponível;
- disponibilidade;
- risco;
- custo de coordenação;
- risco de retrabalho.

### Princípio de governança

O desenvolvedor define recursos autorizados, limites e políticas de uso. O Orchestrator realiza a alocação operacional dentro dessas regras.

Modelo não é identidade do agente. Um mesmo agente poderá utilizar modelos diferentes conforme a unidade de trabalho e as circunstâncias.

---

## 3.7 Delegation & Coordination

### Objetivo

Delegar trabalho de maneira contextual, suficiente e economicamente adequada.

Uma delegação deve fornecer, conforme aplicável:

- objetivo;
- escopo;
- contexto relevante;
- artefatos de entrada;
- restrições;
- dependências;
- critério de sucesso;
- formato esperado de resultado;
- necessidade de revisão.

### A coordenação deve permitir

- delegação;
- acompanhamento;
- handoff;
- recebimento;
- integração;
- sincronização;
- bloqueio e liberação;
- encerramento da unidade.

### Princípio de economicidade

Delegar mais não significa necessariamente obter melhor resultado. O Orchestrator deve considerar o custo de múltiplos agentes, compartilhamento de contexto, coordenação, latência e retrabalho.

---

## 3.8 Result Evaluation

### Objetivo

Avaliar criticamente os resultados produzidos pelos agentes antes de incorporá-los ao projeto.

### Deve verificar, conforme aplicável

- correção;
- completude;
- coerência;
- aderência ao objetivo;
- aderência às decisões existentes;
- dependências;
- impactos;
- rastreabilidade;
- qualidade;
- novas lacunas;
- riscos;
- necessidade de retrabalho.

### Fluxo

```text
resultado
→ avaliação
→ aprovado

ou

resultado
→ avaliação
→ problemas
→ feedback
→ revisão do agente
→ nova avaliação
```

Produzir um resultado não significa concluí-lo.

---

## 3.9 Replanning

### Objetivo

Reavaliar o plano quando novas informações ou resultados modificarem as condições do projeto.

O Orchestrator deverá poder reagir a:

- novos requisitos;
- novas dependências;
- erros;
- resultados inesperados;
- bloqueios;
- alterações de prioridade;
- alterações de escopo;
- mudanças de custo ou disponibilidade;
- descoberta de lacunas;
- necessidade de reabertura.

### Princípio

O planejamento é adaptativo. Uma estrutura aprovada fornece estabilidade, mas não impede mudanças justificadas.

---

## 3.10 Continuity & Learning

### Objetivo

Preservar conhecimento operacional e utilizar experiências anteriores para melhorar decisões futuras.

### Deve preservar, conforme aplicável

- estado;
- decisões;
- justificativas;
- resultados;
- erros;
- avaliações;
- feedback;
- histórico;
- evidências;
- lições aprendidas;
- conhecimento candidato a reutilização.

### Princípio

Aprendizado não deve alterar silenciosamente regras fundamentais. Mudanças metodológicas relevantes devem ser avaliadas, rastreadas e governadas.

---

# 4. Relação entre as capacidades

As capacidades não devem ser tratadas como funções isoladas.

O comportamento esperado do Orchestrator forma um ciclo:

```text
Project Awareness
        ↓
Project Management
        ↓
Structural Analysis
        ↓
Agent & Skill Analysis
        ↓
Resource / Model Selection
        ↓
Delegation & Coordination
        ↓
Execution by specialist agents
        ↓
Result Evaluation
        ↓
Replanning
        ↓
Continuity & Learning
        ↺
Project Awareness
```

`Ecosystem Awareness` atua transversalmente sobre o ciclo, fornecendo conhecimento sobre os recursos disponíveis para as decisões de delegação e seleção.

---

# 5. Relação com agentes especialistas

O Orchestrator não deve concentrar toda a execução.

Exemplo conceitual:

```text
Orchestrator
    ↓
identifica necessidade de arquitetura
    ↓
Architecture Skill
    ↓
Architecture Agent
    ↓
resultado
    ↓
Orchestrator avalia
    ↓
aprova / solicita revisão
    ↓
integra ao Project Knowledge
    ↓
planeja próximas unidades
```

O mesmo princípio pode ser aplicado a agentes de:

- requisitos;
- modelagem;
- dados;
- implementação;
- testes;
- documentação;
- segurança;
- revisão;
- outras especializações identificadas pelo projeto.

O conjunto final de agentes não é fixo e deve ser determinado conforme as características do projeto.

---

# 6. Relação entre conhecimento do Orchestrator e conhecimento dos especialistas

O Orchestrator deve possuir conhecimento suficientemente aprofundado para:

- compreender o trabalho especializado;
- avaliar se a delegação é necessária;
- selecionar o agente adequado;
- avaliar a resposta recebida;
- detectar problemas;
- decidir a próxima ação.

Isso não implica que o Orchestrator deva executar pessoalmente todas as especialidades.

Parte do conhecimento poderá posteriormente ser transformada em Skills para agentes especialistas.

Assim:

```text
Master / Knowledge Base
        ↓
conhecimento reutilizável
        ├── Orchestrator Knowledge
        ├── Skill Knowledge
        ├── Component Knowledge
        └── outros destinos definidos posteriormente
```

A distribuição definitiva do conhecimento será determinada durante a transição e o desenvolvimento do novo projeto.

---

# 7. Dependências conceituais

As seguintes relações são fundamentais:

```text
Projeto
  ↓
Work Unit
  ↓
Capacidade necessária
  ↓
Skill
  ↓
Agente elegível
  ↓
Modelo elegível
  ↓
Execução
  ↓
Resultado
  ↓
Avaliação
  ↓
Estado atualizado
  ↓
Próxima decisão
```

Uma unidade de trabalho não deve ser iniciada quando dependências relevantes ainda não estiverem suficientemente satisfeitas, salvo decisão explícita dentro das regras de autonomia e governança.

---

# 8. Economicidade

O Orchestrator deverá buscar uma relação adequada entre:

```text
capacidade
+ qualidade
+ risco
+ tempo
+ custo
+ coordenação
+ retrabalho
```

O objetivo não é minimizar isoladamente o número de agentes ou o preço do modelo.

O objetivo é encontrar uma organização de trabalho proporcional ao problema.

Um agente de menor custo poderá ser preferível quando possuir capacidade suficiente para a unidade de trabalho. Um modelo de maior capacidade poderá ser justificável quando a criticidade, complexidade ou risco da unidade exigir.

---

# 9. Conhecimento necessário por capacidade

A próxima fase do projeto deverá detalhar, para cada capacidade:

```text
Capacidade
→ conhecimento necessário
→ decisões necessárias
→ entradas
→ saídas
→ critérios de sucesso
→ conhecimento já existente
→ lacunas
```

A análise do projeto legado deverá ocorrer de forma direcionada por essas necessidades.

O conhecimento legado não será automaticamente incorporado ao novo projeto. Cada conteúdo deverá ser avaliado quanto à pertinência, aplicabilidade e destino.

---

# 10. Relação com o projeto legado

O projeto legado é uma fonte de conhecimento potencialmente reutilizável, não uma estrutura normativa do novo projeto.

O processo previsto é:

```text
necessidade do novo Orchestrator
        ↓
identificar conhecimento necessário
        ↓
verificar conhecimento legado
        ↓
avaliar aplicabilidade
        ↓
reaproveitar / adaptar / complementar / rejeitar
```

A análise do legado deve ocorrer depois que as necessidades do novo projeto estiverem suficientemente definidas.

---

# 11. Critério de conclusão desta definição

Esta definição será considerada suficiente quando cada capacidade possuir:

- propósito claro;
- responsabilidade definida;
- relação com as demais capacidades;
- principais entradas e saídas compreendidas;
- conhecimento necessário identificável;
- critérios de avaliação definíveis;
- limites conceituais suficientemente claros para permitir a próxima fase.

O detalhamento de implementação não pertence a este documento.

---

# 12. Próximo trabalho

O próximo trabalho consiste em detalhar:

```text
Capacidade
→ conhecimento necessário
→ conhecimento existente
→ lacunas
→ desenvolvimento necessário
```

A consulta ao projeto legado deverá ser feita de forma seletiva a partir desse mapeamento.
