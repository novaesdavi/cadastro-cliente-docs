# PRD — Sistema de Cadastro de Novos Clientes

Status: Rascunho
Versão: 7 · Última atualização: 2026-11-02

## 1. Contexto e problema

A empresa precisa de um sistema para cadastrar novos clientes, com verificação do Backoffice antes de os dados chegarem às outras áreas, que os usam para criar contas, perfis de usuário e em outros produtos.

## 2. Objetivos e métricas de sucesso

- **Objetivo**: permitir que o setor de Cadastro registre novos clientes e que somente cadastros aceitos pelo Backoffice sejam enviados às demais áreas.
- **Métrica de sucesso**: o novo sistema é considerado bem-sucedido após 10 cadastros feitos pelo setor de Cadastro, aceitos pelo Backoffice e publicados no tópico. Conta como cadastro feito somente o cadastro aceito pelo Backoffice e publicado no tópico. Não há prazo para atingir os 10 cadastros.

## 3. Usuários e perfis

O sistema é acessado por usuários internos da empresa (colaboradores), com perfis de acesso diferentes. No documento, **usuário** é o colaborador que opera o sistema e **cliente** é a pessoa cadastrada. Há dois perfis:

| Perfil | Pode | Não pode |
|---|---|---|
| Setor de Cadastro | Consultar CPF antes de iniciar um cadastro; iniciar e preencher o cadastro de um novo cliente; salvar o processo em Rascunho; salvar a correção de um processo em Devolvido para correção, sem reenviar; enviar e reenviar o processo para o Backoffice; editar processos com status Rascunho ou Devolvido para correção; alterar o CPF enquanto o cliente estiver Novo; pedir a alteração de dados ou o cancelamento de um cliente Ativo sem processo aberto, informando o motivo; pedir o cancelamento de um cliente Ativo com processo em Devolvido para correção, informando o motivo; reabrir um cliente Cancelado sem processo aberto, informando o motivo; descartar o primeiro processo ou um pedido de alteração, de cancelamento ou de reabertura, em Rascunho ou Devolvido para correção; retomar ou descartar um rascunho do primeiro processo ou de pedido esquecido por outro usuário do setor; consultar a tela de status, inclusive por CPF, com todos os cadastros, de qualquer usuário do setor; abrir os dados cadastrais de um cliente; consultar o histórico de qualquer cadastro. | Iniciar um novo cadastro para um CPF que já tenha cliente; informar na edição um CPF de cliente Novo ou de qualquer cliente com processo aberto; alterar o CPF de um cliente Ativo ou de um cliente Cancelado reaberto; pedir cancelamento de um cliente Novo ou com processo em Enviado para Backoffice; abrir um segundo processo para um cliente com processo aberto, salvo o caso de cancelamento em Devolvido para correção; editar processos com status Enviado para Backoffice, Aceito e enviado para processamento ou Alterações Descartadas; devolver ou aceitar processos; cancelar um cliente Ativo sem a aceitação do Backoffice. |
| Backoffice | Consultar CPF; consultar a tela de status, inclusive por CPF, com a mesma visão dos cadastros do setor de Cadastro; ver a lista única de processos em Enviado para Backoffice; verificar e analisar qualquer processo dessa lista, sem atribuição; devolver para correção um processo com status Enviado para Backoffice, informando o motivo, que pode conter a orientação para cancelar; aceitar um processo com status Enviado para Backoffice; abrir os dados cadastrais de um cliente; consultar o histórico de qualquer cadastro. | Cadastrar novos clientes, inclusive a partir da consulta de CPF; alterar diretamente os dados de um cadastro (todo ajuste passa pela devolução ao setor de Cadastro); cancelar diretamente um cadastro; iniciar uma reabertura, que ele apenas avalia; devolver um processo com status Aceito e enviado para processamento; aceitar ou devolver um processo que o próprio usuário enviou. |

Um mesmo usuário pode ter os dois perfis, mas não pode aceitar nem devolver um processo que ele mesmo enviou, em qualquer envio daquele processo, não só no último.

Não há perfil de administrador neste sistema. A criação de usuários e a atribuição de perfis não são contempladas por este sistema.

## 4. Escopo

### 4.1 Dentro do escopo

- Aplicação web com autenticação.
- Perfis de acesso: setor de Cadastro e Backoffice.
- Consulta de CPF antes do início de um novo cadastro, nos cadastros do próprio sistema.
- Preenchimento do cadastro de novo cliente, com opção de salvar como rascunho.
- Envio do processo para verificação e análise do Backoffice.
- Devolução do processo para correção, com motivo, e reenvio após a correção.
- Aceite do processo pelo Backoffice e publicação em tópico para as outras áreas da empresa.
- Pedido de alteração de dados de um cliente Ativo, com motivo, avaliado pelo Backoffice.
- Pedido de cancelamento de um cliente Ativo, com motivo, avaliado pelo Backoffice.
- Pedido de reabertura de um cliente Cancelado, com motivo, avaliado pelo Backoffice.
- Descarte do primeiro processo ou de um pedido de alteração, de cancelamento ou de reabertura.
- Verificação do CPF a cada edição.
- Aviso de edição simultânea do mesmo cadastro.
- Lista única de processos em Enviado para Backoffice.
- Tela de status dos cadastros, com consulta por CPF.
- Consulta dos dados cadastrais do cliente.
- Histórico de cada cadastro, com mensagens, mudanças de status e antes e depois dos campos alterados.

### 4.2 Fora do escopo

- Perfil de administrador e fluxo de administração de usuários e perfis.
- O processamento do cadastro pelas áreas que o recebem depois da publicação no tópico.
- Comunicação com o cliente (e-mail ou SMS de confirmação).
- Notificações aos usuários (como avisos de cadastro devolvido).
- Relatórios e painéis gerenciais.
- Aplicativo móvel.
- Acesso direto do cliente para preencher ou consultar o próprio cadastro.

## 5. Jornadas e fluxos

### 5.1 Fluxo principal

1. O usuário do setor de Cadastro consulta o CPF do cliente.
2. Se o CPF não tiver cadastro no sistema, o usuário preenche o cadastro do novo cliente. O cliente fica com status Novo, no processo 1.
3. O usuário aciona "Enviar para Backoffice". O processo passa ao status Enviado para Backoffice.
4. O sistema exibe um aviso de que o cadastro foi realizado e um botão para consultar o status.
5. O processo entra na lista única de processos em Enviado para Backoffice. Um usuário do Backoffice, que não tenha enviado esse processo, verifica e analisa o processo.
6. Não havendo problemas de preenchimento, o Backoffice aceita o processo. Todos os dados do cadastro são publicados no tópico, o processo passa ao status Aceito e enviado para processamento, o cliente passa ao status Ativo e os dados novos passam a ser os dados atuais.
7. O setor de Cadastro consulta o status do cadastro na tela de status.

### 5.2 Fluxo alternativo: rascunho

1. Durante o preenchimento, o usuário do setor de Cadastro aciona "Salvar". O processo passa ao status Rascunho e o sistema exibe uma confirmação simples de que foi salvo.
2. O usuário pode voltar ao processo em Rascunho, editá-lo, salvá-lo novamente e, quando quiser, acionar "Enviar para Backoffice".
3. Um processo em Rascunho não é cancelado e pode ficar parado indefinidamente. Enquanto um rascunho de pedido está parado, o cliente segue com os dados atuais.
4. Qualquer usuário do setor de Cadastro pode retomar ou descartar um rascunho do primeiro processo ou de pedido esquecido por outro usuário.

### 5.3 Fluxo alternativo: devolução para correção

