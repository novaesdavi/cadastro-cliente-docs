# Pré-PRD — Sistema de Cadastro de Novos Clientes

Última atualização: 2026-11-02

## Insumos recebidos

### 2026-10-25 — Primeiro insumo do stakeholder (texto original)

> tenho a necessidade de um sistema de cadastro de novos clientes de uma empresa, pois a empresa esta realizando o cadastro através de um sistema de terceiro que está em back level e não tem mais manutenção necessária. Nesse novo sistema, terei uma página web com autenticação e tenha perfis de acesso para diferentes  usuários. Esse cadastro é preenchido em tela e quando cadastrado é enviado para verificação e análise para o setor de backoffice que não pode cadastrar novos usuários, mas pode ajustar cadastros já iniciados pelo primeiro setor (setor de cadastro). Quando não há problemas de preenchimento o cadastro é concluído e o primeiro setor poderá ver a tela de status com o status concluído.
> Ao preencher o novo cadastro, preciso ter um aviso que indique que o cadastro foi realizar e que exista um botão de consulta de status.
> Antes de cadastrar um novo cliente preciso consultar o CPF para analisar se o cliente já existe, e se existir ele deve ver a mensagem de cadastro já iniciado e um link para consultar os dados cadastrais do cliente. a pesquisa precisa estar numa tela, o preenchimento e edição em outra. Acredito que possa ter a mesma tela, mas com funções distintas por área como área de cadastro e área de backoffice.

Material de apoio consultado (somente para perguntas e orientações, não como fonte de requisitos): `treinamento_ai_squad_autonoma_cadastro_clientes.md`.

### 2026-10-25 — Segundo insumo: respostas às perguntas bloqueantes 1 a 7 (texto original)

> **1.** os usuários do backoffice não pode cadastrar novos clientes. Não haverá um perfil administrador, isso fiocará fora desse sistema, talvez dentro da infra do próprio sistema, mas não será contemplado fluxo de administrador.
>
> **2.** Pode ter um rascunho sim, podemos ter o botão salvar e o enviar para backoffice.
>
> **3.** Precisa ter um botão Devolver para correção, mas deverá ser incluído o motivo da devolução num campo de "motivo". Quam marca o cadastro como concluído éo Backoffice mesmo. Deve haver os status Rascunho, Enviado para Backoffice, devolvido para correção, aceito e enviado para processamento, que é quando o Backoffice aceitou o cadastro e enviou para outra área fora desse escopo.
>
> **4.** Quando CPF já existe o sistema deve sim impedir um novo cadastro mesmo que esteja em análise. Mas é possível consultar o CPF na tela de status de cadastros para ver o status desse CPF. Todos podem abrir os dados castrais, se estiver para o time de castro, pode editar, mas se estiver como em analise do Backoffice ou concluído, o backoffice precisa devolver cadastro solitando ajuste, mesmo após concluído.
>
> **5.** deve prodcurar dado somente no próprio sistema. Não haverá migração. Irá funcionar em paralelo somente até a publicação e liberação desse novo.
>
> **6.** Devem ser preenchidos: Nome, e-mail, telefone, data nascimento , endereço e CPF. somente nome e CPF devem ser obrigatórios.
>
> **7.** Vo saber que deu certo depois de 10 cadstros feitos pela área de cadastro.

Perguntas 8 a 14 da rodada anterior: sem resposta.

### 2026-11-02 — Terceiro insumo: respostas às perguntas bloqueantes 1 a 7

Respostas coletadas uma a uma em conversa, na ordem abaixo. As falas originais estão entre aspas.

**Status (pergunta 1)**

- "Concluído" é o mesmo que "Aceito e enviado para processamento": sim.
- "Em análise do Backoffice" é o mesmo que "Enviado para Backoffice": sim.

**Correção, recusa e cancelamento (pergunta 4)**

