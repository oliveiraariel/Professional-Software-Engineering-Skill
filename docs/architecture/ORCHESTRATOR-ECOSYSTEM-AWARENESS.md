# ORCHESTRATOR-ECOSYSTEM-AWARENESS

**Projeto:** Adaptive AI Orchestrator  
**Capacidade:** Ecosystem Awareness  
**Versão:** v0.1 — definição inicial  
**Status:** Em desenvolvimento

---

## 1. Propósito

A capacidade **Ecosystem Awareness** permite ao Orchestrator compreender o ambiente de execução e os recursos cognitivos e operacionais disponíveis para realizar um projeto.

Seu objetivo não é executar diretamente cada recurso do ecossistema, mas permitir que o Orchestrator saiba:

- quais recursos existem;
- quais capacidades cada recurso oferece;
- quais limitações possui;
- quais combinações são possíveis;
- quais pré-condições existem;
- quais políticas governam seu uso;
- quais recursos são adequados a determinada unidade de trabalho.

A capacidade deve permitir que o Orchestrator raciocine sobre o ecossistema sem ficar acoplado conceitualmente a uma única plataforma.

---

## 2. Papel dentro do Orchestrator

Ecosystem Awareness responde principalmente:

> **"Quais recursos existem neste ambiente e o que eles são capazes de fazer?"**

Não responde sozinha:

> "Qual recurso devo utilizar agora?"

Essa decisão pertence principalmente a **Agent & Skill Analysis**, **Resource / Model Selection** e **Delegation & Coordination**, utilizando as informações fornecidas por Ecosystem Awareness.

### Relação com outras capacidades

```text
Project Awareness
        ↓
o que o projeto precisa?

Project Management
        ↓
o que precisa acontecer e quando?

Ecosystem Awareness
        ↓
quais recursos existem?

Agent & Skill Analysis
        ↓
quem é capaz de executar?

Resource / Model Selection
        ↓
qual recurso é adequado?

Delegation & Coordination
        ↓
como executar?

Result Evaluation
        ↓
o resultado foi adequado?
```

---

## 3. Escopo

A capacidade deve conhecer, conforme disponibilidade e relevância:

- agentes;
- Skills;
- modelos;
- providers;
- ferramentas;
- MCPs;
- plugins;
- hooks;
- workspaces;
- mecanismos de delegação;
- sessões;
- memória e contexto;
- limitações de execução;
- políticas de acesso;
- custos conhecidos;
- disponibilidade;
- versões;
- compatibilidades;
- capacidades observadas.

A profundidade deve ser proporcional à decisão que o Orchestrator precisa tomar.

---

## 4. Princípio de separação de recursos

O sistema deve distinguir claramente:

```text
Agent
Skill
Model
Tool
Provider
Runtime
Workspace
Plugin
MCP
Hook
```

Esses elementos podem se relacionar, mas não são equivalentes.

### Agent

Representa uma responsabilidade ou unidade de execução.

### Skill

Representa conhecimento, procedimento ou orientação especializada reutilizável.

### Model

Representa o recurso de inteligência utilizado pelo agente para raciocínio e geração.

### Tool

Representa uma capacidade de ação executável.

### Provider

Representa a origem ou infraestrutura que disponibiliza determinado recurso.

### Runtime / Harness

Representa a plataforma que fornece o ambiente operacional do agente.

### Workspace

Representa o espaço de trabalho e contexto persistente associado ao agente, quando a plataforma fornecer esse mecanismo.

### Plugin

Representa extensão de runtime que pode acrescentar capacidades operacionais.

### MCP

Representa uma forma padronizada de disponibilizar ferramentas ou contexto a agentes, quando suportada.

### Hook

Representa mecanismo de execução associado a eventos do runtime, quando suportado.

---

## 5. Modelo conceitual do ecossistema

```text
                    ECOSYSTEM
                        │
        ┌───────────────┼────────────────┐
        │               │                │
      Agents          Skills           Models
        │               │                │
        └───────────────┼────────────────┘
                        │
                Tools / MCP / Plugins
                        │
                     Runtime
                        │
              Workspace / Sessions
                        │
                  Execution Policy
```

A estrutura física pode variar entre plataformas. O modelo conceitual deve permanecer estável.

---

## 6. Conhecimento sobre agentes

