# Práticas do Time — Perguntas

As opções partem do rascunho do engenheiro de entrega (`team-practices.md`), que vem dos padrões do framework. São sugestões, não fatos: escolha o que o time realmente quer fazer neste projeto, ou escreva a sua resposta.

Contexto: o MVP é um sistema web interno, com prazo de até 3 meses e congelamento de mudanças no fim do ano. A empresa tem conta AWS sem serviços em uso, e não há stack padrão (`feasibility-assessment.md`).

## Q1. [Engenharia] Como o código novo entra no tronco principal?

O padrão sugerido é trabalhar em ramos curtos que voltam ao ramo principal (`main`) com squash, que junta os commits do ramo em um só.

A. Ramos curtos por pedaço de trabalho, que voltam ao `main` com squash (padrão sugerido)
B. Ramos longos por funcionalidade, que voltam ao `main` quando a funcionalidade termina
C. Trabalhar direto no `main`, sem ramos
D. Not yet defined
X. Other (please specify)

[Answer]: B

## Q2. [Engenharia] Construir primeiro uma fatia fina de ponta a ponta? Um walking skeleton é uma versão mínima que roda de ponta a ponta, feita primeiro para provar que as peças se conectam antes de entrarem as funções de verdade.

No MVP, essa fatia seria: entrar no sistema, cadastrar um cliente, enviar ao Backoffice, aceitar e publicar no tópico. Os riscos que a viabilidade apontou (tópico inexistente, ambiente novo, prazo curto) favorecem provar a integração cedo.

A. Sim, construir a fatia fina primeiro e só depois as demais funções
B. Não, seguir a ordem do backlog sem uma fatia inicial separada
C. Not yet defined
X. Other (please specify)

[Answer]: A

## Q3. [Engenharia] Que regras de formatação e de estilo de código o time quer seguir?

A linguagem e a stack ainda não foram escolhidas, então não dá para nomear um formatador específico.

A. O formatador e o linter padrão da linguagem escolhida, rodando na integração, com falha bloqueando o merge (padrão sugerido)
B. Só o formatador padrão da linguagem, sem linter obrigatório
C. Decidir quando a stack for escolhida
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Q4. [Qualidade] Em que ordem escrever o código e os testes?

O padrão sugerido é escrever cada camada do sistema e, em seguida, os testes dela (teste depois). O PRD tem muitas regras de negócio, o que pode favorecer cenários de aceite antes do código.

A. Teste depois: implementar cada camada e escrever os testes dela em seguida (padrão sugerido)
B. Teste antes (TDD): escrever o teste de cada comportamento antes do código dele
C. Misto: cenários de aceite antes do código e testes menores depois dele
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Q5. [Qualidade] Que cobertura mínima de testes o MVP exige antes de um merge?

O padrão do escopo `mvp` é 80% das linhas cobertas, com os testes rodando na integração antes do merge.

A. 80% das linhas e testes na integração antes do merge (padrão sugerido)
B. Outro valor mínimo (diga qual)
C. Sem piso de cobertura, só exigir que os testes existentes passem
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Q6. [Entrega] Como o código chega ao ambiente de homologação e ao de produção?

O padrão sugerido é publicar sozinho em homologação a cada merge e exigir aprovação manual separada para produção.

A. Homologação automática a cada merge, produção com aprovação manual (padrão sugerido)
B. Tudo manual: alguém publica cada ambiente quando decidir
C. Automático até produção, sem aprovação manual
D. Not yet defined
X. Other (please specify)

[Answer]: B

## Q7. [Entrega] Quem aprova uma publicação em produção?

A viabilidade não define quem aprova. A resposta vale só se a Q6 mantiver uma aprovação manual.

A. O líder técnico e o responsável pelo produto, os dois (padrão sugerido)
B. Só o líder técnico
C. Quem conduz o PRD
D. Not yet defined
X. Other (please specify)

[Answer]: C

## Q8. [Entrega] O que o congelamento de mudanças do fim do ano proíbe?

A viabilidade registrou congelamento em dezembro e início de janeiro, sem a regra exata.

A. Nenhuma publicação em produção nesse período
B. Só publicações de correção urgente, com aprovação
C. Ainda não sei a regra exata
D. Not yet defined
X. Other (please specify)

[Answer]: B

## Q9. [Conformidade] Há alguma regra absoluta que o time nunca pode quebrar?

Uma regra absoluta vira uma regra "sempre" ou "nunca" nos registros do projeto. Só entra o que você declarar aqui. O sistema guarda CPF, e-mail, telefone, data de nascimento e endereço, e a LGPD vale (`feasibility-assessment.md`).

A. Nenhuma por enquanto
B. Sim, sobre dados pessoais (por exemplo, nunca registrar CPF em logs ou mensagens de erro)
C. Sim, outra regra absoluta (diga qual)
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Consolidated Summary Confirmation

Does this all look correct before I generate the artifact?

- Ramos (Q1): ramos longos por funcionalidade, que voltam ao `main` quando a funcionalidade termina. Isso muda o padrão sugerido, que era ramos curtos com squash.
- Fatia fina (Q2): sim, construir primeiro uma fatia fina de ponta a ponta (entrar, cadastrar, enviar, aceitar e publicar no tópico) e só depois as demais funções.
- Estilo de código (Q3): o formatador e o linter padrão da linguagem escolhida, rodando na integração, com falha bloqueando o merge.
- Testes (Q4): teste depois, ou seja, implementar cada camada e escrever os testes dela em seguida.
- Cobertura (Q5): 80% das linhas e testes na integração antes do merge.
- Publicação (Q6): tudo manual; alguém publica cada ambiente quando decidir. Isso muda o padrão sugerido, que era homologação automática.
- Aprovador (Q7): quem conduz o PRD aprova uma publicação em produção.
- Congelamento (Q8): no fim do ano, só publicações de correção urgente, com aprovação.
- Regras absolutas (Q9): nenhuma por enquanto, então as duas listas de regras ficam vazias.

- Looks correct
- Request changes

[Answer]: Looks correct
