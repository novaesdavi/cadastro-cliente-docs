# Pré-PRD — Sistema de Cadastro de Novos Clientes

Última atualização: 2026-10-25

## Insumos recebidos

### 2026-10-25 — Primeiro insumo do stakeholder (texto original)

> tenho a necessidade de um sistema de cadastro de novos clientes de uma empresa, pois a empresa esta realizando o cadastro através de um sistema de terceiro que está em back level e não tem mais manutenção necessária. Nesse novo sistema, terei uma página web com autenticação e tenha perfis de acesso para diferentes  usuários. Esse cadastro é preenchido em tela e quando cadastrado é enviado para verificação e análise para o setor de backoffice que não pode cadastrar novos usuários, mas pode ajustar cadastros já iniciados pelo primeiro setor (setor de cadastro). Quando não há problemas de preenchimento o cadastro é concluído e o primeiro setor poderá ver a tela de status com o status concluído.
> Ao preencher o novo cadastro, preciso ter um aviso que indique que o cadastro foi realizar e que exista um botão de consulta de status.
> Antes de cadastrar um novo cliente preciso consultar o CPF para analisar se o cliente já existe, e se existir ele deve ver a mensagem de cadastro já iniciado e um link para consultar os dados cadastrais do cliente. a pesquisa precisa estar numa tela, o preenchimento e edição em outra. Acredito que possa ter a mesma tela, mas com funções distintas por área como área de cadastro e área de backoffice.

Material de apoio consultado (somente para perguntas e orientações, não como fonte de requisitos): `treinamento_ai_squad_autonoma_cadastro_clientes.md`.

### 2026-10-25 — Segundo insumo: respostas às perguntas bloqueantes 1 a 7 (texto original)

> **1.** os usuários do backoffice não pode cadastrar novos clientes. Não haverá um perfil administrador, isso fiocará fora desse sistema, talvez dentro da infra do próprio sistema, mas não será contemplado fluxo de administrador.
>
> **2.** Pode ter um rascunho sim, podemos ter o botão salvar e o enviar para backoffice.
>
> **3.** Precisa ter um botão Devolver para correção, mas deverá ser incluído o motivo da devolução num campo de "motivo". Quam marca o cadastro como concluído éo Backoffice mesmo. Deve haver os status Rascunho, Enviado para Backoffice, devolvido para correção, aceito e enviado para processamento, que é quando o Backoffice aceitou o cadastro e enviou para outra área fora desse escopo.
>
> **4.** Quando CPF já existe o sistema deve sim impedir um novo cadastro mesmo que esteja em análise. Mas é possível consultar o CPF na tela de status de cadastros para ver o status desse CPF. Todos podem abrir os dados castrais, se estiver para o time de castro, pode editar, mas se estiver como em analise do Backoffice ou concluído, o backoffice precisa devolver cadastro solitando ajuste, mesmo após concluído.
>
> **5.** deve prodcurar dado somente no próprio sistema. Não haverá migração. Irá funcionar em paralelo somente até a publicação e liberação desse novo.
>
> **6.** Devem ser preenchidos: Nome, e-mail, telefone, data nascimento , endereço e CPF. somente nome e CPF devem ser obrigatórios.
>
> **7.** Vo saber que deu certo depois de 10 cadstros feitos pela área de cadastro.

Perguntas 8 a 14 da rodada anterior: sem resposta.

## Premissas a validar

Resolvidas nesta rodada (registradas no histórico do PRD): P01 confirmada, P02 confirmada, P03 negada (existe rascunho), P04 confirmada.