Para cada agente disponível, o Orchestrator deve conseguir representar, quando possível:

```text
Agent
├── identidade
├── responsabilidade
├── especializações
├── Skills disponíveis
├── ferramentas disponíveis
├── modelos elegíveis
├── contexto acessível
├── autonomia
├── restrições
├── dependências
├── capacidade esperada
├── custo relativo
├── estado/disponibilidade
└── evidências de desempenho
```

### O Orchestrator não deve assumir que o nome do agente define sua capacidade.

A capacidade deve ser derivada de:

- configuração;
- Skills;
- instruções;
- ferramentas;
- modelo;
- contexto;
- evidência histórica;
- políticas do runtime.

---

## 7. Conhecimento sobre Skills

Para cada Skill, o Orchestrator deve poder conhecer:

```text
Skill
├── finalidade
├── domínio/capacidade
├── descrição
├── entradas necessárias
├── saídas esperadas
├── pré-condições
├── dependências
├── ferramentas utilizadas
├── agentes compatíveis
├── restrições
├── versão
└── evidências de desempenho
```

Uma Skill deve ser considerada uma **capacidade especializada**, e não uma entidade indistinguível do agente que a utiliza.

Quando houver mais de uma Skill capaz de atender à mesma necessidade, a seleção poderá depender de:

- qualidade esperada;
- custo;
- complexidade;
- redundância;
- contexto;
- compatibilidade;
- risco.

---

## 8. Conhecimento sobre modelos

O Orchestrator deve ser capaz de representar conhecimento sobre modelos, quando esse conhecimento estiver disponível:

```text
Model
├── nome
├── versão
├── provider
├── capacidades declaradas
├── capacidades observadas
├── contexto
├── latência
├── custo
├── disponibilidade
├── limitações
├── compatibilidades
├── histórico de desempenho
└── evidências
```

### Importante

Ecosystem Awareness **não deve considerar o modelo "melhor" em termos absolutos**.

Deve representar a adequação de um modelo ao contexto.

O `PROJECT-DEFINITION` já estabelece que a avaliação deve considerar capacidade, custo, latência, contexto, disponibilidade, evidências e histórico, sem tratar um modelo como universalmente superior.

---

## 9. Conhecimento sobre ferramentas

O Orchestrator deve saber:

- quais ferramentas existem;
- para quais finalidades servem;
- quais agentes podem utilizá-las;
- quais permissões exigem;
- quais limitações possuem;
- se exigem credenciais;
- se produzem efeitos externos;
- se são reversíveis;
- se são críticas ou sensíveis.

Uma ferramenta é uma capacidade operacional; não deve ser confundida com Skill.

---

## 10. Conhecimento sobre o Runtime / Harness

O Orchestrator precisa conhecer as características relevantes da plataforma em que está executando.

Exemplos de informações:

```text
Runtime
├── suporte a agentes
├── suporte a subagentes
├── suporte a Skills
├── seleção de modelos
├── workspace
├── ferramentas
├── MCP
├── hooks
├── memória
├── isolamento
├── permissões
├── políticas
└── limites
```

### Princípio

O Orchestrator deve ser **runtime-aware**, mas **runtime-agnostic em sua arquitetura conceitual**.

Isso permite que o mesmo conhecimento seja posteriormente adaptado a:

```text
OpenClaw
Hermes
ou outro runtime
```

sem reconstruir o modelo conceitual do Orchestrator.

---

## 11. OpenClaw como primeira plataforma-alvo

O projeto pode adotar OpenClaw como **primeiro runtime de referência**, sem transformar sua arquitetura conceitual em uma arquitetura dependente dele.

A documentação atual do OpenClaw confirma suporte a:

- runtime incorporado;
- workspace individual por agente;
- Skills por diferentes níveis de precedência;
- controle de Skills por agente;
- subagentes;
- seleção/substituição de modelos de subagentes;
- ferramentas, plugins e outras extensões.

Esses mecanismos são infraestrutura do runtime e devem ser consumidos pelo Orchestrator, não necessariamente reinventados por ele.

---

## 12. Hermes como runtime alternativo

Hermes também fornece mecanismos relevantes:

- Skills sob demanda;
- diretórios externos de Skills;
- criação e gerenciamento de Skills;
- subagentes;
- ferramentas;
- contexto e sessões;
- mecanismos de delegação.

