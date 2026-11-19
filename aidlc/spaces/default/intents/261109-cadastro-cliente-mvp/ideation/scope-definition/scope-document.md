# Documento de Escopo — Sistema de Cadastro de Novos Clientes (MVP)

Este documento parte da declaração de intenção aprovada (`ideation/intent-capture/intent-statement.md`), da avaliação de viabilidade (`ideation/feasibility/feasibility-assessment.md`) e do registro de restrições (`ideation/feasibility/constraint-register.md`). Cada ponto cita a fonte: uma resposta de `scope-definition-questions.md` (Q), uma seção do PRD v7 ou um dos documentos acima.

## Escopo do MVP

O MVP cobre todo o PRD v7, exceto o que ele lista como fora do escopo. O MVP só é considerado entregue com todo o PRD pronto (Q1, `intent-statement.md`).

### Dentro do escopo

| Capacidade | O que o setor ou o perfil consegue fazer | Fonte |
|---|---|---|
| Acesso e perfis | Entrar no sistema com login próprio e usar só as funções do próprio perfil (Setor de Cadastro ou Backoffice) | PRD seções 3, 4.1 e 9; `constraint-register.md` C03 |
| Consulta de CPF e cadastro de novo cliente | Consultar o CPF, preencher o cadastro, salvar como rascunho e trocar o CPF enquanto o cliente é Novo | PRD seções 4.1 e 5.1; Q8 |
| Envio e decisão do Backoffice | Enviar o processo, ver a lista única de processos enviados, devolver com motivo ou aceitar | PRD seções 4.1 e 5.3 |
| Publicação no tópico | Publicar os dados do cadastro aceito no tópico para as outras áreas | PRD seção 10; `constraint-register.md` C01 |
| Status, dados e histórico | Ver o status de cada cadastro, abrir os dados do cliente e consultar o histórico | PRD seções 4.1 e 5.5 |
| Pedido de alteração de dados | Pedir a alteração de dados de um cliente Ativo, com motivo | PRD seção 5.8 |
| Pedido de cancelamento | Pedir o cancelamento de um cliente Ativo, com motivo | PRD seção 5.7 |
| Pedido de reabertura | Pedir a reabertura de um cliente Cancelado, com motivo | PRD seção 5.6 |
| Descarte e retomada de rascunhos | Descartar um processo e retomar um rascunho esquecido por outro usuário | PRD seções 5.2 e 5.10 |
| Aviso de edição simultânea | Avisar quem salva depois de outra pessoa, para recarregar os dados | PRD seção 5.13 |

A troca de CPF na edição, que a Q2 aceitou adiar, entra no MVP, porque a Q8 confirmou que a data se move e o escopo fica.

### Fora do escopo

São os itens que o PRD lista como fora do escopo (PRD seção 4.2; `intent-statement.md`, Initial Scope Signal):

- Perfil de administrador e administração de usuários e perfis.
- O processamento do cadastro pelas áreas que recebem o tópico.
- Comunicação com o cliente.
- Notificações aos usuários.
- Relatórios e painéis.
- Aplicativo móvel.
- Acesso direto do cliente.

As outras áreas não precisam estar consumindo o tópico para o MVP estar pronto (Q4).

## Como o MVP é aceito

O MVP é aceito quando duas condições valem juntas (Q5):

| Condição | Meta | Fonte |
|---|---|---|
| Cadastros feitos pelo setor de Cadastro, aceitos pelo Backoffice e publicados no tópico | 10 cadastros, sem prazo | `intent-statement.md`, Success Metrics; PRD seção 2 |
| Reclamações sobre erros de preenchimento, colhidas fora do sistema | Nenhuma reclamação durante 60 dias | Q5, Q9; `intent-statement.md`, Success Metrics |

## Ordem de construção

A ordem é dependência primeiro: o que as outras partes precisam sai antes (Q3). Acesso e perfis, depois cadastro, depois envio e aceite. A sequência completa, com as dependências de cada parte, está em `intent-backlog.md`.

## Mapa do fluxo de valor

O mapa mostra o caminho de um cadastro até o resultado que a intenção persegue.

```mermaid
flowchart LR
  A["Setor de Cadastro registra o cliente"] --> B["Backoffice verifica o cadastro"]
  B --> C["Cadastro aceito"]
  C --> D["Publicação no tópico"]
  D --> E["Outras áreas usam os dados"]
  E --> F["Menos erros e menos reclamações"]
```

Texto equivalente: o Setor de Cadastro registra o cliente, o Backoffice verifica o cadastro, o cadastro aceito é publicado no tópico, as outras áreas usam os dados e, como resultado esperado, caem os erros de preenchimento e as reclamações. A última etapa é um resultado esperado, não uma garantia: só a meta de 60 dias sem reclamações a confirma (Q9).

## Prazo e escopo

Há uma data-limite para liberar o MVP, em até 3 meses, e há congelamento de mudanças no fim do ano (`feasibility-assessment.md`; `constraint-register.md` C06 e C07). Nenhuma capacidade tem data própria (Q7). Se o escopo e o prazo não couberem, a data se move e o escopo fica (Q6).

Hipótese: com todo o PRD obrigatório (Q1) e 3 meses de prazo, a data tende a se mover. Isso ainda não foi validado e depende de um plano de entrega nas próximas etapas.

## Assumptions & Open Questions

- Hipótese: todo o PRD cabe em 3 meses. Já era um risco na viabilidade (R1) e a Q6 define o que fazer se não couber.
- Hipótese: a Q8 substitui a Q2 para a troca de CPF; nenhuma capacidade fica de fora por prazo.
- Pergunta aberta: de que data os 3 meses contam? Continua em aberto desde a viabilidade (A1).
- Pergunta aberta: como as reclamações são contadas durante os 60 dias, por quem e por quais canais? A Q9 definiu só a janela.
- Pergunta aberta: se a data se move, quem aprova a nova data? O decisor ainda não tem nome ou papel (`intent-statement.md` e `stakeholder-map.md`).
