# Decisões de desenho do EKOM

Este documento registra as razões das principais escolhas do modelo,
incluindo as decisões históricas da EKM 1.x. Não substitui as diretrizes
operacionais vigentes do EKOM.

## DD-001 — Especificação como unidade de comportamento

**Decisão:** funcionalidades e contratos preserváveis devem ser representados por especificações incrementais.

**Motivo:** comportamentos surgem em momentos diferentes; um documento monolítico seria difícil de manter e incentivaria inferências.

## DD-002 — Não existe um único documento da verdade

**Estado:** substituída por DD-031 e ADR-0001 no EKOM 2.0.

**Decisão:** a verdade é distribuída por fontes com responsabilidades explícitas e conectadas por um mapa.

**Motivo:** comportamento, motivação, execução e evidência têm ciclos de vida e autoridades diferentes.

## DD-003 — Dossiê é visão geral, não substituto

**Decisão:** o dossiê facilita navegação e entendimento inicial, mas aponta para especificações especializadas.

**Motivo:** duplicar detalhes cria fontes concorrentes e divergência.

## DD-004 — Estados normativo e de implementação independentes

**Decisão:** cada especificação declara sua autoridade e, separadamente, a situação da implementação.

**Motivo:** uma especificação pode estar vigente sem estar implementada; uma implementação pode existir sem validação suficiente ou estar regredida.

## DD-005 — Transações e lacunas têm identidade própria

**Decisão:** mudanças usam `EKM-CHG-NNNN`; ausências de conhecimento usam `EKM-GAP-NNNN`.

**Motivo:** tarefas concluídas e conhecimento faltante precisam permanecer rastreáveis sem depender de conversas ou listas informais.

## DD-006 — O estado de referência é a árvore de trabalho observada

**Estado:** substituída por DD-019 no modelo 1.9.

**Decisão:** a comparação inclui alterações rastreadas, não rastreadas e preexistentes, não apenas `HEAD`.

**Motivo:** Git identifica commits, mas uma tarefa pode começar sobre trabalho ainda não consolidado.

## DD-007 — Relatório não é fonte normativa

**Decisão:** relatórios registram evidências e desvios, mas não criam ou alteram requisitos implicitamente.

**Motivo:** um relatório descreve uma execução específica e pode omitir consequências semânticas.

## DD-008 — Specification on touch

**Decisão:** ao modificar uma funcionalidade relevante ainda não especificada, seu domínio deve atingir ao menos `Specified`.

**Motivo:** documentar todo o legado de uma vez é caro; não documentar o que muda perpetua perda de conhecimento.

## DD-009 — `Active` exige autoridade humana ou inequívoca

**Decisão:** comportamento descoberto no código não deve virar requisito vigente apenas por inferência do agente.

**Motivo:** o código pode conter bugs, acidentes históricos, compatibilidade obsoleta ou experimentos.

## DD-010 — Autonomia proporcional à certeza

**Decisão:** agentes avançam autonomamente em descobertas e análises verificáveis. Em uma implementação regida por uma especificação atômica, qualquer requisito obrigatório dependente de julgamento bloqueia o recorte inteiro antes da primeira alteração.

**Motivo:** adoção e investigação podem ser incrementais, mas implementar parcialmente uma especificação incompleta rompe a unidade de delegação e permite decisões normativas silenciosas.

## DD-011 — Estrutura mínima antes de expansão

**Decisão:** começar com `AGENTS.md`, mapa, histórico de mudanças, dossiê e
especificações necessárias. Uma diretriz local só é criada quando não existe
referência externa aplicável ou há regras próprias.

**Motivo:** padronização facilita adoção, mas arquivos sem autoridade ou uso claro criam burocracia.

## DD-012 — Revisão de implementabilidade obrigatória

**Decisão:** toda especificação deve receber resultado Implementável
[`Implementable`] ou Precisa de esclarecimento [`Needs Clarification`] antes de
qualquer alteração de implementação.

**Motivo:** um processo de construção funcional pode esconder uma decisão
inferida que não corresponde à intenção. Concentrar lacunas antes do código
aumenta a confiabilidade e permite execução posterior verdadeiramente autônoma.

## DD-013 — Versões normativas em produção são imutáveis

**Decisão:** após `Done`, alterações de comportamento usam nova especificação relacionada, sem reescrever a versão integrada.

**Motivo:** reescrever uma especificação de produção destrói a correspondência histórica entre intenção, implementação e evidência.

## DD-014 — Garantias automatizadas são uma capacidade futura

**Estado:** preservada como decisão histórica; fora do escopo do modelo 1.9.

**Decisão:** prever um `EKM Gate`, sem definir prematuramente sua arquitetura ou alegar garantia ainda inexistente.

**Motivo:** regras verificáveis não devem depender apenas de disciplina, mas a automação precisa nascer de requisitos e experimentos próprios e não substitui julgamento semântico humano.

## DD-015 — Revisão não autoriza a própria implementação

**Estado:** parcialmente substituída por DD-018 e DD-020 no modelo 1.9.

**Decisão:** a revisão de implementabilidade é cumulativa, ocorre em execução
separada da implementação e produz uma recomendação submetida ao responsável
humano. Mesmo Implementável [`Implementable`] exige aprovação explícita e
reconfirmação do estado de referência antes da primeira alteração.

**Motivo:** o mesmo executor pode encontrar um bloqueio suficiente e interromper
prematuramente a investigação, deixando outras lacunas sem registro. Também
existe conflito de responsabilidade quando o agente produz e consome sua própria
autorização. A separação manual preserva o protagonismo humano sem exigir
prematuramente múltiplos agentes ou fluxo automatizado.

## DD-016 — Governança e parecer humano precedem implementabilidade

**Estado:** substituída por DD-018 no modelo 1.9.

**Decisão:** a EKM busca autonomia governada, não autonomia máxima. A modalidade
de confecção da especificação fica fora do contrato e sua automação não é
prevista como requisito ou capacidade do método. O artefato somente segue para
revisão de implementabilidade após parecer humano explícito de que representa a
intenção conhecida.

Esse parecer é diferente tanto do resultado técnico `Implementable` quanto da
autorização humana posterior para alterar o código. Inicialmente, seu registro é
declarativo e não implica verificação automatizada de identidade ou autoridade.

**Motivo:** o Engenheiro Analista deve avaliar se um contrato aceito é passível
de implementação, não decidir o que o produto deve fazer. Interação humana em
decisões, aprovações e validações é governança esperada; o que deve ser reduzido
é retrabalho e coordenação operacional sem valor decisório.

## DD-017 — Português canônico e identificadores legados explícitos

**Decisão:** o português do Brasil é o idioma normativo canônico da EKM.
Termos técnicos externos e identificadores legados podem ser preservados, mas
devem possuir significado canônico em português e aparecer delimitados como
identificadores.

Resultados sobre intenção, admissão, implementabilidade, autorização,
implementação e auditoria devem declarar seu contexto. Um mesmo identificador
legado não autoriza tratar decisões diferentes como equivalentes.

**Motivo:** a mistura não controlada de português e inglês, somada ao uso
contextualmente diferente de valores como `Accepted`, `Pending` e `Blocked`,
aumenta ambiguidade para pessoas, agentes e futuras automações. Traduzir
comandos, APIs ou identificadores de forma indiscriminada também reduziria a
precisão e quebraria compatibilidade. A separação entre rótulo normativo e
identificador preserva clareza e migração gradual.

## DD-018 — Autoridade do Arquiteto e ordem como autorização

**Estado:** esclarecida por DD-032 no EKOM 2.1 quanto à ordem mínima e ao
significado de recorte no ciclo funcional.

**Decisão:** o Arquiteto humano sempre prevalece sobre decisões e recomendações
dos agentes. Cada tarefa é iniciada por ordem do Arquiteto, por prompt ou
pipeline, e essa ordem autoriza a etapa e o recorte solicitados. Não se exige um
segundo registro declarativo de aceite, identidade, data ou marco Git para
repetir a autorização.

A autoridade humana não reescreve fatos: falhas e limitações observadas
permanecem registradas. Se a decisão mudar o comportamento esperado, a
especificação é atualizada.

**Motivo:** o piloto mostrou que múltiplos pareceres documentais repetiam uma
decisão que já estava presente na própria ação do Arquiteto. Preservar a
autoridade sem duplicar sua ordem reduz carga cognitiva e mantém claro quem
decide.

## DD-019 — Git como trilha técnica e entrega obrigatória

**Decisão:** o Git é a fonte da linhagem técnica. SHA, branch de origem, mensagem
de commit e checkpoints não são campos obrigatórios em documentos EKM.

Cada tarefa de agente deve começar com árvore limpa, produzir resultado material
e terminar com commit, push e árvore limpa. Falha no push significa que a etapa
não foi entregue. A ordem normal não autoriza force push, reescrita de
histórico, merge, tag, release ou deploy.

**Motivo:** copiar metadados do Git para o changelog não agrega entendimento
humano e cria divergência e manutenção manual. Em contrapartida, commit e push
são necessários para que o resultado do agente exista de forma versionada e
possa alimentar a próxima etapa.

## DD-020 — Governança proporcional e estado como passagem

**Estado:** parcialmente substituída por DD-032 no EKOM 2.1. A dispensa de
matriz universal e a proporcionalidade continuam vigentes; a permissão de
encerrar a análise formal no primeiro bloqueio não continua.

**Decisão:** a especificação contém o estado necessário para a etapa seguinte.
O changelog registra apenas decisões, lacunas, evidências materiais e resultado.
Matrizes extensas, revisão técnica independente e auditoria de integridade são
usadas somente quando o Arquiteto considerar que agregam confiança ao recorte.

Ao encontrar uma lacuna bloqueante clara, a análise pode encerrar sem buscar uma
classificação exaustiva. Itens materiais já descobertos devem ser agrupados.

**Motivo:** o protocolo anterior tornou cada transferência auditável, mas
introduziu formulários, checkpoints, papéis universais e repetição sem benefício
proporcional. A dose inicial deve proteger conhecimento e decisão enquanto
permite experimentar, entregar e descartar hipóteses rapidamente.

## DD-021 — Pipeline somente como ordem lógica

**Estado:** substituída em parte por DD-031 e ADR-0001 no EKOM 2.0. A exclusão
de filas, locks e infraestrutura universal continua vigente; a exclusão de
orquestração não continua.

