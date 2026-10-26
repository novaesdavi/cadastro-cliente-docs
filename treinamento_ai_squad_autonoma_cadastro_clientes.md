# Treinamento — AI Squad Autônoma para Cadastro de Clientes

## 0. Objetivo do treinamento

Construir, do zero até produção, uma aplicação de cadastro de novos clientes usando uma **squad de agentes de IA** como principal força de execução.

O objetivo não é apenas construir um CRUD. O treinamento deve reproduzir, em escala reduzida, um cenário corporativo real:

- aplicação web autenticada;
- diferentes perfis de acesso;
- setor de Cadastro criando novos cadastros;
- setor de Backoffice analisando e ajustando cadastros;
- Backoffice sem permissão para criar novos cadastros;
- fluxo de estados;
- validações;
- auditoria;
- segurança;
- observabilidade;
- testes;
- CI/CD;
- infraestrutura AWS;
- agentes capazes de interpretar requisitos, planejar, implementar, testar, revisar e corrigir;
- gates humanos somente quando fizer sentido.

### Resultado final esperado

Ao terminar, você deverá ter:

```text
                    ┌─────────────────┐
                    │   Stakeholder   │
                    └────────┬────────┘
                             │
                             ▼
                    PRD / Business Goal
                             │
                             ▼
                  ┌─────────────────────┐
                  │   Product Agent     │
                  └──────────┬──────────┘
                             │
                      Stories / AC
                             │
                             ▼
                  ┌─────────────────────┐
                  │   Tech Lead Agent   │
                  └──────────┬──────────┘
                             │
                     Technical Plan
                             │
                             ▼
        ┌────────────────────────────────────────┐
        │            AI ENGINEERING SQUAD        │
        │                                        │
        │  Coding Agent   Test Agent   Review    │
        │                                        │
        └──────────────────────┬─────────────────┘
                               │
                               ▼
                              PR
                               │
                               ▼
                       CI/CD + Quality Gates
                               │
                               ▼
                         Human Approval
                               │
                               ▼
                         AWS Production
                               │
                               ▼
                    Monitoring / Feedback
```

---

# 1. Regras do treinamento

## 1.1 Você será o Product Owner / Stakeholder

Você deverá definir:

- problema;
- objetivos;
- regras de negócio;
- prioridades;
- critérios de sucesso.

Não entregue para a IA uma especificação perfeita.

Parte do exercício é verificar se os agentes conseguem detectar ambiguidades.

## 1.2 Eu serei seu professor

Durante o treinamento, meu papel será:

- explicar conceitos;
- propor exercícios;
- revisar suas decisões;
- fazer perguntas;
- apontar riscos;
- desafiar arquitetura;
- revisar artefatos;
- sugerir próximos passos.

Eu não devo simplesmente entregar todo o projeto pronto.

Quando você trouxer uma decisão, primeiro vou avaliar seu raciocínio e depois mostrar o que faltou.

## 1.3 Claude será o executor principal

Você possui AWS + Claude.

Portanto, o projeto será desenhado para funcionar com ferramentas acessíveis nesse ambiente, evitando depender inicialmente de uma grande quantidade de SaaS.

Se uma ferramenta externa for necessária, ela será tratada como uma decisão arquitetural explícita.

## 1.4 Regra de ouro

Não construiremos primeiro a aplicação e depois colocaremos agentes.

**Os agentes fazem parte da arquitetura desde o início.**

---

# 2. Visão do sistema de negócio

## 2.1 Atores

Teremos inicialmente:

### Cadastro

Pode:

- iniciar cadastro;
- criar cliente;
- editar seus próprios cadastros enquanto permitidos;
- enviar cadastro para análise;
- consultar status;
- visualizar resultado.

Não pode:

- aprovar sua própria análise;
- executar atividades exclusivas do Backoffice.

### Backoffice

Pode:

- consultar cadastros enviados para análise;
- analisar;
- corrigir informações de cadastros iniciados pelo Cadastro;
- devolver para correção;
- concluir a análise.

Não pode:

- criar um novo cliente do zero.

### Administrador

Pode:

- administrar usuários;
- administrar perfis;
- consultar auditoria;
- eventualmente reprocessar operações administrativas.

---

# 3. Fluxo de negócio

O fluxo inicial será:

```text
DRAFT
  │
  │ Cadastro envia
  ▼
SUBMITTED
  │
  ▼
UNDER_REVIEW
  │
  ├───────────────┐
  │               │
  │ problema      │ aprovado
  ▼               ▼
RETURNED       COMPLETED
  │
  │ Cadastro corrige
  ▼
SUBMITTED
```

O estado deve ser tratado como uma **máquina de estados**, não como um campo que qualquer endpoint pode alterar livremente.

Exemplo:

```text
DRAFT → SUBMITTED
SUBMITTED → UNDER_REVIEW
UNDER_REVIEW → RETURNED
UNDER_REVIEW → COMPLETED
RETURNED → SUBMITTED
```

Defina explicitamente quais transições são permitidas.

---

# 4. Requisitos funcionais

A primeira versão deverá possuir:

## Autenticação

- login;
- logout;
- sessão/token;
- controle de acesso.

## Autorização

RBAC:

```text
ADMIN
REGISTRATION
BACKOFFICE
```

## Cadastro

Campos iniciais:

- nome completo;
- CPF;
- data de nascimento;
- e-mail;
- telefone;
- endereço;
- profissão;
- renda;
- documentos necessários.

## Consulta

Cadastro deverá visualizar:

- dados;
- status;
- histórico;
- pendências.

Backoffice deverá visualizar:

- fila de análise;
- detalhes;
- histórico;
- alterações.

## Auditoria

Registrar:

- quem executou;
- quando;
- ação;
- estado anterior;
- estado posterior;
- campos alterados;
- motivo.

---

# 5. Requisitos não funcionais

O exercício deve considerar:

### Segurança

- autenticação forte;
- autorização server-side;
- menor privilégio;
- proteção de dados sensíveis;
- criptografia;
- secrets fora do código;
- logs sem dados sensíveis.

### Confiabilidade

- operações idempotentes quando necessário;
- retries;
- tratamento de falhas;
- timeouts;
- DLQ para processamento assíncrono quando aplicável.

### Observabilidade

- logs estruturados;
- métricas;
- tracing;
- dashboards;
- alertas.

### Performance

Defina inicialmente metas, por exemplo:

```text
p95 das APIs principais < 300 ms
```

O número é uma hipótese de treinamento. Você deverá justificar ou alterar a meta.

---

# 6. Primeira grande atividade: Product Discovery

Antes de escrever código, produza:

```text
docs/
  product/
    vision.md
    personas.md
    business-rules.md
    user-journeys.md
    acceptance-criteria.md
```

Não peça ao Claude para inventar tudo.

Você deverá fornecer o contexto inicial e pedir que ele:

1. identifique ambiguidades;
2. faça perguntas;
3. encontre regras conflitantes;
4. proponha cenários extremos;
5. transforme requisitos em histórias.

---

# 7. Exercício de ambiguidade

Você deverá deliberadamente analisar perguntas como:

- O que acontece se o CPF já existir?
- Cadastro pode alterar dados depois de enviado?
- Backoffice pode alterar qualquer campo?
- O que acontece quando o cadastro é devolvido?
- Existe prazo para análise?
- Quem pode reabrir um cadastro concluído?
- Pode existir mais de uma análise simultânea?
- O que acontece se dois usuários editarem o mesmo cadastro?
- Quais campos são obrigatórios?
- Como documentos são armazenados?
- O que acontece quando uma operação falha no meio?
- O cliente pode ser criado sem aprovação?

Essas perguntas são importantes porque **agentes precisam de contexto suficientemente explícito para tomar decisões confiáveis**.

