# ORCHESTRATOR-RESULT-EVALUATION

**Projeto:** Adaptive AI Orchestrator  
**Capacidade:** Result Evaluation  
**Versão:** v0.1 — definição inicial  
**Status:** Em desenvolvimento

---

## 1. Propósito

A capacidade **Result Evaluation** permite ao Orchestrator avaliar criticamente os resultados produzidos por agentes, Skills, modelos e processos de execução antes de incorporá-los ao estado confiável do projeto.

Sua finalidade é responder:

> **O resultado recebido é suficientemente correto, completo, consistente, rastreável e adequado para o objetivo para o qual foi produzido?**

A avaliação deve determinar não apenas se um agente respondeu, mas se:

- o resultado atende à Work Unit;
- o resultado respeita as restrições;
- as decisões estão fundamentadas;
- as dependências foram preservadas;
- os artefatos são utilizáveis;
- as premissas estão explícitas;
- as incertezas foram tratadas;
- o resultado introduz riscos;
- o resultado exige revisão;
- o resultado pode ser integrado ao projeto.

---

## 2. Papel dentro do Orchestrator

Result Evaluation é a principal barreira entre:

```text
resultado produzido
```

e:

```text
conhecimento/estado confiável do projeto
```

Fluxo:

```text
Execution
    ↓
Result Package
    ↓
Result Evaluation
    ↓
┌───────────────┬───────────────┬───────────────┐
↓               ↓               ↓
ACCEPT          RETURN          BLOCK
↓               ↓               ↓
integrate       review          investigate
```

Ela não substitui o agente especialista responsável pela produção.

Ela também não deve assumir automaticamente a autoridade de uma decisão de negócio ou política.

---

## 3. Princípio fundamental

> **Receber um resultado não significa aceitá-lo.**

E:

> **Produzir corretamente um formato não significa produzir corretamente o conteúdo.**

A avaliação deve ocorrer em relação ao objetivo, contexto, restrições e critérios definidos para a Work Unit.

---

## 4. Resultado como objeto avaliado

O resultado deve ser avaliado como um conjunto:

```text
RESULT
├── conteúdo
├── artefatos
├── decisões
├── premissas
├── evidências
├── dependências descobertas
├── problemas
├── incertezas
└── metadados de execução
```

Cada parte pode possuir qualidade diferente.

Um resultado pode ser:

```text
conteúdo válido
+
uma premissa não confirmada
```

Nesse caso, talvez não seja simplesmente "aceito" ou "rejeitado"; poderá ser:

```text
ACCEPTED_WITH_CONDITIONS
```

---

## 5. Objetivos da avaliação

A avaliação deve determinar:

1. correção;
2. completude;
3. coerência;
4. aderência ao objetivo;
5. aderência às restrições;
6. suficiência;
7. rastreabilidade;
8. evidência;
9. consistência com decisões existentes;
10. compatibilidade com dependências;
11. impacto;
12. risco;
13. necessidade de revisão;
14. possibilidade de integração;
15. necessidade de replanejamento.

---

## 6. Critério de proporcionalidade

Nem todo resultado precisa receber o mesmo nível de avaliação.

A profundidade deve variar conforme:

```text
impacto
+
criticidade
+
incerteza
+
dependências
+
sensibilidade
+
reversibilidade
```

Um ajuste documental pequeno pode exigir avaliação local.

Uma decisão arquitetural crítica pode exigir avaliação contextual ou global.

Isso reutiliza diretamente o princípio de **diagnóstico adaptativo** do projeto legado.

---

## 7. Níveis de avaliação

### 7.1 Avaliação local

Usada quando:

- mudança pequena;
- escopo isolado;
- baixo impacto;
- poucas dependências.

### 7.2 Avaliação contextual

Usada quando:

- existe impacto semântico;
- há dependências próximas;
- há necessidade de verificar elementos relacionados.

### 7.3 Avaliação global

Usada quando:

- mudança estrutural;
- risco alto;
- contradições generalizadas;
- impacto difícil de determinar;
- decisão crítica;
- auditoria necessária.

O legado já define uma estrutura equivalente de avaliação local, contextual e global.

---

## 8. Critérios de correção

A correção responde:

> **"O resultado está correto em relação ao que se pretendia produzir?"**

Deve considerar:

