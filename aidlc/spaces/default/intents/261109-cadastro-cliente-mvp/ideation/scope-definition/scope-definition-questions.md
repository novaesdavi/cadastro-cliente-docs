# Definição de Escopo — Perguntas

As opções abaixo partem da declaração de intenção aprovada, da avaliação de viabilidade e do PRD (`aidlc/spaces/default/knowledge/documents/PRD.md`, versão 7). Escolha a que vale para este MVP, ou escreva a sua.

Contexto: na Captura da Intenção você definiu que o MVP cobre todo o PRD, exceto o que ele lista como fora do escopo. A viabilidade registrou uma data-limite de até 3 meses e um congelamento de mudanças no fim do ano. As perguntas abaixo testam se isso cabe e como ordenar o trabalho.

## Q1. [Produto] O MVP só é considerado entregue com todo o PRD, ou o fluxo principal pode sair antes?

O fluxo principal do PRD é: consultar o CPF, preencher o cadastro, enviar para o Backoffice, devolver ou aceitar e publicar no tópico, mais a tela de status. Os pedidos de alteração, de cancelamento e de reabertura vêm em cima dele.

A. Todo o PRD precisa estar pronto antes de liberar o MVP
B. O fluxo principal é liberado primeiro, e os pedidos de alteração, de cancelamento e de reabertura entram logo depois, ainda como parte do MVP
C. O fluxo principal é o MVP, e os pedidos ficam para uma versão seguinte
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Q2. [Produto] Se o prazo apertar, o que pode ficar para depois? (select all that apply)

O PRD tem requisitos que dão conforto, mas não são o centro do fluxo. Marque só os que você aceita adiar.

A. O aviso de edição simultânea do mesmo cadastro (quem salvar depois precisa recarregar os dados)
B. Retomar ou descartar um rascunho esquecido por outro usuário do setor de Cadastro
C. Trocar o CPF durante a edição, com a verificação de CPF existente a cada edição
D. Nenhum: tudo isso é indispensável para o MVP
X. Other (please specify)

[Answer]: C

## Q3. [Produto] Em que ordem construir: o que dá mais risco, o que dá mais valor ou o que as outras partes precisam?

A viabilidade apontou três riscos de início: o serviço de tópico não existe, o ambiente de nuvem é novo e a LGPD precisa ser analisada. O valor mais visível é o fluxo principal funcionando.

A. Risco primeiro: tópico, ambiente e LGPD antes das telas
B. Valor primeiro: o fluxo principal aparece rápido, e os riscos são tratados em paralelo
C. Dependência primeiro: o que as outras partes precisam sai antes (acesso e perfis, cadastro, depois envio e aceite)
D. Not yet defined
X. Other (please specify)

[Answer]: C

## Q4. [Produto] Para o MVP estar pronto, as outras áreas já precisam estar consumindo o tópico?

O PRD deixa fora do escopo o processamento do cadastro pelas áreas que recebem o tópico, e a métrica de sucesso conta cadastros publicados no tópico.

A. Não: basta publicar no tópico, como o PRD e a métrica dizem
B. Sim, pelo menos uma área precisa estar consumindo o tópico
C. Not yet defined
X. Other (please specify)

[Answer]: A

## Q5. [Produto] A meta de zerar as reclamações é critério para aceitar o MVP?

Na Captura da Intenção você acrescentou a meta de zerar as reclamações sobre erros de preenchimento, medidas fora do sistema. A revisão apontou que não ficou claro se ela decide a aceitação do MVP.

A. Sim: o MVP só é aceito com os 10 cadastros e a meta de zerar as reclamações
B. Não: o MVP é aceito com os 10 cadastros, e as reclamações são um indicador acompanhado depois do lançamento
C. Not yet defined
X. Other (please specify)

[Answer]: A

## Q6. [Gestão] Se o escopo e o prazo não couberem, o que cede primeiro?

A viabilidade levantou o risco de 3 meses não comportarem o PRD inteiro. Essa escolha define como o risco será tratado.

A. Reduzir o escopo e manter a data
B. Mover a data e manter o escopo
C. Decidir caso a caso, com quem conduz o PRD
D. Not yet defined
X. Other (please specify)

[Answer]: B

## Q7. [Gestão] Alguma capacidade tem data própria, além da data-limite do MVP?

Por exemplo, a publicação no tópico precisar estar pronta antes do desligamento do sistema de terceiro. A viabilidade registrou que essa data de desligamento não está definida.

A. Nenhuma: vale só a data-limite do MVP
B. A publicação no tópico tem data própria (diga qual)
C. Outra capacidade tem data própria (diga qual capacidade e qual data)
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Q8. [Gestão] A troca de CPF pode ser adiada se o prazo apertar, ou a data é que se move?

Na Q2 você aceitou adiar a troca de CPF na edição se o prazo apertar. Na Q6 você disse que, se não couber, a data se move e o escopo fica. E na Q1, que todo o PRD precisa estar pronto antes de liberar. As três respostas não podem valer juntas.

A. Vale a Q6: a data se move, e a troca de CPF entra no MVP
B. Vale a Q2: só a troca de CPF pode ser adiada para manter a data; o resto do PRD continua obrigatório
C. Not yet defined
X. Other (please specify)

[Answer]: A

## Q9. [Produto] Por quanto tempo sem reclamações o MVP é aceito?

Na Q5 você definiu que o MVP só é aceito com os 10 cadastros e a meta de zerar as reclamações sobre erros de preenchimento. Sem uma janela de observação, não dá para dizer quando a meta foi atingida.

A. 30 dias sem reclamações
B. 60 dias sem reclamações
C. 90 dias sem reclamações
D. Not yet defined
X. Other (please specify)

[Answer]: B

## Consolidated Summary Confirmation

Does this all look correct before I generate the artifact?

- Entrega (Q1): todo o PRD precisa estar pronto antes de liberar o MVP.
- Adiáveis (Q2, Q8): a troca de CPF na edição, que a Q2 aceitou adiar, entra no MVP, porque a Q8 confirmou que a data se move e o escopo fica. Nenhuma capacidade fica de fora por prazo.
- Ordem (Q3): dependência primeiro. O que as outras partes precisam sai antes: acesso e perfis, cadastro, depois envio e aceite.
- Áreas consumidoras (Q4): basta publicar no tópico; não é preciso que uma área já esteja consumindo.
- Aceite do MVP (Q5, Q9): os 10 cadastros e a meta de zerar as reclamações sobre erros de preenchimento, com 60 dias sem reclamações.
- O que cede (Q6): se escopo e prazo não couberem, a data se move e o escopo fica.
- Datas próprias (Q7): nenhuma capacidade tem data própria; vale só a data-limite do MVP.

- Looks correct
- Request changes

[Answer]: Looks correct