1. Ao analisar um processo com status Enviado para Backoffice, o Backoffice encontra problemas de preenchimento ou entende que o cadastro deve ser cancelado.
2. O Backoffice aciona "Devolver para correção" e preenche o campo "motivo", que pode conter a orientação para cancelar.
3. O processo passa ao status Devolvido para correção.
4. O setor de Cadastro vê o motivo e edita o processo devolvido. Pode salvar a correção sem reenviar, e o processo continua em Devolvido para correção.
5. Após a correção, o setor de Cadastro aciona "Enviar para Backoffice" e o processo volta ao status Enviado para Backoffice.
6. Em vez de corrigir, o setor de Cadastro pode descartar o processo (5.10) ou, se o cliente estiver Ativo, pedir o cancelamento (5.7).

### 5.4 Fluxo alternativo: CPF já cadastrado

1. O usuário do setor de Cadastro consulta o CPF do cliente.
2. Se o CPF tiver cliente Novo ou Ativo, ou qualquer cliente com processo aberto, o sistema mostra o status do cliente, exibe a mensagem "cadastro já iniciado" e um link para consultar os dados cadastrais do cliente, e não permite iniciar um novo cadastro para esse CPF.
3. Se o cliente estiver Ativo, sem processo aberto, a consulta também oferece ao setor de Cadastro abrir um pedido de alteração (5.8) ou de cancelamento (5.7). Se o cliente estiver Cancelado, sem processo aberto, a consulta mostra o status e oferece a reabertura (5.6).
4. O usuário pode consultar o CPF na tela de status para ver o status do cadastro existente.
5. Se o processo do cadastro estiver com status Rascunho ou Devolvido para correção, o setor de Cadastro pode editá-lo.
6. Se o processo estiver com status Enviado para Backoffice, o setor de Cadastro não pode editá-lo; para que seja ajustado, o Backoffice precisa devolvê-lo para correção.
7. Se o processo estiver com status Aceito e enviado para processamento, o setor de Cadastro não pode editá-lo; o ajuste ocorre por pedido de alteração de dados (5.8).

### 5.5 Ciclo de vida do cadastro

O ciclo de vida tem dois níveis: o cadastro do cliente e o processo no Backoffice. Um cadastro do cliente pode ter vários processos ao longo do tempo, com no máximo um processo aberto por vez. Processo aberto é o que está com status Rascunho, Enviado para Backoffice ou Devolvido para correção; os demais estão encerrados.

Status do cadastro do cliente, identificado por Id Cliente:

| Status | Significado | Situação |
|---|---|---|
| Novo | O primeiro processo ainda não foi aceito. | Saída pelo aceite do primeiro processo ou pelo descarte, quando o cliente deixa de existir. |
| Ativo | O primeiro processo ou um pedido de reabertura foi aceito. | Saída pelo pedido de cancelamento aceito; pode ser o último status do cliente. |
| Cancelado | O pedido de cancelamento foi aceito. Aparece nas consultas de CPF e, sem processo aberto, não aparece como pendente para nenhum setor. | Saída pelo pedido de reabertura aceito; pode ser o último status do cliente. |

Status do processo no Backoffice, identificado por Id Processo:

| Status | Significado | Situação |
|---|---|---|
| Rascunho | Processo salvo pelo setor de Cadastro e ainda não enviado. | Saída por envio ou descarte; pode ficar parado indefinidamente. |
| Enviado para Backoffice | Processo enviado para verificação e análise do Backoffice. | Saída por devolução ou aceite. |
| Devolvido para correção | Processo devolvido pelo Backoffice ao setor de Cadastro, com motivo. | Saída por reenvio, descarte ou pedido de cancelamento de cliente Ativo. |
| Aceito e enviado para processamento | Processo aceito pelo Backoffice e publicado no tópico. | Final do processo. |
| Alterações Descartadas | Processo encerrado por descarte. | Final do processo. |

O status vigente do cliente é o dos dados atuais; o pedido fica nos dados novos. Enquanto um pedido está pendente, o cliente mantém o status vigente: Ativo, em pedido de alteração ou de cancelamento; Cancelado, em pedido de reabertura. Depois do aceite do primeiro processo, Ativo fica nos dados atuais. Depois de uma desistência, o que foi pedido só permanece no histórico.

Transições do processo:

| De | Para | Quem | Ação |
|---|---|---|---|
| (novo cadastro) | Rascunho | Setor de Cadastro | Salvar |
| (novo cadastro) | Enviado para Backoffice | Setor de Cadastro | Enviar para Backoffice |
| (cliente Ativo sem processo aberto) | Rascunho, em novo processo | Setor de Cadastro | Pedir alteração de dados, com motivo |
| (cliente Ativo sem processo aberto) | Rascunho, em novo processo | Setor de Cadastro | Pedir cancelamento, com motivo |
| (cliente Cancelado sem processo aberto) | Rascunho, em novo processo | Setor de Cadastro | Pedir reabertura, com motivo |
| Rascunho | Rascunho | Setor de Cadastro | Salvar |
| Rascunho | Enviado para Backoffice | Setor de Cadastro | Enviar para Backoffice |
| Rascunho, no primeiro processo ou em pedido de alteração, de cancelamento ou de reabertura | Alterações Descartadas | Setor de Cadastro | Descartar |
| Enviado para Backoffice | Devolvido para correção | Backoffice | Devolver para correção, com motivo |
| Enviado para Backoffice | Aceito e enviado para processamento | Backoffice | Aceitar, com publicação bem-sucedida no tópico |
| Devolvido para correção | Devolvido para correção | Setor de Cadastro | Salvar a correção, sem reenviar |
| Devolvido para correção | Enviado para Backoffice | Setor de Cadastro | Enviar para Backoffice, após a correção |
| Devolvido para correção, no primeiro processo ou em pedido de alteração, de cancelamento ou de reabertura | Alterações Descartadas | Setor de Cadastro | Descartar |
| Devolvido para correção, de cliente Ativo | Alterações Descartadas, e novo processo em Rascunho | Setor de Cadastro | Pedir cancelamento, com motivo |
| Rascunho ou Devolvido para correção, de cliente Novo | Alterações Descartadas | Setor de Cadastro | Confirmar o início de outro processo ao editar o CPF (5.12) |

O usuário que tiver feito qualquer envio do processo não pode aceitá-lo nem devolvê-lo, mesmo que também tenha o perfil Backoffice. Se a publicação no tópico falhar, nenhum status muda. Se o processo já tiver sido decidido por outro usuário do Backoffice, a ação do segundo não é aplicada (5.14).

Transições do cadastro do cliente:

| De | Para | Quem | Ação |
|---|---|---|---|
| (sem cadastro no CPF) | Novo | Setor de Cadastro | Iniciar o cadastro |
| Novo | Ativo | Backoffice | Aceitar o primeiro processo |
| Novo | (deixa de existir; mantém-se apenas o histórico) | Setor de Cadastro | Descartar o primeiro processo, inclusive ao confirmar o início de outro processo na edição do CPF |
| Ativo | Ativo | Backoffice | Aceitar o pedido de alteração de dados |
| Ativo | Cancelado | Backoffice | Aceitar o pedido de cancelamento |
| Ativo | Ativo | Setor de Cadastro | Descartar o pedido de alteração ou de cancelamento |
| Cancelado | Ativo | Backoffice | Aceitar o pedido de reabertura |
| Cancelado | Cancelado | Setor de Cadastro | Descartar o pedido de reabertura |

Não existe status próprio para pedidos, como "Cancelamento solicitado".

### 5.6 Fluxo alternativo: reabertura de cliente Cancelado

