# Subagents Claude Code

Subagents de projeto ficam em `.claude/agents/`. Cada arquivo Markdown dessa pasta define um agente independente, com seu próprio contexto e instruções.

## Estrutura

```text
.claude/
├── README.md
└── agents/
    ├── product-agent.md
    ├── tech-lead-agent.md
    ├── implementation-agent.md
    ├── test-agent.md
    └── review-agent.md
```

Crie somente os agentes necessários para a etapa atual. Mantenha cada agente focado em uma responsabilidade e explicite limites de atuação, entradas e formato de saída.

## Template de agente

Copie o bloco abaixo para `.claude/agents/<nome-do-agente>.md` e substitua os campos de exemplo:

```markdown
---
name: nome-do-agente
description: >-
  Acione para [situação específica]. Responsável por [resultado esperado].
tools: Read, Grep, Glob
model: sonnet
---

# Papel

Você é responsável por [responsabilidade única do agente].

## Objetivo

[Resultado que deve produzir.]

## Entradas

- [Artefatos, requisitos ou contexto necessários.]

## Processo

1. [Analise as entradas e identifique lacunas.]
2. [Execute a tarefa dentro do escopo.]
3. [Verifique o resultado e registre riscos ou dúvidas.]

## Limites

- Não [ação fora do escopo ou decisão reservada a outro papel].
- Se faltar informação essencial, declare a lacuna em vez de inventar requisitos.
- Não considere a tarefa concluída sem [critério verificável].

## Saída

Entregue [artefato] com:
- [item obrigatório];
- [item obrigatório];
- riscos, dúvidas e dependências, quando houver.
```

`name` e `description` são os campos essenciais do frontmatter. A descrição deve informar quando o agente deve ser acionado; o Claude Code usa esse texto para decidir quando delegar. Ajuste `tools` ao mínimo necessário e escolha `model` conforme a tarefa.

## Papéis iniciais para este treinamento

- `prd-agent`: conduz o stakeholder na construção do PRD. Dúvidas, premissas e orientações ficam em `docs/product/pre-PRD.md`; só o conteúdo confirmado vai para `docs/product/PRD.md`.
- `product-agent`: transforma o arquivo de PRD em épicos, histórias e critérios de aceitação, apontando ambiguidades. Não aceita PRD pelo chat.
- `tech-lead-agent`: propõe arquitetura, contratos e plano incremental a partir dos requisitos aprovados.
- `implementation-agent`: implementa uma tarefa delimitada conforme o plano e os padrões do repositório.
- `test-agent`: define e executa verificações para os critérios de aceitação, relatando falhas reproduzíveis.
- `review-agent`: revisa mudanças em busca de bugs, riscos de segurança e lacunas de teste; não altera o código por padrão.

Comece com um ou dois agentes. Adicione os demais quando houver uma fronteira de responsabilidade clara e uma saída verificável para cada um.