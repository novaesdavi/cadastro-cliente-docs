# PRD — Sistema de Cadastro de Novos Clientes

Status: Rascunho
Versão: 2 · Última atualização: 2026-10-25

## 1. Contexto e problema

A empresa realiza hoje o cadastro de novos clientes por meio de um sistema de terceiro que está desatualizado (em "back level") e não recebe mais a manutenção necessária. É preciso um novo sistema para o cadastro de novos clientes que substitua esse sistema de terceiro.

## 2. Objetivos e métricas de sucesso

- **Objetivo**: substituir o sistema de terceiro no cadastro de novos clientes.
- **Métrica de sucesso**: o novo sistema é considerado bem-sucedido após 10 cadastros feitos pelo setor de Cadastro.

## 3. Usuários e perfis

O sistema é acessado por usuários internos da empresa (colaboradores), com perfis de acesso diferentes. No documento, **usuário** é o colaborador que opera o sistema e **cliente** é a pessoa cadastrada. Há dois perfis:

| Perfil | Pode | Não pode |
|---|---|---|
| Setor de Cadastro | Consultar CPF antes de iniciar um cadastro; iniciar e preencher o cadastro de um novo cliente; salvar o cadastro como rascunho; enviar o cadastro para o Backoffice; editar cadastros com status Rascunho ou Devolvido para correção; consultar a tela de status, inclusive por CPF; abrir os dados cadastrais de um cliente. | Iniciar um novo cadastro para um CPF que já tem cadastro no sistema; editar cadastros com status Enviado para Backoffice ou Aceito e enviado para processamento; devolver ou aceitar cadastros. |
| Backoffice | Verificar e analisar os cadastros enviados pelo setor de Cadastro; ajustar cadastros já iniciados pelo setor de Cadastro; devolver um cadastro para correção, informando o motivo; aceitar o cadastro e enviá-lo para processamento (é o Backoffice quem marca o cadastro como concluído); abrir os dados cadastrais de um cliente. | Cadastrar novos clientes. |

Não há perfil de administrador neste sistema. A criação de usuários e a atribuição de perfis não são contempladas por este sistema.

## 4. Escopo

### 4.1 Dentro do escopo

- Aplicação web com autenticação.
- Perfis de acesso: setor de Cadastro e Backoffice.
- Consulta de CPF antes do início de um novo cadastro, nos cadastros do próprio sistema.
- Preenchimento do cadastro de novo cliente, com opção de salvar como rascunho.
- Envio do cadastro para verificação e análise do Backoffice.
- Ajuste, pelo Backoffice, de cadastros iniciados pelo setor de Cadastro.
- Devolução do cadastro para correção, com motivo.
- Aceite do cadastro pelo Backoffice e envio para processamento.
- Tela de status dos cadastros, com consulta por CPF.
- Consulta dos dados cadastrais do cliente.

### 4.2 Fora do escopo

- Perfil de administrador e fluxo de administração de usuários e perfis.
- Consulta de clientes no sistema de terceiro.
- Migração dos cadastros existentes no sistema de terceiro.
- O processamento do cadastro pela área que o recebe depois do aceite do Backoffice.

## 5. Jornadas e fluxos

### 5.1 Fluxo principal

1. O usuário do setor de Cadastro consulta o CPF do cliente.
2. Se o CPF não tiver cadastro no sistema, o usuário preenche o cadastro do novo cliente.
3. Ao ser realizado o cadastro, o sistema exibe um aviso de que o cadastro foi realizado e um botão para consultar o status.
4. O usuário aciona "Enviar para Backoffice". O cadastro passa ao status Enviado para Backoffice.
5. O Backoffice verifica e analisa o cadastro e pode ajustá-lo.
6. Não havendo problemas de preenchimento, o Backoffice aceita o cadastro e o envia para processamento em outra área. O cadastro passa ao status Aceito e enviado para processamento.
7. O setor de Cadastro consulta o status do cadastro na tela de status.

### 5.2 Fluxo alternativo: rascunho

1. Durante o preenchimento, o usuário do setor de Cadastro aciona "Salvar". O cadastro passa ao status Rascunho.
2. O usuário pode voltar ao cadastro em Rascunho, editá-lo e, quando quiser, acionar "Enviar para Backoffice".

### 5.3 Fluxo alternativo: devolução para correção

1. Ao analisar um cadastro com status Enviado para Backoffice, o Backoffice encontra problemas de preenchimento.
2. O Backoffice aciona "Devolver para correção" e preenche o campo "motivo".
3. O cadastro passa ao status Devolvido para correção.
4. O setor de Cadastro pode editar o cadastro devolvido.

### 5.4 Fluxo alternativo: CPF já cadastrado

1. O usuário do setor de Cadastro consulta o CPF do cliente.
2. Se já existir cadastro para o CPF no sistema, em qualquer status (inclusive em análise do Backoffice), o sistema exibe a mensagem "cadastro já iniciado" e um link para consultar os dados cadastrais do cliente, e não permite iniciar um novo cadastro para esse CPF.
3. O usuário pode consultar o CPF na tela de status para ver o status do cadastro existente.
4. Se o cadastro existente estiver com status Rascunho ou Devolvido para correção, o setor de Cadastro pode editá-lo. Se estiver com status Enviado para Backoffice ou Aceito e enviado para processamento, o setor de Cadastro não pode editá-lo; para que seja ajustado, o Backoffice precisa devolvê-lo para correção.