- Após corrigir um cadastro devolvido, o setor de Cadastro reenvia por "Enviar para Backoffice" e ele volta a Enviado para Backoffice: sim.
- Motivo visível a quem corrige: "sim, precisa de um campo mensagem de devolução, mas também vamos precisar de um local para exibição do histórico de mensagens e mudanças de status para o cadastro". A "mensagem de devolução" é o mesmo campo "motivo" já existente (confirmado).
- Recusa: "Sim, ele pode devolver, aceitar e também cancelar o cadastro para que seja preenchido do zero novamente, e assim o cadastro deve aparecer em consultas do cpf, mas não irá mais aparecer como pendente para nenhum setor". O nome de status "Cancelado" foi usado na conversa e o stakeholder o adotou em suas falas.
- "da forma como está o fluxo, cancelado e Aceito, podem ser o ultimo status de um cadastro e antes de uma pessoa do cadastro querer incluir um novo cadastro deve ser validado se o cadastro já existe na base. o time do cadastro pode inclusive, obter um cadastro já ativo e aceito e mudar ele para o status cancelado, mas antes precisa passar pela aceitação do Backoffice".
- Depois de um cadastro cancelado, o setor de Cadastro pode iniciar novo cadastro para o mesmo CPF: "sim, e reaproveita os campos do cadastro anterior". Isso substitui o "preenchido do zero".
- O Backoffice deixa de poder devolver um cadastro aceito? "Não", ou seja, a devolução após o aceite continua valendo. Aceito pode ser o último status, mas não é definitivo.
- Antes e depois: "a necessidade de um local para colocar o antes e o depois dos campos alterados. exemplo status de concluído para cancelado, mas o status é Enviado para backoffice, e se o backoffice devolver aparece Devolvido para correção mostrando os campos alterados inicialmente".
- Fluxo de cancelamento confirmado: (1) o setor de Cadastro pede o cancelamento de um cadastro aceito; (2) o cadastro passa a Enviado para Backoffice e o sistema mostra a alteração pedida (de Aceito e enviado para processamento para Cancelado), sem status novo como "Cancelamento solicitado"; (3) se o Backoffice aceitar, passa a Cancelado; (4) se o Backoffice devolver, passa a Devolvido para correção e continua mostrando as alterações pedidas.
- Se o Backoffice devolver e o setor de Cadastro desistir do cancelamento: o setor de Cadastro desfaz o pedido e o cadastro volta direto a Aceito e enviado para processamento, sem novo envio à outra área.
- O setor de Cadastro também pode pedir a alteração de dados de um cadastro aceito pelo mesmo fluxo: sim, mostrando o antes e o depois dos campos, e o Backoffice aceita ou devolve.
- O antes e o depois aparece para toda alteração de campo ou status, em qualquer momento, no histórico do cadastro.
- Cancelar exige motivo (tanto no pedido do setor de Cadastro quanto no cancelamento feito pelo Backoffice): sim, é obrigatório e entra no histórico.
- Status em que o cancelamento pode acontecer: "todos os status podem ir levar ao cancelamento, exceto rascunho, todos os status podem ficar largado em rascunho e nunca sair". Um rascunho não é cancelado e pode ficar parado indefinidamente.

**Envio para processamento (pergunta 3)**

- "é o envio para outras áreas da empresa que realmente irão utilizar o cadastro, enquanto não sair da área de cadastro e backoffice, o cadastro não pode ir para as demais. As outras áreas podem utilizar o cadastro para criar conta, criar perfil de usuário e outras features e produtos da empresa".
- "será enviado via tópico para ser consumido pelas área interessados em mudanças cadastrais ou novos cadastros". A publicação em tópico é uma restrição real declarada pelo stakeholder.
- "certo, então cadastros cancelados realmente precisam ser enviados sim. deve ser enviado o histórico do que foi alterado, e os campos novos". Isso substitui a fala anterior "cadastro cancelado não é enviado para processamento".

**Ajuste pelo Backoffice (pergunta 2)**

- O Backoffice pode alterar os dados diretamente, sem devolver? "Não". Todo ajuste passa pela devolução; o Backoffice só devolve, aceita ou cancela.

**Campos (pergunta 5)**

- Validações confirmadas: Nome não pode ficar em branco; CPF com 11 dígitos e dígitos verificadores válidos; e-mail em formato válido (nome@dominio); telefone com DDD e número válidos; data de nascimento válida e não futura. Não existe idade mínima.
- Endereço dividido em campos: CEP, rua, número, complemento, bairro, cidade e UF. O endereço segue opcional, mas, se qualquer campo for preenchido, todos os demais passam a ser obrigatórios, exceto complemento.
- CPF inválido: o sistema mostra mensagem de CPF inválido, não faz a consulta e o cadastro não pode ser iniciado.
- O Nome é exigido já ao salvar o rascunho.
- As validações também são exigidas ao salvar o rascunho (um rascunho não pode ser salvo com campo inválido).
- Não há documentos a anexar.

