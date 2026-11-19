# Backlog da Intenção — Sistema de Cadastro de Novos Clientes (MVP)

Este backlog lista as partes (proto-unidades) em que o MVP se divide, na ordem de construção. Parte da declaração de intenção aprovada (`ideation/intent-capture/intent-statement.md`) e do documento de escopo (`scope-document.md`). Os requisitos citados (RF) são os do PRD v7.

## Como foi priorizado

- Método: MoSCoW. Todo o PRD é obrigatório para entregar o MVP (Q1 de `scope-definition-questions.md`), então todas as partes são Must. Nenhuma é Should ou Could.
- Won't (neste MVP): os itens fora do escopo do PRD, listados em `scope-document.md`.
- Ordem: dependência primeiro (Q3). Cada parte só começa depois das que ela precisa.
- Nenhuma parte tem data própria; vale só a data-limite do MVP (Q7).

## Partes do MVP, em ordem

| Ordem | Parte | Prioridade | Requisitos do PRD | Depende de |
|---|---|---|---|---|
| 1 | Acesso e perfis | Must | RF01, RF02 | Nada |
| 2 | Consulta de CPF e cadastro de novo cliente | Must | RF03, RF04, RF05, RF10, RF11, RF26, RF29, RF30 | 1 |
| 3 | Envio e decisão do Backoffice | Must | RF06, RF07, RF12, RF13, RF33, RF35, RF37 | 2 |
| 4 | Publicação no tópico | Must | RF22, RF28 | 3 |
| 5 | Status, dados e histórico | Must | RF09, RF14, RF15, RF21, RF24 | 2 |
| 6 | Pedido de alteração de dados | Must | RF18, RF20, RF27, RF36 | 4, 5 |
| 7 | Pedido de cancelamento | Must | RF17, RF23 | 4, 5 |
| 8 | Pedido de reabertura | Must | RF25, RF32 | 4, 5 |
| 9 | Descarte e retomada de rascunhos | Must | RF19, RF31 | 2 |
| 10 | Aviso de edição simultânea | Must | RF34 | 2 |

A tabela cobre todos os requisitos funcionais do PRD v7 (RF01 a RF37, sem RF08 e RF16, que o PRD retirou).

## O que cada parte entrega

| Parte | Resultado para quem usa |
|---|---|
| 1. Acesso e perfis | Cada colaborador entra com login próprio e vê só as funções do seu perfil |
| 2. Consulta de CPF e cadastro de novo cliente | O setor de Cadastro consulta o CPF, preenche o cadastro, salva rascunhos e troca o CPF enquanto o cliente é Novo |
| 3. Envio e decisão do Backoffice | O setor de Cadastro envia o processo, e o Backoffice devolve com motivo ou aceita, sem decidir um processo que ele mesmo enviou |
| 4. Publicação no tópico | O cadastro aceito chega às outras áreas, e uma falha de publicação não muda o status |
| 5. Status, dados e histórico | Os dois perfis acompanham o status, abrem os dados do cliente e consultam o histórico de cada cadastro |
| 6. Pedido de alteração de dados | O setor de Cadastro pede a alteração de dados de um cliente Ativo, e a mudança aceita é publicada no tópico |
| 7. Pedido de cancelamento | O setor de Cadastro pede o cancelamento de um cliente Ativo, e o cancelamento aceito é publicado no tópico |
| 8. Pedido de reabertura | O setor de Cadastro pede a reabertura de um cliente Cancelado, e a reabertura aceita é publicada no tópico |
| 9. Descarte e retomada de rascunhos | O setor de Cadastro descarta processos e retoma rascunhos esquecidos por outro usuário |
| 10. Aviso de edição simultânea | Quem salva depois de outra pessoa é avisado e recarrega os dados antes de continuar |

## Pontos de atenção na ordem

- A parte 4 depende de o serviço de tópico existir, e hoje ele não existe (Q4 de `feasibility-questions.md`; `raid-log.md`, problema I1). É a primeira dependência externa do projeto.
- As partes 6, 7 e 8 só entram depois da 4 e da 5, e são as maiores em regras do PRD.
- A análise das regras de dados do PRD à luz da LGPD (`raid-log.md`, D5) precisa estar resolvida antes de a parte 2 fixar os campos e a guarda dos dados.

## Assumptions & Open Questions

- Hipótese: a divisão em 10 partes é só um ponto de partida; as etapas de projeto podem agrupá-las ou dividi-las de outra forma.
- Hipótese: o tamanho de cada parte é desigual, e as partes 6, 7 e 8 pesam mais. Nenhuma estimativa foi feita.
- Pergunta aberta: o que muda na ordem se o serviço de tópico atrasar? As partes 1, 2, 3, 5, 9 e 10 podem avançar sem ele.
