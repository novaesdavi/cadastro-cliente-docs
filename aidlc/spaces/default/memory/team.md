# Team-Level Rules

> This team's affirmed practices and corrections. Loaded after `org.md` as
> strict-additive guidance; contradictions with broader policy are rejected.
> Populated by the practices-discovery affirmation gate. Edit at the gate,
> not directly.

## Way of Working

- Trabalhamos com ramos longos por funcionalidade, que voltam ao `main` quando a funcionalidade termina (Q1, opção B). Isso substitui o padrão sugerido de ramos curtos com squash.
- Um commit pedido vai para o ramo em que já estamos; só criamos ramo novo quando alguém pedir ou quando a funcionalidade em andamento exigir o seu ramo longo.

## Walking Skeleton

- Construímos primeiro uma fatia fina de ponta a ponta: entrar no sistema, cadastrar um cliente, enviar ao Backoffice, aceitar e publicar no tópico. Só depois entram as demais funções (Q2, opção A).
- A verificação do esqueleto usa o comando de verificação de Construção autorizado por uma pessoa, e a aprovação do checkpoint é humana.

## Testing Posture

- **Methodology**: test-after
- **Ordering**: Implementar cada camada testável aplicável e, em seguida, escrever e executar os testes dessa camada.
- **Methodology evidence**: Resposta da pessoa na Q4 (opção A): teste depois, ou seja, implementar cada camada e escrever os testes dela em seguida.
- Piso de cobertura de 80% das linhas e execução dos testes em CI antes do merge (Q5, opção A).

## Guard Policy

<!-- Affirmed by the team. Mode: strict, relaxed, or off. Strict here holds for every intent, whatever one person asks in chat; relaxed or off here applies to every intent whose policy came from its scope, unless project.md or the person sets another; changing this line changes it. A section under the retired Change Control heading, written by an earlier release, is still read. -->

## Deployment

- A publicação é toda manual: alguém publica cada ambiente quando decidir (Q6, opção B). Isso substitui o padrão sugerido de homologação automática a cada merge.
- Quem conduz o PRD aprova uma publicação em produção (Q7, opção C). A pessoa que conduz o PRD ainda não foi nomeada.
- No congelamento de mudanças do fim do ano (dezembro e início de janeiro), só são permitidas publicações de correção urgente, com aprovação (Q8, opção B).
- Contexto conhecido: a empresa tem conta AWS sem nenhum serviço de aplicação em uso (C04); não há pipeline nem ambiente existentes para reaproveitar.

## Code Style

- Usamos o formatador e o linter padrão da linguagem escolhida, executados em CI, com falha bloqueando o merge (Q3, opção A).
- A linguagem e a stack ainda não foram escolhidas (C09), então o formatador e o linter específicos serão nomeados quando a stack for decidida.
## Forbidden

<!-- Team-specific forbidden patterns -->

## Mandated

<!-- Team-specific mandates -->

## Corrections

<!-- Self-learning loop appends here. -->
