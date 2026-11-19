# Rascunhos de Telas — Sistema de Cadastro de Novos Clientes (MVP)

Estes são rascunhos de baixa fidelidade das telas do MVP. Mostram o que cada tela contém e quais ações cada perfil vê, e não o visual final. Partem da declaração de intenção (`ideation/intent-capture/intent-statement.md`), do documento de escopo (`ideation/scope-definition/scope-document.md`) e do backlog (`ideation/scope-definition/intent-backlog.md`).

## Decisões de design

| Tema | Decisão | Fonte |
|---|---|---|
| Aparelhos | Só computador, pelo navegador no desktop | Q1 de `rough-mockups-questions.md` |
| Visual | Não há identidade visual nem sistema de design; as telas têm visual simples e neutro | Q2 |
| Acessibilidade | WCAG 2.1 nível AA, incluindo uso só com o teclado e leitor de tela | Q3 |
| Entrada | Os dois perfis entram na tela de status e daí vão para o que precisam fazer | Q4 |
| Telas | Todas as telas do PRD são desenhadas | Q5 |
| Formulário | Uma tela só, com seções de dados pessoais, contato e endereço | Q6 |
| Motivo | Janela de confirmação com o campo de motivo, aberta pela ação | Q7 |

Os desenhos usam só caracteres básicos e, por isso, aparecem sem acentos. Nas telas reais, os textos têm acentos. Nomes, CPFs e datas são exemplos.

## Telas e as capacidades do backlog

| Tela | Parte do backlog | Requisitos do PRD |
|---|---|---|
| S01 Login | 1. Acesso e perfis | RF01, RF02 |
| S02 Tela de status | 5. Status, dados e histórico | RF09, RF14, RF24 |
| S03 Consulta de CPF | 2. Consulta de CPF e cadastro | RF03, RF04, RF26, RF36 |
| S04 Cadastro do cliente | 2. Consulta de CPF e cadastro; 9. Descarte e retomada | RF05, RF06, RF07, RF10, RF11, RF19, RF29, RF30, RF31, RF34 |
| S05 Dados cadastrais | 5. Status, dados e histórico | RF15, RF36 |
| S06 Histórico do cadastro | 5. Status, dados e histórico | RF21 |
| S07 Lista de processos | 3. Envio e decisão do Backoffice | RF33 |
| S08 Análise do processo | 3. Envio e decisão do Backoffice | RF12, RF13, RF35, RF37 |
| S09 Janela de motivo | 3, 6, 7 e 8 | RF12, RF17, RF18, RF25 |
| S10 Processo com pedido | 6, 7 e 8 (pedidos de alteração, cancelamento e reabertura) | RF17, RF18, RF20, RF25 |

A publicação no tópico (parte 4) não tem tela própria: acontece quando o Backoffice aceita o processo. Se a publicação falhar, a tela S08 mostra uma mensagem de erro e o status não muda (RF28).

## S01 Login

```
+------------------------------------------------------------------+
| S01 Login                                                        |
+------------------------------------------------------------------+
|                                                                  |
|   Sistema de Cadastro de Clientes                                |
|                                                                  |
|   Usuario  [____________________________]                        |
|   Senha    [____________________________]                        |
|                                                                  |
|   [ Entrar ]                                                     |
|                                                                  |
|   Mensagem de erro (login invalido) aparece aqui                 |
+------------------------------------------------------------------+
```

Acessibilidade: título h1 "Entrar"; região main com o formulário; o foco entra no campo Usuário.

## S02 Tela de status

```
+------------------------------------------------------------------+
| S02 Tela de status   (entrada dos dois perfis)                   |
+------------------------------------------------------------------+
|   Menu: [Status] [Consulta de CPF] [Processos]   Usuario: ___    |
|                                                                  |
|   Buscar por CPF [______________] [ Buscar ]                     |
|                                                                  |
|   CPF            Nome         Cliente    Processo        Id Proc |
|   -------------  -----------  ---------  --------------  ------- |
|   111.222.333-4  Ana Souza    Novo       Rascunho        1       |
|   555.666.777-8  Rui Lima     Ativo      Enviado p/ BO   3       |
|   999.888.777-6  Eva Costa    Cancelado  Devolvido       2       |
|                                                                  |
|   Cada linha abre: [Dados] [Historico]                           |
|   O item Processos do menu so aparece para o perfil Backoffice   |
+------------------------------------------------------------------+
```

Acessibilidade: título h1 "Status dos cadastros"; regiões nav (menu) e main (busca e tabela); o foco entra no primeiro item do menu e a busca por CPF é o segundo ponto de parada.

## S03 Consulta de CPF