---

# 8. Product Agent

Crie o primeiro agente.

Responsabilidade:

```text
PRD
 ↓
Product Agent
 ↓
Stories
 ↓
Acceptance Criteria
 ↓
Open Questions
```

Ele não deve escrever código.

### Entrada

- PRD;
- regras de negócio;
- personas;
- jornadas.

### Saída

- épicos;
- histórias;
- critérios de aceite;
- regras;
- perguntas abertas;
- dependências.

### Exercício

Dê a ele uma especificação propositalmente incompleta.

Observe se ele:

- inventa requisitos;
- pergunta;
- assume;
- sinaliza riscos.

A habilidade de **não inventar contexto** será um dos critérios de qualidade do agente.

---

# 9. Tech Lead Agent

Depois crie o segundo agente.

Responsabilidade:

```text
Stories
+
Engineering Context
+
Architecture Rules
        ↓
Tech Lead Agent
        ↓
Technical Design
```

Ele deve produzir:

- arquitetura;
- componentes;
- contratos;
- modelo de dados;
- eventos;
- APIs;
- decisões arquiteturais;
- estratégia de testes;
- riscos;
- plano de implementação.

Ele também deverá questionar histórias tecnicamente inviáveis.

---

# 10. Context Engineering

Esta é uma das partes mais importantes do treinamento.

O agente não deve receber apenas:

```text
"Implemente a história 123."
```

Ele precisa recuperar contexto.

Crie:

```text
docs/
  architecture/
  standards/
  adr/
  api/
  security/
  testing/
```

Exemplos:

```text
architecture-principles.md
coding-standards.md
api-guidelines.md
security-guidelines.md
testing-strategy.md
observability.md
aws-guidelines.md
```

O objetivo é criar um **Engineering Context** consumível pelos agentes.

---

# 11. Decisão arquitetural da aplicação

Para o treinamento, considere inicialmente uma arquitetura simples e realista.

Uma possível direção:

```text
Web Browser
     │
     ▼
CloudFront
     │
     ▼
Web Application
     │
     ▼
API Gateway
     │
     ▼
Backend API
     │
     ├──────────────► Database
     │
     ├──────────────► Object Storage
     │
     └──────────────► Queue
                           │
                           ▼
                       Worker
```

Você deverá justificar cada componente.

Não escolha tecnologia simplesmente porque é popular.

---

# 12. Domínio

Modele inicialmente entidades como:

```text
User
Role
Customer
CustomerDocument
Review
AuditEntry
```

E agregados / relacionamentos necessários.

O estado do cadastro deve ser controlado pelo domínio.

Não espalhe regras de transição por controllers.

---

# 13. API

Defina contratos antes da implementação.

Exemplo conceitual:

```text
POST   /customers
GET    /customers/{id}
PUT    /customers/{id}
POST   /customers/{id}/submit
GET    /customers/{id}/history

GET    /reviews
GET    /reviews/{id}
POST   /reviews/{id}/approve
POST   /reviews/{id}/return
```

Mas o agente deverá questionar:

- autorização;
- idempotência;
- concorrência;
- versionamento;
- ownership;
- exposição de dados sensíveis.

---

# 14. Agentes de implementação

Agora entra o núcleo da AI Squad.

Inicialmente use poucos agentes.

## Orchestrator

Responsável por:

- receber trabalho;
- identificar tipo;
- montar contexto;
- chamar agentes;
- controlar estado;
- registrar execução.

## Engineering Agent

Responsável por:

- ler código;
- modificar código;
- criar testes;
- executar ferramentas;
- corrigir erros;
- preparar PR.

## Review Agent

Responsável por:

- revisar mudanças;
- verificar padrões;
- procurar vulnerabilidades;
- comparar implementação com critérios de aceite;
- verificar testes.

## Test Agent

Pode inicialmente ser parte do Engineering Agent.

