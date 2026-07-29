# AIPS Domain Model

## Purpose

The AIPS Domain Model defines the main project entities and the relationships between them.

It provides a common structure for representing project knowledge consistently.

## Core Entities

The domain model contains the following core entities:

- Project
- Decision
- Work Item
- Change
- Project State
- Evidence

## Core Flow

The main flow of project development is:

Decision → Work Item → Change → Project State

Evidence provides verification throughout this flow.

## Entity Responsibilities

### Project

Defines the scope in which project knowledge exists.

### Decision

Records a choice that influences or constrains future project development.

### Work Item

Represents planned or ongoing work required to implement Decisions.

### Change

Records a completed modification that affects Project State.

### Project State

Represents verified facts describing the current project.

### Evidence

Confirms or disproves Decisions, Changes and Project State facts.

## Separation Rules

The domain model distinguishes:

- decisions from tasks;
- plans from completed work;
- changes from current state;
- recorded statements from verified facts;
- intention from implementation.

## Traceability

Where applicable, every verified Project State fact should be traceable through:

Project State ← Change ← Work Item ← Decision

Evidence may be connected to any entity requiring verification.

## Model Rule

No entity should perform the responsibility of another entity.

Each entity must retain a clear and limited purpose.
