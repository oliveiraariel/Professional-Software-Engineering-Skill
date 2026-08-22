# ORCHESTRATOR-REQUIREMENTS

**Projeto:** Adaptive AI Orchestrator  
**Versão:** v0.1 — especificação inicial de requisitos  
**Status:** Em desenvolvimento  
**Base principal:** `PROJECT-DEFINITION.md` + capacidades consolidadas do Orchestrator + conhecimento reutilizado do projeto legado

---

# 1. Objetivo do Documento

Este documento formaliza os requisitos do **Adaptive AI Orchestrator** a partir das capacidades anteriormente consolidadas.

Seu objetivo é transformar a visão e as capacidades do Orchestrator em uma definição:

- clara;
- consistente;
- verificável;
- rastreável;
- suficientemente detalhada para orientar a arquitetura e o desenvolvimento.

O documento mantém a separação entre:

```text
objetivo
≠
necessidade
≠
requisito
≠
regra
≠
restrição
≠
critério de aceitação
≠
solução técnica
```

Essas distinções são herdadas e adaptadas da Etapa 4 do projeto anterior.

A especificação não deve antecipar desnecessariamente:

- estrutura interna de código;
- tecnologia definitiva;
- provider específico;
- runtime específico;
- banco de dados;
- arquitetura técnica detalhada.

Esses elementos pertencem às etapas posteriores.

---

# 2. Origem e base metodológica

O requisito atual foi derivado de quatro fontes principais:

```text
PROJECT-DEFINITION
        ↓
ORCHESTRATOR-CAPABILITIES
        ↓
ORCHESTRATOR-KNOWLEDGE-MAP
        ↓
capacidades detalhadas
```

Além disso, são reutilizados princípios metodológicos consolidados no projeto legado:

- compreensão antes da solução;
- evidência;
- separação conceitual;
- suficiência;
- impacto;
- dependências;
- granularidade;
- validação;
- rastreabilidade;
- governança;
- reversibilidade;
- evolução controlada.

A Etapa 4 do projeto legado consolidou requisitos funcionais, requisitos não funcionais, regras, restrições, critérios de aceitação, rastreabilidade e validação como estrutura adequada para uma especificação de requisitos. Esse modelo é reaproveitado aqui, adaptado ao novo sistema.

---

# 3. Definição do Sistema

O Adaptive AI Orchestrator é uma camada de inteligência de orquestração capaz de analisar projetos, compreender seu contexto, estruturar o trabalho, analisar agentes e Skills, selecionar recursos de execução, delegar trabalho, avaliar resultados, replanejar e preservar aprendizado.

O sistema não é definido como:

```text
um modelo
```

nem:

```text
um agente genérico
```

nem:

```text
um roteador de modelos
```

nem:

```text
uma única Skill
```

Ele é definido como um **agente orquestrador especializado, apoiado por conhecimento estruturado e integrado a um ecossistema de agentes, Skills, modelos e ferramentas**.

---

# 4. Objetivo Geral

O sistema deve permitir que um Orchestrator organize e coordene a execução de projetos por agentes especializados de maneira:

- contextual;
- justificável;
- adaptativa;
- rastreável;
- proporcional;
- economicamente adequada;
- orientada por evidências.

---

# 5. Objetivos Específicos

O sistema deverá ser capaz de:

1. compreender o projeto;
2. manter seu estado;
3. compreender o ecossistema disponível;
4. estruturar o trabalho;
5. revisar estruturas produzidas por especialistas;
6. definir unidades de trabalho;
7. identificar capacidades necessárias;
8. analisar agentes e Skills;
9. selecionar recursos;
10. considerar modelos diferentes conforme a tarefa;
11. delegar trabalho;
12. fornecer contexto adequado;
13. receber resultados estruturados;
14. avaliar resultados;
15. controlar dependências;
16. replanejar;
17. preservar continuidade;
18. registrar evidências;
19. aprender com experiências;
20. preservar autoridade do desenvolvedor.

---

# 6. Escopo

## 6.1 Incluído

O sistema inclui conceitualmente:

- Project Awareness;
- Project Management;
- Ecosystem Awareness;
- Structural Analysis;
- Agent & Skill Analysis;
- Resource / Model Selection;
- Delegation & Coordination;
- Result Evaluation;
- Replanning;
- Continuity & Learning.

Também inclui:

- gestão de Work Units;
- seleção contextual de agentes;
- seleção contextual de Skills;
- seleção contextual de modelos;
- controle de dependências;
- análise de custo;
- avaliação de qualidade;
- histórico;
- evidência;
- continuidade;
- aprendizado controlado.

---

## 6.2 Fora do escopo inicial

O projeto não assume inicialmente:

- substituição do desenvolvedor;
- garantia de escolha ótima de modelo;
- conhecimento perfeito;
- autonomia irrestrita;
- dependência de um único runtime;
- definição fixa de quantidade de agentes;
- execução de todo o trabalho por um único agente;
- conhecimento integral de todos os domínios;
- implementação imediata de um novo framework de agentes;
- criação de infraestrutura equivalente ao OpenClaw/Hermes;
- implementação de todos os agentes especialistas antes do Orchestrator;
- automação obrigatória de toda decisão humana.

---

# 7. Stakeholder Principal

### STK-001 — Desenvolvedor / Responsável pelo Projeto

Responsabilidades e interesses:

- definir objetivos;
- estabelecer restrições;
- definir políticas;
- autorizar recursos;
- escolher limites de autonomia;
- avaliar decisões de alto impacto;
- utilizar o sistema;
- avaliar resultados;
- orientar evolução.