Só extraia um agente separado se houver motivo.

---

# 15. Orquestração

Não comece com agentes conversando livremente.

Prefira um fluxo controlado:

```text
Story READY
     │
     ▼
Orchestrator
     │
     ▼
Context Retrieval
     │
     ▼
Planning
     │
     ▼
Implementation
     │
     ▼
Tests
     │
     ▼
Review
     │
     ├── FAIL → Agent correction
     │
     ▼
Quality Gates
     │
     ▼
PR
```

Cada etapa deve produzir artefatos verificáveis.

---

# 16. Tool Calling

Os agentes precisam de ferramentas.

Inicialmente:

```text
read_file
search_code
write_file
run_tests
run_build
run_linter
git_diff
git_status
create_branch
create_commit
create_pull_request
```

Depois:

```text
query_database
inspect_logs
inspect_metrics
deploy
rollback
```

A regra é:

**o modelo decide; a ferramenta executa.**

Não dê ao agente acesso irrestrito ao ambiente.

---

# 17. MCP

Estude e utilize MCP como mecanismo para disponibilizar ferramentas/contexto aos agentes quando fizer sentido.

Exemplo:

```text
Claude
   │
   ▼
MCP
   │
   ├── Git
   ├── Jira/Work tracking
   ├── AWS
   ├── Database
   ├── Tests
   └── Observability
```

O objetivo do exercício não é "usar MCP porque está na moda".

É entender como transformar capacidades externas em ferramentas controladas para agentes.

---

# 18. Human-in-the-loop

Crie explicitamente os pontos de aprovação humana.

### Baixo risco

```text
Agent → execute
```

### Médio risco

```text
Agent → execute → automated validation → PR
```

### Alto risco

```text
Agent → plan → HUMAN APPROVAL → execute
```

Exemplos de alto risco:

- alteração de banco de produção;
- mudança de autorização;
- alteração de contrato externo;
- alteração financeira;
- infraestrutura crítica;
- mudança de segurança.

---

# 19. Risk Engine

Implemente uma política de risco.

Exemplo:

```text
risk = LOW

if database_migration:
    risk = HIGH

if auth_change:
    risk = HIGH

if external_contract_change:
    risk = MEDIUM/HIGH

if production_infrastructure:
    risk = HIGH
```

O Orchestrator decide:

```text
LOW
 → autonomous

MEDIUM
 → automated review + human approval

HIGH
 → mandatory human approval
```

---

# 20. Git workflow

O agente nunca deve trabalhar diretamente na branch principal.

Fluxo:

```text
main
 │
 ├── agent/story-123
 │       │
 │       ├── implementation
 │       ├── tests
 │       └── validation
 │
 └──────────────► PR
```

O agente deverá:

1. criar branch;
2. implementar;
3. testar;
4. revisar;
5. gerar descrição do PR;
6. abrir PR;
7. aguardar gates.

---

# 21. CI/CD

Pipeline mínimo:

```text
Pull Request
    │
    ├── Build
    ├── Unit Tests
    ├── Integration Tests
    ├── Static Analysis
    ├── Security Scan
    ├── Coverage
    └── Agent Review
             │
             ▼
          APPROVED
             │
             ▼
          Deploy
```

O pipeline é parte do sistema de controle dos agentes.

**Nunca use o LLM como única validação de qualidade.**

---

# 22. Testes

Você deverá criar:

### Unit

Regras de domínio.

### Integration

API + banco + infraestrutura relevante.

### Contract

Contratos entre componentes.

### End-to-end

Fluxos completos:

```text
Cadastro cria
 ↓
Submit
 ↓
Backoffice recebe
 ↓
Backoffice analisa
 ↓
Aprova
 ↓
Cadastro consulta
 ↓
COMPLETED
```

E:

```text
Cadastro cria
 ↓
Submit
 ↓
Backoffice devolve
 ↓
Cadastro corrige
 ↓
Submit
 ↓
Backoffice aprova
```

