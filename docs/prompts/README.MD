# Prompt Archive

This folder contains the raw prompts used during the planning, documentation, and implementation of the project.

## Purpose

The goal of this folder is to preserve the prompts used throughout the project in a way that makes the work process traceable and easy to review.

## Organization

Prompt files in this folder are organized by **project workstream** rather than by individual prompt or by a strict one-to-one mapping with the main documentation files.

This approach is used because prompts are expected to support both:

- documentation work, such as the brief, scope, architecture, and validation documents
- implementation work, such as backend design, notification handling, admin functionality, and testing

Each prompt file should group together the raw prompts that belong to a specific area of work.

## Prompt format

Prompts inside each file should be stored in chronological order and numbered sequentially starting from `001`.

Example:

```md id="jlwmyn"
# Prompt 001

I need a well-designed plan to achieve this project in around four hours.

# Prompt 002

Help me define a documentation structure that is robust but small.
```

Prompt numbering is local to each file.

## Rules

- Store raw prompts only.
- Keep the prompt text unchanged after it has been used.
- Group prompts by the work area they contributed to.
- If a prompt could belong to multiple areas, store it in the file that best represents its primary purpose.

## Notes

This folder is intended to document the prompt history of the project as a whole, including both documentation work and application implementation work.