O projeto deve preservar a separação entre:

```text
conhecimento próprio do Orchestrator
```

e

```text
forma específica como o runtime implementa esse conhecimento
```

---

## 13. Catálogo do ecossistema

Ecosystem Awareness deverá produzir ou consumir um **modelo/catalogo de recursos disponíveis**.

Conceitualmente:

```text
ECOSYSTEM CATALOG
│
├── Agents
├── Skills
├── Models
├── Tools
├── Providers
├── Runtimes
├── Plugins
├── MCPs
└── Policies
```

Esse catálogo não precisa ser necessariamente um único arquivo ou banco de dados.

Sua representação física será definida posteriormente.

O requisito conceitual é que o Orchestrator consiga consultar o catálogo de maneira estruturada.

---

## 14. Elegibilidade

Um recurso pode existir no catálogo sem ser elegível para determinada tarefa.

Exemplo:

```text
Agent A
   ↓
possui Skill X
   ↓
mas não possui ferramenta necessária
   ↓
NÃO ELEGÍVEL
```

Ou:

```text
Agent B
   ↓
possui Skill X
   ↓
possui ferramenta necessária
   ↓
modelo compatível
   ↓
ELEGÍVEL
```

Portanto:

```text
Existência ≠ Elegibilidade
```

Essa distinção será usada posteriormente por **Agent & Skill Analysis**.

---

## 15. Compatibilidade

O Orchestrator deve poder raciocinar sobre relações como:

```text
Agent ↔ Skill
Agent ↔ Model
Agent ↔ Tool
Skill ↔ Tool
Skill ↔ Agent
Model ↔ Provider
Tool ↔ Runtime
Skill ↔ Runtime
```

Exemplo:

```text
Architecture Agent
    ↓
Architecture Skill
    ↓
Model X
    ↓
Provider Y
    ↓
Runtime Z
```

Uma incompatibilidade em qualquer ponto pode invalidar uma configuração.

---

## 16. Políticas de acesso e governança

O Orchestrator não deve assumir que todo recurso disponível pode ser usado.

Deve distinguir:

```text
disponível
permitido
elegível
recomendável
```

Exemplo:

```text
Modelo X
↓
disponível = SIM
↓
permitido = NÃO
↓
não pode ser utilizado
```

Ou:

```text
Agent A
↓
disponível = SIM
↓
permitido = SIM
↓
elegível = NÃO
```

As políticas do desenvolvedor/runtimes têm precedência sobre a conveniência da execução.

---

## 17. Conhecimento dinâmico

Algumas informações do ecossistema mudam rapidamente:

- versões;
- preços;
- disponibilidade;
- APIs;
- capacidades;
- limitações;
- ferramentas;
- providers.

Esse conhecimento não deve ser incorporado como verdade permanente.

O `PROJECT-DEFINITION` já estabelece que informações sobre modelos, versões, preços, APIs, capacidades e disponibilidade são conhecimento dinâmico.

O Orchestrator deve portanto trabalhar com:

```text
valor
+
fonte
+
data/versão
+
confiança
```

quando apropriado.

---

## 18. Evidência sobre recursos

O Orchestrator deve distinguir pelo menos:

```text
capacidade declarada
capacidade observada
benchmark
teste controlado
experiência prática
histórico próprio
```

Isso reutiliza diretamente a metodologia de evidência do projeto legado e a seção de Model Intelligence do novo `PROJECT-DEFINITION`.

A frequência de uso de um recurso não deve ser tomada isoladamente como prova de qualidade.

---

## 19. Relação com seleção de modelos

Ecosystem Awareness fornece:

```text
quais modelos existem
quais estão disponíveis
quais são permitidos
quais são elegíveis
quais características possuem
```

Mas não deve tomar a decisão final de seleção.

A cadeia correta será:

```text
Ecosystem Awareness
        ↓
recursos disponíveis
        ↓
Agent & Skill Analysis
        ↓
recursos tecnicamente elegíveis
        ↓
Resource / Model Selection
        ↓
recurso recomendado
```

---

## 20. Relação com economicidade

O catálogo deve possibilitar conhecimento de:

- custo;
- volume;
- latência;
- custo de coordenação;
- contexto;
- quantidade de chamadas;
- disponibilidade.

Entretanto, Ecosystem Awareness **não otimiza o plano**.

Ela fornece os dados.

