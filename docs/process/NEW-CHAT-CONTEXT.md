# Contexto de Continuidade — Professional Software Engineering Skill

## 1. Finalidade

Este documento orienta a retomada do desenvolvimento conceitual e, posteriormente, da implementação da:

**Professional Software Engineering Skill**

A finalidade é permitir a continuidade do trabalho entre diferentes chats, sessões ou contextos sem depender do histórico completo de uma conversa anterior.

Este documento não substitui os demais documentos do projeto.

---

# 2. Fontes de verdade do projeto

Ao iniciar uma nova sessão de trabalho, os documentos devem ser considerados na seguinte ordem de autoridade:

## 2.1 MASTER-SPECIFICATION.md

Local:

```text
specifications/MASTER-SPECIFICATION.md
```

É a fonte normativa principal da Skill.

Contém as decisões conceituais já consolidadas.

Quando houver conflito entre uma hipótese levantada durante uma nova sessão e uma decisão registrada no MASTER-SPECIFICATION.md, a decisão já consolidada deve ser preservada, salvo se houver uma discussão explícita para sua revisão.

## 2.2 DEVELOPMENT-CONTINUITY.md

Local:

docs/DEVELOPMENT-CONTINUITY.md

É o registro operacional de continuidade.

Contém:

estado atual do desenvolvimento;
decisões já discutidas;
decisões ainda pendentes;
contexto necessário para retomada;
ponto exato onde o trabalho foi interrompido;
próximos trabalhos previstos.

## 2.3 GIT-WORKFLOW.md

Local:

docs/GIT-WORKFLOW.md

Contém o procedimento operacional de versionamento do projeto com Git e GitHub.

Ele não define a metodologia da Skill.

# 3. Regra de leitura inicial

Ao iniciar uma nova sessão de desenvolvimento, o agente deve:

identificar os três documentos;
ler o MASTER-SPECIFICATION.md;
ler o DEVELOPMENT-CONTINUITY.md;
ler o GIT-WORKFLOW.md quando a atividade envolver versionamento;
identificar a etapa atual;
identificar o último ponto consolidado;
identificar as questões ainda abertas;
somente então continuar o trabalho.

O agente não deve iniciar uma nova proposta metodológica antes de compreender o estado registrado.

# 4. Regra de preservação das decisões

Decisões já consolidadas não devem ser reabertas apenas porque uma alternativa diferente foi imaginada posteriormente.

Uma decisão consolidada só deve ser reconsiderada quando existir:

nova evidência relevante;
contradição identificada;
impacto anteriormente desconhecido;
mudança significativa de contexto;
necessidade explícita de revisão;
evolução metodológica devidamente fundamentada.

Quando uma decisão consolidada for reconsiderada, o agente deve:

identificar decisão atual
        ↓
explicar motivo da revisão
        ↓
avaliar impactos
        ↓
apresentar alternativas
        ↓
propor nova decisão
        ↓
obter aprovação quando necessário
        ↓
atualizar os registros
        ↓
versionar a alteração
# 5. Regra de distinção entre estados do conhecimento

O agente deve preservar a diferença entre:

FATO
INFERÊNCIA
HIPÓTESE
PROPOSTA
DECISÃO
QUESTÃO PENDENTE
VALIDAÇÃO

Não transformar:

hipótese em fato;
inferência em decisão;
proposta em decisão aprovada;
ausência de informação em requisito;
padrão encontrado em projeto em regra universal da Skill.

# 6. Regra para perguntas

O agente deve fazer perguntas quando uma indefinição realmente impedir uma decisão segura ou ultrapassar sua autoridade.

Não deve perguntar desnecessariamente quando:

a decisão estiver claramente determinada por evidências;
a decisão for operacional;
o impacto for baixo;
a decisão estiver dentro da autoridade concedida;
houver regra metodológica consolidada que determine o procedimento.

Quando precisar perguntar, deve apresentar o contexto necessário para permitir uma decisão consciente.

Sempre que adequado, apresentar:

Questão
Contexto
Evidências
Alternativas
Impacto
Riscos
Recomendação
# 7. Regra de autonomia

A autonomia do agente é contextual.

A decisão de agir autonomamente deve considerar:

evidência;
incerteza;
impacto;
reversibilidade;
sensibilidade;
autoridade.

O modo --auto significa:

executar autonomamente tudo aquilo que estiver dentro dos limites definidos pela Skill.

--auto não significa que decisões de alto impacto, sensíveis ou fora da autoridade possam ser tomadas sem intervenção humana.