O desenvolvedor mantém autoridade final sobre decisões que ultrapassem a autonomia autorizada.

---

# 8. Necessidades Principais

As necessidades do projeto são:

### NEC-001 — Compreensão global

O responsável precisa que o Orchestrator compreenda suficientemente o projeto para tomar decisões de coordenação.

### NEC-002 — Estruturação adequada

O responsável precisa que o projeto seja transformado em uma estrutura executável e revisável.

### NEC-003 — Especialização

O responsável precisa que tarefas sejam encaminhadas a agentes com conhecimento adequado.

### NEC-004 — Seleção de recursos

O responsável precisa utilizar modelos e agentes proporcionais à complexidade e criticidade das tarefas.

### NEC-005 — Economicidade

O responsável precisa evitar uso desnecessário de agentes, contexto, chamadas e modelos de alto custo.

### NEC-006 — Coordenação

O responsável precisa que agentes trabalhem em uma ordem coerente, respeitando dependências.

### NEC-007 — Qualidade

O responsável precisa que resultados sejam avaliados antes de serem tratados como válidos.

### NEC-008 — Adaptabilidade

O responsável precisa que o plano possa mudar diante de descobertas, falhas ou alterações.

### NEC-009 — Continuidade

O responsável precisa que contexto, decisões e estado sejam preservados.

### NEC-010 — Aprendizagem

O responsável precisa que resultados históricos gerem evidência para melhorar decisões futuras.

---

# 9. Modelo Conceitual do Requisito

A relação principal é:

```text
NECESSIDADE
   ↓
REQUISITO
   ↓
CRITÉRIO DE ACEITAÇÃO
   ↓
VERIFICAÇÃO
```

E, transversalmente:

```text
REGRA
   ↓
REQUISITO

RESTRIÇÃO
   ↓
REQUISITO / DECISÃO

DECISÃO
   ↓
ELEMENTOS AFETADOS
```

---

# 10. Requisitos Funcionais

## RF-ORC-001 — Identificar o projeto

**Descrição:**  
O Orchestrator deve identificar o projeto sobre o qual está operando e manter uma referência inequívoca ao seu contexto e estado.

**Origem:** NEC-001

**Dependências:** Project Awareness

**Critério de aceitação:**

```text
Dado um projeto identificado,
o Orchestrator deve conseguir recuperar
o contexto mínimo necessário para iniciar
uma análise sem confundir o projeto com outro.
```

---

## RF-ORC-002 — Compreender contexto

**Descrição:**  
O Orchestrator deve analisar contexto, objetivos, escopo, restrições, necessidades, requisitos e estado conforme a informação disponível.

**Origem:** NEC-001

**Critério de aceitação:**

O sistema deve produzir uma representação suficientemente estruturada do contexto necessário à tarefa atual.

---

## RF-ORC-003 — Representar incertezas

**Descrição:**  
O Orchestrator deve distinguir informações confirmadas, inferidas, propostas, pendentes, contraditórias ou desconhecidas quando relevante.

**Origem:** NEC-001

**Critério de aceitação:**

Uma informação não confirmada não deve ser apresentada como fato confirmado.

---

## RF-ORC-004 — Manter estado do projeto

**Descrição:**  
O Orchestrator deve manter uma representação do estado operacional do projeto.

**Estado deve poder representar, conforme aplicável:**

- Work Units;
- dependências;
- estados;
- decisões;
- resultados;
- pendências;
- bloqueios;
- baseline;
- histórico relevante.

**Origem:** NEC-009

---

## RF-ORC-005 — Identificar trabalho necessário

**Descrição:**  
O Orchestrator deve identificar o trabalho necessário para atingir os objetivos do projeto.

**Origem:** NEC-002

---

## RF-ORC-006 — Solicitar estruturação especializada

**Descrição:**  
O Orchestrator deve poder delegar a estruturação inicial ou uma reestruturação a um agente especializado quando possuir recursos adequados.

**Origem:** NEC-002

---

## RF-ORC-007 — Avaliar estrutura proposta

**Descrição:**  
O Orchestrator deve avaliar uma estrutura recebida quanto a cobertura, granularidade, dependências, sequência, paralelismo, riscos, critérios e potencial de retrabalho.

**Origem:** NEC-002

---

## RF-ORC-008 — Solicitar correção estrutural

**Descrição:**  
Quando a estrutura proposta não atender aos critérios, o Orchestrator deve poder devolvê-la ao agente responsável para revisão.

**Fluxo:**

```text
REPROVADA
→ feedback
→ revisão
→ nova avaliação
```

---

## RF-ORC-009 — Aprovar estrutura

**Descrição:**  
O Orchestrator deve poder considerar uma estrutura aprovada quando os critérios de suficiência forem atendidos e as pendências impeditivas forem resolvidas.

---

## RF-ORC-010 — Estabelecer baseline estrutural

**Descrição:**  
Após aprovação, o Orchestrator deve poder estabelecer a estrutura aprovada como baseline do projeto.

---

## RF-ORC-011 — Decompor projeto em Work Units

**Descrição:**  
O Orchestrator deve transformar a estrutura aprovada em unidades de trabalho adequadas à execução, avaliação e delegação.

---

## RF-ORC-012 — Definir dependências

**Descrição:**  
O Orchestrator deve identificar e registrar dependências entre Work Units quando relevantes.

---

## RF-ORC-013 — Determinar elegibilidade de execução

**Descrição:**  
O Orchestrator deve determinar quando uma Work Unit possui pré-condições suficientes para iniciar.

