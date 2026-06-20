---
source: sources/wiki-Dynamo_storage_system.md
source_url: https://en.wikipedia.org/wiki/Dynamo_(storage_system)
---

## Amazon Dynamo: Highly Available Key-Value Storage System

Amazon Dynamo is a set of techniques for building a highly available key-value structured storage system or distributed data store. Developed internally at Amazon to address scalability issues encountered during the 2004 holiday season, Dynamo combines properties of both databases and distributed hash tables (DHTs). The original paper was published in 2007 at SOSP. Amazon never released the implementation, but the paper inspired major NoSQL systems including Apache Cassandra, Riak, and Project Voldemort.

## Key Concepts

- **Leaderless replication**: Dynamo uses leaderless (peer-to-peer) replication — every node has the same responsibilities with no distinguished leader node
- **Four design principles**:
  - *Incremental scalability*: Scale out one node at a time with minimal impact
  - *Symmetry*: Every node has identical responsibilities — no special roles
  - *Decentralization*: Favors peer-to-peer techniques over centralized control
  - *Heterogeneity*: Exploits differences in node capabilities; work distribution proportional to server capacity
- **Dynamo vs. DynamoDB**: Despite the similar name, Amazon DynamoDB uses a completely different architecture — single-leader replication rather than Dynamo's leaderless model. DynamoDB is "built on the principles of Dynamo" but is a distinct hosted AWS service
- **Not publicly available**: Amazon never released Dynamo externally; only the paper was published

## Commands and Syntax

No commands or configuration syntax — Dynamo is a design described in an academic paper, not a released product. The techniques are implemented in derivative systems (Cassandra, Riak, Voldemort).

## Relationships

| Problem | Technique | Purpose |
|---------|-----------|---------|
| Dataset partitioning | **Consistent hashing** | Linear scalability proportional to number of nodes |
| Highly available writes | **Vector clocks** / Dotted-Version-Vector Sets | Version size decoupled from update rates; reconciliation during reads |
| Temporary failures | **Sloppy quorum** + **hinted handoff** | High availability when some replicas are unavailable |
| Permanent failures | **Anti-entropy via Merkle trees** | Identify and synchronize divergent replicas proactively |
| Membership & failure detection | **Gossip protocol** | Decentralized membership and liveness tracking — no central registry |

- **Amazon S3**: The S3 index layer implements and extends core Dynamo features
- **Apache Cassandra**: Directly inspired by Dynamo (partitioning, replication) combined with Bigtable's data model
- **Riak, Voldemort**: Other open-source implementations based on the Dynamo paper
- Related to broader topics: distributed data stores, NoSQL, structured storage

## Exam-Relevant Points

- Dynamo is **leaderless**; DynamoDB is **single-leader** — this is a common trick question
- The five core techniques and which problem each solves (consistent hashing, vector clocks, sloppy quorum + hinted handoff, Merkle trees, gossip protocol) — memorize the problem-technique-advantage table
- Dynamo was created to solve Amazon's **2004 holiday season scalability** problems
- Dynamo favors **availability over consistency** (AP in CAP theorem terms) — writes are always accepted, conflicts reconciled on read
- Sloppy quorum means writes can go to nodes that aren't the "home" for a key, with hinted handoff returning data to the correct node later
- Vector clocks track causality to detect concurrent updates; reconciliation happens at read time, not write time
- Amazon never released Dynamo's implementation — only the 2007 SOSP paper
- The Dynamo paper is one of the most influential papers in distributed systems, spawning the NoSQL movement