**Decisão:** o fluxo atual é uma sequência de etapas comandadas pelo Arquiteto.
O modelo 1.9 não incorpora concorrência, locks, filas ou mecanismos de
orquestração, e esses conceitos não participam dos experimentos atuais.

**Motivo:** não se deve adicionar ao processo uma preocupação ainda não adotada.
Antecipá-la criaria regras e custo antes de existir evidência de utilidade.

## DD-022 — Fluxo iniciado em branch derivada da `main`

**Decisão:** todo fluxo de trabalho deve começar em uma branch de trabalho
derivada da `main`, nunca diretamente na `main`. A mesma branch pode atravessar
as etapas autorizadas do recorte; não se exige uma branch nova por atuação.

**Motivo:** usar a `main` como origem comum torna explícito o baseline de
produção, preserva a linhagem da mudança e mantém o trabalho isolado até a
decisão humana de integração, sem duplicar metadados do Git nos documentos EKM.

## DD-023 — Modelo de atores como fluxo oficial

**Decisão:** a EKM 1.11 organiza cada tarefa por um papel explicitamente
selecionado na ordem do Arquiteto. O agente lê as regras comuns, exatamente um
perfil correspondente, a especificação indicada e somente as fontes técnicas
pertinentes.

Os atores oficiais são Autor da Especificação, Engenheiro Analista, Engenheiro
Implementador e Engenheiro Revisor. Cada ator atualiza o conhecimento afetado,
promove somente os estados sustentados por sua etapa e entrega o resultado por
commit e push. Não existe um ator adicional destinado apenas a reconciliar ou
versionar o trabalho dos demais.

O Engenheiro Revisor pode registrar validação do Tech Lead, aprovação do
Arquiteto e confirmação de integração quando essas decisões já tiverem sido
fornecidas explicitamente. Ele não produz aprovação própria nem substitui a
autoridade humana.

**Motivo:** o ciclo completo no aplicativo iotsmarthome demonstrou que prompts
curtos e perfis referenciados conseguem dirigir agentes e modelos diferentes,
preservando continuidade por meio da especificação, dos estados e do Git. O
mesmo caso mostrou que papéis incompatíveis e regras genéricas favorecem
promoções incorretas e reinterpretações. Tornar responsabilidades e passagens
explícitas aumenta aderência sem criar um ator burocrático de reconciliação.

## DD-024 — O Autor investiga e propõe sem revisar a própria implementabilidade

**Decisão:** o Autor da Especificação pode analisar um problema complexo,
inspecionar fontes técnicas, comparar alternativas e propor uma solução
arquitetural e implementável. Não é criado um papel adicional de coautoria.

Essa decisão rejeita um coautor dentro do fluxo funcional. Ela não impede um
papel institucional de apoio ao Arquiteto fora desse fluxo, posteriormente
definido por `DD-026`.

O Autor separa fatos observados, intenção e decisões confirmadas, solução
proposta e decisões pendentes. Recomendações permanecem subordinadas ao
Arquiteto. A própria autoria não produz `Implementable`: a revisão de
implementabilidade continua pertencendo a uma atuação independente do
Engenheiro Analista.

**Alternativas consideradas:**

- criar um Coautor ou Especialista de Solução formal foi rejeitado porque
  duplicaria a responsabilidade do Autor e acrescentaria passagem operacional;
- limitar o Autor à transcrição de requisitos foi rejeitado porque problemas
  transversais exigem investigação e desenho antes de formarem um contrato
  implementável;
- permitir que o Autor aprovasse a própria implementabilidade foi rejeitado
  porque eliminaria a verificação independente e misturaria produção e
  autorização do contrato;
- tratar o Autor como Autor/Analista foi rejeitado porque tornaria ambíguo qual
  atuação sustenta `Implementable`.

**Motivo:** o perfil anterior já exigia uma especificação implementável, mas
não explicitava que a investigação e a proposição de solução pertenciam à
autoria. Essa ambiguidade permitia tanto uma autoria superficial quanto a
criação de decisões pendentes artificiais para escolhas opcionais. Um
experimento anterior registrou sobreposição parcial da autoria com a revisão de
implementabilidade e lacunas artificiais; o início do experimento de remoção de
dados sensíveis tornou explícita a hipótese de que a autoria de um problema
transversal precisa formular uma solução, não apenas reproduzir a intenção
inicial.

Essa primeira autoria ainda não foi avaliada pelo Arquiteto e não constitui
evidência de sucesso da decisão. Ela motivou o esclarecimento normativo que será
confrontado nas etapas seguintes.

**Riscos para reavaliação:**

- o Autor pode apresentar recomendação como decisão confirmada;
- pode devolver escolhas técnicas resolvíveis como falsas decisões do
  Arquiteto;
- pode produzir proposta enviesada que o Analista apenas ratifique;
- a separação conceitual pode não ser suficiente para preservar independência
  quando agentes compartilham contexto.

A decisão deve ser reavaliada se os experimentos mostrarem autoaprovação,
aumento de decisões artificiais, perda de independência da análise ou
necessidade recorrente de um especialista com responsabilidade realmente
distinta. A motivação e estes critérios permanecem neste registro de desenho,
fora das fontes carregadas pelos atores em uma tarefa funcional normal; o
perfil contém somente a regra operacional necessária.

## DD-025 — Objetivos multi-contexto usam coordenação por especificações

**Decisão:** quando um objetivo depende de fontes e implementações mantidas em
repositórios, serviços, aplicativos ou infraestruturas independentes, a EKM usa
uma especificação coordenadora para o resultado ponta a ponta e especificações
subordinadas executáveis em cada contexto de entrega.

A especificação coordenadora registra decisões arquiteturais, relações,
dependências e critérios de integração. Cada especificação subordinada
permanece junto às fontes que governam sua implementação, percorre o fluxo
normal de atores e promove somente os próprios estados. A conclusão de um
recorte não promove automaticamente os demais nem comprova o objetivo
coordenado; este exige evidência de integração dos recortes obrigatórios.

As relações registram identificadores, fontes responsáveis, dependências e
estados materiais. Não duplicam especificações externas nem transcrevem a
linhagem preservada pelo Git.

**Motivo:** a análise da remoção de dados sensíveis do `iotsmarthome` mostrou
que o resultado depende primeiro de mudanças no provedor OAuth/OIDC, nas APIs
protegidas e no contrato de configuração, além da posterior migração do
aplicativo. Tratar tudo como uma única especificação local permitiria que um
ator do app inferisse contratos externos ou declarasse um resultado impossível
de validar naquele repositório. Tratar cada mudança isoladamente, sem uma fonte
coordenadora, perderia o objetivo arquitetural que dá sentido aos recortes.

**Alternativas consideradas:**

- ampliar a especificação do aplicativo para autorizar mudanças em todos os
  repositórios foi rejeitado por misturar fontes, autoridades e ciclos de
  integração independentes;
- criar um novo Coordenador como ator obrigatório foi rejeitado porque o
  Arquiteto já dirige as atuações e as especificações podem preservar as
  relações materiais;
- usar apenas uma lista informal de tarefas foi rejeitado porque não preserva
  contratos, decisões nem critérios de conclusão ponta a ponta;
- exigir sincronização automática, locks ou estado distribuído foi rejeitado
  por antecipar mecanismos ainda não adotados.

**Aplicação proporcional:** a estrutura só é usada quando existe dependência
material entre contextos de entrega. Uma mudança inteiramente local continua
com uma única especificação e o fluxo normal.

**Critérios de reavaliação:** reavaliar se a coordenação duplicar conhecimento,
criar manutenção manual sem apoiar decisões, tornar ambígua a autoridade dos
estados ou não permitir verificar a integração ponta a ponta.

## DD-026 — Consultor de Arquitetura como apoio institucional subordinado

**Decisão:** a EKM institui o Consultor de Arquitetura como papel de IA que
apoia o Arquiteto e o Tech Lead em atividades transversais. O Arquiteto
permanece o ator principal e a única autoridade final sobre intenção,
arquitetura, risco, autorização, validação e integração.

O Consultor pode investigar, propor e executar documentação, código, testes,
configuração, análise, revisão ou coordenação somente dentro de ordem explícita
do Arquiteto. O papel não concede permissão implícita para qualquer dessas
operações e não transforma a IA em aprovadora das próprias recomendações.

Antes do commit final, o Consultor apresenta e recebe confirmação explícita do
Arquiteto sobre um registro que identifica ordem, recorte, operações, decisões
confirmadas, resultado e limitações. Essa confirmação não equivale a aprovação
técnica, validação ou integração, salvo quando o Arquiteto atribuir
explicitamente esse significado.

**Relação com decisões anteriores:**

- `DD-018` continua válida para os atores funcionais; o registro adicional do
  Consultor é uma exceção proporcional à amplitude de sua atuação;
- `DD-023` continua definindo somente quatro atores no pipeline;
- `DD-024` continua rejeitando um coautor dentro da autoria funcional;
- `DD-025` continua coordenando objetivos multi-contexto por especificações,
  sem transformar o Consultor em orquestrador ou fonte global de estado.

**Salvaguardas:**

- cada ordem identifica resultado, repositório, recorte e operações;
- ampliações materiais exigem nova confirmação antes da ação;
- decisões propostas só se tornam confirmadas por manifestação do Arquiteto;
- o Tech Lead não delega autoridade reservada sem delegação explícita;
- participação anterior impede alegação posterior de independência no mesmo
  recorte;
- ações destrutivas, merge, release e deploy mantêm autorização específica;
- o registro final é confirmado antes do commit e preservado na fonte
  materialmente apropriada.

**Alternativas consideradas:**

- manter a colaboração arquitetural apenas informal foi rejeitado porque
  decisões e autorizações ficariam dependentes da conversa;
- tornar o Consultor um quinto ator sequencial foi rejeitado porque apoio
  transversal não corresponde a uma etapa única;
- conceder autorização ampla por definição do papel foi rejeitado porque
  inverteria a autoridade e ampliaria silenciosamente o escopo;
- obrigar o Consultor a trocar de papel para toda contribuição foi rejeitado
  porque impediria coautoria de governança e arquitetura, embora promoções
  formais continuem pertencendo aos atores;