---

# 23. Segurança

O agente deve ser treinado para identificar:

- broken access control;
- privilege escalation;
- IDOR;
- exposição de PII;
- secrets;
- SQL injection;
- XSS;
- CSRF quando aplicável;
- insecure logging;
- excesso de permissões;
- endpoints sem autorização.

Crie testes específicos para garantir:

```text
BACKOFFICE
   X
POST /customers
```

e:

```text
REGISTRATION
   X
POST /reviews/{id}/approve
```

---

# 24. AWS

Depois da aplicação local funcionar, leve para AWS.

Você deverá aprender a justificar:

- rede;
- IAM;
- compute;
- API;
- banco;
- storage;
- filas;
- secrets;
- observabilidade;
- CI/CD;
- DNS;
- CDN;
- WAF;
- backups;
- disaster recovery.

Não é necessário usar todos os serviços possíveis.

A pergunta deve ser:

> "Qual problema este serviço resolve?"

---

# 25. Produção

A versão final deverá possuir:

```text
Internet
   │
   ▼
CloudFront / WAF
   │
   ▼
Web
   │
   ▼
API
   │
   ├── Auth
   ├── Customer
   ├── Review
   └── Audit
         │
         ▼
       Database

Async:
API → Queue → Worker

Observability:
Logs + Metrics + Traces
```

---

# 26. Observabilidade dos agentes

Não monitore somente a aplicação.

Monitore a própria AI Squad.

Métricas:

```text
stories_received
stories_completed
stories_failed
agent_execution_time
agent_token_usage
agent_cost
tool_calls
human_interventions
rework_rate
test_failure_rate
PR_acceptance_rate
```

E especialmente:

```text
autonomous_completion_rate
```

Exemplo:

```text
100 stories
 ↓
70 concluídas sem intervenção
 ↓
20 precisaram de correção
 ↓
10 exigiram humano
```

Autonomous Completion Rate:

```text
70 / 100 = 70%
```

---

# 27. Métricas de qualidade dos agentes

Não basta medir quantidade.

Crie:

### Agent Success Rate

Percentual de tarefas concluídas corretamente.

### Rework Rate

Quantas tarefas precisaram ser refeitas.

### Human Intervention Rate

Quantas exigiram intervenção humana.

### Defect Escape Rate

Quantos defeitos chegaram a ambientes posteriores.

### Cost per Story

Custo médio da IA para entregar uma história.

### Lead Time

Tempo:

```text
READY → PRODUCTION
```

---

# 28. Agent Evaluation

Crie um conjunto fixo de histórias de teste.

Por exemplo:

```text
Evaluation Dataset

story-001 simple CRUD
story-002 validation
story-003 authorization
story-004 state transition
story-005 concurrency
story-006 integration
story-007 security
story-008 database migration
story-009 failure recovery
story-010 ambiguous requirement
```

Toda mudança no agente deverá rodar esse conjunto.

Isso permite responder:

> "Meu agente ficou melhor ou pior?"

sem depender de impressão subjetiva.

---

# 29. Golden Tasks

Crie 10–20 tarefas representativas.

Para cada uma defina:

```text
Input
Expected behavior
Expected files
Expected tests
Forbidden behavior
Security requirements
```

Exemplo:

```text
TASK:
Backoffice must not create customers.

EXPECTED:
POST /customers returns 403 for BACKOFFICE.

MUST HAVE:
authorization test.

MUST NOT:
allow role escalation.
```

Isso será seu benchmark interno.

---

# 30. Falhas que você deve procurar deliberadamente

Durante o treinamento, tente fazer o agente falhar.

### Context failure

Agente não encontrou documentação.

### Reasoning failure

Agente interpretou regra errada.

### Tool failure

Ferramenta retornou erro.

### Security failure

Agente criou autorização incorreta.

### State failure

Agente permitiu transição inválida.

### Hallucination

