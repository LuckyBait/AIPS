# Relationships

## Purpose

This document defines the core relationships between the main AIPS concepts.

Relationships provide traceability and explain how project knowledge is connected.

## Core Flow

The main project flow is:

Decision → Work Item → Change → Project State

Evidence may validate or challenge any relevant part of this flow.

## Decision Relationships

A Decision may:

- create or justify Work Items;
- define a target state;
- constrain future work;
- be implemented by one or more Changes;
- be supported or challenged by Evidence.

A Decision does not modify Project State directly.

## Work Item Relationships

A Work Item may:

- implement one or more Decisions;
- produce one or more Changes;
- reference Evidence;
- depend on other Work Items.

A Work Item affects Project State only through completed Changes.

## Change Relationships

A Change may:

- be produced by a Work Item;
- implement one or more Decisions;
- modify one or more Project State items;
- reference Evidence confirming its completion.

## Project State Relationships

A Project State item may:

- be created, modified or closed by a Change;
- be affected by a Decision;
- be validated or contradicted by Evidence;
- change over time.

## Evidence Relationships

Evidence may:

- validate or invalidate a Project State item;
- support or challenge a Decision;
- confirm that a Change was completed;
- be referenced by a Work Item.

## Traceability Rule

Every verified Project State change should be traceable through the following chain where applicable:

Project State ← Change ← Work Item ← Decision

Evidence may be attached to any element that requires verification.

## Direction Rule

Relationships must clearly distinguish:

- intention from implementation;
- planned work from completed work;
- recorded information from verified fact.