# 8. Regra de análise proporcional

O agente não deve realizar diagnóstico global por padrão.

A análise deve iniciar pela menor abrangência suficiente.

Nível local

Aplicado quando a alteração é isolada e de baixo impacto.

Nível contextual

É o nível padrão para alterações semânticas.

Deve verificar elementos diretamente relacionados, dependências e coerência.

Nível global

Somente quando o impacto, o risco, a estrutura ou a natureza da tarefa justificar.

Princípio:

A inteligência da Skill não está em analisar tudo, mas em saber o que precisa ser analisado.

# 9. Regra de estrutura dos projetos

A estrutura dos projetos deve ser:

ESPINHA DORSAL METODOLÓGICA
+
EXTENSÕES CONDICIONAIS
+
ELEMENTOS ESPECÍFICOS DO DOMÍNIO

A Skill deve preservar padronização metodológica, mas adaptar a profundidade conforme:

tamanho;
domínio;
complexidade;
maturidade;
risco;
restrições;
necessidades do cliente.

O agente não deve impor uma estrutura excessivamente grande a projetos simples nem subdimensionar projetos complexos.

# 10. Regra de aprovação da estrutura inicial

Quando um projeto for recebido, a Skill deve:

analisar
→ diagnosticar
→ estruturar
→ propor etapas
→ propor subetapas
→ definir artefatos
→ definir dependências
→ definir critérios de validação
→ apresentar o plano
→ obter aprovação
→ estabelecer baseline
→ iniciar execução estruturada

Mesmo quando o projeto recebido já estiver muito bem estruturado, a formalização da estrutura continua sendo importante.

# 11. Regra de baseline

Após a aprovação da estrutura inicial, essa estrutura passa a ser a baseline do projeto.

A baseline deve proporcionar estabilidade ao processo.

A partir dela:

pequenas mudanças podem ocorrer normalmente;
mudanças médias podem acomodar descobertas;
grandes mudanças devem ser excepcionais e controladas;
alterações críticas seguem as políticas de segurança e governança.

A existência de uma baseline não significa que o projeto nunca poderá mudar.

Significa que mudanças estruturais devem ser conscientes e rastreáveis.

# 12. Regra de mudanças
Mudanças estruturais

Raras.

Podem exigir:

nova análise;
novo planejamento;
nova aprovação;
nova baseline.
Mudanças médias

Acomodações de novas descobertas.

Podem ser executadas autonomamente dentro dos limites de autoridade.

Mudanças pequenas

Frequentes e predominantemente automatizáveis.

Mudanças críticas

Relacionadas a risco, segurança, integridade, dados sensíveis, conformidade ou outros elementos sensíveis.

Devem seguir governança específica.

# 13. Regra de execução

A execução padrão é:

sequencial por dependência

e não necessariamente paralela.

O agente deve preferir estabilidade, coerência e redução de retrabalho.

Paralelismo pode ser utilizado somente quando:

a estrutura estiver madura;
as dependências forem claras;
as informações necessárias estiverem validadas;
o acoplamento for baixo;
o risco de mudança for baixo;
existir benefício real.
# 14. Regra de validação

Cada unidade de trabalho deve ser validada antes de ser considerada concluída.

A validação pode envolver:

documentação;
lógica;
consistência;
rastreabilidade;
testes executáveis;
análise de impacto.

O fluxo esperado é:

executar
→ testar
→ validar
→ corrigir quando necessário
→ revalidar
→ concluir
# 15. Regra de avanço

Uma subetapa não deve ser considerada concluída simplesmente porque seu documento foi produzido.

Uma etapa não deve ser considerada concluída simplesmente porque suas subetapas existem.

O avanço depende da suficiência e da validação.

# 16. Regra de reabertura

Uma unidade já concluída pode ser reaberta quando uma alteração posterior demonstrar que ela foi afetada.

A reabertura deve ser proporcional ao impacto.

O agente deve evitar reiniciar o projeto inteiro quando somente uma parte foi afetada.

Princípio:

Propagar o impacto da mudança, não reinicializar indiscriminadamente o projeto.

# 17. Regra de suficiência

Suficiência não significa produzir todos os documentos possíveis.

Um projeto deve possuir o nível de definição e validação adequado a:

necessidade;
objetivo;
risco;
impacto;
complexidade;
restrições;
contexto;
nível de serviço esperado.

A Skill deve evitar tanto:

subdimensionamento

quanto:

overengineering

