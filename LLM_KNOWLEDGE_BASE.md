# Usage of LLM Knowledge Bases

## Purpose

This repository uses a hierarchical LLM Knowledge Base (LLM KB) model.

Before performing substantial implementation, architecture, testing, review, or
documentation work, use the available Knowledge Bases as additional engineering
context.

Knowledge is distributed across multiple scopes with different ownership,
authority, confidentiality, and lifecycle.

Do not treat the Knowledge Bases as isolated repositories. Together they form
the available knowledge context for this project.

---

# Knowledge Base Scopes

Three Knowledge Base scopes are available.

## 1. Personal / Global Knowledge Base

Location:

    ~/llm-knowledge/

Contains general and reusable engineering knowledge such as:

- software engineering
- architecture
- coding practices
- testing
- programming languages
- AI engineering
- consulting
- project management

This represents personal knowledge, experience, preferences, and reusable
engineering guidance.

It MUST NOT contain project- or customer-confidential information.

---

## 2. Company Knowledge Base

Location:

    ~/llm-knowledge-company/

Contains company-wide knowledge and standards, including:

- engineering standards
- coding conventions
- architecture principles
- security requirements
- testing standards
- delivery practices
- reusable implementation patterns
- company-specific SAP practices
- templates and checklists

Company standards have higher normative authority than personal preferences or
personal standards.

---

## 3. Project Knowledge Base

Location:

    ./llm-knowledge-project/

Contains knowledge that applies specifically to this project and customer.

Examples:

- project architecture
- architectural decisions
- ADRs
- customer requirements
- project conventions
- integration specifications
- system landscape
- testing conventions
- deployment procedures
- known issues
- workarounds
- project-specific implementation patterns
- customer-specific information

This is the most specific Knowledge Base for this repository.

Project knowledge may contain confidential information and MUST NOT be copied
into less restricted Knowledge Bases automatically.

---

# Knowledge Model

Do not interpret the hierarchy as simple inheritance.

There are two different mechanisms:

1. Knowledge Aggregation
2. Rule Resolution

They must be handled differently.

---

# Knowledge Aggregation

Descriptive and complementary knowledge from all accessible Knowledge Bases may
be combined.

Conceptually:

    Personal KB
        +
    Company KB
        +
    Project KB
        =
    Available Knowledge Context

Example:

The Personal KB may contain detailed knowledge about Playwright.

The Company KB may specify that Playwright is the preferred E2E testing
technology.

The Project KB may document the project's Playwright fixtures and test setup.

These pieces of knowledge complement each other and should all be considered.

Do NOT ignore useful general knowledge merely because a more specific Knowledge
Base exists.

---

# Rule Resolution

Normative rules, standards, conventions, and explicit decisions follow a
specificity hierarchy.

When rules conflict, use:

    Current explicit task instruction
        >
    Explicit project decision / ADR
        >
    Project-specific rule or convention
        >
    Company rule or standard
        >
    Personal standard or preference
        >
    General engineering knowledge

More specific rules override more general rules only within their applicable
scope.

An override does not invalidate the general rule outside that scope.

---

# Explicit Overrides

A project-specific deviation from a company standard SHOULD be explicit.

Prefer documentation such as:

    Company Standard:
    Constructor injection is required.

    Project Override:
    Legacy extension X continues to use setter injection.

    Reason:
    Changing the injection mechanism would require modification of generated
    legacy configuration outside the scope of the current migration.

Do not infer an override merely because existing project code violates a
company or personal standard.

Existing code is evidence of current implementation, not automatically an
architectural decision.

When project code conflicts with a higher-level standard and no documented
project decision exists:

1. identify the conflict,
2. check the Project KB for an explicit decision,
3. check relevant ADRs,
4. do not silently assume the existing implementation is authoritative,
5. surface the discrepancy when it affects the task.

---

# Authority vs. Source Quality

Specificity and factual correctness are different dimensions.

A project rule may override a company standard for this project.

However, a project document does not automatically override factual technical
knowledge.

Example:

If a project note contradicts official SAP behavior, do not assume that the
project note changes how SAP Commerce actually works.

Distinguish between:

- facts,
- recommendations,
- standards,
- preferences,
- project decisions,
- customer requirements.

Resolve conflicts according to their type.

---

# Knowledge Base Usage

For substantial engineering tasks, determine which Knowledge Base topics are
relevant before implementing the solution.

Do NOT load or read the entire Knowledge Base indiscriminately.

Use targeted retrieval.

A typical workflow is:

    Understand task
        ↓
    Inspect repository context
        ↓
    Identify relevant knowledge domains
        ↓
    Query Project KB
        ↓
    Query Company KB
        ↓
    Query Personal KB where useful
        ↓
    Resolve applicable rules
        ↓
    Perform task
        ↓
    Validate against applicable standards

Prioritize the Project KB when searching for project-specific context.

Use Company and Personal KBs to complement it with broader engineering
knowledge.

---

# Project Repository Is Authoritative for Current State

The Knowledge Bases provide context, standards, decisions, and accumulated
knowledge.

The repository itself remains authoritative for the actual current
implementation.

Always inspect relevant source code, configuration, tests, and documentation
before modifying the project.

Do not assume that a Knowledge Base accurately describes the current
implementation when the repository can verify it directly.

If implementation and documentation differ, identify the discrepancy.

---

# Applying Knowledge During Development

Use applicable Knowledge Base guidance actively.