| ID | Interpretação | Motivo | Seção do PRD afetada |
|---|---|---|---|
| P05 | O Backoffice também usa a consulta de CPF e a tela de status. | Foi confirmado que "todos podem abrir os dados cadastrais", mas não foi dito quem usa a consulta de CPF e a tela de status além do setor de Cadastro. | 3, 6 (RF03, RF09, RF14) |
| P06 | Pesquisa e preenchimento/edição podem ser a mesma tela para as duas áreas, com funções diferentes por área. | Foi dito como "acredito que possa ter"; é sugestão, não confirmação. Também é detalhe de solução, que pode não precisar estar no PRD. | 6 (RF10) |
| P07 | Depois de corrigir um cadastro devolvido, o setor de Cadastro o reenvia pela ação "Enviar para Backoffice" e o cadastro volta ao status Enviado para Backoffice. | A resposta 4 diz que o setor de Cadastro pode editar o cadastro que está com ele, mas não diz como o cadastro corrigido volta ao Backoffice. | 5.3, 5.5, 7 |
| P08 | "Concluído" e "Aceito e enviado para processamento" são o mesmo status. | A resposta 3 diz que o Backoffice "marca como concluído", mas a lista de status não tem "Concluído". | 3, 5.5, 7 (RN03) |
| P09 | "Em análise do Backoffice" (resposta 4) corresponde ao status Enviado para Backoffice, e não a um status separado. | A lista de status da resposta 3 não tem "Em análise". | 5.5 |
| P10 | O motivo da devolução fica visível para o setor de Cadastro no cadastro devolvido. | O motivo é obrigatório, mas não foi dito quem o vê nem onde. | 5.3, 6 (RF12) |

## Conflitos e ambiguidades

- **"concluído" x "aceito e enviado para processamento"**: o primeiro insumo e as respostas 3 e 4 falam em "concluído", mas a lista de status da resposta 3 não tem esse status; o último status é "aceito e enviado para processamento". Ver P08.
- **"em análise do Backoffice" x "Enviado para Backoffice"**: a resposta 4 cita "em análise", que não está na lista de status da resposta 3. Ver P09.
- **Ajuste direto pelo Backoffice x devolução**: o primeiro insumo diz que o Backoffice "pode ajustar cadastros já iniciados". A resposta 4 diz que, se o cadastro estiver em análise ou concluído, "o backoffice precisa devolver cadastro solicitando ajuste". Não está claro se o Backoffice continua ajustando diretamente ou se todo ajuste passa pela devolução. O PRD mantém RF08 (ajuste pelo Backoffice) como estava no primeiro insumo, sem definir campos nem status em que o ajuste é permitido.
- **Devolução depois do aceite**: a resposta 4 diz que o Backoffice pode devolver o cadastro "mesmo após concluído". Pela resposta 3, nesse momento o cadastro já foi enviado para outra área, fora do escopo. Não está claro o que acontece com o processamento já iniciado nessa área. Essa transição (Aceito e enviado para processamento → Devolvido para correção) **não** foi levada ao PRD até ser esclarecida.
- **Edição depois do envio**: a pergunta 2 (o setor de Cadastro pode editar depois de enviar?) não foi respondida diretamente; a resposta 4 indica que não, salvo devolução. O PRD registra isso em RN07, com base na resposta 4.
- **Momento do aviso "cadastro realizado"**: o primeiro insumo pede um aviso de que o cadastro foi realizado. Com as ações "Salvar" e "Enviar para Backoffice" (resposta 2), não está claro se o aviso aparece ao salvar, ao enviar ou em ambos.
- **Convivência com o sistema de terceiro**: a resposta 5 diz que os sistemas funcionam "em paralelo somente até a publicação e liberação desse novo". Não está claro se, após a liberação, o sistema de terceiro deixa de ser usado imediatamente, nem como evitar que o mesmo cliente seja cadastrado nos dois sistemas.
- **"usuário" x "cliente"**: resolvido. No PRD, **usuário** = colaborador que opera o sistema e **cliente** = pessoa cadastrada (resposta 1).
- **"cadastro" com dois sentidos**: nome do setor (setor de Cadastro) e o registro do cliente. No PRD, usa-se "setor de Cadastro" para a área e "cadastro" para o registro.
- **Telas**: "a pesquisa precisa estar numa tela, o preenchimento e edição em outra" (afirmação) convive com "acredito que possa ter a mesma tela, mas com funções distintas por área" (sugestão). Ver P06.
- **Material de apoio x insumo**: o roteiro do treinamento cita auditoria e outros itens não ditos pelo stakeholder; esses itens ficam apenas como perguntas e orientações.

