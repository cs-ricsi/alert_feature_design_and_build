# Decision: Alert Subscription Model for the MVP

## Goal

Define how alerts should work in the MVP given the limited timeframe and the ambiguity of the brief.

The original brief states that users should be able to set up alerts so they get notified when something important happens in the world, with examples such as breaking news, market movements, and natural disasters. However, it does not explicitly state whether users are expected to configure detailed event rules, choose event categories, or simply subscribe to important world-event notifications.

## Decision

For the MVP, alerts are interpreted as **channel-specific subscriptions to important world events**, not as user-defined event rules or event-category filters.

This means:

- a user creates an alert by choosing a supported notification channel
- each alert is tied to exactly one delivery channel
- the user does not explicitly define which event types should trigger the alert
- the system is responsible for determining whether an event is important enough to notify users about
- every active alert receives every event that the system classifies as alert-worthy

Because the MVP initially supports only **email** and **Slack**, a user can currently have up to **two alerts**: one email alert and one Slack alert.

## Reasoning

The original brief is open to multiple interpretations. One possible interpretation is that users should be able to create detailed alert rules for specific event categories such as breaking news, market movements, or natural disasters. Another interpretation is that users are subscribing to notifications about important world events, while the system decides which events qualify.

For the MVP, the second interpretation was chosen, but with alerts modeled as **channel-specific subscriptions** rather than a single subscription with multiple channels.

This approach was chosen for the following reasons:

### 1. It stays closer to the minimum explicit requirements of the brief

The brief clearly states that users should be able to set up alerts and receive notifications through email and Slack. It does not explicitly require user-defined filtering, event-specific subscriptions, or a rule-building interface.

A channel-based subscription model satisfies the core requirement of allowing users to receive important-event notifications while avoiding assumptions about product behavior that the brief does not define.

### 2. It significantly reduces implementation complexity

A rule-based alert model would require additional product and technical decisions, including:

- how users define event categories or conditions
- how alert rules are stored and validated
- how events are matched against user-defined rules
- how the UI exposes that configuration clearly

A subscription-based model avoids this complexity and keeps the MVP focused on the core alert delivery flow.

### 3. It fits the timeboxed nature of the project

The project is being delivered within a limited timeframe. Treating alerts as channel-specific subscriptions allows the MVP to demonstrate the end-to-end system without requiring a larger product-definition exercise or a more complex matching engine.

### 4. It keeps channel operations simple and explicit

Modeling each alert as a single-channel subscription makes common operations easier to reason about and implement.

This includes:

- deleting or disabling an alert for one channel without affecting another
- searching or filtering alerts by channel
- inspecting channel-specific delivery behavior more cleanly
- keeping each alert record tied to a single delivery configuration

This is particularly useful for the MVP because the initial channels are limited and clearly defined.

### 5. It provides a cleaner path for future alert evolution

Although the MVP does not support alert types or user-defined filters, channel-specific alerts create a cleaner foundation for future extensions.

If alert types, priorities, or preferences are introduced later, it will be easier to attach those settings directly to a specific alert/channel combination rather than introducing channel-specific overrides inside a shared multi-channel subscription.

## Impact

This decision affects the MVP in several ways:

- the user-facing alert model becomes a subscription model rather than a rule-definition model
- each alert is represented as a single-channel subscription rather than a multi-channel subscription object
- the event-processing flow becomes a system-driven “important event broadcast” flow rather than a user-rule matching engine
- the notification model is simplified to “send important events to all active alerts”
- the data model only needs to represent channel-specific subscriptions rather than complex alert conditions
- the admin view can focus on alerts, processed events, and notification deliveries

## Concerns and Tradeoffs

This decision intentionally simplifies the product model for the MVP, but it also introduces some limitations that should be acknowledged.

### 1. Alerts are simplified into subscriptions

In this MVP, users are not defining what they want to be alerted about. They are only choosing whether they want to receive important world-event alerts and through which channels. This means the MVP behaves more like a subscription system than a personalized alert-definition system.

### 2. Personalization is intentionally limited

Because every important event is sent to every active alert, the MVP does not yet support user-level filtering such as event categories, severity preferences, topic preferences, or geographic relevance.

### 3. Event importance becomes a system concern

Since users do not define alert criteria, the system must decide which events are important enough to notify. For the MVP, this is acceptable, but it shifts product complexity away from user-defined rules and into the event-processing logic.

### 4. The product model is narrower than a typical “alerts” system

A natural interpretation of “set up alerts” may imply that users can control what they are alerted about, not only where notifications are delivered. This MVP intentionally chooses a narrower interpretation in order to keep the implementation small and coherent within the timebox.

### 5. Future alert types should remain an extension path

This decision is specific to the MVP and should not block future support for richer alert models. The architecture should therefore avoid hard-coding assumptions that prevent later introduction of features such as:

- alert types or event categories
- per-alert filters or preferences
- event severity thresholds
- more granular matching rules

The MVP should be designed so these capabilities can be added later without requiring the alerting system to be fundamentally rethought.