**Auditoria e dados pessoais (pergunta 7)**

- Cada registro do histórico guarda usuário, data e hora da ação, e os dois perfis consultam o histórico de qualquer cadastro: confirmado.
- Nenhum dado é mascarado; os dois perfis veem tudo.
- Sem prazo de guarda definido nesta versão: os dados são mantidos e não há exclusão automática. Foi recomendado ao stakeholder validar isso com a área responsável pela LGPD.

**Meta e escopo (pergunta 6)**

- Conta como cadastro feito o cadastro aceito pelo Backoffice e publicado no tópico. Sem prazo para atingir os 10 cadastros.
- Ficam fora da primeira versão: comunicação com o cliente (e-mail ou SMS de confirmação); notificações aos usuários (como avisos de cadastro devolvido); relatórios e painéis gerenciais; aplicativo móvel; acesso direto do cliente para preencher ou consultar o próprio cadastro.

**Interpretações apresentadas e não confirmadas explicitamente**

O stakeholder foi avisado destas interpretações e não se opôs, mas não as confirmou: ver P11 e P12.

Perguntas 8 a 14, P05 e P06: sem resposta nesta rodada.

### 2026-11-02 — Quarto insumo: respostas às perguntas 15 a 25 e modelo de dois níveis

**Tabela enviada pelo stakeholder (versão limpa, que substitui uma anterior)**

```text
Cadastro concluído    dados atuais    dados novos
Status cadastro Cliemte            Id Cliente    Status processo Backoffice    Id Processo
        Novo    1    Rascunho    1
        Novo    1    Enviado para Backoffice    1
        Novo    1    Devolvido para correção    1
        Ativo    1    Aceito e enviado para processamento    1

Cadastro cancelado (já ativo)
    Ativo    Cancelado    1    Rascunho    2
    Ativo    Cancelado    1    Enviado para Backoffice    2
    Ativo    Cancelado    1    Devolvido para correção    2
    Cancelado    Cancelado    1    Aceito e enviado para processamento    2

Desistencia de cancelamento ou outra alteração
    Ativo    Cancelado    1    Rascunho    3
    Ativo    Cancelado    1    Enviado para Backoffice    3
    Ativo    Cancelado    1    Devolvido para correção    3
    Ativo    Cancelado    1    Alterações Descartadas    3
```

**Modelo confirmado pelo stakeholder (substitui o ciclo de vida anterior de 5.5)**

- Dois níveis. Cadastro do cliente: identificado por Id Cliente, que não muda, com status Novo (primeiro processo ainda não aceito), Ativo (primeiro processo aceito) e Cancelado (pedido de cancelamento aceito). Processo no Backoffice: identificado por Id Processo, um novo a cada mudança, com status Rascunho, Enviado para Backoffice, Devolvido para correção, Aceito e enviado para processamento e Alterações Descartadas.
- "Cancelado" deixa de ser status do processo e passa a ser status do cliente. O processo de cancelamento termina em Aceito e enviado para processamento.
- O status vigente do cliente é o de "dados atuais"; o pedido fica em "dados novos". Enquanto um pedido está pendente, o cliente continua Ativo.
- Ao aceitar um processo, os dados novos sempre passam a ser os dados atuais.
- Pedidos de alteração ou cancelamento abrem um novo processo que começa em Rascunho (substitui "vai direto para Enviado para Backoffice").
- Desistência de pedido de cancelamento ou de alteração: o processo termina em Alterações Descartadas, os valores pedidos são descartados e o cliente continua Ativo (substitui "volta direto para Aceito"). Sem nova publicação no tópico.
- Os processos 2 e 3 da tabela são cenários alternativos, não uma sequência.

**Respostas**

