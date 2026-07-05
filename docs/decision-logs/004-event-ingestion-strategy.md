# Decision: Event Ingestion Strategy for the MVP

## Goal

Define how the MVP should ingest alert-triggering events and route them to user alerts.

The brief requires alerts for important world events, but it does not define where those events come from or how the system should receive them. This decision defines the MVP event source and ingestion flow.

## Decision

For the MVP, alert-triggering events will be ingested by **polling FreeNewsAPI.io** on a fixed schedule.

The ingestion model is based on the following decisions:

- the system polls **FreeNewsAPI.io** every **10 minutes**
- each polling cycle fetches articles from the **last 10 minutes**
- fetched articles are normalized into an internal event shape during processing
- article metadata such as `uuid`, `topics`, `publisher`, and `published_at` is preserved where useful during the processing flow
- alerts are matched against fetched events using the article `topics` and the categories selected on each alert
- the MVP does **not** persist processed event identifiers or implement a deduplication layer

The MVP event flow is therefore:

**poll → normalize → match → notify**

## Reasoning

### 1. It is a practical way to ingest real events within the timebox

Polling a free external API is simpler and safer for the MVP than building a production-grade ingestion pipeline or relying on a webhook-based source strategy.

### 2. FreeNewsAPI provides metadata that supports alert matching

The provider returns article topics, publisher information, timestamps, and article identifiers. This makes it suitable for category-based routing without requiring the system to build its own event classification model.

### 3. Fetching once is more efficient than polling per category

Because the provider already returns article topics, the system can fetch a shared stream of recent articles once and perform category matching internally rather than issuing separate requests per category.

### 4. The MVP intentionally accepts a simplified polling window model

The MVP fetches only the last 10 minutes of articles on each 10-minute polling cycle and does not persist processed event identifiers for deduplication.

This keeps the ingestion flow smaller and easier to implement, but it also means the system may miss edge-case articles around polling boundaries if an article is not returned in the expected polling cycle and later falls outside the next 10-minute fetch window. This tradeoff is accepted for the MVP in order to keep the ingestion model simple.

## Impact

This decision affects the MVP architecture in the following ways:

- the system needs a scheduled polling component
- the event-ingestion layer must normalize provider articles into an internal event format during processing
- the alert dispatch flow must match article topics against alert categories before sending notifications
- the MVP does not require processed-event persistence or a deduplication layer
- the architecture should keep the provider integration isolated so it can be replaced or extended later
