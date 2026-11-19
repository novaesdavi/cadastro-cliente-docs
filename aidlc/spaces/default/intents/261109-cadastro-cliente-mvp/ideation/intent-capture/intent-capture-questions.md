# Captura da Intenção — Perguntas

As opções abaixo foram montadas a partir do PRD (`aidlc/spaces/default/knowledge/documents/PRD.md`, versão 7, na base de conhecimento do projeto). Escolha a que confirma o que vale para este MVP, ou escreva a sua.

## Sources

- [desc] Initial description: "MVP utilizando o PRD que está no diretório (docs/product/PRD.md) como fonte dos dados para o projeto"
- [scope] Workflow-selected scope: `mvp`.

## Q1. [Negócio] Qual problema de negócio este MVP resolve?

O PRD (seção 1) descreve a necessidade de cadastrar novos clientes com verificação do Backoffice antes de os dados chegarem às outras áreas.

A. Cadastrar novos clientes com verificação do Backoffice antes de os dados chegarem às outras áreas, que os usam para criar contas, perfis de usuário e em outros produtos (como no PRD, seção 1)
B. Substituir o sistema de terceiro usado hoje no cadastro de clientes
C. As duas coisas: A e B
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Q2. [Negócio] Por que fazer isto agora? Qual é o gatilho da iniciativa?

O PRD registra que um sistema de terceiro fica em uso somente até a publicação e liberação do novo sistema (decisão de 2026-10-25).

A. Substituir o sistema de terceiro atual, que só fica em uso até o novo ser liberado
B. Falta de controle: hoje os dados chegam às outras áreas sem uma verificação formal do Backoffice
C. A e B
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Q3. [Negócio] Que dor os usuários e as áreas sentem hoje? (select all that apply)

O PRD não descreve a dor atual; a resposta orienta como medimos o valor do MVP.

A. Cadastros chegam às outras áreas com erros de preenchimento, sem verificação
B. Falta de rastreabilidade: não há histórico de quem mudou o quê e quando
C. Dependência de um sistema de terceiro que vai ser desligado
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Q4. [Produto] Quem se beneficia do sistema?

No PRD (seção 3), quem opera o sistema são colaboradores internos com os perfis setor de Cadastro e Backoffice; as outras áreas recebem os cadastros aceitos por um tópico.

A. Setor de Cadastro e Backoffice (quem opera) e as áreas que consomem o tópico (quem recebe os dados)
B. Somente o setor de Cadastro e o Backoffice
C. Somente as áreas que consomem o tópico
D. Not identified
X. Other (please specify)

[Answer]: A

## Q5. [Negócio] Como medimos o sucesso do MVP?

O PRD (seção 2) define: 10 cadastros feitos pelo setor de Cadastro, aceitos pelo Backoffice e publicados no tópico, sem prazo.

A. Exatamente a métrica do PRD: 10 cadastros aceitos e publicados no tópico, sem prazo
B. A métrica do PRD, mas com um prazo para atingir os 10 cadastros (diga qual)
C. A métrica do PRD e mais outras (por exemplo, tempo de análise do Backoffice ou taxa de devolução; diga quais)
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Q6. [Negócio] Quem são os stakeholders principais? (select all that apply)

A lista define o mapa de stakeholders; marque só quem de fato participa ou é afetado.

A. Setor de Cadastro (opera o cadastro)
B. Backoffice (verifica, devolve ou aceita)
C. Áreas que consomem o tópico (contas, perfis de usuário e outros produtos)
D. Responsável pelo sistema de terceiro atual (desligamento e transição)
E. Not identified
X. Other (please specify)

[Answer]: A, B, C

## Q7. [Negócio] Quem decide o escopo e as prioridades, e quem influencia essas decisões?

O PRD cita "o stakeholder" como quem confirma as decisões, sem dizer o cargo.

A. Eu (quem está conduzindo este PRD) decido; as áreas de Cadastro e Backoffice influenciam
B. O gestor do setor de Cadastro decide; o Backoffice influencia
C. Um patrocinador de negócio decide (diga quem); Cadastro e Backoffice influenciam
D. Not identified
X. Other (please specify)

[Answer]: A

## Q8. [Negócio] Há alguma exigência de comunicação ou de acompanhamento do projeto?

Por exemplo, a quem informar o andamento e com que frequência.

A. None: sem exigência formal
B. Atualização semanal para o decisor
C. Apresentação ao fim de cada fase (ideia, planejamento, construção)
D. Not yet defined
X. Other (please specify)

[Answer]: B

## Q9. [Produto] O que esta primeira versão deixa de fora?

O plano escolhido é `mvp`. O PRD (seção 4.2) já lista o que está fora do escopo: perfil de administrador, processamento pelas áreas que recebem o tópico, comunicação com o cliente, notificações aos usuários, relatórios e painéis, aplicativo móvel e acesso direto do cliente.

A. Só o que o PRD já lista como fora do escopo; o MVP cobre todo o resto do PRD
B. Além do que o PRD lista, adiar os pedidos de alteração, de cancelamento e de reabertura para uma versão seguinte
C. Além do que o PRD lista, adiar outra parte do PRD (diga qual)
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Requested Changes Feedback

Pedido de mudança sobre a métrica de sucesso (R-01 da revisão): a métrica do PRD mede só a conclusão do fluxo, não a dor.

[Answer]: o item R-01 realmente não mede os erros de preenchimento, esse números são colhidos fora do sistema, e veêm de comentários feitos por outros canais, e nosso objetivo é zerar essas reclamações

## Q10. [Negócio] Qual é a meta ligada à dor dos erros de preenchimento, e como ela é medida?

Você disse que os erros de preenchimento são medidos fora do sistema, a partir de comentários recebidos por outros canais. Esta pergunta registra a meta como resposta confirmada, para ela poder entrar na declaração de intenção.

A. Zerar as reclamações sobre erros de preenchimento, medidas fora do sistema (comentários por outros canais), além dos 10 cadastros do PRD
B. Zerar as reclamações, medidas fora do sistema, no lugar dos 10 cadastros do PRD
C. Not yet defined
X. Other (please specify)

[Answer]: A

## Consolidated Summary Confirmation

Does this all look correct before I generate the artifact?

- Problema (Q1): cadastrar novos clientes com verificação do Backoffice antes de os dados chegarem às outras áreas, que os usam para criar contas, perfis de usuário e em outros produtos.
- Gatilho (Q2): substituir o sistema de terceiro atual, que só fica em uso até o novo ser liberado.
- Dor atual (Q3): cadastros chegam às outras áreas com erros de preenchimento, sem verificação.
- Beneficiados (Q4): setor de Cadastro e Backoffice (quem opera) e as áreas que consomem o tópico (quem recebe os dados).
- Sucesso (Q5): a métrica do PRD, 10 cadastros aceitos pelo Backoffice e publicados no tópico, sem prazo.
- Stakeholders (Q6): setor de Cadastro, Backoffice e áreas que consomem o tópico.
- Decisão (Q7): quem conduz o PRD decide; Cadastro e Backoffice influenciam.
- Comunicação (Q8): atualização semanal para o decisor.
- Fora do MVP (Q9): só o que o PRD já lista como fora do escopo; o MVP cobre todo o resto do PRD.
- Meta ligada à dor (Q10): zerar as reclamações sobre erros de preenchimento, medidas fora do sistema (comentários por outros canais), além dos 10 cadastros do PRD.

- Looks correct
- Request changes

[Answer]: Looks correct