- dispensar o registro final foi rejeitado porque a amplitude do papel exige
  tornar localizável o que o Arquiteto efetivamente autorizou e confirmou.

**Motivo:** decisões de arquitetura, evolução da EKM e apoio ao Tech Lead já
são discutidos com IA, mas o modelo não possuía um papel institucional para
essa colaboração. Ordens ad hoc tornavam ambíguos o recorte permitido, a
autoridade humana preservada e o valor probatório da participação da IA.

**Critérios de reavaliação:** reduzir ou retirar o papel se o registro final
virar formalidade sem apoiar decisão, se surgir autorização genérica, se o
Consultor obscurecer a responsabilidade dos atores, se a confirmação humana
for confundida com validação ou se a participação transversal comprometer
revisões independentes.

### Registro inaugural da atuação

**Estado da confirmação final:** Confirmada pelo Arquiteto.

O Arquiteto confirmou o registro inaugural e autorizou o commit e o push do
resultado preparado. A confirmação não declarou eficácia comprovada, validação
experimental, integração à `main`, release ou deploy.

- **Papel exercido:** Consultor de Arquitetura e par do Arquiteto na autoria da
  EKM.
- **Ordem autorizada:** criar um papel institucional de IA para apoiar
  transversalmente o Arquiteto e o Tech Lead, preservando o Arquiteto como ator
  principal.
- **Repositório e recorte:** `EKM-guidelines`; método, perfil, regras comuns,
  roteamento, templates, histórico, decisão de desenho e caso de estudo em
  andamento.
- **Operações autorizadas:** investigar as fontes vigentes, propor o contrato,
  editar documentação e templates, validar a consistência e, após confirmação
  final, criar commit e realizar push.
- **Decisões explicitamente recebidas:** o Consultor pode atuar em todas as
  naturezas de atividade quando solicitado pelo Arquiteto; cada atuação depende
  de autorização e confirmação explícitas; a autorização deve ficar registrada
  ao final; o Arquiteto continua sendo o ator principal.
- **Resultado material preparado:** EKM 1.14 com perfil
  `CONSULTOR-DE-ARQUITETURA`, comando reutilizável, salvaguardas de autoridade e
  independência, atualização das fontes vigentes e registro no caso de estudo.
- **Validações e limitações:** consistência textual, referências e versões
  verificadas; nenhuma eficácia do papel foi ainda demonstrada; esta atuação
  participou da solução e não pode constituir revisão independente dela.
- **Significado solicitado para a confirmação final:** confirmar que este
  registro representa a autorização e as decisões do Arquiteto e autorizar o
  commit e o push do resultado preparado. A confirmação não declara eficácia,
  validação experimental, integração à `main`, release ou deploy.

## DD-027 — Preservação arquitetural local com evolução explícita

**Decisão:** a EKM estabelece como comportamento padrão que implementações
preservem a arquitetura, a organização e a separação de responsabilidades do
repositório, usando o precedente equivalente mais próximo. Um agente não cria
nova camada, pasta estrutural, abstração transversal ou padrão arquitetural por
preferência própria.

Uma especificação Implementável pode autorizar evolução arquitetural quando a
mudança for consciente e delimitada. Para isso, ela identifica:

1. o padrão, a restrição ou o precedente atual afetado;
2. a mudança pretendida;
3. o alcance da mudança;
4. a justificativa ou decisão do Arquiteto que a sustenta.

Ausência de orientação, necessidade técnica inferida, oportunidade de melhoria
ou redação genérica não constituem autorização. Ausência ou conflito de
precedentes devolve a decisão ao Arquiteto.

**Aplicação por ator:**

- o Autor localiza o precedente e torna qualquer desvio explícito;
- o Analista verifica se a mudança pode ser executada sem inferência
  arquitetural;
- o Implementador preserva o precedente ou executa somente o desvio
  delimitado;
- o Revisor confronta organização, responsabilidades e autorização do desvio.

**Aplicação proporcional:** a EKM central define o comportamento, mas a
arquitetura concreta permanece no repositório. O `AGENTS.md` apenas localiza as
fontes técnicas e declara invariantes locais. Não é criado um documento
arquitetural obrigatório; a especificação detalha os quatro elementos somente
quando existir desvio.

**Alternativas consideradas:**

- congelar todo padrão existente foi rejeitado porque transformaria legado em
  norma e impediria evolução intencional;
- permitir que o agente reorganize o projeto quando julgar tecnicamente melhor
  foi rejeitado porque transfere decisão arquitetural e amplia escopo;
- exigir aprovação externa para todo novo arquivo foi rejeitado por adicionar
  custo sem distinguir manutenção comum de mudança estrutural;
- criar um manual arquitetural universal na EKM foi rejeitado porque padrões
  pertencem ao contexto de cada repositório.

**Motivo:** uma regra curta e localizável reduz a criação incidental de
estruturas desconhecidas e a mistura de responsabilidades, preservando uma
válvula de escape para mudanças conscientemente conduzidas pela especificação.

**Caráter experimental:** a regra será inicialmente observada no ciclo da
especificação `OAUTH-END-USER-AUTHORIZATION-001`. Ela ainda não comprova
redução de retrabalho ou aumento de aderência entre modelos. A adoção da EKM
1.15 nesse repositório permanece uma mudança local separada.

**Critérios de reavaliação:** simplificar, retirar ou especializar a regra se
ela congelar código inadequado, gerar consultas frequentes sem valor, permitir
interpretações divergentes de “precedente equivalente” ou não reduzir desvios
arquiteturais materiais.

**Estado da decisão:** confirmada pelo Arquiteto para incorporação à EKM 1.15.

### Registro da atuação EKM 1.18

**Estado da confirmação final:** Confirmada pelo Arquiteto.

- **Papel exercido:** Consultor de Arquitetura e par do Arquiteto.
- **Ordem autorizada:** incorporar à EKM a preservação arquitetural local com
  uma exceção consciente e explícita pela especificação.
- **Repositório e recorte:** `EKM-guidelines`; método, regras comuns, perfis dos
  quatro atores, templates, governança, conceito e decisão de desenho.
- **Operações autorizadas:** editar as fontes afetadas, validar consistência,
  criar commit e realizar push.
- **Decisões confirmadas:** preservar arquitetura, organização e separação de
  responsabilidades por padrão; autorizar desvios somente quando a
  especificação identificar padrão atual, mudança, alcance e justificativa ou
  decisão do Arquiteto.
- **Resultado material:** EKM 1.15 preparada sem novo documento obrigatório,
  com responsabilidades distribuídas pelos atores e observação inicial
  prevista no ciclo `OAUTH-END-USER-AUTHORIZATION-001`.
- **Validações e limitações:** consistência textual e de versões verificada;
  eficácia ainda não demonstrada. O Consultor participou da criação e não pode
  atuar como revisor independente dessa regra.
- **Significado da confirmação:** o Arquiteto confirmou que o registro
  representa a discussão e autorizou commit e push. A confirmação não declara
  eficácia experimental, validação funcional, integração à `main`, release ou
  deploy.

## DD-028 — Conclusão exige estado terminal das execuções iniciadas

**Decisão:** nenhum agente pode promover estado, registrar validação como
aprovada, criar o commit final, realizar push ou emitir resposta conclusiva
enquanto tarefa, comando, processo, build, teste, upload ou execução delegada
que tenha iniciado permanecer em estado não terminal ou desconhecido.

Antes do encerramento, o agente identifica essas execuções, confirma o estado
terminal e captura resultado, código de saída ou limitação material. Trabalho
inconclusivo não se converte em sucesso por cancelamento, abandono ou emissão de
relatório.

**Evidência:** na análise de `OAUTH-END-USER-AUTHORIZATION-001`, um agente
promoveu a especificação, criou commit, realizou push e declarou conclusão
enquanto duas tarefas de build ainda executavam; uma permanecia pendente após o
relatório.

**Proporcionalidade:** o controle é local ao trabalho iniciado pelo próprio
agente. Ele permite continuar outras ações autorizadas durante a espera e não
introduz fila, lock, orquestrador ou sincronização entre atores.

**Alternativas rejeitadas:**

- confiar que a ferramenta cancelará tarefas ao concluir foi rejeitado porque
  não preserva resultado nem código de saída;
- exigir espera imediata após cada comando foi rejeitado porque impediria
  paralelismo útil;
- aplicar a regra somente a builds foi rejeitado porque testes, uploads e
  execuções delegadas produzem o mesmo risco de evidência prematura.

**Critérios de reavaliação:** simplificar a enumeração de estados ou operações
se ambientes diferentes não conseguirem aplicá-la de forma consistente;
especializar a regra se ela bloquear trabalho sem relação com evidência ou
entrega.

**Estado da decisão:** confirmada pelo Arquiteto para incorporação à EKM 1.16.

## DD-029 — Adequação é medida por perfil executor, papel e amostra

**Decisão:** a EKM adota experimentalmente uma métrica de zero a cem para
avaliar autoridade e escopo, correção técnica, evidências, conhecimento EKM e
encerramento Git. Desvios críticos são eliminatórios e não podem ser compensados
pela soma.

A unidade avaliada combina modelo, ambiente agente, configuração, instruções,
versão EKM e papel. Aceitação para um papel exige ao menos três execuções em
dois contextos, média mínima de 85, nenhuma nota abaixo de 75 e nenhum desvio
eliminatório.

**Motivo:** uma nota intuitiva isolada não explica por que uma execução foi
aceitável, mistura resultado técnico com conformidade e pode atribuir ao modelo
um comportamento causado pelo ambiente ou pelas ferramentas.

**Evidência inicial:** a análise de `OAUTH-END-USER-AUTHORIZATION-001` produziu
uma conclusão de implementabilidade defensável, mas encerrou antes das tasks,
omitiu uma falha de teste e misturou prontidão com estado normativo no mapa. A
decomposição resultou em 60/100 e tornou visíveis os descontos materiais.

**Evidência adicional:** duas execuções do Claude Sonnet 5 no Claude Code sem
adaptador explícito para `AGENTS.md` foram Reprovadas com 61/100 e 67/100 por
encerramento Git incompleto. Mantidos modelo, ambiente, papel, especificação e
prompt mínimo, a inclusão de `CLAUDE.md` como roteador das fontes EKM produziu
uma execução Aceitável de 89/100, sem eliminatório. O resultado confirma que o
mecanismo de carregamento das instruções integra a configuração avaliada e que
perfis com e sem o adaptador não devem ser tratados como equivalentes.

