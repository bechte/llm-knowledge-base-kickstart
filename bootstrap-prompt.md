# Bootstrap a Personal LLM Knowledge Base

I want you to create and bootstrap a local, Git-based LLM Knowledge Base (LLM KB) that will serve as my long-term personal engineering knowledge system and can be used by Codex and other LLM-based coding agents.

The Knowledge Base should be inspired by the LLM Knowledge Base / LLM Wiki approach described by Andrej Karpathy and the workflow demonstrated by Austin in this video:

- Karpathy LLM Wiki concept:
  https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f

- Austin's LLM Knowledge Base workflow:
  https://www.youtube.com/watch?v=yfeHoOkn2TI

Use these concepts as architectural inspiration, but adapt them specifically for OpenAI Codex and a software engineering knowledge base.

Do not blindly reproduce a Claude-specific setup.

For Codex, use `AGENTS.md` as the primary agent instruction and schema file.

---

# 1. Goal

Create a durable, continuously improving personal engineering Knowledge Base.

It should serve two purposes:

1. Human-readable engineering documentation and reference.
2. Machine-readable knowledge that Codex and other coding agents can actively use while:
   - designing software,
   - implementing features,
   - reviewing code,
   - creating tests,
   - debugging,
   - making architectural decisions,
   - working with SAP Commerce Cloud,
   - working with SAP BTP,
   - and performing recurring engineering tasks.

The Knowledge Base must not become a dump of summaries.

It should evolve into a structured, cross-referenced knowledge graph consisting of concise Markdown pages, concepts, practices, checklists, patterns, decisions, and workflows.

The system should become more useful as additional sources and experience are added.

Think of it as a **compounding engineering knowledge artifact**.

---

# 2. Two Knowledge Base Levels

The overall architecture must distinguish between:

## Global / Personal LLM KB

This repository is my personal, reusable engineering Knowledge Base.

It contains knowledge that is generally applicable across projects.

Examples:

- software engineering principles,
- coding conventions,
- Clean Code,
- SOLID,
- software architecture,
- design patterns,
- Java development,
- testing strategies,
- JUnit,
- integration testing,
- End-to-End testing,
- Playwright,
- SAP Commerce Cloud,
- SAP BTP,
- Cloud Foundry,
- AI engineering,
- LLM workflows,
- Codex usage,
- engineering checklists,
- reusable troubleshooting knowledge.

It must NOT contain confidential customer or project-specific information.

---

## Project-specific LLM KB

Individual software projects may maintain their own local Knowledge Base.

Project KBs may contain:

- project architecture,
- customer-specific requirements,
- ADRs,
- integrations,
- project-specific conventions,
- project-specific testing infrastructure,
- deployment procedures,
- known issues,
- workarounds,
- operational knowledge,
- team knowledge.

A project may use the Global LLM KB as general engineering guidance.

Project-specific rules may refine or override global recommendations when appropriate.

The conceptual precedence is:

    general engineering knowledge
            ↓
      Global LLM KB
            ↓
      Project LLM KB
            ↓
     repository / code
            ↓
     current task context

More specific and current information takes precedence over generic information.

However, contradictions should be surfaced rather than silently resolved whenever the correct precedence is unclear.

---

# 3. Strict Knowledge Boundary

Project-specific information must NEVER automatically flow back into the Global LLM KB.

This is especially important for:

- customer names,
- customer architecture,
- credentials,
- URLs,
- internal systems,
- proprietary code,
- confidential requirements,
- project-specific decisions.

Instead, support the concept of:

    Project Knowledge
          ↓
    reusable insight detected
          ↓
    Promotion Candidate
          ↓
    sanitize + generalize
          ↓
    human review
          ↓
    Global LLM KB

Call this process:

    PROMOTE

Promotion must never happen automatically.

A human must explicitly approve knowledge before it becomes part of the Global KB.

---

# 4. Core Repository Model

Create a simple filesystem-based Knowledge Base.