- Pergunta 15: "um cadastro aceito para correção não pode ser devolvido pelo backoffice, ele precisa ser localizado pelo time de cadastro, e então enviado para o backoffice avaliar". Isso substitui a fala anterior "mesmo após concluído" e a resposta anterior "i) Não", dada sobre o Backoffice deixar de poder devolver um cadastro aceito. Só o setor de Cadastro reabre um cadastro aceito, por pedido de alteração ou cancelamento que o Backoffice avalia. A pergunta 15 deixa de existir.
- Perguntas 16 e 17 (confirma P11): publicação no tópico. Primeiro aceite: todos os dados do cadastro. Backoffice aceita pedido de alteração: histórico do que mudou e novos valores dos campos. Backoffice aceita pedido de cancelamento: histórico do que mudou e novos valores dos campos, indicando o cancelamento. Pedido pendente, devolvido ou desfeito: nada.
- Pergunta 18: o tópico só recebe o cancelamento de um cadastro que já tinha sido aceito.
- Pergunta 19: os dados aceitos anteriormente continuam valendo para as outras áreas até o Backoffice aceitar o pedido. As áreas não são avisadas do pedido pendente.
- Pergunta 20: se a publicação falhar, o status não muda; o Backoffice vê uma mensagem de erro e precisa aceitar novamente.
- Pergunta 21: "Status atual Enviado para Bacoffice = Backoffice pode devolver para correção colocando no motivo a orientação para cancelar, mas não pode cancelar diretamente." O Backoffice nunca cancela diretamente, o que substitui a resposta anterior de que ele podia cancelar; o cancelamento só acontece quando o setor de Cadastro pede e o Backoffice aceita. Foi proposta uma tabela e o stakeholder só ajustou esse ponto. Os itens restantes da tabela foram avisados a ele, que não se opôs, mas não os confirmou expressamente: ver P13.
- Pergunta 22: o pedido de alteração de dados exige motivo, que entra no histórico. A desistência segue o modelo acima.
- Pergunta 23 (confirmada): a consulta de CPF mostra que existe cadastro cancelado, com link para ver os dados, e permite iniciar um novo; a mensagem "cadastro já iniciado" fica só para CPF com cliente Novo ou Ativo. O novo cadastro recebe novo Id Cliente, e o cancelado permanece como está, com seu histórico. Os campos vêm preenchidos automaticamente e todos podem ser editados, exceto o CPF nesse reaproveitamento inicial. Com vários cancelamentos, são reaproveitados os dados do mais recente. O novo cadastro começa como cliente Novo, no processo 1, em Rascunho.
- Pergunta 24: o setor de Cadastro pode alterar o CPF em qualquer processo que esteja editando. O sistema valida o novo CPF e não aceita um que já tenha cliente Novo ou Ativo.
- Pergunta 25 (confirma P12): a regra do endereço completo também vale ao salvar o rascunho. CEP com 8 dígitos e UF com uma das 27 siglas válidas do Brasil.

Perguntas 8 a 14, 26 e 27, P05 e P06: sem resposta nesta rodada.

### 2026-11-02 — Quinto insumo: respostas às perguntas 28 a 34

**Pergunta 28: regras de cancelamento (confirma P13, com um ajuste)**

- Confirmadas: em Enviado para Backoffice, o setor de Cadastro não pode pedir cancelamento; em Devolvido para correção, ele pode pedir, com motivo; em cliente Ativo sem pedido aberto, ele pode pedir, com motivo, e o Backoffice só avalia; processo em Rascunho não é cancelado.
- Ajuste, nas palavras do stakeholder: "Ciente Cancelado pode ser reaberto e segue o processo de aprovação." Isso substitui a regra de que cadastro cancelado não reabre.
- A reabertura funciona como as demais mudanças: novo processo, com Cancelado em dados atuais e Ativo em dados novos. No aceite, o cliente volta a Ativo e o sistema publica no tópico. O stakeholder foi avisado desta interpretação e não se opôs, mas não a confirmou expressamente: ver P14.
- Reabertura e novo cadastro (confirmado, opção 1): a reabertura substitui o novo cadastro para CPF cancelado. A consulta de CPF cancelado oferece reabrir o cadastro existente, com o mesmo Id Cliente, os campos já preenchidos e todo o histórico. Cada CPF passa a ter um único cliente. Isso substitui a resposta à pergunta 23 sobre novo Id Cliente, reaproveitamento e vários cancelamentos.
- Pedido de cancelamento em processo devolvido (confirmado, opção 1): o processo devolvido termina em Alterações Descartadas, e um novo processo de cancelamento começa em Rascunho.

