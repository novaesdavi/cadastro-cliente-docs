# Rascunhos de Telas — Perguntas

As opções abaixo partem da declaração de intenção, do documento de escopo e do backlog aprovados, e do PRD (`aidlc/spaces/default/knowledge/documents/PRD.md`, versão 7). Escolha a que vale para este MVP, ou escreva a sua.

Contexto: o PRD diz que o MVP é uma aplicação web com autenticação, usada por colaboradores internos com dois perfis, Setor de Cadastro e Backoffice. Aplicativo móvel e acesso direto do cliente estão fora do escopo.

## Q1. [Design] Em que aparelhos o sistema precisa funcionar?

O PRD (seção 4.1) define uma aplicação web, e deixa o aplicativo móvel fora do escopo (seção 4.2). Isso decide quanto as telas precisam se adaptar ao tamanho da tela.

A. Só em computador (navegador no desktop)
B. Em computador e tablet
C. Em computador, tablet e celular, pelo navegador
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Q2. [Design] Existe uma identidade visual ou um sistema de design da empresa a seguir?

A resposta evita desenhar telas que depois precisem ser refeitas para seguir um padrão.

A. Existe um guia de marca ou sistema de design que as telas devem seguir (diga qual)
B. Não existe: as telas podem ter um visual simples e neutro
C. Not yet defined
X. Other (please specify)

[Answer]: B

## Q3. [Design] Que exigências de acessibilidade valem para as telas?

O PRD não cita acessibilidade. Como são usuários internos, a exigência pode vir da empresa.

A. Seguir a WCAG 2.1 nível AA, incluindo uso só com o teclado e leitor de tela
B. Garantir só o uso com o teclado e contraste adequado, sem exigência formal
C. Nenhuma exigência conhecida
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Q4. [Design] Por onde cada perfil entra depois do login?

O PRD descreve o fluxo principal: o setor de Cadastro começa pela consulta de CPF (seção 5.1), e o Backoffice trabalha sobre a lista única de processos enviados (RF33). Os dois perfis têm também a tela de status (RF09).

A. Cada perfil entra na sua tela de trabalho: o Setor de Cadastro na consulta de CPF e o Backoffice na lista de processos enviados
B. Os dois entram na tela de status, e daí vão para o que precisam fazer
C. Not yet defined
X. Other (please specify)

[Answer]: B

## Q5. [Design] Quais telas desenhar nos rascunhos?

As telas do PRD são: login, consulta de CPF, cadastro do cliente, tela de status, dados cadastrais, histórico, lista de processos do Backoffice, análise do processo (aceitar ou devolver) e pedidos de alteração, cancelamento e reabertura.

A. Todas as telas listadas
B. Só as do fluxo principal: login, consulta de CPF, cadastro, tela de status, lista de processos do Backoffice e análise do processo
C. Not yet defined
X. Other (please specify)

[Answer]: A

## Q6. [Design] Como o formulário de cadastro deve ser organizado?

O cadastro tem Nome, CPF, e-mail, telefone, data de nascimento e endereço (CEP, rua, número, complemento, bairro, cidade e UF). Só Nome e CPF são obrigatórios, e o endereço é todo obrigatório se qualquer campo dele for preenchido (PRD, seção 8).

A. Uma tela só, com seções: dados pessoais, contato e endereço
B. Em passos, um grupo de campos por vez
C. Not yet defined
X. Other (please specify)

[Answer]: A

## Q7. [Design] Como pedir o motivo de uma devolução ou de um pedido?

O PRD exige motivo para devolver um processo, para pedir alteração, cancelamento ou reabertura (seção 8).

A. Em uma janela de confirmação com o campo de motivo, aberta pela ação
B. Em um campo na própria tela do processo, antes de acionar a ação
C. Not yet defined
X. Other (please specify)

[Answer]: A

## Consolidated Summary Confirmation

Does this all look correct before I generate the artifact?

- Aparelhos (Q1): só em computador, pelo navegador no desktop.
- Visual (Q2): não existe identidade visual nem sistema de design; as telas têm um visual simples e neutro.
- Acessibilidade (Q3): seguir a WCAG 2.1 nível AA, incluindo uso só com o teclado e leitor de tela.
- Entrada (Q4): os dois perfis entram na tela de status e daí vão para o que precisam fazer.
- Telas (Q5): desenhar todas as telas listadas, incluindo dados cadastrais, histórico e os pedidos de alteração, cancelamento e reabertura.
- Formulário (Q6): uma tela só, com seções de dados pessoais, contato e endereço.
- Motivo (Q7): uma janela de confirmação com o campo de motivo, aberta pela ação.

- Looks correct
- Request changes

[Answer]: Looks correct