**Proporcionalidade:** a métrica permanece experimental e não cria uma etapa
obrigatória em toda tarefa. Ela é aplicada quando o Arquiteto avaliar perfis,
experimentos ou decisões de autonomia.

**Alternativas rejeitadas:**

- classificar somente pelo nome do modelo foi rejeitado porque ambiente e
  configuração alteram o comportamento;
- aceitar por uma única execução foi rejeitado porque não demonstra
  repetibilidade;
- usar apenas eliminatórios foi rejeitado porque não diferencia qualidade entre
  execuções válidas;
- usar apenas média foi rejeitado porque permitiria compensar falha crítica com
  pontos em dimensões menos relevantes.

**Critérios de reavaliação:** após cinco a dez execuções, revisar pesos,
limiares, consistência entre avaliadores, custo do registro e poder de prever
retrabalho. Simplificar ou retirar a métrica se ela gerar falsa precisão ou
burocracia sem ganho decisório.

**Estado da decisão:** confirmada pelo Arquiteto para incorporação experimental
à EKM 1.17.

## DD-030 — Critérios de aceite precisam permitir asserção objetiva

**Decisão:** cada requisito obrigatório possui critério suficiente para que o
executor classifique a evidência como aprovação, reprovação ou ausência de
verificação sem inventar o comportamento esperado durante a implementação.

O critério identifica, proporcionalmente ao risco, cenário ou condição inicial,
ação ou evento, resultado observável e evidência. Agrupamento só é válido quando
um mesmo oráculo comprova todos os requisitos agrupados. Mocks, fakes,
emuladores e fixtures preservam as semânticas materiais substituídas.
Compilação não é execução; quando o comportamento precisar ser executado, zero
casos ou falha de infraestrutura não aprovam o critério.

**Problema observado:** na implementação experimental de persistência binária
do IoTSmartSysCore, uma especificação listava testes esperados, mas não tornava
explícitos os oráculos. O executor:

- declarou que todas as classes derivadas passavam por um caminho comum sem
  confrontar o override de LED;
- testou a válvula com mock que aceitava `open`/`closed`, embora o adapter real
  exigisse conversão para `on`/`off`;
- tratou tamanho e versão como evidência suficiente de corrupção;
- registrou compilação com zero casos executados como suporte a `Implemented`;
- não produziu a injeção separada de falhas NVS exigida.

**Aplicação por ator:** o Autor define critérios assertáveis; o Analista
confirma suficiência e viabilidade; o Implementador confronta todos com
evidência terminal; o Revisor verifica a correspondência entre oráculo,
evidência e integração real.

**Proporcionalidade:** a regra não exige linguagem Gherkin, matriz universal,
um teste por requisito nem execução em hardware para todo recorte. Critérios
podem compartilhar evidência e usar inspeção ou validação humana quando isso
for suficiente, desde que ainda distingam os três resultados.

**Alternativas rejeitadas:**

- exigir apenas “mais testes” foi rejeitado porque quantidade não corrige
  oráculo incompatível;
- tornar integração real obrigatória em todos os testes foi rejeitado porque
  doubles semanticamente fiéis continuam úteis;
- impor formato universal detalhado foi rejeitado porque aumentaria carga
  cognitiva sem ganho proporcional em recortes simples;
- confiar que o Revisor descobrirá critérios implícitos foi rejeitado porque
  transfere ao fim do ciclo uma ambiguidade que deveria limitar a implementação.

**Critérios de reavaliação:** simplificar se a regra produzir repetição
editorial; especializar se agentes continuarem criando mocks incompatíveis ou
promovendo estados com zero execução; retirar se não reduzir falso sucesso e
retrabalho em novos experimentos.

**Estado da decisão:** confirmada pelo Arquiteto para incorporação à EKM 1.18.

**Operacionalização na EKM 1.19:** o perfil do Autor passa a exigir inventário
rastreável dos requisitos, escrita explícita de condição inicial, ação,
resultado e evidência, confronto com uma implementação incorreta plausível,
fidelidade semântica dos doubles e separação entre gate automatizável e
validações posteriores. A especificação só segue para análise quando um
executor independente consegue transformar o resultado em asserção sem tomar
nova decisão funcional ou arquitetural.

Esse detalhamento preserva a proporcionalidade da decisão: não exige Gherkin,
um teste por requisito, matriz universal nem antecipação da estrutura interna.

**Refinamento no EKOM 2.1:** o experimento do registry de dispositivos pareados
em NVS confirmou que a utilidade vinha dos cenários explícitos, não do volume de
campos. A escrita `Dado / Quando / Então` passa a ser a forma preferida quando
melhora a leitura, sem obrigatoriedade de Gherkin. Evidência parcial deve ser
nomeada como parcial e nunca sustenta aprovação do critério completo. O template
deixa de repetir um checklist de autoria com oito itens; as regras continuam no
perfil e no método, enquanto a especificação preserva apenas o contrato útil à
implementação e à validação.

### Registro da atuação

**Estado da confirmação final:** Confirmada pelo Arquiteto.

- **Papel exercido:** Consultor de Arquitetura e par do Arquiteto.
- **Ordem autorizada:** transformar o problema observado no experimento de
  persistência binária em critérios de aceite claros, simples e assertáveis na
  EKM.
- **Repositórios e recorte:** `EKM-guidelines` e adoção local no
  IoTSmartSysCore; método, regras comuns, decisão de desenho, histórico
  experimental, navegação e templates afetados.
- **Operações autorizadas:** investigar as fontes vigentes, editar governança e
  templates, reconciliar a adoção local, validar consistência e, após
  confirmação final, criar commits e realizar push.
- **Decisões confirmadas:** restaurar posteriormente o projeto ao estado
  anterior à implementação; adicionar critérios suficientes para o agente
  afirmar conformidade; tornar a diretiva explícita na EKM oficial.
- **Resultado material preparado:** EKM 1.18 com critérios assertáveis por
  cenário, resultado observável e evidência, fidelidade semântica de doubles,
  distinção entre compilação e execução e gate de `Implemented`.
- **Validações e limitações:** integridade textual e versões verificadas; a
  eficácia da regra ainda não foi demonstrada e será confrontada pela nova
  execução do experimento. O Consultor participou desta solução e não poderá
  alegar revisão independente dela.
- **Significado solicitado para a confirmação final:** confirmar que este
  registro representa a ordem, as decisões e o resultado preparados e
  autorizar commit e push nos dois repositórios. A confirmação não declara
  eficácia da EKM 1.18, validação funcional, integração à `main`, release ou
  deploy.

### Registro da operacionalização EKM 1.19

**Estado da confirmação final:** Confirmada pelo Arquiteto.

- **Papel exercido:** Consultor de Arquitetura.
- **Ordem autorizada:** criar diretrizes claras para que o Autor da
  Especificação elabore critérios de aceite assertáveis.
- **Repositório e recorte:** `EKM-guidelines`; perfil do Autor, método,
  template de especificação, decisão de desenho, histórico experimental,
  navegação e referências de versão afetadas.
- **Operações autorizadas:** investigar as fontes vigentes, editar a governança,
  validar consistência e, após confirmação final, criar commit e realizar push.
- **Decisões confirmadas:** operacionalizar a regra transversal da EKM 1.18 no
  perfil do Autor e adotá-la como evolução compatível EKM 1.19.
- **Resultado material produzido:** procedimento rastreável de autoria, teste
  de suficiência independente, falsificabilidade da evidência, fidelidade
  semântica dos doubles, separação dos gates e checklist no template.
- **Validações e limitações:** integridade textual verificada; a eficácia será
  confrontada na repetição do experimento. O IoTSmartSysCore ainda não adotou a
  EKM 1.19. O Consultor participou da formulação e não poderá alegar revisão
  independente dela.
- **Significado da confirmação final:** aprovar a formulação como EKM 1.19 e
  autorizar commit e push no repositório oficial. A confirmação não declara
  eficácia, não atualiza o projeto adotante e não aprova a especificação
  funcional.

## DD-031 — Especificações orquestram; código implementa

**Decisão:** o Engineering Knowledge Orchestration Model (EKOM) 2.0 sucede a
formulação Engineering Knowledge Model (EKM) 1.x. A especificação é a fonte
única da verdade para o comportamento pretendido e o principal objeto do
pipeline. Ela atua como plano de controle que coordena humanos, agentes de IA,
automações, implementação, validação, evidências e evolução.

> **Specifications orchestrate. Code implements.**

Fontes permanecem separadas por responsabilidade, mas não por autoridade
normativa concorrente. ADRs explicam decisões; diretrizes governam o método;
mapas localizam; código e testes implementam e comprovam; Git preserva linhagem;
relatórios registram execuções. Cada fonte referencia a especificação aplicável.

**Motivo:** a evolução do modelo de atores demonstrou que a especificação não
apenas armazena conhecimento. Ela determina recorte, estados, passagens e
evidências, coordenando participantes sem criar um chefe entre eles. Tornar
essa função explícita reduz interpretações concorrentes entre documentos,
prompts, automações e implementação.

**Compatibilidade:** registros EKM 1.x permanecem históricos. Os identificadores
`EKM-CHG` e `EKM-GAP` continuam aceitos em projetos adotantes; novos projetos
podem usar `EKOM-CHG` e `EKOM-GAP`, conforme o namespace declarado no mapa.

**Registro completo:**
[`ADR-0001 — Evolução de EKM para EKOM`](adr/ADR-0001-EKM-TO-EKOM.md).

## DD-032 — A versão normativa é integral e atômica para os atores

**Problema observado:** ao receber uma ordem que identificava o papel
Engenheiro Analista e `IOTSSC-BINARY-COMMAND-STATE@0.5`, um executor recusou a
etapa porque o prompt não repetia o resultado `Implementable` ou `Needs
Clarification` nem declarava recorte. A especificação estava `Proposed` e
`Pending Review`, de modo que perfil, objeto e estado já determinavam
inequivocamente o resultado canônico. Exigir os campos repetidos fez o prompt
competir com a função de orquestração da especificação.

**Decisão:** no ciclo funcional, papel e especificação formam a ordem mínima. O
perfil e o estado vigente determinam o resultado canônico da etapa. Ausência de
resultado repetido ou de recorte adicional não bloqueia a entrada.