**Pergunta 29: cancelamento de cliente Novo**

- "um cliente novo não pode ser cancelado, somente outros campos podem ser editados, o que pode ser feito é descartar as alterações". O cancelamento fica restrito a clientes Ativos. A pergunta 29 fica encerrada, sem novo status de processo.

**Pergunta 30: descarte no primeiro processo (confirmado, opção 3)**

- O processo termina em Alterações Descartadas, o cliente deixa de existir como Novo e o CPF fica livre para um novo cadastro, mantendo apenas o histórico.

**Pergunta 31: rascunhos e pedidos simultâneos**

O stakeholder respondeu "sim". Foi avisado de que isso vale para os dois pontos abaixo e não se opôs.

- Cada cliente tem no máximo um processo aberto por vez; só depois de encerrado é possível abrir outro.
- Um rascunho de pedido pode ficar parado indefinidamente; enquanto isso, o cliente segue com os dados atuais.
- O setor de Cadastro pode descartar um rascunho de pedido a qualquer momento: o processo termina em Alterações Descartadas, sem publicação.
- Qualquer usuário do setor de Cadastro pode retomar ou descartar um rascunho esquecido por outro usuário.
- Um rascunho do primeiro processo também pode ser descartado, com o resultado da pergunta 30.

**Perguntas 32 e 34: alteração do CPF (opção 1)**

- "opcao 1 e sempre que esse CPF for editado, é necessário verifdicar se existe algum cadastro para aquele cpf, e se existir, e for possível de acordo com outras regras, perguntar se o usuário que iniciar outro processo com o cpf indicado".
- O CPF só pode ser alterado enquanto o cliente estiver como Novo. Se o CPF de um cliente Ativo estiver errado, o setor de Cadastro pede o cancelamento e inicia um novo cadastro com o CPF correto. Isso substitui a resposta à pergunta 24. As perguntas 32 e 34 ficam encerradas.
- Um cliente Cancelado reaberto não pode trocar de CPF.

**Pergunta 33: CPF informado na edição (confirmado)**

A cada edição do CPF, o sistema verifica o CPF informado:

- Sem cadastro: aceita o CPF e segue a edição.
- Cliente Ativo sem processo aberto: pergunta se o usuário quer abrir um pedido de alteração ou de cancelamento para esse cliente.
- Cliente Cancelado sem processo aberto: pergunta se o usuário quer reabrir esse cliente.
- Cliente Novo ou qualquer cliente com processo aberto: não permite iniciar outro processo, mostra "cadastro já iniciado" e o link para consultar os dados, e recusa o CPF digitado.

Se o usuário aceitar iniciar outro processo (confirmado, opção 1): o sistema avisa antes e, com a confirmação, o cadastro em edição é descartado. Ele termina em Alterações Descartadas, o cliente Novo deixa de existir e o CPF original fica livre.

Perguntas 8 a 14, 26, 27 e 35 a 37, P05 e P06: sem resposta nesta rodada.

### 2026-11-02 — Sexto insumo: respostas às perguntas 38, 39, 9, 10, 8 e 40

**Perguntas 38 e 39: reabertura (confirma P14; tabela confirmada expressamente)**

- Início: a reabertura abre um novo processo, em Rascunho, com o mesmo Id Cliente. Pode partir da consulta de CPF ou da verificação na edição.
- Dados: Cancelado em dados atuais e Ativo em dados novos, com os campos já preenchidos.
- Campos: todos podem ser editados, exceto o CPF.
- Motivo: obrigatório, como nos demais pedidos, e entra no histórico.
- Aceite: o cliente volta a Ativo, e os dados novos passam a ser os dados atuais.
- Devolução: o processo vai para Devolvido para correção, como os demais.
- Descarte: pode ocorrer em Rascunho ou Devolvido para correção. O processo termina em Alterações Descartadas e o cliente continua Cancelado.
- Publicação no aceite (opção 1): o histórico do que mudou e os novos valores dos campos, indicando a reabertura, como nos demais pedidos.

**Pergunta 9 (confirma P05)**

- O setor de Cadastro vê na tela de status todos os cadastros, de qualquer usuário do setor.
- O Backoffice usa a consulta de CPF e a tela de status, com a mesma visão dos cadastros, mas não pode iniciar um novo cadastro a partir da consulta.

