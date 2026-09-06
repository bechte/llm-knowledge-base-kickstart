ℹ️ *Put the following at the end of your regular AGENTS.md file:*

## LLM Knowledge Base

This project uses a hierarchical LLM Knowledge Base consisting of personal,
company-wide, and project-specific knowledge.

Before performing substantial work involving implementation, architecture,
testing, code review, technical decisions, or documentation, read and follow:

**[LLM_KNOWLEDGE_BASE.md](./LLM_KNOWLEDGE_BASE.md)**

It defines:

- the available Personal, Company, and Project Knowledge Bases,
- how knowledge from these scopes is combined,
- precedence rules for standards and project-specific decisions,
- confidentiality boundaries,
- and how reusable knowledge may be promoted between scopes.

Treat these instructions as part of this project's agent instructions.

Do not assume that existing project code overrides documented standards.
When rules conflict, apply the precedence model defined in
`LLM_KNOWLEDGE_BASE.md`.

If a task falls within the scope of `LLM_KNOWLEDGE_BASE.md`, reading that file
is mandatory before making changes.
