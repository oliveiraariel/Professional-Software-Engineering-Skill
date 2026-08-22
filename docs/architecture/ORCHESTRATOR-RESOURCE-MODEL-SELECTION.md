# ORCHESTRATOR-RESOURCE-MODEL-SELECTION

**Projeto:** Adaptive AI Orchestrator  
**Capacidade:** Resource / Model Selection  
**Versão:** v0.1 — definição inicial  
**Status:** Em desenvolvimento

---

## 1. Propósito

A capacidade **Resource / Model Selection** permite ao Orchestrator selecionar, entre os recursos tecnicamente elegíveis, a configuração de execução mais adequada para uma Work Unit.

A seleção pode envolver:

```text
Agent
+
Skill(s)
+
Model
+
Provider
+
Runtime configuration
+
Ferramentas necessárias
```

O objetivo não é simplesmente escolher o recurso de maior capacidade aparente ou menor custo.

O objetivo é encontrar uma configuração proporcional ao problema, considerando:

- capacidade necessária;
- qualidade esperada;
- criticidade;
- complexidade;
- contexto;
- custo;
- latência;
- risco;
- retrabalho;
- disponibilidade;
- histórico;
- restrições;
- políticas do desenvolvedor.

---

## 2. Papel dentro do Orchestrator

A pergunta central desta capacidade é:

> **"Entre as configurações tecnicamente elegíveis, qual oferece a melhor relação entre adequação, qualidade, risco, tempo e custo para esta Work Unit?"**

Ela recebe principalmente:

- Work Unit;
- contexto do projeto;
- requisitos de qualidade;
- dependências;
- candidatos produzidos por Agent & Skill Analysis;
- informações do ecossistema;
- políticas do desenvolvedor;
- conhecimento disponível sobre modelos;
- histórico de desempenho, quando existir.

Ela produz:

- configuração recomendada;
- alternativas;
- justificativa;
- fatores considerados;
- incertezas;
- custo/risco estimados, quando possível;
- condições para execução.

---

## 3. Separação de responsabilidades

A capacidade deve preservar a seguinte divisão:

```text
Project Management
→ define o trabalho e suas condições

Ecosystem Awareness
→ conhece os recursos disponíveis

Agent & Skill Analysis
→ identifica candidatos tecnicamente elegíveis

Resource / Model Selection
→ escolhe a configuração mais adequada

Delegation & Coordination
→ executa a configuração escolhida

Result Evaluation
→ verifica se a escolha funcionou
```

Portanto:

> **selecionar não é executar.**

E:

> **ser elegível não significa ser selecionado.**

---

## 4. Princípio fundamental

A seleção deve começar pela necessidade do projeto e terminar no recurso.

```text
Work Unit
    ↓
Required Capability
    ↓
Eligible Agent / Skill combinations
    ↓
Eligible Models
    ↓
Resource evaluation
    ↓
Configuration selection
```

Nunca deve ocorrer:

```text
Model popular
    ↓
forçar a tarefa ao modelo
```

nem:

```text
Agent disponível
    ↓
procurar qualquer tarefa para utilizá-lo
```

---

## 5. Separação entre identidade e recurso

O modelo não define a identidade do agente.

Exemplo:

```text
Architecture Agent
│
├── Architecture Skill
├── ferramentas
└── modelos elegíveis
    ├── Model A
    ├── Model B
    └── Model C
```

O mesmo papel pode utilizar modelos diferentes em tarefas diferentes.

Da mesma forma, um mesmo modelo pode ser utilizado por agentes diferentes.

Essa separação é requisito arquitetural do projeto.

---

## 6. Autoridade do desenvolvedor

O desenvolvedor permanece responsável por definir:

- modelos permitidos;
- providers permitidos;
- orçamento;
- limites de custo;
- regras de segurança;
- recursos proibidos;
- níveis de autonomia;
- critérios mínimos de qualidade;
- políticas de uso.

O Orchestrator opera dentro dessas políticas.

Portanto:

```text
DEV
 ↓
políticas + limites + recursos autorizados
 ↓
ORCHESTRATOR
 ↓
seleção operacional
```

O Orchestrator não deve alterar silenciosamente essas políticas.

---

## 7. Recursos obrigatórios, preferidos e proibidos

Para uma Work Unit, uma configuração pode estar:

```text
REQUIRED
PREFERRED
ALLOWED
DISCOURAGED
FORBIDDEN
```

Exemplo:

