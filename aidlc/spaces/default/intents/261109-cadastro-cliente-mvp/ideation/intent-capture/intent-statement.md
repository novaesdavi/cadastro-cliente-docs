# Declaração de Intenção — Sistema de Cadastro de Novos Clientes (MVP)

## Problem Statement

A empresa precisa cadastrar novos clientes com verificação do Backoffice antes de os dados chegarem às outras áreas, que usam esses dados para criar contas, perfis de usuário e em outros produtos. [Q1]

Hoje os cadastros chegam às outras áreas com erros de preenchimento, sem verificação. [Q3]

O MVP usa o PRD do projeto como fonte dos dados. [desc]

## Target Customer

| Quem | Papel | Como se beneficia | Source |
|---|---|---|---|
| Setor de Cadastro | Opera o sistema: registra os novos clientes | Registra os novos clientes com verificação do Backoffice antes de os dados chegarem às outras áreas | [Q4] [Q1] |
| Backoffice | Opera o sistema: verifica os cadastros antes do envio | Passa a verificar formalmente cada cadastro antes de os dados seguirem | [Q4] [Q1] |
| Áreas que consomem o tópico | Recebem os cadastros aceitos | Recebem dados verificados, sem os erros de preenchimento de hoje | [Q4] [Q3] |

## Success Metrics

| Métrica | Meta | Prazo | Source |
|---|---|---|---|
| Cadastros feitos pelo setor de Cadastro, aceitos pelo Backoffice e publicados no tópico | 10 cadastros | Sem prazo definido | [Q5] |
| Reclamações sobre erros de preenchimento, colhidas fora do sistema a partir de comentários recebidos por outros canais | Zerar as reclamações, além dos 10 cadastros acima | Sem prazo definido | [Q10] [Q3] |

## Initiative Trigger

Substituir o sistema de terceiro usado hoje, que só fica em uso até o novo sistema ser liberado. [Q2]

## Initial Scope Signal

- Escopo do fluxo de trabalho (workflow-selected): `mvp`. [scope]
- Fronteira do produto confirmada: fica fora do MVP somente o que o PRD já lista como fora do escopo — perfil de administrador, processamento pelas áreas que recebem o tópico, comunicação com o cliente, notificações aos usuários, relatórios e painéis, aplicativo móvel e acesso direto do cliente. O MVP cobre todo o resto do PRD. [Q9]

## Assumptions & Open Questions

None.
