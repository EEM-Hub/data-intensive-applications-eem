---
source: sources/wiki-Message_broker.md
source_url: https://en.wikipedia.org/wiki/Message_broker
---

## Message Brokers: Architecture, Purpose, and Patterns

A message broker is an intermediary program module that translates messages between the formal messaging protocols of senders and receivers. It is an architectural pattern for message validation, transformation, and routing that mediates communication among applications while minimizing their mutual awareness — effectively implementing decoupling. Message brokers are a building block of message-oriented middleware (MOM) but are not a replacement for traditional middleware like MOM and remote procedure call (RPC).

## Key Concepts

- **Core function**: Takes incoming messages from applications and performs actions on them — routing, transforming, aggregating, storing, or enriching messages
- **Decoupling**: The central value proposition — applications don't need to know about each other, only about the broker
- **Two fundamental architectures**:
  - **Hub-and-spoke**: A central server provides integration services
  - **Message bus**: The broker is a distributed communication backbone acting on a bus
  - **Multi-hub**: A more scalable variant integrating multiple brokers
- **Message aggregation**: Can decompose messages into multiple parts, send to destinations, then recompose responses into a single return message
- **Guaranteed delivery**: Brokers can provide reliable storage, guaranteed message delivery, and transaction management
- **Content-based routing**: Brokers can route using the publish-subscribe pattern based on content or topic
- **Real-time semantics**: Purpose-built brokers can achieve time-bounded, end-to-end predictable communications (relevant for robotics, vehicle automation, software-defined radio)
- **End-to-end predictability** (per OMG Real-time CORBA): Respecting thread priorities, bounding priority inversions, bounding invocation latencies

## Commands and Syntax

No CLI commands per se, but the broker lifecycle actions are important to understand:

- **Route** messages to one or more destinations
- **Transform** messages to alternative representations
- **Aggregate/decompose** messages across multiple receivers
- **Augment** messages via external repository interaction
- **Invoke** web services for data retrieval
- **Respond** to events or errors
- **Publish-subscribe** content and topic-based routing

## Relationships

- **Message-oriented middleware (MOM)**: Brokers are a building block of MOM but not a full replacement
- **Publish-subscribe pattern**: A key routing mechanism implemented by brokers
- **Message queues**: Brokers often manage workload or message queues for multiple receivers
- **Remote procedure call (RPC)**: Brokers complement rather than replace RPC
- **MQTT**: A lightweight messaging protocol commonly used with IoT-focused brokers
- **Web services**: Brokers can invoke web services to retrieve or enrich data
- **Stream processing**: Systems like Apache Kafka and Kinesis blur the line between message broker and stream processing platform

## Exam-Relevant Points

- A message broker implements **decoupling** — this is the primary architectural benefit to remember
- Know the two architectures: **hub-and-spoke** (centralized) vs. **message bus** (distributed)
- Brokers are a **building block of MOM**, not a replacement for it
- Key broker capabilities: routing, transformation, aggregation, guaranteed delivery, transaction management
- **Apache Kafka**, **RabbitMQ**, **Apache ActiveMQ**, and cloud services (AWS SQS/SNS, Google Pub/Sub, Azure Service Bus) are the most commonly referenced implementations
- RabbitMQ is written in **Erlang**, NATS in **Go**, Redpanda in **C++** (Kafka API-compatible) — language choices reflect performance and reliability trade-offs
- Real-time brokers must bound **latency** and **priority inversion** duration per OMG CORBA spec
- The broker pattern supports **non-functional requirements** like reliability, scalability, and transaction management — not just message routing