```
+------------------------------------------------------------------+
| S03 Consulta de CPF   (Setor de Cadastro e Backoffice)           |
+------------------------------------------------------------------+
|   CPF [______________]  [ Consultar ]                            |
|                                                                  |
|   Resultado, uma das situacoes abaixo:                           |
|                                                                  |
|   a) CPF invalido                                                |
|      Mensagem: CPF invalido. A consulta nao e feita.             |
|   b) Sem cadastro                                                |
|      [ Iniciar cadastro ]      (so Setor de Cadastro)            |
|   c) Cliente Novo ou Ativo, ou com processo aberto               |
|      Mensagem: cadastro ja iniciado   [ Ver dados ]              |
|      Se Ativo sem processo aberto (so Setor de Cadastro):        |
|      [ Pedir alteracao ]  [ Pedir cancelamento ]                 |
|   d) Cliente Cancelado sem processo aberto                       |
|      Cadastro cancelado existe   [ Ver dados ]                   |
|      [ Reabrir cadastro ]      (so Setor de Cadastro)            |
+------------------------------------------------------------------+
```

Acessibilidade: título h1 "Consulta de CPF"; regiões nav e main; o foco entra no campo CPF, e o resultado é anunciado por leitor de tela quando aparece.

## S04 Cadastro do cliente

```
+------------------------------------------------------------------+
| S04 Cadastro do cliente   (Setor de Cadastro)                    |
+------------------------------------------------------------------+
|   Processo Id ___   Cliente: Novo   Status: Rascunho             |
|                                                                  |
|   Dados pessoais                                                 |
|   Nome *            [______________________________]             |
|   CPF *             [______________]                             |
|   Data nascimento   [__/__/____]                                 |
|                                                                  |
|   Contato                                                        |
|   E-mail            [______________________________]             |
|   Telefone          [(__) _____-____]                            |
|                                                                  |
|   Endereco  (se preencher um campo, os demais sao exigidos)      |
|   CEP [________]  Rua [________________]  Numero [_____]         |
|   Complemento [__________]  Bairro [____________]                |
|   Cidade [______________]  UF [__]                               |
|                                                                  |
|   [ Salvar ]   [ Enviar para Backoffice ]   [ Descartar ]        |
|   Erros de campo aparecem sob o campo e no topo da tela          |
+------------------------------------------------------------------+
```

Estados: ao salvar um rascunho, aparece só uma confirmação simples de que foi salvo; ao enviar, aparece o aviso de que o cadastro foi realizado e um botão para consultar o status (RF06, RF11). Se outra pessoa salvou antes, a tela avisa e pede que se recarreguem os dados (RF34). Ao trocar o CPF de um cliente Novo por um que já tem cadastro, a tela pergunta o que fazer, conforme a seção 5.12 do PRD (RF29, RF30).

Acessibilidade: título h1 "Cadastro do cliente" e h2 em cada seção; regiões nav e main; o foco entra no campo Nome, e os erros de campo são ligados ao campo e anunciados por leitor de tela.

## S05 Dados cadastrais

```
+------------------------------------------------------------------+
| S05 Dados cadastrais   (leitura, os dois perfis)                 |
+------------------------------------------------------------------+
|   Cliente Id ___   Status: Ativo    CPF ______________           |
|                                                                  |
|   Nome ____________   Nascimento ___/___/_____                   |
|   E-mail ____________   Telefone ____________                    |
|   Endereco ______________________________________                |
|                                                                  |
|   Ultimo processo Id ___   Status: Aceito e enviado              |
|                                                                  |
|   [ Ver historico ]                                              |
|   Setor de Cadastro, se Ativo sem processo aberto:               |
|   [ Pedir alteracao ]  [ Pedir cancelamento ]                    |
|   Setor de Cadastro, se Cancelado sem processo aberto:           |
|   [ Reabrir cadastro ]                                           |
+------------------------------------------------------------------+
```

Acessibilidade: título h1 "Dados cadastrais"; regiões nav e main; o foco entra no título da tela e o primeiro ponto de parada é o botão Ver histórico.

## S06 Histórico do cadastro

```
+------------------------------------------------------------------+
| S06 Historico do cadastro   (os dois perfis)                     |
+------------------------------------------------------------------+
|   Cliente Id ___   CPF ______________                            |
|                                                                  |
|   Data e hora   Usuario  Acao             Antes      Depois      |
|   ------------  -------  ---------------  ---------  ---------   |
|   02/11 10:15   Ana      Salvou rascunho  -          -           |
|   02/11 10:40   Ana      Enviou           Rascunho   Enviado     |
|   02/11 11:05   Rui      Devolveu         Enviado    Devolvido   |
|                          Motivo: ____________________            |
|                                                                  |
|   Mostra mensagens, mudancas de status e o antes e o depois      |
|   de cada campo alterado                                         |
+------------------------------------------------------------------+
```

Acessibilidade: título h1 "Histórico do cadastro"; regiões nav e main com uma tabela com cabeçalhos; o foco entra no título da tela e a tabela é navegável por teclado.

## S07 Lista de processos