At minimum, establish:

    /
    ├── AGENTS.md
    ├── README.md
    ├── learnings.md
    ├── log.md
    ├── raw/
    └── wiki/
        └── index.md

Do NOT create dozens of empty directories upfront.

The taxonomy should evolve organically based on actual knowledge.

Create new directories only when actual content requires them.

---

# 5. raw/ — Immutable Source Material

`raw/` contains source material.

Examples:

- articles,
- documentation,
- Markdown files,
- PDFs,
- notes,
- transcripts,
- specifications,
- exported web pages,
- technical documentation,
- conference notes,
- book notes,
- research,
- code examples.

Treat `raw/` as the provenance layer and source of truth.

Important rules:

1. Never rewrite source files to make them fit the wiki.
2. Never silently alter source material.
3. Preserve provenance.
4. Knowledge extracted from sources must remain traceable back to its source.
5. Distinguish clearly between:
   - statements directly supported by sources,
   - synthesis across multiple sources,
   - engineering recommendations,
   - assumptions,
   - project conventions,
   - unresolved questions.

Do not invent information when sources are incomplete.

---

# 6. wiki/ — Synthesized Knowledge

`wiki/` contains the organized, synthesized Knowledge Base.

The wiki must NOT simply mirror `raw/`.

A source document may influence many wiki pages.

A wiki page may synthesize knowledge from many sources.

Prefer:

    sources
      ↓
    concepts
      ↓
    relationships
      ↓
    practices
      ↓
    actionable engineering guidance

over:

    source
      ↓
    summary.md

The Knowledge Base should organize information around concepts rather than source documents.

---

# 7. Atomic Knowledge Pages

Prefer focused, atomic pages.

One page should represent one meaningful concept whenever practical.

Examples:

    SOLID
    Dependency Inversion Principle
    Testing Pyramid
    Test Doubles
    Playwright Locators
    SAP Commerce Type System
    SAP Commerce ItemsXML
    SAP Commerce Backoffice Configuration
    SAP Commerce Localization
    SAP Commerce Integration API
    BTP Cloud Foundry
    CAP
    ADRs

Avoid giant documents containing unrelated concepts.

However, do not fragment knowledge excessively.

Use judgment.

---

# 8. Cross-References and Wikilinks

Knowledge should be heavily cross-referenced.

Use Obsidian-compatible Markdown wikilinks where appropriate:

    [[SAP Commerce Type System]]
    [[ItemsXML]]
    [[Backoffice]]
    [[Localization]]
    [[JUnit]]
    [[Testing Strategy]]

Pages should reference related concepts.

The result should behave more like a knowledge graph than a directory of documents.

Avoid orphan pages.

---

# 9. Wiki Page Schema

Define a practical standard page structure in `AGENTS.md`.

Do not require every heading when it provides no value, but prefer something similar to:

    # Concept

    ## Summary

    ## Why it matters

    ## Details

    ## Engineering Guidance

    ## Checklist

    ## Examples

    ## Common Mistakes

    ## Related Concepts

    ## Sources

Important:

Keep pages concise where possible.

Prefer actionable engineering knowledge over unnecessary prose.

---

# 10. Engineering Standards vs Descriptive Knowledge

The Knowledge Base must distinguish between:

## Descriptive knowledge

"What is this?"

Example:

    SAP Commerce items.xml defines parts of the platform type system.

## Engineering guidance

"What should I normally do?"

Example:

    When adding a new attribute, review localization and Backoffice implications.

## Normative engineering standards

"What do I expect Codex to verify when working on my code?"

Example:

    A new SAP Commerce attribute should not be considered complete until
    its localization, Backoffice representation, persistence implications,
    migration implications and tests have been reviewed.

Mark these differences clearly.

Codex should be able to use normative knowledge during implementation and code review.

---

# 11. Prefer Operational Knowledge

Whenever appropriate, transform knowledge into actionable:

- checklists,
- decision trees,
- workflows,
- review criteria,
- implementation steps,
- troubleshooting procedures,
- verification steps.

For example, knowledge about SAP Commerce ItemsXML should eventually allow a checklist such as:

    When modifying ItemsXML:

    [ ] Type system impact reviewed
    [ ] Attribute definition reviewed
    [ ] Modifiers reviewed
    [ ] Persistence implications reviewed
    [ ] Indexes reviewed
    [ ] Localization added/reviewed
    [ ] Backoffice labels added/reviewed
    [ ] Backoffice configuration reviewed
    [ ] ImpEx implications reviewed
    [ ] Generated model/API implications reviewed
    [ ] System update implications reviewed
    [ ] Migration/backward compatibility reviewed
    [ ] Unit tests reviewed
    [ ] Integration tests reviewed
    [ ] Documentation updated where required

This is an EXAMPLE of the desired knowledge style.

Do NOT treat the example itself as an authoritative SAP Commerce source.

It must later be validated and refined using actual source material.

---

# 12. Initial Knowledge Domains

The initial expected domains include, but are not limited to:

## Software Engineering

- Coding Conventions
- Clean Code
- SOLID
- Software Architecture
- Design Patterns
- Refactoring
- API Design
- Error Handling
- Logging
- Security
- Performance
- Code Reviews

## Testing

- Testing Strategy
- Unit Testing
- Integration Testing
- End-to-End Testing
- Test Pyramid
- JUnit
- Mockito
- Playwright
- Test Data
- Test Isolation
- Reliable Tests
- CI Testing

## Java

- Modern Java
- Spring
- Dependency Injection
- Testing
- Concurrency
- Performance
- Build tooling

## SAP Commerce Cloud

Examples:

- Architecture
- Extension development
- Type System
- ItemsXML
- Localization
- Backoffice
- ImpEx
- FlexibleSearch
- Services
- DAOs
- Interceptors
- Events
- CronJobs
- Integration APIs
- OCC
- Security
- Testing
- Performance
- CCv2
- Deployment
- System Updates
- Integration patterns
- SAP Commerce Cloud best practices

## SAP BTP

Examples:

- BTP architecture
- Cloud Foundry
- CAP
- Integration Suite
- Connectivity
- Destinations
- Security
- Identity
- Deployment
- Observability
- Application development
- Integration patterns

## AI Engineering

Examples:

- LLMs
- Prompting
- Context Engineering
- Agents
- Codex
- Agentic workflows
- Knowledge Bases
- RAG
- MCP
- AI-assisted development
- AI-assisted code review

These are seed domains, not a fixed taxonomy.

Do NOT generate placeholder pages for all these topics.

Only create knowledge pages when actual knowledge exists.

---

# 13. Core Knowledge Operations

The Knowledge Base must define four primary operations:

    INGEST
    QUERY
    LINT
    PROMOTE

Document them clearly in `AGENTS.md`.

---

# 14. INGEST

INGEST processes new material from `raw/`.

When ingesting a source:

1. Identify the source.
2. Determine its subject and scope.
3. Inspect existing wiki knowledge before creating new pages.
4. Extract meaningful concepts.
5. Determine whether concepts:
   - already exist,
   - extend existing knowledge,
   - contradict existing knowledge,
   - require new pages.
6. Update existing pages when appropriate.
7. Create new pages only when necessary.
8. Cross-reference related concepts.
9. Add source provenance.
10. Update `wiki/index.md`.
11. Update relevant navigation/index pages.
12. Append the operation to `log.md`.

Do NOT create:

    raw/article.pdf
        →
    wiki/article-summary.md

unless a source-specific summary is genuinely useful.

Prefer integrating the knowledge into the existing conceptual graph.

---

# 15. Contradictory Sources

Never silently merge contradictory information.

When sources disagree:

