## Architecture Goal

The goal of the MVP architecture is to support a simple but extensible alerting workflow that satisfies the brief while remaining realistic to implement within a limited timeframe.

The architecture should support the following core flow:

1. a user creates an alert for a supported notification channel and selects one or more alert categories
2. the system periodically fetches recent articles from an external news source
3. fetched articles are normalized into a common internal event format
4. the system skips already processed events, matches new events to alerts based on category/topic matching, and dispatches notifications
5. the user can review and manage existing alerts through the alert management view

The architecture is intentionally designed around a constrained MVP alert model: each alert is tied to a single notification channel and one or more predefined categories, rather than supporting arbitrary user-defined alert rules.

## High-Level Overview

At a high level, the MVP consists of five main concerns:

1. **Alert management**
   Stores and manages user alerts, including notification channel configuration and selected alert categories.

2. **Event fetching**
   Polls the external news source on a schedule and retrieves recent articles.

3. **Event normalization and deduplication**
   Converts provider articles into a common internal event format and skips already processed articles.

4. **Alert matching and notification dispatch**
   Matches events to alerts based on category/topic overlap and sends notifications through the configured channels.

5. **Alert management view**
   Provides the user-facing interface for listing, creating, editing, and deleting alerts.

In the MVP, the system does not independently determine which world events are globally important. Instead, it relies on the external provider as the source of incoming events and uses the categories selected on each alert to determine which alerts should receive which events.

## Core Components

The MVP architecture is built around the following logical components.

### 1. Alert Management

Responsible for storing and managing user alerts.

Responsibilities:

- create an alert
- update an existing alert
- delete an alert
- list alerts for a user
- validate alert configuration at the application level
- persist channel-specific configuration data
- persist selected alert categories

### 2. Event Fetcher

Responsible for retrieving recent articles from the external source.

Responsibilities:

- poll **FreeNewsAPI.io** on a fixed interval
- fetch recent articles from the configured source query
- pass raw provider articles into the normalization step

For the MVP, the default polling interval is **10 minutes**.

### 3. Event Processor

Responsible for converting fetched articles into the internal event format used during alert matching and dispatch.

Responsibilities:

- normalize provider articles into the internal event shape
- preserve useful metadata such as article UUID, topics, publisher, and publication timestamp
- forward fetched events into the alert-matching flow

### 4. Alert Matching and Dispatch

Responsible for determining which alerts should receive a given event and coordinating notification delivery.

Responsibilities:

- load alerts relevant to the event
- match event topics against alert category selections
- invoke notification delivery for each matching alert

For the MVP, an event matches an alert if the event topics intersect with the categories configured on that alert.

### 5. Notification Delivery

Responsible for sending notifications through the correct channel for each alert.

Responsibilities:

- accept a dispatch request for a specific alert and event
- resolve the alert’s channel type
- invoke the correct channel-specific delivery implementation
- encapsulate the channel-specific delivery logic for each supported notification channel

Examples of channel-specific delivery implementations:

- email delivery
- Slack delivery

### 6. Alert Management UI

Responsible for the user-facing alert management experience.

Responsibilities:

- display the user’s current alerts
- allow creation of a new alert
- allow modification of an existing alert
- allow deletion of an existing alert

This UI is the MVP interpretation of the brief’s “admin view” requirement.