```text
Modelo X
→ permitido

Modelo Y
→ permitido, mas preferível apenas para tarefas críticas

Modelo Z
→ proibido por política
```

A política deve prevalecer sobre qualquer preferência de eficiência.

---

## 8. Fatores de seleção

A seleção pode considerar:

```text
capacidade
qualidade esperada
especialização
complexidade
criticidade
contexto
custo
latência
disponibilidade
risco
retrabalho
estabilidade
histórico
compatibilidade
necessidade de revisão
```

Nem todos os fatores têm o mesmo peso.

O peso deve depender da natureza da Work Unit.

---

## 9. Adequação ao problema

O objetivo não é descobrir:

> "Qual é o melhor modelo?"

Mas:

> **"Qual configuração é suficientemente boa e adequadamente dimensionada para esta tarefa?"**

Isso significa que um modelo frontier pode ser correto em uma tarefa crítica e desnecessário em uma tarefa simples.

Da mesma forma, um modelo menor pode ser inadequado para uma decisão arquitetural crítica mesmo sendo mais barato.

---

## 10. Economicidade

Economicidade deve ser tratada como **otimização da solução**, não simplesmente redução de preço.

Uma configuração barata pode ser pior quando gerar:

```text
mais erros
+
mais retrabalho
+
mais revisões
+
mais chamadas
+
mais contexto
+
maior latência
```

A função conceitual pode ser pensada como:

```text
Valor operacional
=
qualidade
+
adequação
+
risco controlado
+
tempo adequado

versus

custo total
+
coordenação
+
retrabalho
+
contexto
```

Não é necessária uma fórmula matemática fixa nesta fase.

O requisito é que o Orchestrator raciocine explicitamente sobre o conjunto.

---

## 11. Custo total

Quando possível, considerar:

```text
custo do modelo
+
custo das chamadas
+
custo de contexto
+
custo de ferramentas
+
custo de coordenação
+
custo de revisão
+
custo esperado de retrabalho
```

Uma solução com modelo mais caro pode ser globalmente mais econômica quando reduz significativamente retrabalho ou coordenação.

---

## 12. Número de agentes como recurso econômico

A seleção de modelo não pode ser separada do número de agentes.

Exemplo:

```text
Opção A
1 agente forte
1 contexto
1 execução
```

versus:

```text
Opção B
4 agentes especializados
4 contextos
coordenação
handoffs
integração
```

A Opção B não deve ser assumida como superior.

O benefício da especialização precisa superar o custo adicional de coordenação.

---

## 13. Custo de contexto

O Orchestrator deve considerar que cada agente adicional pode exigir:

- contexto inicial;
- transferência de artefatos;
- explicações;
- resultados intermediários;
- sincronização;
- reprocessamento.

Portanto:

```text
Agent count
```

é um recurso econômico e cognitivo.

---

## 14. Seleção de modelos por criticidade

Uma política possível:

```text
baixa criticidade
→ modelo econômico suficiente

média criticidade
→ modelo intermediário

alta criticidade
→ modelo mais capaz

crítica
→ modelo de alta capacidade + revisão
```

Isso é apenas uma estrutura conceitual.

A política concreta deverá considerar contexto, evidência e regras do projeto.

---

## 15. Seleção por complexidade

A complexidade da Work Unit deve influenciar o nível de modelo necessário.

Exemplo:

```text
Tarefa simples
→ geração estruturada/repetitiva

Tarefa média
→ análise contextual

Tarefa complexa
→ raciocínio profundo

Tarefa crítica
→ raciocínio profundo + revisão
```

O Orchestrator não deve utilizar a maior capacidade disponível simplesmente porque ela existe.

---

## 16. Seleção por especialização

Especialização pode justificar o uso de um modelo ou agente diferente quando:

- o domínio é específico;
- a tarefa possui vocabulário especializado;
- o erro é caro;
- existe Skill altamente especializada;
- há histórico demonstrando benefício.

A especialização deve ser tratada como vantagem possível, não como requisito universal.

---

## 17. Seleção por contexto

Modelos e agentes podem possuir diferentes capacidades de contexto.

A seleção deve considerar:

```text
tamanho necessário
+
estrutura do contexto
+
capacidade de retenção
+
necessidade de recuperação
+
custo do contexto
```

Um recurso não deve ser selecionado somente pela capacidade nominal do modelo.

---

## 18. Seleção por latência

Algumas tarefas toleram latência maior.

