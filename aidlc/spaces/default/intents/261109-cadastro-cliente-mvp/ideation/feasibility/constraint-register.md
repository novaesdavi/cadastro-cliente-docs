# Registro de Restrições — Sistema de Cadastro de Novos Clientes (MVP)

Parte da declaração de intenção aprovada (`ideation/intent-capture/intent-statement.md`). Cada restrição cita a fonte: uma resposta de `feasibility-questions.md` (Q) ou uma seção do PRD v7.

## Restrições técnicas

| ID | Restrição | Fonte | Impacto |
|---|---|---|---|
| C01 | Os cadastros aceitos pelo Backoffice são enviados às outras áreas por publicação em tópico. É uma restrição declarada pelo stakeholder. | PRD seção 10 | O desenho da integração parte desse formato. |
| C02 | Ainda não existe um serviço de tópico; é preciso escolher e criar um para este MVP. | Q4 | Cria trabalho e dependência antes da primeira publicação. |
| C03 | O sistema tem login e perfis próprios, e a administração de usuários e perfis fica fora dele. | Q5, PRD seção 9 | O MVP não oferece tela de administração; a gestão de acessos depende de um processo externo. |
| C04 | A empresa tem conta AWS, mas nenhum serviço de aplicação em uso. | Q6, Q11 | O MVP não reaproveita serviços existentes. |
| C05 | O sistema de terceiro continua em uso somente até a publicação e a liberação do novo, e não há migração de dados. | PRD, histórico de decisões de 2026-10-25 | O MVP começa sem dados anteriores. |

## Restrições organizacionais

| ID | Restrição | Fonte | Impacto |
|---|---|---|---|
| C06 | Há uma data-limite para liberar o MVP, em até 3 meses. | Q2, Q9 | Limita o escopo que cabe na primeira versão. |
| C07 | Há congelamento de mudanças no fim do ano (dezembro e início de janeiro). | Q3, Q10, Q13 | Reduz o tempo útil se o prazo de 3 meses cobrir esse período. |
| C08 | Não foi informado limite de orçamento. | Q2 | Custo não é uma restrição conhecida; precisa ser confirmado. |
| C09 | Não há stack padrão da empresa; o time escolhe a tecnologia. | Q7 | Não é uma limitação, mas exige decidir e justificar a escolha. |

## Restrições regulatórias

| ID | Restrição | Fonte | Impacto |
|---|---|---|---|
| C10 | A LGPD vale para o sistema, que guarda CPF, e-mail, telefone, data de nascimento e endereço. | Q8, Q12 | Exige analisar as regras de dados do PRD. |
| C11 | O PRD define que nenhum dado é mascarado, que os dois perfis veem todos os dados e que não há prazo de guarda nem exclusão automática. | PRD seção 9 | Pode conflitar com a C10; a análise ainda não foi feita. |

## Assumptions & Open Questions

- Hipótese: a C11 conflita com a C10. Precisa de análise de quem responde pela conformidade.
- Pergunta aberta: o limite de orçamento (C08) existe ou não?
- Pergunta aberta: o prazo da C06 conta a partir de qual data?
