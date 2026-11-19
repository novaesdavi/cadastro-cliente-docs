# Registro RAID — Sistema de Cadastro de Novos Clientes (MVP)

RAID reúne Riscos, Suposições, Problemas e Dependências. Parte da declaração de intenção aprovada (`ideation/intent-capture/intent-statement.md`). Cada linha cita a fonte (Q de `feasibility-questions.md`, seção do PRD v7 ou restrição de `constraint-register.md`).

## Riscos

| ID | Risco | Probabilidade | Impacto | Fonte | O que fazer |
|---|---|---|---|---|---|
| R1 | O prazo de até 3 meses não comporta o escopo completo do PRD v7. | Hipótese: alta | Alto | Q9, C06 | Validar o escopo contra o prazo nas etapas seguintes; se não couber, o decisor escolhe entre cortar escopo e mover a data. |
| R2 | O congelamento de fim de ano reduz o tempo útil do prazo. | Hipótese: média | Médio | Q10, Q13, C07 | Confirmar a data de início do prazo e planejar a entrega considerando o congelamento. |
| R3 | A escolha e a criação do serviço de tópico atrasam a primeira publicação. | Hipótese: média | Alto | Q4, C02 | Tratar o tópico como primeira dependência do projeto (D1). |
| R4 | As regras do PRD sobre dados pessoais conflitam com a LGPD. | Hipótese: média | Alto | Q12, C10, C11 | Pedir análise de quem responde pela conformidade antes de fixar as regras. |
| R5 | Sem serviços AWS em uso, o ambiente novo toma tempo do prazo. | Hipótese: média | Médio | Q11, C04 | Incluir a criação do ambiente no plano e confirmar as permissões da conta (D2). |
| R6 | Sem data de desligamento do sistema de terceiro, a pressão pelo prazo não tem referência. | Média | Baixo | Q1, C05 | Registrar a data quando ela existir. |

## Suposições

| ID | Suposição | Fonte | Confirmada? |
|---|---|---|---|
| A1 | O prazo de 3 meses conta a partir de 19 de novembro de 2026. | Q9 | Não |
| A2 | As áreas consumidoras ainda não têm sistema pronto para receber os eventos do tópico. | PRD seção 10 | Não |
| A3 | Não há limite de orçamento. | Q2 | Não: a Q2 só confirmou a data-limite. |

## Problemas

| ID | Problema | Fonte | Situação |
|---|---|---|---|
| I1 | Não existe serviço de tópico, e o PRD exige esse formato de envio. | Q4, PRD seção 10 | Aberto |
| I2 | Quem administra usuários e perfis fora do sistema não está definido. | Q5, PRD seção 9 | Aberto |

## Dependências

| ID | Dependência | De quem | Fonte |
|---|---|---|---|
| D1 | Escolha e criação do serviço de tópico | Quem decide a tecnologia do MVP | Q4, Q7 |
| D2 | Permissões e acesso à conta AWS para criar o ambiente | Responsável pela conta AWS | Q6, Q11 |
| D3 | Definição de quem administra usuários e perfis | A empresa, fora do sistema | Q5 |
| D4 | Acordo com as áreas consumidoras sobre o conteúdo de cada evento publicado | Áreas que consomem o tópico | PRD seção 10 |
| D5 | Análise das regras de dados do PRD à luz da LGPD | Quem responde pela conformidade | Q12, C10, C11 |

## Assumptions & Open Questions

- Pergunta aberta: o prazo de 3 meses conta a partir de qual data (A1)?
- Pergunta aberta: existe limite de orçamento (A3)?
- Pergunta aberta: quem responde pela conformidade com a LGPD no projeto (D5)?
