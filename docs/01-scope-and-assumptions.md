# Scope and Assumptions

## Objective

The goal of this project is to deliver a timeboxed MVP of a world alerts system based on the brief in `docs/00-brief.md`.

The MVP should demonstrate the core alerting flow end-to-end: a user can create and manage alerts, the system can process incoming alert-triggering events, matching alerts can trigger notifications, and users can manage their existing alerts through a dedicated management view.

The system should support **email and Slack as the initial notification channels**, while being designed in a way that makes it straightforward to add additional channels later.

The goal is not to build a production-ready platform, but to deliver a coherent and extensible MVP within the available timeframe.

## MVP Scope

The MVP includes the minimum functionality needed to demonstrate the core alerting workflow described in the brief.

### 1. Alert management

The system should allow a user to create and manage alerts for important world-event notifications.

For the MVP, an alert represents a **channel-specific subscription with category selection** rather than a fully user-defined event rule. Each alert is tied to exactly one notification channel and includes one or more selected categories used for event matching.

This includes:

- creating an alert for a supported notification channel
- selecting one or more supported alert categories for that alert
- editing the category selections of an existing alert
- viewing existing alerts
- modifying an existing alert
- deleting an existing alert

Because the MVP initially supports only **email** and **Slack**, a user can have up to **two alerts** in total, with at most one alert per supported channel.

### 2. Event processing

The system should support receiving events that are intended to trigger alerts and processing them through the alerting flow.

For the MVP, the responsibility of the system is to receive alert-triggering events from an external source, process them through the alerting flow, and notify the alerts whose selected categories match the event metadata. Determining which real-world events should enter the system is treated as a separate concern from the alert delivery flow itself.

This includes:

- creating, ingesting, or otherwise receiving events that should trigger alerts
- processing those events through the alerting flow
- matching event metadata to alert category selections
- notifying the alerts that match a given event

### 3. Notification delivery

The system should support the notification channels explicitly mentioned in the brief.

For the MVP, this includes:

- email notifications
- Slack notifications
- one alert per supported channel per user
- a channel design that can be extended to additional notification channels later

### 4. Alert management view

The brief states that the system should include an admin view, but it does not define the intended responsibilities of that view in detail.

For the MVP, this requirement is interpreted as a **user-facing alert management view** rather than a dedicated administrator dashboard for internal admin users. This interpretation is based on the assumption that users need a way to review and manage their existing alerts as part of the core alerting workflow, while a separate administrator-facing interface would introduce additional scope and complexity that is not clearly required by the brief.

The alert management view is the surface through which users can review, create, modify, and delete their alerts.

A dedicated administrator-facing view for internal or privileged users is considered a possible future extension, but it is not treated as part of the MVP scope unless later implementation work makes it necessary.

## Out of Scope

The following items are intentionally out of scope for this MVP.

### 1. Fully user-defined alert rules and advanced filtering

The MVP supports selecting from a predefined set of alert categories, but users do not define custom alert rules, arbitrary filters, thresholds, keyword-based matching, or complex event conditions.

### 2. Dedicated administrator-facing dashboard

The MVP does not include a separate internal dashboard for administrator or privileged users. The brief’s “admin view” requirement is interpreted in the MVP as a user-facing alert management view.

### 3. Event importance classification inside the alerting system

The MVP does not independently determine which real-world events are important enough to trigger alerts. It assumes that alert-triggering events are supplied to the system by an external source, manual input, or a simplified ingestion mechanism.

### 4. Production-grade event ingestion and source integrations

The MVP does not require a production-ready pipeline for ingesting breaking news, market events, natural disasters, or other world events from real external providers. The mechanism for obtaining alert-triggering events is intentionally kept flexible and may be simplified for demonstration purposes.

### 5. Advanced notification delivery infrastructure

The MVP does not include retry queues, batching, throttling, delivery analytics, or other production-grade notification infrastructure beyond what is needed to demonstrate the core alert flow.

### 6. Channel-specific validation and delivery verification

The MVP does not include advanced validation of channel-specific configuration data, such as verifying that a provided email address is valid or that a Slack user identifier or destination is correct and reachable.

The MVP also does not include delivery verification or notification delivery checks beyond attempting to send through the configured channel integration.

### 7. Full production hardening

The MVP does not aim to cover production concerns such as comprehensive authorization models, large-scale observability, high-volume performance optimization, or deployment-grade operational safeguards.

## Assumptions

The MVP is based on the following working assumptions derived from the brief and the limited implementation timeframe.

### 1. Alert-triggering events are provided to the system from outside the core alert flow

The MVP assumes that events intended to trigger alerts are supplied to the system by an external source, manual input, seeded data, or another simplified ingestion mechanism. Determining which real-world events should become alert-triggering events is treated as a separate concern from the alert delivery workflow itself.

### 2. Each alert is tied to a single notification channel and one or more selected categories

For the MVP, an alert is assumed to represent a channel-specific subscription to alert-triggering events with one or more selected categories. A user may therefore create separate alerts for different supported channels rather than configuring multiple channels within a single alert.

This also implies that alerts may require channel-specific configuration data depending on the selected channel. For example, an email alert may require an email address, while a Slack alert may require a Slack-specific identifier or destination value.

### 3. A user needs to be able to manage existing alerts

The MVP assumes that alert creation alone is not sufficient and that users need a way to review, modify, and delete previously created alerts. This assumption is the basis for interpreting the brief’s “admin view” requirement as a user-facing alert management view in the MVP.

### 4. Additional alert types and delivery channels are future extensions

The MVP assumes that the alert model will likely become more sophisticated over time, potentially including richer alert types, more advanced filters, or more granular delivery preferences. The initial implementation should therefore avoid making architectural choices that would unnecessarily block these extensions later.

### 5. Supported channels are assumed to have a notification delivery mechanism available

The MVP assumes that each supported notification channel can be reached through some delivery mechanism, such as an external API, SDK, or service integration. For example, Slack notifications may be sent through a Slack integration endpoint, and email notifications may be sent through an email delivery provider.

The exact delivery implementation is not defined by the brief and may vary by channel, but the MVP assumes that a callable mechanism exists for sending notifications through each supported channel.
