# Decision: Event Ingestion Strategy for the MVP

## Goal

Define how the MVP should ingest alert-triggering events and route them to user alerts.

The brief requires alerts for important world events, but it does not define where those events come from or how the system should receive them. This decision defines the MVP event source and ingestion flow.

## Decision

For the MVP, alert-triggering events will be ingested by **polling FreeNewsAPI.io** on a fixed schedule.

The ingestion model is based on the following decisions:

- the system polls **FreeNewsAPI.io** every **10 minutes**
- each polling cycle fetches a shared stream of recent articles
- fetched articles are normalized into an internal alert-event shape
- article metadata such as `uuid`, `topics`, `publisher`, and `published_at` is preserved where useful
- alerts are matched against fetched events using the article `topics` and the categories selected on each alert
- already processed articles are skipped based on their provider `uuid` to avoid duplicate notifications

The MVP event flow is therefore:

**poll → normalize → deduplicate → match → notify**

## Reasoning

### 1. It is a practical way to ingest real events within the timebox

Polling a free external API is simpler and safer for the MVP than building a production-grade ingestion pipeline or relying on a webhook-based source strategy.

### 2. FreeNewsAPI provides metadata that supports alert matching

The provider returns article topics and a stable article identifier, which makes it suitable both for category-based routing and for deduplication.

### 3. Fetching once is more efficient than polling per category

Because the provider already returns article topics, the system can fetch a shared stream of articles once and perform category matching internally rather than issuing separate requests per category.

### 4. Deduplication is required for polling-based ingestion

Polling recent articles will naturally return overlapping results across runs. Tracking processed article UUIDs prevents duplicate notifications.

## Impact

This decision affects the MVP architecture in the following ways:

- the system needs a scheduled polling component
- the event-ingestion layer must normalize provider articles into an internal event format
- the alert dispatch flow must match article topics against alert categories before sending notifications
- the system must store processed article UUIDs to avoid duplicate alerts
- the architecture should keep the provider integration isolated so it can be replaced or extended later