1. preserve both claims,
2. identify their sources,
3. explain the contradiction,
4. determine whether differences may be caused by:
   - software version,
   - publication date,
   - context,
   - environment,
   - opinion,
   - deprecated behavior,
5. mark unresolved contradictions explicitly.

For technologies such as SAP Commerce Cloud, version context can be critical.

Preserve version information whenever relevant.

---

# 16. QUERY

QUERY means answering a question using the Knowledge Base.

When querying:

1. Start from `wiki/index.md`.
2. Navigate relevant wiki pages.
3. Follow related concepts.
4. Consult `raw/` when provenance or additional detail is necessary.
5. Clearly distinguish:
   - KB-supported facts,
   - synthesis,
   - assumptions,
   - missing knowledge.

If answering a query produces a durable, reusable insight, propose that the knowledge be added to the wiki.

Do not automatically persist speculative conclusions.

---

# 17. LINT

LINT means inspecting the Knowledge Base itself.

Check for:

- orphan pages,
- broken wikilinks,
- duplicate concepts,
- contradictory pages,
- stale information,
- missing provenance,
- overly large pages,
- overly fragmented knowledge,
- unclear terminology,
- missing cross-references,
- inconsistent naming,
- taxonomy problems,
- obsolete information,
- unprocessed raw sources,
- knowledge gaps revealed by existing pages.

Linting should improve the structure and reliability of the Knowledge Base.

---

# 18. PROMOTE

PROMOTE applies primarily when a project-specific Knowledge Base produces knowledge that may be reusable globally.

The workflow is:

    project insight
        ↓
    identify reusable principle
        ↓
    remove project/customer specifics
        ↓
    generalize
        ↓
    verify against authoritative sources when possible
        ↓
    present promotion candidate
        ↓
    HUMAN APPROVAL
        ↓
    global KB

Never automatically promote project information.

---

# 19. Automation Philosophy

Use this principle:

> Prefer hooks over loops and schedules.

When an event can trigger processing directly, prefer event-driven automation over:

- polling,
- periodic loops,
- cron jobs,
- scheduled rescanning.

The desired conceptual workflow is:

    file written to raw/
            ↓
       filesystem event
            ↓
          ingest
            ↓
      inspect existing KB
            ↓
    extract concepts
            ↓
      synthesize/update
            ↓
      cross-reference
            ↓
       update index
            ↓
        append log

However:

Do NOT assume Claude-specific hooks exist.

Inspect the current Codex/local environment and determine the simplest reliable event-driven implementation.

Keep automation separate from the actual knowledge.

The Markdown Knowledge Base must remain usable even if the automation layer changes.

The KB should remain compatible with:

- Codex,
- ChatGPT,
- other coding agents,
- normal text editors,
- Git,
- and ideally Obsidian.

---

# 20. Safe Automation

Automatic ingestion must not create uncontrolled changes.

Design ingestion to be:

- deterministic where possible,
- inspectable,
- traceable,
- Git-friendly,
- recoverable.

Do not automatically delete knowledge.

Prefer Git diffs and explicit modifications.

If fully automatic LLM invocation from a filesystem hook would be unreliable or unnecessarily complex in the current environment, implement the cleanest event detection/invocation boundary possible and document how ingestion should be triggered.

Do not invent capabilities that the current Codex environment does not provide.

---

# 21. AGENTS.md

Create a comprehensive `AGENTS.md`.

This is the operating manual and schema for agents working with this repository.

It should explain at minimum:

- purpose of the KB,
- Global vs Project KB distinction,
- repository structure,
- raw source rules,
- wiki rules,
- page conventions,
- naming conventions,
- wikilink conventions,
- provenance requirements,
- source handling,
- version handling,
- INGEST,
- QUERY,
- LINT,
- PROMOTE,
- automation philosophy,
- security/privacy boundaries,
- how to update `index.md`,
- how to update `log.md`,
- how to update `learnings.md`.

Keep `AGENTS.md` precise enough that a new Codex session can understand how to operate the KB without relying on previous chat context.