1. O usuário do setor de Cadastro consulta um CPF cujo cliente está Cancelado, sem processo aberto, ou informa esse CPF na edição (5.12).
2. Na consulta, o sistema mostra que existe cadastro cancelado, com um link para ver os dados, e oferece reabrir o cadastro existente. Na edição, pergunta se o usuário quer reabrir esse cliente.
3. O setor de Cadastro pede a reabertura e informa o motivo. Abre-se um novo processo, em Rascunho, com o mesmo Id Cliente, Cancelado nos dados atuais e Ativo nos dados novos, com os campos já preenchidos e todo o histórico. O cliente continua Cancelado.
4. Todos os campos podem ser editados, exceto o CPF.
5. O setor de Cadastro aciona "Enviar para Backoffice". O processo passa ao status Enviado para Backoffice e o sistema mostra as alterações pedidas.
6. Se o Backoffice aceitar, o histórico do que mudou e os novos valores dos campos são publicados no tópico, indicando a reabertura, o processo passa ao status Aceito e enviado para processamento, o cliente volta ao status Ativo e os dados novos passam a ser os dados atuais.
7. Se o Backoffice devolver, o processo passa ao status Devolvido para correção e continua mostrando as alterações pedidas. O cliente continua Cancelado.
8. Se o CPF do cliente Cancelado pertencer a outra pessoa, o caminho é reabrir e substituir os dados pelos da pessoa correta, com motivo e aprovação do Backoffice. O histórico guarda tudo, e as outras áreas recebem a mudança como uma reabertura, com o antes e o depois dos campos.

### 5.7 Fluxo alternativo: pedido de cancelamento pelo setor de Cadastro

1. O setor de Cadastro pede o cancelamento de um cliente Ativo e informa o motivo. Abre-se um novo processo, em Rascunho, e o pedido fica nos dados novos. O cliente continua Ativo.
2. Se o cliente Ativo tiver um processo em Devolvido para correção, esse processo termina em Alterações Descartadas e o novo processo de cancelamento começa em Rascunho.
3. O setor de Cadastro aciona "Enviar para Backoffice". O processo passa ao status Enviado para Backoffice e o sistema mostra a alteração pedida.
4. Se o Backoffice aceitar, o cancelamento é publicado no tópico, o processo passa ao status Aceito e enviado para processamento, o cliente passa ao status Cancelado e os dados novos passam a ser os dados atuais.
5. Se o Backoffice devolver, o processo passa ao status Devolvido para correção e continua mostrando as alterações pedidas. O cliente continua Ativo.

### 5.8 Fluxo alternativo: pedido de alteração de dados

1. O setor de Cadastro pede a alteração de dados de um cliente Ativo sem processo aberto e informa o motivo. Abre-se um novo processo, em Rascunho, e os valores pedidos ficam nos dados novos. O cliente continua Ativo.
2. O setor de Cadastro aciona "Enviar para Backoffice". O processo passa ao status Enviado para Backoffice e o sistema mostra o antes e o depois dos campos.
3. Se o Backoffice aceitar, o histórico do que mudou e os novos valores dos campos são publicados no tópico, o processo passa ao status Aceito e enviado para processamento e os dados novos passam a ser os dados atuais. O cliente continua Ativo.
4. Se o Backoffice devolver, o processo passa ao status Devolvido para correção e continua mostrando as alterações pedidas. O cliente continua Ativo.
5. O CPF de um cliente Ativo não pode ser alterado por este fluxo. Se estiver errado, o setor de Cadastro pede o cancelamento (5.7) e inicia um novo cadastro com o CPF correto.

### 5.9 Fluxo de erro: CPF inválido

1. O usuário informa um CPF inválido na consulta.
2. O sistema mostra uma mensagem de CPF inválido e não faz a consulta.
3. O cadastro não pode ser iniciado.

### 5.10 Fluxo alternativo: descarte de um processo

1. Com um processo em Rascunho ou Devolvido para correção, o setor de Cadastro decide descartá-lo.
2. O processo termina no status Alterações Descartadas e nada é publicado no tópico.
3. Se for um pedido de alteração ou de cancelamento, os valores pedidos são descartados e o cliente continua Ativo, com os dados atuais.
4. Se for um pedido de reabertura, os valores pedidos são descartados e o cliente continua Cancelado.
5. Se for o primeiro processo, o cliente deixa de existir como Novo, mantém-se apenas o histórico e o CPF fica livre para um novo cadastro.

### 5.11 Fluxo de erro: falha na publicação

1. O Backoffice aceita um processo e a publicação no tópico falha.
2. O status não muda.
3. O Backoffice vê uma mensagem de erro e precisa aceitar novamente.

### 5.12 Fluxo alternativo: verificação do CPF na edição

Enquanto o cliente estiver Novo, o setor de Cadastro pode alterar o CPF. A cada edição, o sistema verifica o CPF informado:

| Situação do CPF informado | Comportamento do sistema |
|---|---|
| Sem cadastro | Aceita o CPF e segue a edição. |
| Cliente Ativo sem processo aberto | Pergunta se o usuário quer abrir um pedido de alteração ou de cancelamento para esse cliente. |
| Cliente Cancelado sem processo aberto | Pergunta se o usuário quer reabrir esse cliente. |
| Cliente Novo ou qualquer cliente com processo aberto | Não permite iniciar outro processo, mostra "cadastro já iniciado" e o link para consultar os dados, e recusa o CPF digitado. |

Se o usuário aceitar iniciar outro processo, o sistema avisa antes e, com a confirmação, o cadastro em edição é descartado: termina em Alterações Descartadas, o cliente Novo deixa de existir e o CPF original fica livre.

Se o usuário recusar abrir um pedido ou reabrir um cliente, o CPF digitado é recusado e a edição continua com o CPF anterior.

### 5.13 Fluxo alternativo: edição simultânea

1. Dois usuários abrem o mesmo cadastro.
2. Um deles salva.
3. Quando o outro tenta salvar depois disso, vê um aviso e precisa recarregar os dados antes de continuar.
4. Nenhuma alteração é sobrescrita sem que o usuário saiba.

### 5.14 Fluxo de erro: processo já decidido

1. Dois usuários do Backoffice analisam o mesmo processo.
2. Um deles aceita ou devolve o processo.
3. Quando o outro tenta agir, vê um aviso de que o processo já foi decidido, e sua ação não é aplicada.

## 6. Requisitos funcionais

