# Decision Log

This folder contains records of important project decisions made during the design and implementation of the MVP.

## Purpose

The goal of the decision log is to document decisions that materially affect the project’s scope, architecture, implementation approach, or tradeoffs. This makes it easier to revisit earlier choices, understand why they were made, and update them later with proper context.

## When to add a decision

Create a decision entry when a choice has a meaningful impact on:

- MVP scope
- architecture or data modeling
- notification delivery design
- admin capabilities
- implementation tradeoffs caused by the timebox
- validation or testing strategy

## Relationship to the main docs

The main documents in `docs/` describe the current state of the project.
The decision log captures the reasoning behind important decisions made along the way.

## Naming convention

Decision files should use a numeric prefix to keep them ordered chronologically:

- `001-...`
- `002-...`
- `003-...`

Use short descriptive file names, for example:

- `001-mvp-scope.md`
- `002-alert-rule-model.md`
- `003-notification-channel-abstraction.md`