Do not treat the KB merely as documentation to quote.

For example, when implementing a SAP Commerce type-system change, relevant
knowledge may result in checking:

- ItemsXML
- localization
- Backoffice configuration
- ImpEx implications
- persistence
- indexes
- system update implications
- migration compatibility
- tests

The actual checklist must come from the available Knowledge Bases and project
context.

Do not invent standards that are not documented.

---

# Knowledge Gaps

If information required for a task is missing from all Knowledge Bases:

1. inspect the repository,
2. consult authoritative sources when available and permitted,
3. distinguish new findings from established KB knowledge,
4. do not pretend the missing information existed in the KB.

Durable findings may become candidates for Knowledge Base updates.

---

# Updating the Project Knowledge Base

When work produces durable project-specific knowledge, consider updating:

    ./llm-knowledge-project/

Examples:

- architectural decisions
- newly discovered constraints
- integration behavior
- important troubleshooting knowledge
- project conventions
- implementation procedures
- recurring project-specific checklists

Follow the instructions defined by the Project KB itself when modifying it.

Do not store temporary task state or trivial implementation details as durable
knowledge.

---

# Knowledge Promotion

Knowledge must NEVER automatically flow from the Project KB into the Company or
Personal KB.

Project knowledge can contain customer-confidential or context-specific
information.

If project work reveals a generally reusable insight, treat it as a:

    PROMOTION CANDIDATE

The process is:

    Project insight
        ↓
    Determine whether it is reusable
        ↓
    Remove customer/project-specific information
        ↓
    Generalize the knowledge
        ↓
    Validate against authoritative sources where appropriate
        ↓
    Human review
        ↓
    Explicit promotion

Possible targets are:

    Project → Company KB

or, where appropriate:

    Project → Personal KB

Promotion requires explicit human approval.

Never copy customer names, internal URLs, credentials, architecture details,
source code, business information, or other confidential information into a
less restricted Knowledge Base.

---

# Personal to Company Promotion

Knowledge from:

    ~/llm-knowledge/

may also be useful as a company standard or shared practice.

Treat this in the same way:

    Personal insight
        ↓
    Promotion candidate
        ↓
    Company review
        ↓
    Explicit adoption
        ↓
    Company KB

A personal preference does not become a company standard merely because it
exists in the Personal KB.

---

# Confidentiality Boundary

Treat:

    ./llm-knowledge-project/

and this repository as potentially customer-confidential.

Never automatically propagate their contents to:

    ~/llm-knowledge/

or:

    ~/llm-knowledge-company/

Information may only cross this boundary through an explicit, reviewed
promotion process.

When generalizing project knowledge, remove identifying and confidential
information before proposing promotion.

When uncertain whether information is confidential, keep it inside the project
scope.

---

# Knowledge Ownership

The Knowledge Bases have different owners and lifecycles.

## Personal KB

    ~/llm-knowledge/

Owner:
Individual developer.

Purpose:
Long-term personal and professional knowledge.

---

## Company KB

    ~/llm-knowledge-company/

Owner:
Company / engineering organization / responsible communities.

Purpose:
Shared organizational knowledge and standards.

Do not modify company standards merely to make them fit the current project.

Project deviations belong in the Project KB.

---

## Project KB

    ./llm-knowledge-project/

Owner:
Project team.

Purpose:
Knowledge and decisions specific to this project and customer.

---

# General Principles

Follow these principles when working in this repository:

1. Aggregate knowledge across accessible scopes.

2. Resolve normative rules from most specific to most general.

3. Distinguish facts from rules, standards, preferences, and decisions.

4. Do not mistake existing code for an intentional project decision.

5. Prefer explicit project overrides over implicit deviations.

6. Use the repository as the source of truth for current implementation.

7. Use Knowledge Bases as accumulated context and engineering guidance.

8. Retrieve relevant knowledge instead of loading entire Knowledge Bases.

9. Preserve confidentiality boundaries.

10. Never automatically promote project knowledge.

11. Generalize and sanitize reusable project insights before promotion.

12. Require human approval for cross-scope promotion.

13. Surface contradictions instead of silently choosing when authority is
    unclear.

14. Do not invent Knowledge Base rules or facts.

15. Keep knowledge close to the scope that owns it.

---

# Effective Context Model

For work in this repository, think in terms of:

    ┌───────────────────────────────────┐
    │ Personal Knowledge               │
    │ ~/llm-knowledge/                  │
    └─────────────────┬─────────────────┘
                      │
                      ▼
    ┌───────────────────────────────────┐
    │ Company Knowledge                │
    │ ~/llm-knowledge-company/          │
    └─────────────────┬─────────────────┘
                      │
                      ▼
    ┌───────────────────────────────────┐
    │ Project / Customer Knowledge     │
    │ ./llm-knowledge-project/          │
    └─────────────────┬─────────────────┘
                      │
                      ▼
    ┌───────────────────────────────────┐
    │ Repository / Current State       │
    └─────────────────┬─────────────────┘
                      │
                      ▼
    ┌───────────────────────────────────┐
    │ Current Task                     │
    └───────────────────────────────────┘

This diagram represents increasing contextual specificity.

For KNOWLEDGE:

    aggregate relevant information from all scopes.

For RULES:

    Current Task
        >
    Project
        >
    Company
        >
    Personal
        >
    General

For CONFIDENTIALITY:

    information stays within its owning scope unless explicitly reviewed and
    promoted.