```
+------------------------------------------------------------------+
| S07 Lista de processos   (so Backoffice)                         |
+------------------------------------------------------------------+
|   Processos em Enviado para Backoffice   (lista unica)           |
|                                                                  |
|   Id Proc  CPF            Nome        Enviado por  Tipo          |
|   -------  -------------  ----------  -----------  ---------     |
|   4        555.666.777-8  Rui Lima    Ana          Alteracao     |
|   5        111.222.333-4  Bia Reis    Leo          Novo          |
|   6        222.333.444-5  Teo Dias    Ana          Cancelam.     |
|                                                                  |
|   Qualquer processo pode ser aberto, sem atribuicao              |
|   [ Analisar ] em cada linha                                     |
+------------------------------------------------------------------+
```

Acessibilidade: título h1 "Processos enviados"; regiões nav e main com tabela; o foco entra no primeiro botão Analisar.

## S08 Análise do processo

```
+------------------------------------------------------------------+
| S08 Analise do processo   (so Backoffice)                        |
+------------------------------------------------------------------+
|   Processo Id ___   Tipo: Alteracao   Enviado por: Ana           |
|                                                                  |
|   Campo         Antes             Depois                         |
|   ------------  ----------------  ----------------               |
|   Telefone      (11) 90000-0000   (11) 91111-1111                |
|   Endereco: UF  SP                RJ                             |
|                                                                  |
|   Motivo do pedido: ____________________________                 |
|                                                                  |
|   [ Aceitar ]    [ Devolver para correcao ]    [ Voltar ]        |
|   Se o usuario enviou este processo, os botoes de decisao ficam  |
|   desligados, com a mensagem de que ele nao pode decidir         |
+------------------------------------------------------------------+
```

Estados: se outro usuário do Backoffice já decidiu o processo, a tela mostra um aviso de que ele já foi decidido e a ação não é aplicada (RF37). Se a publicação no tópico falhar ao aceitar, a tela mostra uma mensagem de erro, o status não muda e o usuário precisa aceitar de novo (RF28). Aceitar não pede motivo; Devolver abre a janela S09.

Acessibilidade: título h1 "Análise do processo"; regiões nav e main; o foco entra no título da tela, e os botões desligados explicam o motivo em texto, não só pela cor.

## S09 Janela de motivo

```
+------------------------------------------------------------------+
| S09 Janela de motivo   (abre pela acao)                          |
+------------------------------------------------------------------+
|   Devolver para correcao                                         |
|   (a mesma janela serve para pedido de alteracao,                |
|   de cancelamento e de reabertura)                               |
|                                                                  |
|   Motivo *                                                       |
|   [____________________________________________]                 |
|   [____________________________________________]                 |
|                                                                  |
|   [ Confirmar ]    [ Cancelar ]                                  |
|   Sem motivo, Confirmar fica desligado                           |
+------------------------------------------------------------------+
```

Acessibilidade: janela com título h2 e região de diálogo; o foco entra no campo Motivo, fica preso dentro da janela e volta ao botão que a abriu ao fechar, e a tecla Esc cancela.

## S10 Processo com pedido

```
+------------------------------------------------------------------+
| S10 Processo com pedido   (Setor de Cadastro)                    |
+------------------------------------------------------------------+
|   Processo Id ___   Pedido: Alteracao   Status: Devolvido        |
|                                                                  |
|   Motivo da devolucao (do Backoffice):                           |
|   ____________________________________________                   |
|                                                                  |
|   Alteracoes pedidas                                             |
|   Campo         Antes             Depois                         |
|   ------------  ----------------  -----------------              |
|   Telefone      (11) 90000-0000   [(11) 91111-1111]              |
|                                                                  |
|   [ Salvar correcao ]  [ Enviar para Backoffice ]                |
|   [ Descartar ]                                                  |
|   CPF nao pode ser alterado em cliente Ativo ou reaberto         |
+------------------------------------------------------------------+
```

A mesma tela serve para pedidos de alteração, de cancelamento e de reabertura, mudando o tipo do pedido e os campos mostrados. Enquanto o pedido está em Enviado para Backoffice ou Devolvido para correção, a tela mostra as alterações pedidas (RF20).

Acessibilidade: título h1 "Processo com pedido"; regiões nav e main; o foco entra no título da tela, e o motivo da devolução vem antes do formulário.

## Assumptions & Open Questions

- Hipótese: as telas de pedido de alteração, de cancelamento e de reabertura compartilham o desenho da S10. A diferença de campos entre os três tipos fica para o refinamento dos mockups.
- Hipótese: o menu da S02 é suficiente para o Setor de Cadastro chegar à Consulta de CPF e ao Backoffice chegar à lista de processos. Não foi testado com usuários.
- Pergunta aberta: a tela de status precisa de filtros por status ou só da busca por CPF? O PRD (RF09, RF14) pede a busca por CPF e a visão de todos os cadastros.
- Pergunta aberta: como a lista de processos do Backoffice é ordenada (mais antigos primeiro, por tipo)? O PRD não define.