**Pergunta 10**

- Edição simultânea (opção 1): dois usuários podem abrir o mesmo cadastro, mas quem salvar por último, depois de outra pessoa já ter salvado, vê um aviso e precisa recarregar os dados antes de continuar. Nenhuma alteração é sobrescrita sem que o usuário saiba.
- Fila do Backoffice (opção 1): há uma lista única de processos em Enviado para Backoffice, e qualquer usuário do Backoffice pode analisar qualquer um, sem atribuição.
- Dois perfis (opção 2): um mesmo usuário pode ter os dois perfis, mas não pode aceitar nem devolver um processo que ele mesmo enviou.

**Pergunta 8**

- O aviso com o botão de consultar status aparece ao enviar para o Backoffice. Ao salvar um rascunho, aparece só uma confirmação simples de que foi salvo.

**Pergunta 40 (opção 1)**

- Quando um cliente Cancelado tem CPF que pertence a outra pessoa, o caminho é reabrir e substituir os dados pelos da pessoa correta, com motivo e aprovação do Backoffice. O histórico guarda tudo, e a regra de um cliente por CPF continua valendo. As outras áreas recebem a mudança como uma reabertura, com o antes e o depois dos campos.

Perguntas 11 a 14, 26, 27, 35 a 37, 41 a 43 e P06: sem resposta nesta rodada.

### 2026-11-02 — Sétimo insumo: sistema de terceiro, interpretações e perguntas não bloqueantes

**Sistema de terceiro removido do PRD**

- "não precisa considerar o sistema de terceiro, aja como se não houvesse sistema de terceiro, e atue como se esse fosse o primeiro sistema de cadastro na empresa". A pergunta 12 fica encerrada.
- Contexto e problema confirmado: "a empresa precisa de um sistema para cadastrar novos clientes, com verificação do Backoffice antes de os dados chegarem às outras áreas, que os usam para criar contas, perfis de usuário e em outros produtos."
- Objetivo confirmado: "permitir que o setor de Cadastro registre novos clientes e que somente cadastros aceitos pelo Backoffice sejam enviados às demais áreas."
- Alterações confirmadas: a métrica de sucesso não muda; a seção 4.2 perde a consulta ao sistema de terceiro e a migração; RN05 é retirada, sem reutilizar o número; a seção 10 fica só com a publicação no tópico; a regra de que a consulta de CPF olha os cadastros do próprio sistema continua valendo, sem citar outro sistema; o histórico é mantido.

**Interpretações confirmadas**

- a) O aviso de "cadastro realizado" aparece em todo envio ao Backoffice, inclusive reenvios e pedidos.
- b) O cliente Cancelado não aparece como pendente, exceto quando há um processo aberto, como um pedido de reabertura.
- c) Só o setor de Cadastro pode iniciar a reabertura; o Backoffice apenas a avalia.

**Respostas às perguntas não bloqueantes (sugestões aceitas)**

- 44: se dois usuários do Backoffice agirem no mesmo processo, o segundo vê um aviso de que o processo já foi decidido, e sua ação não é aplicada.
- 45: a restrição de não aceitar nem devolver o que o próprio usuário enviou considera qualquer envio daquele processo, não só o último.
- 36: o envio sem salvar antes é permitido, e também é possível salvar uma correção em Devolvido para correção sem reenviar.
- 26: outro usuário do setor de Cadastro pode assumir um rascunho do primeiro processo, como já vale para rascunhos de pedido.
- 42: na edição do CPF, se o usuário recusar abrir um pedido ou reabrir um cliente, o CPF digitado é recusado e a edição continua com o anterior. A consulta mostra o status do cliente e oferece as mesmas ações da edição.
- 35: encerrada. "Ativo" fica em dados atuais depois do aceite do primeiro processo, e o que foi pedido em uma desistência só permanece no histórico.
- 37: encerrada, já que a reabertura mantém o mesmo cliente.

**Perguntas adiadas pelo stakeholder**

As perguntas 11, 13 (P06), 14, 27, 41 e 43 ficam adiadas.

## Premissas a validar

Resolvidas em 2026-10-25 (registradas no histórico do PRD): P01 confirmada, P02 confirmada, P03 negada (existe rascunho), P04 confirmada.

