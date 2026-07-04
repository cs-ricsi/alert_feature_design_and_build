# Alerts MVP

## Overview

Alerts MVP is a timeboxed prototype of a world-event alerting system.

The MVP allows users to create alerts for selected event categories and receive notifications through supported channels when matching events are processed by the system. The initial notification channels are **email** and **Slack**.

The system is being designed with a limited implementation timeframe in mind, so the focus is on delivering a coherent end-to-end alerting flow rather than a production-ready platform.

This repository contains the MVP implementation, project documentation, decision logs, and prompt artifacts produced during the design and development process.

---

## Project Brief

The project is based on the following brief:

> We want users to be able to set up alerts so they get notified when something important happens in the world — like breaking news, market movements, natural disasters, that kind of thing. Should work for both email and Slack. Make it flexible enough that we can add more channels later. We need an admin view too.

---

## Current Goal

The goal of this project is to design and implement a timeboxed MVP that demonstrates the core alerting workflow end-to-end while documenting the assumptions, decisions, and working process clearly.

At a high level, the MVP is intended to cover:

- alert creation and management
- category-based alert subscriptions
- multi-channel notification delivery through email and Slack
- event ingestion, matching, and notification dispatch
- a user-facing alert management view
- an architecture that can be extended with additional notification channels later

---

## Repository Structure

- `docs/` — project documentation, decision logs, and open questions
- `src/` — application source code
- `prompt-artifacts/` — raw prompts and prompt history collected during development

---

## Documentation

Project documentation is maintained in the `docs/` directory. This includes:

- the original brief
- scope and assumptions
- architecture notes
- decision logs
- open questions

Prompt history and raw prompts are stored separately in `prompt-artifacts/`.

Because the project is being developed from a short and ambiguous brief, the documentation is expected to evolve alongside the implementation.

---

## Status

This project is currently in the MVP planning and implementation phase.

The scope, architecture, and implementation details are being defined incrementally based on the brief, documented assumptions, and decisions made during the build process.