Agente inventou API ou requisito.

### Infinite loop

Agente continua corrigindo o mesmo problema.

### Cost explosion

Agente consome tokens excessivamente.

### Cascading failure

Um erro de um agente contamina os próximos.

---

# 31. Guardrails

Defina limites antes de liberar autonomia.

Exemplos:

```text
MAX_EXECUTION_TIME
MAX_TOOL_CALLS
MAX_RETRIES
MAX_COST
ALLOWED_REPOSITORIES
ALLOWED_BRANCHES
ALLOWED_AWS_RESOURCES
```

E:

```text
NEVER:
- push directly to main
- delete production data
- expose secrets
- bypass CI
- disable security controls
```

---

# 32. Estado da execução

O Orchestrator precisa saber onde está.

Exemplo:

```text
RECEIVED
   ↓
CONTEXT_READY
   ↓
PLANNED
   ↓
IMPLEMENTING
   ↓
TESTING
   ↓
REVIEWING
   ↓
WAITING_HUMAN
   ↓
APPROVED
   ↓
DEPLOYING
   ↓
COMPLETED
```

Em caso de falha:

```text
FAILED
```

com motivo e possibilidade de retry controlado.

---

# 33. Event-driven Agent Squad

Quando o MVP funcionar, evolua de chamadas síncronas para eventos.

Exemplo:

```text
StoryCreated
     ↓
Orchestrator
     ↓
PlanningCompleted
     ↓
ImplementationStarted
     ↓
ImplementationCompleted
     ↓
TestsCompleted
     ↓
ReviewCompleted
     ↓
ApprovalRequired
     ↓
DeploymentStarted
     ↓
DeploymentCompleted
```

Isso permitirá que a arquitetura de agentes se aproxime de uma plataforma real.

---

# 34. Chat

O chat deve existir, mas como **control plane humano**.

Imagine:

```text
Human
  │
  ▼
AI Squad Chat
  │
  ├── status
  ├── explain
  ├── approve
  ├── reject
  ├── retry
  ├── investigate
  └── intervene
```

Exemplos:

```text
"Por que a story 123 está bloqueada?"

"Mostre as alterações feitas pelo agente."

"Quais decisões arquiteturais foram tomadas?"

"Execute novamente os testes."

"Não aprove essa alteração."

"Por que você alterou esse contrato?"
```

Mas não transforme o chat no workflow principal.

---

# 35. O papel do Tech Lead humano

No modelo final:

```text
                    HUMAN TECH LEAD
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
      Architecture      Policies         Risk
          │                │                │
          └────────────────┼────────────────┘
                           ▼
                     AI ORCHESTRATOR
                           │
                           ▼
                    AI ENGINEERING
```

Você deverá gastar menos tempo:

- escrevendo código;
- revisando cada linha;
- acompanhando cada tarefa.

E mais tempo:

- definindo boundaries;
- melhorando contexto;
- criando guardrails;
- analisando métricas;
- corrigindo falhas sistêmicas;
- evoluindo a arquitetura dos agentes.

---

# 36. Plano de execução do treinamento

## Etapa 1 — Business

Entregáveis:

```text
PRD
Personas
Journey
Business Rules
State Machine
```

Objetivo:

**entender o problema.**

---

## Etapa 2 — Architecture

Entregáveis:

```text
Context Map
Architecture Diagram
ADR
API Contract
Data Model
Security Model
```

Objetivo:

**entender como o software deverá funcionar.**

---

## Etapa 3 — Agent Architecture

Entregáveis:

```text
Agent Responsibilities
Agent Tools
Context Sources
Orchestration Flow
Risk Model
Human Gates
Evaluation Strategy
```

Objetivo:

**entender como a AI Squad trabalhará.**

---

## Etapa 4 — MVP Agent

Construir:

```text
Orchestrator
Engineering Agent
Review Agent
Tool Layer
```

Objetivo:

**uma story → código → testes → PR.**

