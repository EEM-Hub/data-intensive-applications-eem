---
source: sources/wiki-Apache_Kafka.md
source_url: https://en.wikipedia.org/wiki/Apache_Kafka
---

## Apache Kafka: Distributed Event Streaming Platform

Apache Kafka is an open-source distributed event store and stream-processing platform, originally developed at LinkedIn and now maintained by the Apache Software Foundation. Written in Java and Scala, it provides a unified, high-throughput, low-latency platform for handling real-time data feeds. Kafka uses a binary TCP-based protocol optimized for efficiency, grouping messages into "message sets" to reduce network overhead and turn random writes into linear sequential writes.

## Key Concepts

- **Distributed log-based messaging**: Unlike queue-based systems, Kafka retains messages in a durable, append-only log; multiple consumers read at different offsets independently
- **Partition-based ordering**: Guarantees message ordering within individual partitions, not across an entire topic
- **Manual offset management**: Consumers control their own retry and failure handling by deciding when to commit offsets; a failed consumer delays its partition without affecting others
- **Fault isolation**: Partition-based design enables parallel processing while isolating failures to individual partitions
- **Share groups (2025)**: "Queues for Kafka" (KIP-932) adds queue-like semantics where consumers cooperatively process records from the same partitions with individual message acknowledgment — consumers can exceed partition count, solving the "over-partitioning" problem
- **Message set abstraction**: Groups messages together for larger network packets, larger sequential disk operations, and contiguous memory blocks

## Commands and Syntax

No CLI commands detailed in the source. Key APIs:

- **Connect API** (Kafka Connect, added 0.9.0.0): Framework for importing/exporting data to/from external systems using "connectors." Uses Producer and Consumer APIs internally.
- **Streams API** (Kafka Streams, added 0.10.0.0): Java stream-processing library with two sub-APIs:
  - **DSL**: High-level operators — `filter`, `map`, `grouping`, `windowing`, `aggregation`, `joins`, plus table abstraction
  - **Processor API**: Low-level custom operator development (can be mixed with DSL)
- **State management**: Kafka Streams uses RocksDB for local state; state can exceed main memory since RocksDB writes to disk. All local state updates are replicated to a Kafka topic for fault-tolerant state reconstruction.

## Relationships

- **Alternatives/competitors**: RabbitMQ, Redis, NATS — other message brokers with different trade-offs (Kafka's append-only log vs. traditional queue deletion after consumption)
- **Stream processing ecosystem**: Apache Flink, Apache Samza, Apache Spark Streaming — complementary or competing stream processors
- **Architectural patterns**: Message-oriented middleware, Enterprise Integration Patterns, Event-driven SOA, Service-oriented architecture
- **Internal dependency**: RocksDB — used by Kafka Streams for local stateful processing
- **Category**: Both a message broker and a stream-processing platform — bridges two traditionally separate categories

## Exam-Relevant Points

- Kafka guarantees ordering **within a partition**, not across a topic — a critical distinction from total-order systems
- Messages are **retained in the log** after consumption (unlike traditional queues that delete on acknowledgment); consumers track their position via offsets
- Consumer offset management is **manual** — consumers choose when to commit, enabling custom retry logic
- Kafka Connect uses Producer and Consumer APIs internally — it is a framework layer, not a separate protocol
- Kafka Streams stores local state in **RocksDB** and replicates state changes to a **changelog topic** for fault tolerance — this is how state survives consumer failures
- Share groups (KIP-932) allow **more consumers than partitions** — unlike traditional consumer groups where each partition is exclusively assigned to one consumer
- Kafka uses a **binary TCP protocol** with message batching (message sets) — this is key to its throughput characteristics
- Originally developed at **LinkedIn**, open-sourced **January 2011**, graduated Apache Incubator **October 2012**
- Written in **Java and Scala**, licensed under **Apache License 2.0**
- Current stable version: **4.3.0** (May 2026)
