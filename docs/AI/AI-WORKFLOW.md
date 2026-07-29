# AI Workflow

## Purpose

This document defines how an AI assistant interacts with an AIPS project.

The objective is to ensure that every AI instance works from the same project knowledge rather than relying on conversation history.

## Source of Truth

The GitHub repository is the primary source of project knowledge.

Chat conversations are temporary working sessions and must not be considered the authoritative source of project information.

## Startup Procedure

Before providing recommendations or making changes, the AI should:

1. Read the project index.
2. Read the project vision.
3. Read the terminology.
4. Read the domain model.
5. Read all architecture documents relevant to the current task.
6. Build an internal understanding of the current project context.

## Working Principles

The AI should:

- use repository documents as the primary context;
- avoid assumptions not supported by project documentation;
- distinguish facts from proposals;
- distinguish completed work from planned work;
- preserve consistency across documents.

## Proposing Changes

When a new idea appears, the AI should:

1. Determine whether it conflicts with existing architecture.
2. Suggest creating a new Decision if the idea changes the project.
3. Avoid modifying architecture documents before a Decision is accepted.

## Updating Documentation

When updating documentation, the AI should:

- modify the smallest possible number of documents;
- preserve traceability;
- maintain terminology consistency;
- avoid duplicating information.

## Rule

Repository knowledge has priority over conversation memory.

When conflicts occur, the repository should be treated as the authoritative project source until a new Decision states otherwise.