---

## Etapa 5 — Application MVP

Construir:

```text
Authentication
RBAC
Customer
Review
State Machine
Audit
```

Objetivo:

**produto funcionando.**

---

## Etapa 6 — AWS

Implementar:

```text
Infrastructure
Networking
IAM
Compute
Database
Storage
Queue
Secrets
CI/CD
Observability
```

Objetivo:

**ambiente próximo de produção.**

---

## Etapa 7 — Autonomous Loop

Implementar:

```text
Story
 ↓
Agent
 ↓
Code
 ↓
Test
 ↓
Review
 ↓
Human Gate
 ↓
Deploy
 ↓
Observe
```

Objetivo:

**primeira versão da squad autônoma.**

---

## Etapa 8 — Evaluation

Criar:

```text
Golden Tasks
Regression Suite
Agent Metrics
Cost Metrics
Quality Metrics
```

Objetivo:

**provar que o sistema é confiável.**

---

## Etapa 9 — Production Hardening

Adicionar:

```text
Security
Resilience
Rate Limits
Failure Recovery
Backups
Alerts
Audit
Cost Controls
Disaster Recovery
```

Objetivo:

**aproximar de um ambiente corporativo real.**

---

# 37. Ordem de aprendizado

Não tente estudar tudo antes de começar.

Use o próprio projeto para aprender.

### Bloco 1

**Agentic Engineering**

Aprender:

- agents;
- tools;
- context;
- orchestration;
- MCP;
- human-in-the-loop.

### Bloco 2

**Software Architecture**

Aprender:

- bounded contexts;
- APIs;
- events;
- async processing;
- state machines;
- consistency;
- resilience.

### Bloco 3

**Cloud**

Aprender:

- AWS architecture;
- IAM;
- networking;
- compute;
- database;
- queues;
- observability.

### Bloco 4

**Production Engineering**

Aprender:

- CI/CD;
- testing;
- security;
- SRE;
- DORA;
- incident management.

### Bloco 5

**AI Evaluation**

Aprender:

- evals;
- benchmarks;
- hallucination detection;
- agent traces;
- cost;
- reliability.

---

# 38. Critério final de sucesso

Ao final do treinamento, você deverá conseguir colocar uma história como:

```text
Como usuário do setor de Cadastro,
quero cadastrar um novo cliente,
para que ele possa ser analisado pelo Backoffice.
```

em um sistema onde:

```text
Story
 ↓
Product understanding
 ↓
Technical planning
 ↓
Context retrieval
 ↓
Implementation
 ↓
Tests
 ↓
Security review
 ↓
PR
 ↓
Human gate
 ↓
Deployment
 ↓
Production
 ↓
Monitoring
```

com o mínimo possível de intervenção humana.

E você deverá conseguir explicar, para cada etapa:

> **Quem decide?**

> **Qual contexto utiliza?**

> **Qual ferramenta executa?**

> **Como sabemos que a decisão estava correta?**

> **Quando o humano precisa intervir?**

> **Como recuperamos de uma falha?**

Essa será a linha central de todo o treinamento.

---

# 39. Primeiro exercício

Não comece criando agentes.

Comece criando o **PRD da aplicação de cadastro**.

Produza apenas:

```text
docs/product/vision.md
```

Contendo:

1. problema;
2. objetivo;
3. usuários;
4. contexto atual;
5. fluxo esperado;
6. resultado esperado;
7. regras conhecidas;
8. o que está explicitamente fora do escopo.

Depois entregue esse documento para o Claude e peça para ele **não escrever código**.

Peça apenas:

> "Analise este PRD como Product Agent. Identifique ambiguidades, requisitos ausentes, conflitos, riscos e perguntas que precisam ser respondidas antes da decomposição em histórias."

Esse será o nosso **primeiro teste da AI Squad**.

Não avance para arquitetura até conseguirmos observar como o agente lida com requisitos incompletos.
