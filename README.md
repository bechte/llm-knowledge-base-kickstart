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

1. **Add a source**: copy it into `raw/`. Preserve its original bytes and record origin, dates, version, and capture limitations in an adjacent `.source.md` file. ⚠️
2. **INGEST**: open this repository in Codex and ask:
    ```Read AGENTS.md. INGEST raw/my-first-source.md.
    Show changes and run scoped LINT. Do not commit.
    Optionally generate a fingerprinted request:

    python3 scripts/prepare_ingest.py raw/my-first-source.md```
3. **QUERY**:
    ```Read AGENTS.md. QUERY: <question>.
    Cite KB evidence, identify gaps, and do not modify files.```
4. **LINT**:
    ```Read AGENTS.md. LINT the KB and report findings without modifying files.```
5. **PROMOTE**: prepare and sanitize the candidate inside its Project KB, verify it, obtain explicit human approval of the exact content, then transfer and ingest the approved artifact.

Codex will analyze the source, extract relevant concepts and integrate them into the existing `wiki/` instead of simply creating another document summary.

From there, your Knowledge Base can grow incrementally with every new source and every new piece of knowledge.

## Next Step

The complete setup instructions, conventions and design principles are defined in:

👉 **[`bootstrap-prompt.md`](./bootstrap-prompt.md)**

Use this file to bootstrap a new personal or project-specific LLM Knowledge Base.
