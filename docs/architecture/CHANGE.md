# Change

## Definition

A Change is a recorded modification that transforms the Project State.

A Change represents completed work, not planned work.

## Purpose

A Change records what has actually changed in the project.

## Properties

A Change:

- has a timestamp;
- has an author;
- may reference one or more Work Items;
- may implement one or more Decisions;
- produces a new Project State.

## Relationships

A Change may:

- implement Decisions;
- be produced by Work Items;
- modify Project State;
- reference Evidence.

## Rule

Only a completed Change may modify the Project State.

Planned work never changes the Project State.