- **RF01** — O sistema só pode ser usado após autenticação do usuário.
- **RF02** — O sistema controla o acesso por perfil, com funções diferentes para o setor de Cadastro e para o Backoffice, conforme a seção 3.
- **RF03** — O sistema permite aos dois perfis consultar um cliente pelo CPF. O setor de Cadastro faz essa consulta antes de iniciar um novo cadastro; o Backoffice não pode iniciar um novo cadastro a partir dela. A consulta considera somente os cadastros do próprio sistema.
- **RF04** — Quando o CPF consultado tiver cliente Novo ou Ativo, ou qualquer cliente com processo aberto, o sistema exibe a mensagem "cadastro já iniciado" e um link para consultar os dados cadastrais do cliente, e impede o início de um novo cadastro para esse CPF.
- **RF05** — O sistema permite ao setor de Cadastro preencher o cadastro de um novo cliente com os campos da seção 8.
- **RF06** — Em todo envio de um processo para o Backoffice, inclusive reenvios e pedidos, o sistema exibe um aviso de que o cadastro foi realizado e um botão para consultar o status. Ao salvar um rascunho, esse aviso não é exibido; aparece só a confirmação simples de RF11.
- **RF07** — O setor de Cadastro pode enviar o processo para verificação e análise do Backoffice pela ação "Enviar para Backoffice", inclusive para reenviar um processo corrigido após a devolução.
- **RF09** — O sistema oferece uma tela de status com o status de cada cadastro, conforme a seção 5.5. Os dois perfis veem nessa tela todos os cadastros, de qualquer usuário do setor de Cadastro.
- **RF10** — A consulta (pesquisa por CPF) e o preenchimento/edição do cadastro são funções separadas, em telas distintas.
- **RF11** — O setor de Cadastro pode salvar o processo como rascunho pela ação "Salvar". Ao salvar um rascunho, o sistema exibe uma confirmação simples de que foi salvo. Em Devolvido para correção, a mesma ação salva a correção sem reenviar, e o status não muda.
- **RF12** — O Backoffice pode devolver um processo com status Enviado para Backoffice pela ação "Devolver para correção", com preenchimento do campo "motivo", que pode conter a orientação para cancelar. O motivo fica visível para quem corrige o processo.
- **RF13** — O Backoffice pode aceitar um processo com status Enviado para Backoffice.
- **RF14** — A tela de status permite consultar um cadastro pelo CPF.
- **RF15** — Os dois perfis (setor de Cadastro e Backoffice) podem abrir os dados cadastrais de um cliente.
- **RF17** — O setor de Cadastro pode pedir o cancelamento de um cliente Ativo sem processo aberto, ou com processo em Devolvido para correção, informando o motivo. O pedido abre um novo processo, em Rascunho; havendo processo devolvido, ele termina em Alterações Descartadas.
- **RF18** — O setor de Cadastro pode pedir a alteração de dados de um cliente Ativo sem processo aberto, informando o motivo. O pedido abre um novo processo, em Rascunho.
- **RF19** — O setor de Cadastro pode descartar o primeiro processo ou um pedido de alteração de dados, de cancelamento ou de reabertura, em Rascunho ou Devolvido para correção. O processo termina no status Alterações Descartadas.
- **RF20** — Enquanto um pedido de alteração de dados, de cancelamento ou de reabertura estiver com status Enviado para Backoffice ou Devolvido para correção, o sistema mostra as alterações pedidas.
- **RF21** — O sistema oferece um local para exibir o histórico de cada cadastro, com as mensagens, as mudanças de status e o antes e o depois de toda alteração de campo ou de status, em qualquer momento. Os dois perfis podem consultar o histórico de qualquer cadastro.
- **RF22** — Quando o Backoffice aceita o primeiro processo de um cadastro, o sistema publica todos os dados do cadastro em tópico, consumido pelas áreas interessadas em novos cadastros ou em mudanças cadastrais.
- **RF23** — Quando o Backoffice aceita o pedido de cancelamento de um cadastro que já tinha sido aceito, o sistema publica no tópico o histórico do que mudou e os novos valores dos campos, indicando o cancelamento.
- **RF24** — O cliente Cancelado aparece nas consultas de CPF e não aparece como pendente para nenhum setor, exceto quando há um processo aberto, como um pedido de reabertura.
- **RF25** — Quando o CPF consultado tiver cliente Cancelado sem processo aberto, o sistema mostra que existe cadastro cancelado, com um link para ver os dados, e oferece ao setor de Cadastro reabrir o cadastro existente. O pedido de reabertura exige motivo e abre um novo processo, em Rascunho, com o mesmo Id Cliente, os campos já preenchidos e todo o histórico. Todos os campos podem ser editados, exceto o CPF.
- **RF26** — Ao receber um CPF inválido, o sistema mostra uma mensagem de CPF inválido, não faz a consulta e não permite iniciar o cadastro.
- **RF27** — Quando o Backoffice aceita um pedido de alteração de dados, o sistema publica no tópico o histórico do que mudou e os novos valores dos campos.
- **RF28** — Se a publicação no tópico falhar, o sistema não muda o status e mostra uma mensagem de erro ao Backoffice, que precisa aceitar novamente.
- **RF29** — O setor de Cadastro só pode alterar o CPF enquanto o cliente estiver Novo. A cada edição, o sistema valida o CPF informado e aplica a verificação de 5.12.
- **RF30** — Na edição do CPF, se o usuário aceitar iniciar outro processo para o cliente do CPF informado, o sistema avisa antes e, com a confirmação, descarta o cadastro em edição.
- **RF31** — Qualquer usuário do setor de Cadastro pode retomar ou descartar um rascunho do primeiro processo ou de pedido esquecido por outro usuário.
- **RF32** — Quando o Backoffice aceita um pedido de reabertura, o sistema publica no tópico o histórico do que mudou e os novos valores dos campos, indicando a reabertura.
- **RF33** — O sistema oferece ao Backoffice uma lista única de processos em Enviado para Backoffice. Qualquer usuário do Backoffice pode analisar qualquer processo da lista, sem atribuição.
- **RF34** — Quando um usuário tenta salvar um cadastro depois de outra pessoa já ter salvado, o sistema mostra um aviso e exige que ele recarregue os dados antes de continuar.
- **RF35** — O sistema não permite que um usuário aceite ou devolva um processo do qual tenha feito qualquer envio, não só o último.
- **RF36** — A consulta de CPF mostra o status do cliente e oferece ao setor de Cadastro as mesmas ações da edição: pedido de alteração ou de cancelamento para cliente Ativo sem processo aberto e reabertura para cliente Cancelado sem processo aberto. Essas ações não são oferecidas ao Backoffice.
- **RF37** — Se dois usuários do Backoffice agirem no mesmo processo, o segundo vê um aviso de que o processo já foi decidido, e sua ação não é aplicada.

## 7. Regras de negócio