Estados conceituais:

```text
BLOCKED
PARTIALLY_READY
READY
```

A nomenclatura final do estado operacional poderá ser refinada na arquitetura.

---

## RF-ORC-014 — Identificar capacidades necessárias

**Descrição:**  
O Orchestrator deve analisar uma Work Unit e determinar as capacidades especializadas necessárias para executá-la.

---

## RF-ORC-015 — Identificar Skills necessárias

**Descrição:**  
O Orchestrator deve identificar Skills que possam fornecer as capacidades necessárias.

---

## RF-ORC-016 — Avaliar agentes elegíveis

**Descrição:**  
O Orchestrator deve identificar agentes capazes de executar uma Work Unit considerando responsabilidades, Skills, ferramentas, contexto, restrições e evidências.

---

## RF-ORC-017 — Detectar lacunas de capacidade

**Descrição:**  
Quando não houver combinação conhecida suficiente de agente e Skill, o Orchestrator deve registrar a lacuna e impedir que ela seja preenchida por invenção.

---

## RF-ORC-018 — Avaliar composição de Skills

**Descrição:**  
O Orchestrator deve poder considerar múltiplas Skills para uma mesma Work Unit quando uma única Skill não cobrir adequadamente a necessidade.

---

## RF-ORC-019 — Avaliar composição de agentes

**Descrição:**  
O Orchestrator deve poder considerar múltiplos agentes quando a especialização, validação, independência ou risco justificarem a composição.

---

## RF-ORC-020 — Evitar fragmentação desnecessária

**Descrição:**  
O Orchestrator não deve dividir uma Work Unit apenas para aumentar o número de agentes.

A divisão deve possuir benefício justificável.

---

## RF-ORC-021 — Selecionar configuração de execução

**Descrição:**  
O Orchestrator deve selecionar, entre configurações elegíveis, aquela que apresentar adequação suficiente ao contexto.

Uma configuração pode compreender:

```text
Agent
+
Skill(s)
+
Model
+
Provider
+
runtime configuration
```

---

## RF-ORC-022 — Selecionar modelos conforme contexto

**Descrição:**  
O Orchestrator deve poder selecionar modelos diferentes para tarefas diferentes, quando os recursos e políticas permitirem.

---

## RF-ORC-023 — Considerar economicidade

**Descrição:**  
Ao selecionar configurações, o Orchestrator deve considerar, conforme aplicável:

- custo;
- quantidade de agentes;
- chamadas;
- contexto;
- coordenação;
- latência;
- qualidade;
- risco;
- retrabalho.

---

## RF-ORC-024 — Respeitar políticas de recursos

**Descrição:**  
O Orchestrator deve respeitar modelos, providers, agentes, ferramentas e demais recursos permitidos pelo desenvolvedor ou pela política do ambiente.

---

## RF-ORC-025 — Preparar delegação

**Descrição:**  
O Orchestrator deve preparar as informações necessárias para a execução de uma Work Unit.

O pacote deve conter, conforme aplicável:

- objetivo;
- escopo;
- contexto;
- entradas;
- dependências;
- restrições;
- Skill;
- agente;
- modelo;
- resultado esperado;
- critérios de conclusão.

---

## RF-ORC-026 — Controlar contexto delegado

**Descrição:**  
O Orchestrator deve transmitir contexto suficiente para execução responsável, evitando contexto desnecessário quando possível.

---

## RF-ORC-027 — Executar handoff

**Descrição:**  
O Orchestrator deve transferir formalmente uma Work Unit ao agente selecionado.

---

## RF-ORC-028 — Acompanhar execução

**Descrição:**  
O Orchestrator deve acompanhar o estado observável das Work Units delegadas.

---

## RF-ORC-029 — Receber resultado estruturado

**Descrição:**  
O Orchestrator deve receber o resultado da execução em formato suficientemente estruturado para permitir avaliação.

---

## RF-ORC-030 — Registrar premissas e incertezas

**Descrição:**  
O Orchestrator deve preservar premissas, incertezas, decisões, problemas e dependências descobertas no resultado.

---

## RF-ORC-031 — Avaliar resultado

**Descrição:**  
O Orchestrator deve avaliar resultados recebidos contra objetivo, escopo, critérios, restrições, dependências, evidências e impacto.

---

## RF-ORC-032 — Aprovar resultado

**Descrição:**  
O Orchestrator deve poder aprovar um resultado quando os critérios aplicáveis forem atendidos.

---

## RF-ORC-033 — Aceitar resultado com condições

**Descrição:**  
O Orchestrator deve poder aceitar um resultado quando pendências não impeditivas forem explicitamente registradas e controladas.

---

## RF-ORC-034 — Devolver resultado para revisão

**Descrição:**  
O Orchestrator deve poder devolver resultados quando houver problemas que possam ser corrigidos.

---

## RF-ORC-035 — Bloquear resultado

**Descrição:**  
O Orchestrator deve poder bloquear o avanço quando não existir base suficiente ou quando a continuidade segura exigir decisão externa.

---

## RF-ORC-036 — Rejeitar resultado

**Descrição:**  
O Orchestrator deve poder rejeitar um resultado que não possa ser incorporado em sua forma atual.

---

## RF-ORC-037 — Identificar impacto do resultado

**Descrição:**  
O Orchestrator deve identificar o impacto potencial de resultados que alterem elementos relevantes do projeto.

---

## RF-ORC-038 — Reabrir unidades afetadas