Outras são altamente interativas.

O Orchestrator deve considerar:

```text
latência aceitável
vs.
qualidade necessária
```

A menor latência não deve prevalecer quando comprometer qualidade crítica.

---

## 19. Disponibilidade

Um recurso pode ser tecnicamente excelente, mas temporariamente indisponível.

A seleção deve considerar:

- disponibilidade atual;
- limites;
- quota;
- rate limits;
- configuração;
- estado do provider;
- capacidade de fallback.

---

## 20. Fallback

Quando o recurso preferencial não estiver disponível, o Orchestrator pode utilizar uma alternativa elegível, desde que:

```text
qualidade mínima
+
política
+
risco aceitável
```

estejam preservados.

Exemplo:

```text
Preferred Model
      ↓
indisponível
      ↓
Fallback 1
      ↓
indisponível
      ↓
Fallback 2
```

As regras para fallback serão definidas posteriormente na arquitetura operacional.

---

## 21. Modelos diferentes por tarefa

O mesmo agente pode executar:

```text
Task A → Model X
Task B → Model Y
Task C → Model Z
```

quando essas escolhas forem permitidas e justificadas.

A identidade do agente permanece estável.

Somente o recurso de inferência varia.

---

## 22. Modelos diferentes durante uma mesma unidade

Também pode ser admissível:

```text
Modelo A
→ produção inicial

Modelo B
→ revisão

Modelo C
→ síntese final
```

Essa composição só deve ser utilizada quando o ganho superar o custo de coordenação e contexto.

---

## 23. Revisão como estratégia de seleção

Em tarefas críticas, o Orchestrator pode preferir:

```text
1 agente de produção
+
1 agente/modelo de revisão
```

em vez de:

```text
1 modelo extremamente caro
```

ou, em outros casos, justamente o contrário.

A decisão deve depender de:

- criticidade;
- confiabilidade histórica;
- custo;
- independência da revisão;
- impacto do erro.

---

## 24. Diversidade de modelos

Quando houver risco de erro correlacionado, diferentes modelos podem ser usados para revisão.

Exemplo:

```text
Agent A / Model X
        ↓
resultado

Agent B / Model Y
        ↓
revisão independente
```

A diversidade só deve ser utilizada quando trouxer benefício real.

Executar os mesmos agentes em paralelo sem ganho esperado é desperdício.

---

## 25. Histórico de desempenho

Quando houver histórico suficiente, a seleção pode considerar:

```text
Task Type
+
Agent
+
Skill
+
Model
+
Resultado
```

e observar:

- qualidade;
- erro;
- retrabalho;
- custo;
- tempo;
- necessidade de intervenção;
- estabilidade.

Essa informação é especialmente importante para o modelo adaptativo do projeto.

---

## 26. Evidência para seleção

A evidência pode ser:

```text
capacidade declarada
benchmark
teste controlado
experiência prática
resultado histórico
feedback
```

Nenhuma fonte isolada deve ser tratada como verdade universal.

O projeto já estabelece que evidências devem ser interpretadas em contexto e que o histórico do próprio sistema é uma dimensão relevante de avaliação.

---

## 27. Confiança da seleção

Toda seleção importante pode possuir:

```text
HIGH CONFIDENCE
MEDIUM CONFIDENCE
LOW CONFIDENCE
UNKNOWN
```

A confiança deve refletir:

- qualidade da informação;
- estabilidade do conhecimento;
- histórico;
- similaridade da tarefa;
- incerteza.

---

## 28. Conhecimento dinâmico de modelos

As informações sobre:

- preços;
- versões;
- disponibilidade;
- contexto;
- APIs;
- capacidades;

podem mudar.

Portanto, o Orchestrator deve tratar essas informações como dados atualizáveis.

Não deve codificá-las permanentemente no prompt.

---

## 29. Seleção não deve depender de ranking absoluto

O sistema não deve operar com:

```text
#1 modelo = sempre melhor
```

O critério deve ser:

```text
adequação contextual
```

Assim:

```text
Modelo A
→ melhor para arquitetura crítica

Modelo B
→ melhor para documentação repetitiva

Modelo C
→ melhor para processamento volumoso
```

A especialização contextual é mais útil do que um ranking único.

---

## 30. Regras de seleção condicionais

As regras podem assumir forma:

```text
SE
criticidade = crítica
E
qualidade exigida = alta
ENTÃO
preferir configuração de alta capacidade
+
revisão
```

