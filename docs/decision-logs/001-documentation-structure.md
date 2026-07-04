# Decision: Documentation Structure for the MVP

## Goal

Define a documentation structure that is lightweight enough to maintain within a limited implementation timeframe, while still providing a clear and reviewable record of the project’s scope, design, validation approach, prompts, and key decisions.

## Decision

Use a compact documentation structure centered around four main project documents, plus two supporting folders for raw prompts and decision tracking:

```text
docs/
├─ 00-brief.md
├─ 01-scope-and-assumptions.md
├─ 02-architecture.md
├─ 03-validations.md
├─ prompts/
└─ decision-log/
```

## Reasoning

The project is being delivered under a limited timeframe, so the documentation structure needs to balance two competing goals:

1. **Keep the documentation small enough to maintain during a short MVP build**
2. **Still provide enough structure and traceability to make the project well-documented and easy to review**

A larger documentation set would create overhead and increase the risk of spending too much time maintaining documentation instead of building the MVP. At the same time, relying on only a README would not provide enough clarity around scope, assumptions, architecture, validation, or the decision-making process.

The chosen structure is intended to cover the essential needs of the project without becoming too heavy:

- **`00-brief.md`** preserves the original product brief, delivery expectations, and time constraints.
- **`01-scope-and-assumptions.md`** translates the brief into a realistic MVP scope and makes assumptions explicit.
- **`02-architecture.md`** captures the main system design, data model direction, and technical approach.
- **`03-validations.md`** documents how the MVP is validated and what evidence exists that it works as intended.

Two supporting folders are included to improve traceability without expanding the number of main documents:

- **`docs/prompts/`** stores the raw prompts used during the project.
- **`docs/decision-log/`** stores important implementation and design decisions so they can be revisited later with proper context.

This structure intentionally prioritizes **clarity, maintainability, and traceability** over documentation breadth. It is designed to support a timeboxed MVP while still producing a well-documented project.
