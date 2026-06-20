---
source: sources/wiki-Merkle_tree.md
source_url: https://en.wikipedia.org/wiki/Merkle_tree
---

## Merkle Trees (Hash Trees): Structure, Verification, and Applications

A Merkle tree (or hash tree) is a tree-based data structure in which every leaf node contains the cryptographic hash of a data block, and every internal node contains the hash of the concatenation of its children's hashes. This structure enables efficient and secure verification of large datasets by reducing the proof of membership to O(log n) hash computations. Invented by Ralph Merkle and patented in 1979, Merkle trees are foundational to distributed systems, version control, filesystems, and blockchain technologies.

## Key Concepts

- **Leaf nodes** are labelled with the cryptographic hash of a data block; **internal nodes** hash the concatenation of their children's labels.
- The **root hash** (top hash / master hash) serves as a single fingerprint for the entire dataset — a compact cryptographic commitment.
- **Membership proof** (Merkle proof): verifying that a leaf belongs to the tree requires only O(log n) hashes, compared to O(n) for a flat hash list.
- Merkle trees generalize both **hash lists** and **hash chains**.
- Most implementations are **binary** (two children per node), but arbitrary branching factors are possible.
- A cryptographic hash function (e.g., SHA-2) is typically used; non-cryptographic checksums (e.g., CRC) suffice when only detecting unintentional corruption.
- The root hash is obtained from a **trusted source**; the rest of the tree can be received from untrusted peers and verified against it.
- Individual **branches can be verified independently** without downloading the entire tree — this enables incremental download and verification in P2P systems.
- Merkle trees function as an efficient **cryptographic commitment scheme**: the root is the commitment, and leaf reveals constitute partial openings.
- **Anti-entropy repair** in distributed databases (Cassandra, Riak, Dynamo): replicas exchange Merkle trees to identify divergent key ranges, minimizing data transfer during synchronization.

## Commands and Syntax

No CLI commands per se, but the core algorithmic procedure:

```
# Verifying leaf L2 given root hash:
1. hash(L2) → hash_0_1
2. concatenate(hash_0_0, hash_0_1) → hash_0  
3. concatenate(hash_0, hash_1) → candidate_root
4. Compare candidate_root == trusted_root_hash
```

**Second preimage attack mitigation** (Certificate Transparency approach):
```
leaf_hash   = hash(0x00 || data_block)
internal_hash = hash(0x01 || left_child || right_child)
```
Prepending domain-separation bytes (0x00 for leaves, 0x01 for internal nodes) prevents an attacker from constructing a shorter tree whose root collides with the original.

**Tiger tree hash**: a specific instantiation using binary tree structure, 1024-byte data blocks, and the Tiger hash function. Used in Gnutella, Gnutella2, and Direct Connect P2P protocols.

## Relationships

- **Hash lists / hash chains**: Merkle trees generalize these; the tree structure provides logarithmic rather than linear verification cost.
- **Cryptographic hash functions** (SHA-2, Tiger): the building blocks for node labels.
- **P2P networks** (BitTorrent, IPFS, Gnutella): use Merkle trees to verify block integrity from untrusted peers.
- **Distributed version control** (Git, Mercurial): use Merkle DAGs (a generalization of Merkle trees using directed acyclic graphs) for content-addressable storage.
- **Blockchain** (Bitcoin, Ethereum): Merkle trees structure transactions within blocks, enabling lightweight SPV (Simplified Payment Verification) proofs.
- **Filesystems** (ZFS, OpenZFS): use Merkle trees for end-to-end data integrity and protection against bit rot.
- **NoSQL / distributed databases** (Cassandra, Riak, Dynamo): Merkle trees power anti-entropy protocols to efficiently synchronize replicas.
- **Certificate Transparency**: uses Merkle trees as append-only logs with efficient inclusion and consistency proofs.
- **Content-addressable storage** (Nix, GNU Guix, IPFS, Dat): content is identified and deduplicated by hash, with Merkle trees providing structural integrity.
- **Cryptographic commitment schemes**: the root hash commits to the entire dataset; individual leaves can be revealed with compact proofs.

## Exam-Relevant Points

- **Verification complexity**: proving a leaf is part of a Merkle tree requires O(log n) hashes; a hash list requires O(n). This logarithmic efficiency is the primary advantage.
- **Root hash trust model**: the root hash must come from a trusted source; all other tree data can be fetched from untrusted sources and verified.
- **Incremental verification**: unlike hash lists, individual branches can be checked before the full tree is available — critical for streaming/P2P scenarios.
- **Second preimage attack**: because the root hash does not encode tree depth, an attacker can forge a shorter tree with the same root. Mitigated by prepending 0x00 to leaf hashes and 0x01 to internal node hashes (the Certificate Transparency approach).
- **Anti-entropy in distributed databases**: Cassandra, Riak, and Dynamo use Merkle trees to compare replica state hierarchically, exchanging progressively finer-grained hashes until out-of-sync keys are isolated — this minimizes unnecessary data transfer.
- **Git uses a Merkle DAG, not strictly a Merkle tree** — it is a directed acyclic graph where objects reference their parents by hash.
- **Tiger tree hash**: binary tree, 1024-byte blocks, Tiger hash function — the standard for P2P file sharing protocols.
- **Named after Ralph Merkle**, patented in 1979 (US Patent 4,309,569).
