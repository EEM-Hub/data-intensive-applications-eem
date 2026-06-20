---
source: sources/wiki-PublishE28093subscribe_pattern.md
source_url: https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern
---

## Publish–Subscribe Messaging Pattern

The publish–subscribe (pub/sub) pattern is a messaging architecture where message senders (publishers) categorize messages into topics and send them without knowing who will receive them, while receivers (subscribers) express interest in specific topics without knowing who publishes them. This decoupling enables asynchronous, many-to-many communication and is a core component of message-oriented middleware systems.

## Key Concepts

- **Publishers** send messages categorized by topic/class without knowledge of subscribers
- **Subscribers** register interest in topics and receive only matching messages, without knowledge of publishers
- **Decoupling** is the central design goal — spatial (location), temporal (timing), and identity decoupling between producers and consumers
- **Contrast with message queues**: pub/sub delivers to all matching subscribers (fan-out); message queues deliver each message to one consumer (competing consumers)
- **Contrast with observer pattern**: pub/sub emphasizes distributed, broker-mediated communication; observer pattern is typically in-process and tightly coupled
- **Message filtering** determines which messages reach which subscribers:
  - **Topic-based**: subscribers register for named channels; receive all messages on those channels
  - **Content-based**: subscribers define attribute constraints; messages delivered only if they match
  - **Hybrid**: topic-based routing with content-based filters applied within topics
- **Broker-based topology**: a central intermediary (message broker/event bus) receives, routes, and optionally stores messages
- **Brokerless topology**: publishers and subscribers discover each other directly (e.g., DDS using IP multicast); requires overlay network construction
- **Subscriber registration timing**: build-time (hardcoded handlers), initialization-time (XML config), or runtime (dynamic add/remove)
- Earliest known pub/sub system: the "news" subsystem of the **Isis Toolkit** (1987, SOSP '87)

## Commands and Syntax

No specific CLI commands — pub/sub is a pattern, not a tool. Key implementations and protocols:

- **Apache Kafka** — distributed log-based pub/sub with topic partitions
- **MQTT** — lightweight pub/sub protocol for IoT and constrained networks
- **Java Message Service (JMS)** — Java API supporting both pub/sub and point-to-point
- **Data Distribution Service (DDS)** — brokerless middleware using IP multicast
- **RSS / Atom** — web syndication protocols implementing pub/sub at Internet scale
- **WebSub** — W3C protocol for real-time pub/sub over HTTP

## Relationships

- **Message queue**: sibling paradigm — queues use competing consumers (one receiver per message); pub/sub uses fan-out (all matching subscribers receive)
- **Message-oriented middleware (MOM)**: pub/sub is typically one component within a larger MOM system
- **Observer pattern**: in-process predecessor; pub/sub evolved from observer to handle distributed, asynchronous scenarios
- **Event-driven programming**: pub/sub is the distributed implementation of event-driven architecture
- **Message broker**: the intermediary component in brokered pub/sub topologies
- **RPC / point-to-point**: synchronous alternatives that provide less decoupling but stronger delivery guarantees
- **Producer–consumer problem**: pub/sub is one solution pattern for this concurrency challenge
- **Store and forward**: brokers may buffer messages for offline subscribers
- **Enterprise Integration Patterns** (Hohpe, 2003): canonical reference for messaging patterns including pub/sub

## Exam-Relevant Points

- Pub/sub provides the **highest level of decoupling** among messaging architectures — more than RPC or point-to-point
- **Three filtering approaches**: topic-based, content-based, hybrid — know the tradeoffs
- **Advantages**: loose coupling, scalability via parallel operation and caching, easy addition of redundant subscribers without impacting existing components
- **Disadvantages**: no guaranteed delivery by default (must be engineered separately), potential for load surges and throughput instability at scale, security risks (unauthorized publishers injecting messages, brokers sending to wrong clients)
- Pub/sub scales well at **small scale** and **Internet scale** (RSS/Atom), but enterprise-scale data centers with thousands of servers present **scalability challenges** that remain active research
- **Temporal decoupling**: publishers and subscribers need not be running simultaneously — a key distinction from client-server
- Adding **redundant subscribers** increases reliability without affecting publishers or other subscribers — contrasts with client-server where redundant servers add complexity
- **Semantic/format coupling** is the hidden risk: even though components are locationally decoupled, changes to message structure can make systems brittle
- Brokerless systems (DDS) use **Navigable Small-World topologies** (Kleinberg) for efficient decentralized routing