Cada versão normativa é a unidade integral e atômica dos resultados formais. Se
a ordem indicar um recorte, ele é interpretado como foco adicional de atenção,
prioridade ou profundidade; não exclui requisitos, critérios, decisões, falhas,
relações ou gates da mesma versão.

Uma atuação parcial continua permitida quando explicitamente ordenada como
diagnóstico, investigação ou execução parcial. Ela não produz promoção formal
representativa da versão inteira. O Autor permanece dependente de intenção,
objetivo ou mudança fornecida pelo Arquiteto, e o Consultor permanece sujeito à
entrada explícita de seu perfil transversal.

**Aplicação por ator:**

- o Autor reconcilia a versão inteira mesmo quando a intenção altera apenas um
  ponto;
- o Analista confronta a totalidade da versão antes de declarar
  `Implementable` ou `Needs Clarification`; um primeiro bloqueio não pode
  ocultar outros conflitos materiais do mesmo contrato;
- o Implementador responde por todos os requisitos e critérios obrigatórios;
  trabalho parcial permanece `In Progress`;
- o Revisor cobre a versão inteira antes de sustentar promoção global; risco
  regula profundidade e evidência, não cobertura normativa.

**Proporcionalidade:** integralidade não exige matriz universal, documento
monolítico, mesma profundidade para todo risco ou leitura indiscriminada do
repositório. Especificações continuam incrementais e relacionadas; apenas não
podem ser subdivididas silenciosamente dentro de uma promoção formal.

**Alternativas rejeitadas:**

- exigir que toda ordem repita resultado e recorte foi rejeitado por duplicar
  informação já determinada pelo perfil, estado e especificação;
- permitir análise formal parcial foi rejeitado porque uma conclusão global
  poderia ignorar requisitos não confrontados;
- tratar recorte explícito como exclusão foi rejeitado porque transforma foco
  operacional em redução normativa concorrente;
- proibir qualquer trabalho parcial foi rejeitado porque diagnóstico e
  investigação localizada continuam úteis quando não promovem estado global.

**Critérios de reavaliação:** revisar a regra se atores não conseguirem inferir
o resultado canônico a partir do perfil e do estado, se a integralidade induzir
leitura indiscriminada sem ganho ou se focos adicionais deixarem de orientar
adequadamente tarefas de alto risco.

**Estado da decisão:** confirmada pelo Arquiteto para incorporação ao EKOM 2.1.

### Registro da atuação EKOM 2.1

**Estado da confirmação final:** Confirmada pelo Arquiteto.

- **Papel exercido:** Consultor de Arquitetura e par do Arquiteto.
- **Ordem autorizada:** tornar a versão normativa integral a unidade padrão dos
  atores e remover a exigência redundante de resultado e recorte explícitos no
  ciclo funcional.
- **Repositório e recorte:** `EKM-guidelines`; método, regras comuns, perfis dos
  quatro atores, princípios, conceito, glossário, templates, navegação, versão
  do modelo e decisão de desenho.
- **Operações autorizadas:** investigar as fontes vigentes, editar governança e
  templates, validar consistência e, após confirmação final, criar commit e
  realizar push.
- **Decisões confirmadas:** papel e especificação acionam o resultado canônico;
  ausência de recorte significa versão integral; recorte explícito é foco
  adicional; atuação parcial não promove estado global; Autor e Consultor
  preservam suas entradas específicas.
- **Resultado material preparado:** EKOM 2.1 com atomicidade operacional,
  cobertura integral distribuída pelos atores e comando mínimo simplificado.
- **Validações e limitações:** integridade do diff, referências de versão e
  ausência das regras operacionais contraditórias verificadas; nenhuma
  validação funcional se aplica à mudança documental. A eficácia será observada
  em novas execuções. O Consultor participou da solução e não pode alegar
  revisão independente dela.
- **Significado da confirmação final:** o registro representa a decisão e o
  EKOM 2.1 permanece vigente. A ordem posterior de promoção autoriza sua
  integração à `main`; não declara eficácia universal, adoção automática por
  projetos existentes, release ou deploy.

## DD-033 — EKOM 3.0 preserva execução delegada e devolve julgamento ao Arquiteto

**Problema observado:** os experimentos produziram implementações geralmente
funcionais sem desenvolvimento direto pelo Arquiteto, mas a sequência universal
de quatro atores gerou handoffs, disputas sobre testes e riscos teóricos e
pretensão de independência sem ganho funcional proporcional. Testes verdes e
revisão por agente semelhante não provaram correção.

**Decisão:** adotar o
[`ADR-0002`](adr/ADR-0002-EKOM-3-OPERATIONAL-AUTHORITY.md) e promover o modelo
para EKOM 3.0.

- a especificação governa a execução;
- o Arquiteto mantém decisões, risco, validação e conclusão;
- análise de implementabilidade continua obrigatória, mas pode ser realizada
  pelo Autor ou por capacidade especializada;
- Crítico/Revisor torna-se challenge consultivo acionado por risco ou ordem;
- testes são evidências proporcionais, não prova absoluta;
- evidência de ambiente real pode prevalecer na aceitação funcional;
- somente o Arquiteto conclui ou reabre o workflow;
- autonomia completa permanece horizonte, não capacidade atual.

**Hipóteses sustentadas:** execução amplamente delegada, especificação como
coordenação, preservação do Arquiteto como autoridade, conclusão funcional sem
desenvolvimento direto, valor do ambiente real e IA como ampliação da
investigação e execução.

**Hipóteses revisadas ou refutadas:** Revisor separado universal, Analista
obrigatoriamente separado, múltiplos agentes como independência, teste verde
como prova suficiente e autonomia completa como capacidade atual.

**Compatibilidade:** a decisão substitui a sequência operacional universal da
DD-023 e as promoções reservadas ao Revisor na DD-032. Perfis permanecem
disponíveis como capacidades acionáveis. Experimentos e registros anteriores
continuam válidos sob suas versões originais.

**Versionamento:** `major`, pois altera de forma incompatível o modelo de
atores, os gates e a autoridade de conclusão. Versão anterior: EKOM 2.1; versão
vigente: EKOM 3.0.

**Limitações:** julgamento humano continua necessário; evidência real pode ser
cara ou incompleta; risco elevado ainda pode exigir segregação e revisão
independente desenhada conscientemente.

**Estado da decisão:** confirmada pelo Arquiteto para incorporação ao EKOM 3.0.

## DD-034 — Responsabilidade documental exige destino operacional

**Problema observado:** a separação conceitual entre especificação, ADR e
relatório coexistia com um template que incorporava análise, implementação e
validação à própria especificação. Sem destinos e autoridade de escrita, o
experimento de variantes do IoTSmartLink15.4 acumulou histórico na fonte
normativa e elevou a carga cognitiva.

**Decisão:** adotar a
[`ADR-0003`](adr/ADR-0003-DOCUMENT-ROUTING-AND-EVIDENCE-SEPARATION.md) e promover
o modelo para EKOM 3.1. Especificação preserva contrato vigente; ADR, decisão
arquitetural durável; relatório, atuação; mapa, localização; changelog, estado
resumido; Git, linhagem. Templates e roteadores tornam essa separação
operacional.

**Proporcionalidade:** guardas automáticas cobrem apenas estrutura objetiva.
Necessidade semântica de ADR, suficiência de evidência e relevância de achado
continuam sob julgamento humano. Migração de conteúdo histórico é deliberada,
não automática.

**Estado da decisão:** confirmada pelo Arquiteto para incorporação ao EKOM 3.1;
a eficácia ainda será confrontada em novo experimento pequeno.

## DD-035 — O mapa combina autoridade, hierarquia e relações

**Problema observado:** o índice tabular do mapa localizava fontes, mas não
representava adequadamente composição e conexão entre alvos separados. No
IoTSmartLink15.4, árvore e diagrama permitiram compreender product firmware,
board, componentes, client e coordenador sem varredura ampla do repositório.

**Decisão:** adotar a
[`ADR-0004`](adr/ADR-0004-KNOWLEDGE-MAP-VISUAL-STRUCTURE.md) e promover o modelo
para EKOM 3.2. Tabela de autoridade é sempre obrigatória; árvore e Mermaid são
obrigatórios quando seus gatilhos materiais forem satisfeitos e explicitamente
não aplicáveis nos demais casos.

**Proporcionalidade:** visuais permanecem pequenos e navegacionais, não
duplicam contrato nem inventariam arquivos. A guarda verifica presença ou
justificativa; qualidade semântica continua sob julgamento humano.

**Estado da decisão:** confirmada pelo Arquiteto para incorporação normativa e
integração na `main` como EKOM 3.2; eficácia além do caso observado permanece
hipótese a confrontar.

## DD-036 — A autoria confronta autoridades antes da prontidão

**Problema observado:** na especificação de deep sleep do
`IoTSmartLink15.4`, fontes anteriores foram lidas, mas não confrontadas como
autoridades. A proposta recomendou prontidão enquanto alterava implicitamente
API pública, lifecycle e nomenclatura governados por especificações Active.

**Decisão:** adotar a
[`ADR-0005`](adr/ADR-0005-SPECIFICATION-AUTHORITY-CONFRONTATION.md) e promover o
modelo para EKOM 3.3. O Autor identifica os elementos afetados, localiza suas
autoridades, classifica as relações e devolve conflitos ao Arquiteto antes da
prontidão. A especificação registra relações vigentes; o relatório de análise,
a matriz detalhada. O Analista reconfronta ambas.

**Proporcionalidade:** o confronto é orientado por impacto, não leitura integral
do acervo. Uma mudança isolada pode produzir uma matriz mínima; a obrigação
cresce somente quando comportamento, API, estado, lifecycle, persistência,
compatibilidade, nome ou fronteira cruzarem autoridades.

**Estado da decisão:** confirmada pelo Arquiteto para incorporação ao EKOM 3.3;
sua eficácia na redução de retornos tardios permanece hipótese a confrontar.

## DD-037 — A funcionalidade não absorve pré-requisito arquitetural

**Problema observado:** o confronto de autoridade do EKOM 3.3 revelou
corretamente contratos afetados no deep sleep do `IoTSmartLink15.4`, mas não
impediu que sucessivos retornos fossem incorporados à mesma especificação. Uma
funcionalidade pequena passou a definir lifecycle, quiescência, encerramento e
arbitragem transversais. O resultado genérico de prontidão condicionada não
distinguia defeito funcional de baseline arquitetural insuficiente.