- **RN01** — A consulta do CPF deve ser feita antes do cadastro de um novo cliente.
- **RN02** — Somente o setor de Cadastro inicia cadastros de novos clientes. O Backoffice não pode cadastrar novos clientes; atua apenas sobre processos já iniciados pelo setor de Cadastro. O Backoffice pode usar a consulta de CPF, mas não pode iniciar um novo cadastro a partir dela.
- **RN03** — Somente o Backoffice aceita um processo, seja o primeiro processo do cadastro, um pedido de alteração de dados, um pedido de cancelamento ou um pedido de reabertura.
- **RN04** — Cada CPF tem um único cliente. Se o CPF tiver cliente Novo ou Ativo, o sistema impede o início de um novo cadastro. Se o CPF tiver cliente Cancelado, a consulta oferece a reabertura do cadastro existente, e não um novo cadastro. Um cliente Novo descartado deixa de existir e seu CPF fica livre para um novo cadastro. A verificação de CPF existente considera somente os cadastros do próprio sistema.
- **RN06** — A devolução para correção exige o preenchimento do motivo. Sem motivo, a devolução não é realizada.
- **RN07** — O setor de Cadastro só pode editar processos com status Rascunho ou Devolvido para correção. Processos com status Enviado para Backoffice só podem ser ajustados depois da devolução pelo Backoffice. Processos com status Aceito e enviado para processamento não podem ser editados nem devolvidos; o ajuste de um cliente Ativo ocorre somente por novo processo, aberto pelo setor de Cadastro e avaliado pelo Backoffice.
- **RN08** — Os campos Nome e CPF são obrigatórios. Os demais campos são opcionais, com esta exceção: o endereço é opcional, mas, se qualquer um de seus campos for preenchido, todos os demais passam a ser obrigatórios, exceto o complemento.
- **RN09** — O CPF é válido quando tem 11 dígitos e dígitos verificadores válidos. Com CPF inválido, o sistema não faz a consulta e o cadastro não pode ser iniciado.
- **RN10** — O Nome é exigido já ao salvar o rascunho. As validações da seção 8 e a regra de endereço completo de RN08 também são exigidas ao salvar o rascunho; um rascunho não pode ser salvo com campo inválido nem com endereço parcial.
- **RN11** — O Backoffice não altera diretamente os dados do cadastro e nunca cancela diretamente; ele só devolve ou aceita. Todo ajuste passa pela devolução ao setor de Cadastro. Para orientar um cancelamento, o Backoffice devolve o processo e escreve a orientação no motivo.
- **RN13** — O cancelamento só acontece quando o setor de Cadastro pede e o Backoffice aceita, e fica restrito a clientes Ativos. Um cliente Novo não pode ser cancelado; pode ter suas alterações descartadas. Com processo em Enviado para Backoffice, o setor de Cadastro não pode pedir cancelamento. Um processo em Rascunho não é cancelado e pode ficar parado indefinidamente.
- **RN14** — O pedido de cancelamento, o pedido de alteração de dados e o pedido de reabertura exigem motivo. Sem motivo, o pedido não é realizado. O motivo entra no histórico.
- **RN15** — No descarte de um pedido de alteração de dados ou de cancelamento, o processo termina no status Alterações Descartadas, os valores pedidos são descartados, o cliente continua Ativo e nada é publicado no tópico. No descarte de um pedido de reabertura, em Rascunho ou Devolvido para correção, ocorre o mesmo, e o cliente continua Cancelado. O que foi pedido só permanece no histórico.
- **RN16** — Enquanto não sair do setor de Cadastro e do Backoffice, o cadastro não pode ir para as outras áreas da empresa.
- **RN17** — O tópico só recebe o cancelamento de um cadastro que já tinha sido aceito. Um pedido pendente, devolvido, desfeito ou descartado não publica nada no tópico.
- **RN18** — Não existem idade mínima para o cliente nem documentos a anexar ao cadastro.
- **RN19** — Cada cliente tem um Id Cliente, que não muda, inclusive na reabertura. Cada mudança abre um processo com novo Id Processo.
- **RN20** — Ao aceitar um processo, os dados novos sempre passam a ser os dados atuais.
- **RN21** — Os dados aceitos anteriormente continuam valendo para as outras áreas até o Backoffice aceitar o pedido. As áreas não são avisadas do pedido pendente.
- **RN22** — Se a publicação no tópico falhar, o status não muda e o Backoffice precisa aceitar novamente.
- **RN23** — O CPF só pode ser alterado enquanto o cliente estiver Novo. Se o CPF de um cliente Ativo estiver errado, o setor de Cadastro pede o cancelamento e inicia um novo cadastro com o CPF correto. Um cliente Cancelado reaberto não pode trocar de CPF.
- **RN24** — Cada cliente tem no máximo um processo aberto por vez; só depois de encerrado é possível abrir outro. A exceção é o pedido de cancelamento de cliente Ativo com processo em Devolvido para correção, em que o processo devolvido termina em Alterações Descartadas e o novo começa em Rascunho.
- **RN25** — No descarte do primeiro processo, o processo termina em Alterações Descartadas, o cliente deixa de existir como Novo e o CPF fica livre para um novo cadastro, mantendo-se apenas o histórico.
- **RN26** — A cada edição do CPF, o sistema verifica o CPF informado. Sem cadastro, aceita. Cliente Ativo sem processo aberto: pergunta se o usuário quer abrir pedido de alteração ou de cancelamento. Cliente Cancelado sem processo aberto: pergunta se o usuário quer reabri-lo. Cliente Novo ou qualquer cliente com processo aberto: não permite iniciar outro processo, mostra "cadastro já iniciado" e o link para consultar os dados, e recusa o CPF digitado. Se o usuário recusar abrir um pedido ou reabrir um cliente, o CPF digitado é recusado e a edição continua com o anterior.
- **RN27** — Um cliente Cancelado sem processo aberto pode ser reaberto, a partir da consulta de CPF ou da verificação na edição. Só o setor de Cadastro pode iniciar a reabertura; o Backoffice apenas a avalia. A reabertura abre um novo processo, em Rascunho, com o mesmo Id Cliente, Cancelado nos dados atuais e Ativo nos dados novos, os campos já preenchidos e todo o histórico. Todos os campos podem ser editados, exceto o CPF. Se o Backoffice devolver, o processo vai para Devolvido para correção; se aceitar, o cliente volta a Ativo e os dados novos passam a ser os dados atuais.
- **RN28** — Se, na edição do CPF, o usuário aceitar iniciar outro processo, o sistema avisa antes e, com a confirmação, o cadastro em edição termina em Alterações Descartadas, o cliente Novo deixa de existir e o CPF original fica livre.
- **RN29** — Dois usuários podem abrir o mesmo cadastro. Quem salvar depois de outra pessoa já ter salvado vê um aviso e precisa recarregar os dados antes de continuar. Nenhuma alteração é sobrescrita sem que o usuário saiba.
- **RN30** — Quando um cliente Cancelado tem CPF que pertence a outra pessoa, o caminho é reabrir e substituir os dados pelos da pessoa correta, com motivo e aprovação do Backoffice. O histórico guarda tudo, a regra de um cliente por CPF continua valendo e as outras áreas recebem a mudança como uma reabertura, com o antes e o depois dos campos.
- **RN31** — Um mesmo usuário pode ter os dois perfis, mas não pode aceitar nem devolver um processo que ele mesmo enviou. A restrição considera qualquer envio daquele processo, não só o último.
- **RN32** — Há uma lista única de processos em Enviado para Backoffice, e qualquer usuário do Backoffice pode analisar qualquer um, sem atribuição.
- **RN33** — Se dois usuários do Backoffice agirem no mesmo processo, o segundo vê um aviso de que o processo já foi decidido, e sua ação não é aplicada.
- **RN34** — Um novo cadastro pode ser enviado ao Backoffice sem ter sido salvo antes. Em Devolvido para correção, é possível salvar uma correção sem reenviar.

## 8. Dados

Identificadores, no nível de negócio:

| Identificador | Significado |
|---|---|
| Id Cliente | Identifica o cliente e não muda, inclusive na reabertura. |
| Id Processo | Identifica o processo no Backoffice. Há um novo a cada mudança do cadastro, e ele se mantém enquanto o mesmo processo passa pelos seus status. O novo cadastro começa no processo 1. |

Conjuntos de dados:

| Conjunto | Significado |
|---|---|
| Dados atuais | Dados e status vigentes do cliente, aceitos pelo Backoffice. |
| Dados novos | Dados e status pedidos no processo, que passam a ser os dados atuais quando o processo é aceito. |

Campos do cadastro do cliente:

| Campo | Obrigatório | Validação |
|---|---|---|
| Nome | Sim, já ao salvar o rascunho | Não pode ficar em branco. |
| CPF | Sim | 11 dígitos e dígitos verificadores válidos. Só pode ser alterado enquanto o cliente estiver Novo, com a verificação de RN26 a cada edição. |
| E-mail | Não | Formato válido (nome@dominio). |
| Telefone | Não | DDD e número válidos. |
| Data de nascimento | Não | Data válida e não futura. |
| Endereço: CEP | Se qualquer campo do endereço for preenchido | 8 dígitos. |
| Endereço: rua | Se qualquer campo do endereço for preenchido | — |
| Endereço: número | Se qualquer campo do endereço for preenchido | — |
| Endereço: complemento | Não | — |
| Endereço: bairro | Se qualquer campo do endereço for preenchido | — |
| Endereço: cidade | Se qualquer campo do endereço for preenchido | — |
| Endereço: UF | Se qualquer campo do endereço for preenchido | Uma das 27 siglas válidas do Brasil. |

Não há documentos a anexar.

Motivos:

| Campo | Obrigatório |
|---|---|
| Motivo da devolução | Sim |
| Motivo do pedido de cancelamento | Sim |
| Motivo do pedido de alteração de dados | Sim |
| Motivo do pedido de reabertura | Sim |

Dados de cada registro do histórico:

- usuário que fez a ação;
- data e hora da ação;
- mensagem ou motivo, quando houver;
- antes e depois do campo ou do status alterado.

O histórico de um cliente Novo descartado é mantido.

## 9. Requisitos não funcionais

- **Autenticação**: o sistema só pode ser usado após autenticação do usuário.
- **Perfis de acesso**: as ações disponíveis dependem do perfil do usuário, conforme a seção 3.
- **Segregação de funções**: um usuário com os dois perfis não pode aceitar nem devolver um processo que ele mesmo enviou, em qualquer envio daquele processo.
- **Histórico**: toda alteração de campo ou de status, em qualquer momento, fica registrada no histórico do cadastro, com usuário, data e hora da ação e o antes e o depois.
- **Visibilidade dos dados**: nenhum dado é mascarado; os dois perfis veem todos os dados.
- **Guarda dos dados**: não há prazo de guarda definido nesta versão. Os dados são mantidos e não há exclusão automática.

## 10. Integrações

- O "envio para processamento" é o envio do cadastro às outras áreas da empresa, que realmente irão utilizá-lo, por exemplo para criar conta, criar perfil de usuário e em outras funcionalidades e produtos da empresa.
- O envio é feito por publicação em tópico, consumido pelas áreas interessadas em novos cadastros ou em mudanças cadastrais. O uso de tópico é uma restrição declarada pelo stakeholder.
- Os dados aceitos anteriormente continuam valendo para as outras áreas até o Backoffice aceitar um pedido, e as áreas não são avisadas do pedido pendente.

O que é publicado no tópico:

| Evento | Publicação |
|---|---|
| Backoffice aceita o primeiro processo do cadastro | Todos os dados do cadastro |
| Backoffice aceita pedido de alteração de dados | Histórico do que mudou e novos valores dos campos |
| Backoffice aceita pedido de cancelamento de um cadastro que já tinha sido aceito | Histórico do que mudou e novos valores dos campos, indicando o cancelamento |
| Backoffice aceita pedido de reabertura | Histórico do que mudou e novos valores dos campos, indicando a reabertura |
| Pedido pendente, devolvido, desfeito ou descartado | Nada |

Se a publicação falhar, o status não muda; o Backoffice vê uma mensagem de erro e precisa aceitar novamente.

## 12. Histórico de decisões

