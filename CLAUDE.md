# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

AIPS (AI-assisted Intelligent Project System) is not an application — there is no source code, build system, package manifest, linter, or test suite in this repo. It is a **knowledge-base repository**: a small set of Markdown/YAML documents that define a domain model and workflow for managing project knowledge (decisions, state, work, evidence) so that humans and AI assistants share a consistent, versioned understanding of a project instead of relying on chat history.

Because there is no code to build or test, your job in this repo is almost always to **read, extend, or reconcile documentation and decision records** according to the rules below — not to write application code.

## Repository layout

```
README.md                                  One-line project description
docs/AIPS-INDEX.md                         Checklist-style index of what's documented vs. still open
docs/VISION.md                             Purpose, core principles, goals
docs/TERMINOLOGY.md                        Canonical one-paragraph definitions of core terms
docs/CORE-CONCEPTS.md                      Short restatement of the core entities
docs/AI/AI-WORKFLOW.md                     Rules for how an AI assistant must operate on this repo
docs/architecture/DOMAIN-MODEL.md          The entity model and how entities relate (start here for architecture)
docs/architecture/DECISION.md              Spec for the Decision entity
docs/architecture/WORK-ITEM.md             Spec for the Work Item entity
docs/architecture/CHANGE.md                Spec for the Change entity
docs/architecture/PROJECT-STATE.md         Spec for the Project State entity
docs/architecture/EVIDENCE.md              Spec for the Evidence entity
docs/architecture/RELATIONSHIPS.md         How the entities connect; the traceability chain
decisions/DEC-NNNN-slug.yaml               Actual recorded Decision records (append-only log)
```

`docs/AIPS-INDEX.md` tracks which sections of the system are documented (`[x]`) vs. still open (`[ ]`) — check it to see what's settled vs. still being designed before assuming a topic is decided.

## The domain model (read this before editing anything)

The system is built around six entities and one directional flow:

```
Decision → Work Item → Change → Project State
                                     ↑
                                  Evidence (validates/challenges any of the above)
```

- **Decision** — a recorded choice that changes or constrains future development. Lifecycle: `Proposed → Accepted / Rejected / Superseded`. A Decision never modifies Project State by itself.
- **Work Item** — planned/ongoing work created to implement one or more Decisions. Does not modify Project State directly.
- **Change** — a *completed* modification that produces a new Project State. Only Changes may modify Project State; planned work never does.
- **Project State** — the collection of *verified facts* about the project right now. Never contains ideas, proposals, planned work, or assumptions. If it hasn't happened yet, it isn't Project State.
- **Evidence** — information (test results, commits, logs, approvals, screenshots, etc.) that confirms or disproves a Decision, Change, or Project State fact. A claim isn't a verified fact just because it was discussed — it needs Evidence or must be explicitly marked unverified.

Traceability rule: every verified Project State fact should trace back through `Project State ← Change ← Work Item ← Decision`. Each entity keeps a single, non-overlapping responsibility — don't let one entity's document absorb another's role (e.g., don't record planned work inside Project State, don't let a Work Item claim to change state directly).

## Operating rules for AI assistants (from docs/AI/AI-WORKFLOW.md)

**GitHub is the source of truth** (see `decisions/DEC-0001-github-as-source-of-truth.yaml`). Chat/session history is a temporary collaboration surface and is never authoritative — the repository always wins on conflict.

Before making recommendations or changes, orient by reading in this order:
1. `docs/AIPS-INDEX.md`
2. `docs/VISION.md`
3. `docs/TERMINOLOGY.md`
4. `docs/architecture/DOMAIN-MODEL.md`
5. Whichever `docs/architecture/*.md` files are relevant to the task at hand

While working:
- Treat repository documents as primary context; don't assume facts not backed by the documents.
- Keep facts distinct from proposals, and completed work distinct from planned work.
- Keep documents mutually consistent — don't let one doc drift from another (e.g., terminology used differently in two places).

When a new idea or change comes up:
1. Check whether it conflicts with the existing domain model / architecture docs.
2. If it changes the project in a meaningful way, propose it as a new Decision (new `decisions/DEC-NNNN-slug.yaml`) rather than editing architecture docs directly.
3. Don't modify architecture documents to reflect an idea until the corresponding Decision is Accepted.

When updating documentation:
- Touch the smallest number of documents necessary.
- Preserve traceability between Decision → Work Item → Change → Project State → Evidence.
- Keep terminology consistent with `docs/TERMINOLOGY.md` — don't introduce synonyms for existing core terms.
- Don't duplicate information that already lives in another document; link/reference it instead.

## Decision record conventions

Decisions live in `decisions/` as YAML files named `DEC-NNNN-kebab-case-title.yaml` (zero-padded, sequential id matching the filename prefix). Follow the structure established by `DEC-0001-github-as-source-of-truth.yaml`:

```yaml
id: DEC-000N
title: <short imperative/descriptive title>
status: proposed | accepted | rejected | superseded
date: YYYY-MM-DD
decision: |
  <what was decided, in prose>
rationale: |
  <why>
consequences:
  - <bullet list of resulting effects>
```

Use the next sequential `DEC-NNNN` number and set `status: proposed` for anything not yet ratified.

## Working conventions

- Commits in this repo are typically one doc per commit with messages like `Create X.md` / `Update X.md` — keep changes scoped and the message reflective of the single file/concept touched.
- There is no build, lint, or test tooling to run — validate changes by re-reading the affected docs for internal consistency and consistency with `docs/TERMINOLOGY.md` and `docs/architecture/DOMAIN-MODEL.md`, and by updating `docs/AIPS-INDEX.md` if a checklist item's status changed.