## Perguntas abertas

Ordenadas por impacto em escopo. [BLOQUEANTE] = impede o PRD de ficar pronto.

1. [BLOQUEANTE] Na lista de status que você passou não aparecem "Concluído" nem "Em análise". "Concluído" é o mesmo que "Aceito e enviado para processamento"? E "em análise do Backoffice" é o mesmo que "Enviado para Backoffice", ou precisa existir um status "Em análise" (por exemplo, quando um analista pega o cadastro)? (P08, P09)
2. [BLOQUEANTE] O Backoffice continua podendo ajustar o cadastro diretamente, sem devolvê-lo? Se sim, em quais status e quais campos ele pode alterar (por exemplo, pode alterar o CPF)? Ou todo ajuste deve passar pela devolução ao setor de Cadastro?
3. [BLOQUEANTE] Você disse que o Backoffice pode devolver um cadastro mesmo depois de concluído. Nesse momento ele já foi enviado para outra área. O que acontece com o processamento nessa área? O cadastro volta para Devolvido para correção? E o "envio para processamento" é só uma mudança de status neste sistema, ou os dados precisam ser transmitidos para outro sistema ou área?
4. [BLOQUEANTE] Depois de corrigir um cadastro devolvido, o setor de Cadastro o reenvia por "Enviar para Backoffice" e ele volta ao status Enviado para Backoffice? O motivo da devolução fica visível para quem vai corrigir? O Backoffice pode recusar ou cancelar um cadastro de vez, ou só devolver e aceitar? (P07, P10)
5. [BLOQUEANTE] Quais validações cada campo precisa (formato de e-mail, telefone, data de nascimento, CPF válido, idade mínima)? O endereço é um único campo ou dividido (CEP, rua, número, cidade, UF)? O que acontece se o CPF digitado for inválido? Nome e CPF são exigidos já ao salvar o rascunho ou só ao enviar para o Backoffice? Há documentos a anexar?
6. [BLOQUEANTE] Sobre a meta de 10 cadastros: conta o cadastro enviado ao Backoffice ou só o aceito? Há prazo para atingir esses 10 (por exemplo, no primeiro mês após a liberação) ou algum critério de qualidade (por exemplo, sem devolução)? E o que fica explicitamente fora desta primeira versão, além do perfil administrador, da migração e do processamento pela outra área?
7. [BLOQUEANTE] O que é preciso registrar sobre quem fez cada ação (criou, salvou, enviou, ajustou, devolveu, aceitou), quando e o que mudou? Quem pode consultar esse histórico? Algum dado (por exemplo, CPF ou data de nascimento) deve aparecer mascarado em consultas, ou há prazo de guarda dos dados?
8. O aviso de "cadastro realizado" com o botão de consulta de status deve aparecer ao salvar o rascunho, ao enviar para o Backoffice ou nos dois casos?
9. O setor de Cadastro vê todos os cadastros na tela de status, ou apenas os que o próprio usuário iniciou? O Backoffice também usa a consulta de CPF e a tela de status? (P05)
10. Dois usuários podem trabalhar no mesmo cadastro ao mesmo tempo? O Backoffice trabalha com uma fila de cadastros a analisar? Um mesmo usuário pode ter os dois perfis?
11. Existe prazo para o Backoffice analisar um cadastro? O que acontece se ele não for cumprido?
12. Há data prevista para deixar de usar o sistema de terceiro? Até lá, como evitar que o mesmo cliente seja cadastrado nos dois sistemas?
13. A pesquisa e o preenchimento devem ser a mesma tela para as duas áreas, com funções diferentes, ou telas separadas por área? (P06)
14. Há metas de disponibilidade, horário de uso ou volume de cadastros por dia que o sistema precisa suportar?

