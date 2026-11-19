# Avaliação de Viabilidade — Sistema de Cadastro de Novos Clientes (MVP)

Esta avaliação parte da declaração de intenção aprovada (`ideation/intent-capture/intent-statement.md`) e das respostas em `feasibility-questions.md`. Onde falta informação, o texto marca a frase como hipótese.

## Resumo

O MVP é viável, com condições. Nada impede o projeto, mas três pontos pedem decisão antes de começar: o prazo de até 3 meses (Q9) é curto para o tamanho do PRD, o serviço de tópico ainda não existe (Q4) e a exigência da LGPD (Q12) não aparece nas regras do PRD sobre dados pessoais.

| Área | Situação | Fonte |
|---|---|---|
| Prazo e orçamento | Atenção: prazo curto, orçamento desconhecido | Q2, Q9 |
| Integração por tópico | Atenção: o serviço precisa ser escolhido e criado | Q4, PRD seção 10 |
| Acesso e perfis | Viável: login e perfis próprios, administração fora do sistema | Q5, PRD seção 9 |
| Ambiente de nuvem | Atenção: há conta AWS, sem nenhum serviço em uso | Q6, Q11 |
| Equipe e tecnologia | Viável: sem padrão da empresa, o time escolhe | Q7 |
| Dados pessoais | Atenção: a LGPD vale, e o PRD não mascara dados nem define prazo de guarda | Q8, Q12, PRD seção 9 |
| Organização | Atenção: congelamento de mudanças no fim do ano | Q3, Q10, Q13 |

## Viabilidade por área

### Prazo e orçamento

Há uma data-limite para liberar o MVP, em até 3 meses (Q9). Não foi informado limite de orçamento (Q2).

Hipótese: o PRD v7 tem muitas regras (ciclo de vida do cliente, pedidos de alteração, cancelamento e reabertura, histórico de cada campo), e a declaração de intenção confirma que o MVP cobre tudo, exceto o que o PRD lista como fora do escopo (Q9 da Captura da Intenção). Cabe validar nas próximas etapas se isso cabe em 3 meses. Se não couber, a decisão é cortar escopo ou mover a data, e ela é do decisor.

### Integração por tópico

O PRD declara o uso de tópico como restrição do stakeholder (seção 10). Hoje não existe serviço de tópico para as áreas (Q4). Então o MVP depende de escolher e criar esse serviço, e de combinar com as áreas que vão consumir o que será publicado em cada evento (primeiro aceite, alteração aceita, cancelamento aceito, reabertura aceita).

Hipótese: as áreas consumidoras ainda não têm sistema pronto para receber esses eventos. Essa dependência não foi confirmada.

### Acesso e perfis

O sistema tem login e perfis próprios (Setor de Cadastro e Backoffice), e a administração de usuários e perfis fica fora dele (Q5, PRD seção 9). É viável. Falta definir quem faz essa administração fora do sistema (ver `raid-log.md`, dependência D3).

### Ambiente de nuvem

A empresa tem conta AWS, mas nenhum serviço de aplicação em uso (Q6, Q11). O MVP não pode reaproveitar serviços existentes e vai precisar de ambiente novo.

### Equipe e tecnologia

Não há stack padrão da empresa (Q7), então o time escolhe a tecnologia. A escolha fica para as etapas de projeto. Não foi informado o perfil do time.

### Dados pessoais

O sistema guarda CPF, e-mail, telefone, data de nascimento e endereço, e a LGPD vale para ele (Q8, Q12). O PRD diz que nenhum dado é mascarado, que os dois perfis veem tudo e que não há prazo de guarda nem exclusão automática (seção 9).

Hipótese: essas regras do PRD podem entrar em conflito com a LGPD, por exemplo quanto a guardar dados sem prazo. Isso precisa de análise de quem responde pela conformidade, e não foi confirmado.

### Organização

Há congelamento de mudanças no fim do ano, em dezembro e início de janeiro (Q10, Q13). A marcação "nenhum bloqueio conhecido" da Q3 foi corrigida pela Q10.

Hipótese: se o prazo de 3 meses for contado a partir de hoje (19 de novembro de 2026), o congelamento cai dentro dele e reduz o tempo útil. A data de início do prazo não foi informada.

## Conclusão

Viável com condições. Para seguir com segurança, as próximas etapas precisam tratar: o serviço de tópico e o formato dos eventos, a análise do PRD à luz da LGPD, e a relação entre o prazo, o congelamento do fim do ano e o escopo.

## Assumptions & Open Questions

- Hipótese: 3 meses é suficiente para o escopo completo do PRD v7 exceto o que está fora do escopo. Não foi validada.
- Hipótese: o prazo de 3 meses conta a partir de hoje, 19 de novembro de 2026. Não foi confirmado.
- Hipótese: as áreas consumidoras ainda não têm sistema pronto para receber os eventos do tópico. Não foi confirmado.
- Hipótese: as regras do PRD sobre dados pessoais (sem mascaramento, sem prazo de guarda) podem conflitar com a LGPD.
- Pergunta aberta: existe limite de orçamento? A Q2 só confirmou a data-limite.
- Pergunta aberta: quem administra usuários e perfis fora do sistema?
