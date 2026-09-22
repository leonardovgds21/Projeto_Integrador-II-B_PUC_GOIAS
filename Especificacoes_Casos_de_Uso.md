# Especificações de Casos de Uso

Este documento detalha, no formato de especificação de caso de uso, os 15 casos de uso apresentados no [Diagrama de Casos de Uso](README.md#diagrama-de-casos-de-uso) do projeto. Cada especificação está vinculada ao(s) requisito(s) funcional(is) (RF) correspondente(s) do [README.md](README.md).

## Índice de casos de uso

| ID | Caso de uso | Ator principal | Requisito(s) relacionado(s) |
|---|---|---|---|
| UC00 | Autenticar-se no Painel Administrativo | Administrador | — *(sem RF associado — ver observação abaixo)* |
| UC01 | Gerenciar Departamentos | Administrador | RF03 |
| UC02 | Gerenciar Atendentes | Administrador | RF04 |
| UC03 | Visualizar Dashboard de Atendimentos | Administrador | RF01 |
| UC03b | Filtrar por Período *(«extend» de UC03)* | Administrador | RF02 |
| UC04 | Monitorar Conversas dos Atendentes | Administrador | RF05 |
| UC05 | Configurar Chatbot | Administrador | RF06 |
| UC06 | Autenticar-se no Aplicativo | Atendente | RF07 |
| UC07 | Alterar Status de Disponibilidade | Atendente | RF08 |
| UC08 | Visualizar Atendimentos Direcionados | Atendente | RF09 |
| UC09 | Responder Cliente | Atendente | RF10, RF13 |
| UC10 | Encerrar Atendimento | Atendente | RF11 |
| UC11 | Marcar Atendimento como Aguardando Retorno | Atendente | RF12 |
| UC12 | Solicitar Atendimento via WhatsApp | Cliente | RF14, RF15, RF16, RF17, RF18 |
| UC13 | Registrar Histórico de Conversa *(«include»)* | Cliente / Atendente | RF19 |

> **Observação:** UC00 foi incluído no diagrama porque toda ação do administrador exige login prévio, mas não existe hoje um requisito funcional documentado para a autenticação do administrador (só o RF07 cobre a autenticação do atendente). Recomenda-se formalizar um RF20 — Autenticação do administrador para manter requisitos e diagrama coerentes.

---

## UC00 — Autenticar-se no Painel Administrativo

| Campo | Descrição |
|---|---|
| **Identificador único do caso de uso** | UC00 |
| **Descrição** | Permite que o administrador se autentique no sistema web por meio de login e senha antes de acessar qualquer funcionalidade do módulo administrativo. |
| **Ator principal** | Administrador |
| **Atores secundários** | — |
| **Pré-condições** | O administrador possui uma conta cadastrada no sistema. |
| **Gatilho** | O administrador acessa a tela de login do sistema web. |

**Fluxo principal**

| Ações do ator | Ações do sistema |
|---|---|
| 1. Acessa a URL do sistema web. | 1. Exibe a tela de login. |
| 2. Informa usuário e senha. | 2. Valida as credenciais informadas. |
| | 3. Autentica o administrador e exibe a tela inicial (dashboard). |

**Fluxo alternativo**

*Nenhum previsto.*

**Fluxo de exceção**

| Ações do ator | Ações do sistema |
|---|---|
| 1. Informa credenciais inválidas. | 1. Exibe a mensagem "usuário ou senha inválidos" e mantém a tela de login. |

**Pós-condição:** O administrador está autenticado e pode acessar as funcionalidades do módulo administrativo.

---

## UC01 — Gerenciar Departamentos

| Campo | Descrição |
|---|---|
| **Identificador único do caso de uso** | UC01 |
| **Descrição** | Permite ao administrador cadastrar, editar e excluir departamentos, utilizados para classificar e direcionar os atendimentos. |
| **Ator principal** | Administrador |
| **Atores secundários** | — |
| **Pré-condições** | Administrador autenticado (UC00). |
| **Gatilho** | Administrador acessa a área "Departamentos" do sistema web. |

**Fluxo principal (cadastrar)**

| Ações do ator | Ações do sistema |
|---|---|
| 1. Seleciona "Novo departamento". | 1. Exibe o formulário de cadastro. |
| 2. Informa o nome do departamento e confirma. | 2. Valida os dados e salva o novo departamento. |
| | 3. Exibe o departamento na lista, com mensagem de confirmação. |

**Fluxo alternativo**

| Ações do ator | Ações do sistema |
|---|---|
| A1. Seleciona um departamento e a opção "Editar", altera os dados e confirma. | A1. Valida e atualiza o departamento, exibindo confirmação. |
| A2. Seleciona um departamento e a opção "Excluir". | A2. Solicita confirmação da exclusão; após confirmar, remove o departamento e atualiza a lista. |

**Fluxo de exceção**

| Ações do ator | Ações do sistema |
|---|---|
| E1. Informa nome de departamento já existente. | E1. Exibe "departamento já cadastrado" e mantém o formulário aberto. |
| E2. Tenta excluir um departamento com atendentes vinculados. | E2. Impede a exclusão e informa que existem atendentes vinculados. |

**Pós-condição:** O departamento é criado, atualizado ou removido, refletindo no cadastro de atendentes (UC02) e no menu do chatbot (UC12).

---

## UC02 — Gerenciar Atendentes

| Campo | Descrição |
|---|---|
| **Identificador único do caso de uso** | UC02 |
| **Descrição** | Permite ao administrador cadastrar, editar e excluir atendentes, incluindo departamento de atuação e credenciais de acesso (login e senha) ao aplicativo mobile. |
| **Ator principal** | Administrador |
| **Atores secundários** | — |
| **Pré-condições** | Administrador autenticado (UC00); ao menos um departamento cadastrado (UC01). |
| **Gatilho** | Administrador acessa a área "Atendentes" do sistema web. |

**Fluxo principal (cadastrar)**

| Ações do ator | Ações do sistema |
|---|---|
| 1. Seleciona "Novo atendente". | 1. Exibe o formulário de cadastro (nome, departamento, login, senha). |
| 2. Preenche os dados e confirma. | 2. Valida os dados, cria a conta do atendente e o inclui na fila do departamento selecionado. |
| | 3. Exibe confirmação; o atendente passa a constar na lista. |

**Fluxo alternativo**

| Ações do ator | Ações do sistema |
|---|---|
| A1. Seleciona um atendente e "Editar", altera dados (ex.: departamento, senha) e confirma. | A1. Atualiza o cadastro do atendente. |
| A2. Seleciona um atendente e "Excluir", confirma. | A2. Remove o atendente da fila e do sistema. |

**Fluxo de exceção**

| Ações do ator | Ações do sistema |
|---|---|
| E1. Informa login já utilizado por outro atendente. | E1. Exibe "login já cadastrado" e mantém o formulário aberto. |
| E2. Tenta excluir atendente com atendimentos em aberto. | E2. Impede a exclusão e solicita o encerramento ou a transferência prévia dos atendimentos. |

**Pós-condição:** Atendente cadastrado, atualizado ou removido; apto a autenticar-se (UC06) e a entrar na fila de distribuição (UC12).

---

## UC03 — Visualizar Dashboard de Atendimentos

| Campo | Descrição |
|---|---|
| **Identificador único do caso de uso** | UC03 |
| **Descrição** | Permite ao administrador visualizar relatórios de atendimento por departamento e por atendente, incluindo quantidade de atendimentos, tempo de resposta entre mensagens e tempo entre início e encerramento do atendimento. |
| **Ator principal** | Administrador |
| **Atores secundários** | — |
| **Pré-condições** | Administrador autenticado (UC00). |
| **Gatilho** | Administrador acessa a tela "Dashboard". |

**Fluxo principal**

| Ações do ator | Ações do sistema |
|---|---|
| 1. Acessa o dashboard. | 1. Consulta os dados de atendimento do período padrão e exibe quantidade de atendimentos, tempo de resposta e tempo de encerramento, agrupados por departamento e por atendente. |
| | 2. Exibe os dados em gráficos/tabelas. |

**Fluxo alternativo**

| Ações do ator | Ações do sistema |
|---|---|
| A1. Solicita "Filtrar por período". | A1. Executa o caso de uso estendido UC03b — Filtrar por Período e atualiza os dados exibidos. |

**Fluxo de exceção**

| Ações do ator | Ações do sistema |
|---|---|
| E1. — | E1. Não há atendimentos no período exibido: sistema mostra "nenhum dado encontrado para o período selecionado". |

**Pós-condição:** Administrador visualiza os relatórios solicitados.

---

## UC03b — Filtrar por Período *(«extend» de UC03)*

| Campo | Descrição |
|---|---|
| **Identificador único do caso de uso** | UC03b |
| **Descrição** | Permite ao administrador refinar os dados exibidos no dashboard, selecionando um período em horas, dias ou meses. |
| **Ator principal** | Administrador |
| **Atores secundários** | — |
| **Pré-condições** | UC03 (Visualizar Dashboard) em execução. |
| **Gatilho** | Administrador seleciona a opção de filtro de período no dashboard. |

**Fluxo principal**

| Ações do ator | Ações do sistema |
|---|---|
| 1. Seleciona a unidade (horas, dias ou meses) e o intervalo desejado. | 1. Valida o intervalo informado. |
| 2. Confirma o filtro. | 2. Reconsulta os dados no período informado e atualiza o dashboard (UC03). |

**Fluxo alternativo**

*Nenhum previsto.*

**Fluxo de exceção**

| Ações do ator | Ações do sistema |
|---|---|
| E1. Informa um intervalo inválido (ex.: data final anterior à inicial). | E1. Exibe mensagem de erro e mantém o filtro anterior. |

**Pós-condição:** Dashboard atualizado com os dados do período filtrado.

---

## UC04 — Monitorar Conversas dos Atendentes

| Campo | Descrição |
|---|---|
| **Identificador único do caso de uso** | UC04 |
| **Descrição** | Permite ao administrador visualizar, em modo de leitura, as conversas de todos os atendentes. |
| **Ator principal** | Administrador |
| **Atores secundários** | — |
| **Pré-condições** | Administrador autenticado (UC00); existência de ao menos um atendimento em andamento ou finalizado. |
| **Gatilho** | Administrador acessa a área "Monitoramento de Conversas". |

**Fluxo principal**

| Ações do ator | Ações do sistema |
|---|---|
| 1. Acessa a lista de atendimentos. | 1. Exibe a lista de conversas de todos os atendentes, com departamento e status. |
| 2. Seleciona um atendimento. | 2. Exibe o histórico completo da conversa selecionada, em modo somente leitura. |

**Fluxo alternativo**

| Ações do ator | Ações do sistema |
|---|---|
| A1. Filtra a lista por departamento ou atendente. | A1. Exibe apenas as conversas correspondentes ao filtro. |

**Fluxo de exceção**

| Ações do ator | Ações do sistema |
|---|---|
| E1. — | E1. Não há atendimentos disponíveis: sistema exibe "nenhuma conversa encontrada". |

**Pós-condição:** Administrador visualiza a(s) conversa(s) consultada(s), sem alterá-las.

---

## UC05 — Configurar Chatbot

| Campo | Descrição |
|---|---|
| **Identificador único do caso de uso** | UC05 |
| **Descrição** | Permite ao administrador editar as mensagens padrão do menu do chatbot e criar, editar e excluir mensagens automáticas. |
| **Ator principal** | Administrador |
| **Atores secundários** | — |
| **Pré-condições** | Administrador autenticado (UC00). |
| **Gatilho** | Administrador acessa a área "Configurações do Chatbot". |

**Fluxo principal (editar mensagens do menu)**

| Ações do ator | Ações do sistema |
|---|---|
| 1. Seleciona "Mensagens do menu". | 1. Exibe as mensagens padrão atuais do menu. |
| 2. Edita o texto e confirma. | 2. Valida e salva a nova mensagem padrão. |

**Fluxo alternativo**

| Ações do ator | Ações do sistema |
|---|---|
| A1. Seleciona "Nova mensagem automática", define gatilho/conteúdo e confirma. | A1. Cria e ativa a mensagem automática. |
| A2. Seleciona uma mensagem automática existente, altera o conteúdo e confirma. | A2. Atualiza a mensagem. |
| A3. Seleciona uma mensagem automática e "Excluir", confirma. | A3. Remove a mensagem automática. |

**Fluxo de exceção**

| Ações do ator | Ações do sistema |
|---|---|
| E1. Tenta salvar mensagem (de menu ou automática) em branco. | E1. Exibe "o campo de mensagem não pode estar vazio" e mantém o formulário aberto. |

**Pós-condição:** As mensagens do menu e/ou automáticas ficam atualizadas e passam a ser utilizadas pelo chatbot (UC12).

---

## UC06 — Autenticar-se no Aplicativo

| Campo | Descrição |
|---|---|
| **Identificador único do caso de uso** | UC06 |
| **Descrição** | Permite que o atendente acesse o aplicativo mobile utilizando login e senha individuais cadastrados pelo administrador. |
| **Ator principal** | Atendente |
| **Atores secundários** | — |
| **Pré-condições** | Atendente previamente cadastrado pelo administrador (UC02). |
| **Gatilho** | Atendente abre o aplicativo mobile. |

**Fluxo principal**

| Ações do ator | Ações do sistema |
|---|---|
| 1. Informa login e senha. | 1. Valida as credenciais. |
| | 2. Autentica o atendente e exibe a tela de atendimentos direcionados (UC08). |

**Fluxo alternativo**

*Nenhum previsto.*

**Fluxo de exceção**

| Ações do ator | Ações do sistema |
|---|---|
| E1. Informa credenciais inválidas. | E1. Exibe "usuário ou senha inválidos" e mantém a tela de login. |

**Pós-condição:** Atendente autenticado e apto a utilizar as funcionalidades do aplicativo mobile.

---

## UC07 — Alterar Status de Disponibilidade

| Campo | Descrição |
|---|---|
| **Identificador único do caso de uso** | UC07 |
| **Descrição** | Permite que o atendente altere seu status entre disponível, ausente e offline, determinando se poderá receber novos atendimentos. |
| **Ator principal** | Atendente |
| **Atores secundários** | — |
| **Pré-condições** | Atendente autenticado (UC06). |
| **Gatilho** | Atendente seleciona a opção de status no aplicativo. |

**Fluxo principal**

| Ações do ator | Ações do sistema |
|---|---|
| 1. Seleciona o novo status (disponível, ausente ou offline). | 1. Atualiza o status do atendente. |
| | 2. Passa a considerar (ou não) o atendente na fila de distribuição de novos atendimentos (UC12), conforme o status definido. |

**Fluxo alternativo**

*Nenhum previsto.*

**Fluxo de exceção**

| Ações do ator | Ações do sistema |
|---|---|
| E1. Altera o status para "ausente"/"offline" com atendimentos em aberto. | E1. Mantém os atendimentos já direcionados ao atendente, apenas suspendendo o recebimento de novos atendimentos. |

**Pós-condição:** Status do atendente atualizado, refletindo na distribuição de novos atendimentos.

---

## UC08 — Visualizar Atendimentos Direcionados

| Campo | Descrição |
|---|---|
| **Identificador único do caso de uso** | UC08 |
| **Descrição** | Permite que o atendente visualize as conversas dos atendimentos direcionados exclusivamente a ele. |
| **Ator principal** | Atendente |
| **Atores secundários** | — |
| **Pré-condições** | Atendente autenticado (UC06). |
| **Gatilho** | Atendente acessa a tela inicial do aplicativo. |

**Fluxo principal**

| Ações do ator | Ações do sistema |
|---|---|
| 1. Acessa a lista de atendimentos. | 1. Exibe os atendimentos direcionados a ele, com status (em andamento, aguardando retorno). |
| 2. Seleciona um atendimento. | 2. Exibe o histórico da conversa selecionada. |

**Fluxo alternativo**

*Nenhum previsto.*

**Fluxo de exceção**

| Ações do ator | Ações do sistema |
|---|---|
| E1. — | E1. Não há atendimentos direcionados: sistema exibe "nenhum atendimento no momento". |

**Pós-condição:** Atendente visualiza os atendimentos e conversas sob sua responsabilidade.

---

## UC09 — Responder Cliente

| Campo | Descrição |
|---|---|
| **Identificador único do caso de uso** | UC09 |
| **Descrição** | Permite que o atendente responda às mensagens recebidas nos atendimentos direcionados a ele, dentro da janela de atendimento de 24 horas da API oficial do WhatsApp. |
| **Ator principal** | Atendente |
| **Atores secundários** | API Meta (WhatsApp) |
| **Pré-condições** | Atendente autenticado (UC06); atendimento direcionado ao atendente (UC08); atendimento não encerrado (UC10). |
| **Gatilho** | Cliente envia uma mensagem, ou atendente seleciona um atendimento em aberto para responder. |

**Fluxo principal**

| Ações do ator | Ações do sistema |
|---|---|
| 1. Seleciona o atendimento e digita a resposta. | 1. Valida se a última mensagem do cliente está dentro da janela de 24 horas. |
| 2. Envia a mensagem. | 2. Encaminha a mensagem à API Meta, que a entrega ao cliente pelo WhatsApp. |
| | 3. Registra a mensagem no histórico da conversa (**«include» UC13 — Registrar Histórico de Conversa**). |

**Fluxo alternativo**

*Nenhum previsto — o atendente não pode iniciar uma conversa; só pode responder mensagens já recebidas (RF13).*

**Fluxo de exceção**

| Ações do ator | Ações do sistema |
|---|---|
| E1. Tenta responder após a janela de 24h ter expirado. | E1. Bloqueia o envio da mensagem livre e informa que o cliente precisa enviar uma nova mensagem antes de uma nova resposta. |
| E2. — | E2. Falha de comunicação com a API Meta: sistema exibe erro de envio e mantém a mensagem como pendente para nova tentativa. |

**Pós-condição:** Mensagem enviada ao cliente e registrada no histórico do atendimento.

---

## UC10 — Encerrar Atendimento

| Campo | Descrição |
|---|---|
| **Identificador único do caso de uso** | UC10 |
| **Descrição** | Permite que o atendente encerre um atendimento, impedindo o envio de novas mensagens naquele atendimento. |
| **Ator principal** | Atendente |
| **Atores secundários** | — |
| **Pré-condições** | Atendente autenticado (UC06); atendimento em aberto direcionado ao atendente. |
| **Gatilho** | Atendente seleciona a opção "Encerrar atendimento". |

**Fluxo principal**

| Ações do ator | Ações do sistema |
|---|---|
| 1. Seleciona "Encerrar atendimento". | 1. Solicita confirmação. |
| 2. Confirma. | 2. Altera o status do atendimento para "encerrado" e bloqueia o envio de novas mensagens naquele atendimento. |

**Fluxo alternativo**

*Nenhum previsto.*

**Fluxo de exceção**

| Ações do ator | Ações do sistema |
|---|---|
| E1. Tenta enviar mensagem em atendimento já encerrado. | E1. Impede o envio e informa que o atendimento está encerrado. |

**Pós-condição:** Atendimento encerrado; deixa de estar associado como "em aberto" ao atendente.

---

## UC11 — Marcar Atendimento como Aguardando Retorno

| Campo | Descrição |
|---|---|
| **Identificador único do caso de uso** | UC11 |
| **Descrição** | Permite que o atendente altere o atendimento para o status "Aguardando retorno", mantendo-o aberto para posterior continuidade. |
| **Ator principal** | Atendente |
| **Atores secundários** | — |
| **Pré-condições** | Atendente autenticado (UC06); atendimento em aberto direcionado ao atendente. |
| **Gatilho** | Atendente seleciona a opção "Aguardando retorno". |

**Fluxo principal**

| Ações do ator | Ações do sistema |
|---|---|
| 1. Seleciona "Aguardando retorno". | 1. Altera o status do atendimento para "Aguardando retorno" e o mantém em aberto. |
| | 2. Mantém o atendimento associado ao mesmo atendente, sem novas mensagens até o retorno do cliente. |

**Fluxo alternativo**

*Nenhum previsto.*

**Fluxo de exceção**

*Nenhuma prevista.*

**Pós-condição:** Atendimento permanece em aberto, no status "Aguardando retorno", associado ao mesmo atendente.

---

## UC12 — Solicitar Atendimento via WhatsApp

| Campo | Descrição |
|---|---|
| **Identificador único do caso de uso** | UC12 |
| **Descrição** | Processo em que o cliente inicia contato pelo WhatsApp, seleciona um departamento no menu do chatbot e é encaminhado a um atendente disponível, conforme a fila de distribuição. |
| **Ator principal** | Cliente |
| **Atores secundários** | API Meta (WhatsApp) |
| **Pré-condições** | Ao menos um departamento e um atendente cadastrados (UC01, UC02); chatbot configurado (UC05). |
| **Gatilho** | Cliente envia uma mensagem para o número de WhatsApp da empresa. |

**Fluxo principal**

| Ações do ator | Ações do sistema |
|---|---|
| 1. Envia uma mensagem para a empresa. | 1. Recebe a mensagem via API Meta e apresenta o menu de departamentos. |
| 2. Seleciona um departamento válido. | 2. Identifica o atendente disponível no início da fila do departamento e encaminha o atendimento a ele. |
| | 3. Move o atendente para o final da fila do departamento. |
| | 4. Registra o atendimento e a conversa no histórico (**«include» UC13 — Registrar Histórico de Conversa**). |

**Fluxo alternativo**

| Ações do ator | Ações do sistema |
|---|---|
| A1. — | A1. Departamento selecionado sem atendente disponível (fila vazia): sistema transfere o atendimento para o atendente de outro departamento com a menor quantidade de atendimentos em fila. |

**Fluxo de exceção**

| Ações do ator | Ações do sistema |
|---|---|
| E1. Informa uma opção inválida no menu. | E1. Exibe "opção inválida" e reapresenta o menu; esse fluxo se repete a cada nova tentativa inválida. |
| E2. Atinge 5 tentativas inválidas consecutivas. | E2. Exibe "tentativas excedidas, tente novamente mais tarde" e encerra a interação. |

**Pós-condição:** Atendimento criado e direcionado a um atendente disponível, com a conversa registrada no histórico.

---

## UC13 — Registrar Histórico de Conversa *(«include»)*

| Campo | Descrição |
|---|---|
| **Identificador único do caso de uso** | UC13 |
| **Descrição** | Caso de uso incluído que armazena o histórico das conversas e o número de telefone dos clientes em banco de dados, acionado sempre que uma mensagem é trocada dentro de um atendimento. |
| **Ator principal** | Cliente / Atendente *(acionado indiretamente, por inclusão a partir de UC09 e UC12)* |
| **Atores secundários** | — |
| **Pré-condições** | Atendimento em andamento (originado por UC12) ou mensagem sendo enviada pelo atendente (UC09). |
| **Gatilho** | Envio ou recebimento de uma mensagem dentro de um atendimento. |

**Fluxo principal**

| Ações do ator | Ações do sistema |
|---|---|
| — *(caso de uso incluído; sem interação direta do ator)* | 1. Registra a mensagem, o número de telefone do cliente e o horário no histórico do atendimento, associando-o ao banco de dados. |

**Fluxo alternativo**

*Nenhum previsto.*

**Fluxo de exceção**

| Ações do ator | Ações do sistema |
|---|---|
| E1. — | E1. Falha na gravação no banco de dados: sistema registra a falha em log interno e sinaliza erro ao caso de uso que o incluiu (UC09 ou UC12), sem interromper o restante do fluxo de atendimento. |

**Pós-condição:** Mensagem e dados do cliente armazenados no histórico do atendimento.
