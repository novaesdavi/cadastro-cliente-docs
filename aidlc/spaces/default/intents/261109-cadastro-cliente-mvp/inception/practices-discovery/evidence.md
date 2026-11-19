# Evidências — Descoberta de Práticas

## O que foi inspecionado

- `aidlc/spaces/default/memory/org.md`: as cinco seções (Way of Working, Walking Skeleton, Testing Posture, Deployment, Code Style) como padrões sugeridos. Projeto novo, portanto greenfield.
- `aidlc/spaces/default/memory/team.md`: seções vazias; não havia baseline afirmado.
- `ideation/feasibility/feasibility-assessment.md` e `constraint-register.md`: prazo de 3 meses (C06), congelamento de fim de ano (C07), conta AWS sem serviços de aplicação (C04), sem stack padrão (C09), LGPD aplicável (C10), serviço de tópico a criar (C02).
- `ideation/scope-definition/scope-document.md`: escopo completo do PRD v7 no MVP; se não couber, a data se move e o escopo fica.
- Git: ramos `main` e `setup-aidlc`; commits lineares (HEAD `f56309e`). Não há CI, configuração de implantação nem ramos de feature.

## O que foi inferido

- O histórico git não permite concluir uma estratégia de ramificação; as sugestões vieram do org.md e foram substituídas pelas respostas da pessoa.
- A recomendação de fatia fina decorreu do risco de prazo e da infraestrutura inexistente.
- O valor `skeleton` do escopo `mvp` não foi verificado nesta etapa.

## Decisões da entrevista

- Q1 (B): ramos longos por funcionalidade, que voltam ao `main` quando a funcionalidade termina. Substituiu o padrão sugerido (ramos curtos com squash).
- Q2 (A): construir primeiro uma fatia fina de ponta a ponta e só depois as demais funções.
- Q3 (A): formatador e linter padrão da linguagem escolhida, em CI, com falha bloqueando o merge.
- Q4 (A): teste depois (Methodology `test-after`), implementando cada camada e escrevendo os testes dela em seguida.
- Q5 (A): piso de 80% das linhas e testes em CI antes do merge.
- Q6 (B): publicação toda manual; alguém publica cada ambiente quando decidir. Substituiu o padrão sugerido (homologação automática a cada merge).
- Q7 (C): quem conduz o PRD aprova uma publicação em produção. Substituiu o padrão sugerido (líder técnico e responsável pelo produto).
- Q8 (B): no congelamento do fim do ano, só publicações de correção urgente, com aprovação.
- Q9 (A): nenhuma regra absoluta por enquanto; `## Mandated` e `## Forbidden` ficam com `None.`.
- O resumo consolidado foi confirmado pela pessoa (Looks correct).

## Incertezas não resolvidas

- A linguagem e a stack não foram escolhidas; formatador, linter e ferramentas de CI não podem ser nomeados.
- Quem conduz o PRD (e, portanto, aprova a produção) não foi nomeado.
- A data exata de início do prazo de 3 meses é desconhecida.
- O tamanho e a experiência do time com testes e AWS não foram informados.
- O rascunho não teve revisão de suporte (colaboradores desativados).
