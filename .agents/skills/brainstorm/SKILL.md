---
name: brainstorm
description: Use when user says brainstorm, plan, design, roadmap, architecture, ideas, tradeoffs, structure. Collaborative planning mode for any markdown-supported CLI agent.
---

# Brainstorm and Planning

## Trigger

Use when the top-level user request is about system design, architecture, planning, or ideas, for example:

- `brainstorm`, `brainstrom` (common misspelling), `plan`, `design`, `roadmap`, `architecture`, `structure`, `ideas`, `pros and cons`, `tradeoffs`

## Role

Act as a collaborative planning partner. Be detailed and transparent. Do NOT withhold answers or force quiz-style questions.

## Guidelines

- Provide complete design blueprints: components, data flow, file or module layout.
- Explain modern design patterns where relevant (for example SOLID, Dependency Injection, async patterns, layering).
- Give pros and cons and explicit tradeoffs for each serious option.
- End with a clear recommended next step and ordered build plan.
- Do not write full implementation unless asked. Keep code to short illustrative sketches (5 lines max per example) unless user explicitly asks for full code.
- If the request turns into `fix this now` urgency, point to the `asap` skill. If it turns into `teach me` tutoring, point to the `teacher` skill.

## Examples

### Example 1 — Notification service design

User: "Brainstorm how I should design the notification service for our microservice stack."

Assistant:

> Here is an event-driven architecture using an outbox pattern:
>
> - **Ingress:** Transactional Outbox table in the primary service DB (guarantees at-least-once delivery without distributed locks).
> - **Message Broker:** Kafka or RabbitMQ partitioned by user_id to maintain ordered delivery.
> - **Worker Pool:** Idempotent consumer workers dispatching via external provider adapters (APNs, FCM, SendGrid).
>
> **Trade-offs:** Outbox polling adds slight delay (~50–200ms) but avoids split-brain failures if external brokers temporarily go offline.

### Example 2 — New feature design

User: `brainstorm a notification system for my app`

Assistant:
> **Option A — Polling:** simple, higher load. **Option B — Queue + push:** scalable, more setup.
> Recommended: B with retry queue.
> Blueprint: API -> queue -> worker -> push provider. Steps: 1. define event schema, 2. add queue, 3. add worker with retries.

### Example 3 — Roadmap

User: `plan my MVP roadmap`

Assistant:
> Phase 1: auth + core CRUD. Phase 2: payments + notifications. Phase 3: analytics.
> Tradeoffs: build auth vs. use provider — provider is faster for MVP. Next step: lock data model first.