**Descrição:**  
O Orchestrator deve poder reabrir apenas as unidades afetadas quando uma alteração posterior invalidar ou modificar trabalho previamente concluído.

---

## RF-ORC-039 — Replanejar

**Descrição:**  
O Orchestrator deve poder atualizar o plano quando resultados, mudanças, falhas, custos, dependências ou evidências alterarem as condições de execução.

---

## RF-ORC-040 — Preservar trabalho válido

**Descrição:**  
O Orchestrator deve evitar reiniciar o projeto integralmente quando apenas parte do trabalho for afetada.

---

## RF-ORC-041 — Criar Work Units novas

**Descrição:**  
O Orchestrator deve poder criar novas Work Units quando descobertas, riscos ou requisitos legítimos revelarem trabalho adicional necessário.

---

## RF-ORC-042 — Bloquear unidades dependentes

**Descrição:**  
O Orchestrator deve impedir avanço de unidades que dependam de uma unidade bloqueada quando a dependência for necessária.

Unidades independentes não devem ser bloqueadas automaticamente.

---

## RF-ORC-043 — Continuar trabalho não bloqueador

**Descrição:**  
O Orchestrator deve poder continuar trabalho independente enquanto outra parte do projeto estiver bloqueada, desde que isso seja seguro e útil.

---

## RF-ORC-044 — Registrar decisões

**Descrição:**  
Decisões relevantes devem ser registradas com contexto, evidências, alternativas, impacto, riscos, responsável, resultado e versionamento quando aplicável.

---

## RF-ORC-045 — Manter rastreabilidade

**Descrição:**  
O Orchestrator deve manter relações rastreáveis entre elementos relevantes do projeto.

Exemplo:

```text
Objetivo
→ Necessidade
→ Requisito
→ Work Unit
→ Resultado
→ Critério
→ Avaliação
```

A rastreabilidade deve permitir navegação nas duas direções quando necessário.

---

## RF-ORC-046 — Registrar evidências

**Descrição:**  
Informações relevantes devem possuir, quando possível:

- origem;
- evidência;
- estado;
- confiança;
- impacto.

---

## RF-ORC-047 — Registrar telemetria

**Descrição:**  
Quando disponível, o sistema deve registrar dados relevantes da execução:

- agente;
- Skill;
- modelo;
- custo;
- tempo;
- chamadas;
- retries;
- falhas;
- intervenção;
- qualidade;
- retrabalho.

---

## RF-ORC-048 — Aprender com execução

**Descrição:**  
O Orchestrator deve poder transformar resultados históricos em candidatos a conhecimento para futuras decisões.

---

## RF-ORC-049 — Não generalizar automaticamente

**Descrição:**  
Uma experiência isolada não deve ser convertida automaticamente em regra geral.

---

## RF-ORC-050 — Atualizar conhecimento sobre recursos

**Descrição:**  
O sistema deve poder atualizar informações sobre agentes, Skills, modelos, providers e outros recursos quando novas evidências ou mudanças forem observadas.

---

## RF-ORC-051 — Registrar conhecimento específico e geral

**Descrição:**  
O sistema deve distinguir conhecimento específico do projeto de conhecimento potencialmente reutilizável.

---

## RF-ORC-052 — Preservar histórico

**Descrição:**  
O sistema deve preservar histórico relevante de decisões, mudanças, resultados e evolução do projeto.

---

## RF-ORC-053 — Recuperar continuidade

**Descrição:**  
O Orchestrator deve ser capaz de recuperar o estado suficiente para continuar o projeto sem depender exclusivamente de memória da sessão atual.

---

## RF-ORC-054 — Avaliar seleção após execução

**Descrição:**  
O Orchestrator deve comparar, quando possível, a configuração escolhida com o resultado efetivamente obtido.

---

## RF-ORC-055 — Avaliar eficiência

**Descrição:**  
O sistema deve poder avaliar eficiência considerando resultado obtido em relação a:

- tempo;
- custo;
- número de agentes;
- contexto;
- coordenação;
- retrabalho.

---

## RF-ORC-056 — Registrar falhas de coordenação

**Descrição:**  
O sistema deve poder distinguir falhas de:

- planejamento;
- seleção;
- Skill;
- contexto;
- delegação;
- agente;
- modelo;
- ferramenta;
- integração;
- avaliação.

---

## RF-ORC-057 — Escalar decisões

**Descrição:**  
O Orchestrator deve solicitar intervenção humana quando uma decisão ultrapassar sua autoridade ou quando o impacto, risco ou incerteza exigirem.

---

## RF-ORC-058 — Preparar decisão para o desenvolvedor

**Descrição:**  
Quando precisar de intervenção, o Orchestrator deve apresentar, quando aplicável:

- questão;
- contexto;
- evidências;
- alternativas;
- impacto;
- riscos;
- recomendação.

Essa estrutura deriva diretamente do modelo de decisão consolidado no legado.

---

## RF-ORC-059 — Preservar autoridade humana

**Descrição:**  
O Orchestrator não deve assumir autoridade sobre decisões pertencentes ao desenvolvedor.

---

## RF-ORC-060 — Suportar revisão independente

**Descrição:**  
O Orchestrator deve poder solicitar revisão independente de resultados quando criticidade, impacto, incerteza ou política justificarem.

---

# 11. Requisitos Não Funcionais

Os requisitos não funcionais são adaptativos. Não devem ser tratados como checklist universal. Sua necessidade depende do contexto de implementação e operação.

## RNF-ORC-001 — Rastreabilidade

Decisões e eventos relevantes devem poder ser relacionados aos elementos que os originaram e aos resultados que produziram.

