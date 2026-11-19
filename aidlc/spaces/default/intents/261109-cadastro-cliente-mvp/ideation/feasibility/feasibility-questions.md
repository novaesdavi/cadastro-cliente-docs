# Viabilidade e Restrições — Perguntas

As opções abaixo partem da declaração de intenção aprovada e do PRD (`aidlc/spaces/default/knowledge/documents/PRD.md`, versão 7). Escolha a que vale para este MVP, ou escreva a sua.

## Q1. [Negócio] Há data prevista para desligar o sistema de terceiro?

O PRD (decisão de 2026-10-25) diz que o sistema de terceiro fica em uso somente até a publicação e a liberação do novo. A resposta mostra se existe um prazo que limita o MVP.

A. Sim, há uma data fixa de desligamento (diga qual)
B. Não, ele só sai quando o novo sistema for liberado
C. Not yet defined
X. Other (please specify)

[Answer]: C

## Q2. [Gestão] Que limites de prazo e de orçamento valem para o MVP?

O PRD não define prazo para atingir os 10 cadastros. Aqui perguntamos se há limites para construir e liberar o sistema.

A. Há uma data-limite para liberar o MVP (diga qual)
B. Há um limite de orçamento (diga qual)
C. Os dois: data-limite e limite de orçamento (diga quais)
D. Nenhum dos dois é conhecido hoje
X. Other (please specify)

[Answer]: A

## Q3. [Gestão] Há bloqueios da organização que possam atrasar o MVP? (select all that apply)

Por exemplo, períodos em que mudanças em produção são proibidas, disputa por pessoas ou aprovações de outras áreas.

A. Nenhum bloqueio conhecido
B. Congelamento de mudanças em algum período (diga quando)
C. Falta de pessoas disponíveis por causa de outras prioridades
D. Dependência de aprovação de outra área para publicar no tópico
E. Not yet defined
X. Other (please specify)

[Answer]: A, B

## Q4. [Arquitetura] Que serviço de tópico as outras áreas já usam hoje?

O PRD (seção 10) declara o uso de tópico como restrição do stakeholder, sem dizer qual tecnologia. Isso define a integração mais importante do MVP.

A. Já existe um serviço de tópico (ou mensageria) da empresa que as áreas consomem (diga qual)
B. Ainda não existe: é preciso escolher e criar um para este MVP
C. Not yet defined
X. Other (please specify)

[Answer]: B

## Q5. [Arquitetura] Como os colaboradores vão entrar no sistema e receber seus perfis?

O PRD (seção 9) exige autenticação e dois perfis (setor de Cadastro e Backoffice), e deixa a administração de usuários e perfis fora do sistema.

A. Há um provedor de identidade da empresa (login único) que fornece o login e os perfis
B. O sistema precisa ter login e perfis próprios, com a administração feita fora dele, como o PRD diz
C. Not yet defined
X. Other (please specify)

[Answer]: B

## Q6. [Infraestrutura] Que contas e serviços de nuvem estão em uso hoje?

A resposta mostra onde o MVP pode rodar sem criar uma estrutura nova.

A. Já há conta AWS e serviços em uso na empresa (diga quais)
B. Vamos usar AWS, mas a conta ainda precisa ser criada
C. Não vamos usar AWS (diga o ambiente)
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Q7. [Tecnologia] Existe uma stack padrão da empresa e o time conhece ela?

A resposta evita escolher uma tecnologia que o time não sabe sustentar.

A. Existe uma stack padrão que o time deve seguir (diga qual)
B. Não há padrão: o time pode escolher a tecnologia
C. Not yet defined
X. Other (please specify)

[Answer]: B

## Q8. [Conformidade] Que exigências de proteção de dados pessoais valem para este sistema?

O sistema guarda CPF, e-mail, telefone, data de nascimento e endereço. O PRD (seção 9) diz que nenhum dado é mascarado e que não há prazo de guarda definido nesta versão.

A. Há política de privacidade ou exigência legal (por exemplo, a LGPD) que o sistema precisa cumprir além do PRD (diga qual)
B. Nenhuma exigência além do que o PRD já descreve
C. Not yet defined
X. Other (please specify)

[Answer]: A

## Q9. [Gestão] Qual é a data-limite para liberar o MVP?

Na Q2 você disse que há uma data-limite, mas não disse qual. Escolha o intervalo, ou escreva a data exata em Other.

A. Em até 3 meses
B. Entre 3 e 6 meses
C. Em mais de 6 meses
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Q10. [Gestão] Existe um congelamento de mudanças? Em que período?

Na Q3 você marcou "Nenhum bloqueio conhecido" e também "Congelamento de mudanças". As duas respostas não podem valer juntas.

A. Sim, há um congelamento de mudanças (escreva o período em Other)
B. Não, marquei por engano: não há nenhum bloqueio conhecido
C. Not yet defined
X. Other (please specify)

[Answer]: A

## Q11. [Infraestrutura] Que serviços AWS já estão em uso na empresa? (select all that apply)

Na Q6 você disse que já há conta AWS e serviços em uso. A resposta mostra o que o MVP pode reaproveitar.

A. Computação (servidores, contêineres ou funções)
B. Banco de dados gerenciado
C. Mensageria ou filas
D. Só conta, rede e identidade, sem serviços de aplicação
E. Not yet defined
X. Other (please specify)

[Answer]: D (só tem conta, mas sem nenhum serviço)

## Q12. [Conformidade] Qual é a exigência de proteção de dados pessoais?

Na Q8 você disse que há uma exigência além do PRD, mas não disse qual.

A. A LGPD (Lei Geral de Proteção de Dados)
B. Uma política interna de privacidade da empresa
C. As duas: a LGPD e a política interna
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Q13. [Gestão] Em que período há congelamento de mudanças?

Na Q10 você confirmou que há um congelamento, mas não disse o período. Escolha o que mais se aproxima, ou escreva o período exato em Other.

A. No fim do ano (dezembro e início de janeiro)
B. Em fechamentos mensais ou trimestrais
C. Em períodos que a empresa define caso a caso
D. Not yet defined
X. Other (please specify)

[Answer]: A

## Consolidated Summary Confirmation

Does this all look correct before I generate the artifact?

- Desligamento do sistema de terceiro (Q1): sem data definida.
- Prazo e orçamento (Q2, Q9): há uma data-limite para liberar o MVP, em até 3 meses; não foi informado limite de orçamento.
- Bloqueios (Q3, Q10, Q13): há congelamento de mudanças no fim do ano (dezembro e início de janeiro); a marcação "nenhum bloqueio conhecido" da Q3 foi corrigida pela Q10.
- Tópico (Q4): ainda não existe um serviço de tópico; é preciso escolher e criar um para este MVP.
- Autenticação (Q5): o sistema tem login e perfis próprios, com a administração feita fora dele, como o PRD diz.
- Nuvem (Q6, Q11): a empresa tem conta AWS, mas sem nenhum serviço de aplicação em uso.
- Stack (Q7): não há stack padrão; o time escolhe a tecnologia.
- Dados pessoais (Q8, Q12): vale a LGPD, além do que o PRD descreve.

- Looks correct
- Request changes

[Answer]: Looks correct