**Decisão:** adotar a
[`ADR-0006`](adr/ADR-0006-SPECIFICATION-SCOPE-AND-ARCHITECTURAL-PREREQUISITES.md)
e promover o modelo para EKOM 3.4. A análise classifica separadamente prontidão,
defeito da especificação, pré-requisito arquitetural, evidência requerida,
conflito de restrição e impacto não delimitado. Capacidade ausente, independente
e transversal bloqueia a funcionalidade e retorna ao Arquiteto para análise e
preparação arquitetural separadas.

**Proporcionalidade:** tocar componente compartilhado não cria automaticamente
outra especificação. A separação exige materialidade, capacidade com contrato
próprio ou impacto ainda desconhecido. Correções locais continuam no contrato
funcional.

**Estado da decisão:** confirmada pelo Arquiteto para incorporação ao EKOM 3.4;
a eficácia na redução de ciclos de análise permanece hipótese a confrontar.

### Registro da atuação EKOM 3.4

**Estado da confirmação final:** Confirmada pelo Arquiteto.

- **Papel exercido:** Consultor de Arquitetura.
- **Ordem autorizada:** incorporar limites de escopo funcional, classificação
  de inviabilidade no recorte e preparação arquitetural separada ao EKOM.
- **Repositório e recorte:** `EKM-guidelines`; regras comuns, perfis de Autor,
  Analista e Implementador, método, ADR, princípios, glossário, templates,
  prompts, diagramas e navegação afetados.
- **Operações autorizadas:** investigar fontes vigentes, editar a governança,
  validar consistência e, após confirmação final, criar commit e realizar push
  na branch de trabalho.
- **Decisões confirmadas:** promover o modelo para EKOM 3.4; tornar obrigatória
  a taxonomia de implementabilidade; bloquear funcionalidade que dependa de
  capacidade arquitetural ausente, independente e transversal; separar análise
  e especificação preparatória por decisão do Arquiteto.
- **Resultado material produzido:** ADR-0006, DD-037, teste de fronteira,
  relações `Depends On` e `Enables`, campos obrigatórios no relatório e
  roteamento operacional entre defeito funcional, evidência, preparação,
  conflito de restrição e impacto não delimitado.
- **Validações e limitações:** integridade do diff e guarda documental
  verificadas; mudança exclusivamente documental; eficácia depende de novas
  atuações. O Consultor participou da formulação e não alega revisão
  independente.
- **Significado da confirmação final:** confirmar a formulação como EKOM 3.4 e
  autorizar commit e push na branch atual. A confirmação não autoriza merge,
  release, adoção automática por projetos existentes nem declara eficácia
  comprovada.

## DD-039 — Build canônico integra a implementação autorizada

**Problema observado:** ao promover a v0.11 de deep sleep do
`IoTSmartLink15.4`, a especificação ainda agrupava build, testes e hardware como
operações não autorizadas. O Arquiteto precisou esclarecer depois da promoção
que build deve ser executado na implementação e que somente testes e operações
físicas permanecem dependentes de autorização própria.

**Decisão:** adotar a
[`ADR-0008`](adr/ADR-0008-BUILD-INTRINSIC-TO-IMPLEMENTATION.md) e promover o
modelo para EKOM 3.6. Autorização de implementação de artefato construível
inclui e exige build canônico proporcional dos entregáveis afetados. A
especificação funcional não repete essa permissão; fontes locais determinam
comandos, targets e configurações. Testes, hardware, deploy e operações
externas não são inferidos do build.

**Proporcionalidade:** mudança documental ou contexto sem artefato construível
não recebe comando artificial. O conjunto de builds segue o delta e os
consumidores materiais, não uma matriz universal. Comando híbrido deve separar
o build ou pedir autorização adicional.

**Estado da decisão:** confirmada pelo Arquiteto para formulação no EKOM 3.6; a
eficácia será observada em novas implementações.

### Registro da atuação EKOM 3.6

- **Capacidade:** Consultor de Arquitetura.
- **Ordem:** tornar o build obrigação normativa transversal da EKOM, sem
  repeti-lo como autorização da especificação funcional.
- **Recorte:** regras comuns, perfil do Implementador, método, princípios,
  glossário, governança, templates, ADR-0008 e adoção local pelo
  `IoTSmartLink15.4`.
- **Decisão confirmada:** implementação autorizada de artefato construível
  inclui e exige build canônico proporcional; execução de testes, hardware e
  operações externas conserva autorização própria.
- **Resultado material:** EKOM promovido para 3.6; especificação de deep sleep
  reconciliada para não autorizar nem proibir o build ordinário.
- **Validação e limites:** guardas documentais aprovadas nos dois repositórios;
  nenhuma construção, execução de teste ou operação em hardware integrou esta
  atuação documental. A eficácia operacional permanece hipótese futura.
- **Confirmação final:** concedida pelo Arquiteto em 2026-08-12 para registrar,
  commitar e enviar os branches correntes dos dois repositórios. Não constitui
  autorização de implementação da v0.11, testes, hardware, merge, release ou
  deploy.

## DD-038 — Ordem de implementação não satisfaz gates ausentes

**Problema observado:** um executor recebeu ordem para implementar uma versão
em `Draft`, reconheceu que faltavam análise e promoção, mas decidiu prosseguir
e registrar o desvio porque “a ordem prevalece”. O Arquiteto interrompeu a
execução e desfez as alterações.

**Decisão:** adotar a
[`ADR-0007`](adr/ADR-0007-NON-IMPLICIT-IMPLEMENTATION-GATES.md) e promover o
modelo para EKOM 3.5. Análise `Ready`, promoção registrada para Pronta e
autorização da mesma versão são gates cumulativos. Ordem de implementação não
substitui os dois primeiros; ausência obriga recusa sem mutação e orientação da
próxima etapa.

**Proporcionalidade:** diagnóstico e experimento em `Draft` continuam possíveis
quando explicitamente nomeados e limitados, mas não representam implementação
normativa nem promovem estado.

**Estado da decisão:** confirmada pelo Arquiteto para formulação no EKOM 3.5; a
eficácia será testada repetindo a ordem que originou o caso.

### Registro da atuação EKOM 3.5

**Estado da confirmação final:** Confirmada pelo Arquiteto.

- **Papel exercido:** Consultor de Arquitetura.
- **Ordem autorizada:** tornar obrigatória a recusa da implementação quando a
  especificação ainda não tiver satisfeito todos os gates de entrada.
- **Repositório e recorte:** `EKM-guidelines`; regras comuns, perfil do
  Implementador, método, ADR, princípios, glossário, templates, prompts,
  diagramas e navegação afetados.
- **Operações autorizadas:** investigar o caso observado, editar a governança,
  validar consistência e, após confirmação final, criar commit e realizar push
  na branch de trabalho.
- **Decisões confirmadas:** promover o modelo para EKOM 3.5; tratar análise
  `Ready`, promoção registrada e autorização da mesma versão como gates
  cumulativos; proibir promoção implícita e regularização posterior por
  relatório; exigir recusa sem mutação e indicação da próxima etapa.
- **Resultado material produzido:** ADR-0007, DD-038, resposta canônica de
  recusa, campos explícitos no template de especificação e roteamento visual
  entre análise, promoção, autorização e implementação.
- **Validações e limitações:** integridade do diff e guarda documental
  verificadas; mudança exclusivamente documental; eficácia depende da repetição
  da ordem contra uma especificação em `Draft`. O Consultor participou da
  formulação e não alega revisão independente.
- **Significado da confirmação final:** confirmar a formulação como EKOM 3.5 e
  autorizar commit e push na branch atual. A confirmação não autoriza merge,
  release, adoção automática por projetos existentes nem declara eficácia
  comprovada.

## DD-039 — Quatro estágios e uma decisão por passagem

**Problema observado:** os três gates do EKOM 3.5 impediram implementação
prematura, mas obrigaram o Arquiteto a repetir a mesma intenção como análise
`Ready`, promoção para Pronta, campo de autorização e ordem. Em uma
especificação já analisada e promovida, o Implementador recusou corretamente a
ordem porque faltava apenas o registro documental da autorização. O controle
era seguro, porém confundia estados com etapas e não acrescentava decisão.

**Decisão:** adotar a
[`ADR-0009`](adr/ADR-0009-FOUR-STAGE-WORKFLOW.md) e promover o modelo para EKOM
4.0. O fluxo oficial possui Autoria, Análise de Implementabilidade,
Implementação e Revisão. Para entrar em Implementação bastam `Ready` aplicável
à versão corrente e ordem explícita do Arquiteto para implementá-la. A ordem é
a aprovação da passagem; `In Progress` é registrado pelo Implementador como
efeito, não como precondição.

**Limites preservados:** mudança normativa posterior invalida o `Ready`;
análise não pronta retorna à Autoria; pré-requisito arquitetural nasce em
especificação preparatória; build é intrínseco à Implementação; testes,
hardware, deploy e operações externas conservam permissão própria. Revisão é
obrigatória como estágio, com profundidade e independência proporcionais ao
risco. Somente o Arquiteto decide `Done`, reabertura e integração.

**Estado da decisão:** confirmada pelo Arquiteto em 2026-08-12 para tornar o
fluxo simplificado vigente. A eficácia será medida pela redução de paradas
administrativas sem implementação de versões não analisadas.

### Registro da atuação EKOM 4.0

- **Capacidade:** Consultor de Arquitetura.
- **Ordem:** incorporar e tornar vigente o workflow simplificado em quatro
  estágios.
- **Recorte:** regras comuns, perfis, método, princípios, glossário,
  governança, templates, diagramas, ADRs, decisões de desenho e histórico
  experimental do repositório central `EKM-guidelines`.
- **Decisões confirmadas:** `Ready` da versão corrente e ordem explícita do
  Arquiteto iniciam a Implementação; não existe promoção nem autorização
  documental intermediária; build permanece intrínseco; testes, hardware e
  operações externas conservam permissão própria; Revisão é o quarto estágio.
- **Resultado material:** ADR-0009 aceita, ADR-0007 substituída e modelo
  promovido para EKOM 4.0 nas fontes vigentes e reutilizáveis.
- **Validação e limites:** guarda documental e integridade do diff aprovadas;
  mudança exclusivamente documental. O Consultor participou da formulação e
  não alega revisão independente. A eficácia operacional ainda será observada.
- **Confirmação final:** concedida pelo Arquiteto em 2026-08-12 para registrar,
  commitar e enviar a branch corrente. Não autoriza merge, release, adoção
  automática por projetos existentes nem operação externa adicional.

## DD-040 — Testes só entram no recorte por decisão da especificação

**Problema observado:** a regra de atualizar “código, testes e conhecimento
afetado” permitia ao Implementador criar várias suítes por iniciativa própria.
Embora executar testes exigisse autorização, sua criação já aumentava o volume
de código, manutenção e oráculos derivados sem decisão normativa equivalente.

**Decisão:** adotar a
[`ADR-0010`](adr/ADR-0010-SPECIFICATION-DRIVEN-TESTS.md) e promover o modelo para
EKOM 4.1. Criar, ampliar, reestruturar ou corrigir testes só integra a
Implementação quando a especificação corrente o exige explicitamente e o
vincula a requisito ou critério de aceite, cenário, resultado e meio. Menção
genérica a qualidade, cobertura, regressão ou validação proporcional não
autoriza teste.

**Fronteira operacional:** criar teste contratado não autoriza executá-lo.
Inspeção do delta e build canônico permanecem intrínsecos; outras validações só
são implementadas quando exigidas pela especificação e executadas quando
cobertas pela permissão aplicável. Teste existente fora do recorte que quebrar
é impacto registrado, não autorização implícita para corrigi-lo.

**Estado da decisão:** confirmada pelo Arquiteto em 2026-08-12. A eficácia será
avaliada pela redução de testes sem vínculo normativo, sem ocultar consumidores
afetados nem converter ausência de execução em sucesso.

### Registro da atuação EKOM 4.1

- **Capacidade:** Consultor de Arquitetura.
- **Ordem:** restringir criação e alteração de testes à exigência explícita da
  especificação e limitar execução de validações às permissões operacionais.
- **Recorte:** regras comuns, perfis, método, princípios, glossário,
  governança, templates, prompts, navegação, histórico, diagrama e ADR do
  repositório central `EKM-guidelines`.
- **Decisões confirmadas:** somente teste contratado integra a implementação;
  criação não autoriza execução; build permanece intrínseco; teste fora do
  recorte que quebrar é impacto a registrar, não correção implícita.
- **Resultado material:** ADR-0010 aceita e modelo promovido para EKOM 4.1 nas
  fontes vigentes e reutilizáveis.
- **Validação e limites:** guarda documental e integridade do diff aprovadas;
  mudança exclusivamente documental no EKOM central. A especificação e a
  implementação correntes do projeto consumidor não foram alteradas. O
  Consultor participou da formulação e não alega revisão independente.
- **Confirmação final:** concedida pelo Arquiteto em 2026-08-12 para registrar,
  commitar e enviar a branch corrente. Não autoriza merge, release, adoção
  automática em projetos consumidores nem operação externa adicional.

## DD-041 — Entrega Git faz parte da atuação material

**Problema observado:** regras que exigiam push “quando autorizado” e uma
confirmação final no perfil do Consultor faziam agentes concluir alterações e
parar antes de commit ou push. A confirmação repetia a autorização inicial e
deixava árvore suja ou branch local não sincronizada sem produzir decisão nova.

**Decisão:** adotar a
[`ADR-0011`](adr/ADR-0011-INTRINSIC-GIT-DELIVERY.md) e promover o modelo para
EKOM 4.2. Toda atuação autorizada que produza mudança material inclui commit e
push da branch corrente e termina com árvore limpa, sem confirmação final
adicional. Atuação somente leitura não cria commit e proibição explícita do
Arquiteto prevalece.

**Fronteira operacional:** a autorização não alcança force push, reescrita de
histórico, merge, tag, release, deploy, exclusão de branch, outro destino ou
mudança alheia ao recorte. Falha do remoto é registrada sem alegar
sincronização. Alterações preexistentes são preservadas e nunca absorvidas para
fabricar limpeza.

**Estado da decisão:** confirmada pelo Arquiteto em 2026-08-12. A eficácia será
avaliada pela ausência de novas paradas administrativas entre resultado
material pronto e entrega da branch, sem aumento de operações Git indevidas.

### Registro da atuação EKOM 4.2

- **Capacidade:** Consultor de Arquitetura.
- **Ordem:** tornar commit, push e árvore limpa parte automática de todo
  trabalho material autorizado.
- **Recorte:** regras comuns, perfil do Consultor, método, princípios,
  glossário, governança, templates, prompts, navegação, decisão e histórico do
  repositório central `EKM-guidelines`.
- **Decisões confirmadas:** entrega Git normal não cria gate final; atuação
  somente leitura não cria commit; proibição explícita prevalece; operações de
  integração, publicação e reescrita continuam fora do recorte implícito.
- **Resultado material:** ADR-0011 aceita e modelo promovido para EKOM 4.2 nas
  fontes vigentes e reutilizáveis.
- **Validação e limites:** mudança exclusivamente documental; o Consultor
  participou da formulação e não alega revisão independente. A eficácia
  operacional será observada em atuações futuras.

## DD-042 — A especificação determina a branch de trabalho

**Problema observado:** o piloto n8n solicitava `working_branch` ao submeter uma
especificação. O campo adicionava linguagem operacional à autoria, permitia
divergência entre documento e branch e dificultava gatilhos futuros por commit.

**Decisão:** adotar a
[`ADR-0012`](adr/ADR-0012-SPECIFICATION-DERIVED-BRANCH.md) e promover o modelo
para EKOM 4.3. O nome do documento em `docs/specs/` determina uma branch
`spec/<slug>` previsível. Colisão ou ausência de uma especificação coordenadora
retorna ao Arquiteto em vez de gerar nome alternativo silencioso.

**Estado da decisão:** confirmada pelo Arquiteto em 2026-08-13 para incorporação
e promoção na `main` como regra vigente.

### Registro da atuação EKOM 4.3

- **Capacidade:** Consultor de Arquitetura.
- **Ordem:** padronizar branches pelo nome da especificação e promover a versão
  local para a `main` vigente.
- **Recorte:** método, princípios, governança, templates, navegação, decisão e
  histórico do repositório central `EKM-guidelines`.
- **Resultado material:** ADR-0012 aceita e convenção operacional incorporada
  ao EKOM 4.3.
- **Validação e limites:** mudança documental; não altera automaticamente
  branches existentes nem autoriza criação, análise, merge ou publicação fora
  da entrega explicitamente ordenada.

## DD-043 — Débito técnico tem identidade e guarda próprias

**Problema observado:** o EKOM preservava lacunas, desvios, riscos residuais e
transações, mas não distinguia a postergação consciente de uma condição técnica
conhecida. No piloto IoTSmartLink15.4, essa necessidade mostrou que usar
`EKOM-GAP` confundiria conhecimento ausente com compromisso conhecido, enquanto
manter o achado apenas em relatório não garantiria reavaliação ou quitação.

**Decisão:** adotar a
[`ADR-0013`](adr/ADR-0013-TECHNICAL-DEBT.md) e promover o modelo para EKOM 4.4.
`EKOM-DEBT-NNNN` identifica condição conhecida cuja correção foi postergada por
decisão explícita do Arquiteto. O mapa mantém condição, alcance, evidência,
consequência, decisão, gatilho ou critério de quitação e relações materiais.

**Fronteira operacional:** agentes podem descobrir e relatar candidatos, mas
não aceitam dívida nem determinam quitação. Aceitar débito não altera evidência,
não torna conforme uma violação normativa e não cria autorização implícita para
remediação. A correção usa `EKOM-CHG` e o workflow aplicável. Prazo, prioridade e
estimativa permanecem opcionais; não surge estágio ou backlog universal.

**Estado da decisão:** confirmada pelo Arquiteto em 2026-08-14. A eficácia será
avaliada pela capacidade de localizar, reavaliar e quitar postergações reais sem
converter todo defeito, risco ou lacuna em dívida.

### Registro da atuação EKOM 4.4

- **Capacidade:** Consultor de Arquitetura.
- **Ordem:** normatizar débito técnico, consolidar na branch de evolução vigente
  e promover o resultado para `main`, mantendo a major 4.
- **Recorte:** método, princípios, glossário, regras comuns, governança,
  templates, navegação, ADR e registro de decisões do repositório central.
- **Decisões confirmadas:** dívida é postergação consciente; `GAP` permanece
  conhecimento ausente; somente o Arquiteto aceita e quita; evidência e
  conformidade não são alteradas pela aceitação; remediação usa transação.
- **Resultado material:** ADR-0013 aceita e modelo EKOM 4.4 vigente nas
  fontes e templates reutilizáveis.
- **Validação e limites:** guarda documental, template do mapa e integridade do
  diff aprovados; mudança exclusivamente documental. O Consultor participou da
  formulação e não alega revisão independente. A eficácia será observada em
  casos reais de registro e remediação.
- **Confirmação final:** concedida pelo Arquiteto em 2026-08-14 para consolidar
  a decisão na branch corrente, promovê-la à `main` e torná-la vigente sem sair
  da major 4. Não autoriza release, deploy ou operação externa adicional.

## DD-044 — Prontidão de implementação usa suficiência, não exaustão

**Problema observado:** no piloto da capability de bateria do
`IoTSmartLink15.4`, a análise continuou produzindo bloqueios depois de o escopo,
as relações normativas e os débitos técnicos terem sido delimitados. Escolhas
locais de implementação e evidências próprias da execução foram tratadas como
lacunas da especificação, criando retorno potencialmente ilimitado à Autoria.

**Hipótese experimental:** uma especificação está pronta quando existe ao menos
uma implementação tecnicamente plausível e conforme dentro da baseline e do
recorte. Solução interna completa, escolha antecipada entre alternativas locais
e evidência produzível durante Implementação ou Revisão não são condições de
prontidão.

**Limite de bloqueio:** somente impossibilidade ou conflito, decisão normativa
ausente, pré-requisito arquitetural independente, impacto material não
delimitado ou evidência prévia indispensável para decidir se qualquer solução
conforme é possível impedem `Ready`.