---

## RNF-ORC-002 — Auditabilidade

Ações relevantes do Orchestrator devem possuir histórico suficiente para reconstruir:

```text
o que aconteceu
→ por que aconteceu
→ qual recurso foi utilizado
→ qual resultado ocorreu
```

---

## RNF-ORC-003 — Explicabilidade operacional

Recomendações e decisões relevantes devem possuir justificativas observáveis, sem exigir exposição de cadeia privada de raciocínio do modelo.

---

## RNF-ORC-004 — Determinismo estrutural

Para um mesmo estado, configuração e política, o sistema deve buscar comportamento consistente sempre que o runtime e os modelos permitirem.

O projeto não exige determinismo absoluto de modelos generativos.

---

## RNF-ORC-005 — Extensibilidade

A arquitetura deve permitir adicionar:

- novos agentes;
- novas Skills;
- novos modelos;
- novos providers;
- novas ferramentas;
- novos runtimes.

sem reescrever o núcleo conceitual do Orchestrator.

---

## RNF-ORC-006 — Portabilidade de conhecimento

O conhecimento desenvolvido pelo projeto não deve ficar conceitualmente preso a OpenClaw.

Deve poder ser adaptado a outros runtimes compatíveis.

---

## RNF-ORC-007 — Modularidade

As responsabilidades do Orchestrator devem permanecer separadas conforme as capacidades definidas.

---

## RNF-ORC-008 — Baixo acoplamento

O núcleo de orquestração não deve depender diretamente de detalhes específicos de um provider, modelo ou runtime quando uma abstração adequada puder ser utilizada.

---

## RNF-ORC-009 — Coesão

Cada componente deve possuir responsabilidade clara e relacionada.

---

## RNF-ORC-010 — Manutenibilidade

O sistema deve poder evoluir Skills, prompts, agentes, regras e componentes sem exigir alterações desnecessárias em todo o sistema.

---

## RNF-ORC-011 — Observabilidade

Execuções relevantes devem possuir informações suficientes para diagnosticar:

- custo;
- latência;
- falhas;
- retries;
- resultados;
- uso de agentes;
- uso de modelos.

---

## RNF-ORC-012 — Segurança

O sistema deve respeitar:

- permissões;
- políticas;
- limites de ferramentas;
- controle de acesso;
- proteção de informações sensíveis.

---

## RNF-ORC-013 — Integridade

O sistema não deve permitir que resultados não avaliados sejam tratados automaticamente como estado confiável quando critérios de validação forem exigidos.

---

## RNF-ORC-014 — Reversibilidade

Alterações relevantes devem ser rastreáveis e reversíveis quando tecnicamente possível.

---

## RNF-ORC-015 — Proporcionalidade

O nível de processamento, documentação, avaliação e coordenação deve ser proporcional a:

- impacto;
- risco;
- complexidade;
- incerteza;
- criticidade.

---

## RNF-ORC-016 — Eficiência

O sistema deve evitar:

- delegação desnecessária;
- múltiplos agentes sem benefício;
- contexto redundante;
- retries sem causa justificável;
- replanejamento excessivo.

---

## RNF-ORC-017 — Economicidade

A arquitetura deve permitir análise do custo total da execução, incluindo custo de modelos, coordenação, contexto, retries e retrabalho quando os dados estiverem disponíveis.

---

## RNF-ORC-018 — Consistência

O sistema deve preservar coerência entre elementos relacionados do projeto.

---

## RNF-ORC-019 — Continuidade

A execução de um projeto não deve depender exclusivamente do contexto volátil de uma única sessão.

---

## RNF-ORC-020 — Atualização de conhecimento

Conhecimento dinâmico sobre modelos, providers, preços e capacidades deve poder ser atualizado sem reescrever a metodologia do Orchestrator.

---

## RNF-ORC-021 — Versionamento

Mudanças relevantes em:

- Skills;
- prompts;
- regras;
- agentes;
- modelos;
- políticas;
- conhecimento;

devem poder ser versionadas quando o impacto justificar.

---

## RNF-ORC-022 — Isolamento de projetos

O sistema deve evitar mistura acidental de contexto, memória ou conhecimento específico entre projetos distintos.

---

## RNF-ORC-023 — Privacidade

Dados sensíveis não devem ser incorporados ao conhecimento compartilhado ou histórico de forma indiscriminada.

---

## RNF-ORC-024 — Escalabilidade

A solução deve permitir crescimento de:

- agentes;
- Skills;
- Work Units;
- projetos;
- registros históricos;

sem exigir alteração estrutural do conceito central.

A estratégia técnica de escalabilidade será definida posteriormente.

---

## RNF-ORC-025 — Confiabilidade

Falhas de agente, modelo, ferramenta ou provider não devem causar perda silenciosa do estado do projeto.

---

## RNF-ORC-026 — Recuperabilidade

O sistema deve permitir recuperar o trabalho até um estado consistente após falhas relevantes, quando o ambiente técnico possibilitar.

---

## RNF-ORC-027 — Testabilidade

Os principais comportamentos de orquestração devem poder ser verificados de maneira isolada e integrada.

---

## RNF-ORC-028 — Interoperabilidade

A arquitetura deve permitir adaptação para diferentes runtimes de agentes sem alterar os conceitos centrais de:

```text
Work Unit
Task Package
Result Package
Agent
Skill
Model
Evaluation
Replanning
```

---

# 12. Regras de Orquestração

As seguintes regras são tratadas como **Regras de Orquestração**, não como requisitos funcionais.