A otimização pertence a:

```text
Project Management
+
Resource / Model Selection
+
Delegation & Coordination
```

---

## 21. Descoberta versus conhecimento consolidado

O Orchestrator deve distinguir:

```text
recurso conhecido
recurso descoberto
recurso verificado
recurso permitido
recurso elegível
recurso validado
```

Não deve tratar uma descoberta superficial como verdade consolidada.

---

## 22. Atualização do catálogo

O catálogo deve permitir atualização sem alterar silenciosamente as regras centrais do Orchestrator.

Ciclo:

```text
descoberta
→ verificação
→ classificação
→ atualização
→ versionamento, quando necessário
```

Essa abordagem segue o princípio herdado de evolução governada: observação externa não se torna automaticamente um novo padrão.

---

## 23. Autoconsciência operacional

A capacidade deve permitir ao Orchestrator conhecer **seu próprio ecossistema operacional** em nível suficiente para responder:

> O que eu posso usar?

> O que eu não posso usar?

> O que está disponível agora?

> O que é adequado?

> O que depende de configuração?

> O que é caro?

> O que tem limitações?

> O que exige intervenção humana?

Essa é uma forma de **consciência operacional**, não uma afirmação de consciência no sentido filosófico.

---

## 24. Não confundir Ecosystem Awareness com autonomia

Conhecer recursos não significa possuir autoridade irrestrita para utilizá-los.

O Orchestrator deve permanecer sujeito a:

- políticas;
- permissões;
- limites;
- autoridade do desenvolvedor;
- segurança;
- disponibilidade;
- orçamento;
- restrições do runtime.

---

## 25. Relação com subagentes

Quando o runtime suporta subagentes, o Orchestrator deve conhecer:

- como iniciar;
- quais parâmetros podem ser definidos;
- quais modelos podem ser usados;
- qual contexto pode ser transmitido;
- como o resultado retorna;
- quais limitações existem;
- qual custo adicional existe.

No OpenClaw, por exemplo, subagentes executam em sessões próprias e têm contexto separado por padrão; a documentação recomenda modelos mais econômicos para trabalhos pesados/repetitivos quando apropriado. Isso é infraestrutura do runtime que o Orchestrator poderá explorar.

---

## 26. Recursos não precisam estar previamente definidos como agentes completos

O ecossistema pode conter recursos em diferentes níveis:

```text
Agent pronto
Skill disponível
Modelo disponível
Tool disponível
```

O Orchestrator não deve pressupor que toda capacidade precisa estar encapsulada previamente em um agente.

Entretanto, a possibilidade de composição deve respeitar as capacidades reais do runtime.

---

## 27. Estrutura de representação conceitual

Uma representação lógica mínima de um recurso seria:

```text
RESOURCE
├── id
├── type
├── name
├── version
├── capabilities
├── dependencies
├── permissions
├── eligibility
├── constraints
├── cost
├── availability
├── evidence
└── status
```

Esse é um **modelo conceitual**, não ainda um schema de implementação.

---

## 28. Estado do recurso

Um recurso pode, conforme aplicável, ser:

```text
UNKNOWN
DISCOVERED
REGISTERED
AVAILABLE
UNAVAILABLE
RESTRICTED
ELIGIBLE
INELIGIBLE
DEPRECATED
VALIDATED
```

A implementação final poderá usar estados diferentes, desde que preserve a semântica necessária.

---

## 29. Relação com conhecimento do projeto

O Orchestrator deverá combinar:

```text
PROJECT KNOWLEDGE
        +
ECOSYSTEM KNOWLEDGE
        ↓
DECISION
```

Exemplo:

```text
Projeto exige:
"revisão arquitetural crítica"

        ↓

Ecosystem Awareness:
Opus disponível
Sonnet disponível
Architecture Agent disponível

        ↓

outras capacidades
avaliam adequação

        ↓

decisão
```

Ecosystem Awareness sozinho não escolhe.

---

## 30. Relação com agentes especialistas

Um agente especializado pode possuir:

```text
Role
+
Skill
+
Tools
+
Model
```

Mas esses elementos podem ser conhecidos separadamente pelo catálogo.

Isso permite que o Orchestrator perceba:

```text
"Tenho um Architecture Agent"

ou

"Não tenho Architecture Agent,
mas possuo uma Architecture Skill
e um agente que pode utilizá-la."
```