ou:

```text
SE
complexidade = baixa
E
volume = alto
E
risco = baixo
ENTÃO
preferir configuração econômica
```

Essas regras serão refinadas quando o modelo de decisão estiver especificado.

---

## 31. Seleção multiobjetivo

A decisão normalmente envolve vários objetivos simultâneos:

```text
Qualidade
Custo
Tempo
Risco
Contexto
Cobertura
```

Portanto, a escolha deve buscar uma solução **suficiente e proporcional**, não uma otimização absoluta de apenas um fator.

---

## 32. Quando duas configurações são equivalentes

Se duas configurações apresentarem resultados esperados semelhantes, deve-se preferir, conforme aplicável:

1. menor custo;
2. menor complexidade;
3. menor coordenação;
4. maior estabilidade;
5. maior reversibilidade;
6. maior facilidade de monitoramento.

A ordem exata pode ser refinada posteriormente.

---

## 33. Quando a escolha é incerta

Se não for possível diferenciar adequadamente duas configurações:

```text
não inventar certeza
```

O Orchestrator deve:

- registrar a incerteza;
- selecionar dentro dos limites permitidos;
- considerar experimento controlado quando o custo justificar;
- submeter a decisão ao desenvolvedor quando o impacto for elevado.

---

## 34. Experimentação controlada

Em tarefas não críticas, pode ser útil executar:

```text
Config A
vs.
Config B
```

com uma amostra limitada.

O objetivo seria obter evidência para futuras execuções.

Esse mecanismo deve ser tratado como:

```text
experimental
```

e não como comportamento obrigatório de toda tarefa.

---

## 35. Seleção e aprendizagem

Uma seleção bem-sucedida gera evidência.

Uma seleção ruim também.

Após a execução:

```text
selection decision
        ↓
actual result
        ↓
compare
        ↓
historical record
```

Isso permite melhorar futuras decisões.

---

## 36. Feedback de resultado

O Orchestrator deve registrar, quando possível:

```text
seleção feita
resultado esperado
resultado obtido
qualidade
custo
tempo
retrabalho
intervenções
falhas
```

Esses dados alimentarão **Continuity & Learning** e poderão modificar a confiança atribuída a uma configuração.

---

## 37. Não converter automaticamente experiência em regra

O resultado:

```text
Model X funcionou bem uma vez
```

não deve automaticamente gerar:

```text
Model X é o melhor.
```

O resultado deve ser tratado como evidência histórica contextual.

Essa é uma aplicação direta do princípio de evolução governada e aprendizagem baseada em evidência do projeto legado e do novo `PROJECT-DEFINITION`.

---

## 38. Critério de adequação

Uma configuração é adequada quando:

```text
capacidade suficiente
+
restrições satisfeitas
+
risco aceitável
+
qualidade esperada
+
custo proporcional
+
contexto adequado
```

não sendo necessário provar que ela é globalmente ótima.

---

## 39. Saída conceitual

A saída da capacidade deve poder ser representada como:

```text
RESOURCE-SELECTION
├── work_unit
├── selected_agent
├── selected_skills
├── selected_model
├── provider
├── configuration
├── alternatives
├── rationale
├── constraints
├── expected_quality
├── expected_cost
├── expected_latency
├── confidence
├── fallback
└── evidence
```

Nem todos os campos estarão disponíveis em todas as execuções.

---

## 40. Interface com Delegation & Coordination

A saída desta capacidade se torna a entrada para a delegação:

```text
Resource / Model Selection
        ↓
configuration approved
        ↓
Delegation & Coordination
```

O delegador não deve reinterpretar silenciosamente a seleção.

Se houver necessidade de mudança, deve retornar ao ciclo decisório apropriado.

---

## 41. Alteração de seleção durante execução

Uma configuração pode precisar ser alterada durante a execução quando houver:

- indisponibilidade;
- mudança de contexto;
- descoberta de maior complexidade;
- falha;
- aumento de risco;
- custo inesperado.

Fluxo:

```text
configuração
   ↓
execução
   ↓
mudança de condição
   ↓
reavaliação
   ↓
nova seleção
```

A nova seleção deve ser registrada.

---

## 42. Política de reuso

Quando uma combinação apresentar histórico consistente e bom desempenho, o Orchestrator pode utilizá-la novamente com menor necessidade de análise, desde que:

- o contexto seja suficientemente semelhante;
- as condições relevantes não tenham mudado;
- a política permita;
- a evidência permaneça válida.

