# LLM Knowledge Base Kickstart

This repository provides a simple starting point for creating your own **LLM Knowledge Base (LLM KB)** with AI coding agents such as OpenAI Codex.

An LLM Knowledge Base turns source material such as documentation, articles, notes or project knowledge into a persistent, structured and cross-referenced knowledge base that can be reused across LLM sessions.

The basic idea is:

```
Raw Sources → LLM Processing → Structured Wiki → Continuously Improving Knowledge
```

The approach is based on [Andrej Karpathy's LLM Wiki concept](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

The Knowledge Base can be used either as a **personal/global KB** for reusable knowledge or as a **project-specific KB** for architecture, conventions, decisions and shared team knowledge.

## Getting Started

### 1. Create a repository for your Knowledge Base

Create an empty Git repository and open it with an AI coding agent such as **OpenAI Codex**.

For example:

```
mkdir my-llm-knowledge-base
cd my-llm-knowledge-base
git init
```

### 2. Run the Bootstrap Prompt

Copy the content of [`bootstrap-prompt.md`](./bootstrap-prompt.md) into your Codex session.

The prompt instructs Codex to bootstrap the initial structure, conventions and workflows of your Knowledge Base.

The resulting structure will look roughly like:

```
.
├── AGENTS.md
├── README.md
├── learnings.md
├── log.md
├── raw/
└── wiki/
    └── index.md
```

### 3. Add your first source

Put your first document into:

```
raw/
```

Then ask Codex to **INGEST** it.

Codex will analyze the source, extract relevant concepts and integrate them into the existing `wiki/` instead of simply creating another document summary.

From there, your Knowledge Base can grow incrementally with every new source and every new piece of knowledge.

## Next Step

The complete setup instructions, conventions and design principles are defined in:

👉 **[`bootstrap-prompt.md`](./bootstrap-prompt.md)**

Use this file to bootstrap a new personal or project-specific LLM Knowledge Base.