## RO-001 — Compreender antes de delegar

Uma Work Unit não deve ser delegada quando o contexto necessário for insuficiente para uma execução responsável.

---

## RO-002 — Selecionar por capacidade

A análise deve partir da necessidade da tarefa e chegar ao recurso.

```text
necessidade
→ capacidade
→ Skill
→ agente
→ modelo
```

---

## RO-003 — Modelo não é agente

Um agente e um modelo são entidades conceitualmente distintas.

---

## RO-004 — Não existe modelo universalmente melhor

A seleção deve ser contextual.

---

## RO-005 — Não fragmentar sem benefício

A divisão só deve ocorrer quando houver benefício justificável.

---

## RO-006 — Dependências precedem execução

Uma unidade dependente não deve iniciar antes de possuir suas pré-condições necessárias.

---

## RO-007 — Produção não é conclusão

```text
produzir
→ avaliar
→ corrigir
→ reavaliar
→ concluir
```

quando aplicável.

---

## RO-008 — Bloqueio é diferente de reprovação

```text
REPROVADA
→ pode ser corrigida autonomamente

BLOQUEADA
→ continuidade autônoma não é possível ou autorizada
```

Essa distinção é diretamente herdada do legado.

---

## RO-009 — Bloqueio não se propaga indiscriminadamente

Somente unidades dependentes afetadas devem ser bloqueadas.

---

## RO-010 — Preservar trabalho válido

O Orchestrator não deve reiniciar trabalho não afetado por uma mudança.

---

## RO-011 — Replanejar por impacto

O nível de replanejamento deve ser proporcional ao impacto.

---

## RO-012 — Evidência antes de conclusão

Informações relevantes devem ser fundamentadas quando possível.

---

## RO-013 — Não inventar

Ausência de informação não pode ser transformada em fato.

---

## RO-014 — Autonomia contextual

Autonomia depende de:

```text
evidência
+
incerteza
+
impacto
+
reversibilidade
+
sensibilidade
+
autoridade
```

---

## RO-015 — Segurança acima da autonomia

Quando houver conflito:

```text
segurança / integridade
>
autonomia
```

---

## RO-016 — Desenvolvedor mantém autoridade

O Orchestrator recomenda, coordena e executa dentro dos limites autorizados, mas não assume autoridade indevida.

---

## RO-017 — Aprendizado não altera regras automaticamente

Experiências geram evidência e candidatos a melhoria.

---

## RO-018 — Conhecimento específico não contamina automaticamente conhecimento geral

Um aprendizado de projeto deve ser avaliado antes de virar padrão global.

---

## RO-019 — Contexto deve ser proporcional

O Orchestrator deve fornecer contexto suficiente, evitando transferência redundante.

---

## RO-020 — Economicidade é multidimensional

A menor despesa monetária não é necessariamente a melhor configuração.

---

# 13. Casos de Uso Principais

## UC-ORC-001 — Inicializar projeto

**Ator principal:** Desenvolvedor

**Objetivo:** iniciar o Orchestrator com um novo projeto.

**Fluxo:**

```text
projeto fornecido
→ identificar projeto
→ carregar contexto
→ diagnosticar
→ identificar lacunas
→ preparar estado inicial
```

**Resultado:** projeto pronto para estruturação.

---

## UC-ORC-002 — Estruturar projeto

```text
Orchestrator
→ solicita estrutura
→ agente especializado produz
→ Orchestrator revisa
→ aprova ou devolve
```

---

## UC-ORC-003 — Criar Work Units

```text
estrutura aprovada
→ decomposição
→ Work Units
→ dependências
→ critérios
```

---

## UC-ORC-004 — Selecionar agente

```text
Work Unit
→ identificar capacidade
→ identificar Skills
→ candidatos
→ elegibilidade
```

---

## UC-ORC-005 — Selecionar modelo

```text
candidatos
→ políticas
→ criticidade
→ complexidade
→ custo
→ contexto
→ histórico
→ seleção
```

---

## UC-ORC-006 — Delegar trabalho

```text
configuração selecionada
→ Task Package
→ pré-condições
→ handoff
→ execução
```

---

## UC-ORC-007 — Avaliar resultado

```text
Result Package
→ critérios
→ avaliação
→ aceitar / revisar / bloquear / rejeitar
```

---

## UC-ORC-008 — Replanejar

```text
resultado / mudança / falha
→ impacto
→ conjunto afetado
→ atualização
→ novo plano
```

---

## UC-ORC-009 — Recuperar continuidade

```text
retomar projeto
→ recuperar estado
→ recuperar decisões
→ identificar pendências
→ identificar próxima ação
```

---

## UC-ORC-010 — Aprender com execução

```text
execução
→ telemetria
→ avaliação
→ evidência
→ candidato a conhecimento
→ futura melhoria
```

---

# 14. Casos de Uso de Exceção

## UC-EXC-001 — Informação insuficiente

```text
informação necessária ausente
→ identificar lacuna
→ avaliar impacto
→ continuar parcialmente
ou
→ solicitar informação
```

---

## UC-EXC-002 — Nenhum agente elegível

```text
Work Unit
→ nenhum agente adequado
→ capability gap
→ registrar
→ buscar alternativa
→ escalar quando necessário
```

---

## UC-EXC-003 — Modelo indisponível

```text
modelo escolhido
→ indisponível
→ verificar fallback
→ nova seleção
```

---

## UC-EXC-004 — Resultado reprovado

```text
resultado
→ REPROVADA
→ análise
→ correção
→ nova execução
→ reavaliação
```