Resolvidas em 2026-11-02 (registradas no histórico do PRD): P07, P08, P09, P10, P11 e P12 confirmadas; P13 confirmada, com o ajuste de que cliente Cancelado pode ser reaberto; P05 e P14 confirmadas.

| ID | Interpretação | Motivo | Seção do PRD afetada |
|---|---|---|---|
| P06 | [Adiada pelo stakeholder] Pesquisa e preenchimento/edição podem ser a mesma tela para as duas áreas, com funções diferentes por área. | Foi dito como "acredito que possa ter"; é sugestão, não confirmação. Também é detalhe de solução, que pode não precisar estar no PRD. | 6 (RF10) |

## Conflitos e ambiguidades

- **"Cadastro já iniciado" x ações na consulta**: a resposta 42 diz que a consulta mostra o status e oferece as mesmas ações da edição, mas não retira a mensagem "cadastro já iniciado" para cliente Ativo, confirmada na resposta 23. O PRD mantém a mensagem e acrescenta as ações ao setor de Cadastro. Vale conferir isso na confirmação final.
- **Salvar correção em Devolvido para correção**: a resposta 36 permite salvar sem reenviar, mas a confirmação simples e as validações foram confirmadas ao salvar um rascunho. O PRD não estende essas regras ao salvamento da correção. O detalhe não impede a passagem ao `product-agent`.
- **Telas**: "a pesquisa precisa estar numa tela, o preenchimento e edição em outra" (afirmação) convive com "acredito que possa ter a mesma tela, mas com funções distintas por área" (sugestão). Ver P06, adiada pelo stakeholder.
- **"usuário" x "cliente"**: resolvido. No PRD, **usuário** = colaborador que opera o sistema e **cliente** = pessoa cadastrada (resposta 1).
- **"cadastro" com dois sentidos**: nome do setor (setor de Cadastro) e o registro do cliente. No PRD, usa-se "setor de Cadastro" para a área e "cadastro" para o registro.
- **Material de apoio x insumo**: o roteiro do treinamento é usado apenas para perguntas e orientações, não como fonte de requisitos.

## Perguntas abertas

Ordenadas por impacto em escopo. [BLOQUEANTE] = impede o PRD de ficar pronto. Os números não são reaproveitados, para manter a rastreabilidade: as perguntas 1 a 10, 16 a 26, 28 a 40, 42, 44 e 45 foram respondidas ou encerradas em 2026-11-02, a pergunta 15 deixou de existir, e as demais mantêm o número original.

Não há pergunta bloqueante nesta versão. As perguntas abaixo foram adiadas pelo stakeholder, não bloqueiam e não têm resposta no PRD.

- **41.** [Adiada pelo stakeholder] O histórico de um cliente Novo descartado é mantido, mas o cliente deixa de existir. Quem consegue consultar esse histórico e como? Se o mesmo CPF for cadastrado de novo, o histórico antigo aparece na consulta ou no novo cadastro, ou fica separado? A tela de status mostra esse cadastro descartado?
- **43.** [Adiada pelo stakeholder] No cadastro comum, o CPF consultado já entra preenchido no novo cadastro?
- **27.** [Adiada pelo stakeholder] Para a meta de 10 cadastros, cada cliente conta uma vez? Um cadastro aceito e depois cancelado continua contando?
- **11.** [Adiada pelo stakeholder] Existe prazo para o Backoffice analisar um cadastro? O que acontece se ele não for cumprido?
- **13.** [Adiada pelo stakeholder] A pesquisa e o preenchimento devem ser a mesma tela para as duas áreas, com funções diferentes, ou telas separadas por área? (P06)
- **14.** [Adiada pelo stakeholder] Há metas de disponibilidade, horário de uso ou volume de cadastros por dia que o sistema precisa suportar?

## Orientações