- requisitos;
- regras;
- lógica;
- domínio;
- dados;
- arquitetura;
- implementação;
- testes;
- critérios da Work Unit.

Quando aplicável:

```text
Regra
→ Requisito
→ Caso de Uso
→ Domínio
→ Implementação
→ Teste
```

deve permanecer coerente.

---

## 9. Critérios de completude

Completude responde:

> **"O agente produziu tudo que era necessário para concluir sua responsabilidade?"**

Não significa produzir tudo o que poderia ser produzido.

Significa atender ao escopo definido.

Exemplo:

```text
Work Unit exige:
- arquitetura
- responsabilidades
- dependências
```

Resultado contém:

```text
arquitetura
```

mas não contém:

```text
dependências
```

→ incompleto.

---

## 10. Critério de suficiência

A avaliação deve utilizar o princípio:

> **suficiente para o contexto, e não máximo em quantidade.**

Um resultado pode ser aprovado sem ser exaustivo.

Isso evita:

```text
"faltou documentar tudo"
```

quando o que faltou não era necessário para a Work Unit.

---

## 11. Aderência ao objetivo

Pergunta:

> **"O resultado resolve o problema para o qual foi solicitado?"**

Um agente pode produzir um resultado tecnicamente correto, mas inadequado.

Exemplo:

```text
solicitado:
arquitetura simples para projeto pequeno

resultado:
arquitetura excessivamente complexa
```

Pode ser tecnicamente válida, mas inadequada ao objetivo e ao princípio de proporcionalidade.

---

## 12. Aderência ao escopo

A avaliação deve detectar:

```text
faltou trabalho
```

e também:

```text
trabalho excedente relevante
```

Escopo excedente pode:

- gerar custo;
- introduzir decisões não solicitadas;
- criar dependências;
- aumentar risco;
- dificultar integração.

Excesso também pode ser defeito quando altera o projeto sem justificativa.

---

## 13. Aderência às restrições

A avaliação deve verificar se o resultado respeita:

- requisitos;
- políticas;
- restrições técnicas;
- segurança;
- privacidade;
- orçamento;
- arquitetura aprovada;
- decisões do responsável;
- limites de autonomia.

Uma solução tecnicamente boa pode ser inválida se viola uma restrição.

---

## 14. Consistência interna

O resultado deve ser internamente consistente.

Exemplo:

```text
Componente A depende de B
```

e em outra parte:

```text
B depende de A
```

Se essa relação criar contradição ou ciclo não permitido, o resultado precisa ser revisto.

---

## 15. Consistência com o projeto

Também é necessário verificar o resultado contra o estado global.

O agente pode ter produzido algo internamente coerente, mas incompatível com:

- decisões anteriores;
- requisitos;
- domínio;
- arquitetura;
- dados;
- interfaces;
- testes;
- outras Work Units.

O legado estabelece explicitamente que o agente deve preservar coerência global e analisar elementos conectados quando uma alteração possuir dependências relevantes.

---

## 16. Consistência temporal

O Orchestrator deve considerar o momento do resultado.

Uma decisão que era válida antes pode se tornar inválida depois de uma mudança.

Portanto:

```text
resultado
+
versão do projeto
+
baseline
+
decisões posteriores
```

devem ser considerados.

---

## 17. Dependências

O resultado deve ser analisado quanto a:

- dependências satisfeitas;
- novas dependências descobertas;
- dependências alteradas;
- dependências quebradas.

Se o resultado depender de algo ainda não validado:

```text
resultado ≠ totalmente consolidado
```

---

## 18. Novas descobertas

Um resultado pode trazer conhecimento novo.

Exemplo:

```text
Agent A
→ descobre nova restrição
```

O Orchestrator deve verificar:

```text
essa descoberta é:
fato?
inferência?
hipótese?
decisão?
```

antes de propagá-la.

Isso reutiliza diretamente o modelo epistemológico do legado.

---

## 19. Evidência

Quando uma afirmação relevante estiver sustentada por evidência, a avaliação deve verificar:

```text
fonte
+
evidência
+
estado
+
confiança
+
impacto
```

Quando não existir evidência suficiente:

```text
não converter ausência em fato
```

---

## 20. Premissas

Toda premissa relevante deve ser identificável.

Exemplo:

```text
Assumption:
"o módulo de autenticação será externo."
```

A avaliação deve perguntar:

```text
confirmada?
inferida?
necessita decisão?
```

Uma premissa crítica não confirmada pode impedir a aprovação.

---

## 21. Incerteza

O resultado pode possuir:

```text
certeza alta
certeza média
certeza baixa
desconhecido
contraditório
```

A incerteza não precisa necessariamente bloquear o resultado.

O impacto da incerteza é que determina o tratamento.

---

## 22. Contradições

Quando um resultado contradizer conhecimento existente, a avaliação deve:

1. identificar a contradição;
2. localizar os elementos envolvidos;
3. verificar versões;
4. verificar evidências;
5. determinar se a contradição é real;
6. determinar seu impacto;
7. decidir se precisa de resolução.

Não deve escolher arbitrariamente uma das versões.

---

## 23. Rastreabilidade

O resultado deve poder ser relacionado, quando aplicável, a:

```text
Work Unit
→ requisito
→ decisão
→ artefato
→ resultado
→ validação
```

Isso permite auditoria e evolução.

---

## 24. Qualidade dos artefatos

Quando o resultado produzir arquivos ou outros artefatos, avaliar:

- presença;
- integridade;
- estrutura;
- consistência;
- formato;
- nomenclatura;
- referências;
- alinhamento com o projeto;
- legibilidade;
- utilidade.

No caso de código, a avaliação também deve considerar:

```text
correção
organização
responsabilidade
coesão
acoplamento
manutenibilidade
testabilidade
```

---

## 25. Avaliação de código

Para código produzido por agentes, Result Evaluation deve verificar, conforme contexto:

```text
compila/executa?
funciona?
atende aos requisitos?
respeita arquitetura?
há duplicação relevante?
há responsabilidades mal distribuídas?
há tratamento inadequado de erro?
há problemas de segurança?
há testes suficientes?
```

A avaliação não deve ser reduzida a "funcionou uma vez".

---

## 26. Avaliação documental

Para documentação:

```text
estrutura
consistência
completude
rastreabilidade
terminologia
coerência com decisões
adequação ao público
```

A documentação é tratada como representação formal do projeto no conhecimento legado; alterações relevantes devem ser analisadas como mudanças no próprio projeto.

---

## 27. Avaliação de decisões

Quando um agente retornar uma decisão, avaliar:

```text
questão
contexto
evidências
alternativas
impacto
riscos
recomendação
responsável
resultado
```

O formato de decisão já consolidado no legado pode ser reutilizado.

---

## 28. Avaliação de implementação versus avaliação de raciocínio

Quando possível, separar:

```text
resultado final
```

de:

```text
qualidade do processo utilizado para chegar ao resultado
```

Um resultado pode estar correto por acaso.

Outro pode apresentar raciocínio fundamentado e ainda possuir um erro final.

Ambos fornecem evidências diferentes.

O sistema não precisa avaliar ou armazenar cadeia privada de raciocínio do modelo; deve avaliar **artefatos observáveis, justificativas, decisões, evidências e resultados**.

---

## 29. Avaliação por critérios de aceitação

Toda Work Unit relevante deve possuir critérios verificáveis.

Exemplo:

```text
Critério:
"Todos os componentes principais possuem responsabilidade definida."

Avaliação:
PASS / FAIL / UNKNOWN
```

Isso é preferível a uma avaliação puramente subjetiva.

---

## 30. Estados de avaliação

Um resultado pode receber estados como:

```text
NOT_EVALUATED
UNDER_REVIEW
ACCEPTED
ACCEPTED_WITH_CONDITIONS
RETURNED_FOR_REVISION
BLOCKED
REJECTED
SUPERSEDED
REOPENED
```

A terminologia pode ser refinada na arquitetura do estado global.

---

## 31. Accepted

Um resultado pode ser aceito quando:

```text
critérios atendidos
+
restrições respeitadas
+
riscos aceitáveis
+
dependências consistentes
+
nível de confiança suficiente
```

---

## 32. Accepted with conditions

Utilizado quando:

```text
resultado suficiente
+
pendência não bloqueadora
```

Exemplo:

```text
Arquitetura aceita
+
documentação de implantação pendente
```

A condição deve possuir registro e responsável/contexto quando necessário.

