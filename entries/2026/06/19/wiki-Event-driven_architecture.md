---
source: sources/wiki-Event-driven_architecture.md
source_url: https://en.wikipedia.org/wiki/Event-driven_architecture
---

## Event-Driven Architecture (EDA)

A software architecture paradigm built around the production, detection, and consumption of events — significant changes in state. EDA provides high fault tolerance, performance, and scalability through loose coupling and asynchronous communication, but introduces complexity in testing, error handling, and data consistency. It is well-suited for complex, dynamic workloads and often built atop message-driven architectures.

## Key Concepts

- **Event**: A significant change in state (e.g., order placed, door opened). Technically, what is transmitted is an *event notification* (a message), not the event itself — the event is the state change that triggered the message.
- **Core components**: Event emitters (producers/agents), event consumers (sinks), and event channels (conduits). Emitters don't know about consumers — full decoupling.
- **Two topologies**:
  - **Broker topology**: Components broadcast events system-wide with no orchestrator. Higher performance and scalability.
  - **Mediator topology**: Central orchestrator controls event workflow. Better control and error handling.
  - Hybrid approaches combine both.
- **Event types**:
  - **Domain events**: Scoped to a single bounded context, lighter payloads, used for internal business logic.
  - **Integration events**: Cross bounded contexts, heavier payloads with extra attributes to ensure data consistency across services.
- **Event structure**: Header (name, timestamp, type) + body/payload (state change details). Payload sizing is a spectrum — full data (fast but coupling/consistency risk) vs. keys-only requiring consumer lookups (slower but less coupling).
- **Loose coupling**: Decoupled in space, time, and synchronization — but *semantically coupled* via event subscriptions and schemas.
- **Horizontal scalability**: Application state can be copied across parallel snapshots; new nodes take a state copy and replay the event stream.

## Event Processing Styles

- **Simple event processing**: Direct reaction to a single notable event (e.g., sensor detects low tire pressure → warning light). Reduces lag time.
- **Event stream processing (ESP)**: Screens ordinary and notable events from continuous streams, enabling real-time information flow and in-time decision making.
- **Complex event processing (CEP)**: Detects patterns across multiple simple/ordinary events over time. Uses event correlation (causal, temporal, spatial) to infer higher-order events. Used for anomaly detection, threats, opportunities.
- **Online event processing (OLEP)**: Uses asynchronous distributed event logs for complex scenarios across heterogeneous systems. Strong consistency but no guaranteed upper bound on processing time.

## Event Flow Layers (Four-Layer Model)

1. **Event producer**: Senses facts and represents them as event messages (sensors, email clients, e-commerce systems).
2. **Event channel**: Propagates events from producer to engine (TCP/IP, files, queues). Typically asynchronous with events queued for processing.
3. **Event processing engine**: Identifies events, selects and executes appropriate reactions, can trigger assertions/actions.
4. **Downstream event-driven activity**: Where consequences manifest (emails, UI warnings, automated workflows).

## Commands and Syntax

No specific CLI commands — this is an architectural pattern. Key implementation concerns:

- **Synchronous transactions in EDA** (two approaches):
  - Two separate queues: one for requests, one for replies; producer waits for response.
  - One dedicated ephemeral queue per request.
- **Event payload strategies**: Include all attributes in payload vs. include only keys/IDs with consumer-side lookups. Architect must size payloads to consumer needs.
- **Error handling pattern**: Dedicated error-handler processor receives failed events asynchronously, attempts repair and resubmits to original channel. Failed repairs escalate to administrator. Caveat: resubmitted events process out of order.
- **Data loss prevention**: Persist in-transit events; dequeue only after next component acknowledges receipt ("client acknowledge mode," "last participant support").

## Relationships

- **Service-Oriented Architecture (SOA)**: EDA complements SOA — services activate via triggers on incoming events. SOA 2.0 / Event-driven SOA merges both paradigms.
- **Message-oriented middleware**: Common physical implementation for event channels.
- **Distributed computing**: EDA simplifies horizontal scaling in distributed models.
- **Domain-driven design**: Domain events align with bounded contexts; integration events bridge them — directly tied to DDD concepts.
- **Circuit breaker pattern**: Addresses the Timeout AntiPattern in distributed EDA systems by monitoring service health rather than relying on timeout values.
- **Event sourcing**: Related pattern where application state is derived from replaying event streams (referenced via Fowler).
- **Complex event processing / Event stream processing**: Specialized processing styles within EDA.
- **Staged event-driven architecture (SEDA)**: Variant that decomposes processing into stages connected by queues.
- **Space-based architecture**: Related distributed architecture pattern.

## Exam-Relevant Points

- An event is a state change; what travels is the *event notification message*, not the event itself.
- Broker topology = performance/scalability; Mediator topology = control/error handling.
- Domain events are intra-bounded-context with light payloads; integration events are cross-context with heavier payloads.
- Full-payload events trade speed for coupling and consistency risk; key-only payloads trade speed for reduced coupling.
- EDA is loosely coupled in space, time, and synchronization but *tightly coupled semantically* through event schemas and subscriptions.
- The four event flow layers: producer → channel → processing engine → downstream activity.
- Three core processing styles: simple (single event → reaction), stream (filtering/routing continuous events), complex (pattern detection across multiple events over time).
- OLEP provides strong consistency via distributed event logs but cannot guarantee processing time bounds.
- Key challenges: testing difficulty, error handling (use dedicated error-handler processors), data loss (persist in-transit events with acknowledgment), event granularity (too many overwhelms; too few causes unnecessary processing), and the fallacies of distributed computing.
- The Timeout AntiPattern: short timeouts fail legitimate requests; long timeouts degrade UX. Circuit breaker pattern is the recommended solution.
- Event evolution strategies include semantic versioning, schema evolution, and adapter patterns for backward/forward compatibility.
- Scalability via state snapshots: copy application state, feed event stream to new nodes.