---

# 22. wiki/index.md

Create `wiki/index.md` as the primary semantic entry point into the Knowledge Base.

It should eventually provide:

- major domains,
- important concepts,
- navigation,
- recently developed areas where useful,
- high-value engineering standards,
- relevant topic indexes.

Do not turn it into a complete list of every Markdown file.

It should help both humans and agents navigate the knowledge graph.

---

# 23. log.md

`log.md` is an append-only operational history.

Track meaningful KB operations.

For example:

    2026-09-06 | BOOTSTRAP | Initialized Knowledge Base
    2026-09-07 | INGEST | Processed source XYZ
    2026-09-07 | QUERY | Investigated ItemsXML localization
    2026-09-08 | LINT | SAP Commerce knowledge
    2026-09-09 | PROMOTE | Proposed generic testing rule from project X

Keep entries concise.

Do not use `log.md` as a knowledge page.

---

# 24. learnings.md

`learnings.md` contains meta-learning about operating the Knowledge Base itself.

It should answer questions such as:

- What organizational approaches worked?
- What created unnecessary duplication?
- Which page structures work well for Codex?
- Which structures make retrieval difficult?
- Which ingestion techniques produce good results?
- What conventions should change?
- What automation failed?
- What should future agents do differently?

After substantial KB work, review whether something should be added to `learnings.md`.

Example:

    ## 2026-09-06

    ### Observation
    Large pages made cross-referencing difficult.

    ### Learning
    Prefer atomic concept pages.

    ### Future rule
    Split pages when multiple independently reusable concepts emerge.

Use learnings to improve future KB maintenance.

---

# 25. Source Quality

Not all sources have equal authority.

When synthesizing technical knowledge, prefer roughly:

1. official specifications,
2. official product documentation,
3. primary technical sources,
4. source code / authoritative repositories,
5. respected engineering publications,
6. well-supported community knowledge,
7. informal articles,
8. forum/social-media claims.

Do not automatically discard lower-authority sources.

Instead, preserve their context and confidence appropriately.

For SAP topics, official SAP documentation should generally carry more authority than an unsourced blog post.

For Java, JUnit, Playwright, frameworks, etc., prefer their official documentation when establishing normative technical facts.

---

# 26. Temporal and Version Awareness

Software knowledge becomes stale.

Where relevant, capture:

- product version,
- framework version,
- publication date,
- verification date,
- deprecated status.

Avoid presenting version-specific behavior as timeless knowledge.

This is particularly important for:

- SAP Commerce Cloud,
- SAP BTP,
- Java,
- Spring,
- Playwright,
- JUnit,
- Codex,
- LLM tooling.

---

# 27. Git

Assume this Knowledge Base should be version-controlled with Git.

If this directory is not already a Git repository, initialize it unless there is a concrete reason not to.

Create an appropriate `.gitignore`.

Use Git as the safety mechanism for:

- history,
- diffs,
- rollback,
- experimentation,
- review.

Do not make unnecessary commits unless explicitly appropriate in the current environment.

---

# 28. README.md

Create a concise human-facing `README.md`.

Explain:

- what this repository is,
- `raw/` vs `wiki/`,
- how to add sources,
- how ingestion works,
- how to query the KB with Codex,
- how to lint the KB,
- what `AGENTS.md` does,
- Global vs Project KB,
- basic privacy/security rules.

Do not duplicate the entire `AGENTS.md`.

---

# 29. No Hallucinated Bootstrap Knowledge

This requirement is critical.

At bootstrap time, DO NOT populate the wiki with supposed knowledge about:

- Clean Code,
- SOLID,
- SAP Commerce,
- SAP BTP,
- Playwright,
- JUnit,
- or any other domain

unless source material is already present in `raw/`.

The initial goal is to build the Knowledge Base SYSTEM, not pretend that the Knowledge Base already contains validated knowledge.

The domain lists above describe intended future scope.

They are not source material.

