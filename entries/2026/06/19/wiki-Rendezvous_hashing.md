---
source: sources/wiki-Rendezvous_hashing.md
source_url: https://en.wikipedia.org/wiki/Rendezvous_hashing
---

## Rendezvous (Highest Random Weight) Hashing

Rendezvous hashing, also called Highest Random Weight (HRW) hashing, is a distributed agreement algorithm that allows clients to independently and deterministically select the same k sites out of n possible sites for placing an object. It predates consistent hashing (1996 vs 1997), is simpler conceptually, and is increasingly preferred in production systems including GitHub's load balancer, Apache Ignite, Apache Kafka, and Twitter EventBus.

## Key Concepts

- **Core mechanism**: For each object O, compute a hash weight w(i,j) = h(O_i, S_j) for every site S_j. All clients independently pick the k sites with the highest hash values — guaranteed agreement with no coordination.
- **Minimal disruption**: When a site fails or is removed, only objects mapped to that site are remapped. All other assignments remain stable.
- **Consistent hashing is a special case**: Consistent hashing solves only k=1 using a token ring; rendezvous hashing generalizes to arbitrary k with a simpler algorithm.
- **Load balancing**: With a uniform hash function, each of n sites is equally likely to receive any given object.
- **Heterogeneous capacity**: Sites with higher capacity are represented multiple times in the site list (e.g., a site with 2x capacity appears twice), causing proportionally more objects to map to them.
- **Distributed k-agreement**: Selecting the top k sites from the weight ordering naturally extends to placing replicas or shares across k sites.
- **No precomputation or token storage**: Unlike consistent hashing, HRW requires no precomputed token rings, no metadata, and no sorted token lists.
- **Failure handling**: On site failure, the client simply picks the next-highest-weighted site. No global reorganization needed.

## Commands and Syntax

**Basic HRW algorithm (pseudocode)**:
```
function assign(object O, sites S[1..n]):
    for each site S[j]:
        w[j] = hash(O, S[j])
    return site S[j] with max w[j]
```

**For k-way replication**:
```
function assign_k(object O, sites S[1..n], k):
    for each site S[j]:
        w[j] = hash(O, S[j])
    return top-k sites by w[j]
```

**Hierarchical (skeleton) variant for O(log n)**:
1. Choose constant cluster size m; organize n sites into ceil(n/m) clusters.
2. Build a virtual tree with fanout f over the clusters.
3. At each tree level, apply HRW to the f children of the current node.
4. Descend into the winning branch; at the leaf cluster, apply HRW to the m real nodes.
5. Total hashes: O(f * log_f(n/m) + m) = O(log n) since m and f are constants.

**Capacity weighting**:
```
# Site S_k has 2x capacity — list it twice
sites = [S1, S2, S3, S_k_1, S_k_2, S5, ...]
```

## Relationships

- **Consistent hashing**: Rendezvous hashing is a strict generalization. Consistent hashing maps sites to tokens on a unit circle and uses clockwise traversal; HRW subsumes this by appropriate choice of a two-place hash function. Consistent hashing only handles k=1 natively.
- **Distributed hash tables (DHTs)**: HRW solves a general version of the DHT assignment problem.
- **Replication strategies**: HRW's ranked ordering of all sites per object provides a natural replication scheme — replicate to the top r sites.
- **Load balancing**: Uniform hash functions ensure even distribution; capacity-weighted variants handle heterogeneous clusters.
- **Sharding and partitioning**: Used in distributed databases (Apache Ignite, Apache Druid, IBM Cloud Object Store) to assign data partitions to nodes with minimal reshuffling on topology changes.

## Exam-Relevant Points

- **Time complexity**: Basic HRW is O(n) per lookup. Skeleton-based hierarchical variant achieves O(log n) by organizing sites into clusters and descending a virtual tree.
- **When a site is removed**: Only objects assigned to that site are remapped — all other assignments are untouched (minimal disruption guarantee).
- **When a site is added**: Only objects in the same leaf-level cluster need to be considered for remapping, not all objects in the system.
- **HRW vs consistent hashing trade-offs**: HRW is simpler (no tokens, no ring, no metadata), distributes more uniformly, and generalizes to k > 1. Consistent hashing can offer O(log n) lookup via binary search on sorted token lists but requires 100-200 tokens per site for reasonable balance.
- **Capacity handling differs**: HRW uses multiplicity in site list; consistent hashing uses proportional token counts.
- **Skeleton parameters**: Cluster size m trades off load balance under failure (higher m = better balance) vs search overhead (higher m = more hashes). Setting m = n degenerates to flat HRW.
- **Replication within skeleton**: Replicate across top-r sites within the leaf cluster. On failure, next-ranked site in the same cluster serves the object.
- **Real-world adopters**: GitHub load balancer, Apache Ignite, Apache Druid, Apache Kafka, Twitter EventBus, Tahoe-LAFS, IBM Cloud Object Store, Microsoft CARP.