| Data | Decisão | Origem |
|---|---|---|
| 2026-10-25 | Versão inicial do PRD com o contexto, as áreas (setor de Cadastro e Backoffice), o fluxo principal, a consulta de CPF e a consulta de status, conforme descrito pelo stakeholder. | Primeiro insumo do stakeholder |
| 2026-10-25 | O Backoffice não pode cadastrar novos clientes (confirma P01). Não haverá perfil de administrador; administração de usuários e perfis fica fora deste sistema. | Resposta à pergunta 1 |
| 2026-10-25 | Existe rascunho: ações "Salvar" e "Enviar para Backoffice" (nega P03). | Resposta à pergunta 2 |
| 2026-10-25 | Devolução para correção com motivo obrigatório; o Backoffice é quem marca o cadastro como concluído (confirma P02); status Rascunho, Enviado para Backoffice, Devolvido para correção e Aceito e enviado para processamento; o processamento após o aceite fica fora do escopo. | Resposta à pergunta 3 |
| 2026-10-25 | CPF existente impede novo cadastro em qualquer status (confirma P04); consulta de CPF na tela de status; todos os perfis abrem os dados cadastrais; o setor de Cadastro só edita cadastros que estão com ele; para os demais, o Backoffice precisa devolver. | Resposta à pergunta 4 |
| 2026-10-25 | Consulta de CPF somente no próprio sistema; sem migração; sistema de terceiro em uso somente até a publicação e liberação do novo. | Resposta à pergunta 5 |
| 2026-10-25 | Campos do cadastro: Nome, e-mail, telefone, data de nascimento, endereço e CPF; obrigatórios: Nome e CPF. | Resposta à pergunta 6 |
| 2026-10-25 | Métrica de sucesso: 10 cadastros feitos pelo setor de Cadastro. | Resposta à pergunta 7 |
| 2026-10-25 | RF09 passa a tratar da tela de status com todos os status do ciclo de vida; incluídos RF11 a RF15 e RN04 a RN08; RN03 reescrita para o aceite pelo Backoffice. | Respostas às perguntas 1 a 7 |
| 2026-11-02 | "Concluído" é o mesmo que Aceito e enviado para processamento, e "em análise do Backoffice" é o mesmo que Enviado para Backoffice (confirma P08 e P09). O corpo do PRD passa a usar somente os nomes de status. | Resposta à pergunta 1 |
| 2026-11-02 | O Backoffice não altera dados diretamente; só devolve, aceita ou cancela. RF08 removido, sem reutilização do identificador; perfil, escopo e fluxo principal ajustados; incluída RN11. | Resposta à pergunta 2 |
| 2026-11-02 | O envio para processamento é o envio às outras áreas da empresa, por publicação em tópico; o cadastro não vai a essas áreas enquanto não sair do setor de Cadastro e do Backoffice. Cadastros cancelados são publicados, o que substitui a fala anterior de que não seriam enviados. Incluídos RF22, RF23, RN16 e RN17; seção 10 atualizada. | Resposta à pergunta 3 |
| 2026-11-02 | Após a correção, o setor de Cadastro reenvia pelo "Enviar para Backoffice" (confirma P07). O motivo da devolução, também chamado de "mensagem de devolução", é o campo "motivo" e fica visível para quem corrige (confirma P10). | Resposta à pergunta 4 |
| 2026-11-02 | Novo status Cancelado, adotado pelo stakeholder. O Backoffice pode cancelar um cadastro; o cancelamento exige motivo, pode ocorrer a partir de qualquer status, exceto Rascunho, e o cadastro cancelado aparece nas consultas de CPF sem aparecer como pendente. | Resposta à pergunta 4 |
| 2026-11-02 | Depois de um cancelamento, o setor de Cadastro pode iniciar novo cadastro para o mesmo CPF, reaproveitando os campos do cadastro anterior, o que substitui o "preenchido do zero". RN04 e RF04 reescritos; incluídos RF24 e RF25. | Resposta à pergunta 4 |
| 2026-11-02 | A devolução de um cadastro com status Aceito e enviado para processamento continua valendo: esse pode ser o último status, mas não é definitivo. Transição incluída em 5.5; RN07 e 5.4 alinhadas à tabela de transições; incluída RN12. | Resposta à pergunta 4 |
| 2026-11-02 | O setor de Cadastro pode pedir o cancelamento ou a alteração de dados de um cadastro com status Aceito e enviado para processamento, sem status novo: o cadastro passa a Enviado para Backoffice mostrando as alterações pedidas, e o Backoffice aceita ou devolve. Na desistência de um pedido de cancelamento devolvido, o cadastro volta direto a Aceito e enviado para processamento, sem novo envio. Incluídos 5.6 a 5.8, RF16 a RF20 e RN13 a RN15. | Resposta à pergunta 4 |
| 2026-11-02 | Histórico por cadastro com mensagens, mudanças de status e antes e depois de toda alteração de campo ou de status, em qualquer momento; cada registro guarda usuário, data e hora; os dois perfis consultam o histórico de qualquer cadastro. Incluído RF21. | Respostas às perguntas 4 e 7 |
| 2026-11-02 | Validações definidas; endereço dividido em CEP, rua, número, complemento, bairro, cidade e UF, com preenchimento completo quando iniciado, exceto complemento; CPF inválido impede a consulta e o início do cadastro; Nome e validações de campos exigidos ao salvar o rascunho; sem idade mínima e sem documentos a anexar. RN08 e seção 8 atualizadas; incluídos 5.9, RF26, RN09, RN10 e RN18. | Resposta à pergunta 5 |
| 2026-11-02 | Conta como cadastro feito o cadastro aceito pelo Backoffice e publicado no tópico, sem prazo para atingir os 10 cadastros. Ficam fora da primeira versão: comunicação com o cliente, notificações aos usuários, relatórios e painéis gerenciais, aplicativo móvel e acesso direto do cliente. | Resposta à pergunta 6 |
| 2026-11-02 | Nenhum dado é mascarado; sem prazo de guarda definido nesta versão, com dados mantidos e sem exclusão automática. Criada a seção 9. | Resposta à pergunta 7 |
| 2026-11-02 | Versão 4: ciclo de vida em dois níveis. Cadastro do cliente, com Id Cliente que não muda e status Novo, Ativo e Cancelado; processo no Backoffice, com novo Id Processo a cada mudança e status Rascunho, Enviado para Backoffice, Devolvido para correção, Aceito e enviado para processamento e Alterações Descartadas. Substitui o ciclo de vida anterior de 5.5. Incluídas RN19 e RN20 e a seção 8 com identificadores, dados atuais e dados novos. | Modelo confirmado pelo stakeholder |
| 2026-11-02 | "Cancelado" deixa de ser status do processo e passa a ser status do cliente. O processo de cancelamento termina em Aceito e enviado para processamento. Substitui a decisão anterior sobre o status Cancelado. | Modelo confirmado pelo stakeholder |
| 2026-11-02 | Pedidos de alteração ou de cancelamento abrem novo processo, que começa em Rascunho. Substitui a passagem direta para Enviado para Backoffice. Enquanto um pedido está pendente, o cliente continua Ativo. RF17 e RF18 reescritos; 5.7 e 5.8 reescritos. | Modelo confirmado pelo stakeholder |
| 2026-11-02 | Na desistência de um pedido de alteração ou de cancelamento, o processo termina em Alterações Descartadas, os valores pedidos são descartados e o cliente continua Ativo, sem publicação. Substitui a volta direta a Aceito e enviado para processamento. RF19 e RN15 reescritos; incluído 5.10. | Modelo confirmado pelo stakeholder; resposta à pergunta 22 |
| 2026-11-02 | O Backoffice não devolve um cadastro aceito; só o setor de Cadastro reabre um cadastro aceito, por pedido que o Backoffice avalia. Substitui a fala "mesmo após concluído" e a resposta anterior de que a devolução após o aceite continuava valendo. Retirados a transição correspondente e RN12, sem reutilização do identificador; RN07 e 5.4 reescritas. | Resposta à pergunta 15 |
| 2026-11-02 | Publicação: primeiro aceite, todos os dados; pedido de alteração aceito, histórico do que mudou e novos valores; pedido de cancelamento aceito, histórico do que mudou e novos valores, indicando o cancelamento; pedido pendente, devolvido ou desfeito, nada (confirma P11). RF22 e RF23 reescritos; incluído RF27; seção 10 atualizada. | Respostas às perguntas 16 e 17 |
| 2026-11-02 | O tópico só recebe o cancelamento de um cadastro que já tinha sido aceito. Substitui, nessa parte, a decisão anterior de publicar cadastros cancelados. RN17 reescrita. | Resposta à pergunta 18 |
| 2026-11-02 | Os dados aceitos anteriormente continuam valendo para as outras áreas até o Backoffice aceitar o pedido, e as áreas não são avisadas do pedido pendente. Incluída RN21. | Resposta à pergunta 19 |
| 2026-11-02 | Se a publicação falhar, o status não muda; o Backoffice vê uma mensagem de erro e precisa aceitar novamente. Incluídos 5.11, RF28 e RN22. | Resposta à pergunta 20 |
| 2026-11-02 | O Backoffice nunca cancela diretamente; pode devolver com a orientação para cancelar no motivo. O cancelamento só acontece quando o setor de Cadastro pede e o Backoffice aceita. Substitui a decisão de que o Backoffice podia cancelar e a regra de que todos os status, exceto Rascunho, levam ao cancelamento. Retirados RF16 e o fluxo de cancelamento pelo Backoffice, sem reutilização do identificador; RN11, RN13 e RF12 reescritos. | Resposta à pergunta 21 |
| 2026-11-02 | O pedido de alteração de dados exige motivo, que entra no histórico. RF18 e RN14 reescritos; seção 8 atualizada. | Resposta à pergunta 22 |
| 2026-11-02 | CPF com cliente Cancelado: a consulta mostra o cadastro cancelado, com link, e permite iniciar um novo; "cadastro já iniciado" fica só para CPF com cliente Novo ou Ativo. O novo cadastro recebe novo Id Cliente e começa como cliente Novo, no processo 1, em Rascunho; o cancelado permanece como está, com seu histórico. Campos preenchidos automaticamente a partir do cancelamento mais recente e editáveis, exceto o CPF nesse reaproveitamento inicial. RF04, RF25 e RN04 reescritos; 5.6 reescrito para este fluxo. | Resposta à pergunta 23 |
| 2026-11-02 | O setor de Cadastro pode alterar o CPF em qualquer processo que esteja editando; o sistema valida o novo CPF e não aceita um que já tenha cliente Novo ou Ativo. Incluídos RF29 e RN23. | Resposta à pergunta 24 |
| 2026-11-02 | A regra do endereço completo também vale ao salvar o rascunho (confirma P12). CEP com 8 dígitos e UF com uma das 27 siglas válidas do Brasil. RN10 e seção 8 atualizadas. | Resposta à pergunta 25 |
| 2026-11-02 | Versão 5. Regras de cancelamento confirmadas (confirma P13, com ajuste): com processo em Enviado para Backoffice, o setor de Cadastro não pode pedir cancelamento; em Devolvido para correção, pode, com motivo; em cliente Ativo sem pedido aberto, pode, com motivo, e o Backoffice só avalia; processo em Rascunho não é cancelado. RN13 e RF17 reescritos. | Resposta à pergunta 28 |
| 2026-11-02 | Um cliente Cancelado pode ser reaberto e segue o processo de aprovação. Substitui a regra, ainda não confirmada, de que cadastro cancelado não reabre. Incluída RN27. | Resposta à pergunta 28 |
| 2026-11-02 | A reabertura substitui o novo cadastro para CPF cancelado: a consulta oferece reabrir o cadastro existente, com o mesmo Id Cliente, os campos já preenchidos e todo o histórico, e cada CPF passa a ter um único cliente. Substitui a resposta à pergunta 23 sobre novo Id Cliente, reaproveitamento e vários cancelamentos. RN04, RN19, RF25, 5.6 e seção 8 reescritos. | Resposta à pergunta 28 |
| 2026-11-02 | No pedido de cancelamento com processo em Devolvido para correção, o processo devolvido termina em Alterações Descartadas e um novo processo de cancelamento começa em Rascunho. Substitui a passagem direta do processo devolvido para Enviado para Backoffice, proposta na pergunta 21. | Resposta à pergunta 28 |
| 2026-11-02 | Um cliente Novo não pode ser cancelado; o cancelamento fica restrito a clientes Ativos, sem novo status de processo. RN13 reescrita. | Resposta à pergunta 29 |
| 2026-11-02 | No descarte do primeiro processo, ele termina em Alterações Descartadas, o cliente deixa de existir como Novo e o CPF fica livre para um novo cadastro, mantendo-se apenas o histórico. Amplia Alterações Descartadas, antes restrita a pedidos, e substitui o entendimento de que todo CPF iniciado fica retido. Incluída RN25. | Resposta à pergunta 30 |
| 2026-11-02 | Cada cliente tem no máximo um processo aberto por vez. O rascunho de pedido pode ficar parado indefinidamente, pode ser descartado a qualquer momento, sem publicação, e pode ser retomado ou descartado por qualquer usuário do setor de Cadastro. O rascunho do primeiro processo também pode ser descartado. Substitui a desistência restrita a pedidos devolvidos. RF19 e 5.10 reescritos; incluídos RF31 e RN24. | Resposta à pergunta 31 |
| 2026-11-02 | O CPF só pode ser alterado enquanto o cliente estiver Novo. Se o CPF de um cliente Ativo estiver errado, o setor de Cadastro pede o cancelamento e inicia um novo cadastro com o CPF correto; um cliente Cancelado reaberto não pode trocar de CPF. Substitui a resposta à pergunta 24. RF29 e RN23 reescritos. | Respostas às perguntas 32 e 34 |
| 2026-11-02 | A cada edição do CPF, o sistema o verifica: sem cadastro, aceita; cliente Ativo sem processo aberto, pergunta sobre pedido de alteração ou de cancelamento; cliente Cancelado sem processo aberto, pergunta sobre reabertura; cliente Novo ou com processo aberto, recusa, com "cadastro já iniciado" e link. Substitui a validação anterior, que apenas recusava CPF de cliente Novo ou Ativo. Incluídos 5.12 e RN26. | Respostas às perguntas 32 e 33 |
| 2026-11-02 | Se o usuário aceitar iniciar outro processo na edição do CPF, o sistema avisa antes e, com a confirmação, o cadastro em edição termina em Alterações Descartadas, o cliente Novo deixa de existir e o CPF original fica livre. Incluídos RF30 e RN28. | Resposta à pergunta 33 |
| 2026-11-02 | Versão 6. Reabertura definida (confirma P14): pedido com motivo obrigatório, que abre novo processo em Rascunho, com o mesmo Id Cliente, Cancelado nos dados atuais e Ativo nos dados novos, a partir da consulta de CPF ou da verificação na edição; todos os campos são editáveis, exceto o CPF. No aceite, o cliente volta a Ativo; na devolução, o processo vai para Devolvido para correção; no descarte, em Rascunho ou Devolvido para correção, termina em Alterações Descartadas e o cliente continua Cancelado. Substitui a descrição genérica de "processo de aprovação". Transições de 5.5 e 5.6 reescritas; RF19, RF20, RF25, RN03, RN14, RN15 e RN27 atualizados. | Respostas às perguntas 38 e 39 |
| 2026-11-02 | No aceite da reabertura, publicam-se o histórico do que mudou e os novos valores dos campos, indicando a reabertura. Incluído RF32; seção 10 atualizada. | Resposta à pergunta 38 |
| 2026-11-02 | O setor de Cadastro vê na tela de status todos os cadastros, de qualquer usuário do setor. O Backoffice usa a consulta de CPF e a tela de status, com a mesma visão, mas não pode iniciar um novo cadastro a partir da consulta (confirma P05). RF03, RF09 e RN02 atualizados. RF24 passa a valer para cliente Cancelado sem processo aberto, porque um pedido de reabertura precisa aparecer para avaliação do Backoffice. | Resposta à pergunta 9 |
| 2026-11-02 | Edição simultânea: dois usuários podem abrir o mesmo cadastro, mas quem salvar depois de outra pessoa vê um aviso e precisa recarregar os dados. Incluídos 5.13, RF34 e RN29. | Resposta à pergunta 10 |
| 2026-11-02 | Lista única de processos em Enviado para Backoffice, que qualquer usuário do Backoffice pode analisar, sem atribuição. Incluídos RF33 e RN32. | Resposta à pergunta 10 |
| 2026-11-02 | Um mesmo usuário pode ter os dois perfis, mas não pode aceitar nem devolver um processo que ele mesmo enviou. Incluídos RF35 e RN31; seções 3, 5.5 e 9 atualizadas. | Resposta à pergunta 10 |
| 2026-11-02 | O aviso com o botão de consultar status aparece ao enviar para o Backoffice; ao salvar um rascunho, aparece só uma confirmação simples. Substitui o momento indefinido "ao ser realizado". RF06 e RF11 reescritos; 5.1 e 5.2 ajustados. | Resposta à pergunta 8 |
| 2026-11-02 | Quando um cliente Cancelado tem CPF de outra pessoa, o caminho é reabrir e substituir os dados pelos da pessoa correta, com motivo e aprovação do Backoffice; o histórico guarda tudo, a regra de um cliente por CPF continua valendo e as outras áreas recebem a mudança como uma reabertura. Incluída RN30. | Resposta à pergunta 40 |
| 2026-11-02 | Versão 7. O sistema de terceiro deixa de ser considerado: o PRD trata este como o primeiro sistema de cadastro da empresa. Substitui as decisões anteriores sobre substituição, consulta, migração e convivência. Seção 1 e objetivo reescritos com o texto confirmado; retirados os dois itens de 4.2 e RN05, sem reutilização do identificador; seção 10 passa a tratar só de integrações. A consulta de CPF continua considerando somente os cadastros do próprio sistema, agora em RF03 e RN04. | Decisão do stakeholder; pergunta 12 encerrada |
| 2026-11-02 | O aviso de "cadastro realizado" aparece em todo envio ao Backoffice, inclusive reenvios e pedidos. RF06 atualizado. | Confirmação de interpretação |
| 2026-11-02 | O cliente Cancelado não aparece como pendente, exceto quando há um processo aberto, como um pedido de reabertura. RF24 atualizado. | Confirmação de interpretação |
| 2026-11-02 | Só o setor de Cadastro pode iniciar a reabertura; o Backoffice apenas a avalia. Perfil Backoffice e RN27 atualizados. | Confirmação de interpretação |
| 2026-11-02 | Se dois usuários do Backoffice agirem no mesmo processo, o segundo vê um aviso de que o processo já foi decidido, e sua ação não é aplicada. Incluídos 5.14, RF37 e RN33. | Resposta à pergunta 44 |
| 2026-11-02 | A restrição de não aceitar nem devolver o que o próprio usuário enviou considera qualquer envio daquele processo, não só o último. RF35 e RN31 atualizados. | Resposta à pergunta 45 |
| 2026-11-02 | O envio sem salvar antes é permitido, confirmando a transição mantida até aqui, e é possível salvar uma correção em Devolvido para correção sem reenviar. Incluídos a transição correspondente e RN34; RF11 atualizado. | Resposta à pergunta 36 |
| 2026-11-02 | Outro usuário do setor de Cadastro pode assumir um rascunho do primeiro processo, como já vale para rascunhos de pedido. RF31 e 5.2 atualizados. | Resposta à pergunta 26 |
| 2026-11-02 | Na edição do CPF, se o usuário recusar abrir um pedido ou reabrir um cliente, o CPF digitado é recusado e a edição continua com o anterior. A consulta mostra o status do cliente e oferece as mesmas ações da edição. RF04, RN26 e 5.4 atualizados; incluído RF36. | Resposta à pergunta 42 |
| 2026-11-02 | Ativo fica nos dados atuais depois do aceite do primeiro processo, e o que foi pedido em uma desistência só permanece no histórico. RN15 e 5.5 atualizados. | Resposta à pergunta 35 |
| 2026-11-02 | Pergunta 37 encerrada, já que a reabertura mantém o mesmo cliente. | Resposta à pergunta 37 |
