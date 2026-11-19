# Análise de Requisitos — Perguntas

As funções do sistema já estão detalhadas no PRD (`aidlc/spaces/default/knowledge/documents/PRD.md`, versão 7), e os requisitos funcionais serão organizados a partir dele. As perguntas abaixo cobrem o que o PRD não define e que só você sabe: volume, disponibilidade, desempenho, acesso e proteção de dados. Escolha a que vale para este MVP, ou escreva a sua.

## Q1. [Negócio] Quantas pessoas vão usar o sistema e quantos cadastros por dia?

O PRD não diz o tamanho do uso. A resposta define os limites que o sistema precisa suportar. A meta de sucesso é de 10 cadastros aceitos, mas o sistema deve continuar funcionando depois disso, quando substituir o sistema de terceiro.

A. Pequeno: até 20 usuários e até 50 cadastros por dia
B. Médio: de 20 a 200 usuários e até 500 cadastros por dia
C. Grande: mais de 200 usuários ou mais de 500 cadastros por dia
D. Not yet defined
X. Other (please specify)

[Answer]:

## Q2. [Negócio] Em que horários o sistema precisa estar disponível?

A resposta define o quanto de parada o sistema tolera, inclusive para publicações manuais (a prática afirmada é publicar tudo à mão).

A. Só em horário comercial (por exemplo, de segunda a sexta, das 8h às 19h), com parada permitida fora dele
B. Todos os dias, 24 horas, com parada curta permitida de madrugada
C. Todos os dias, 24 horas, sem paradas planejadas
D. Not yet defined
X. Other (please specify)

[Answer]:

## Q3. [Negócio] Que tempo de resposta é aceitável nas telas?

O PRD pede só que as telas funcionem. Um número evita discussão na hora de aceitar o MVP.

A. Até 2 segundos em 95% das ações (consultar CPF, salvar, abrir a tela de status)
B. Até 5 segundos em 95% das ações
C. Sem exigência de tempo no MVP
D. Not yet defined
X. Other (please specify)

[Answer]:

## Q4. [Arquitetura] A mesma mensagem pode chegar duas vezes às outras áreas?

O PRD diz que, se a publicação falhar, o status não muda e o Backoffice aceita de novo (RF28). Se a publicação der certo mas o sistema falhar logo depois, o novo aceite pode publicar o mesmo cadastro outra vez.

A. Pode: cada mensagem traz o Id Processo, e as áreas ignoram uma repetição
B. Não pode: o sistema precisa garantir uma única publicação por aceite
C. Not yet defined
X. Other (please specify)

[Answer]:

## Q5. [Segurança] Como as contas dos colaboradores chegam ao sistema?

O PRD diz que o sistema tem login próprio, mas que a criação de usuários e a atribuição de perfis não fazem parte dele (seções 3 e 9). Alguém precisa colocar as contas no sistema por fora.

A. A equipe técnica faz uma carga de contas e perfis fora do sistema, por um procedimento combinado, quando houver mudança
B. As contas vêm de um cadastro de colaboradores da empresa, por uma integração que ainda não existe
C. Not yet defined
X. Other (please specify)

[Answer]:

## Q6. [Segurança] Depois de quanto tempo parado o sistema encerra a sessão?

O PRD exige autenticação, e o sistema guarda dados pessoais. A tela de cadastro com dados não salvos exibirá aviso antes de a sessão encerrar.

A. 15 minutos sem uso
B. 30 minutos sem uso
C. 60 minutos sem uso
D. Not yet defined
X. Other (please specify)

[Answer]:

## Q7. [Conformidade] O que fazer com o CPF e os dados pessoais, já que a LGPD vale e o PRD não mascara nem define prazo de guarda?

O PRD (seção 9) diz que nenhum dado é mascarado, que os dois perfis veem tudo e que os dados ficam sem prazo de guarda. A viabilidade registrou que isso pode conflitar com a LGPD.

A. Manter como o PRD diz no MVP, e registrar uma análise da LGPD como pendência para uma etapa posterior
B. Manter a visibilidade do PRD, mas definir agora um prazo de guarda (diga qual)
C. Mascarar o CPF e os dados de contato nas listas e na tela de status, mostrando completos só nos dados cadastrais
D. Not yet defined
X. Other (please specify)

[Answer]:

## Q8. [Operação] Como o time deve ser avisado quando algo falhar em produção?

Hoje não há serviços de aplicação em uso na AWS, e o PRD só define a mensagem de erro que o Backoffice vê quando a publicação falha.

A. Registro técnico dos erros e um alerta quando a publicação no tópico falhar
B. Só o registro técnico dos erros, consultado quando alguém reclamar
C. Not yet defined
X. Other (please specify)

[Answer]:
