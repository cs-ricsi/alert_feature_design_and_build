# Decision: Alert Subscription Model for the MVP

## Goal

Define how alerts should work in the MVP given the limited timeframe, the ambiguity of the brief, and the capabilities of the selected event source.

The original brief states that users should be able to set up alerts so they get notified when something important happens in the world, with examples such as breaking news, market movements, and natural disasters. However, it does not explicitly state whether users are expected to configure detailed event rules, choose event categories, or simply subscribe to a general stream of important notifications.

## Decision

For the MVP, alerts are interpreted as **channel-specific subscriptions to selected news categories**, not as fully user-defined event rules.

This means:

- a user creates an alert by choosing a supported notification channel
- each alert is tied to exactly one delivery channel
- each alert also includes one or more selected categories
- the system fetches articles from a shared external news source and routes them to alerts based on category/topic matching
- the user does not define custom alert rules, thresholds, or complex filter logic
- an alert receives an event when the event’s topics match one or more of the categories selected for that alert

Because the MVP initially supports only **email** and **Slack**, a user can currently have up to **two alerts**: one email alert and one Slack alert. Each of those alerts can be configured with its own category selections.

## Reasoning

The original brief is open to multiple interpretations. One possible interpretation is that users should be able to create detailed alert rules for specific event categories such as breaking news, market movements, or natural disasters. Another interpretation is that users are subscribing to notifications about important world events, while the system decides which events qualify.

The selected event source introduces a useful middle ground. It returns article-level topic metadata, which allows the MVP to support category-based subscriptions without requiring a complex rule engine or separate source requests per category.

For the MVP, alerts are therefore modeled as **channel-specific subscriptions with category selection**.

This approach was chosen for the following reasons:

### 1. It gives users meaningful control over what they receive

Allowing users to select one or more categories makes the alerting experience more aligned with the brief than a pure “send everything to everyone” subscription model. Users can express what kinds of events they want to hear about without needing a complex alert-definition interface.

### 2. It uses provider metadata that is already available

The selected event source returns article topics as part of the response. That means category-based routing can be supported without multiplying source requests by topic and without introducing a separate event-classification system inside the MVP.

### 3. It still keeps the alert model simple

Although alerts now include categories, the MVP still avoids a more complex rule-definition model. Users are not defining arbitrary conditions, keywords, severity thresholds, geographic filters, or custom logic. The subscription model remains intentionally constrained to a supported set of categories.

### 4. It fits the timeboxed nature of the project

The project is being delivered within a limited timeframe. Category-based subscriptions add useful personalization while keeping the matching logic simple: an event is routed to an alert if the event topics intersect with the alert’s selected categories.

### 5. It keeps channel operations simple and explicit

Modeling each alert as a single-channel subscription continues to make common operations easier to reason about and implement.

This includes:

- creating separate alerts for email and Slack if needed
- editing or deleting an alert for one channel without affecting another
- keeping channel-specific delivery configuration isolated per alert
- allowing different category selections per channel if desired

### 6. It provides a cleaner foundation for future alert evolution

This model creates a practical path toward richer alerting later. If the product evolves, additional subscription settings can be attached to a channel-specific alert without redesigning the basic alert structure.

## Impact

This decision affects the MVP in several ways:

- the user-facing alert model becomes a **category-based subscription model** rather than a pure broadcast subscription model
- each alert is represented as a **single-channel subscription with category selections**
- the event-processing flow includes **matching event topics to alert categories** before dispatching notifications
- the notification model becomes “send fetched events to alerts whose selected categories match the event topics”
- the data model must store both **channel-specific configuration** and **selected categories** for each alert
- the alert management UI must allow users to choose categories when creating or editing an alert

## Concerns and Tradeoffs

This decision improves the usefulness of the MVP, but it also introduces tradeoffs that should be acknowledged.

### 1. The alert model is still intentionally limited

Users can select categories, but they still cannot define fully custom alert logic. The MVP does not support arbitrary rules, keyword filters, thresholds, severity settings, or geographic constraints.

### 2. Category quality depends on the external provider’s topic metadata

The selected categories are matched against provider topics. If provider topic tagging is broad, inconsistent, or incomplete, alert matching quality may be affected.

### 3. The supported category set must be curated carefully

Although the provider may expose many topics, the MVP should avoid exposing an uncontrolled or overly large category list. A smaller supported set is easier to explain, implement, and test.

### 4. The matching model is intentionally simple

The MVP uses category/topic intersection as the routing rule. This is intentionally much simpler than a full alert-rule engine, but it also means users cannot express more nuanced preferences.

### 5. Future alert types and filters should remain an extension path

This decision is specific to the MVP and should not block future support for richer alert models. The architecture should therefore avoid hard-coding assumptions that prevent later introduction of features such as:

- more granular alert categories
- keyword or entity-based filters
- severity or urgency thresholds
- geographic relevance
- more advanced matching rules
