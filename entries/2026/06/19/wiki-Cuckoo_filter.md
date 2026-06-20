---
source: sources/wiki-Cuckoo_filter.md
source_url: https://en.wikipedia.org/wiki/Cuckoo_filter
---

## Cuckoo Filters: Space-Efficient Probabilistic Set Membership

Cuckoo filters are a probabilistic data structure introduced in 2014 that test whether an element belongs to a set. Like Bloom filters, they allow false positives but never false negatives. Their key advantage over Bloom filters is support for element deletion and, in many configurations, lower space overhead.

## Key Concepts

- **Probabilistic set membership**: queries return "possibly in set" or "definitely not in set" — never a false negative
- **Based on cuckoo hashing**: uses a hash table that stores only fingerprints (compact hashes) of items, not the items themselves
- **Two candidate buckets**: each item maps to exactly two buckets via h1(x) = hash(x) and h2(x) = h1(x) XOR hash(fingerprint(x))
- **XOR symmetry**: the alternate bucket can always be computed from the current bucket and the fingerprint alone — this is what makes cuckoo hashing of fingerprints possible
- **Bucket size b**: the table is divided into buckets of fixed size b; lookup and delete are O(b), which is constant in practice
- **Eviction on collision**: if both candidate buckets are full, an existing fingerprint is displaced to its alternate bucket (cuckoo-style), potentially cascading
- **Supports deletion**: unlike Bloom filters, items can be removed — but only items known to have been inserted
- **False positive rate**: bounded by epsilon <= b / 2^(f-1), where f is fingerprint size in bits
- **Minimum fingerprint size**: f must be at least Omega((log n) / b) bits for theoretical guarantees
- **Amortized O(1) insertion**: though individual insertions can fail and trigger rehashing
- **High table utilization**: load factor alpha can reach 95.5%

## Commands and Syntax

No CLI commands — this is a data structure specification. Key formulas:

- **Bucket computation**: h1(x) = hash(x); h2(x) = h1(x) XOR hash(fingerprint(x))
- **Space per key**: (log2(1/epsilon) + 1 + log2(b)) / alpha
- **Bloom filter space per key** (for comparison): 1.44 * log2(1/epsilon)
- **False positive bound**: epsilon <= b / 2^(f-1)
- **Lookup cost**: at most 2b memory accesses (check two buckets of size b)

## Relationships

- **Bloom filters**: the primary comparison point — cuckoo filters add deletion support and can be more space-efficient at moderate false positive rates, but Bloom filters support fast union/intersection via bitwise operations and degrade more gracefully under high load
- **Cuckoo hashing** (Pagh & Rodler, 2001): the underlying hash table strategy that enables two-choice placement and eviction chains
- **Fingerprinting**: compact hash representations that make the structure space-efficient — only fingerprints are stored, not full keys
- **Hash tables**: cuckoo filters are fundamentally a specialized hash table optimized for membership queries
- **Quotient filters, counting Bloom filters**: other probabilistic structures that support deletion (related design space)

## Exam-Relevant Points

- Cuckoo filters support deletion; standard Bloom filters do not — this is the most frequently tested differentiator
- False negatives are impossible; false positives are possible (same guarantee as Bloom filters)
- The XOR-based bucket computation is essential: it allows computing the alternate bucket from any bucket plus the fingerprint, without needing the original item
- Space advantage over Bloom filters depends on the target false positive rate — cuckoo filters win at moderately low rates
- Bloom filters offer bitwise union/intersection; cuckoo filters do not
- Insertion can fail when the table is too full, requiring rehashing — but amortized insertion is still O(1)
- You can only delete items known to have been inserted; deleting a non-member can corrupt the filter
- Load factor can reach 95.5%, meaning cuckoo filters achieve high space utilization
- Information-theoretic lower bound for any such structure is log2(1/epsilon) bits per item — both Bloom and cuckoo filters approach but don't reach this
