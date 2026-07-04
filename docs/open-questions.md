# Open Questions

This document tracks the main design and implementation questions that remain open for the MVP.

These questions are not blockers for documenting the current MVP direction, but they still need to be resolved before or during implementation in order to complete the system coherently.

## 1. Channel-specific alert configuration

The alert model supports multiple notification channels, but each channel may require different configuration data.

Open questions:

- What exact configuration should an **email** alert require?
- What exact configuration should a **Slack** alert require?
- How should channel-specific settings be stored in the alert model?
- What level of validation should be applied to each channel-specific field?

This decision affects the alert schema, alert creation/editing UI, and notification sender implementations.

## 2. Final alert data model

The alert subscription model has been defined conceptually as:

- one alert per channel per user
- one or more selected categories per alert
- channel-specific delivery settings per alert

The exact stored shape of the alert record still needs to be finalized.

Open questions:

- What are the final required fields on the `Alert` model?
- How should selected categories be stored?
- Should one-alert-per-channel be enforced at the database level, the application level, or both?

## 3. Event persistence strategy

The event-ingestion flow requires deduplication based on provider article UUIDs, but the MVP has not yet finalized how much event data should be stored.

Open questions:

- Should the system store only processed provider UUIDs for deduplication?
- Or should it also persist normalized alert events for traceability and future UI/admin use?

This decision affects the data model, event-processing flow, and future visibility into processed events.

## 4. Polling execution model

The MVP uses a polling-based ingestion strategy, but the exact execution model is still open.

Open questions:

- How should the 10-minute polling cycle be triggered?
- Should polling run as a cron job, background worker, scheduled task, or another mechanism?

This decision affects the implementation structure and deployment model of the MVP.

## 5. Supported category set

The MVP now includes category-based subscriptions, but the exact category list has not yet been finalized.

Open questions:

- Which categories should be exposed in the MVP?
- Should the system expose raw provider topics directly, or define a curated supported category list?
- If a curated list is used, how should provider topics map to internal categories?

## 6. Scope of the alert management view

The MVP includes a user-facing alert management view, but the exact contents of that view can still be clarified.

Open questions:

- Should the view only show the user’s alerts?
- Should it also show recent processed events or notification history if such data is stored?
- How much operational visibility is needed in the MVP UI versus only in logs or internal tooling?