---

## UC-EXC-005 — Resultado bloqueado

```text
resultado
→ BLOQUEADA
→ impedir avanço dependente
→ preparar decisão
→ intervenção humana ou nova evidência
```

---

## UC-EXC-006 — Conflito entre agentes

```text
resultado A
vs.
resultado B
→ detectar divergência
→ analisar evidências
→ revisar
ou
→ solicitar decisão
```

---

## UC-EXC-007 — Descoberta estrutural

```text
agente encontra dependência inesperada
→ registrar
→ avaliar impacto
→ replanejar
```

---

# 15. Critérios de Aceitação Globais

A especificação do Orchestrator deve ser considerada suficientemente definida quando:

```text
objetivos compreendidos
+
necessidades identificadas
+
escopo definido
+
requisitos funcionais formalizados
+
requisitos não funcionais tratados
+
regras de orquestração definidas
+
critérios de aceitação suficientes
+
rastreabilidade suficiente
+
consistência verificada
+
verificabilidade suficiente
+
sem bloqueios impeditivos
+
suficiência atingida
```

---

# 16. Critérios de Aceitação por Capacidade

## CA-PROJ — Project Awareness

O sistema deve representar suficientemente contexto, objetivos, estado, decisões, dependências e incertezas relevantes.

## CA-MGT — Project Management

O sistema deve conseguir manter Work Units, dependências, prioridade, estados e fluxo de execução.

## CA-ECO — Ecosystem Awareness

O sistema deve identificar recursos disponíveis, capacidades, restrições e elegibilidade.

## CA-STR — Structural Analysis

O sistema deve revisar uma estrutura produzida por especialista e aprová-la ou devolvê-la para correção.

## CA-AGT — Agent & Skill Analysis

O sistema deve identificar capacidades, Skills e agentes adequados.

## CA-RES — Resource / Model Selection

O sistema deve selecionar configurações considerando adequação, custo, risco e políticas.

## CA-DEL — Delegation & Coordination

O sistema deve enviar e acompanhar Work Units com contexto suficiente e receber resultados estruturados.

## CA-EVL — Result Evaluation

O sistema deve avaliar resultados e produzir decisão de aceitação, revisão, bloqueio ou rejeição.

## CA-RPL — Replanning

O sistema deve atualizar o plano diante de mudanças e preservar trabalho não afetado.

## CA-LRN — Continuity & Learning

O sistema deve preservar estado e histórico e produzir conhecimento candidato com base em evidências.

---

# 17. Matriz de Rastreabilidade de Alto Nível

| Necessidade | Capacidades | Requisitos principais | Critério |
|---|---|---|---|
| NEC-001 Compreensão global | Project Awareness | RF-001 a RF-004 | CA-PROJ |
| NEC-002 Estruturação | Structural Analysis | RF-005 a RF-011 | CA-STR |
| NEC-003 Especialização | Agent & Skill Analysis | RF-014 a RF-020 | CA-AGT |
| NEC-004 Seleção | Resource / Model Selection | RF-021 a RF-024 | CA-RES |
| NEC-005 Economicidade | Management + Resource Selection | RF-023, RNF-017, RO-020 | CA-MGT / CA-RES |
| NEC-006 Coordenação | Delegation & Coordination | RF-025 a RF-030, RF-042 | CA-DEL |
| NEC-007 Qualidade | Result Evaluation | RF-031 a RF-040 | CA-EVL |
| NEC-008 Adaptabilidade | Replanning | RF-037 a RF-043 | CA-RPL |
| NEC-009 Continuidade | Continuity & Learning | RF-044 a RF-053 | CA-LRN |
| NEC-010 Aprendizagem | Continuity & Learning | RF-047 a RF-056 | CA-LRN |

---

# 18. Matriz de Rastreabilidade das Capacidades

```text
Project Awareness
→ RF-001..RF-004
→ RNF-001..RNF-004
→ RO-001, RO-012, RO-013

Project Management
→ RF-005, RF-011..RF-013, RF-042, RF-043
→ RNF-015, RNF-016
→ RO-005, RO-006, RO-011

Ecosystem Awareness
→ RF-024, RF-050
→ RNF-005, RNF-006, RNF-020, RNF-028
→ RO-002, RO-003, RO-004

Structural Analysis
→ RF-006..RF-011
→ RF-037..RF-040
→ RO-005, RO-010, RO-011

Agent & Skill Analysis
→ RF-014..RF-020
→ RF-017, RF-060
→ RO-002, RO-005

Resource / Model Selection
→ RF-021..RF-024, RF-054
→ RNF-016, RNF-017
→ RO-004, RO-020

Delegation & Coordination
→ RF-025..RF-030, RF-042, RF-056
→ RNF-011, RNF-013, RNF-025
→ RO-006, RO-019

Result Evaluation
→ RF-031..RF-040, RF-060
→ RNF-001..RNF-004, RNF-018
→ RO-007, RO-012, RO-013

Replanning
→ RF-037..RF-043
→ RF-055, RF-056
→ RO-010, RO-011

Continuity & Learning
→ RF-044..RF-056
→ RNF-001, RNF-002, RNF-011, RNF-019..RNF-023
→ RO-012, RO-018
```

---

# 19. Requisitos de Verificabilidade

Cada requisito deve possuir uma forma razoável de verificar atendimento.

Os métodos de verificação podem incluir:

```text
inspeção documental
análise lógica
teste funcional
teste de integração
teste de sistema
simulação
execução controlada
avaliação de artefato
observação operacional
```