- **Guarda de dados (LGPD)**: foi recomendado validar com a área responsável pela LGPD a decisão de manter os dados sem prazo de guarda e sem exclusão automática. CPF, data de nascimento, endereço, e-mail e telefone são dados pessoais; rascunhos parados indefinidamente, cadastros cancelados e o histórico de clientes Novos descartados também ficam guardados. A mesma validação vale para a visibilidade total dos dados aos dois perfis.
- **Dados pessoais no tópico**: publicar dados e histórico para as áreas interessadas amplia quem tem acesso a dados pessoais. Vale incluir na validação com a área responsável pela LGPD quais áreas consomem o tópico e quais dados cada uma precisa receber.
- **Alteração e cancelamento após o aceite**: as áreas que consomem o tópico podem já ter criado conta ou perfil com o cadastro. Vale combinar com elas o que fazer quando um cadastro é alterado ou cancelado depois de usado, em especial quando um cliente cancelado é reaberto ou quando um CPF errado é corrigido por cancelamento e novo cadastro, e nomear um responsável por essas áreas.
- **Reabertura com dados de outra pessoa**: pela resposta 40, o mesmo Id Cliente passa a representar outra pessoa, e o histórico guarda os dados das duas. Vale avisar as áreas que consomem o tópico de que uma reabertura pode trocar a pessoa, e incluir esse caso na validação com a área responsável pela LGPD.
- **Correção de CPF de cliente Ativo**: o cancelamento e o novo cadastro com o CPF correto geram dois clientes sem vínculo definido no PRD. Vale considerar se os usuários precisam chegar de um ao outro.
- **Falha persistente na publicação**: como o único caminho é o Backoffice aceitar novamente, vale definir com quem ele fala se a falha persistir, para que os processos não fiquem parados em Enviado para Backoffice.
- **Sem notificações**: com as notificações fora da primeira versão, o setor de Cadastro só descobre um processo devolvido ao consultá-lo, e a orientação para cancelar também chega só pelo motivo. Vale considerar como esse acompanhamento será feito na rotina.
- **Segregação de funções**: como um usuário não pode aceitar nem devolver um processo do qual tenha feito qualquer envio, vale garantir que sempre haja outro usuário do Backoffice disponível, para que o processo não fique parado.
- **Administração de acessos**: fica fora deste sistema, mas alguém precisa criar usuários, atribuir perfis e removê-los quando o colaborador sai. Vale registrar quem é o responsável, para não bloquear a liberação.

## Checklist de prontidão

- [x] Problema e objetivo descritos, com ao menos uma métrica de sucesso. *(Métrica confirmada: 10 cadastros aceitos pelo Backoffice e publicados no tópico, sem prazo. O detalhe de contagem da pergunta 27 foi adiado pelo stakeholder.)*
- [x] Todos os perfis definidos, com permissões e proibições. *(Ações, visibilidade, consulta de CPF, lista do Backoffice, reabertura e usuário com os dois perfis definidos.)*
- [x] Escopo e fora do escopo explícitos. *(Dentro do escopo atualizado e sete itens fora do escopo confirmados.)*
- [x] Fluxo principal e fluxos alternativos/de erro descritos de ponta a ponta. *(Descritos: principal, rascunho, devolução, CPF existente, CPF inválido, reabertura, pedidos de cancelamento e de alteração, descarte, falha na publicação, verificação do CPF na edição, edição simultânea e processo já decidido.)*
- [x] Ciclo de vida (estados e transições) definido, se houver. *(Dois níveis confirmados; todo status do processo e do cliente é final declarado ou tem saída.)*
- [x] Campos, obrigatoriedade e validações definidos. *(Campos, endereço, validações, regra do rascunho e regras do CPF confirmados; sem documentos. A pergunta 43 foi adiada pelo stakeholder.)*
- [x] Regras de negócio com exceções. *(RN01 a RN04, RN06 a RN11 e RN13 a RN34 confirmadas; RN05 e RN12 retiradas. A pergunta 41 foi adiada pelo stakeholder.)*
- [x] Integrações tratadas; legado não aplicável. *(Publicação no tópico definida para primeiro aceite, alteração, cancelamento, reabertura e descarte. Por decisão do stakeholder, não há sistema anterior a considerar.)*
- [x] Requisitos não funcionais mínimos (segurança, dados sensíveis, auditoria). *(Autenticação, perfis, segregação, histórico, sem mascaramento e sem prazo de guarda confirmados. A validação com a área responsável pela LGPD segue como orientação; as metas da pergunta 14 foram adiadas pelo stakeholder.)*

Falta a confirmação final do stakeholder sobre o PRD inteiro. Até lá, o status do PRD permanece Rascunho.