---

## 33. Returned for revision

Usado quando o resultado é potencialmente aproveitável, mas precisa de correção.

Fluxo:

```text
Result
 ↓
Evaluation
 ↓
Revision Request
 ↓
Agent
 ↓
New Result
 ↓
Evaluation
```

O feedback deve ser específico.

---

## 34. Rejection

Rejeição deve ser utilizada quando o resultado não é aproveitável na forma atual.

Exemplos:

- incompatibilidade estrutural;
- violação grave de requisito;
- risco inaceitável;
- premissa inválida;
- arquitetura incompatível.

A rejeição deve possuir justificativa.

---

## 35. Blocked

Um resultado pode estar bloqueado sem estar errado.

Exemplo:

```text
resultado depende de decisão humana
```

ou:

```text
informação essencial ausente
```

Nesse caso:

```text
BLOCKED
```

é diferente de:

```text
REJECTED
```

---

## 36. Reabertura

Um resultado anteriormente aceito pode ser reaberto quando uma mudança posterior afetá-lo.

O legado já estabelece:

```text
unidade validada
→ estável para dependências
→ alteração posterior
→ reabertura
→ análise de impacto
→ revalidação do conjunto afetado
```

Essa regra deve ser preservada.

---

## 37. Avaliação de impacto

Quando um resultado modifica o projeto, avaliar:

```text
abrangência
dependências
incerteza
reversibilidade
risco
sensibilidade
```

O nível de revisão deve ser proporcional ao impacto.

---

## 38. Avaliação de retrabalho

O resultado deve ser analisado também quanto a:

> **"Quais partes futuras terão de ser refeitas caso este resultado permaneça?"**

Um resultado aparentemente correto pode criar:

```text
retrabalho elevado
```

por causa de uma decisão inadequada.

---

## 39. Avaliação de custo-benefício

Em determinados casos, o Orchestrator pode descobrir:

```text
resultado correto
mas
custo excessivo
```

Isso não significa automaticamente rejeição.

Deve verificar se:

```text
qualidade / risco / tempo
```

justificam o custo.

Essa avaliação retorna informações para Resource / Model Selection e Project Management.

---

## 40. Avaliação de consistência entre agentes

Quando múltiplos agentes produzem resultados relacionados, comparar:

```text
convergência
divergência
contradição
complementaridade
```

Exemplo:

```text
Architecture Agent
+
Security Agent
```

A análise deve determinar se:

```text
resultados se reforçam
```

ou:

```text
resultados entram em conflito
```

---

## 41. Revisão independente

Em resultados críticos, a avaliação pode ser feita por:

```text
Orchestrator
```

e, quando justificar custo:

```text
Review Agent
```

ou:

```text
Review Model
```

O revisor não precisa ser o mesmo agente que produziu o resultado.

---

## 42. Critério para revisão adicional

A revisão adicional pode ser motivada por:

- criticidade alta;
- confiança baixa;
- impacto alto;
- novidade;
- divergência;
- histórico de falhas;
- falta de evidência;
- mudança estrutural.

---

## 43. Resultado de avaliação

A avaliação deve produzir algo estruturado:

```text
EVALUATION RESULT
├── work_unit
├── result_id
├── verdict
├── criteria
├── failures
├── warnings
├── strengths
├── evidence
├── confidence
├── impact
├── risks
├── dependencies
├── revision_required
├── integration_allowed
└── recommended_next_action
```

---

## 44. Justificativa da avaliação

Uma decisão de aceitação ou rejeição deve poder responder:

```text
Por quê?
Com base em quê?
Qual critério foi usado?
Qual evidência sustenta?
Qual impacto foi considerado?
```

Isso protege a auditabilidade do Orchestrator.

---

## 45. Avaliação automática versus humana

O Orchestrator pode avaliar autonomamente quando:

```text
regras claras
+
evidência suficiente
+
baixo/médio impacto
+
autoridade disponível
```

A intervenção humana pode ser necessária quando:

- decisão de negócio;
- alto impacto;
- segurança;
- dados sensíveis;
- impacto desconhecido;
- política do Orchestrator;
- alteração de núcleo protegido.

Essa lógica reutiliza diretamente a governança da Skill legada.

---

## 46. Avaliação de resultados de baixa incerteza