Reuso reduz custo de planejamento.

---

## 43. Catálogo de configurações

Futuramente, o sistema poderá registrar configurações recorrentes:

```text
Architecture Critical Review
→ Architecture Agent
→ Architecture Skill
→ Model X
→ Reviewer Model Y
```

Essas configurações podem funcionar como padrões candidatos.

Elas não devem se tornar regras imutáveis automaticamente.

---

## 44. Critérios de sucesso

A capacidade estará suficientemente desenvolvida quando o Orchestrator puder:

1. receber candidatos tecnicamente elegíveis;
2. considerar qualidade, custo, risco e contexto;
3. separar agente de modelo;
4. escolher modelos diferentes conforme tarefa;
5. escolher configurações diferentes para tarefas do mesmo agente;
6. considerar número de agentes;
7. considerar custo de coordenação e contexto;
8. utilizar histórico e evidências;
9. representar incerteza;
10. oferecer alternativas quando apropriado;
11. definir fallback;
12. justificar decisões;
13. preservar políticas do desenvolvedor;
14. registrar decisões para aprendizagem posterior;
15. permitir futura substituição de runtime/provider.

---

## 45. Relação com o conhecimento legado

O legado fornece diretamente:

- suficiência;
- proporcionalidade;
- impacto;
- risco;
- prioridade;
- dependências;
- paralelismo;
- evidência;
- confiança;
- reversibilidade;
- análise de mudanças;
- aprendizagem governada.

Esses conceitos podem ser reutilizados sem copiar a arquitetura antiga.

O conhecimento novo desta capacidade inclui principalmente:

- seleção agente/Skill/modelo;
- custo de coordenação;
- custo de contexto;
- catálogo de modelos;
- fallback;
- elegibilidade econômica;
- comparação multiobjetivo;
- seleção dinâmica;
- histórico de configuração de execução.

---

## 46. Limites

Resource / Model Selection não deve:

- executar tarefas;
- inventar capacidades;
- alterar políticas do desenvolvedor;
- ignorar restrições;
- avaliar resultados finais;
- replanejar o projeto inteiro;
- considerar custo como único objetivo;
- tratar ranking global como decisão contextual;
- transformar uma única experiência em regra universal.

---

## 47. Relação com o objetivo adaptativo

A capacidade permite que:

```text
mesma Work Unit
```

possa receber configurações diferentes em momentos diferentes, porque:

```text
contexto mudou
modelo mudou
preço mudou
disponibilidade mudou
histórico mudou
risco mudou
```

Portanto, a adaptação ocorre sem alterar necessariamente a identidade da Work Unit ou do agente.

---

## 48. Princípio operacional consolidado

> **O Orchestrator deve selecionar o menor conjunto de recursos capaz de atender aos requisitos da Work Unit com qualidade, risco e custo proporcionais ao contexto, respeitando as políticas do desenvolvedor e considerando evidências disponíveis.**

"Menor conjunto" não significa necessariamente menor número absoluto de recursos.

Significa:

> **não utilizar recursos adicionais sem benefício justificável.**

---

## 49. Fluxo completo

```text
Work Unit
    ↓
Agent & Skill Analysis
    ↓
candidatos elegíveis
    ↓
Resource / Model Selection
    ↓
avaliação multiobjetivo
    ↓
configuração selecionada
    ↓
fallback / alternativas
    ↓
Delegation & Coordination
    ↓
execução
    ↓
Result Evaluation
    ↓
feedback
    ↓
Continuity & Learning
```

---

## 50. Estado

**Status:** Definição inicial concluída.

### Artefatos relacionados

- `PROJECT-DEFINITION.md`
- `ORCHESTRATOR-CAPABILITIES.md`
- `ORCHESTRATOR-KNOWLEDGE-MAP.md`
- `ORCHESTRATOR-PROJECT-AWARENESS.md`
- `ORCHESTRATOR-PROJECT-MANAGEMENT.md`
- `ORCHESTRATOR-ECOSYSTEM-AWARENESS.md`
- `ORCHESTRATOR-AGENT-AND-SKILL-ANALYSIS.md`

### Próxima capacidade

**Delegation & Coordination**

Pergunta central:

> **"Como transformar uma configuração selecionada em uma execução real, fornecer o contexto correto ao agente, controlar o handoff, receber o resultado e manter a coordenação sem produzir contexto ou trabalho desnecessários?"**
