# Fluxo do Usuário — Sistema de Cadastro de Novos Clientes (MVP)

Este documento mostra como cada perfil circula pelas telas desenhadas em `wireframes.md`. Parte da declaração de intenção (`ideation/intent-capture/intent-statement.md`), do documento de escopo (`ideation/scope-definition/scope-document.md`) e do backlog (`ideation/scope-definition/intent-backlog.md`). Os fluxos seguem as seções 5.1 a 5.14 do PRD v7 e as decisões de `rough-mockups-questions.md` (Q4: os dois perfis entram na tela de status; Q7: o motivo é pedido numa janela).

Os desenhos usam só caracteres básicos e, por isso, aparecem sem acentos.

## Quem vê o quê

| Tela | Setor de Cadastro | Backoffice |
|---|---|---|
| S01 Login | Sim | Sim |
| S02 Tela de status | Sim | Sim |
| S03 Consulta de CPF | Sim, com as ações de iniciar cadastro, pedir e reabrir | Sim, só para consultar |
| S04 Cadastro do cliente | Sim | Não |
| S05 Dados cadastrais | Sim, com as ações de pedir e reabrir | Sim, só leitura |
| S06 Histórico do cadastro | Sim | Sim |
| S07 Lista de processos | Não | Sim |
| S08 Análise do processo | Não | Sim |
| S09 Janela de motivo | Sim, nos pedidos | Sim, ao devolver |
| S10 Processo com pedido | Sim | Não |

## Fluxo principal: do cadastro novo ao aceite

O caminho feliz segue a seção 5.1 do PRD: o Setor de Cadastro consulta o CPF, preenche e envia; o Backoffice verifica e aceita; o cadastro é publicado no tópico.

```
Setor de Cadastro
+-----------------------------+
| S01 Login                   |
+-----------------------------+
               |
               v
+-----------------------------+
| S02 Tela de status          |
+-----------------------------+
               |
               v
+-----------------------------+
| S03 Consulta de CPF         |
| CPF sem cadastro            |
+-----------------------------+
               |
               v
+-----------------------------+
| S04 Cadastro do cliente     |
| Salvar ou Enviar            |
+-----------------------------+
               |
               v
+-----------------------------+
| Aviso: cadastro realizado   |
| [ Consultar status ]        |
+-----------------------------+
               |
               v
Backoffice
+-----------------------------+
| S07 Lista de processos      |
+-----------------------------+
               |
               v
+-----------------------------+
| S08 Analise do processo     |
| Aceitar                     |
+-----------------------------+
               |
               v
+-----------------------------+
| Publicacao no topico        |
| Processo aceito e enviado   |
| Cliente passa a Ativo       |
+-----------------------------+
               |
               v
+-----------------------------+
| S02 Tela de status          |
| Setor de Cadastro consulta  |
+-----------------------------+
```

## Fluxo alternativo: devolução e correção

Segue a seção 5.3 do PRD. O Backoffice devolve o processo com motivo, e o Setor de Cadastro corrige e reenvia.

```
+-----------------------------+      +-----------------------------+
| S08 Analise do processo     |      | S09 Janela de motivo        |
| Devolver para correcao      |----->| Motivo obrigatorio          |
+-----------------------------+      +-----------------------------+
                                                    |
                                                    v
+-----------------------------+      +-----------------------------+
| S04 Cadastro do cliente     |      | Processo Devolvido          |
| Corrigir, Salvar correcao   |<-----| Setor de Cadastro ve motivo |
+-----------------------------+      +-----------------------------+
               |
               v
+-----------------------------+
| Enviar para Backoffice      |
| Volta a S07 Lista           |
+-----------------------------+
```

Em vez de corrigir, o Setor de Cadastro pode descartar o processo pela S04, ou, se o cliente estiver Ativo, pedir o cancelamento (PRD seções 5.3 e 5.7).

## Fluxo alternativo: pedidos de alteração, cancelamento e reabertura

Seguem as seções 5.6, 5.7 e 5.8 do PRD. Os três têm a mesma forma: o pedido abre um novo processo em Rascunho, com motivo, e o Backoffice aceita ou devolve.

```
+-----------------------------+      +-----------------------------+
| S03 Consulta de CPF         |      | S09 Janela de motivo        |
| ou S05 Dados cadastrais     |----->| Pedir alteracao, cancelar   |
| Pedir alteracao,            |      | ou reabrir, com motivo      |
| cancelamento ou reabertura  |      +-----------------------------+
+-----------------------------+                     |
                                                    v
                                     +-----------------------------+
                                     | S10 Processo com pedido     |
                                     | Rascunho: salvar ou enviar  |
                                     +-----------------------------+
                                                    |
                                                    v
                                     +-----------------------------+
                                     | S08 Analise do processo     |
                                     | Backoffice aceita ou        |
                                     | devolve                     |
                                     +-----------------------------+
```

Se o Backoffice aceitar, a mudança é publicada no tópico. Se devolver, o processo volta ao Setor de Cadastro em Devolvido para correção, e o cliente continua com o status anterior. Se o Setor de Cadastro desistir, o processo é descartado e nada é publicado.

## Fluxos de erro e de aviso

| Situação | O que o usuário vê | Fonte no PRD |
|---|---|---|
| CPF inválido na consulta | Mensagem de CPF inválido; a consulta não é feita e o cadastro não começa | 5.9, RF26 |
| CPF já cadastrado | Mensagem "cadastro já iniciado" e link para os dados do cliente | 5.4, RF04 |
| Falha na publicação ao aceitar | Mensagem de erro; o status não muda e o Backoffice aceita de novo | 5.11, RF28 |
| Processo já decidido por outro usuário | Aviso de que já foi decidido; a ação não é aplicada | 5.14, RF37 |
| Edição simultânea | Aviso; o usuário recarrega os dados antes de continuar | 5.13, RF34 |
| Usuário enviou o processo e tenta decidi-lo | Botões de decisão desligados, com a explicação em texto | RF35 |

## Hierarquia da informação

```
Sistema de Cadastro de Clientes
|
+-- S01 Login
|
+-- S02 Tela de status (entrada dos dois perfis)
    |
    +-- S03 Consulta de CPF
    |   |
    |   +-- S04 Cadastro do cliente   (Setor de Cadastro)
    |   +-- S05 Dados cadastrais
    |   +-- S10 Processo com pedido   (Setor de Cadastro)
    |
    +-- S05 Dados cadastrais
    |   |
    |   +-- S06 Historico do cadastro
    |
    +-- S07 Lista de processos        (Backoffice)
        |
        +-- S08 Analise do processo
            |
            +-- S09 Janela de motivo
```

A S09 também é aberta a partir da S03, da S05 e da S10 nos pedidos do Setor de Cadastro. O menu da tela de status leva às telas S02, S03 e, para o Backoffice, S07.

## Assumptions & Open Questions

- Hipótese: o Setor de Cadastro chega à lista dos seus rascunhos pela tela de status. O PRD não define uma lista própria de rascunhos.
- Hipótese: o botão Consultar status do aviso de cadastro realizado leva à S02 já filtrada pelo CPF do cadastro enviado.
- Pergunta aberta: o Backoffice também faz consulta de CPF pelo menu? O PRD permite (RF03), e este desenho mantém a S03 só para consulta.
