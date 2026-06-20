---
source: sources/wiki-Consistent_hashing.md
source_url: https://en.wikipedia.org/wiki/Consistent_hashing
---

## Consistent Hashing: Minimal-Disruption Key Distribution for Distributed Systems

Consistent hashing is a hashing technique designed for distributed systems where the set of nodes (servers) changes dynamically. Unlike traditional modular hashing where changing the number of slots forces nearly all keys to be remapped, consistent hashing ensures that only `n/m` keys (keys divided by slots) need redistribution when nodes are added or removed. Invented at MIT by David Karger et al. in 1997, it became foundational to CDNs, distributed caches, and distributed hash tables.

## Key Concepts

- **The core problem**: Traditional hash tables use `hash(key) % n` to assign keys to slots. When `n` changes, nearly every key remaps — catastrophic for distributed systems.
- **Hash ring (unit circle)**: Both keys and servers are hashed onto a circular space (0–360 degrees). Each key is assigned to the next server found in clockwise order.
- **Minimal disruption guarantee**: Adding the nth server causes only `1/n` fraction of keys to relocate. Removing a server only affects keys assigned to that server.
- **Virtual nodes**: To prevent skewed distribution, each physical server gets multiple positions ("virtual nodes") on the ring. The number of virtual nodes per server is its "weight."
- **Hot spot handling**: A hot key can be replicated to multiple contiguous servers by traversing clockwise. If two hot keys hash near each other, different hash functions per key can spread them across different server sets.
- **Cache miss on new nodes**: In web caching, newly added servers don't require explicit data transfer — cache misses trigger fetches from origin, and stale copies on old servers are evicted by normal cache policies.
- **Rendezvous hashing**: An alternative (1996) that achieves the same goals using Highest Random Weight (HRW). Consistent hashing is actually a special case of rendezvous hashing.

## Commands and Syntax

**Lookup (key placement):**
1. Compute `hash(key) % 360` to get position on ring
2. Binary search the sorted list of server positions to find the next clockwise server — O(log N)
3. If key's hash exceeds all server positions, wrap to the smallest server position

**Implementation uses a BST** to maintain server positions dynamically:
- **Insert key**: Find successor of `hash(key)` in BST of server IDs; assign key to that server
- **Delete key**: Find successor, remove key from that server
- **Add server**: Insert new server position into BST; migrate keys whose hash < new server's hash from the successor server
- **Remove server**: Move all keys from departing server to its successor in the BST

## Relationships

- **Distributed Hash Tables (DHTs)**: Consistent hashing is the cornerstone — Chord, DynamoDB, Cassandra all use it for key-space partitioning
- **Load Balancing**: Used in CDNs (Akamai), gRPC routing, and application-level routing (Discord, Akka)
- **Replication**: Works alongside replication strategies — keys can be assigned to multiple consecutive ring positions for redundancy
- **Partitioning (Chapter 6 of DDIA)**: Consistent hashing is one approach to hash-based partitioning, contrasted with range-based partitioning
- **CAP Theorem / Dynamo-style systems**: Consistent hashing enables the "A" and "P" by allowing the system to keep serving when nodes fail, with only local redistribution

## Exam-Relevant Points

- **Complexity comparison**: Classic hash table does O(K) work to add/remove a node vs. consistent hashing's O(K/N + log N). But key lookup degrades from O(1) to O(log N).
- **Only K/N keys move** on average when adding or removing a node — this is the defining property.
- **Virtual nodes solve load skew** — without them, servers can end up with very uneven arc lengths on the ring.
- **Real-world systems using consistent hashing**: Amazon Dynamo, Apache Cassandra, Riak, Couchbase, ScyllaDB, Akamai CDN, Discord, OpenStack Swift, GlusterFS, MinIO.
- **Consistent hashing is a special case of rendezvous hashing** — rendezvous hashing is more general and simpler but both achieve the same minimal-disruption goal.
- **Akamai** was founded by the co-authors of the consistent hashing paper (Lewin and Leighton); it uses consistent hashing within clusters and stable marriage across clusters.
- **Linear hashing** handles sequential server add/remove; consistent hashing handles arbitrary-order changes — an important distinction.