Essa distinção poderá ser importante no futuro para permitir composição dinâmica.

---

## 31. Relação com Skills externas

O Orchestrator poderá encontrar Skills:

- locais;
- do workspace;
- compartilhadas;
- instaladas;
- fornecidas pelo runtime;
- desenvolvidas internamente;
- provenientes de terceiros.

Mas a existência de uma Skill externa não garante sua confiabilidade.

Ela deve passar pelas políticas de confiança e elegibilidade apropriadas.

---

## 32. Relação com conhecimento legado

O projeto anterior fornece conceitos diretamente reutilizáveis:

- separação conceitual;
- evidência;
- estados;
- incerteza;
- dependências;
- impacto;
- rastreabilidade;
- mudanças;
- validação.

Entretanto, o catálogo do ecossistema é **conhecimento novo**.

O legado fornece a metodologia para raciocinar sobre recursos, mas não fornece por si só o inventário específico de OpenClaw/Hermes ou de modelos atuais.

---

## 33. Limites desta capacidade

Ecosystem Awareness não deve:

- executar tarefas de projeto;
- escolher sozinho a ordem de execução;
- substituir Project Management;
- definir sozinho o melhor agente;
- definir sozinho o melhor modelo;
- avaliar profundamente o resultado de um subagente;
- modificar políticas do desenvolvedor;
- assumir que um recurso é seguro apenas por estar disponível.

Sua função é **conhecer, representar, verificar e disponibilizar informações sobre o ecossistema**.

---

## 34. Entradas

Pode receber:

```text
runtime configuration
agent registry
skill registry
model registry
tool registry
provider information
permissions
policies
historical data
external metadata
execution results
```

---

## 35. Saídas

Pode produzir:

```text
ecosystem state
resource catalog
capability profile
eligibility information
compatibility information
availability information
restriction information
resource evidence
```

Essas saídas alimentam as capacidades seguintes.

---

## 36. Critérios de sucesso

Ecosystem Awareness será considerada suficientemente implementada quando o Orchestrator puder:

1. identificar os recursos relevantes disponíveis;
2. distinguir agentes, Skills, modelos, ferramentas e runtime;
3. conhecer capacidades e limitações relevantes;
4. distinguir disponibilidade, permissão e elegibilidade;
5. identificar compatibilidades e incompatibilidades;
6. representar conhecimento dinâmico;
7. considerar evidências e confiança;
8. fornecer informações suficientes para seleção e delegação;
9. operar sem depender conceitualmente de um único runtime;
10. utilizar corretamente as interfaces reais do runtime escolhido.

---

## 37. Relação com a primeira implementação

O primeiro runtime-alvo será tratado como **implementação de referência**, não como definição do conceito.

A primeira implementação poderá explorar diretamente as capacidades disponíveis na plataforma escolhida, enquanto o modelo conceitual permanecerá independente.

```text
ECOSYSTEM AWARENESS
        │
        ▼
ABSTRAÇÃO CONCEITUAL
        │
   ┌────┴────┐
   ▼         ▼
OpenClaw   Hermes
```

---

## 38. Conclusão

Ecosystem Awareness é a capacidade que dá ao Orchestrator **conhecimento operacional sobre o espaço de recursos onde ele pode agir**.

Ela permite que o Orchestrator deixe de ser um agente que simplesmente "sabe delegar" e passe a ser um agente que conhece:

```text
o projeto
+
o trabalho
+
o ecossistema
```

A combinação dessas informações será usada posteriormente para:

```text
analisar
→ selecionar
→ delegar
→ coordenar
→ avaliar
→ replanejar
```

---

## 39. Estado

**Status:** Definição inicial concluída.

### Dependências

- `ORCHESTRATOR-PROJECT-AWARENESS.md`
- `ORCHESTRATOR-PROJECT-MANAGEMENT.md`
- `ORCHESTRATOR-CAPABILITIES.md`
- `ORCHESTRATOR-KNOWLEDGE-MAP.md`
- `PROJECT-DEFINITION.md`

### Próxima capacidade

**Agent & Skill Analysis**

Essa capacidade utilizará as informações produzidas aqui para responder:

> **"Dado o trabalho que precisa ser realizado e o ecossistema disponível, quais agentes e Skills são tecnicamente adequados?"**
