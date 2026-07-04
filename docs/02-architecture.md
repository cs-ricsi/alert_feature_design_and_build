## Architecture Goal

The goal of the MVP architecture is to support a simple but extensible alerting workflow that satisfies the brief while remaining realistic to implement within a limited timeframe.

The architecture should support the following core flow:

1. a user creates an alert for a supported notification channel and selects one or more alert categories
2. the system periodically fetches recent articles from an external news source
3. fetched articles are normalized into a common internal event format
4. the system skips already processed events, matches new events to alerts based on category/topic matching, and dispatches notifications
5. the user can review and manage existing alerts through the alert management view

The architecture is intentionally designed around a constrained MVP alert model: each alert is tied to a single notification channel and one or more predefined categories, rather than supporting arbitrary user-defined alert rules.