---

# 30. Bootstrap Sources

The architectural inspiration itself may be documented as bootstrap provenance:

- Andrej Karpathy:
  https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f

- Austin's videos:
  https://www.youtube.com/watch?v=yfeHoOkn2TI
  https://www.youtube.com/watch?v=yfeHoOkn2TI

If you have web access, inspect these sources before finalizing the architecture.

Do not assume claims from this prompt are exact quotations from either source.

Treat this prompt as my desired architecture and the external sources as conceptual inspiration.

---

# 31. First Execution

Now bootstrap the Knowledge Base.

Proceed in this order:

1. Inspect the current directory.
2. Determine whether any relevant files or existing repository structure already exist.
3. Do not overwrite meaningful existing content.
4. Inspect the two architectural sources above if accessible.
5. Create the minimal repository structure.
6. Create `AGENTS.md`.
7. Create `README.md`.
8. Create `wiki/index.md`.
9. Create `log.md`.
10. Create `learnings.md`.
11. Create an appropriate `.gitignore`.
12. Initialize Git if appropriate.
13. Design the INGEST / QUERY / LINT / PROMOTE workflows.
14. Investigate how event-driven ingestion can best be implemented in the current Codex environment.
15. Prefer hooks/events over loops or schedules.
16. Do not introduce unnecessary infrastructure.
17. Do not populate domain knowledge without sources.
18. Validate the resulting repository for internal consistency.
19. Report what you created and any decisions you made.

---

# 32. Before Implementing Complex Automation

Do not overengineer the filesystem hook.

First determine:

- what Codex can reliably execute in this environment,
- whether a native hook/event mechanism exists,
- whether a small watcher is required,
- whether external dependencies would be introduced,
- whether automatic LLM invocation is actually possible and safe.

Prefer the smallest reliable implementation.

If there are multiple viable approaches with significant architectural trade-offs, explain the trade-offs before introducing substantial infrastructure.

The Knowledge Base itself is more important than the automation around it.

---

# 33. Design Principles

Use these principles throughout the implementation:

**Sources are immutable.**

**The wiki is synthesized knowledge, not a collection of summaries.**

**Prefer concepts over documents.**

**Prefer updating existing knowledge over creating duplicates.**

**Prefer atomic pages over giant documents.**

**Prefer cross-references over isolated pages.**

**Prefer actionable engineering guidance over verbose prose.**

**Prefer checklists for recurring engineering work.**

**Prefer authoritative sources.**

**Preserve provenance.**

**Preserve version context.**

**Surface contradictions.**

**Never silently invent missing knowledge.**

**Prefer hooks over loops and schedules.**

**Keep project knowledge isolated from the personal Global KB.**

**Promotion from Project KB to Global KB always requires human approval.**

**Keep the system simple, Markdown-based, Git-friendly and agent-agnostic.**

**Let the taxonomy emerge from actual knowledge.**

**Continuously improve the Knowledge Base based on `learnings.md`.**

---

# 34. Expected Result

After this bootstrap session I expect to have a clean foundation approximately like:
```
    .
    ├── AGENTS.md
    ├── README.md
    ├── .gitignore
    ├── learnings.md
    ├── log.md
    ├── raw/
    └── wiki/
        └── index.md
```

plus only those scripts/configuration files that are genuinely useful for the chosen ingestion workflow.

Do not create empty domain trees merely to make the repository look complete.

The Knowledge Base should now be ready for me to place the first real source into `raw/`.

At the end, show me:

1. the resulting repository tree,
2. the most important conventions established in `AGENTS.md`,
3. how I add my first source,
4. how I manually trigger INGEST,
5. whether automatic event-driven ingestion was implemented,
6. how I run QUERY,
7. how I run LINT,
8. how PROMOTE should work with future Project KBs,
9. any unresolved architectural decisions.

Then stop.

Do not fabricate the first knowledge articles.

We will ingest the first real sources in the next step.