**Autoridade limitada:** uma fonte governa somente comportamentos, garantias e
restrições explicitamente contratados. Título, domínio, arquivo, classe,
fachada, componente, dependência ou inventário não concedem autoridade sobre
extensões futuras. Listas são abertas salvo declaração normativa inequívoca de
exaustividade; extensão aditiva pode governar seu próprio contrato.

**Teste causal fechado:** fonte anterior só bloqueia quando coexistem requisito
anterior explícito e aplicável, requisito novo necessariamente incompatível,
conflito inevitável independentemente da escolha técnica e ausência de
implementação conforme no recorte. O Analista não exige prova de ausência de
regressão, não cria experimento para procurar justificativa de bloqueio e não
converte risco hipotético em defeito.

**Controle contra omissão:** objetividade limita a saída, não a cobertura. A
análise confronta requisitos, critérios e débitos; dispõe todo bloqueador
anterior; preserva até cinco restrições materiais não bloqueantes; e executa
challenge limitado antes de `Ready`. Critério que exige remediação postergada ou
fora do recorte permanece bloqueante. Parecer não persistido é consultivo e não
conclui o estágio formal.

**Síntese operacional em 2026-08-15:** o experimento mostrou que declarar
objetividade sem reduzir o template produz relatório extenso. O relatório passa
a ter cinco blocos, máximo de 800 palavras e proibição de repetir contrato,
antecipar implementação, sugerir correção ou listar próximos passos. Cada
execução cria arquivo novo, imutável e identificável por UTC, revisão e ID da
execução; o delta deve registrá-lo como adição.

**Estado da decisão:** confirmada pelo Arquiteto em 2026-08-15 e incorporada ao
EKOM 4.5. O experimento da bateria descartou bloqueios por autoridade adjacente
e por escolhas locais, mas uma primeira execução `Ready` omitiu um critério
internamente insatisfazível. Os controles de cobertura, reconciliação e
challenge foram então acrescentados; duas análises independentes convergiram no
único bloqueador material, a especificação foi corrigida e a v0.5 chegou a
`Ready`, implementação aderente e validação aceitável em hardware.

### Registro da atuação EKOM 4.5

- **Capacidade:** Consultor de Arquitetura.
- **Ordem:** registrar o experimento, incorporar os limites de prontidão e
  promover a EKOM para `main` e estado vigente sem alterar a major 4.
- **Recorte:** conceito, método, princípios, glossário, regras comuns, perfis,
  templates, validação documental, navegação, histórico e decisão arquitetural
  do repositório central.
- **Resultado material:** ADR-0014 aceita e EKOM 4.5 vigente, com teste de
  suficiência, autoridade limitada, controle contra omissão e relatório curto e
  imutável.
- **Validação e limites:** o caso sustenta utilidade no recorte simples a médio
  observado, não eficácia universal. A primeira falsa classificação `Ready` é
  preservada como evidência de que concisão sem controle pode ocultar defeitos.
- **Confirmação final:** concedida pelo Arquiteto em 2026-08-15 para registrar,
  promover à `main` e tornar vigente. Não autoriza release, deploy nem adoção
  automática por repositórios consumidores.

## DD-045 — A autoria confirma o rascunho antes do registro normativo

**Problema observado:** escrever imediatamente o arquivo da especificação
transferia ambiguidades de intenção para a fonte normativa e produzia
retrabalho. No extremo oposto, explorar todo o código antes de conversar com o
Arquiteto elevava custo e latência sem garantia proporcional de qualidade.

**Evidência:** no experimento `Client-SDK-Configurable-Features` do
`IoTSmartLink15.4`, a consulta prévia ao mapa, especificações e ADRs, combinada
com inspeção dirigida do código, revelou antes da escrita as duas temporizações
de deep sleep, o intervalo próprio da bateria sem deep sleep, a fronteira entre
GPIO configurável e board model, a ordem da primeira medição após o boot e um
débito fora do recorte. As decisões foram reconciliadas em um rascunho aprovado
antes da criação da especificação. A análise formal posterior confrontou 25
requisitos, 12 critérios e um débito relacionado sem encontrar lacuna ou
bloqueador.

**Decisão:** para especificação nova ou revisão material, o Autor consulta
primeiro as fontes de conhecimento aplicáveis, explora o código apenas para
resolver dúvidas materiais e apresenta ao Arquiteto um rascunho funcional
conciso. O rascunho explicita comportamento, defaults, dependências, escopo,
fontes relacionadas, decisões e perguntas que alterem contrato, arquitetura ou
alcance. Respostas são reconciliadas antes do registro normativo.

**Fronteira operacional:** o rascunho é conversacional e provisório; não é
especificação, relatório nem substituto da análise de implementabilidade.
Pergunta, consulta sobre o próximo passo ou concordância com o conteúdo não
autoriza mutação. Criar ou alterar a especificação exige ordem explícita do
Arquiteto. Escolhas técnicas locais permanecem nos estágios posteriores.

**Proporcionalidade:** a investigação é orientada por conhecimento e impacto,
não por leitura universal do repositório. A regra busca antecipar decisões
materiais sem converter a Autoria em análise exaustiva ou desenho de
implementação.

**Estado da decisão:** confirmada pelo Arquiteto em 2026-08-18 e incorporada ao
EKOM 4.6 como evolução compatível da etapa de Autoria.

### Registro da atuação EKOM 4.6

- **Capacidade:** Consultor de Arquitetura.
- **Ordem:** incorporar o aprendizado do experimento ao perfil do Autor da
  Especificação e promovê-lo a vigente sem alterar a major 4.
- **Recorte:** perfil do Autor, versões vigentes do modelo, navegação, decisão
  de desenho e histórico experimental do repositório central. Nenhum template
  ou regra comum operacional foi criado.
- **Resultado material:** perfil do Autor 3.3 e EKOM 4.6 vigentes, com
  investigação dirigida, rascunho funcional, reconciliação humana e ordem
  explícita antes da escrita normativa.
- **Validação e limites:** mudança exclusivamente documental, sustentada por um
  caso de firmware com participação ativa do Arquiteto; não demonstra eficácia
  universal nem dispensa análise de implementabilidade.
- **Confirmação final:** concedida pelo Arquiteto em 2026-08-18 para registrar,
  promover à `main` e tornar vigente dentro da major 4. Não autoriza release,
  deploy nem adoção automática por repositórios consumidores.

## DD-046 — O Consultor pode executar implementação pequena sem especificação

**Problema observado:** o workflow completo orientado por especificação impõe
custo desproporcional quando o Arquiteto já delimitou uma alteração pequena,
local e de baixo risco.

**Decisão:** adotar a
[`ADR-0015`](adr/ADR-0015-SMALL-CONSULTANT-IMPLEMENTATION.md) e promover o
modelo para EKOM 4.7. Exclusivamente o Consultor de Arquitetura pode implementar
sem especificação quando o Arquiteto determinar explicitamente que a alteração
é pequena, ordenar essa via e delimitar objetivo, recorte e operações.

**Guardas:** ampliação material de arquitetura, contrato, dados, segurança,
protocolo, concorrência, operação, componentes, consumidores, escopo ou risco
torna a exceção inaplicável. O Consultor não implementa nem parcela trabalho
grande. Se estiver na `main`, cria antes uma branch derivada dela; ao final,
atualiza obrigatoriamente o mapa de conhecimento.

**Estado da decisão:** confirmada pelo Arquiteto em 2026-08-31 e incorporada ao
EKOM 4.7 como evolução compatível e proporcional.

## DD-047 — A adoção exige contrato de engenharia e qualificação do repositório

**Decisão:** incorporar a exigência determinada pelo Arquiteto em 2026-09-05,
conforme [ADR-0016](adr/ADR-0016-REPOSITORY-ENGINEERING-CONTRACT-READINESS.md).
EKOM 5.0 exige regras de construção explícitas aprovadas por humano e avaliação
de readiness antes de habilitar implementação, inclusive a via curta.
A especificação governa comportamento; contrato governa construção; precedentes
não substituem norma. A classificação do repositório não altera a da tarefa.

**Hipótese ainda não comprovada:** o controle reduz desvios e retrabalho com
custo proporcional. O [experimento planejado](experiments/REPOSITORY-READINESS-RUN-001.md)
fornece cenários positivos, negativos e medidas; não há resultado registrado.
A revisão é major pelo novo pré-requisito de adoção. Registros 4.x são preservados.

### Registro da promoção da EKOM 5.0

- **Decisão humana:** em 2026-09-22, o Arquiteto determinou promover a versão
  local 5.0 para a referência principal e colocá-la em vigência online.
- **Recorte:** consolidar as regras já registradas de contrato de engenharia,
  Repository Readiness, via curta do Consultor e proteção de informações
  sensíveis; alinhar a referência do modelo na métrica experimental dos atores.
- **Resultado normativo:** EKOM 5.0 aprovada e vigente como referência central,
  com ADR-0016 aceita e decisões anteriores preservadas.
- **Validações:** guarda estrutural documental aprovada; 121 referências locais
  dos documentos alterados verificadas; integridade do diff conferida. Não foi
  executado experimento de eficácia, nem se declara auditoria independente.
- **Limites:** a promoção não aprova contratos de repositórios adotantes, não
  certifica Repository Readiness de nenhum projeto e não migra consumidores
  automaticamente. Não inclui tag, release, deploy ou reescrita de histórico.

## DD-048 — Nenhuma informação sensível pode ser versionada

**Estado:** vigente, determinada pelo Arquiteto em 17/09/2026 como emenda à EKOM 5.0.

**Decisão humana:** incorporar imediatamente a proibição de versionar qualquer
informação sensível. A ordem expressa do Arquiteto aprova esta regra; não é
proposta pendente nem depende da aprovação de contratos de repositórios adotantes.

**Aplicação:** a seção 8.0 do método define alcance, conferência de commit/push,
exemplos sanitizados e tratamento de exposição anterior. Princípios, regras
comuns e templates de roteamento, contrato e adoção propagam a obrigação.
A regra limita a entrega Git e a preservação de evidências: nenhuma delas
justifica armazenar segredos ou dados confidenciais no histórico.

**Limites:** esta alteração documental não audita nem saneia históricos dos
adotantes, não instala scanners e não executa rotação de credenciais. Não há
alegação de detecção automática ou ausência de informação sensível no legado.