Quando:

```text
critério objetivo
+
resultado facilmente verificável
```

a avaliação pode ser automatizada.

Exemplos:

```text
arquivo existe?
teste passou?
requisito foi coberto?
referência está válida?
```

---

## 47. Avaliação de resultados de alta incerteza

Quando:

```text
resultado subjetivo
ou
evidência fraca
ou
impacto alto
```

a avaliação deve aumentar em profundidade.

Pode envolver:

```text
mais contexto
+
mais evidência
+
agente revisor
+
modelo alternativo
+
decisão humana
```

---

## 48. Falha de avaliação

A avaliação também pode falhar.

Exemplo:

```text
não há informação suficiente para determinar se o resultado está correto
```

Nesse caso:

```text
EVALUATION_UNKNOWN
```

é preferível a:

```text
ACCEPT
```

ou:

```text
REJECT
```

sem fundamento.

---

## 49. Aprendizagem a partir da avaliação

Cada avaliação gera evidência sobre:

```text
Agent
Skill
Model
Delegation
Context
Task Type
```

Isso pode alimentar o histórico:

```text
configuração
→ execução
→ avaliação
→ qualidade
```

e melhorar futuras seleções.

---

## 50. Não transformar avaliação em regra automaticamente

Um agente ser reprovado uma vez não significa:

```text
agente ruim
```

Pode significar:

- contexto inadequado;
- Skill inadequada;
- modelo inadequado;
- tarefa incomum;
- falha transitória.

A experiência deve ser contextualizada.

---

## 51. Indicadores de qualidade

Quando viável, registrar:

```text
quality score
criteria pass rate
rework
review count
human intervention
defect count
time
cost
```

Esses indicadores não precisam ser usados como uma única nota universal.

---

## 52. Qualidade qualitativa

Números não substituem observações relevantes.

Também registrar:

```text
strengths
limitations
unexpected findings
failure mode
contextual observations
```

---

## 53. Relação com Resource / Model Selection

A avaliação deve fornecer feedback:

```text
selected configuration
        ↓
actual performance
        ↓
evaluation
        ↓
historical evidence
        ↓
future selection
```

Isso fecha o ciclo adaptativo.

---

## 54. Relação com Delegation & Coordination

A delegação informa:

```text
o que foi enviado
```

A avaliação informa:

```text
o que deveria ter acontecido
vs.
o que aconteceu
```

Essa comparação permite identificar:

```text
delegation error
```

quando o problema ocorreu no próprio Task Package/handoff.

---

## 55. Relação com Project Management

Quando o resultado for aceito:

```text
Work Unit
→ COMPLETED
```

Quando houver revisão:

```text
Work Unit
→ IN REVIEW / REOPENED
```

Quando houver bloqueio:

```text
Work Unit
→ BLOCKED
```

Quando houver impacto:

```text
Project Management
→ replanejamento
```

---

## 56. Relação com Continuity & Learning

O resultado final da avaliação deve alimentar:

```text
project state
historical record
performance evidence
future recommendation
```

Não necessariamente todo detalhe deve ser preservado para sempre.

O nível de retenção será definido pela arquitetura de conhecimento e pelas políticas de continuidade.

---

## 57. Exemplo completo

```text
Work Unit:
"Definir arquitetura do sistema."

        ↓

Architecture Agent
        ↓
Result Package
        ↓
Result Evaluation

Critérios:
✓ responsabilidades definidas
✓ dependências definidas
✓ requisitos arquiteturais atendidos
✗ integração X sem decisão
```

Veredicto:

```text
ACCEPTED_WITH_CONDITIONS
```

Condição:

```text
definir integração X
```

O projeto não precisa necessariamente voltar ao início.

O Orchestrator pode:

```text
criar nova Work Unit
ou
devolver ao Architecture Agent
```

conforme impacto e dependência.

---

## 58. Exemplo de rejeição

```text
Result:
arquitetura proposta

Evaluation:
✗ contradiz requisito
✗ cria acoplamento proibido
✗ dependência crítica não considerada
```

Veredicto:

```text
RETURNED_FOR_REVISION
```

O Orchestrator devolve ao agente:

```text
problemas
+
evidências
+
critérios
+
expectativa de correção
```

---

## 59. Exemplo de bloqueio