### 5.5 Ciclo de vida do cadastro

Status:

| Status | Significado |
|---|---|
| Rascunho | Cadastro salvo pelo setor de Cadastro e ainda não enviado. |
| Enviado para Backoffice | Cadastro enviado pelo setor de Cadastro para verificação e análise do Backoffice. |
| Devolvido para correção | Cadastro devolvido pelo Backoffice ao setor de Cadastro, com motivo. |
| Aceito e enviado para processamento | Cadastro aceito pelo Backoffice e enviado para outra área, fora do escopo deste sistema. |

Transições:

| De | Para | Quem | Ação |
|---|---|---|---|
| (novo cadastro) | Rascunho | Setor de Cadastro | Salvar |
| (novo cadastro) ou Rascunho | Enviado para Backoffice | Setor de Cadastro | Enviar para Backoffice |
| Enviado para Backoffice | Devolvido para correção | Backoffice | Devolver para correção, com motivo |
| Enviado para Backoffice | Aceito e enviado para processamento | Backoffice | Aceitar e enviar para processamento |

## 6. Requisitos funcionais

- **RF01** — O sistema só pode ser usado após autenticação do usuário.
- **RF02** — O sistema controla o acesso por perfil, com funções diferentes para o setor de Cadastro e para o Backoffice, conforme a seção 3.
- **RF03** — O sistema permite consultar um cliente pelo CPF antes de iniciar um novo cadastro. A consulta considera somente os cadastros do próprio sistema.
- **RF04** — Quando o CPF consultado já tiver cadastro no sistema, o sistema exibe a mensagem "cadastro já iniciado" e um link para consultar os dados cadastrais do cliente, e impede o início de um novo cadastro para esse CPF.
- **RF05** — O sistema permite ao setor de Cadastro preencher o cadastro de um novo cliente com os campos da seção 8.
- **RF06** — Ao ser realizado um novo cadastro, o sistema exibe um aviso de que o cadastro foi realizado e um botão para consultar o status.
- **RF07** — O setor de Cadastro pode enviar o cadastro para verificação e análise do Backoffice pela ação "Enviar para Backoffice".
- **RF08** — O Backoffice pode ajustar cadastros iniciados pelo setor de Cadastro.
- **RF09** — O sistema oferece uma tela de status com o status de cada cadastro, conforme a seção 5.5.
- **RF10** — A consulta (pesquisa por CPF) e o preenchimento/edição do cadastro são funções separadas, em telas distintas.
- **RF11** — O setor de Cadastro pode salvar o cadastro como rascunho pela ação "Salvar".
- **RF12** — O Backoffice pode devolver um cadastro para correção pela ação "Devolver para correção", com preenchimento do campo "motivo".
- **RF13** — O Backoffice pode aceitar um cadastro e enviá-lo para processamento.
- **RF14** — A tela de status permite consultar um cadastro pelo CPF.
- **RF15** — Os dois perfis (setor de Cadastro e Backoffice) podem abrir os dados cadastrais de um cliente.

## 7. Regras de negócio

- **RN01** — A consulta do CPF deve ser feita antes do cadastro de um novo cliente.
- **RN02** — Somente o setor de Cadastro inicia cadastros de novos clientes. O Backoffice não pode cadastrar novos clientes; atua apenas sobre cadastros já iniciados pelo setor de Cadastro.
- **RN03** — Somente o Backoffice aceita um cadastro. Ao aceitar, o cadastro é enviado para processamento em outra área e passa ao status Aceito e enviado para processamento.
- **RN04** — Não pode existir mais de um cadastro para o mesmo CPF. Se o CPF já tiver cadastro no sistema, em qualquer status (inclusive em análise do Backoffice), o sistema impede o início de um novo cadastro.
- **RN05** — A verificação de CPF existente considera somente os cadastros do próprio sistema; cadastros feitos no sistema de terceiro não são considerados.
- **RN06** — A devolução para correção exige o preenchimento do motivo. Sem motivo, a devolução não é realizada.
- **RN07** — O setor de Cadastro só pode editar cadastros com status Rascunho ou Devolvido para correção. Cadastros com status Enviado para Backoffice ou Aceito e enviado para processamento não podem ser editados pelo setor de Cadastro; para que sejam ajustados, o Backoffice precisa devolvê-los para correção.
- **RN08** — Os campos Nome e CPF são obrigatórios; os demais campos do cadastro são opcionais.

## 8. Dados

Campos do cadastro do cliente:

| Campo | Obrigatório |
|---|---|
| Nome | Sim |
| CPF | Sim |
| E-mail | Não |
| Telefone | Não |
| Data de nascimento | Não |
| Endereço | Não |

Dado da devolução:

| Campo | Obrigatório |
|---|---|
| Motivo da devolução | Sim |

## 10. Integrações e legado

- O novo sistema substitui o sistema de terceiro usado atualmente para o cadastro de novos clientes.
- A consulta de CPF não busca dados no sistema de terceiro.
- Não haverá migração dos cadastros existentes no sistema de terceiro.
- O sistema de terceiro continua em uso somente até a publicação e liberação do novo sistema.

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