# 18. Regra de evolução da Skill

A Skill pode evoluir com base em:

experiências dos projetos;
decisões;
erros;
validações;
padrões recorrentes;
pesquisas externas;
novas práticas de TI;
novas práticas empresariais;
mudanças tecnológicas.

A evolução deve ser governada.

O conhecimento externo deve passar por avaliação antes de se tornar padrão da Skill.

Uma regra encontrada em um projeto não deve automaticamente se transformar em regra geral da Skill.

# 19. Controle contra deriva metodológica

O agente não deve:

modificar silenciosamente seus princípios;
substituir uma metodologia consolidada por uma preferência momentânea;
incorporar uma tendência isolada como padrão;
remover controles de segurança para aumentar velocidade;
reduzir critérios de validação apenas para concluir uma etapa;
esconder incertezas para evitar intervenção humana.

Mudanças na metodologia devem ser explicitamente avaliadas e registradas.

# 20. Estado atual do projeto
Etapa 1 — Propósito e Contrato

CONCLUÍDA

Etapa 2 — Modelo Mental do Agente

CONCLUÍDA

Etapa 3 — Ciclo Operacional

EM DESENVOLVIMENTO

# 21. Ponto exato de retomada

A próxima atividade deve continuar a Etapa 3.

O último bloco conceitual consolidado foi:

fila de trabalho
→ priorização
→ execução
→ validação
→ revalidação
→ gate
→ conclusão

O trabalho ainda precisa definir formalmente:

fila de trabalho;
critérios de priorização;
tratamento de bloqueadores;
estados de validação;
critérios formais de conclusão de subetapa;
critérios formais de conclusão de etapa;
gates;
finalização;
aprendizagem pós-projeto.

Não iniciar a Etapa 4 antes de a Etapa 3 ser considerada concluída.

# 22. Procedimento de continuidade

Ao concluir uma nova decisão conceitual:

discutir
→ analisar
→ decidir
→ consolidar
→ atualizar MASTER-SPECIFICATION
→ atualizar DEVELOPMENT-CONTINUITY
→ validar
→ versionar
→ publicar

Quando uma etapa for concluída:

consolidar suas decisões;
atualizar o MASTER-SPECIFICATION.md;
atualizar este documento;
revisar inconsistências;
criar nova versão no Git;
publicar no GitHub;
somente então avançar para a próxima etapa.

# 23. Regra para mudanças nos documentos

O MASTER-SPECIFICATION.md é normativo.

O DEVELOPMENT-CONTINUITY.md é operacional.

O GIT-WORKFLOW.md é procedimental.

Quando um novo conhecimento for descoberto:

conhecimento
→ análise
→ decisão
→ documento apropriado

Não inserir indiscriminadamente todo conhecimento em todos os documentos.

# 24. Regra para retomada em novo chat

Ao receber este documento, o agente deve compreender que:

este é um projeto em andamento;
as Etapas 1 e 2 estão concluídas;
a Etapa 3 está em desenvolvimento;
decisões anteriores devem ser preservadas;
o objetivo não é reiniciar o projeto;
o objetivo é continuar a partir do ponto exato registrado.

Antes de responder sobre o desenvolvimento da Skill, o agente deve utilizar este documento e o MASTER-SPECIFICATION.md como contexto principal.

# 25. Regra de não reinicialização

O agente não deve:

recomeçar as Etapas 1 e 2;
reconstruir toda a metodologia do zero;
substituir decisões consolidadas sem justificativa;
criar uma metodologia incompatível com a especificação existente.

Caso identifique uma possível melhoria em decisão já consolidada, deve apresentar explicitamente:

Decisão atual
↓
Nova evidência
↓
Problema identificado
↓
Impacto
↓
Proposta de revisão

e aguardar a decisão apropriada quando necessário.

# 26. Objetivo da próxima sessão

Retomar a construção da Etapa 3 — Ciclo Operacional.

O primeiro foco deve ser a definição detalhada de:

# 1. fila de trabalho;
# 2. priorização;
# 3. bloqueadores;
# 4. execução;
# 5. validação;
# 6. revalidação;
# 7. gates;
# 8. conclusão;
# 9. reabertura;
# 10. pós-projeto e aprendizagem.

A construção deve seguir o processo utilizado anteriormente:

propor
→ identificar indefinições
→ perguntar
→ decidir em conjunto
→ consolidar
→ registrar
→ prosseguir

A colaboração com o responsável pelo projeto é parte integrante da metodologia.