O método específico será definido posteriormente quando o sistema estiver implementado.

---

# 20. Tipos de validação

A validação do Orchestrator pode incluir:

### Validação documental

Verifica especificações e artefatos.

### Validação lógica

Verifica coerência das relações.

### Validação funcional

Verifica comportamento do sistema.

### Validação de integração

Verifica comunicação entre Orchestrator, agentes, Skills, modelos e runtime.

### Validação operacional

Verifica uso real.

### Validação empírica

Avalia desempenho observado ao longo de execuções.

---

# 21. Validação da própria especificação

A especificação deve ser avaliada quanto a:

```text
completude suficiente
consistência
clareza
não ambiguidade
rastreabilidade
verificabilidade
coerência com capacidades
coerência com objetivos
coerência com escopo
```

Resultado:

```text
APROVADA
ou
REPROVADA
```

`BLOQUEADA` permanece um estado operacional, não resultado normativo de validação.

Essa distinção é diretamente consolidada no legado.

---

# 22. Tratamento da reprovação

```text
REPROVADA
→ analisar
→ corrigir
→ revalidar
```

Quando a continuidade não puder ser resolvida autonomamente:

```text
REPROVADA
→ BLOQUEADA
→ intervenção humana
```

---

# 23. Limites desta fase

Este documento não define ainda:

- arquitetura técnica;
- estrutura de classes;
- APIs;
- banco;
- linguagem;
- runtime;
- OpenClaw como dependência obrigatória;
- Hermes como dependência obrigatória;
- schema físico do catálogo;
- implementação do grafo;
- implementação de memória;
- prompt final;
- estrutura final de `SKILL.md`.

Essas decisões pertencem às próximas fases.

---

# 24. Requisitos de qualidade de implementação futuros

Quando a implementação começar, os requisitos devem ser traduzidos para uma arquitetura que preserve:

```text
responsabilidades claras
baixo acoplamento
alta coesão
interfaces explícitas
testabilidade
observabilidade
extensibilidade
manutenibilidade
rastreabilidade
```

O projeto deve evitar código monolítico concentrando todas as responsabilidades em um único módulo do Orchestrator.

---

# 25. Relação com o futuro Orchestrator Prompt

Este documento não é o prompt final do Orchestrator.

Os requisitos servirão posteriormente para derivar:

```text
requisitos
→ comportamento
→ regras
→ Skill
→ prompt
→ ferramentas
→ avaliações
```

O prompt deverá expressar principalmente:

- papel;
- prioridades;
- limites;
- comportamento;
- política de decisão.

Conhecimento aprofundado deverá permanecer distribuído entre Skill, referências, estado e demais mecanismos apropriados.

---

# 26. Relação com futuras Skills especializadas

Os requisitos também servirão para determinar conhecimento que poderá ser delegado a agentes especialistas.

Por exemplo:

```text
Requisitos do Orchestrator
        ↓
Requirement Knowledge
        ↓
Requirements Skill

Architecture Knowledge
        ↓
Architecture Skill

Documentation Knowledge
        ↓
Documentation Skill

Testing Knowledge
        ↓
Testing Skill
```

O Orchestrator continuará responsável pela coordenação e avaliação global.

---

# 27. Princípio de desenvolvimento

A implementação futura deve preservar:

```text
especificação
→ arquitetura
→ design
→ código
→ integração
→ validação
```

sem inverter a ordem apenas por conveniência de implementação.

---

# 28. Critério de conclusão da fase de requisitos

A fase estará conceitualmente concluída quando:

```text
objetivos compreendidos
+
necessidades identificadas
+
escopo definido
+
RF definidos
+
RNF definidos
+
regras de orquestração definidas
+
casos de uso principais definidos
+
critérios de aceitação definidos
+
rastreabilidade suficiente
+
consistência verificada
+
verificabilidade suficiente
+
sem bloqueios impeditivos
```

Então:

```text
VALIDAÇÃO APROVADA
→ GATE
→ REQUISITOS CONSOLIDADOS
```

---

# 29. Estado atual

**Status:** ESPECIFICAÇÃO INICIAL CONSOLIDADA.

Esta versão representa a primeira especificação formal dos requisitos do Adaptive AI Orchestrator.

A especificação deverá ser reavaliada antes do avanço para a arquitetura, especialmente quanto a:

- consistência;
- sobreposição entre requisitos;
- requisitos ausentes;
- rastreabilidade;
- verificabilidade;
- limites de autonomia.

---

# 30. Próxima fase

Depois da validação desta especificação, o próximo nível será:

## Arquitetura do Sistema

A arquitetura deverá determinar:

```text
quais componentes existem
+
quais responsabilidades possuem
+
como se comunicam
+
quais estados compartilham
+
quais limites existem
+
como o runtime será integrado
```

Somente nessa fase deverá ser definido como os conceitos atuais serão materializados tecnicamente.

---

# 31. Fechamento

A especificação atual transforma as dez capacidades do Orchestrator em uma definição verificável de comportamento.

O modelo completo é:

```text
PROJECT
   ↓
UNDERSTAND
   ↓
STRUCTURE
   ↓
DECOMPOSE
   ↓
ANALYZE AGENTS / SKILLS
   ↓
SELECT RESOURCES
   ↓
DELEGATE
   ↓
EXECUTE
   ↓
EVALUATE
   ↓
REPLAN
   ↓
PRESERVE / LEARN
   ↺
```

Este ciclo constitui a base funcional para a futura arquitetura e implementação do Adaptive AI Orchestrator.