## Orientações

- **Fora do escopo**: já há itens confirmados (administrador, migração, consulta ao legado, processamento pela outra área). Vale listar outros que não entram na primeira versão (por exemplo: comunicação com o cliente, aplicativo móvel, relatórios).
- **Devolução após aceite**: permitir devolver um cadastro já enviado para outra área exige combinar com essa área como cancelar ou suspender o processamento; caso contrário, o mesmo cliente pode ser processado com dados que depois mudam.
- **Segregação de funções**: considerar se um mesmo usuário pode ter os dois perfis e, nesse caso, se pode aceitar um cadastro que ele mesmo iniciou.
- **Auditoria**: com análise, ajuste e devolução por outra área, costuma-se registrar quem fez cada ação, quando, o que foi alterado e o motivo.
- **Dados sensíveis (LGPD)**: CPF, data de nascimento, endereço, e-mail e telefone são dados pessoais. Como todos os perfis podem abrir os dados cadastrais, vale definir se algum dado aparece mascarado e por quanto tempo os dados são guardados.
- **Administração de acessos**: fica fora deste sistema, mas alguém precisa criar usuários, atribuir perfis e removê-los quando o colaborador sai. Vale registrar quem é o responsável, para não bloquear a liberação.
- **Legado e CPF duplicado**: como a consulta de CPF não olha o sistema de terceiro e não haverá migração, clientes já cadastrados no sistema antigo podem ser cadastrados de novo no novo sistema sem aviso. Vale confirmar se isso é aceitável.
- **Métrica de sucesso**: "10 cadastros" fica mais verificável com prazo e critério do que conta como cadastro feito.

## Checklist de prontidão

- [ ] Problema e objetivo descritos, com ao menos uma métrica de sucesso. *(Problema, objetivo e métrica confirmados; falta definir o que conta como cadastro feito e se há prazo — pergunta 6.)*
- [ ] Todos os perfis definidos, com permissões e proibições. *(Cadastro e Backoffice com permissões e proibições; administrador fora do sistema. Falta: ajuste direto pelo Backoffice e campos (pergunta 2), visibilidade dos cadastros (pergunta 9), usuário com os dois perfis (pergunta 10).)*
- [ ] Escopo e fora do escopo explícitos. *(Dentro do escopo e quatro itens fora do escopo confirmados; falta a confirmação do que mais fica fora da primeira versão — pergunta 6.)*
- [ ] Fluxo principal e fluxos alternativos/de erro descritos de ponta a ponta. *(Principal, rascunho, devolução e CPF existente descritos. Falta: reenvio após correção, recusa, CPF inválido, devolução após aceite — perguntas 3, 4 e 5.)*
- [ ] Ciclo de vida (estados e transições) definido, se houver. *(Quatro status e transições principais confirmados. Falta: "Concluído"/"Em análise", reenvio, devolução após aceite, recusa — perguntas 1, 3 e 4.)*
- [ ] Campos, obrigatoriedade e validações definidos. *(Campos e obrigatoriedade confirmados; faltam validações, estrutura do endereço, documentos e momento da obrigatoriedade — pergunta 5.)*
- [ ] Regras de negócio com exceções. *(RN01 a RN08 confirmadas; faltam exceções de CPF inválido, reenvio e devolução após aceite.)*
- [ ] Integrações e legado tratados (ou marcados como fora do escopo). *(Legado tratado: sem consulta, sem migração, uso até a liberação. Falta: natureza do envio para processamento — pergunta 3.)*
- [ ] Requisitos não funcionais mínimos (segurança, dados sensíveis, auditoria). *(Só autenticação e perfis; auditoria e dados sensíveis em aberto — pergunta 7.)*