```text
Result:
modelo de dados

Evaluation:
estrutura plausível
mas
regra de negócio essencial não confirmada
```

Veredicto:

```text
BLOCKED
```

Não é rejeitado porque não está necessariamente errado.

Ele não pode ser consolidado porque falta informação fundamental.

---

## 60. Exemplo de revisão independente

```text
Architecture Agent
        ↓
produção

Security Reviewer
        ↓
revisão

Orchestrator
        ↓
comparação
        ↓
avaliação final
```

Isso pode ser usado em áreas críticas.

---

## 61. Critérios de sucesso

Result Evaluation estará suficientemente desenvolvida quando o Orchestrator puder:

1. avaliar resultados contra a Work Unit;
2. avaliar completude sem exigir excesso;
3. verificar coerência interna e global;
4. analisar restrições;
5. verificar evidências;
6. distinguir fato, inferência, premissa e decisão;
7. avaliar dependências;
8. detectar contradições;
9. classificar impacto;
10. decidir entre aceitar, aceitar com condições, revisar, bloquear ou rejeitar;
11. reabrir resultados quando necessário;
12. justificar decisões;
13. utilizar revisão independente quando justificável;
14. produzir feedback acionável;
15. alimentar histórico e aprendizagem;
16. evitar transformar evidência limitada em regra universal.

---

## 62. Limites

Result Evaluation não deve:

- alterar automaticamente requisitos de negócio;
- inventar evidências;
- aprovar por ausência de erro evidente;
- reprovar sem critério;
- substituir decisão humana quando fora da autoridade;
- transformar opinião em fato;
- tratar benchmark isolado como verdade;
- considerar volume de produção como prova de qualidade;
- apagar resultados rejeitados sem histórico;
- mascarar incerteza.

---

## 63. Princípio operacional consolidado

> **Nenhum resultado deve ser incorporado como estado confiável do projeto sem avaliação proporcional ao seu impacto, criticidade, incerteza e dependências, sendo aceitação, revisão, bloqueio ou rejeição decisões justificadas por critérios e evidências observáveis.**

---

## 64. Fluxo completo

```text
RESULT PACKAGE
      ↓
CLASSIFY
      ↓
DETERMINE EVALUATION DEPTH
      ↓
CHECK OBJECTIVE
      ↓
CHECK SCOPE
      ↓
CHECK CORRECTNESS
      ↓
CHECK COMPLETENESS
      ↓
CHECK CONSISTENCY
      ↓
CHECK CONSTRAINTS
      ↓
CHECK DEPENDENCIES
      ↓
CHECK EVIDENCE
      ↓
CHECK IMPACT / RISK
      ↓
VERDICT
      │
      ├── ACCEPT
      │
      ├── ACCEPTED_WITH_CONDITIONS
      │
      ├── RETURNED_FOR_REVISION
      │
      ├── BLOCKED
      │
      └── REJECTED
      ↓
PROJECT STATE / REPLANNING / LEARNING
```

---

## 65. Conhecimento legado reutilizado

Esta capacidade reutiliza de forma ampla:

- evidência antes de conclusão;
- separação entre fato e inferência;
- estados epistemológicos;
- incerteza;
- modelo de decisão;
- maturidade;
- suficiência;
- diagnóstico adaptativo;
- classificação de impacto;
- prioridade;
- coerência global;
- validação antes de avanço;
- análise de impacto;
- estados de execução;
- baseline;
- reabertura;
- evolução governada.

O aproveitamento é direto porque esses mecanismos já foram concebidos para distinguir produção, validação, correção e estabilidade do projeto.

---

## 66. Conhecimento novo

O novo conhecimento específico inclui:

- avaliação de resultados de subagentes;
- critérios de aceitação entre agentes;
- avaliação de Task/Result Packages;
- diagnóstico de falhas de delegação;
- avaliação de qualidade da configuração Agent + Skill + Model;
- revisão independente entre agentes;
- avaliação de eficiência real da execução;
- integração da avaliação com seleção futura;
- armazenamento de evidência de desempenho.

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

### Próxima capacidade

**Replanning**

Pergunta central:

> **"Diante do novo estado, dos resultados recebidos, das descobertas, falhas, mudanças e avaliações, qual deve ser o próximo plano de trabalho?"**
