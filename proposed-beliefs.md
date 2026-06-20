# Proposed Beliefs

Review each entry: change `[ACCEPT]` to `[ACCEPT]` to keep, or vice versa.
Then run: `expert-build accept-beliefs`

---

**Generated:** 2026-06-19
**Source:** 123 entries from entries/
**Model:** claude

### [ACCEPT] acid-acronym-coined-1983
The ACID acronym was coined in 1983 by Andreas Reuter and Theo Härder, building on Jim Gray's earlier work on atomicity, consistency, and durability
- Source: entries/2026/06/19/wiki-ACID.md
- Source URL: https://en.wikipedia.org/wiki/ACID

### [ACCEPT] acid-atomicity-all-or-nothing
Atomicity guarantees a transaction is indivisible — it either succeeds completely or fails completely with no partial updates visible
- Source: entries/2026/06/19/wiki-ACID.md
- Source URL: https://en.wikipedia.org/wiki/ACID

### [ACCEPT] acid-consistency-valid-state-transitions
Consistency guarantees a transaction can only bring the database from one valid state to another, preserving all defined rules including constraints, cascades, triggers, and referential integrity
- Source: entries/2026/06/19/wiki-ACID.md
- Source URL: https://en.wikipedia.org/wiki/ACID

### [ACCEPT] acid-isolation-serializable-equivalence
Isolation guarantees that concurrent transactions produce the same result as if they were executed sequentially
- Source: entries/2026/06/19/wiki-ACID.md
- Source URL: https://en.wikipedia.org/wiki/ACID

### [ACCEPT] acid-durability-survives-failures
Durability guarantees that once a transaction is committed, its effects persist even through system failures such as power outages and crashes, achieved by writing to non-volatile memory
- Source: entries/2026/06/19/wiki-ACID.md
- Source URL: https://en.wikipedia.org/wiki/ACID

### [ACCEPT] wal-durability-technique
Write-Ahead Logging (WAL) achieves durability by writing prospective changes to a persistent log before modifying the database, enabling crash recovery
- Source: entries/2026/06/19/wiki-ACID.md
- Source URL: https://en.wikipedia.org/wiki/ACID

### [ACCEPT] shadow-paging-durability-alternative
Shadow paging is an alternative durability technique to WAL where updates are applied to a partial copy of the database and the new copy is activated atomically on commit
- Source: entries/2026/06/19/wiki-ACID.md
- Source URL: https://en.wikipedia.org/wiki/ACID

### [ACCEPT] mvcc-readers-dont-block-writers
Multiversion Concurrency Control (MVCC) allows readers to see a prior consistent snapshot while writers modify data, so readers do not block writers and vice versa
- Source: entries/2026/06/19/wiki-ACID.md
- Source URL: https://en.wikipedia.org/wiki/ACID

### [ACCEPT] two-phase-commit-vs-two-phase-locking
Two-phase commit (2PC) is a distributed transaction protocol ensuring atomicity across multiple nodes, distinct from two-phase locking (2PL) which is a concurrency control protocol ensuring isolation
- Source: entries/2026/06/19/wiki-ACID.md
- Source URL: https://en.wikipedia.org/wiki/ACID

### [ACCEPT] base-availability-over-consistency
BASE (Basically Available, Soft state, Eventually consistent) prioritizes availability over consistency, conceptually opposite to ACID which prioritizes consistency over availability
- Source: entries/2026/06/19/wiki-ACID.md
- Source URL: https://en.wikipedia.org/wiki/ACID

### [ACCEPT] ibm-ims-acid-1973
IBM IMS supported ACID transactions as early as 1973, predating the ACID acronym by a decade
- Source: entries/2026/06/19/wiki-ACID.md
- Source URL: https://en.wikipedia.org/wiki/ACID

### [ACCEPT] adt-defined-by-behavior-not-implementation
An abstract data type (ADT) is defined entirely by its behavior — possible values, operations, and constraints — rather than by its concrete representation or implementation
- Source: entries/2026/06/19/wiki-Abstract_data_type.md
- Source URL: https://en.wikipedia.org/wiki/Abstract_data_type

### [ACCEPT] adt-two-specification-styles
ADTs have two formal specification styles: axiomatic semantics (functional, pure, order-independent with algebraic laws) and operational semantics (imperative, mutable, order-dependent)
- Source: entries/2026/06/19/wiki-Abstract_data_type.md
- Source URL: https://en.wikipedia.org/wiki/Abstract_data_type

### [ACCEPT] adt-introduced-liskov-zilles-1974
Abstract data types were first proposed by Barbara Liskov and Stephen Zilles in 1974 during CLU language development
- Source: entries/2026/06/19/wiki-Abstract_data_type.md
- Source URL: https://en.wikipedia.org/wiki/Abstract_data_type

### [ACCEPT] adt-stack-canonical-axiom
The canonical axiom for an abstract stack is pop(push(S, v)) = (S, v), meaning pop undoes push
- Source: entries/2026/06/19/wiki-Abstract_data_type.md
- Source URL: https://en.wikipedia.org/wiki/Abstract_data_type

### [ACCEPT] boom-hierarchy-algebraic-properties
The Boom hierarchy shows how adding algebraic properties transforms data types: identity yields trees, adding associativity yields lists, adding commutativity yields bags, adding idempotence yields sets
- Source: entries/2026/06/19/wiki-Abstract_data_type.md
- Source URL: https://en.wikipedia.org/wiki/Abstract_data_type

### [ACCEPT] akamai-founded-on-consistent-hashing
Akamai Technologies was founded in 1998 based on consistent hashing research from MIT, published in 1997 by Karger, Lewin, Leighton et al.
- Source: entries/2026/06/19/wiki-Akamai_Technologies.md
- Source URL: https://en.wikipedia.org/wiki/Akamai_Technologies

### [ACCEPT] akamai-365k-servers-135-countries
Akamai operates approximately 365,000 servers across 135+ countries on roughly 1,350 networks worldwide
- Source: entries/2026/06/19/wiki-Akamai_Technologies.md
- Source URL: https://en.wikipedia.org/wiki/Akamai_Technologies

### [ACCEPT] akamai-dns-based-request-routing
Akamai uses DNS-based request routing to direct users to the nearest edge server, not centralized load balancers — the mapping system translates domain names to edge server IPs based on content type and user location
- Source: entries/2026/06/19/wiki-Akamai_Technologies.md
- Source URL: https://en.wikipedia.org/wiki/Akamai_Technologies

### [ACCEPT] consistent-hashing-minimizes-redistribution
Consistent hashing maps content to servers in a way that minimizes redistribution when servers join or leave the cluster, enabling distributed caching
- Source: entries/2026/06/19/wiki-Akamai_Technologies.md
- Source URL: https://en.wikipedia.org/wiki/Akamai_Technologies

### [ACCEPT] amortized-analysis-introduced-tarjan-1985
Amortized analysis was introduced by Robert Tarjan in 1985, originally motivated by binary trees and union-find data structures
- Source: entries/2026/06/19/wiki-Amortized_analysis.md
- Source URL: https://en.wikipedia.org/wiki/Amortized_analysis

### [ACCEPT] amortized-analysis-not-average-case
Amortized analysis is a worst-case technique that makes no assumptions about input distribution, unlike average-case analysis which assumes a distribution over inputs
- Source: entries/2026/06/19/wiki-Amortized_analysis.md
- Source URL: https://en.wikipedia.org/wiki/Amortized_analysis

### [ACCEPT] amortized-analysis-three-methods
The three methods for amortized analysis — aggregate (T(n)/n), accounting (save/spend credit), and potential (amortized = actual + ΔΦ) — are equivalent in power
- Source: entries/2026/06/19/wiki-Amortized_analysis.md
- Source URL: https://en.wikipedia.org/wiki/Amortized_analysis

### [ACCEPT] dynamic-array-append-amortized-o1
Dynamic array append (e.g., ArrayList, std::vector) has amortized O(1) cost per insertion despite individual resizes being O(n), because resize costs form a geometric series summing to O(n) over n pushes
- Source: entries/2026/06/19/wiki-Amortized_analysis.md
- Source URL: https://en.wikipedia.org/wiki/Amortized_analysis

### [ACCEPT] two-stack-queue-amortized-o1
A queue implemented with two stacks achieves amortized O(1) for both enqueue and dequeue, because each element is moved from input stack to output stack exactly once
- Source: entries/2026/06/19/wiki-Amortized_analysis.md
- Source URL: https://en.wikipedia.org/wiki/Amortized_analysis

### [ACCEPT] accounting-method-credit-nonnegative-invariant
The accounting method for amortized analysis requires accumulated credit to remain non-negative at all times — this invariant is what guarantees the amortized cost is an upper bound on actual cost
- Source: entries/2026/06/19/wiki-Amortized_analysis.md
- Source URL: https://en.wikipedia.org/wiki/Amortized_analysis

### [ACCEPT] arxiv-founded-1991-ginsparg
arXiv was founded on August 14, 1991 by Paul Ginsparg at Los Alamos National Laboratory
- Source: entries/2026/06/19/wiki-ArXiv_identifier.md
- Source URL: https://en.wikipedia.org/wiki/ArXiv_(identifier)

### [ACCEPT] arxiv-moved-cornell-2001
arXiv moved from Los Alamos National Laboratory to Cornell University in 2001
- Source: entries/2026/06/19/wiki-ArXiv_identifier.md
- Source URL: https://en.wikipedia.org/wiki/ArXiv_(identifier)

### [ACCEPT] arxiv-moderated-not-peer-reviewed
arXiv content is moderated by area moderators and automated screening but is not peer reviewed
- Source: entries/2026/06/19/wiki-ArXiv_identifier.md
- Source URL: https://en.wikipedia.org/wiki/ArXiv_(identifier)

### [ACCEPT] arxiv-endorsement-system-2004
arXiv introduced an endorsement system in 2004 requiring new authors to be endorsed by established contributors; authors from recognized academic institutions receive automatic endorsement
- Source: entries/2026/06/19/wiki-ArXiv_identifier.md
- Source URL: https://en.wikipedia.org/wiki/ArXiv_(identifier)

### [ACCEPT] arxiv-identifier-format-yymm-nnnnn
Modern arXiv paper identifiers follow the format YYMM.NNNNN (e.g., 1507.00123) with optional version suffix vN; legacy format is arch-ive/YYMMNNN (e.g., hep-th/9901001)
- Source: entries/2026/06/19/wiki-ArXiv_identifier.md
- Source URL: https://en.wikipedia.org/wiki/ArXiv_(identifier)

### [ACCEPT] arxiv-metadata-oai-pmh
arXiv metadata is exposed via the OAI-PMH protocol, the standard protocol for open access repositories
- Source: entries/2026/06/19/wiki-ArXiv_identifier.md
- Source URL: https://en.wikipedia.org/wiki/ArXiv_(identifier)

### [ACCEPT] arxiv-dois-since-2022-datacite
arXiv has automatically assigned DOIs to articles since January 2022, in collaboration with DataCite
- Source: entries/2026/06/19/wiki-ArXiv_identifier.md
- Source URL: https://en.wikipedia.org/wiki/ArXiv_(identifier)

### [ACCEPT] argon2-won-2015-phc
Argon2 won the 2015 Password Hashing Competition and is standardized in RFC 9106 (September 2021)
- Source: entries/2026/06/19/wiki-Argon2.md
- Source URL: https://en.wikipedia.org/wiki/Argon2

### [ACCEPT] argon2id-recommended-variant
RFC 9106 recommends Argon2id as the default variant; it uses Argon2i (password-independent memory access) for the first half-pass, then Argon2d (password-dependent) for subsequent passes
- Source: entries/2026/06/19/wiki-Argon2.md
- Source URL: https://en.wikipedia.org/wiki/Argon2

### [ACCEPT] argon2-three-tunable-params
Argon2 has three tunable parameters: execution time (iterations), memory required (memorySizeKB), and degree of parallelism (threads)
- Source: entries/2026/06/19/wiki-Argon2.md
- Source URL: https://en.wikipedia.org/wiki/Argon2

### [ACCEPT] argon2-uses-blake2b-internally
Argon2 uses BLAKE2b for all internal hashing including initial hash, block generation, and variable-length output
- Source: entries/2026/06/19/wiki-Argon2.md
- Source URL: https://en.wikipedia.org/wiki/Argon2

### [ACCEPT] argon2-rfc9106-recommended-minimums
RFC 9106 recommends minimum parameters of 2 GiB memory with 1 iteration and parallelism 4 (default), or 64 MiB memory with 3 iterations and parallelism 4 (memory-constrained)
- Source: entries/2026/06/19/wiki-Argon2.md
- Source URL: https://en.wikipedia.org/wiki/Argon2

### [ACCEPT] argon2d-resists-gpu-vulnerable-sidechannel
Argon2d uses password-dependent memory access to maximize GPU/TMTO cracking resistance but is vulnerable to side-channel attacks; Argon2i uses password-independent access to resist side-channel attacks but is weaker against TMTO
- Source: entries/2026/06/19/wiki-Argon2.md
- Source URL: https://en.wikipedia.org/wiki/Argon2

### [ACCEPT] array-constant-time-element-access
Array element access (read/write by index) is O(1) worst-case, computed via the formula address = base + stride * index
- Source: entries/2026/06/19/wiki-Array_data_structure.md
- Source URL: https://en.wikipedia.org/wiki/Array_data_structure

### [ACCEPT] array-row-major-vs-column-major
Row-major order (C, C++) stores elements of each row contiguously with the last index varying fastest; column-major order (Fortran) stores elements of each column contiguously with the first index varying fastest
- Source: entries/2026/06/19/wiki-Array_data_structure.md
- Source URL: https://en.wikipedia.org/wiki/Array_data_structure

### [ACCEPT] array-dope-vector-descriptor
A dope vector (descriptor/stride vector) is a record packing dimension count, base address, and per-dimension increments that serves as a complete handle for an array and enables efficient slicing
- Source: entries/2026/06/19/wiki-Array_data_structure.md
- Source URL: https://en.wikipedia.org/wiki/Array_data_structure

### [ACCEPT] iliffe-vector-pointer-array
An Iliffe vector is an alternative to true multidimensional arrays that uses an array of pointers to sub-arrays, enabling jagged arrays where rows can differ in size
- Source: entries/2026/06/19/wiki-Array_data_structure.md
- Source URL: https://en.wikipedia.org/wiki/Array_data_structure

### [ACCEPT] hashed-array-tree-sqrt-n-overhead
Hashed array trees achieve O(1) amortized append with only O(sqrt(n)) excess space, better than dynamic arrays' O(n) excess space
- Source: entries/2026/06/19/wiki-Array_data_structure.md
- Source URL: https://en.wikipedia.org/wiki/Array_data_structure

### [ACCEPT] assoc-array-hashtable-avg-o1-worst-on
Hash tables provide average O(1) for lookup, insert, and remove but degrade to O(n) in the worst case; self-balancing BSTs guarantee O(log n) for all operations in all cases
- Source: entries/2026/06/19/wiki-Associative_array.md
- Source URL: https://en.wikipedia.org/wiki/Associative_array

### [ACCEPT] open-addressing-vs-separate-chaining
Open addressing has better cache performance than separate chaining when the hash table is mostly empty but degrades exponentially as load increases; separate chaining uses less memory unless entries are very small (< 4x pointer size)
- Source: entries/2026/06/19/wiki-Associative_array.md
- Source URL: https://en.wikipedia.org/wiki/Associative_array

### [ACCEPT] python-dict-insertion-order-cpp-map-sorted
Python dicts and Java LinkedHashMap preserve insertion order; C++ std::map preserves sorted key order — these are distinct ordered-dictionary semantics
- Source: entries/2026/06/19/wiki-Associative_array.md
- Source URL: https://en.wikipedia.org/wiki/Associative_array

### [ACCEPT] trees-support-range-queries-hashtables-do-not
Tree-based associative array implementations support range queries and ordered traversal; hash table implementations do not
- Source: entries/2026/06/19/wiki-Associative_array.md
- Source URL: https://en.wikipedia.org/wiki/Associative_array

### [ACCEPT] asymmetric-equals-antisymmetric-plus-irreflexive
A binary relation is asymmetric if and only if it is both antisymmetric and irreflexive; this equivalence is both necessary and sufficient
- Source: entries/2026/06/19/wiki-Asymmetric_relation.md
- Source URL: https://en.wikipedia.org/wiki/Asymmetric_relation

### [ACCEPT] transitive-relation-asymmetric-iff-irreflexive
For transitive relations, asymmetry and irreflexivity are equivalent: a transitive relation is asymmetric if and only if it is irreflexive
- Source: entries/2026/06/19/wiki-Asymmetric_relation.md
- Source URL: https://en.wikipedia.org/wiki/Asymmetric_relation

### [ACCEPT] asymmetric-not-same-as-not-symmetric
Asymmetric and 'not symmetric' are distinct properties; the <= relation is neither symmetric nor asymmetric, and the empty relation is the only relation that is both symmetric and asymmetric
- Source: entries/2026/06/19/wiki-Asymmetric_relation.md
- Source URL: https://en.wikipedia.org/wiki/Asymmetric_relation

### [ACCEPT] strict-orders-asymmetric-nonstrict-not
Strict partial orders (irreflexive + transitive) are always asymmetric; non-strict partial orders (reflexive + antisymmetric + transitive) are not asymmetric because they are reflexive
- Source: entries/2026/06/19/wiki-Asymmetric_relation.md
- Source URL: https://en.wikipedia.org/wiki/Asymmetric_relation

### [ACCEPT] avro-row-oriented-serialization
Apache Avro is a row-oriented data serialization format, in contrast to column-oriented formats like Parquet and ORC
- Source: entries/2026/06/19/wiki-Apache_Avro.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Avro

### [ACCEPT] avro-no-code-generation-required
Avro does not require a code-generation step when schemas change, unlike Thrift and Protocol Buffers
- Source: entries/2026/06/19/wiki-Apache_Avro.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Avro

### [ACCEPT] avro-schema-json-data-binary
Avro schemas are defined in JSON (or Avro IDL) while data is serialized in a compact binary format by default
- Source: entries/2026/06/19/wiki-Apache_Avro.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Avro

### [ACCEPT] avro-object-container-files-self-describing
Avro Object Container Files embed the writer's schema in the file header, making them self-describing
- Source: entries/2026/06/19/wiki-Apache_Avro.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Avro

### [ACCEPT] avro-file-header-magic-bytes
Avro Object Container File headers begin with magic bytes 'Obj' followed by version 1 (hex: 4F 62 6A 01)
- Source: entries/2026/06/19/wiki-Apache_Avro.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Avro

### [ACCEPT] avro-sync-marker-enables-splitting
The 16-byte sync marker in Avro file headers enables splitting large files for parallel processing in MapReduce
- Source: entries/2026/06/19/wiki-Apache_Avro.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Avro

### [ACCEPT] avro-union-types-for-nullable-fields
Avro uses union types (e.g., ["null", "int"]) as the mechanism for expressing nullable/optional fields
- Source: entries/2026/06/19/wiki-Apache_Avro.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Avro

### [ACCEPT] avro-supports-serialization-and-rpc
Avro supports both data serialization (persistent storage) and RPC (wire protocol for inter-node communication)
- Source: entries/2026/06/19/wiki-Apache_Avro.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Avro

### [ACCEPT] cassandra-ap-system-cap-theorem
Apache Cassandra is an AP system under the CAP theorem, prioritizing availability and partition tolerance over strong consistency
- Source: entries/2026/06/19/wiki-Apache_Cassandra.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Cassandra

### [ACCEPT] cassandra-masterless-architecture
Cassandra uses a masterless architecture where all nodes perform identical functions with no single point of failure
- Source: entries/2026/06/19/wiki-Apache_Cassandra.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Cassandra

### [ACCEPT] cassandra-lsm-tree-storage
Cassandra uses Log-Structured Merge Trees (LSM trees) for storage, not B-trees, optimizing for write throughput via append-only operations
- Source: entries/2026/06/19/wiki-Apache_Cassandra.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Cassandra

### [ACCEPT] cassandra-write-path-commitlog-memtable-sstable
Cassandra's write path is: write to commit log + memtable, then flush to SSTable when threshold is reached
- Source: entries/2026/06/19/wiki-Apache_Cassandra.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Cassandra

### [ACCEPT] cassandra-deletes-use-tombstones
Cassandra uses tombstones for deletes rather than direct removal, which can cause performance issues in delete-heavy workloads
- Source: entries/2026/06/19/wiki-Apache_Cassandra.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Cassandra

### [ACCEPT] cassandra-gossip-protocol-cluster-communication
Cassandra uses a gossip protocol for peer-to-peer cluster communication and seed nodes to bootstrap the cluster
- Source: entries/2026/06/19/wiki-Apache_Cassandra.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Cassandra

### [ACCEPT] cassandra-phi-accrual-failure-detector
Cassandra uses the Phi Accrual Failure Detector for probabilistic node failure detection rather than binary alive/dead determination
- Source: entries/2026/06/19/wiki-Apache_Cassandra.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Cassandra

### [ACCEPT] cassandra-combines-dynamo-and-bigtable
Cassandra combines Amazon Dynamo's distributed storage and replication techniques with Google Bigtable's data storage engine model
- Source: entries/2026/06/19/wiki-Apache_Cassandra.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Cassandra

### [ACCEPT] cassandra-denormalized-no-joins
Cassandra's data model is denormalized with no JOINs or ad hoc aggregations; schema must be designed around known access patterns
- Source: entries/2026/06/19/wiki-Apache_Cassandra.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Cassandra

### [ACCEPT] cassandra-hinted-handoff-mechanism
Cassandra uses hinted handoff where the coordinator stores writes destined for offline nodes as hints and replays them when the node returns
- Source: entries/2026/06/19/wiki-Apache_Cassandra.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Cassandra

### [ACCEPT] hbase-cp-system-cap-theorem
Apache HBase is a CP system under the CAP theorem, favoring consistency and partition tolerance over availability
- Source: entries/2026/06/19/wiki-Apache_HBase.md
- Source URL: https://en.wikipedia.org/wiki/Apache_HBase

### [ACCEPT] hbase-modeled-after-google-bigtable
Apache HBase is the open-source implementation of the Google Bigtable data model
- Source: entries/2026/06/19/wiki-Apache_HBase.md
- Source URL: https://en.wikipedia.org/wiki/Apache_HBase

### [ACCEPT] hbase-runs-on-hdfs
HBase runs on top of HDFS (Hadoop Distributed File System) as part of the Apache Hadoop ecosystem
- Source: entries/2026/06/19/wiki-Apache_HBase.md
- Source URL: https://en.wikipedia.org/wiki/Apache_HBase

### [ACCEPT] hbase-no-native-sql
HBase does not support SQL natively; Apache Phoenix or Apache Trafodion are needed for SQL access over HBase
- Source: entries/2026/06/19/wiki-Apache_HBase.md
- Source URL: https://en.wikipedia.org/wiki/Apache_HBase

### [ACCEPT] hbase-per-column-bloom-filters-compression
HBase supports Bloom filters, compression, and in-memory operation configured on a per-column basis
- Source: entries/2026/06/19/wiki-Apache_HBase.md
- Source URL: https://en.wikipedia.org/wiki/Apache_HBase

### [ACCEPT] hbase-tables-mapreduce-input-output
HBase tables can serve as both input and output for Hadoop MapReduce jobs
- Source: entries/2026/06/19/wiki-Apache_HBase.md
- Source URL: https://en.wikipedia.org/wiki/Apache_HBase

### [ACCEPT] facebook-migrated-hbase-to-myrocks-2018
Facebook adopted HBase for messaging in 2010 but migrated to MyRocks in 2018
- Source: entries/2026/06/19/wiki-Apache_HBase.md
- Source URL: https://en.wikipedia.org/wiki/Apache_HBase

### [ACCEPT] kafka-ordering-within-partition-only
Kafka guarantees message ordering within a partition, not across an entire topic
- Source: entries/2026/06/19/wiki-Apache_Kafka.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Kafka

### [ACCEPT] kafka-retains-messages-after-consumption
Kafka retains messages in a durable append-only log after consumption, unlike traditional queues that delete messages on acknowledgment
- Source: entries/2026/06/19/wiki-Apache_Kafka.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Kafka

### [ACCEPT] kafka-consumers-manual-offset-management
Kafka consumers control their own retry and failure handling by manually deciding when to commit offsets
- Source: entries/2026/06/19/wiki-Apache_Kafka.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Kafka

### [ACCEPT] kafka-streams-uses-rocksdb-local-state
Kafka Streams uses RocksDB for local state storage and replicates state changes to a changelog topic for fault tolerance
- Source: entries/2026/06/19/wiki-Apache_Kafka.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Kafka

### [ACCEPT] kafka-share-groups-kip-932
Kafka share groups (KIP-932) add queue-like semantics where consumers can exceed partition count with individual message acknowledgment
- Source: entries/2026/06/19/wiki-Apache_Kafka.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Kafka

### [ACCEPT] kafka-binary-tcp-protocol-message-sets
Kafka uses a binary TCP-based protocol that batches messages into message sets to reduce network overhead and enable sequential disk writes
- Source: entries/2026/06/19/wiki-Apache_Kafka.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Kafka

### [ACCEPT] kafka-connect-uses-producer-consumer-apis
Kafka Connect uses Producer and Consumer APIs internally; it is a framework layer, not a separate protocol
- Source: entries/2026/06/19/wiki-Apache_Kafka.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Kafka

### [ACCEPT] google-wave-used-operational-transformation
Google Wave used Operational Transformation (OT) for concurrent editing, not CRDTs
- Source: entries/2026/06/19/wiki-Apache_Wave.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Wave

### [ACCEPT] wave-federation-protocol-xmpp-extension
The Wave Federation Protocol was built as an XMPP extension, with the originating server responsible for hosting, processing, and concurrency control
- Source: entries/2026/06/19/wiki-Apache_Wave.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Wave

### [ACCEPT] wave-retired-2018-never-left-incubator
Apache Wave was retired in January 2018 without ever leaving Apache incubator status
- Source: entries/2026/06/19/wiki-Apache_Wave.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Wave

### [ACCEPT] cassandra-vs-hbase-ap-vs-cp
Cassandra is an AP system and HBase is a CP system under the CAP theorem, representing opposite trade-offs among wide-column stores
- Source: entries/2026/06/19/wiki-Apache_Cassandra.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Cassandra

### [ACCEPT] cassandra-read-path-memtable-then-sstables-bloom-filters
Cassandra's read path checks the memtable first, then searches SSTables newest-to-oldest using Bloom filters
- Source: entries/2026/06/19/wiki-Apache_Cassandra.md
- Source URL: https://en.wikipedia.org/wiki/Apache_Cassandra

### [ACCEPT] atomic-broadcast-equals-total-order-broadcast
Atomic broadcast and total order broadcast are the same primitive: all correct processes deliver the same messages in the same sequence.
- Source: entries/2026/06/19/wiki-Atomic_broadcast.md
- Source URL: https://en.wikipedia.org/wiki/Atomic_broadcast

### [ACCEPT] atomic-broadcast-four-properties
Atomic broadcast requires four properties: Validity, Uniform Agreement, Uniform Integrity, and Uniform Total Order.
- Source: entries/2026/06/19/wiki-Atomic_broadcast.md
- Source URL: https://en.wikipedia.org/wiki/Atomic_broadcast

### [ACCEPT] total-order-not-fifo-not-causal
Total order, FIFO order, and causal order are distinct ordering guarantees that neither imply nor are implied by each other.
- Source: entries/2026/06/19/wiki-Atomic_broadcast.md
- Source URL: https://en.wikipedia.org/wiki/Atomic_broadcast

### [ACCEPT] atomic-broadcast-equivalent-to-consensus
In crash-failure models, atomic broadcast and consensus are equivalent — each is reducible to the other (Chandra and Toueg, 1996).
- Source: entries/2026/06/19/wiki-Atomic_broadcast.md
- Source URL: https://en.wikipedia.org/wiki/Atomic_broadcast

### [ACCEPT] flp-impossibility-applies-to-atomic-broadcast
The FLP impossibility result (Fischer, Lynch, Paterson, 1985) applies to atomic broadcast because atomic broadcast is equivalent to consensus, making it impossible to guarantee in a purely asynchronous system with even one crash failure.
- Source: entries/2026/06/19/wiki-Atomic_broadcast.md
- Source URL: https://en.wikipedia.org/wiki/Atomic_broadcast

### [ACCEPT] zab-underlies-zookeeper
ZAB (ZooKeeper Atomic Broadcast) is the protocol underlying Apache ZooKeeper, providing atomic broadcast for distributed coordination.
- Source: entries/2026/06/19/wiki-Atomic_broadcast.md
- Source URL: https://en.wikipedia.org/wiki/Atomic_broadcast

### [ACCEPT] consensus-to-atomic-broadcast-reduction
Consensus reduces to atomic broadcast by broadcasting proposed values and deciding on the first message delivered; atomic broadcast reduces to consensus by agreeing on messages one at a time via repeated consensus rounds.
- Source: entries/2026/06/19/wiki-Atomic_broadcast.md
- Source URL: https://en.wikipedia.org/wiki/Atomic_broadcast

### [ACCEPT] atomicity-is-acid-a
Atomicity is the 'A' in ACID, guaranteeing that a database transaction either completes entirely or has no effect at all.
- Source: entries/2026/06/19/wiki-Atomicity_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Atomicity_(database_systems)

### [ACCEPT] atomicity-not-orthogonal-to-isolation-consistency
Atomicity is not orthogonal to isolation and consistency — both isolation (rollback on deadlock) and consistency (rollback on constraint violation) depend on atomicity's rollback capability.
- Source: entries/2026/06/19/wiki-Atomicity_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Atomicity_(database_systems)

### [ACCEPT] databases-implement-atomicity-via-wal
Databases implement atomicity via write-ahead logs; file systems use journaling or read-copy-update (RCU).
- Source: entries/2026/06/19/wiki-Atomicity_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Atomicity_(database_systems)

### [ACCEPT] distributed-atomicity-2pc-bottleneck
Two-Phase Commit (2PC) provides distributed atomicity across shards but introduces performance bottlenecks due to global transaction ordering.
- Source: entries/2026/06/19/wiki-Atomicity_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Atomicity_(database_systems)

### [ACCEPT] hardware-atomic-ops-cas-testandset-fetchandadd-llsc
Hardware-level atomic operations include Test-and-set, Fetch-and-add, Compare-and-swap (CAS), and Load-Link/Store-Conditional (LL/SC), used together with memory barriers.
- Source: entries/2026/06/19/wiki-Atomicity_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Atomicity_(database_systems)

### [ACCEPT] 1nf-atomicity-differs-from-transaction-atomicity
First Normal Form (1NF) 'atomicity' means field values must not contain decomposable sub-values, which is a different concept from transaction atomicity (all-or-nothing execution).
- Source: entries/2026/06/19/wiki-Atomicity_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Atomicity_(database_systems)

### [ACCEPT] btree-invented-1970-bayer-mccreight
The B-tree was invented in 1970 by Rudolf Bayer and Edward McCreight at Boeing Research Labs.
- Source: entries/2026/06/19/wiki-B-tree.md
- Source URL: https://en.wikipedia.org/wiki/B-tree

### [ACCEPT] btree-all-operations-ologn
All B-tree operations (search, insert, delete) run in O(log n) time, both amortized and worst case.
- Source: entries/2026/06/19/wiki-B-tree.md
- Source URL: https://en.wikipedia.org/wiki/B-tree

### [ACCEPT] btree-all-leaves-same-depth
In a B-tree, all leaf nodes are always at the same depth; tree height changes only when the root splits or merges.
- Source: entries/2026/06/19/wiki-B-tree.md
- Source URL: https://en.wikipedia.org/wiki/B-tree

### [ACCEPT] btree-knuth-order-m-max-children
Knuth's definition of B-tree order m is the maximum number of children any node may have; maximum keys per node = m−1; minimum children for non-root internal nodes = ⌈m/2⌉.
- Source: entries/2026/06/19/wiki-B-tree.md
- Source URL: https://en.wikipedia.org/wiki/B-tree

### [ACCEPT] btree-disk-advantage-logb-vs-log2
B-trees reduce disk reads from log₂ N (binary search) to log_b N (where b is the blocking factor) by packing many keys per node sized to match a disk block.
- Source: entries/2026/06/19/wiki-B-tree.md
- Source URL: https://en.wikipedia.org/wiki/B-tree

### [ACCEPT] bplus-tree-data-pointers-at-leaves-only
B+ trees store all data/record pointers in leaf nodes only; internal nodes hold only keys and child pointers, enabling higher fan-out than standard B-trees.
- Source: entries/2026/06/19/wiki-B-tree.md
- Source URL: https://en.wikipedia.org/wiki/B-tree

### [ACCEPT] bstar-tree-two-thirds-occupancy
B* trees require nodes to be at least 2/3 full (vs. 1/2 for standard B-trees), using sibling redistribution to delay splits.
- Source: entries/2026/06/19/wiki-B-tree.md
- Source URL: https://en.wikipedia.org/wiki/B-tree

### [ACCEPT] btree-standard-index-in-relational-databases
B-tree is the standard index implementation in virtually all relational databases including PostgreSQL, MySQL/InnoDB, SQLite, Oracle, and SQL Server.
- Source: entries/2026/06/19/wiki-B-tree.md
- Source URL: https://en.wikipedia.org/wiki/B-tree

### [ACCEPT] bitcask-append-only-with-inmemory-hashtable
Bitcask combines an append-only log-structured file on disk with an in-memory hash table that maps every key to its on-disk byte offset.
- Source: entries/2026/06/19/wiki-Bitcask.md
- Source URL: https://en.wikipedia.org/wiki/Bitcask

### [ACCEPT] bitcask-single-disk-seek-per-read
Bitcask requires at most one disk seek per read because the in-memory hash table gives the exact on-disk location of the value.
- Source: entries/2026/06/19/wiki-Bitcask.md
- Source URL: https://en.wikipedia.org/wiki/Bitcask

### [ACCEPT] bitcask-all-keys-must-fit-in-ram
Bitcask requires the entire keyspace to fit in memory — this is its primary capacity limitation.
- Source: entries/2026/06/19/wiki-Bitcask.md
- Source URL: https://en.wikipedia.org/wiki/Bitcask

### [ACCEPT] bitcask-developed-by-basho-for-riak
Bitcask was developed by Basho Technologies as the default storage backend for Riak KV.
- Source: entries/2026/06/19/wiki-Bitcask.md
- Source URL: https://en.wikipedia.org/wiki/Bitcask

### [ACCEPT] bitcask-data-file-is-the-wal
In Bitcask, the data file effectively is the write-ahead log — there is no separate log and data store.
- Source: entries/2026/06/19/wiki-Bitcask.md
- Source URL: https://en.wikipedia.org/wiki/Bitcask

### [ACCEPT] bitcask-compaction-required-for-disk-reclamation
Bitcask requires periodic compaction/merging of old log files to reclaim disk space from overwritten or deleted keys; without it, disk usage grows without bound.
- Source: entries/2026/06/19/wiki-Bitcask.md
- Source URL: https://en.wikipedia.org/wiki/Bitcask

### [ACCEPT] bloom-filter-no-false-negatives
A Bloom filter guarantees no false negatives — it returns either 'possibly in set' or 'definitely not in set'.
- Source: entries/2026/06/19/wiki-Bloom_filter.md
- Source URL: https://en.wikipedia.org/wiki/Bloom_filter

### [ACCEPT] bloom-filter-no-deletion-standard
Elements cannot be removed from a standard Bloom filter because clearing a bit could invalidate other elements sharing that position, introducing false negatives.
- Source: entries/2026/06/19/wiki-Bloom_filter.md
- Source URL: https://en.wikipedia.org/wiki/Bloom_filter

### [ACCEPT] bloom-filter-9point6-bits-per-element-1pct-fp
A Bloom filter requires approximately 9.6 bits per element for a 1% false positive rate, regardless of element size; each additional ~4.8 bits per element reduces the FP rate by 10x.
- Source: entries/2026/06/19/wiki-Bloom_filter.md
- Source URL: https://en.wikipedia.org/wiki/Bloom_filter

### [ACCEPT] bloom-filter-optimal-k-formula
The optimal number of hash functions for a Bloom filter is k = (m/n) * ln(2), at which point approximately half the bits in the array are set to 1.
- Source: entries/2026/06/19/wiki-Bloom_filter.md
- Source URL: https://en.wikipedia.org/wiki/Bloom_filter

### [ACCEPT] bloom-filter-ok-time-add-lookup
Bloom filter add and lookup operations take O(k) time — constant regardless of the number of elements in the set.
- Source: entries/2026/06/19/wiki-Bloom_filter.md
- Source URL: https://en.wikipedia.org/wiki/Bloom_filter

### [ACCEPT] bloom-filter-union-via-bitwise-or-lossless
Two Bloom filters with the same size and hash functions can be merged via bitwise OR to compute their union losslessly (identical to building from scratch on the union set).
- Source: entries/2026/06/19/wiki-Bloom_filter.md
- Source URL: https://en.wikipedia.org/wiki/Bloom_filter

### [ACCEPT] counting-bloom-filter-enables-deletion
A counting Bloom filter replaces single bits with counters, enabling element removal at the cost of additional space.
- Source: entries/2026/06/19/wiki-Bloom_filter.md
- Source URL: https://en.wikipedia.org/wiki/Bloom_filter

### [ACCEPT] bloom-filter-used-in-lsm-sstable-reads
In LSM-tree storage engines, Bloom filters sit in front of SSTables to short-circuit reads for keys that don't exist at a given level, avoiding unnecessary disk lookups.
- Source: entries/2026/06/19/wiki-Bloom_filter.md
- Source URL: https://en.wikipedia.org/wiki/Bloom_filter

### [ACCEPT] bully-algorithm-highest-id-wins
The bully algorithm elects the process with the highest process ID among all non-failed processes as the coordinator.
- Source: entries/2026/06/19/wiki-Bully_algorithm.md
- Source URL: https://en.wikipedia.org/wiki/Bully_algorithm

### [ACCEPT] bully-algorithm-synchronous-model-required
The bully algorithm requires a synchronous system model with bounded message delays for its timeout mechanisms to function correctly.
- Source: entries/2026/06/19/wiki-Bully_algorithm.md
- Source URL: https://en.wikipedia.org/wiki/Bully_algorithm

### [ACCEPT] bully-algorithm-three-message-types
The bully algorithm uses three message types: Election (announce election), Answer/Alive (higher-ID process is alive), and Coordinator/Victory (declare new leader).
- Source: entries/2026/06/19/wiki-Bully_algorithm.md
- Source URL: https://en.wikipedia.org/wiki/Bully_algorithm

### [ACCEPT] bully-algorithm-worst-case-n-squared
The bully algorithm has worst-case message complexity of Θ(N²), triggered when the lowest-ID process initiates the election.
- Source: entries/2026/06/19/wiki-Bully_algorithm.md
- Source URL: https://en.wikipedia.org/wiki/Bully_algorithm

### [ACCEPT] bully-algorithm-victory-condition
In the bully algorithm, a process sends a Victory message only if it receives no Answer from any higher-ID process.
- Source: entries/2026/06/19/wiki-Bully_algorithm.md
- Source URL: https://en.wikipedia.org/wiki/Bully_algorithm

### [ACCEPT] bully-algorithm-recovery-triggers-election
In the bully algorithm, when a process recovers from failure it initiates a new election rather than passively rejoining.
- Source: entries/2026/06/19/wiki-Bully_algorithm.md
- Source URL: https://en.wikipedia.org/wiki/Bully_algorithm

### [ACCEPT] bully-algorithm-crash-faults-only
The bully algorithm handles crash-recovery faults only, not Byzantine (arbitrary) faults.
- Source: entries/2026/06/19/wiki-Bully_algorithm.md
- Source URL: https://en.wikipedia.org/wiki/Bully_algorithm

### [ACCEPT] chang-roberts-ring-topology-nlogn
The Chang and Roberts algorithm is a leader election algorithm that operates on a logical ring topology with O(N log N) average-case message complexity.
- Source: entries/2026/06/19/wiki-Bully_algorithm.md
- Source URL: https://en.wikipedia.org/wiki/Bully_algorithm

### [ACCEPT] bft-3f-plus-1-rule
Without message signing, Byzantine fault tolerance requires n > 3f nodes (at least 3f+1) to tolerate f faulty nodes; this bound is both necessary and sufficient.
- Source: entries/2026/06/19/wiki-Byzantine_fault.md
- Source URL: https://en.wikipedia.org/wiki/Byzantine_fault

### [ACCEPT] bft-full-requirements-three-conditions
Full BFT requires three conditions simultaneously: 3F+1 nodes, 2F+1 independent communication paths, and F+1 rounds of communication.
- Source: entries/2026/06/19/wiki-Byzantine_fault.md
- Source URL: https://en.wikipedia.org/wiki/Byzantine_fault

### [ACCEPT] bft-with-signatures-arbitrary-faults
With unforgeable digital signatures, BFT can tolerate an arbitrary number of faulty nodes.
- Source: entries/2026/06/19/wiki-Byzantine_fault.md
- Source URL: https://en.wikipedia.org/wiki/Byzantine_fault

### [ACCEPT] bft-broadcast-consistency-not-correctness
BFT guarantees broadcast consistency (all receivers get the same value) but does NOT verify correctness of the value itself.
- Source: entries/2026/06/19/wiki-Byzantine_fault.md
- Source URL: https://en.wikipedia.org/wiki/Byzantine_fault

### [ACCEPT] pbft-castro-liskov-1999
Practical Byzantine Fault Tolerance (PBFT) was introduced by Castro and Liskov in 1999, processing thousands of requests per second with sub-millisecond latency overhead.
- Source: entries/2026/06/19/wiki-Byzantine_fault.md
- Source URL: https://en.wikipedia.org/wiki/Byzantine_fault

### [ACCEPT] byzantine-generals-lamport-shostak-pease-1982
The Byzantine generals problem was formalized by Lamport, Shostak, and Pease in their seminal 1982 paper, which won the 2005 Dijkstra Prize.
- Source: entries/2026/06/19/wiki-Byzantine_fault.md
- Source URL: https://en.wikipedia.org/wiki/Byzantine_fault

### [ACCEPT] byzantine-faults-subsume-all-failure-classes
Byzantine faults are the most general failure class in distributed systems, subsuming crash faults, omission faults, and timing faults.
- Source: entries/2026/06/19/wiki-Byzantine_fault.md
- Source URL: https://en.wikipedia.org/wiki/Byzantine_fault

### [ACCEPT] byzantine-faults-not-only-adversarial
Byzantine failures can arise from purely physical or software faults (e.g., incorrect voltages propagating through encryption), not just adversarial behavior.
- Source: entries/2026/06/19/wiki-Byzantine_fault.md
- Source URL: https://en.wikipedia.org/wiki/Byzantine_fault

### [ACCEPT] cap-theorem-at-most-two-of-three
The CAP theorem states any distributed data store can provide at most two of three guarantees: Consistency, Availability, and Partition tolerance.
- Source: entries/2026/06/19/wiki-CAP_theorem.md
- Source URL: https://en.wikipedia.org/wiki/CAP_theorem

### [ACCEPT] cap-brewer-2000-gilbert-lynch-2002
CAP was conjectured by Eric Brewer in 2000 and formally proven by Gilbert and Lynch in 2002.
- Source: entries/2026/06/19/wiki-CAP_theorem.md
- Source URL: https://en.wikipedia.org/wiki/CAP_theorem

### [ACCEPT] cap-consistency-not-acid-consistency
CAP consistency (linearizability — every read sees the most recent write) is not the same as ACID consistency (database invariants preserved).
- Source: entries/2026/06/19/wiki-CAP_theorem.md
- Source URL: https://en.wikipedia.org/wiki/CAP_theorem

### [ACCEPT] cap-no-distributed-db-is-ca
No distributed database is classified as CA because network partitions cannot be avoided in practice, making partition tolerance non-optional.
- Source: entries/2026/06/19/wiki-CAP_theorem.md
- Source URL: https://en.wikipedia.org/wiki/CAP_theorem

### [ACCEPT] cap-pick-two-is-oversimplified
The 'pick two out of three' CAP framing is oversimplified; Brewer clarified in 2012 that the C vs A trade-off only applies during actual network partitions.
- Source: entries/2026/06/19/wiki-CAP_theorem.md
- Source URL: https://en.wikipedia.org/wiki/CAP_theorem

### [ACCEPT] pacelc-extends-cap-latency-consistency
The PACELC theorem extends CAP: if Partition, choose Availability or Consistency; Else, choose Latency or Consistency.
- Source: entries/2026/06/19/wiki-CAP_theorem.md
- Source URL: https://en.wikipedia.org/wiki/CAP_theorem

### [ACCEPT] cap-cp-examples-mongo-redis
CP systems (consistency over availability during partitions) include MongoDB, Redis, and traditional RDBMS.
- Source: entries/2026/06/19/wiki-CAP_theorem.md
- Source URL: https://en.wikipedia.org/wiki/CAP_theorem

### [ACCEPT] cap-ap-examples-couch-cassandra
AP systems (availability over consistency during partitions) include CouchDB, Cassandra, and ScyllaDB.
- Source: entries/2026/06/19/wiki-CAP_theorem.md
- Source URL: https://en.wikipedia.org/wiki/CAP_theorem

### [ACCEPT] crc32-polynomial-division-gf2
CRC computation is polynomial long division over GF(2), where XOR replaces subtraction with no borrow/carry.
- Source: entries/2026/06/19/wiki-CRC-32.md
- Source URL: https://en.wikipedia.org/wiki/CRC-32

### [ACCEPT] crc32-lsbit-polynomial-edb88320
The lsbit-first polynomial for CRC-32 is 0xEDB88320; msbit-first is 0x04C11DB7 — these are bit-reversals of each other.
- Source: entries/2026/06/19/wiki-CRC-32.md
- Source URL: https://en.wikipedia.org/wiki/CRC-32

### [ACCEPT] crc32-preset-minus-one-purpose
CRC preset to -1 (0xFFFF...) ensures that leading zero bytes affect the CRC, preventing the weakness where prepending zeros leaves the checksum unchanged.
- Source: entries/2026/06/19/wiki-CRC-32.md
- Source URL: https://en.wikipedia.org/wiki/CRC-32

### [ACCEPT] crc32-post-invert-trailing-zeros
CRC post-inversion (complementing the final remainder) ensures that appending zero bytes also affects the CRC.
- Source: entries/2026/06/19/wiki-CRC-32.md
- Source URL: https://en.wikipedia.org/wiki/CRC-32

### [ACCEPT] crc32-correct-message-residue-nonzero
The CRC remainder of a correct message (data + appended CRC) is a fixed non-zero constant (the 'residue') when preset-to-minus-1 and post-invert are used, but is zero for pure polynomial division without these steps.
- Source: entries/2026/06/19/wiki-CRC-32.md
- Source URL: https://en.wikipedia.org/wiki/CRC-32

### [ACCEPT] crc32-table-linearity-property
CRC lookup tables exploit linearity: table[i XOR j] = table[i] XOR table[j], so only log2(256) = 8 direct CRC computations are needed to fill a 256-entry table.
- Source: entries/2026/06/19/wiki-CRC-32.md
- Source URL: https://en.wikipedia.org/wiki/CRC-32

### [ACCEPT] crc32c-preferred-new-designs
CRC-32C (Castagnoli) is preferred over CRC-32 for new designs due to better error detection properties and hardware acceleration support (Intel CRC32 instruction, SSE 4.2 PCLMULQDQ).
- Source: entries/2026/06/19/wiki-CRC-32.md
- Source URL: https://en.wikipedia.org/wiki/CRC-32

### [ACCEPT] cdc-delta-driven-incremental-integration
Change Data Capture (CDC) enables incremental delta-driven data integration by capturing only changes rather than reprocessing entire datasets.
- Source: entries/2026/06/19/wiki-Change_data_capture.md
- Source URL: https://en.wikipedia.org/wiki/Change_data_capture

### [ACCEPT] cdc-six-techniques
There are six CDC techniques: timestamps, version numbers, status indicators, combined (time/version/status), database triggers, and transaction log reading.
- Source: entries/2026/06/19/wiki-Change_data_capture.md
- Source URL: https://en.wikipedia.org/wiki/Change_data_capture

### [ACCEPT] cdc-transaction-log-advantages
Transaction log-based CDC has minimal database impact, requires no application or schema changes, provides low latency, and preserves transactional integrity by replaying commits in order.
- Source: entries/2026/06/19/wiki-Change_data_capture.md
- Source URL: https://en.wikipedia.org/wiki/Change_data_capture

### [ACCEPT] cdc-transaction-log-vendor-specific
Transaction log-based CDC uses vendor-specific formats with no cross-DBMS standard, requiring handling of log archiving, uncommitted/rolled-back changes, and format differences across versions.
- Source: entries/2026/06/19/wiki-Change_data_capture.md
- Source URL: https://en.wikipedia.org/wiki/Change_data_capture

### [ACCEPT] cdc-vs-scd-type2-history
CDC produces a delta-driven dataset (only changes, like SCD Type 1), while SCD Type 2 produces a historized dataset preserving all versions; the choice depends on whether history is needed at the target.
- Source: entries/2026/06/19/wiki-Change_data_capture.md
- Source URL: https://en.wikipedia.org/wiki/Change_data_capture

### [ACCEPT] cdc-row-level-version-not-for-locking
Row-level version numbers used for optimistic locking are NOT usable for CDC because CDC would need to know every row's starting version, which is impractical.
- Source: entries/2026/06/19/wiki-Change_data_capture.md
- Source URL: https://en.wikipedia.org/wiki/Change_data_capture

### [ACCEPT] consistent-hashing-invented-1997-mit
Consistent hashing was invented at MIT by David Karger et al. in 1997
- Source: entries/2026/06/19/wiki-Consistent_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Consistent_hashing

### [ACCEPT] consistent-hashing-only-k-over-n-keys-move
When adding or removing a node in consistent hashing, only K/N keys need to be redistributed on average (where K is total keys and N is total nodes)
- Source: entries/2026/06/19/wiki-Consistent_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Consistent_hashing

### [ACCEPT] consistent-hashing-lookup-olog-n
Key lookup in consistent hashing is O(log N) via binary search of sorted server positions, compared to O(1) in traditional modular hashing
- Source: entries/2026/06/19/wiki-Consistent_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Consistent_hashing

### [ACCEPT] consistent-hashing-virtual-nodes-solve-skew
Virtual nodes (multiple positions per physical server on the hash ring) solve load skew caused by uneven arc lengths in consistent hashing
- Source: entries/2026/06/19/wiki-Consistent_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Consistent_hashing

### [ACCEPT] consistent-hashing-special-case-rendezvous
Consistent hashing is a special case of rendezvous hashing (Highest Random Weight), which was invented in 1996
- Source: entries/2026/06/19/wiki-Consistent_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Consistent_hashing

### [ACCEPT] akamai-founded-by-consistent-hashing-authors
Akamai was founded by co-authors of the consistent hashing paper (Lewin and Leighton) and uses consistent hashing within clusters
- Source: entries/2026/06/19/wiki-Consistent_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Consistent_hashing

### [ACCEPT] consistent-hashing-used-by-dynamo-cassandra-riak
Systems using consistent hashing include Amazon Dynamo, Apache Cassandra, Riak, Couchbase, ScyllaDB, Akamai CDN, Discord, OpenStack Swift, GlusterFS, and MinIO
- Source: entries/2026/06/19/wiki-Consistent_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Consistent_hashing

### [ACCEPT] count-sketch-invented-2004-charikar
Count sketch was invented by Charikar, Chen, and Farach-Colton in 2004 as an improvement to the AMS Sketch
- Source: entries/2026/06/19/wiki-Count_sketch.md
- Source URL: https://en.wikipedia.org/wiki/Count_sketch

### [ACCEPT] count-sketch-uses-two-hash-families
Count sketch uses two families of pairwise independent hash functions: bucket hashes h_i mapping elements to buckets and sign hashes s_i mapping elements to {+1, -1}
- Source: entries/2026/06/19/wiki-Count_sketch.md
- Source URL: https://en.wikipedia.org/wiki/Count_sketch

### [ACCEPT] count-sketch-uses-median-not-mean
Count sketch aggregates estimates across rows using the median (not mean), providing exponentially decreasing failure probability — this is called the 'median trick'
- Source: entries/2026/06/19/wiki-Count_sketch.md
- Source URL: https://en.wikipedia.org/wiki/Count_sketch

### [ACCEPT] count-sketch-two-sided-error
Count sketch provides two-sided error bounds (can both overestimate and underestimate), unlike count-min sketch which only overestimates
- Source: entries/2026/06/19/wiki-Count_sketch.md
- Source URL: https://en.wikipedia.org/wiki/Count_sketch

### [ACCEPT] count-sketch-linear-then-nonlinear
Count sketch is a linear mapping (sketch/projection step) followed by a non-linear reconstruction (median step)
- Source: entries/2026/06/19/wiki-Count_sketch.md
- Source URL: https://en.wikipedia.org/wiki/Count_sketch

### [ACCEPT] tensor-sketch-convolution-of-count-sketches
The count sketch of an outer product equals the convolution of two independent count sketches (Pham & Pagh 2013), enabling fast explicit polynomial kernel approximation
- Source: entries/2026/06/19/wiki-Count_sketch.md
- Source URL: https://en.wikipedia.org/wiki/Count_sketch

### [ACCEPT] counting-bloom-filter-counters-not-bits
A counting Bloom filter replaces the bit array of a standard Bloom filter with an array of counters, enabling frequency-based threshold queries
- Source: entries/2026/06/19/wiki-Counting_Bloom_filter.md
- Source URL: https://en.wikipedia.org/wiki/Counting_Bloom_filter

### [ACCEPT] counting-bloom-filter-deletion-causes-false-negatives
Deleting elements from a counting Bloom filter by decrementing counters can introduce false negatives if a never-inserted element is deleted, breaking the standard Bloom filter guarantee
- Source: entries/2026/06/19/wiki-Counting_Bloom_filter.md
- Source URL: https://en.wikipedia.org/wiki/Counting_Bloom_filter

### [ACCEPT] cbf-same-structure-as-count-min-sketch
A counting Bloom filter and a count-min sketch are the same underlying data structure used for different purposes (threshold testing vs. frequency estimation)
- Source: entries/2026/06/19/wiki-Counting_Bloom_filter.md
- Source URL: https://en.wikipedia.org/wiki/Counting_Bloom_filter

### [ACCEPT] ibf-extends-cbf-with-idsum-hashsum
An invertible Bloom filter (IBF) extends a counting Bloom filter with idSum and hashSum fields per cell, enabling enumeration of remaining elements when the set is small
- Source: entries/2026/06/19/wiki-Counting_Bloom_filter.md
- Source URL: https://en.wikipedia.org/wiki/Counting_Bloom_filter

### [ACCEPT] iblt-extends-ibf-with-values
An invertible Bloom lookup table (IBLT) extends an IBF with a valueSum field to store key-value pairs, used in database synchronization and data compression
- Source: entries/2026/06/19/wiki-Counting_Bloom_filter.md
- Source URL: https://en.wikipedia.org/wiki/Counting_Bloom_filter

### [ACCEPT] cm-sketch-invented-2003-cormode-muthukrishnan
The count-min sketch was invented by Cormode and Muthukrishnan in 2003
- Source: entries/2026/06/19/wiki-Countmin_sketch.md
- Source URL: https://en.wikipedia.org/wiki/Count–min_sketch

### [ACCEPT] cm-sketch-never-undercounts
The count-min sketch never undercounts — error is strictly one-sided (overestimation only), because hash collisions can only add to counters
- Source: entries/2026/06/19/wiki-Countmin_sketch.md
- Source URL: https://en.wikipedia.org/wiki/Count–min_sketch

### [ACCEPT] cm-sketch-parameter-formulas
Count-min sketch parameter sizing: width w = ceil(e/epsilon) controls error magnitude, depth d = ceil(ln(1/delta)) controls failure probability
- Source: entries/2026/06/19/wiki-Countmin_sketch.md
- Source URL: https://en.wikipedia.org/wiki/Count–min_sketch

### [ACCEPT] cm-sketch-point-query-uses-minimum
Count-min sketch point query returns the minimum value across all d rows for the queried element, providing the tightest upper bound on true frequency
- Source: entries/2026/06/19/wiki-Countmin_sketch.md
- Source URL: https://en.wikipedia.org/wiki/Count–min_sketch

### [ACCEPT] cm-sketch-linear-mergeable
Count-min sketches are linear and mergeable: element-wise addition of two sketches equals the sketch of the concatenated streams, enabling distributed streaming
- Source: entries/2026/06/19/wiki-Countmin_sketch.md
- Source URL: https://en.wikipedia.org/wiki/Count–min_sketch

### [ACCEPT] cm-sketch-conservative-update-breaks-linearity
Conservative update in count-min sketch reduces overestimation by only incrementing cells to max(current, estimate + c), but this optimization breaks linearity
- Source: entries/2026/06/19/wiki-Countmin_sketch.md
- Source URL: https://en.wikipedia.org/wiki/Count–min_sketch

### [ACCEPT] cuckoo-filter-supports-deletion
Cuckoo filters support element deletion while standard Bloom filters do not — this is the primary differentiator
- Source: entries/2026/06/19/wiki-Cuckoo_filter.md
- Source URL: https://en.wikipedia.org/wiki/Cuckoo_filter

### [ACCEPT] cuckoo-filter-xor-alternate-bucket
Cuckoo filters compute alternate buckets via h2(x) = h1(x) XOR hash(fingerprint(x)), allowing the alternate bucket to be found from any bucket plus the fingerprint alone
- Source: entries/2026/06/19/wiki-Cuckoo_filter.md
- Source URL: https://en.wikipedia.org/wiki/Cuckoo_filter

### [ACCEPT] cuckoo-filter-false-positive-bound
Cuckoo filter false positive rate is bounded by epsilon <= b / 2^(f-1), where b is bucket size and f is fingerprint size in bits
- Source: entries/2026/06/19/wiki-Cuckoo_filter.md
- Source URL: https://en.wikipedia.org/wiki/Cuckoo_filter

### [ACCEPT] cuckoo-filter-load-factor-95-percent
Cuckoo filters can achieve a load factor (alpha) of up to 95.5%, providing high space utilization
- Source: entries/2026/06/19/wiki-Cuckoo_filter.md
- Source URL: https://en.wikipedia.org/wiki/Cuckoo_filter

### [ACCEPT] cuckoo-filter-no-bitwise-union-intersection
Bloom filters support fast union and intersection via bitwise operations, while cuckoo filters do not support these operations
- Source: entries/2026/06/19/wiki-Cuckoo_filter.md
- Source URL: https://en.wikipedia.org/wiki/Cuckoo_filter

### [ACCEPT] cuckoo-filter-delete-only-known-members
In a cuckoo filter, only items known to have been inserted may be deleted; deleting a non-member can corrupt the filter
- Source: entries/2026/06/19/wiki-Cuckoo_filter.md
- Source URL: https://en.wikipedia.org/wiki/Cuckoo_filter

### [ACCEPT] checksum-verifies-integrity-not-authenticity
Checksums verify data integrity (data unchanged) but do not verify data authenticity (data from trusted source)
- Source: entries/2026/06/19/wiki-Checksum.md
- Source URL: https://en.wikipedia.org/wiki/Checksum

### [ACCEPT] parity-xor-checksum-misses-even-bit-errors
Parity (XOR) checksum detects all odd-number-of-bit errors but misses even-number errors at corresponding positions across words, with probability of undetected two-bit error being 1/n
- Source: entries/2026/06/19/wiki-Checksum.md
- Source URL: https://en.wikipedia.org/wiki/Checksum

### [ACCEPT] position-dependent-checksums-detect-reordering
Position-dependent checksums (Fletcher, Adler-32, CRC) incorporate word position to detect reordering, insertion, and deletion of zero-words, overcoming weaknesses of simple parity/sum checksums
- Source: entries/2026/06/19/wiki-Checksum.md
- Source URL: https://en.wikipedia.org/wiki/Checksum

### [ACCEPT] crc-dominant-checksum-in-practice
CRC (Cyclic Redundancy Check) is the most widely used position-dependent checksum in practice, used in Ethernet, ZIP, and PNG
- Source: entries/2026/06/19/wiki-Checksum.md
- Source URL: https://en.wikipedia.org/wiki/Checksum

### [ACCEPT] filesystems-with-checksum-integrity
Bcachefs, Btrfs, ReFS, and ZFS perform automatic file integrity checking via checksums
- Source: entries/2026/06/19/wiki-Checksum.md
- Source URL: https://en.wikipedia.org/wiki/Checksum

### [ACCEPT] twos-complement-checksum-verification
With two's complement sum checksum, the receiver adds all words including the checksum and the result must be all zeros or an error occurred
- Source: entries/2026/06/19/wiki-Checksum.md
- Source URL: https://en.wikipedia.org/wiki/Checksum

### [ACCEPT] cqs-devised-by-meyer-for-eiffel
Command-Query Separation (CQS) was devised by Bertrand Meyer as part of the Eiffel programming language
- Source: entries/2026/06/19/wiki-CommandE28093query_separation.md
- Source URL: https://en.wikipedia.org/wiki/Command%E2%80%93query_separation

### [ACCEPT] cqs-methods-either-return-or-mutate
CQS states that every method should either be a command (performs an action, modifies state) or a query (returns data), but never both
- Source: entries/2026/06/19/wiki-CommandE28093query_separation.md
- Source URL: https://en.wikipedia.org/wiki/Command%E2%80%93query_separation

### [ACCEPT] cqs-method-level-cqrs-architecture-level
CQS is a method-level principle; CQRS is the architecture-level generalization that uses separate read and write models, interfaces, and often separate data stores
- Source: entries/2026/06/19/wiki-CommandE28093query_separation.md
- Source URL: https://en.wikipedia.org/wiki/Command%E2%80%93query_separation

### [ACCEPT] cqs-race-condition-limitation
CQS introduces complexity in multithreaded code because separating a combined atomic operation (like incrementAndReturn) into separate command and query calls creates a race condition
- Source: entries/2026/06/19/wiki-CommandE28093query_separation.md
- Source URL: https://en.wikipedia.org/wiki/Command%E2%80%93query_separation

### [ACCEPT] cqrs-pairs-with-event-sourcing-eventual-consistency
CQRS pairs naturally with event-based architectures, eventual consistency, and Domain-Driven Design
- Source: entries/2026/06/19/wiki-CommandE28093query_separation.md
- Source URL: https://en.wikipedia.org/wiki/Command%E2%80%93query_separation

### [ACCEPT] 2pc-proposed-by-jim-gray-1978
Two-Phase Commit (2PC) was proposed by Jim Gray in 1978 and consists of a preparation phase followed by a commit phase
- Source: entries/2026/06/19/wiki-Commit_data_management.md
- Source URL: https://en.wikipedia.org/wiki/Commit_(data_management)

### [ACCEPT] 2pc-is-blocking-on-coordinator-failure
Two-Phase Commit is blocking: if the coordinator fails after sending PREPARE but before sending COMMIT/ROLLBACK, participants are stuck waiting indefinitely
- Source: entries/2026/06/19/wiki-Commit_data_management.md
- Source URL: https://en.wikipedia.org/wiki/Commit_(data_management)

### [ACCEPT] 3pc-adds-precommit-phase-non-blocking
Three-Phase Commit adds a pre-commit phase between preparation and commit plus a timeout mechanism, making it non-blocking at the cost of additional message overhead
- Source: entries/2026/06/19/wiki-Commit_data_management.md
- Source URL: https://en.wikipedia.org/wiki/Commit_(data_management)

### [ACCEPT] presumed-commit-abort-from-ibm-r-star
Presumed Commit and Presumed Abort protocols were introduced by IBM's R* system (Mohan, Lindsay, Obermarck, 1986); PC reduces overhead for the success path, PA reduces overhead for the failure path
- Source: entries/2026/06/19/wiki-Commit_data_management.md
- Source URL: https://en.wikipedia.org/wiki/Commit_(data_management)

### [ACCEPT] optimistic-commit-uses-compensating-transactions
Optimistic commit protocol allows transactions to temporarily access uncommitted data to avoid blocking, requiring compensating transactions on failure to achieve semantic atomicity
- Source: entries/2026/06/19/wiki-Commit_data_management.md
- Source URL: https://en.wikipedia.org/wiki/Commit_(data_management)

### [ACCEPT] redo-vs-undo-recovery-from-transaction-log
Redo recovery re-applies committed transactions after a crash; undo recovery reverses uncommitted transactions; both rely on the transaction log
- Source: entries/2026/06/19/wiki-Commit_data_management.md
- Source URL: https://en.wikipedia.org/wiki/Commit_(data_management)

### [ACCEPT] crdt-strong-eventual-consistency
CRDTs guarantee strong eventual consistency: replicas that have received the same set of updates are guaranteed identical, with no conflict resolution needed
- Source: entries/2026/06/19/wiki-Conflict-free_replicated_data_type.md
- Source URL: https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type

### [ACCEPT] crdt-state-based-vs-operation-based
State-based CRDTs (CvRDTs) send full local state and require merge to be commutative, associative, and idempotent; operation-based CRDTs (CmRDTs) transmit operations and require exactly-once causally-ordered delivery; the two approaches are theoretically equivalent
- Source: entries/2026/06/19/wiki-Conflict-free_replicated_data_type.md
- Source URL: https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type

### [ACCEPT] crdt-merge-must-form-semilattice
CRDT merge function must form a join-semilattice (commutative, associative, idempotent), and update function must be monotone with respect to the partial order, which guarantees convergence regardless of message ordering or duplication
- Source: entries/2026/06/19/wiki-Conflict-free_replicated_data_type.md
- Source URL: https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type

### [ACCEPT] pn-counter-internal-monotonic-external-not
In a PN-Counter (two G-Counters for increments and decrements), internal state grows monotonically even though externally visible query values can decrease
- Source: entries/2026/06/19/wiki-Conflict-free_replicated_data_type.md
- Source URL: https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type

### [ACCEPT] 2p-set-no-readd-after-removal
In a 2P-Set CRDT, once an element is removed (tombstoned) it can never be re-added; LWW-Element-Set and OR-Set overcome this limitation
- Source: entries/2026/06/19/wiki-Conflict-free_replicated_data_type.md
- Source URL: https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type

### [ACCEPT] delta-crdts-solve-bandwidth-problem
Delta state CRDTs solve the bandwidth problem of state-based CRDTs by disseminating only recent mutations rather than full state
- Source: entries/2026/06/19/wiki-Conflict-free_replicated_data_type.md
- Source URL: https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type

### [ACCEPT] crdt-industry-adoption
Redis, Riak, Cosmos DB have native CRDT support; Apple Notes, Figma, Facebook (Apollo), Phoenix framework, and League of Legends (7.5M concurrent users, 11K messages/second) all use CRDTs in production
- Source: entries/2026/06/19/wiki-Conflict-free_replicated_data_type.md
- Source URL: https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type

### [ACCEPT] flp-impossibility-result
The FLP impossibility result (Fischer, Lynch, Paterson, 1985) proves no deterministic algorithm can guarantee consensus in a fully asynchronous message-passing system if even one process can crash; randomized algorithms can circumvent this by achieving safety and liveness with overwhelming probability
- Source: entries/2026/06/19/wiki-Consensus_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Consensus_(computer_science)

### [ACCEPT] byzantine-fault-tolerance-thresholds
Byzantine fault tolerance requires n > 3f in oral/unauthenticated model and only n > f+1 in written/signed model (Dolev-Strong)
- Source: entries/2026/06/19/wiki-Consensus_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Consensus_(computer_science)

### [ACCEPT] consensus-number-hierarchy
Consensus number hierarchy: atomic read/write registers = 1, test-and-set/swap/fetch-and-add = 2, compare-and-swap (CAS) = infinity (universal); an object with infinite consensus number can implement any concurrent object wait-free
- Source: entries/2026/06/19/wiki-Consensus_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Consensus_(computer_science)

### [ACCEPT] consensus-three-properties
A correct consensus protocol must satisfy three properties: Termination (every correct process eventually decides), Integrity (if all propose same value v they decide v), and Agreement (every correct process decides the same value)
- Source: entries/2026/06/19/wiki-Consensus_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Consensus_(computer_science)

### [ACCEPT] phase-king-algorithm-n-gt-4f
The Phase King algorithm (Garay & Berman) tolerates Byzantine faults in synchronous systems, runs in f+1 phases with 2 rounds each, and requires n > 4f
- Source: entries/2026/06/19/wiki-Consensus_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Consensus_(computer_science)

### [ACCEPT] atomic-broadcast-equivalent-to-consensus
Atomic broadcast is equivalent to consensus: solving one solves the other; similarly, Terminating Reliable Broadcast, Consensus, and Weak Interactive Consistency are reducible to each other
- Source: entries/2026/06/19/wiki-Consensus_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Consensus_(computer_science)

### [ACCEPT] crdts-enable-ap-systems-cap-theorem
CRDTs enable AP (available, partition-tolerant) systems under the CAP theorem that still converge, sacrificing strong consistency for availability without losing eventual convergence guarantees
- Source: entries/2026/06/19/wiki-Conflict-free_replicated_data_type.md
- Source URL: https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type

### [ACCEPT] crc-detects-burst-errors-up-to-n-bits
An n-bit CRC detects any single burst error up to n bits long and catches approximately (1 − 2^−n) of longer bursts
- Source: entries/2026/06/19/wiki-Cyclic_redundancy_check.md
- Source URL: https://en.wikipedia.org/wiki/Cyclic_redundancy_check

### [ACCEPT] crc-arithmetic-uses-gf2-xor
CRC arithmetic uses the finite field GF(2) where addition is XOR with no carry, making hardware implementation trivial
- Source: entries/2026/06/19/wiki-Cyclic_redundancy_check.md
- Source URL: https://en.wikipedia.org/wiki/Cyclic_redundancy_check

### [ACCEPT] crc-generator-polynomial-degree-determines-width
A CRC generator polynomial of degree n has (n+1) terms and produces an n-bit CRC remainder
- Source: entries/2026/06/19/wiki-Cyclic_redundancy_check.md
- Source URL: https://en.wikipedia.org/wiki/Cyclic_redundancy_check

### [ACCEPT] crc-not-cryptographically-secure
CRCs are affine functions over XOR (CRC(x XOR y) = CRC(x) XOR CRC(y) XOR c), making them trivially forgeable and unsuitable for cryptographic integrity — this was exploited in WEP
- Source: entries/2026/06/19/wiki-Cyclic_redundancy_check.md
- Source URL: https://en.wikipedia.org/wiki/Cyclic_redundancy_check

### [ACCEPT] crc-primitive-polynomial-maximal-block-length
A primitive polynomial of degree r yields maximal block length 2^r − 1 with all single-bit and double-bit errors detectable; multiplying by (1+x) adds odd-error detection but halves maximal block length to 2^(r−1) − 1
- Source: entries/2026/06/19/wiki-Cyclic_redundancy_check.md
- Source URL: https://en.wikipedia.org/wiki/Cyclic_redundancy_check

### [ACCEPT] crc32c-hardware-acceleration-intel-arm
CRC-32C (Castagnoli) has dedicated hardware instructions in Intel SSE4.2 (Nehalem onward) and ARM AArch64
- Source: entries/2026/06/19/wiki-Cyclic_redundancy_check.md
- Source URL: https://en.wikipedia.org/wiki/Cyclic_redundancy_check

### [ACCEPT] crc-verification-zero-remainder
CRC verification works by appending the CRC to the original message and repeating the polynomial division; a zero remainder indicates no detectable error
- Source: entries/2026/06/19/wiki-Cyclic_redundancy_check.md
- Source URL: https://en.wikipedia.org/wiki/Cyclic_redundancy_check

### [ACCEPT] silent-data-corruption-most-dangerous
Silent data corruption (SDC) — errors undetected by disk firmware or OS — is the most dangerous form of data corruption because there is no error indication and corrupted state can compound over time
- Source: entries/2026/06/19/wiki-Data_corruption.md
- Source URL: https://en.wikipedia.org/wiki/Data_corruption

### [ACCEPT] firmware-bugs-5-10-percent-storage-failures
Firmware bugs account for 5–10% of storage failures according to a USENIX study of 39,000 storage systems
- Source: entries/2026/06/19/wiki-Data_corruption.md
- Source URL: https://en.wikipedia.org/wiki/Data_corruption

### [ACCEPT] faulty-cpu-cores-several-per-thousand
Google and Facebook (2021) identified faulty (mercurial) CPU cores as a data corruption source, occurring at a rate of several per thousand cores
- Source: entries/2026/06/19/wiki-Data_corruption.md
- Source URL: https://en.wikipedia.org/wiki/Data_corruption

### [ACCEPT] cern-silent-corruption-128mb-per-97pb
CERN found approximately 128 MB silently corrupted out of 97 PB over six months, demonstrating that real-world silent corruption rates are far higher than theoretical 1 in 10^16 bits
- Source: entries/2026/06/19/wiki-Data_corruption.md
- Source URL: https://en.wikipedia.org/wiki/Data_corruption

### [ACCEPT] checksumming-filesystems-zfs-btrfs-hammer-refs
ZFS, Btrfs, HAMMER, and ReFS are filesystems with built-in checksumming of both data and metadata, providing end-to-end integrity across the full storage stack
- Source: entries/2026/06/19/wiki-Data_corruption.md
- Source URL: https://en.wikipedia.org/wiki/Data_corruption

### [ACCEPT] end-to-end-data-protection-superior-to-layer-specific
End-to-end data protection (e.g., ZFS checksumming data and metadata) is superior to layer-specific integrity checks because corruption can occur at layer boundaries between components
- Source: entries/2026/06/19/wiki-Data_corruption.md
- Source URL: https://en.wikipedia.org/wiki/Data_corruption

### [ACCEPT] bit-rot-affects-all-storage-media-types
Data degradation (bit rot) affects all storage media types — DRAM (cosmic ray bit flips), solid-state (charge leakage), magnetic (orientation decay), optical (dye degradation), and paper (acid hydrolysis) — through different physical mechanisms
- Source: entries/2026/06/19/wiki-Data_degradation.md
- Source URL: https://en.wikipedia.org/wiki/Data_degradation

### [ACCEPT] flash-storage-decay-charge-leakage
Flash memory and SSDs store data as electrical charges that slowly leak through imperfect insulation; multi-level cells (MLC) are especially vulnerable due to narrower voltage margins
- Source: entries/2026/06/19/wiki-Data_degradation.md
- Source URL: https://en.wikipedia.org/wiki/Data_degradation

### [ACCEPT] latent-faults-silent-until-access
Latent faults are silent data corruptions detected only when the affected data is actually accessed and audited — not at write time — making checksumming and replication the only proactive detection mechanism
- Source: entries/2026/06/19/wiki-Data_degradation.md
- Source URL: https://en.wikipedia.org/wiki/Data_degradation

### [ACCEPT] no-technology-eliminates-data-degradation
No technology fully eliminates data degradation — all strategies (ECC, checksumming, replication, scrubbing) are mitigation, not prevention
- Source: entries/2026/06/19/wiki-Data_degradation.md
- Source URL: https://en.wikipedia.org/wiki/Data_degradation

### [ACCEPT] clustered-index-one-per-table-physical-order
A clustered index reorders physical data rows to match the index order; only one clustered index is allowed per table because it defines the physical row layout
- Source: entries/2026/06/19/wiki-Database_index.md
- Source URL: https://en.wikipedia.org/wiki/Database_index

### [ACCEPT] composite-index-leftmost-prefix-rule
In a composite index on (A, B, C), only the leftmost prefix of columns can be used efficiently — queries filtering on B alone or C alone cannot use the index; queries on A or A+B can
- Source: entries/2026/06/19/wiki-Database_index.md
- Source URL: https://en.wikipedia.org/wiki/Database_index

### [ACCEPT] covering-index-eliminates-table-lookup
A covering index contains all columns needed by a query, eliminating the need to read the base table row entirely; INCLUDE clause adds non-key columns at the leaf level only to enable covering with smaller index keys
- Source: entries/2026/06/19/wiki-Database_index.md
- Source URL: https://en.wikipedia.org/wiki/Database_index

### [ACCEPT] bitmap-indexes-low-cardinality-btree-high
Bitmap indexes are optimal for low-cardinality columns (few distinct values) using bitwise operations to combine conditions; B-tree indexes are better for high-cardinality columns
- Source: entries/2026/06/19/wiki-Database_index.md
- Source URL: https://en.wikipedia.org/wiki/Database_index

### [ACCEPT] leading-wildcards-defeat-index-usage
Leading wildcards in LIKE '%value' are not sargable and force full table scans; workarounds include reverse expression indexes or trigram/GIN indexes (PostgreSQL)
- Source: entries/2026/06/19/wiki-Database_index.md
- Source URL: https://en.wikipedia.org/wiki/Database_index

### [ACCEPT] no-iso-sql-standard-for-create-index
There is no ISO SQL standard for CREATE INDEX — index creation syntax is entirely vendor-specific
- Source: entries/2026/06/19/wiki-Database_index.md
- Source URL: https://en.wikipedia.org/wiki/Database_index

### [ACCEPT] transaction-log-guarantees-atomicity-durability
Transaction logs guarantee atomicity (undo uncommitted work on crash) and durability (redo committed work not yet materialized) — these are the two ACID properties they enforce
- Source: entries/2026/06/19/wiki-Database_log.md
- Source URL: https://en.wikipedia.org/wiki/Database_log

### [ACCEPT] lsn-monotonically-increasing-for-recovery
Log Sequence Numbers (LSNs) are unique, monotonically increasing identifiers for each log record; this ordering property is essential for recovery algorithms like ARIES
- Source: entries/2026/06/19/wiki-Database_log.md
- Source URL: https://en.wikipedia.org/wiki/Database_log

### [ACCEPT] clr-one-to-one-with-update-record
A Compensation Log Record (CLR) corresponds to exactly one Update Log Record and contains an undoNextLSN pointer to the next record to undo during rollback
- Source: entries/2026/06/19/wiki-Database_log.md
- Source URL: https://en.wikipedia.org/wiki/Database_log

### [ACCEPT] checkpoint-record-redo-undo-lsn
Checkpoint records contain redoLSN (where redo scanning starts — first dirty unflushed update) and undoLSN (oldest active transaction) which together define the recovery window
- Source: entries/2026/06/19/wiki-Database_log.md
- Source URL: https://en.wikipedia.org/wiki/Database_log

### [ACCEPT] six-transaction-log-record-types
Transaction logs have six record types: Update, Compensation (CLR), Commit, Abort, Checkpoint, and Completion — where Completion is distinct from Commit and indicates all work (commit or abort) is fully done
- Source: entries/2026/06/19/wiki-Database_log.md
- Source URL: https://en.wikipedia.org/wiki/Database_log

### [ACCEPT] codd-relational-model-1970
Edgar F. Codd proposed the relational model in 1970, organizing data into tables (relations) with rows (tuples) and columns (domains), using primary keys instead of disk addresses for cross-references
- Source: entries/2026/06/19/wiki-Database_system.md
- Source URL: https://en.wikipedia.org/wiki/Database_system

### [ACCEPT] sql-declarative-dbms-optimizes
SQL is a declarative query language that expresses what data is needed, not how to find it — the DBMS handles query optimization, enabled by the mathematical foundations (relational calculus) of the relational model
- Source: entries/2026/06/19/wiki-Database_system.md
- Source URL: https://en.wikipedia.org/wiki/Database_system

### [ACCEPT] cap-theorem-pick-two
The CAP theorem states a distributed system cannot simultaneously guarantee consistency, availability, and partition tolerance — at most two of three
- Source: entries/2026/06/19/wiki-Database_system.md
- Source URL: https://en.wikipedia.org/wiki/Database_system

### [ACCEPT] nosql-characteristics
NoSQL databases (2000s) use denormalized data, no fixed schemas, avoid joins, and emphasize horizontal scaling; they typically sacrifice consistency for availability and partition tolerance (eventual consistency)
- Source: entries/2026/06/19/wiki-Database_system.md
- Source URL: https://en.wikipedia.org/wiki/Database_system

### [ACCEPT] newsql-combines-sql-acid-with-nosql-scale
NewSQL databases retain the relational/SQL model and ACID guarantees while targeting NoSQL-level scalability for OLTP workloads
- Source: entries/2026/06/19/wiki-Database_system.md
- Source URL: https://en.wikipedia.org/wiki/Database_system

### [ACCEPT] ims-hierarchical-1966-apollo
IBM's IMS (1966) used the hierarchical database model, was developed for the Apollo program, and is still in use today
- Source: entries/2026/06/19/wiki-Database_system.md
- Source URL: https://en.wikipedia.org/wiki/Database_system

### [ACCEPT] normalization-each-fact-stored-once
Database normalization splits data so each fact is stored exactly once, simplifying updates; denormalization (used by NoSQL) trades this for read performance and horizontal scalability
- Source: entries/2026/06/19/wiki-Database_system.md
- Source URL: https://en.wikipedia.org/wiki/Database_system

### [ACCEPT] three-eras-database-technology
Three eras of database technology: navigational (1960s, hierarchical/network models), relational/SQL (1970s-80s), and post-relational/NoSQL (2000s)
- Source: entries/2026/06/19/wiki-Database_system.md
- Source URL: https://en.wikipedia.org/wiki/Database_system

### [ACCEPT] acid-properties-definition
ACID properties: Atomic (all-or-nothing), Consistent (conforms to database constraints), Isolated (does not affect other transactions), Durable (persisted to non-volatile storage)
- Source: entries/2026/06/19/wiki-Database_transaction.md
- Source URL: https://en.wikipedia.org/wiki/Database_transaction

### [ACCEPT] transaction-two-purposes
Database transactions serve two fundamental purposes: (1) providing reliable units of work for correct recovery from failures, and (2) providing isolation between programs accessing a database concurrently
- Source: entries/2026/06/19/wiki-Database_transaction.md
- Source URL: https://en.wikipedia.org/wiki/Database_transaction

### [ACCEPT] serializability-highest-isolation
Serializability is the highest transaction isolation level, guaranteeing that concurrent transaction effects are equivalent to some serial (sequential) execution
- Source: entries/2026/06/19/wiki-Database_transaction.md
- Source URL: https://en.wikipedia.org/wiki/Database_transaction

### [ACCEPT] read-uncommitted-lowest-isolation
READ UNCOMMITTED is the lowest transaction isolation level — it allows dirty reads (seeing uncommitted changes from other transactions) but maximizes concurrency
- Source: entries/2026/06/19/wiki-Database_transaction.md
- Source URL: https://en.wikipedia.org/wiki/Database_transaction

### [ACCEPT] compensating-transactions-undo-committed
Compensating transactions undo the effects of a previously committed transaction — they are used for long-lived distributed transactions where holding locks (as in 2PC) is impractical
- Source: entries/2026/06/19/wiki-Database_transaction.md
- Source URL: https://en.wikipedia.org/wiki/Database_transaction

### [ACCEPT] mysql-innodb-transactions-myisam-not
MySQL's InnoDB storage engine supports transactions; MyISAM does not
- Source: entries/2026/06/19/wiki-Database_transaction.md
- Source URL: https://en.wikipedia.org/wiki/Database_transaction

### [ACCEPT] dag-iff-topological-ordering
A directed graph is a DAG if and only if it admits a topological ordering — this bidirectional equivalence is the fundamental characterization
- Source: entries/2026/06/19/wiki-Directed_acyclic_graph.md
- Source URL: https://en.wikipedia.org/wiki/Directed_acyclic_graph

### [ACCEPT] topological-sort-linear-time
Topological sort runs in O(V + E) time using either Kahn's algorithm (iteratively remove zero-in-degree vertices) or reverse-postorder DFS
- Source: entries/2026/06/19/wiki-Directed_acyclic_graph.md
- Source URL: https://en.wikipedia.org/wiki/Directed_acyclic_graph

### [ACCEPT] dag-shortest-longest-path-linear-time
Shortest and longest paths in DAGs are solvable in O(V + E) linear time by processing vertices in topological order — in contrast, longest path in general graphs is NP-hard
- Source: entries/2026/06/19/wiki-Directed_acyclic_graph.md
- Source URL: https://en.wikipedia.org/wiki/Directed_acyclic_graph

### [ACCEPT] dag-transitive-reduction-unique
The transitive reduction of a DAG (fewest edges preserving reachability) is unique; for cyclic directed graphs it is not unique
- Source: entries/2026/06/19/wiki-Directed_acyclic_graph.md
- Source URL: https://en.wikipedia.org/wiki/Directed_acyclic_graph

### [ACCEPT] dag-reachability-partial-order
The reachability relation of a DAG forms a partial order on its vertices; every finite partial order can be represented as a DAG, and vice versa
- Source: entries/2026/06/19/wiki-Directed_acyclic_graph.md
- Source URL: https://en.wikipedia.org/wiki/Directed_acyclic_graph

### [ACCEPT] condensation-scc-to-dag
Any directed graph can be converted to a DAG by computing its condensation — contracting each strongly connected component into a single supervertex
- Source: entries/2026/06/19/wiki-Directed_acyclic_graph.md
- Source URL: https://en.wikipedia.org/wiki/Directed_acyclic_graph

### [ACCEPT] git-history-is-dag-not-tree
Git commit history forms a DAG, not a tree, because merge commits create vertices with multiple parents
- Source: entries/2026/06/19/wiki-Directed_acyclic_graph.md
- Source URL: https://en.wikipedia.org/wiki/Directed_acyclic_graph

### [ACCEPT] shared-nothing-requires-partitioning
Shared-nothing database architecture requires data partitioning (sharding) across nodes since each node has its own memory and storage; shared-disk and shared-memory architectures do not require partitioning
- Source: entries/2026/06/19/wiki-Distributed_database.md
- Source URL: https://en.wikipedia.org/wiki/Distributed_database

### [ACCEPT] replication-vs-duplication
Replication is change-driven and bidirectional (propagates detected changes to converge all copies); duplication uses a single master copied periodically to other locations, where only the master may be modified by users
- Source: entries/2026/06/19/wiki-Distributed_database.md
- Source URL: https://en.wikipedia.org/wiki/Distributed_database

### [ACCEPT] cloud-db-hybrid-shared-nothing-compute-shared-disk-storage
Modern cloud databases (e.g., Snowflake, Aurora) commonly use a hybrid architecture: shared-nothing compute layer combined with a shared-disk storage layer
- Source: entries/2026/06/19/wiki-Distributed_database.md
- Source URL: https://en.wikipedia.org/wiki/Distributed_database

### [ACCEPT] distributed-db-loosely-coupled
Distributed databases consist of loosely coupled sites sharing no physical components, distinguishing them from tightly coupled parallel database systems
- Source: entries/2026/06/19/wiki-Distributed_database.md
- Source URL: https://en.wikipedia.org/wiki/Distributed_database

### [ACCEPT] 2pc-short-lived-transactions-only
Two-phase commit (2PC) is designed for short-lived distributed transactions (milliseconds to minutes); it is unsuitable for long-lived transactions because it holds locks too long
- Source: entries/2026/06/19/wiki-Distributed_transaction.md
- Source URL: https://en.wikipedia.org/wiki/Distributed_transaction

### [ACCEPT] global-serializability-can-break-across-dbs
Global serializability can be violated even when every individual database in a distributed system provides local serializability — individual serializability does not compose automatically
- Source: entries/2026/06/19/wiki-Distributed_transaction.md
- Source URL: https://en.wikipedia.org/wiki/Distributed_transaction

### [ACCEPT] ss2pl-ensures-global-serializability
Strong strict two-phase locking (SS2PL) ensures global serializability in distributed transactions, but only if all participating databases employ it
- Source: entries/2026/06/19/wiki-Distributed_transaction.md
- Source URL: https://en.wikipedia.org/wiki/Distributed_transaction

### [ACCEPT] xopen-xa-standard-not-long-lived
X/Open XA (from The Open Group) is the de facto standard for distributed transaction processing but does not cover long-lived distributed transactions
- Source: entries/2026/06/19/wiki-Distributed_transaction.md
- Source URL: https://en.wikipedia.org/wiki/Distributed_transaction

### [ACCEPT] distributed-transactions-not-limited-to-databases
Distributed transactions are not limited to databases — they apply to any transactional resource in a distributed environment
- Source: entries/2026/06/19/wiki-Distributed_transaction.md
- Source URL: https://en.wikipedia.org/wiki/Distributed_transaction

### [ACCEPT] durability-is-d-in-acid
Durability is the 'D' in ACID, guaranteeing that once a transaction is committed, its effects survive permanently even through crashes, power outages, and hardware failures
- Source: entries/2026/06/19/wiki-Durability_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Durability_(database_systems)

### [ACCEPT] durability-three-failure-classes
A durable system must tolerate three failure classes: transaction failures (application-level aborts), system failures (volatile memory loss), and media failures (non-volatile storage damage)
- Source: entries/2026/06/19/wiki-Durability_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Durability_(database_systems)

### [ACCEPT] wal-logs-before-commit-ack
Write-Ahead Logging (WAL) requires buffering changes to non-volatile storage before acknowledging a commit, enabling redo of committed and undo of uncommitted transactions during recovery
- Source: entries/2026/06/19/wiki-Durability_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Durability_(database_systems)

### [ACCEPT] two-phase-commit-distributed-durability
Two-Phase Commit Protocol (2PC) coordinates distributed transaction commits across multiple nodes — all nodes must agree before commit is acknowledged
- Source: entries/2026/06/19/wiki-Durability_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Durability_(database_systems)

### [ACCEPT] aries-recovery-algorithm
ARIES (Algorithms for Recovery and Isolation Exploiting Semantics) is a widely adopted recovery algorithm family for distributed databases supporting fine-granularity locking and partial rollbacks
- Source: entries/2026/06/19/wiki-Durability_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Durability_(database_systems)

### [ACCEPT] stable-memory-via-replication
Stable memory is an idealized failure-resistant memory achieved through replication and robust write protocols, not through any single physical device
- Source: entries/2026/06/19/wiki-Durability_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Durability_(database_systems)

### [ACCEPT] jim-gray-1981-transaction-concept
Jim Gray's 1981 paper 'The Transaction Concept' formally proposed the concept of system reliability encompassing durability, linking it to atomicity and consistency
- Source: entries/2026/06/19/wiki-Durability_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Durability_(database_systems)

### [ACCEPT] dynamo-leaderless-replication
Amazon Dynamo uses leaderless (peer-to-peer) replication where every node has identical responsibilities with no distinguished leader node
- Source: entries/2026/06/19/wiki-Dynamo_storage_system.md
- Source URL: https://en.wikipedia.org/wiki/Dynamo_(storage_system)

### [ACCEPT] dynamo-2004-holiday-origin
Amazon Dynamo was developed internally at Amazon to address scalability issues encountered during the 2004 holiday season, with the paper published in 2007 at SOSP
- Source: entries/2026/06/19/wiki-Dynamo_storage_system.md
- Source URL: https://en.wikipedia.org/wiki/Dynamo_(storage_system)

### [ACCEPT] dynamo-vs-dynamodb-architecture
DynamoDB uses single-leader replication, which is a completely different architecture from Dynamo's leaderless model, despite the similar name
- Source: entries/2026/06/19/wiki-Dynamo_storage_system.md
- Source URL: https://en.wikipedia.org/wiki/Dynamo_(storage_system)

### [ACCEPT] dynamo-five-core-techniques
Dynamo's five core techniques are: consistent hashing (partitioning), vector clocks (write versioning), sloppy quorum with hinted handoff (temporary failures), Merkle trees (permanent failure repair), and gossip protocol (membership/failure detection)
- Source: entries/2026/06/19/wiki-Dynamo_storage_system.md
- Source URL: https://en.wikipedia.org/wiki/Dynamo_(storage_system)

### [ACCEPT] dynamo-favors-availability-over-consistency
Dynamo favors availability over consistency (AP in CAP theorem terms) — writes are always accepted and conflicts are reconciled on read using vector clocks
- Source: entries/2026/06/19/wiki-Dynamo_storage_system.md
- Source URL: https://en.wikipedia.org/wiki/Dynamo_(storage_system)

### [ACCEPT] dynamo-inspired-cassandra-riak-voldemort
The Dynamo paper directly inspired major NoSQL systems including Apache Cassandra, Riak, and Project Voldemort, though Amazon never released Dynamo's implementation
- Source: entries/2026/06/19/wiki-Dynamo_storage_system.md
- Source URL: https://en.wikipedia.org/wiki/Dynamo_(storage_system)

### [ACCEPT] eda-event-is-state-change-not-message
In event-driven architecture, an event is a significant change in state; what is transmitted is an event notification message, not the event itself
- Source: entries/2026/06/19/wiki-Event-driven_architecture.md
- Source URL: https://en.wikipedia.org/wiki/Event-driven_architecture

### [ACCEPT] eda-broker-vs-mediator-topology
EDA has two topologies: broker topology (no orchestrator, higher performance/scalability) and mediator topology (central orchestrator, better control/error handling)
- Source: entries/2026/06/19/wiki-Event-driven_architecture.md
- Source URL: https://en.wikipedia.org/wiki/Event-driven_architecture

### [ACCEPT] eda-domain-vs-integration-events
Domain events are scoped to a single bounded context with lighter payloads; integration events cross bounded contexts with heavier payloads to ensure data consistency across services
- Source: entries/2026/06/19/wiki-Event-driven_architecture.md
- Source URL: https://en.wikipedia.org/wiki/Event-driven_architecture

### [ACCEPT] eda-loose-coupled-semantically-tight
Event-driven architecture is loosely coupled in space, time, and synchronization but semantically coupled through event schemas and subscriptions
- Source: entries/2026/06/19/wiki-Event-driven_architecture.md
- Source URL: https://en.wikipedia.org/wiki/Event-driven_architecture

### [ACCEPT] eda-four-event-flow-layers
The four event flow layers in EDA are: event producer, event channel, event processing engine, and downstream event-driven activity
- Source: entries/2026/06/19/wiki-Event-driven_architecture.md
- Source URL: https://en.wikipedia.org/wiki/Event-driven_architecture

### [ACCEPT] cep-detects-patterns-across-events
Complex event processing (CEP) detects patterns across multiple simple events over time using event correlation (causal, temporal, spatial) to infer higher-order events
- Source: entries/2026/06/19/wiki-Event-driven_architecture.md
- Source URL: https://en.wikipedia.org/wiki/Event-driven_architecture

### [ACCEPT] olep-no-guaranteed-processing-time-bound
Online event processing (OLEP) uses asynchronous distributed event logs for complex scenarios with strong consistency but no guaranteed upper bound on processing time
- Source: entries/2026/06/19/wiki-Event-driven_architecture.md
- Source URL: https://en.wikipedia.org/wiki/Event-driven_architecture

### [ACCEPT] eventual-consistency-liveness-not-safety
Eventual consistency provides only a liveness guarantee (reads will eventually return the same value) but no safety guarantee — any intermediate value may be returned before convergence
- Source: entries/2026/06/19/wiki-Eventual_consistency.md
- Source URL: https://en.wikipedia.org/wiki/Eventual_consistency

### [ACCEPT] base-semantics-definition
BASE stands for Basically Available (concurrent access for all users), Soft-state (data has transient states that change without external input), and Eventually Consistent (convergence after all updates complete)
- Source: entries/2026/06/19/wiki-Eventual_consistency.md
- Source URL: https://en.wikipedia.org/wiki/Eventual_consistency

### [ACCEPT] strong-eventual-consistency-via-crdts
Strong Eventual Consistency (SEC) adds a safety guarantee — any two nodes that received the same unordered set of updates will be in the same state — commonly achieved using conflict-free replicated data types (CRDTs)
- Source: entries/2026/06/19/wiki-Eventual_consistency.md
- Source URL: https://en.wikipedia.org/wiki/Eventual_consistency

### [ACCEPT] conflict-resolution-read-write-async-repair
Reconciliation timing strategies in eventually consistent systems are: read repair (corrects during reads), write repair (corrects during writes), and asynchronous repair (background correction outside read/write paths)
- Source: entries/2026/06/19/wiki-Eventual_consistency.md
- Source URL: https://en.wikipedia.org/wiki/Eventual_consistency

### [ACCEPT] last-writer-wins-most-widespread-conflict-resolution
Last writer wins (LWW) is the most widespread conflict resolution approach in eventually consistent systems, where the update with the latest timestamp takes precedence
- Source: entries/2026/06/19/wiki-Eventual_consistency.md
- Source URL: https://en.wikipedia.org/wiki/Eventual_consistency

### [ACCEPT] external-sort-optimal-io-complexity
Asymptotically optimal external sorting achieves O((N/B) · log_{M/B}(N/B)) I/O operations, where N is data size, M is internal memory size, and B is block size
- Source: entries/2026/06/19/wiki-External_sorting.md
- Source URL: https://en.wikipedia.org/wiki/External_sorting

### [ACCEPT] external-merge-sort-hybrid-strategy
External merge sort uses a hybrid sort-merge strategy: sort phase creates sorted chunks that fit in RAM, merge phase combines them using K-way merge
- Source: entries/2026/06/19/wiki-External_sorting.md
- Source URL: https://en.wikipedia.org/wiki/External_sorting

### [ACCEPT] external-sort-seek-vs-transfer-tradeoff
In external sorting on HDD, a typical 10ms disk seek equals transferring ~1MB at 100 MB/s; buffer sizes below ~1MB mean most time is spent seeking rather than transferring data
- Source: entries/2026/06/19/wiki-External_sorting.md
- Source URL: https://en.wikipedia.org/wiki/External_sorting

### [ACCEPT] doubling-ram-reduces-seeks-75-percent
In external sorting, doubling available RAM reduces disk seeks by approximately 75% because it halves the number of chunks AND halves reads per chunk
- Source: entries/2026/06/19/wiki-External_sorting.md
- Source URL: https://en.wikipedia.org/wiki/External_sorting

### [ACCEPT] replacement-selection-doubles-run-length
The replacement-selection algorithm produces initial sorted runs averaging twice the memory size, halving the number of initial chunks compared to simple in-memory sorting
- Source: entries/2026/06/19/wiki-External_sorting.md
- Source URL: https://en.wikipedia.org/wiki/External_sorting

### [ACCEPT] fsync-flushes-single-fd-data-and-metadata
fsync(fd) flushes buffered data and metadata for a specific file descriptor to non-volatile storage, while fdatasync(fd) flushes only data changes without metadata
- Source: entries/2026/06/19/wiki-Fsync.md
- Source URL: https://en.wikipedia.org/wiki/Fsync

### [ACCEPT] sync-flushes-all-kernel-buffers
The sync() system call flushes all kernel filesystem buffers to non-volatile storage and is declared as void sync(void) in unistd.h
- Source: entries/2026/06/19/wiki-Fsync.md
- Source URL: https://en.wikipedia.org/wiki/Fsync

### [ACCEPT] write-errors-deferred-to-fsync
Write errors in Linux are often not reported at write() time but deferred to fsync(), msync(), or close() — applications must check fsync() return values to detect data loss
- Source: entries/2026/06/19/wiki-Fsync.md
- Source URL: https://en.wikipedia.org/wiki/Fsync

### [ACCEPT] rotating-disk-commits-limited-by-rotation
A rotating hard drive can only commit a durable write once per rotation, limiting single-client durable commits to a few hundred per second
- Source: entries/2026/06/19/wiki-Fsync.md
- Source URL: https://en.wikipedia.org/wiki/Fsync

### [ACCEPT] fua-bypasses-drive-cache-without-full-flush
Force Unit Access (FUA) in SCSI and SATA-NCQ allows the host to ensure specific writes reach disk platters without flushing the entire drive write cache
- Source: entries/2026/06/19/wiki-Fsync.md
- Source URL: https://en.wikipedia.org/wiki/Fsync

### [ACCEPT] ext3-data-ordered-fsync-flushes-entire-fs
On ext3 with data=ordered mode, calling fsync on one file could flush the entire filesystem's write cache, causing performance problems for unrelated I/O (demonstrated by the Firefox/ext3 incident in 2008)
- Source: entries/2026/06/19/wiki-Fsync.md
- Source URL: https://en.wikipedia.org/wiki/Fsync

### [ACCEPT] drive-write-caches-can-lie-about-durability
Storage hardware may report writes as complete when data is only in the drive's volatile write cache, creating a durability gap even when software correctly calls fsync
- Source: entries/2026/06/19/wiki-Fsync.md
- Source URL: https://en.wikipedia.org/wiki/Fsync

### [ACCEPT] wal-pattern-amortizes-fsync-cost
Databases use write-ahead logs (WAL) synced frequently to allow less frequent syncing of main data files, amortizing the cost of fsync as a durability/performance tradeoff
- Source: entries/2026/06/19/wiki-Fsync.md
- Source URL: https://en.wikipedia.org/wiki/Fsync

### [ACCEPT] consistent-cut-no-received-without-sent
A consistent cut in a distributed system requires that for every receive event in the past set, the corresponding send event is also in the past — no message appears received without being sent
- Source: entries/2026/06/19/wiki-Global_state_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Global_state_(computer_science)

### [ACCEPT] chandy-lamport-requires-fifo-channels
The Chandy-Lamport snapshot protocol (1985) requires FIFO channels; Lai-Yang (1987, message colouring) and Mattern (1989, vector clocks) extend snapshot capture to non-FIFO channels
- Source: entries/2026/06/19/wiki-Global_state_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Global_state_(computer_science)

### [ACCEPT] consistent-snapshot-reachability-theorem
The reachability theorem states that any consistent global state S is reachable from the initial state S₀, and the actual current state S' is reachable from S — even if S never simultaneously existed
- Source: entries/2026/06/19/wiki-Global_state_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Global_state_(computer_science)

### [ACCEPT] stable-predicates-detectable-from-snapshot
Stable predicates (properties that once true remain true, such as deadlock, termination, and GC eligibility) can be reliably detected from a single consistent snapshot without pausing the system; unstable predicates cannot
- Source: entries/2026/06/19/wiki-Global_state_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Global_state_(computer_science)

### [ACCEPT] chandy-lamport-marker-before-application-messages
In the Chandy-Lamport protocol, the initiator must send a marker on every outgoing channel before any further application messages — ordering is critical for correctness
- Source: entries/2026/06/19/wiki-Global_state_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Global_state_(computer_science)

### [ACCEPT] global-state-includes-channel-state
Global state of a distributed system is the tuple of all process local states plus all channel states (in-transit messages): GS = (s₁, s₂, …, sₙ, M₁₂, M₁₃, …)
- Source: entries/2026/06/19/wiki-Global_state_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Global_state_(computer_science)

### [ACCEPT] gossip-dissemination-log-n-rounds
Gossip protocols disseminate information to all N nodes in O(log N) rounds through random peer-to-peer exchanges that cause exponential spread
- Source: entries/2026/06/19/wiki-Gossip_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Gossip_protocol

### [ACCEPT] gossip-no-reliable-communication-assumed
Gossip protocols do not assume reliable communication — robustness comes from redundant paths carrying the same information, not from delivery guarantees
- Source: entries/2026/06/19/wiki-Gossip_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Gossip_protocol

### [ACCEPT] gossip-symmetric-decentralized-no-leader
Gossip protocols are symmetric and decentralized — all nodes run the same algorithm with no distinguished roles, leader, or coordinator
- Source: entries/2026/06/19/wiki-Gossip_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Gossip_protocol

### [ACCEPT] gossip-two-families-dissemination-aggregation
Gossip protocols have two families: dissemination protocols (spread data/events) and aggregation protocols (compute network-wide functions like max, min, sum in O(log N) rounds)
- Source: entries/2026/06/19/wiki-Gossip_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Gossip_protocol

### [ACCEPT] gossip-seminal-paper-demers-1987
The seminal gossip protocol paper is Demers et al. (1987), 'Epidemic algorithms for replicated database maintenance', which originated the field
- Source: entries/2026/06/19/wiki-Gossip_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Gossip_protocol

### [ACCEPT] happened-before-strict-partial-order
Lamport's happened-before relation (→) is a strict partial order on events: transitive, irreflexive, and asymmetric (asymmetry derived from transitivity + irreflexivity)
- Source: entries/2026/06/19/wiki-Happened-before.md
- Source URL: https://en.wikipedia.org/wiki/Happened-before

### [ACCEPT] concurrent-events-causally-unrelated
Two events in a distributed system are concurrent if and only if neither happened before the other — concurrency means causally unrelated, not simultaneous
- Source: entries/2026/06/19/wiki-Happened-before.md
- Source URL: https://en.wikipedia.org/wiki/Happened-before

### [ACCEPT] lamport-clocks-one-direction-only
Lamport clocks satisfy a → b implies L(a) < L(b) but NOT the converse; vector clocks satisfy the biconditional (a → b if and only if VC(a) < VC(b) component-wise)
- Source: entries/2026/06/19/wiki-Happened-before.md
- Source URL: https://en.wikipedia.org/wiki/Happened-before

### [ACCEPT] byzantine-faults-prevent-happened-before-detection
Under Byzantine faults, detecting the happened-before relation is provably impossible because Byzantine processes can forge or manipulate causal metadata
- Source: entries/2026/06/19/wiki-Happened-before.md
- Source URL: https://en.wikipedia.org/wiki/Happened-before

### [ACCEPT] lamport-1978-time-clocks-ordering
Lamport's 1978 paper 'Time, Clocks, and the Ordering of Events in a Distributed System' introduced the happened-before relation and is one of the most cited papers in distributed systems
- Source: entries/2026/06/19/wiki-Happened-before.md
- Source URL: https://en.wikipedia.org/wiki/Happened-before

### [ACCEPT] hash-uniformity-most-important-property
Uniformity (even distribution of outputs across the output range) is the most important statistical property of a hash function — uneven distribution degrades hash table performance from O(1) toward O(n)
- Source: entries/2026/06/19/wiki-Hash_function.md
- Source URL: https://en.wikipedia.org/wiki/Hash_function

### [ACCEPT] strict-avalanche-criterion-50pct-bit-flip
The strict avalanche criterion requires that flipping any single input bit changes each output bit with 50% probability
- Source: entries/2026/06/19/wiki-Hash_function.md
- Source URL: https://en.wikipedia.org/wiki/Hash_function

### [ACCEPT] universal-hashing-collision-probability-1-over-m
Universal hashing is a randomized scheme selecting from a family of hash functions such that collision probability for any two keys is 1/m, independent of input distribution
- Source: entries/2026/06/19/wiki-Hash_function.md
- Source URL: https://en.wikipedia.org/wiki/Hash_function

### [ACCEPT] perfect-hash-only-static-key-sets
Perfect hash functions (zero collisions) exist only for static, known key sets and are computationally expensive to find for large sets
- Source: entries/2026/06/19/wiki-Hash_function.md
- Source URL: https://en.wikipedia.org/wiki/Hash_function

### [ACCEPT] multiplicative-hashing-faster-better-than-division
Multiplicative hashing (using irrational constant like golden ratio) is faster and generally better distributed than division hashing, which suffers from CPU cost of division and vulnerability to clustered keys
- Source: entries/2026/06/19/wiki-Hash_function.md
- Source URL: https://en.wikipedia.org/wiki/Hash_function

### [ACCEPT] python-siphash-not-stable-across-runs
Python's hash randomization uses SipHash with a per-process random seed, making hash values non-deterministic across runs and unsuitable for persistence
- Source: entries/2026/06/19/wiki-Hash_function.md
- Source URL: https://en.wikipedia.org/wiki/Hash_function

### [ACCEPT] hash-join-requires-equijoin-predicate
Hash join algorithms require an equijoin predicate and cannot be used for inequality joins
- Source: entries/2026/06/19/wiki-Hash_join.md
- Source URL: https://en.wikipedia.org/wiki/Hash_join

### [ACCEPT] hash-join-build-side-smaller-relation
In a hash join, the smaller relation should be used as the build side to minimize memory usage
- Source: entries/2026/06/19/wiki-Hash_join.md
- Source URL: https://en.wikipedia.org/wiki/Hash_join

### [ACCEPT] classic-hash-join-requires-build-in-memory
Classic hash join requires the entire build relation to fit in memory; when it doesn't, it degenerates into a block nested loop pattern
- Source: entries/2026/06/19/wiki-Hash_join.md
- Source URL: https://en.wikipedia.org/wiki/Hash_join

### [ACCEPT] grace-hash-join-partitions-both-relations
Grace hash join partitions both relations to disk using a hash function on the join key, then joins partition pairs in memory
- Source: entries/2026/06/19/wiki-Hash_join.md
- Source URL: https://en.wikipedia.org/wiki/Hash_join

### [ACCEPT] grace-hash-join-recursive-repartition
Grace hash join applies recursive repartitioning with an orthogonal hash function when a partition still exceeds available memory
- Source: entries/2026/06/19/wiki-Hash_join.md
- Source URL: https://en.wikipedia.org/wiki/Hash_join

### [ACCEPT] hybrid-hash-join-keeps-partition-zero-in-memory
Hybrid hash join keeps partition 0 of the build relation in memory during the partitioning phase, reducing disk I/O compared to Grace hash join
- Source: entries/2026/06/19/wiki-Hash_join.md
- Source URL: https://en.wikipedia.org/wiki/Hash_join

### [ACCEPT] hash-anti-join-evaluates-not-in
Hash anti-join evaluates NOT IN predicates: left anti-join hashes the NOT IN side and selects probe rows with no match; right anti-join hashes the FROM side and removes entries on each hit
- Source: entries/2026/06/19/wiki-Hash_join.md
- Source URL: https://en.wikipedia.org/wiki/Hash_join

### [ACCEPT] hash-table-average-o1-operations
Hash tables provide average-case O(1) time complexity for search, insert, and delete operations, with worst case O(n) when all keys collide into one bucket
- Source: entries/2026/06/19/wiki-Hash_table.md
- Source URL: https://en.wikipedia.org/wiki/Hash_table

### [ACCEPT] hash-table-load-factor-formula
Hash table load factor α = n/m (stored elements divided by total buckets) is the key performance predictor for hash table operations
- Source: entries/2026/06/19/wiki-Hash_table.md
- Source URL: https://en.wikipedia.org/wiki/Hash_table

### [ACCEPT] open-addressing-load-factor-below-one
Open addressing hash tables cannot have load factor α > 1 since each slot holds exactly one item; recommended α_max is 0.6–0.75
- Source: entries/2026/06/19/wiki-Hash_table.md
- Source URL: https://en.wikipedia.org/wiki/Hash_table

### [ACCEPT] separate-chaining-load-factor-can-exceed-one
Separate chaining hash tables can have load factor α > 1, with optimal α_max typically between 1 and 3
- Source: entries/2026/06/19/wiki-Hash_table.md
- Source URL: https://en.wikipedia.org/wiki/Hash_table

### [ACCEPT] hash-table-rehash-trigger-load-factor
Hash table rehashing is triggered when load factor α exceeds α_max; shrinking is triggered when α drops below α_max/4
- Source: entries/2026/06/19/wiki-Hash_table.md
- Source URL: https://en.wikipedia.org/wiki/Hash_table

### [ACCEPT] java-hashmap-bst-buckets-threshold-8
Java's HashMap converts bucket chains from linked lists to self-balancing BSTs when bucket size exceeds 8, reducing worst-case lookup from O(n) to O(log n)
- Source: entries/2026/06/19/wiki-Hash_table.md
- Source URL: https://en.wikipedia.org/wiki/Hash_table

### [ACCEPT] dynamic-perfect-hashing-o1-worst-case
Dynamic perfect hashing guarantees O(1) worst-case lookup using two-level hash tables with k^2 slots per bucket containing k entries
- Source: entries/2026/06/19/wiki-Hash_table.md
- Source URL: https://en.wikipedia.org/wiki/Hash_table

### [ACCEPT] linear-probing-primary-clustering
Linear probing in open addressing hash tables is susceptible to primary clustering, where runs of consecutive occupied slots degrade performance
- Source: entries/2026/06/19/wiki-Hash_table.md
- Source URL: https://en.wikipedia.org/wiki/Hash_table

### [ACCEPT] hyperloglog-1point5kb-for-1e9-cardinality
HyperLogLog can estimate cardinalities exceeding 10^9 with approximately 2% standard error using only 1.5 kB of memory
- Source: entries/2026/06/19/wiki-HyperLogLog.md
- Source URL: https://en.wikipedia.org/wiki/HyperLogLog

### [ACCEPT] hyperloglog-standard-error-formula
HyperLogLog standard error is 1.04/sqrt(m) where m is the number of registers; doubling precision requires 4x the registers
- Source: entries/2026/06/19/wiki-HyperLogLog.md
- Source URL: https://en.wikipedia.org/wiki/HyperLogLog

### [ACCEPT] hyperloglog-merge-is-elementwise-max
HyperLogLog merge operation is element-wise max of register arrays, making it composable across distributed systems where each node maintains a local sketch
- Source: entries/2026/06/19/wiki-HyperLogLog.md
- Source URL: https://en.wikipedia.org/wiki/HyperLogLog

### [ACCEPT] hyperloglog-add-o1-count-merge-om
HyperLogLog Add operation is O(1); Count and Merge operations are O(m) where m is the number of registers
- Source: entries/2026/06/19/wiki-HyperLogLog.md
- Source URL: https://en.wikipedia.org/wiki/HyperLogLog

### [ACCEPT] hyperloglog-small-range-linear-counting
HyperLogLog uses Linear Counting as a fallback for small cardinalities below 5/2 * m, where m is the number of registers
- Source: entries/2026/06/19/wiki-HyperLogLog.md
- Source URL: https://en.wikipedia.org/wiki/HyperLogLog

### [ACCEPT] hllpp-improvements-over-hyperloglog
HLL++ (Google, 2013) improves HyperLogLog with 64-bit hashes (eliminating large-range correction), empirical small-range bias correction, and sparse-to-dense register representation
- Source: entries/2026/06/19/wiki-HyperLogLog.md
- Source URL: https://en.wikipedia.org/wiki/HyperLogLog

### [ACCEPT] hyperloglog-algorithm-lineage
HyperLogLog algorithm lineage: Flajolet-Martin (1984) → LogLog (2003) → HyperLogLog (2007) → HLL++ (2013)
- Source: entries/2026/06/19/wiki-HyperLogLog.md
- Source URL: https://en.wikipedia.org/wiki/HyperLogLog

### [ACCEPT] http-idempotent-methods-get-put-delete
HTTP methods GET, PUT, and DELETE are idempotent; POST is not required to be idempotent
- Source: entries/2026/06/19/wiki-Idempotence.md
- Source URL: https://en.wikipedia.org/wiki/Idempotence

### [ACCEPT] idempotence-not-same-as-safety
Idempotence differs from safety: safe methods (GET) have no side effects; idempotent methods (PUT, DELETE) may have side effects on first call but repeated calls don't change outcome further
- Source: entries/2026/06/19/wiki-Idempotence.md
- Source URL: https://en.wikipedia.org/wiki/Idempotence

### [ACCEPT] idempotent-composition-not-idempotent
Sequential composition of individually idempotent operations is not necessarily idempotent, because later operations may affect values that earlier operations depend on
- Source: entries/2026/06/19/wiki-Idempotence.md
- Source URL: https://en.wikipedia.org/wiki/Idempotence

### [ACCEPT] idempotence-requires-unique-identification
PUT and DELETE idempotence requires targeting a uniquely identified resource; requests targeting 'the most recent record' rather than a specific ID break idempotence
- Source: entries/2026/06/19/wiki-Idempotence.md
- Source URL: https://en.wikipedia.org/wiki/Idempotence

### [ACCEPT] idempotence-enables-safe-retries-distributed
Idempotent operations can be retried without tracking whether they were already performed, enabling at-least-once delivery semantics in distributed systems
- Source: entries/2026/06/19/wiki-Idempotence.md
- Source URL: https://en.wikipedia.org/wiki/Idempotence

### [ACCEPT] isolation-levels-phenomena-matrix
SQL isolation levels prevent phenomena in order: Serializable prevents all three (dirty/non-repeatable/phantom reads); Repeatable Read allows phantom reads; Read Committed allows non-repeatable and phantom reads; Read Uncommitted allows all three
- Source: entries/2026/06/19/wiki-Isolation_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Isolation_(database_systems)

### [ACCEPT] write-skew-not-covered-by-ansi-phenomena
Write skew is a concurrency anomaly not covered by the three ANSI SQL phenomena; it can occur under Repeatable Read and is only prevented at Serializable level
- Source: entries/2026/06/19/wiki-Isolation_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Isolation_(database_systems)

### [ACCEPT] serializable-requires-range-locks-or-write-conflict-detection
Serializable isolation requires range-locks (in lock-based systems) or write-collision detection (in MVCC systems) to prevent all read phenomena
- Source: entries/2026/06/19/wiki-Isolation_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Isolation_(database_systems)

### [ACCEPT] default-isolation-levels-by-dbms
Default isolation levels: PostgreSQL uses Read Committed, MySQL/InnoDB uses Repeatable Read, Oracle uses Read Committed, SQL Server uses Read Committed
- Source: entries/2026/06/19/wiki-Isolation_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Isolation_(database_systems)

### [ACCEPT] ansi-phenomena-free-not-sufficient-serializability
Being free of all three ANSI SQL phenomena (dirty reads, non-repeatable reads, phantom reads) is necessary but not sufficient for true serializability
- Source: entries/2026/06/19/wiki-Isolation_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Isolation_(database_systems)

### [ACCEPT] read-committed-releases-read-locks-immediately
Read Committed isolation releases read locks immediately after the SELECT completes while holding write locks until commit
- Source: entries/2026/06/19/wiki-Isolation_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Isolation_(database_systems)

### [ACCEPT] ansi-sql-isolation-criticized-lock-biased
The ANSI SQL isolation level definitions are criticized as ambiguous and lock-biased, not accurately capturing behavior of real MVCC-based systems (per Berenson et al. 'A Critique of ANSI SQL Isolation Levels')
- Source: entries/2026/06/19/wiki-Isolation_database_systems.md
- Source URL: https://en.wikipedia.org/wiki/Isolation_(database_systems)

### [ACCEPT] journaling-fs-write-ahead-log-for-crash-recovery
Journaling file systems record pending changes to a dedicated log (journal) before committing them to the main file system, enabling crash recovery by replaying the journal instead of running a full fsck.
- Source: entries/2026/06/19/wiki-Journaling_file_system.md
- Source URL: https://en.wikipedia.org/wiki/Journaling_file_system

### [ACCEPT] journaling-physical-vs-logical-tradeoff
Physical journaling logs every changed block (write-twice penalty, full data+metadata protection), while logical/metadata-only journaling logs only metadata changes (better write performance, but file data can be corrupted after a crash).
- Source: entries/2026/06/19/wiki-Journaling_file_system.md
- Source URL: https://en.wikipedia.org/wiki/Journaling_file_system

### [ACCEPT] journaling-journal-entries-atomic
Journal entries are atomic: they either complete fully and are replayed on recovery, or are discarded entirely when incomplete writes are detected via missing or mismatched checksums.
- Source: entries/2026/06/19/wiki-Journaling_file_system.md
- Source URL: https://en.wikipedia.org/wiki/Journaling_file_system

### [ACCEPT] journaling-three-step-delete-problem
Deleting a file requires removing the directory entry, freeing the inode, and freeing disk blocks — no ordering of these three steps prevents all possible corruption scenarios without journaling.
- Source: entries/2026/06/19/wiki-Journaling_file_system.md
- Source URL: https://en.wikipedia.org/wiki/Journaling_file_system

### [ACCEPT] ext4-jbd2-checksum-bracketing
JBD2 (ext4's journaling layer) wraps each logged change with a checksum so that partially written journal entries are detected and skipped during replay.
- Source: entries/2026/06/19/wiki-Journaling_file_system.md
- Source URL: https://en.wikipedia.org/wiki/Journaling_file_system

### [ACCEPT] ext3-ext4-write-barriers-cache-flush
ext3/ext4 use write barriers to force device cache flushes at critical journal points, preventing hardware write reordering from breaking journal consistency guarantees.
- Source: entries/2026/06/19/wiki-Journaling_file_system.md
- Source URL: https://en.wikipedia.org/wiki/Journaling_file_system

### [ACCEPT] cow-fs-no-journaling-needed
Copy-on-write file systems (ZFS, Btrfs) achieve crash consistency without journaling by never modifying data in place — new data is written to fresh blocks, then metadata pointers are updated atomically.
- Source: entries/2026/06/19/wiki-Journaling_file_system.md
- Source URL: https://en.wikipedia.org/wiki/Journaling_file_system

### [ACCEPT] ibm-jfs-first-commercial-unix-journaling-fs-1990
IBM JFS in AIX 3.1 (1990) was among the first commercial UNIX journaling file systems.
- Source: entries/2026/06/19/wiki-Journaling_file_system.md
- Source URL: https://en.wikipedia.org/wiki/Journaling_file_system

### [ACCEPT] lamport-timestamp-one-way-implication
Lamport timestamps satisfy the clock consistency condition in one direction only: if event a happened-before event b then C(a) < C(b), but C(a) < C(b) does NOT imply a happened-before b.
- Source: entries/2026/06/19/wiki-Lamport_timestamp.md
- Source URL: https://en.wikipedia.org/wiki/Lamport_timestamp

### [ACCEPT] lamport-clock-receive-rule-max-plus-one
On message receipt, a Lamport clock sets its counter to max(local_counter, message_timestamp) + 1, not simply incremented.
- Source: entries/2026/06/19/wiki-Lamport_timestamp.md
- Source URL: https://en.wikipedia.org/wiki/Lamport_timestamp

### [ACCEPT] lamport-clocks-partial-order-only
Lamport timestamps establish only a partial order over events; events in processes that never exchange messages are concurrent and cannot be ordered.
- Source: entries/2026/06/19/wiki-Lamport_timestamp.md
- Source URL: https://en.wikipedia.org/wiki/Lamport_timestamp

### [ACCEPT] vector-clocks-strong-clock-consistency
Vector clocks provide strong clock consistency (both directions): if C(a) < C(b) then a happened-before b — a property Lamport clocks lack.
- Source: entries/2026/06/19/wiki-Lamport_timestamp.md
- Source URL: https://en.wikipedia.org/wiki/Lamport_timestamp

### [ACCEPT] lamport-total-order-via-process-id-tiebreak
A total order can be constructed from Lamport timestamps by breaking ties with process IDs, but this artificial ordering does not imply causality.
- Source: entries/2026/06/19/wiki-Lamport_timestamp.md
- Source URL: https://en.wikipedia.org/wiki/Lamport_timestamp

### [ACCEPT] lamport-seminal-paper-1978-cacm
Lamport timestamps were introduced in 'Time, Clocks, and the Ordering of Events in a Distributed System' (1978), published in Communications of the ACM.
- Source: entries/2026/06/19/wiki-Lamport_timestamp.md
- Source URL: https://en.wikipedia.org/wiki/Lamport_timestamp

### [ACCEPT] leader-election-three-properties
Leader election requires three correctness properties: Termination (finishes in finite time), Uniqueness (exactly one leader), and Agreement (all others know who the leader is).
- Source: entries/2026/06/19/wiki-Leader_election.md
- Source URL: https://en.wikipedia.org/wiki/Leader_election

### [ACCEPT] anonymous-ring-deterministic-election-impossible
No deterministic algorithm can elect a leader in anonymous rings (even with known ring size), because identical initial states produce identical transitions at every round, so all nodes reach the same final state.
- Source: entries/2026/06/19/wiki-Leader_election.md
- Source URL: https://en.wikipedia.org/wiki/Leader_election

### [ACCEPT] chang-roberts-ring-election-n-squared
The Chang-Roberts ring election algorithm has O(n²) worst-case message complexity: each node sends its ID clockwise, forwards received IDs greater than its own, and discards smaller ones.
- Source: entries/2026/06/19/wiki-Leader_election.md
- Source URL: https://en.wikipedia.org/wiki/Leader_election

### [ACCEPT] hirschberg-sinclair-ring-election-n-log-n
The Hirschberg-Sinclair algorithm improves ring election to O(n log n) messages using bidirectional probing in exponentially growing neighborhoods across ceil(log(n-1)) phases.
- Source: entries/2026/06/19/wiki-Leader_election.md
- Source URL: https://en.wikipedia.org/wiki/Leader_election

### [ACCEPT] leader-election-building-block-for-consensus
Leader election is a building block for consensus protocols — once a leader is elected, it can coordinate agreement among nodes.
- Source: entries/2026/06/19/wiki-Leader_election.md
- Source URL: https://en.wikipedia.org/wiki/Leader_election

### [ACCEPT] leveldb-embedded-library-not-server
LevelDB is an embedded C++ library that applications link against directly — it is not a standalone server process and has no network protocol or CLI.
- Source: entries/2026/06/19/wiki-LevelDB.md
- Source URL: https://en.wikipedia.org/wiki/LevelDB

### [ACCEPT] leveldb-lsm-tree-from-bigtable-design
LevelDB is based on log-structured merge-tree (LSM-tree) design derived from Google Bigtable's tablet stack, making it write-optimized at the cost of read amplification.
- Source: entries/2026/06/19/wiki-LevelDB.md
- Source URL: https://en.wikipedia.org/wiki/LevelDB

### [ACCEPT] leveldb-sorted-key-value-store
LevelDB stores data sorted by key (arbitrary byte arrays), enabling efficient sequential reads and range queries.
- Source: entries/2026/06/19/wiki-LevelDB.md
- Source URL: https://en.wikipedia.org/wiki/LevelDB

### [ACCEPT] rocksdb-is-leveldb-fork-by-facebook
RocksDB is Facebook's fork of LevelDB with significant performance and feature enhancements including compaction improvements and column families.
- Source: entries/2026/06/19/wiki-LevelDB.md
- Source URL: https://en.wikipedia.org/wiki/LevelDB

### [ACCEPT] leveldb-vs-lmdb-lsm-vs-btree
LevelDB (LSM-tree) vs LMDB (B+ tree) illustrates the classic write-optimized vs read-optimized storage engine tradeoff: LevelDB excels at writes, LMDB is ~10x faster for reads.
- Source: entries/2026/06/19/wiki-LevelDB.md
- Source URL: https://en.wikipedia.org/wiki/LevelDB

### [ACCEPT] leveldb-chrome-indexeddb-backend
LevelDB serves as the storage backend for Chrome's IndexedDB implementation, which was its original motivating use case.
- Source: entries/2026/06/19/wiki-LevelDB.md
- Source URL: https://en.wikipedia.org/wiki/LevelDB

### [ACCEPT] linear-hashing-one-bucket-at-a-time-predetermined-order
Linear hashing grows one bucket at a time in a predetermined sequential order (tracked by a split pointer), unlike extendible hashing which splits only the overflowing bucket.
- Source: entries/2026/06/19/wiki-Linear_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Linear_hashing

### [ACCEPT] linear-hashing-state-level-and-split-pointer
Linear hashing file state is fully captured by two values: level l and split pointer s, with the total number of buckets n = 2^l + s.
- Source: entries/2026/06/19/wiki-Linear_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Linear_hashing

### [ACCEPT] linear-hashing-two-hash-functions-active
Linear hashing uses two hash functions simultaneously: buckets before the split pointer use h_{l+1} (already split), buckets at or after use h_l, with the address check if (a < s) determining which function to apply.
- Source: entries/2026/06/19/wiki-Linear_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Linear_hashing

### [ACCEPT] linear-hashing-operations-constant-time
Linear hashing provides O(1) key-based insert, delete, update, and read operations regardless of the number of records or buckets.
- Source: entries/2026/06/19/wiki-Linear_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Linear_hashing

### [ACCEPT] linear-hashing-invented-litwin-1980
Linear hashing was invented by Witold Litwin in 1980 as the foundational scheme in a family of dynamic hashing algorithms.
- Source: entries/2026/06/19/wiki-Linear_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Linear_hashing

### [ACCEPT] linear-hashing-distributed-lh-star-two-forwards-max
LH* extends linear hashing to distributed systems where each bucket resides on a different server; misrouted requests require at most two forwards, and clients self-correct via Image Adjustment Messages.
- Source: entries/2026/06/19/wiki-Linear_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Linear_hashing

### [ACCEPT] linearizability-introduced-herlihy-wing-1987
Linearizability was introduced by Herlihy and Wing in 1987 as a correctness condition for concurrent programming.
- Source: entries/2026/06/19/wiki-Linearizability.md
- Source URL: https://en.wikipedia.org/wiki/Linearizability

### [ACCEPT] linearizability-equals-serializability-plus-realtime-order
Linearizability equals serializability plus the constraint that real-time ordering of non-overlapping operations must be preserved.
- Source: entries/2026/06/19/wiki-Linearizability.md
- Source URL: https://en.wikipedia.org/wiki/Linearizability

### [ACCEPT] linearizability-composes-serializability-does-not
Linearizability composes across multiple objects (individually linearizable objects remain linearizable together), while serializability does not have this composability property.
- Source: entries/2026/06/19/wiki-Linearizability.md
- Source URL: https://en.wikipedia.org/wiki/Linearizability

### [ACCEPT] linearization-point-cas-is-successful-cas
For CAS-based algorithms, the linearization point is the successful compare-and-swap instruction; for lock-based algorithms, it is any point while the lock is held.
- Source: entries/2026/06/19/wiki-Linearizability.md
- Source URL: https://en.wikipedia.org/wiki/Linearizability

### [ACCEPT] sig-atomic-t-no-atomic-increment
C's sig_atomic_t guarantees atomic reads and writes but does not guarantee atomic increment or decrement operations.
- Source: entries/2026/06/19/wiki-Linearizability.md
- Source URL: https://en.wikipedia.org/wiki/Linearizability

### [ACCEPT] disabling-interrupts-insufficient-multiprocessor-atomicity
Disabling interrupts achieves atomicity on uniprocessors but is insufficient for multiprocessors because each CPU can interfere independently.
- Source: entries/2026/06/19/wiki-Linearizability.md
- Source URL: https://en.wikipedia.org/wiki/Linearizability

### [ACCEPT] linearizability-is-safety-property
Linearizability is a safety property — it ensures operations do not produce unexpected results, rather than guaranteeing progress.
- Source: entries/2026/06/19/wiki-Linearizability.md
- Source URL: https://en.wikipedia.org/wiki/Linearizability

### [ACCEPT] arm-ldrex-strex-fail-on-context-switch
ARM's LDREX/STREX exclusive load/store instructions will fail on context switch, requiring retry — this is by design for correctness.
- Source: entries/2026/06/19/wiki-Linearizability.md
- Source URL: https://en.wikipedia.org/wiki/Linearizability

### [ACCEPT] optimal-dag-task-scheduling-np-hard
Finding the optimal execution order for tasks with dependencies forming a directed acyclic graph (DAG) is NP-hard.
- Source: entries/2026/06/19/wiki-Load_balancing_computing.md
- Source URL: https://en.wikipedia.org/wiki/Load_balancing_(computing)

### [ACCEPT] prefix-sum-optimal-static-load-distribution-log-time
The prefix sum algorithm achieves optimal static load distribution across processors in logarithmic time when tasks are divisible and execution times are known.
- Source: entries/2026/06/19/wiki-Load_balancing_computing.md
- Source URL: https://en.wikipedia.org/wiki/Load_balancing_(computing)

### [ACCEPT] work-stealing-direction-depends-on-load
In work stealing, when the network is heavily loaded, least-loaded nodes should offer availability; when lightly loaded, overloaded nodes should request help — this minimizes message exchange.
- Source: entries/2026/06/19/wiki-Load_balancing_computing.md
- Source URL: https://en.wikipedia.org/wiki/Load_balancing_(computing)

### [ACCEPT] master-worker-scalability-bottleneck
The master-worker load balancing pattern is a scalability bottleneck because the master becomes overloaded with communication as processor count grows.
- Source: entries/2026/06/19/wiki-Load_balancing_computing.md
- Source URL: https://en.wikipedia.org/wiki/Load_balancing_(computing)

### [ACCEPT] moldable-vs-malleable-algorithms
Moldable algorithms adapt to different processor counts but require fixing the count before execution; malleable algorithms handle processor count changes during execution.
- Source: entries/2026/06/19/wiki-Load_balancing_computing.md
- Source URL: https://en.wikipedia.org/wiki/Load_balancing_(computing)

### [ACCEPT] power-of-two-choices-load-balancing
Power of two choices is a load balancing algorithm that picks two random servers and routes to the less loaded one, dramatically improving over pure random selection.
- Source: entries/2026/06/19/wiki-Load_balancing_computing.md
- Source URL: https://en.wikipedia.org/wiki/Load_balancing_(computing)

### [ACCEPT] round-robin-dns-caching-skew
Round-robin DNS load balancing suffers from DNS caching skew, where intermediate caches cause uneven distribution; client-side random selection is unaffected by caching.
- Source: entries/2026/06/19/wiki-Load_balancing_computing.md
- Source URL: https://en.wikipedia.org/wiki/Load_balancing_(computing)

### [ACCEPT] lsm-tree-invented-1996-oneil-et-al
The LSM tree was invented in 1996 by Patrick O'Neil, Edward Cheng, Dieter Gawlick, and Elizabeth O'Neil.
- Source: entries/2026/06/19/wiki-Log-structured_merge-tree.md
- Source URL: https://en.wikipedia.org/wiki/Log-structured_merge-tree

### [ACCEPT] lsm-tree-c0-memory-c1-disk
An LSM tree maintains a small memory-resident sorted structure (C0) and a larger disk-resident structure (C1); new records go into C0 first and are flushed to C1 when a size threshold is exceeded.
- Source: entries/2026/06/19/wiki-Log-structured_merge-tree.md
- Source URL: https://en.wikipedia.org/wiki/Log-structured_merge-tree

### [ACCEPT] lsm-tree-sequential-writes-key-insight
LSM trees convert random writes into sequential writes by batching and merging, which is why they outperform B-trees for write-heavy workloads.
- Source: entries/2026/06/19/wiki-Log-structured_merge-tree.md
- Source URL: https://en.wikipedia.org/wiki/Log-structured_merge-tree

### [ACCEPT] lsm-tree-tombstones-for-deletes
LSM trees use tombstone entries to record deletes because disk components are immutable — deletes cannot modify existing sorted runs in place.
- Source: entries/2026/06/19/wiki-Log-structured_merge-tree.md
- Source URL: https://en.wikipedia.org/wiki/Log-structured_merge-tree

### [ACCEPT] lsm-tree-bloom-filters-critical-for-reads
Bloom filters are critical for LSM tree read performance: without them point lookups are O(L) across levels; with them, existing key lookups approach O(1).
- Source: entries/2026/06/19/wiki-Log-structured_merge-tree.md
- Source URL: https://en.wikipedia.org/wiki/Log-structured_merge-tree

### [ACCEPT] lsm-leveling-vs-tiering-tradeoff
LSM tree leveling compaction has one component per level with frequent merges (better reads, higher write amplification); tiering has multiple components per level with less frequent merges (lower write amplification, higher read cost).
- Source: entries/2026/06/19/wiki-Log-structured_merge-tree.md
- Source URL: https://en.wikipedia.org/wiki/Log-structured_merge-tree

### [ACCEPT] lsm-tree-updates-are-new-writes
In LSM trees, updates are treated as new writes rather than in-place modifications, with older versions resolved during compaction.
- Source: entries/2026/06/19/wiki-Log-structured_merge-tree.md
- Source URL: https://en.wikipedia.org/wiki/Log-structured_merge-tree

### [ACCEPT] logical-clocks-lamport-1978
Logical clocks were introduced by Leslie Lamport in 1978 to capture chronological and causal ordering of events in distributed systems without a shared physical clock.
- Source: entries/2026/06/19/wiki-Logical_clock.md
- Source URL: https://en.wikipedia.org/wiki/Logical_clock

### [ACCEPT] logical-clock-two-data-structures-per-process
Each process in a logical clock system maintains two data structures: logical local time (timestamps its own events) and logical global time (its local view of global time).
- Source: entries/2026/06/19/wiki-Logical_clock.md
- Source URL: https://en.wikipedia.org/wiki/Logical_clock

### [ACCEPT] logical-clock-hierarchy-lamport-vector-version-matrix
The four logical clock algorithms in increasing power are: Lamport timestamps (total order with arbitrary tie-breaking), vector clocks (partial order, detect causality), version vectors (replica ordering), and matrix clocks (global view of vector clocks).
- Source: entries/2026/06/19/wiki-Logical_clock.md
- Source URL: https://en.wikipedia.org/wiki/Logical_clock

### [ACCEPT] non-interacting-processes-no-sync-needed
In distributed systems, if two processes never interact, their lack of clock synchronization is unobservable — agreement on event ordering is sufficient.
- Source: entries/2026/06/19/wiki-Logical_clock.md
- Source URL: https://en.wikipedia.org/wiki/Logical_clock

### [ACCEPT] mapreduce-value-is-scalability-fault-tolerance
MapReduce's primary contribution is scalability and fault tolerance through parallelization, not the map/reduce primitives themselves.
- Source: entries/2026/06/19/wiki-MapReduce.md
- Source URL: https://en.wikipedia.org/wiki/MapReduce

### [ACCEPT] mapreduce-reduce-must-be-monoid
The MapReduce reduce operation must be associative with a neutral element (a monoid) for correctness under arbitrary regrouping.
- Source: entries/2026/06/19/wiki-MapReduce.md
- Source URL: https://en.wikipedia.org/wiki/MapReduce

### [ACCEPT] mapreduce-average-requires-counting-trick
Computing averages in MapReduce requires carrying both sum and count through reduce stages (the counting trick); directly re-reducing averages produces incorrect results due to the weighted average problem.
- Source: entries/2026/06/19/wiki-MapReduce.md
- Source URL: https://en.wikipedia.org/wiki/MapReduce

### [ACCEPT] mapreduce-shuffle-often-dominates-cost
The shuffle phase in MapReduce often dominates total job cost, with communication cost frequently exceeding computation cost.
- Source: entries/2026/06/19/wiki-MapReduce.md
- Source URL: https://en.wikipedia.org/wiki/MapReduce

### [ACCEPT] mapreduce-input-splits-64-128-mb
MapReduce input splits are typically 64–128 MB per split, with one split assigned per mapper.
- Source: entries/2026/06/19/wiki-MapReduce.md
- Source URL: https://en.wikipedia.org/wiki/MapReduce

### [ACCEPT] mapreduce-partition-function-hash-mod
MapReduce's default partition function is hash(key) mod num_reducers; skewed partitioning creates straggler reducers.
- Source: entries/2026/06/19/wiki-MapReduce.md
- Source URL: https://en.wikipedia.org/wiki/MapReduce

### [ACCEPT] google-deprecated-mapreduce-by-2014
Google deprecated MapReduce as its primary big data processing model by 2014, replacing it with streaming/incremental systems (Percolator, FlumeJava, MillWheel).
- Source: entries/2026/06/19/wiki-MapReduce.md
- Source URL: https://en.wikipedia.org/wiki/MapReduce

### [ACCEPT] mapreduce-stateless-acyclic-dataflow
MapReduce programs are stateless and acyclic dataflow programs (stateless mapper to stateless reducer), making iterative algorithms like graph processing and ML training loops difficult to express.
- Source: entries/2026/06/19/wiki-MapReduce.md
- Source URL: https://en.wikipedia.org/wiki/MapReduce

### [ACCEPT] mapreduce-combiners-local-preaggregation
MapReduce combiners perform local pre-aggregation on the mapper side before the shuffle phase, reducing intermediate data volume transmitted across the network.
- Source: entries/2026/06/19/wiki-MapReduce.md
- Source URL: https://en.wikipedia.org/wiki/MapReduce

### [ACCEPT] materialized-view-stores-physical-table
A materialized view stores precomputed query results as a physical table, unlike a regular (virtual) view which re-executes its defining query on each access.
- Source: entries/2026/06/19/wiki-Materialized_view.md
- Source URL: https://en.wikipedia.org/wiki/Materialized_view

### [ACCEPT] materialized-view-tradeoff-reads-vs-freshness
Materialized views trade faster read performance for extra storage cost and potential data staleness, since the materialized result may not reflect the latest base table changes.
- Source: entries/2026/06/19/wiki-Materialized_view.md
- Source URL: https://en.wikipedia.org/wiki/Materialized_view

### [ACCEPT] materialized-view-indexes-any-column
Indexes can be built on any column of a materialized view, whereas regular views can typically only exploit indexes from their underlying base tables.
- Source: entries/2026/06/19/wiki-Materialized_view.md
- Source URL: https://en.wikipedia.org/wiki/Materialized_view

### [ACCEPT] postgresql-materialized-view-manual-refresh
PostgreSQL materialized views (introduced in v9.3) require manual refresh via REFRESH MATERIALIZED VIEW; the CONCURRENTLY option (v9.4+) allows non-blocking refresh but requires a unique index.
- Source: entries/2026/06/19/wiki-Materialized_view.md
- Source URL: https://en.wikipedia.org/wiki/Materialized_view

### [ACCEPT] sql-server-indexed-views-always-synchronized
SQL Server's indexed views are always synchronized with base tables (no manual refresh needed), but require deterministic mappings and SCHEMABINDING.
- Source: entries/2026/06/19/wiki-Materialized_view.md
- Source URL: https://en.wikipedia.org/wiki/Materialized_view

### [ACCEPT] oracle-materialized-view-fast-refresh
Oracle supports REFRESH FAST (incremental) for materialized views and scheduled automatic refresh using NEXT SYSDATE + interval syntax.
- Source: entries/2026/06/19/wiki-Materialized_view.md
- Source URL: https://en.wikipedia.org/wiki/Materialized_view

### [ACCEPT] mysql-no-native-materialized-views
MySQL does not natively support materialized views; workarounds use triggers, stored procedures, or external tools like Flexviews.
- Source: entries/2026/06/19/wiki-Materialized_view.md
- Source URL: https://en.wikipedia.org/wiki/Materialized_view

### [ACCEPT] stream-processing-materialized-views-continuous
In stream processing, materialized views represent continuously maintained query results over unbounded data streams, implemented by systems like Kafka Streams, Flink, Materialize, and RisingWave.
- Source: entries/2026/06/19/wiki-Materialized_view.md
- Source URL: https://en.wikipedia.org/wiki/Materialized_view

### [ACCEPT] merkle-tree-verification-log-n
Verifying that a leaf belongs to a Merkle tree requires O(log n) hash computations, compared to O(n) for a flat hash list.
- Source: entries/2026/06/19/wiki-Merkle_tree.md
- Source URL: https://en.wikipedia.org/wiki/Merkle_tree

### [ACCEPT] merkle-tree-root-hash-trust-model
In a Merkle tree, the root hash must come from a trusted source; all other tree data can be fetched from untrusted sources and verified against it.
- Source: entries/2026/06/19/wiki-Merkle_tree.md
- Source URL: https://en.wikipedia.org/wiki/Merkle_tree

### [ACCEPT] merkle-tree-second-preimage-attack-mitigation
Merkle trees are vulnerable to second preimage attacks because the root hash does not encode tree depth; Certificate Transparency mitigates this by prepending 0x00 to leaf hashes and 0x01 to internal node hashes.
- Source: entries/2026/06/19/wiki-Merkle_tree.md
- Source URL: https://en.wikipedia.org/wiki/Merkle_tree

### [ACCEPT] merkle-tree-anti-entropy-distributed-databases
Cassandra, Riak, and Dynamo use Merkle trees for anti-entropy repair: replicas exchange Merkle trees to hierarchically identify divergent key ranges, minimizing data transfer during synchronization.
- Source: entries/2026/06/19/wiki-Merkle_tree.md
- Source URL: https://en.wikipedia.org/wiki/Merkle_tree

### [ACCEPT] git-uses-merkle-dag-not-tree
Git uses a Merkle DAG (directed acyclic graph where objects reference parents by hash), not strictly a Merkle tree.
- Source: entries/2026/06/19/wiki-Merkle_tree.md
- Source URL: https://en.wikipedia.org/wiki/Merkle_tree

### [ACCEPT] merkle-tree-invented-ralph-merkle-1979
Merkle trees were invented by Ralph Merkle and patented in 1979 (US Patent 4,309,569).
- Source: entries/2026/06/19/wiki-Merkle_tree.md
- Source URL: https://en.wikipedia.org/wiki/Merkle_tree

### [ACCEPT] message-broker-primary-benefit-decoupling
The primary architectural benefit of a message broker is decoupling: applications communicate through the broker without needing to know about each other.
- Source: entries/2026/06/19/wiki-Message_broker.md
- Source URL: https://en.wikipedia.org/wiki/Message_broker

### [ACCEPT] message-broker-two-architectures
Message brokers follow two fundamental architectures: hub-and-spoke (central server provides integration) and message bus (distributed communication backbone).
- Source: entries/2026/06/19/wiki-Message_broker.md
- Source URL: https://en.wikipedia.org/wiki/Message_broker

### [ACCEPT] message-broker-building-block-of-mom
Message brokers are a building block of message-oriented middleware (MOM) but are not a replacement for traditional middleware like MOM and RPC.
- Source: entries/2026/06/19/wiki-Message_broker.md
- Source URL: https://en.wikipedia.org/wiki/Message_broker

### [ACCEPT] rabbitmq-erlang-nats-go-redpanda-cpp
RabbitMQ is written in Erlang, NATS in Go, and Redpanda in C++ (Kafka API-compatible).
- Source: entries/2026/06/19/wiki-Message_broker.md
- Source URL: https://en.wikipedia.org/wiki/Message_broker

### [ACCEPT] multi-master-all-nodes-accept-writes
In multi-master replication, all nodes accept both reads and writes; the system handles propagation and conflict resolution. This contrasts with master-slave (single writer) and failover clustering (passive replicas).
- Source: entries/2026/06/19/wiki-Multi-master_replication.md
- Source URL: https://en.wikipedia.org/wiki/Multi-master_replication

### [ACCEPT] multi-master-async-violates-acid
Most multi-master replication systems use lazy/asynchronous replication, which violates ACID properties in favor of availability; synchronous replication (e.g., two-phase commit) maintains ACID but adds latency.
- Source: entries/2026/06/19/wiki-Multi-master_replication.md
- Source URL: https://en.wikipedia.org/wiki/Multi-master_replication

### [ACCEPT] galera-cluster-synchronous-no-conflicts
Galera Cluster provides synchronous multi-master replication so that no conflicts are possible by design.
- Source: entries/2026/06/19/wiki-Multi-master_replication.md
- Source URL: https://en.wikipedia.org/wiki/Multi-master_replication

### [ACCEPT] couchdb-replication-http-mvcc-last-revision
CouchDB replication is HTTP-based, uses append-only storage with MVCC and revision IDs for conflict detection, and replicates only the last revision of each document.
- Source: entries/2026/06/19/wiki-Multi-master_replication.md
- Source URL: https://en.wikipedia.org/wiki/Multi-master_replication

### [ACCEPT] postgresql-bdr-crdt-column-conflict
PostgreSQL BDR (Bi-Directional Replication) supports column-level conflict detection, CRDTs, eager replication, DDL replication, and online upgrades.
- Source: entries/2026/06/19/wiki-Multi-master_replication.md
- Source URL: https://en.wikipedia.org/wiki/Multi-master_replication

### [ACCEPT] mariadb-multi-master-no-conflict-resolution
MariaDB multi-master replication (10.0+) does not support conflict resolution; each master must contain different databases.
- Source: entries/2026/06/19/wiki-Multi-master_replication.md
- Source URL: https://en.wikipedia.org/wiki/Multi-master_replication

### [ACCEPT] mvcc-reads-never-block-writes
MVCC never blocks reads: read transactions use a timestamp or transaction ID to determine which version to read, requiring no locks, allowing reads and writes to proceed concurrently.
- Source: entries/2026/06/19/wiki-Multiversion_concurrency_control.md
- Source URL: https://en.wikipedia.org/wiki/Multiversion_concurrency_control

### [ACCEPT] mvcc-creates-new-version-no-overwrite
MVCC creates a new version of a data item on update rather than overwriting the original; multiple versions coexist until garbage collected.
- Source: entries/2026/06/19/wiki-Multiversion_concurrency_control.md
- Source URL: https://en.wikipedia.org/wiki/Multiversion_concurrency_control

### [ACCEPT] mvcc-write-abort-rule-timestamp
In MVCC with timestamp ordering, a write to object P by transaction Ti is aborted if TS(Ti) < RTS(P) — meaning a later transaction already read the old value and the write would violate consistency.
- Source: entries/2026/06/19/wiki-Multiversion_concurrency_control.md
- Source URL: https://en.wikipedia.org/wiki/Multiversion_concurrency_control

### [ACCEPT] mvcc-snapshot-isolation-common-level
Snapshot isolation is the most common isolation level implemented via MVCC, where each transaction observes the database state as of when the transaction started.
- Source: entries/2026/06/19/wiki-Multiversion_concurrency_control.md
- Source URL: https://en.wikipedia.org/wiki/Multiversion_concurrency_control

### [ACCEPT] postgresql-vacuum-reclaims-mvcc-versions
PostgreSQL uses VACUUM (including VACUUM FREEZE) to reclaim space from obsolete MVCC versions (dead tuples); undo-log-based systems risk undo log exhaustion under heavy writes.
- Source: entries/2026/06/19/wiki-Multiversion_concurrency_control.md
- Source URL: https://en.wikipedia.org/wiki/Multiversion_concurrency_control

### [ACCEPT] mvcc-first-described-reed-1978
MVCC was first described academically by David P. Reed in his 1978 MIT dissertation and formalized by Bernstein and Goodman in 1981; the first commercial implementation was VAX Rdb/ELN (1984) by Jim Starkey at DEC.
- Source: entries/2026/06/19/wiki-Multiversion_concurrency_control.md
- Source URL: https://en.wikipedia.org/wiki/Multiversion_concurrency_control

### [ACCEPT] network-partition-nodes-still-function
A network partition means nodes lose the ability to communicate across the partition boundary, but nodes within each partition continue to function normally
- Source: entries/2026/06/19/wiki-Network_partitioning.md
- Source URL: https://en.wikipedia.org/wiki/Network_partitioning

### [ACCEPT] cap-theorem-partition-tolerance-is-p
Partition tolerance is the 'P' in the CAP theorem, which states a distributed system can provide at most two of three guarantees: Consistency, Availability, and Partition Tolerance
- Source: entries/2026/06/19/wiki-Network_partitioning.md
- Source URL: https://en.wikipedia.org/wiki/Network_partitioning

### [ACCEPT] cap-real-choice-cp-or-ap
Since network partitions are unavoidable in practice, the CAP theorem's real choice is between CP (consistent but may become unavailable) and AP (available but may return stale data)
- Source: entries/2026/06/19/wiki-Network_partitioning.md
- Source URL: https://en.wikipedia.org/wiki/Network_partitioning

### [ACCEPT] nosql-four-primary-data-models
The four primary NoSQL data models are key-value, document, wide-column, and graph, each optimized for different access patterns
- Source: entries/2026/06/19/wiki-NoSQL.md
- Source URL: https://en.wikipedia.org/wiki/NoSQL

### [ACCEPT] nosql-term-reintroduced-2009-oskarsson
The term 'NoSQL' for the modern non-relational movement was reintroduced by Johan Oskarsson in 2009; Carlo Strozzi first used it in 1998 for a relational DB without a SQL interface
- Source: entries/2026/06/19/wiki-NoSQL.md
- Source URL: https://en.wikipedia.org/wiki/NoSQL

### [ACCEPT] nosql-eventual-consistency-stale-reads
Most NoSQL systems prioritize availability and partition tolerance over strong consistency, using eventual consistency where updates propagate to all nodes eventually but may produce stale reads
- Source: entries/2026/06/19/wiki-NoSQL.md
- Source URL: https://en.wikipedia.org/wiki/NoSQL

### [ACCEPT] nosql-three-techniques-relational-data
NoSQL systems handle relational data without joins using three techniques: multiple queries, denormalization (embedding foreign values), and nesting/embedding related data within a single document
- Source: entries/2026/06/19/wiki-NoSQL.md
- Source URL: https://en.wikipedia.org/wiki/NoSQL

### [ACCEPT] nosql-denormalization-tradeoff
Denormalization in NoSQL optimizes read performance but requires updating data in many places when source values change, making it best suited for read-heavy workloads
- Source: entries/2026/06/19/wiki-NoSQL.md
- Source URL: https://en.wikipedia.org/wiki/NoSQL

### [ACCEPT] nosql-no-universal-query-language
NoSQL databases have no universal query language; query approaches vary by type (e.g., GET/PUT for key-value, Cypher/Gremlin/SPARQL for graph, CQL for Cassandra)
- Source: entries/2026/06/19/wiki-NoSQL.md
- Source URL: https://en.wikipedia.org/wiki/NoSQL

### [ACCEPT] openzfs-pool-version-5000-feature-flags
OpenZFS permanently uses pool version 5000; new on-disk format changes use feature flags (feature@<org>:<name>) instead of version increments
- Source: entries/2026/06/19/wiki-OpenZFS.md
- Source URL: https://en.wikipedia.org/wiki/OpenZFS

### [ACCEPT] openzfs-feature-flag-states
OpenZFS feature flag states progress from disabled (backward-compatible) to enabled (may be used, still backward-compatible) to active (backward-incompatible on-disk changes made)
- Source: entries/2026/06/19/wiki-OpenZFS.md
- Source URL: https://en.wikipedia.org/wiki/OpenZFS

### [ACCEPT] openzfs-cddl-gpl-incompatibility
The CDDL/GPL license incompatibility prevents ZFS from being merged into the mainline Linux kernel; Ubuntu distributes it as a loadable kernel module since 16.04
- Source: entries/2026/06/19/wiki-OpenZFS.md
- Source URL: https://en.wikipedia.org/wiki/OpenZFS

### [ACCEPT] openzfs-copy-on-write-crash-consistency
OpenZFS uses copy-on-write: data is never overwritten in place but written to a new location with atomic metadata updates, underpinning snapshots, clones, and crash consistency
- Source: entries/2026/06/19/wiki-OpenZFS.md
- Source URL: https://en.wikipedia.org/wiki/OpenZFS

### [ACCEPT] openzfs-self-healing-no-fsck
OpenZFS self-healing detects and corrects data errors during normal operation without requiring a dedicated fsck-style filesystem checker
- Source: entries/2026/06/19/wiki-OpenZFS.md
- Source URL: https://en.wikipedia.org/wiki/OpenZFS

### [ACCEPT] openzfs-2-0-merged-2020-linux-canonical
OpenZFS 2.0 (2020) merged the ZFS-on-Linux and broader OpenZFS codebases, making the Linux implementation the canonical upstream for all platforms including FreeBSD
- Source: entries/2026/06/19/wiki-OpenZFS.md
- Source URL: https://en.wikipedia.org/wiki/OpenZFS

### [ACCEPT] ot-transforms-remote-ops-against-local
Operational Transformation works by transforming remote operations against locally-executed concurrent operations before applying them, ensuring all replicas converge to the same state
- Source: entries/2026/06/19/wiki-Operational_transformation.md
- Source URL: https://en.wikipedia.org/wiki/Operational_transformation

### [ACCEPT] ot-intention-preservation-not-serializable
In OT, intention preservation (an operation's effect matches the user's original intent) cannot be achieved by serialization alone — this is OT's key differentiator from locking protocols
- Source: entries/2026/06/19/wiki-Operational_transformation.md
- Source URL: https://en.wikipedia.org/wiki/Operational_transformation

### [ACCEPT] ot-tp1-tp2-transformation-properties
OT transformation property TP1 is required when operations can execute in different orders; TP2 is required when operations can be transformed in different document states
- Source: entries/2026/06/19/wiki-Operational_transformation.md
- Source URL: https://en.wikipedia.org/wiki/Operational_transformation

### [ACCEPT] ot-control-algorithm-vs-transform-functions
OT systems separate into control algorithms (which ops to transform and in what order) and transformation functions (how to transform a specific pair of operations), enabling generic algorithms across application domains
- Source: entries/2026/06/19/wiki-Operational_transformation.md
- Source URL: https://en.wikipedia.org/wiki/Operational_transformation

### [ACCEPT] ot-invented-1989-grove-system
Operational Transformation was invented in 1989; the GROVE system by Ellis and Gibbs was the first OT implementation
- Source: entries/2026/06/19/wiki-Operational_transformation.md
- Source URL: https://en.wikipedia.org/wiki/Operational_transformation

### [ACCEPT] ot-google-docs-wave-production
Google Docs and Google Wave are production systems built on Operational Transformation, adopted in 2009
- Source: entries/2026/06/19/wiki-Operational_transformation.md
- Source URL: https://en.wikipedia.org/wiki/Operational_transformation

### [ACCEPT] occ-four-phases
Optimistic concurrency control has four phases: Begin (record timestamp), Modify (read and tentatively write), Validate (check for conflicts), and Commit/Rollback
- Source: entries/2026/06/19/wiki-Optimistic_concurrency_control.md
- Source URL: https://en.wikipedia.org/wiki/Optimistic_concurrency_control

### [ACCEPT] occ-no-locks-no-deadlocks
OCC transactions never acquire locks during execution, eliminating deadlocks but risking starvation under high contention due to repeated transaction restarts
- Source: entries/2026/06/19/wiki-Optimistic_concurrency_control.md
- Source URL: https://en.wikipedia.org/wiki/Optimistic_concurrency_control

### [ACCEPT] occ-validate-commit-must-be-atomic
In OCC, the validate and commit phases must be performed atomically to avoid time-of-check to time-of-use (TOCTOU) bugs
- Source: entries/2026/06/19/wiki-Optimistic_concurrency_control.md
- Source URL: https://en.wikipedia.org/wiki/Optimistic_concurrency_control

### [ACCEPT] occ-preferred-low-contention
OCC is preferred when data contention is low (higher throughput by avoiding lock overhead); pessimistic locking is preferred when contention is high (avoiding repeated restarts)
- Source: entries/2026/06/19/wiki-Optimistic_concurrency_control.md
- Source URL: https://en.wikipedia.org/wiki/Optimistic_concurrency_control

### [ACCEPT] http-etag-if-match-is-occ
HTTP's ETag + If-Match header mechanism is a built-in optimistic concurrency control implementation in the web protocol
- Source: entries/2026/06/19/wiki-Optimistic_concurrency_control.md
- Source URL: https://en.wikipedia.org/wiki/Optimistic_concurrency_control

### [ACCEPT] occ-proposed-1979-kung-robinson
Optimistic concurrency control was first proposed by H.T. Kung and John T. Robinson in 1979
- Source: entries/2026/06/19/wiki-Optimistic_concurrency_control.md
- Source URL: https://en.wikipedia.org/wiki/Optimistic_concurrency_control

### [ACCEPT] kubernetes-resourceversion-occ
Kubernetes uses resourceVersion for optimistic concurrency control — resource updates are rejected if the version has changed since the client's last read
- Source: entries/2026/06/19/wiki-Optimistic_concurrency_control.md
- Source URL: https://en.wikipedia.org/wiki/Optimistic_concurrency_control

### [ACCEPT] optimistic-replication-allows-temporary-divergence
Optimistic (lazy) replication allows replicas to diverge temporarily and guarantees convergence only after the system has been quiesced, unlike pessimistic replication which enforces identical replicas at all times.
- Source: entries/2026/06/19/wiki-Optimistic_replication.md
- Source URL: https://en.wikipedia.org/wiki/Optimistic_replication

### [ACCEPT] optimistic-replication-five-element-algorithm
The optimistic replication algorithm consists of five elements: operation submission, propagation, scheduling, conflict resolution, and commitment.
- Source: entries/2026/06/19/wiki-Optimistic_replication.md
- Source URL: https://en.wikipedia.org/wiki/Optimistic_replication

### [ACCEPT] replication-state-transfer-vs-operation-transfer
Replication propagation has two strategies: state transfer (ship current state) and operation transfer (ship operations/instructions to reach new state); state transfer is simpler but loses semantic information, limiting conflict resolution to syntactic approaches.
- Source: entries/2026/06/19/wiki-Optimistic_replication.md
- Source URL: https://en.wikipedia.org/wiki/Optimistic_replication

### [ACCEPT] replication-syntactic-vs-semantic-conflict-resolution
Conflict resolution in replication can be syntactic (based on general info like timestamps or location) or semantic (using application-specific knowledge); state transfer systems are limited to syntactic resolution because they lack semantic information.
- Source: entries/2026/06/19/wiki-Optimistic_replication.md
- Source URL: https://en.wikipedia.org/wiki/Optimistic_replication

### [ACCEPT] non-idempotent-ops-replication-lag-hazard
Non-idempotent operations (e.g., incrementing a value) combined with replication lag can cause data corruption when users retry operations they believe failed, and testing environments may mask this because they produce less lag than production.
- Source: entries/2026/06/19/wiki-Optimistic_replication.md
- Source URL: https://en.wikipedia.org/wiki/Optimistic_replication

### [ACCEPT] optimistic-replication-canonical-survey-saito-shapiro-2005
The canonical survey paper on optimistic replication is Saito & Shapiro (2005), 'Optimistic Replication' in ACM Computing Surveys.
- Source: entries/2026/06/19/wiki-Optimistic_replication.md
- Source URL: https://en.wikipedia.org/wiki/Optimistic_replication

### [ACCEPT] pacelc-extends-cap-with-latency-consistency
PACELC extends the CAP theorem: during a partition (P), choose availability (A) or consistency (C); else (E) during normal operation, choose latency (L) or consistency (C).
- Source: entries/2026/06/19/wiki-PACELC_theorem.md
- Source URL: https://en.wikipedia.org/wiki/PACELC_theorem

### [ACCEPT] pacelc-formulated-by-abadi-2010
PACELC was formulated by Daniel Abadi (Yale) in a 2010 blog post and 2012 paper, and was formally proved in 2018 by Wojciech Golab in SIGACT News.
- Source: entries/2026/06/19/wiki-PACELC_theorem.md
- Source URL: https://en.wikipedia.org/wiki/PACELC_theorem

### [ACCEPT] pacelc-pa-el-systems-dynamo-cassandra-riak
PA/EL systems (favor availability and low latency, relaxed consistency) include Dynamo (internal), Cassandra, Riak, and Cosmos DB (default).
- Source: entries/2026/06/19/wiki-PACELC_theorem.md
- Source URL: https://en.wikipedia.org/wiki/PACELC_theorem

### [ACCEPT] pacelc-pc-ec-systems-voltdb-postgresql-hbase
PC/EC systems (favor consistency always, paying availability and latency costs) include VoltDB, Megastore, MySQL Cluster, PostgreSQL, Bigtable, and HBase.
- Source: entries/2026/06/19/wiki-PACELC_theorem.md
- Source URL: https://en.wikipedia.org/wiki/PACELC_theorem

### [ACCEPT] dynamodb-differs-from-dynamo-strong-leader
DynamoDB uses a strong leader model with serialized writes and is not PA/EL like the original internal Dynamo; they are architecturally different systems despite the name.
- Source: entries/2026/06/19/wiki-PACELC_theorem.md
- Source URL: https://en.wikipedia.org/wiki/PACELC_theorem

### [ACCEPT] cosmos-db-five-consistency-levels
Cosmos DB offers five selectable consistency levels: strong, bounded staleness, session, consistent prefix, and eventual.
- Source: entries/2026/06/19/wiki-PACELC_theorem.md
- Source URL: https://en.wikipedia.org/wiki/PACELC_theorem

### [ACCEPT] partitioning-each-record-exactly-one-partition
In database partitioning, each piece of data belongs to exactly one partition, making each partition effectively a small independent database.
- Source: entries/2026/06/19/wiki-Partition_database.md
- Source URL: https://en.wikipedia.org/wiki/Partition_(database)

### [ACCEPT] hash-partitioning-prevents-hotspots-loses-range-queries
Hash partitioning distributes data evenly to prevent hot spots but sacrifices range query efficiency, since adjacent key values are scattered across different partitions.
- Source: entries/2026/06/19/wiki-Partition_database.md
- Source URL: https://en.wikipedia.org/wiki/Partition_(database)

### [ACCEPT] cassandra-compound-primary-key-partitioning
Cassandra's compound primary key hashes the first component for partition assignment and maintains sort order on remaining components within each partition, combining distribution with local ordering.
- Source: entries/2026/06/19/wiki-Partition_database.md
- Source URL: https://en.wikipedia.org/wiki/Partition_(database)

### [ACCEPT] partition-terminology-shard-region-tablet-vnode-vbucket
Partition terminology varies by system: shard (MongoDB/Elasticsearch/SolrCloud), region (HBase), tablet (Bigtable), vnode (Cassandra/Riak), vBucket (Couchbase).
- Source: entries/2026/06/19/wiki-Partition_database.md
- Source URL: https://en.wikipedia.org/wiki/Partition_(database)

### [ACCEPT] partitioning-node-leader-some-follower-others
When partitioning is combined with replication, a single node can simultaneously be leader for some partitions and follower for others.
- Source: entries/2026/06/19/wiki-Partition_database.md
- Source URL: https://en.wikipedia.org/wiki/Partition_(database)

### [ACCEPT] range-partitioning-hotspot-risk-timestamp-keys
Range partitioning enables efficient range scans but risks hot spots with monotonically increasing keys (e.g., timestamps concentrating writes); mitigation is compound keys with a prefix identifier.
- Source: entries/2026/06/19/wiki-Partition_database.md
- Source URL: https://en.wikipedia.org/wiki/Partition_(database)

### [ACCEPT] paxos-requires-2f-plus-1-nodes-tolerate-f-failures
Paxos requires n = 2F + 1 processors to tolerate F simultaneous failures, because the non-faulty count must strictly exceed the faulty count.
- Source: entries/2026/06/19/wiki-Paxos_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Paxos_(computer_science)

### [ACCEPT] paxos-guarantees-safety-not-liveness
Paxos guarantees safety (only proposed values chosen, no two learners learn different values) but does NOT guarantee liveness — it can livelock when multiple proposers conflict with dueling proposal numbers.
- Source: entries/2026/06/19/wiki-Paxos_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Paxos_(computer_science)

### [ACCEPT] flp-impossibility-safety-liveness-fault-tolerance
The FLP impossibility result (Fischer, Lynch, Paterson) proves that no deterministic fault-tolerant consensus protocol can guarantee progress in an asynchronous network — a protocol can have only two of safety, liveness, and fault tolerance.
- Source: entries/2026/06/19/wiki-Paxos_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Paxos_(computer_science)

### [ACCEPT] paxos-proposer-must-adopt-highest-accepted-value
In Paxos Phase 2a, the proposer must adopt the value from the highest-numbered previously accepted proposal reported in Promise messages; it cannot freely choose its own value if any acceptor has already accepted something.
- Source: entries/2026/06/19/wiki-Paxos_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Paxos_(computer_science)

### [ACCEPT] multi-paxos-skips-phase-1-stable-leader
In Multi-Paxos with a stable leader, Phase 1 (Prepare/Promise) can be skipped for subsequent instances, reducing message delay from 4 to 2 per decided value.
- Source: entries/2026/06/19/wiki-Paxos_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Paxos_(computer_science)

### [ACCEPT] paxos-crash-recovery-not-byzantine
Basic Paxos assumes a crash-recovery model where processors may fail and rejoin but do not lie (no Byzantine failures); messages may be lost, reordered, or duplicated but not corrupted.
- Source: entries/2026/06/19/wiki-Paxos_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Paxos_(computer_science)

### [ACCEPT] postgresql-read-uncommitted-actually-read-committed
PostgreSQL's Read Uncommitted isolation level actually behaves as Read Committed — dirty reads are impossible due to MVCC implementation.
- Source: entries/2026/06/19/wiki-PostgreSQL.md
- Source URL: https://en.wikipedia.org/wiki/PostgreSQL

### [ACCEPT] postgresql-serializable-uses-ssi-not-2pl
PostgreSQL implements Serializable isolation using Serializable Snapshot Isolation (SSI), not traditional two-phase locking.
- Source: entries/2026/06/19/wiki-PostgreSQL.md
- Source URL: https://en.wikipedia.org/wiki/PostgreSQL

### [ACCEPT] postgresql-multi-master-not-in-core
Multi-master replication is not in core PostgreSQL; it requires external tools such as Postgres-XC, BDR (Bidirectional Replication), or Bucardo.
- Source: entries/2026/06/19/wiki-PostgreSQL.md
- Source URL: https://en.wikipedia.org/wiki/PostgreSQL

### [ACCEPT] postgresql-table-inheritance-no-unique-fk-propagation
PostgreSQL table inheritance propagates check constraints and NOT NULL to child tables, but does NOT propagate unique, primary key, or foreign key constraints.
- Source: entries/2026/06/19/wiki-PostgreSQL.md
- Source URL: https://en.wikipedia.org/wiki/PostgreSQL

### [ACCEPT] postgresql-six-index-types
PostgreSQL supports six built-in index types: B-tree (default), hash, GiST, GIN, SP-GiST, and BRIN, plus user-defined index methods.
- Source: entries/2026/06/19/wiki-PostgreSQL.md
- Source URL: https://en.wikipedia.org/wiki/PostgreSQL

### [ACCEPT] postgresql-notify-listen-fully-transactional
PostgreSQL's NOTIFY/LISTEN pub/sub messaging system is fully transactional — notifications are not sent until the issuing transaction commits.
- Source: entries/2026/06/19/wiki-PostgreSQL.md
- Source URL: https://en.wikipedia.org/wiki/PostgreSQL

### [ACCEPT] postgresql-sync-replication-four-granularities
PostgreSQL synchronous replication durability can be configured at four granularities: per-database, per-user, per-session, and per-transaction.
- Source: entries/2026/06/19/wiki-PostgreSQL.md
- Source URL: https://en.wikipedia.org/wiki/PostgreSQL

### [ACCEPT] postgresql-schemas-are-namespaces-not-nested
PostgreSQL schemas are namespaces within a single database that cannot be nested; the default search_path is '$user, public' and non-existent schemas in the path are silently skipped.
- Source: entries/2026/06/19/wiki-PostgreSQL.md
- Source URL: https://en.wikipedia.org/wiki/PostgreSQL

### [ACCEPT] bft-requires-3f-plus-1-nodes-without-signatures
Byzantine fault tolerance without message signing requires n > 3f nodes to tolerate f faulty nodes, proved by Shostak and Pease in 1980
- Source: entries/2026/06/19/wiki-Practical_Byzantine_fault_tolerance.md
- Source URL: https://en.wikipedia.org/wiki/Practical_Byzantine_fault_tolerance

### [ACCEPT] bft-with-digital-signatures-tolerates-arbitrary-faults
With unforgeable digital signatures, BFT can tolerate an arbitrary number of faulty nodes regardless of total node count, proved by Lamport
- Source: entries/2026/06/19/wiki-Practical_Byzantine_fault_tolerance.md
- Source URL: https://en.wikipedia.org/wiki/Practical_Byzantine_fault_tolerance

### [ACCEPT] full-bft-resource-triple
Full BFT requires 3F+1 nodes, 2F+1 independent communication paths, and F+1 rounds of communication to tolerate F Byzantine failures
- Source: entries/2026/06/19/wiki-Practical_Byzantine_fault_tolerance.md
- Source URL: https://en.wikipedia.org/wiki/Practical_Byzantine_fault_tolerance

### [ACCEPT] pbft-castro-liskov-1999
Practical Byzantine Fault Tolerance (PBFT) was introduced by Castro and Liskov in 1999 and was the first algorithm to enable high-performance BFT state machine replication with thousands of requests per second
- Source: entries/2026/06/19/wiki-Practical_Byzantine_fault_tolerance.md
- Source URL: https://en.wikipedia.org/wiki/Practical_Byzantine_fault_tolerance

### [ACCEPT] bft-provides-broadcast-consistency-not-value-correctness
BFT ensures all correct nodes receive the same value from a broadcaster (broadcast consistency), but does not validate the correctness of the value itself
- Source: entries/2026/06/19/wiki-Practical_Byzantine_fault_tolerance.md
- Source URL: https://en.wikipedia.org/wiki/Practical_Byzantine_fault_tolerance

### [ACCEPT] byzantine-faults-not-limited-to-malicious-actors
Byzantine faults are not limited to security attacks — hardware glitches, voltage errors, and software bugs can all produce Byzantine symptoms where a faulty component presents different data to different observers
- Source: entries/2026/06/19/wiki-Practical_Byzantine_fault_tolerance.md
- Source URL: https://en.wikipedia.org/wiki/Practical_Byzantine_fault_tolerance

### [ACCEPT] blockchain-weaker-than-classical-bft
Blockchain systems like Bitcoin do not provide classical BFT guarantees — they use resource-intensive mechanisms (e.g., proof-of-work) that make disagreement economically impractical, providing probabilistic finality rather than mathematical guarantees
- Source: entries/2026/06/19/wiki-Practical_Byzantine_fault_tolerance.md
- Source URL: https://en.wikipedia.org/wiki/Practical_Byzantine_fault_tolerance

### [ACCEPT] byzantine-generals-problem-origin
The Byzantine generals problem was conceived by Robert Shostak in 1978 at SRI International for the NASA SIFT project, formalized by Lamport, Shostak, and Pease in 1982, and awarded the 2005 Dijkstra Prize
- Source: entries/2026/06/19/wiki-Practical_Byzantine_fault_tolerance.md
- Source URL: https://en.wikipedia.org/wiki/Practical_Byzantine_fault_tolerance

### [ACCEPT] pubsub-fan-out-vs-queue-competing-consumers
Pub/sub delivers messages to all matching subscribers (fan-out), while message queues deliver each message to exactly one consumer (competing consumers pattern)
- Source: entries/2026/06/19/wiki-PublishE28093subscribe_pattern.md
- Source URL: https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern

### [ACCEPT] pubsub-three-filtering-approaches
Pub/sub systems use three message filtering approaches: topic-based (named channels), content-based (attribute constraints on message content), and hybrid (topic routing with content filters within topics)
- Source: entries/2026/06/19/wiki-PublishE28093subscribe_pattern.md
- Source URL: https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern

### [ACCEPT] pubsub-three-forms-of-decoupling
Pub/sub provides three forms of decoupling between producers and consumers: spatial (location), temporal (timing — publishers and subscribers need not run simultaneously), and identity decoupling
- Source: entries/2026/06/19/wiki-PublishE28093subscribe_pattern.md
- Source URL: https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern

### [ACCEPT] pubsub-no-guaranteed-delivery-by-default
Pub/sub does not guarantee message delivery by default — delivery guarantees must be engineered separately on top of the basic pattern
- Source: entries/2026/06/19/wiki-PublishE28093subscribe_pattern.md
- Source URL: https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern

### [ACCEPT] earliest-pubsub-system-isis-toolkit-1987
The earliest known pub/sub system was the 'news' subsystem of the Isis Toolkit, presented at SOSP 1987
- Source: entries/2026/06/19/wiki-PublishE28093subscribe_pattern.md
- Source URL: https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern

### [ACCEPT] pubsub-semantic-coupling-hidden-risk
Semantic/format coupling is the hidden risk in pub/sub: despite spatial and temporal decoupling, changes to message structure can make the system brittle
- Source: entries/2026/06/19/wiki-PublishE28093subscribe_pattern.md
- Source URL: https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern

### [ACCEPT] quorum-commit-abort-overlap-rule
In quorum-based distributed transactions, the constraint Va + Vc > V (abort quorum + commit quorum > total votes) prevents a transaction from being simultaneously committed and aborted
- Source: entries/2026/06/19/wiki-Quorum_distributed_computing.md
- Source URL: https://en.wikipedia.org/wiki/Quorum_(distributed_computing)

### [ACCEPT] gifford-weighted-voting-quorum-rules
Gifford's weighted voting (1979) for replica control requires Vr + Vw > V (read quorum overlaps write quorum, ensuring reads see latest writes) and Vw > V/2 (write quorum is a strict majority, preventing concurrent conflicting writes)
- Source: entries/2026/06/19/wiki-Quorum_distributed_computing.md
- Source URL: https://en.wikipedia.org/wiki/Quorum_(distributed_computing)

### [ACCEPT] quorum-sizes-tunable-read-write-tradeoff
Quorum sizes are a tunable tradeoff: increasing the read quorum Vr allows decreasing the write quorum Vw and vice versa, enabling optimization for read-heavy or write-heavy workloads
- Source: entries/2026/06/19/wiki-Quorum_distributed_computing.md
- Source URL: https://en.wikipedia.org/wiki/Quorum_(distributed_computing)

### [ACCEPT] quorum-handles-network-partitions
Quorum-based voting handles network partitions by allowing only the partition that can assemble a quorum to proceed, while the minority partition blocks rather than diverging (preventing split-brain)
- Source: entries/2026/06/19/wiki-Quorum_distributed_computing.md
- Source URL: https://en.wikipedia.org/wiki/Quorum_(distributed_computing)

### [ACCEPT] quotient-filter-no-false-negatives-tunable-fpr
Quotient filters produce no false negatives and have a tunable false positive rate of approximately 2^(-r), where r is the remainder bit size
- Source: entries/2026/06/19/wiki-Quotient_filter.md
- Source URL: https://en.wikipedia.org/wiki/Quotient_filter

### [ACCEPT] quotient-filter-mergeable-without-original-keys
Quotient filters can be merged and resized without access to original keys because full fingerprints can be reconstructed from stored quotients and remainders — a key advantage over Bloom filters
- Source: entries/2026/06/19/wiki-Quotient_filter.md
- Source URL: https://en.wikipedia.org/wiki/Quotient_filter

### [ACCEPT] quotient-filter-three-metadata-bits-per-slot
Quotient filters use three metadata bits per slot (is_occupied, is_continuation, is_shifted) to enable reconstruction of which quotient each stored remainder belongs to
- Source: entries/2026/06/19/wiki-Quotient_filter.md
- Source URL: https://en.wikipedia.org/wiki/Quotient_filter

### [ACCEPT] quotient-filter-better-than-bloom-below-1-64-fpr
Quotient filters use less space than Bloom filters when the target false-positive rate is less than 1/64 (Pandey et al. 2017)
- Source: entries/2026/06/19/wiki-Quotient_filter.md
- Source URL: https://en.wikipedia.org/wiki/Quotient_filter

### [ACCEPT] quotient-filter-beneficial-for-lsm-tree-compaction
Quotient filters are especially beneficial for LSM-tree compaction because sub-tree filters can be merged during compaction without re-reading original keys from disk
- Source: entries/2026/06/19/wiki-Quotient_filter.md
- Source URL: https://en.wikipedia.org/wiki/Quotient_filter

### [ACCEPT] raft-not-byzantine-fault-tolerant
Raft is not Byzantine fault tolerant — all participants are assumed trustworthy, and nodes trust the elected leader
- Source: entries/2026/06/19/wiki-Raft_algorithm.md
- Source URL: https://en.wikipedia.org/wiki/Raft_(algorithm)

### [ACCEPT] raft-three-roles-leader-follower-candidate
In Raft, every server is in one of three roles: leader (accepts client requests, replicates log), follower (passive, responds to leader), or candidate (during elections only)
- Source: entries/2026/06/19/wiki-Raft_algorithm.md
- Source URL: https://en.wikipedia.org/wiki/Raft_(algorithm)

### [ACCEPT] raft-entry-committed-on-majority-replication
In Raft, a log entry is committed once it has been replicated to a majority of servers (not all), and once committed it is applied to the state machine
- Source: entries/2026/06/19/wiki-Raft_algorithm.md
- Source URL: https://en.wikipedia.org/wiki/Raft_(algorithm)

### [ACCEPT] raft-timing-invariant
Raft requires the timing invariant broadcastTime << electionTimeout << MTBF, with typical values of 0.5–20ms for broadcast, 10–500ms for election timeout, and weeks to months for MTBF
- Source: entries/2026/06/19/wiki-Raft_algorithm.md
- Source URL: https://en.wikipedia.org/wiki/Raft_(algorithm)

### [ACCEPT] raft-joint-consensus-for-membership-changes
Raft uses joint consensus (Cold ∪ Cnew) for cluster membership changes, requiring majorities from both old and new configurations simultaneously during the transition
- Source: entries/2026/06/19/wiki-Raft_algorithm.md
- Source URL: https://en.wikipedia.org/wiki/Raft_(algorithm)

### [ACCEPT] raft-leader-single-point-of-bottleneck
The Raft leader is a single point of failure and performance bottleneck — Raft does not scale writes with cluster size
- Source: entries/2026/06/19/wiki-Raft_algorithm.md
- Source URL: https://en.wikipedia.org/wiki/Raft_(algorithm)

### [ACCEPT] raft-production-systems
Production systems using Raft include etcd (Kubernetes), CockroachDB, TiDB/TiKV, Kafka KRaft, RabbitMQ quorum queues, ScyllaDB, YugabyteDB, Neo4j, ClickHouse Keeper, Redpanda, NATS JetStream, and Hazelcast CP subsystem
- Source: entries/2026/06/19/wiki-Raft_algorithm.md
- Source URL: https://en.wikipedia.org/wiki/Raft_(algorithm)

### [ACCEPT] redis-stands-for-remote-dictionary-server
Redis stands for Remote Dictionary Server
- Source: entries/2026/06/19/wiki-Redis.md
- Source URL: https://en.wikipedia.org/wiki/Redis

### [ACCEPT] redis-written-in-c
Redis is written in C and runs on Unix-like systems
- Source: entries/2026/06/19/wiki-Redis.md
- Source URL: https://en.wikipedia.org/wiki/Redis

### [ACCEPT] redis-single-threaded-execution
A single Redis instance uses a single-threaded execution model and cannot parallelize tasks within one instance
- Source: entries/2026/06/19/wiki-Redis.md
- Source URL: https://en.wikipedia.org/wiki/Redis

### [ACCEPT] redis-two-persistence-mechanisms
Redis has two persistence mechanisms: RDB snapshots (point-in-time binary dumps) and AOF (append-only journaling), with AOF considered the safer method
- Source: entries/2026/06/19/wiki-Redis.md
- Source URL: https://en.wikipedia.org/wiki/Redis

### [ACCEPT] redis-default-flush-interval-2-seconds
Redis writes to disk at least every 2 seconds by default; a complete system failure loses only a few seconds of data
- Source: entries/2026/06/19/wiki-Redis.md
- Source URL: https://en.wikipedia.org/wiki/Redis

### [ACCEPT] redis-clustering-since-v3-scales-1000-nodes
Redis clustering has been available since v3.0 (April 2015) and scales up to 1,000 nodes
- Source: entries/2026/06/19/wiki-Redis.md
- Source URL: https://en.wikipedia.org/wiki/Redis

### [ACCEPT] redis-multi-key-ops-restricted-same-node
Multi-key operations in a Redis cluster are restricted to keys on the same node
- Source: entries/2026/06/19/wiki-Redis.md
- Source URL: https://en.wikipedia.org/wiki/Redis

### [ACCEPT] redis-uses-fork-for-persistence
Redis uses the fork() system call to create a child process for persistence while the parent continues serving clients
- Source: entries/2026/06/19/wiki-Redis.md
- Source URL: https://en.wikipedia.org/wiki/Redis

### [ACCEPT] redis-license-change-v74-rsal-sspl-v80-agpl
Redis changed from BSD-3 license to RSAL+SSPL in v7.4 (2024), then to tri-licensed RSAL+SSPL+AGPL in v8.0 (May 2025)
- Source: entries/2026/06/19/wiki-Redis.md
- Source URL: https://en.wikipedia.org/wiki/Redis

### [ACCEPT] valkey-fork-of-redis-after-license-change
Valkey is a Linux Foundation fork of Redis created from the last BSD-licensed version after the 2024 license change
- Source: entries/2026/06/19/wiki-Redis.md
- Source URL: https://en.wikipedia.org/wiki/Redis

### [ACCEPT] redis-streams-added-v5-time-based-sequencing
Redis Streams (added in v5.0, 2018) store multiple fields and string values with automatic time-based sequencing at a single key
- Source: entries/2026/06/19/wiki-Redis.md
- Source URL: https://en.wikipedia.org/wiki/Redis

### [ACCEPT] rendezvous-hashing-predates-consistent-hashing
Rendezvous hashing (also called Highest Random Weight / HRW hashing) was published in 1996, predating consistent hashing (1997)
- Source: entries/2026/06/19/wiki-Rendezvous_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Rendezvous_hashing

### [ACCEPT] hrw-hashing-mechanism-highest-weight-selection
In HRW hashing, each client computes hash weight w(i,j) = h(O_i, S_j) for every site and picks the site with the highest hash value; all clients agree without coordination
- Source: entries/2026/06/19/wiki-Rendezvous_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Rendezvous_hashing

### [ACCEPT] hrw-minimal-disruption-on-site-removal
When a site is removed in HRW hashing, only objects assigned to that site are remapped; all other assignments remain stable
- Source: entries/2026/06/19/wiki-Rendezvous_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Rendezvous_hashing

### [ACCEPT] consistent-hashing-special-case-of-hrw-k1
Consistent hashing is a special case of rendezvous hashing that solves only k=1 using a token ring; HRW generalizes to arbitrary k
- Source: entries/2026/06/19/wiki-Rendezvous_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Rendezvous_hashing

### [ACCEPT] hrw-basic-time-complexity-on
Basic HRW hashing has O(n) time complexity per lookup; a skeleton-based hierarchical variant achieves O(log n) by organizing sites into clusters and descending a virtual tree
- Source: entries/2026/06/19/wiki-Rendezvous_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Rendezvous_hashing

### [ACCEPT] hrw-no-precomputed-tokens-or-metadata
Unlike consistent hashing, HRW requires no precomputed token rings, no metadata, and no sorted token lists
- Source: entries/2026/06/19/wiki-Rendezvous_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Rendezvous_hashing

### [ACCEPT] consistent-hashing-needs-100-200-tokens-per-site
Consistent hashing requires 100-200 tokens per site for reasonable load balance across nodes
- Source: entries/2026/06/19/wiki-Rendezvous_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Rendezvous_hashing

### [ACCEPT] hrw-capacity-weighting-via-multiplicity
HRW handles heterogeneous capacity by listing higher-capacity sites multiple times in the site list; consistent hashing uses proportional token counts
- Source: entries/2026/06/19/wiki-Rendezvous_hashing.md
- Source URL: https://en.wikipedia.org/wiki/Rendezvous_hashing

### [ACCEPT] replication-three-approaches-single-multi-leaderless
The three fundamental replication approaches are single-leader, multi-leader, and leaderless, each with distinct consistency and availability characteristics
- Source: entries/2026/06/19/wiki-Replication_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Replication_(computer_science)

### [ACCEPT] synchronous-replication-zero-loss-high-latency
Synchronous replication guarantees zero data loss but increases latency proportional to distance (10 km minimum roundtrip ~67 μs)
- Source: entries/2026/06/19/wiki-Replication_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Replication_(computer_science)

### [ACCEPT] three-db-replication-techniques
Three database replication techniques are statement-based (replays SQL), WAL shipping (replicates storage engine log), and logical/row-based (describes row-level changes in dedicated format)
- Source: entries/2026/06/19/wiki-Replication_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Replication_(computer_science)

### [ACCEPT] statement-based-replication-breaks-nondeterministic
Statement-based replication fails with non-deterministic functions or side effects because replaying the same SQL statement may produce different results
- Source: entries/2026/06/19/wiki-Replication_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Replication_(computer_science)

### [ACCEPT] gray-multi-primary-on3-degradation
Jim Gray's analysis shows multi-primary replication degrades as O(n³) with replica count unless data has a natural partitioning key
- Source: entries/2026/06/19/wiki-Replication_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Replication_(computer_science)

### [ACCEPT] replication-not-backup
Replication is not backup: replicas are continuously updated and lose historical state; backups are point-in-time snapshots preserved long-term
- Source: entries/2026/06/19/wiki-Replication_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Replication_(computer_science)

### [ACCEPT] eager-replication-prevents-lazy-resolves-conflicts
Eager (synchronous) replication prevents conflicts by detecting them before commit; lazy (asynchronous) replication resolves conflicts after both transactions commit
- Source: entries/2026/06/19/wiki-Replication_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Replication_(computer_science)

### [ACCEPT] state-machine-replication-requires-determinism-atomic-broadcast
State machine replication (SMR) requires deterministic replicas and atomic broadcast, typically implemented via consensus algorithms like Paxos
- Source: entries/2026/06/19/wiki-Replication_computer_science.md
- Source URL: https://en.wikipedia.org/wiki/Replication_(computer_science)

### [ACCEPT] semi-synchronous-replication-compromise
Semi-synchronous replication confirms a write after remote receipt/logging but before remote write completes, offering a middle ground between synchronous and asynchronous
- Source: entries/2026/06/19/wiki-Replication_computing.md
- Source URL: https://en.wikipedia.org/wiki/Replication_(computing)

### [ACCEPT] riak-implements-dynamo-paper
Riak is a distributed NoSQL key-value store written in Erlang that directly implements Amazon's Dynamo paper principles: consistent hashing, replication, hinted handoff, and anti-entropy repair
- Source: entries/2026/06/19/wiki-Riak.md
- Source URL: https://en.wikipedia.org/wiki/Riak

### [ACCEPT] riak-masterless-default-nval-3
Riak uses masterless peer-to-peer architecture with no single point of failure; default replication factor (n_val) is 3
- Source: entries/2026/06/19/wiki-Riak.md
- Source URL: https://en.wikipedia.org/wiki/Riak

### [ACCEPT] riak-ap-system-tunable-consistency-per-bucket
Riak is an AP system by default (availability + partition tolerance) but supports tunable consistency per bucket, allowing strong consistency (CP) on a per-bucket basis
- Source: entries/2026/06/19/wiki-Riak.md
- Source URL: https://en.wikipedia.org/wiki/Riak

### [ACCEPT] riak-hinted-handoff-during-outages
Riak uses hinted handoff during node outages: writes go to a neighboring node beyond the initial replicas to ensure continued availability during partitions
- Source: entries/2026/06/19/wiki-Riak.md
- Source URL: https://en.wikipedia.org/wiki/Riak

### [ACCEPT] riak-default-backend-bitcask-keys-in-ram
Riak's default storage backend is Bitcask (log-structured, append-only), which requires all keys to fit in RAM; LevelDB is used when key space exceeds memory
- Source: entries/2026/06/19/wiki-Riak.md
- Source URL: https://en.wikipedia.org/wiki/Riak

### [ACCEPT] riak-crdts-added-v2
Riak added CRDTs in v2.0 (sets, maps, registers, flags) to resolve sibling/conflict problems for specific data structures without application-level conflict resolution
- Source: entries/2026/06/19/wiki-Riak.md
- Source URL: https://en.wikipedia.org/wiki/Riak

### [ACCEPT] riak-cs-stanchion-serialization
Riak CS uses Stanchion as a serialization service for globally unique entities (users, bucket names), acting as a deliberate consistency chokepoint in an otherwise AP system
- Source: entries/2026/06/19/wiki-Riak.md
- Source URL: https://en.wikipedia.org/wiki/Riak

### [ACCEPT] riak-write-once-buckets-v21-immutable-optimization
Riak introduced write-once buckets in v2.1 as an optimization for immutable data (logs, events, sensor readings) that skips conflict resolution for significant performance gains
- Source: entries/2026/06/19/wiki-Riak.md
- Source URL: https://en.wikipedia.org/wiki/Riak

### [ACCEPT] riak-mdc-fullsync-and-realtime-modes
Riak's multi-datacenter replication supports two modes: fullsync (bulk synchronization with metadata-only transfer) and realtime (streaming updates), designed to work together
- Source: entries/2026/06/19/wiki-Riak.md
- Source URL: https://en.wikipedia.org/wiki/Riak

### [ACCEPT] rocksdb-fork-of-leveldb-may-2012
RocksDB was released in May 2012 as a fork of Google's LevelDB, created by Dhruba Borthakur at Facebook to optimize for multi-core CPUs and SSDs.
- Source: entries/2026/06/19/wiki-RocksDB.md
- Source URL: https://en.wikipedia.org/wiki/RocksDB

### [ACCEPT] rocksdb-lsm-tree-embedded-cpp
RocksDB is an embedded C++ library based on LSM trees with no server process, CLI, SQL, or network protocol.
- Source: entries/2026/06/19/wiki-RocksDB.md
- Source URL: https://en.wikipedia.org/wiki/RocksDB

### [ACCEPT] rocksdb-features-beyond-leveldb
RocksDB adds transactions, backups/snapshots, column families, Bloom filters, TTL, universal compaction, and merge operators beyond what LevelDB provides.
- Source: entries/2026/06/19/wiki-RocksDB.md
- Source URL: https://en.wikipedia.org/wiki/RocksDB

### [ACCEPT] rocksdb-merge-operators-defer-rmw
RocksDB merge operators defer read-modify-write operations until compaction time, reducing write amplification.
- Source: entries/2026/06/19/wiki-RocksDB.md
- Source URL: https://en.wikipedia.org/wiki/RocksDB

### [ACCEPT] rocksdb-license-change-2017
RocksDB changed from BSD+Patents to dual Apache 2.0/GPLv2 licensing in 2017 after the Apache Software Foundation blacklisted the BSD+Patents license.
- Source: entries/2026/06/19/wiki-RocksDB.md
- Source URL: https://en.wikipedia.org/wiki/RocksDB

### [ACCEPT] rocksdb-storage-engine-for-other-databases
RocksDB is used as the underlying storage engine by MyRocks (MySQL/MariaDB), Cassandra (Facebook), TiDB, YugabyteDB, ArangoDB, and Ceph BlueStore.
- Source: entries/2026/06/19/wiki-RocksDB.md
- Source URL: https://en.wikipedia.org/wiki/RocksDB

### [ACCEPT] rocksdb-stream-processing-state-store
RocksDB serves as the state store for stream processing in Apache Flink (state backend checkpointing) and Kafka Streams (local state stores).
- Source: entries/2026/06/19/wiki-RocksDB.md
- Source URL: https://en.wikipedia.org/wiki/RocksDB

### [ACCEPT] rollback-restores-pre-transaction-state
A database rollback restores the database to the state before the current transaction's changes; it does not undo already-committed transactions.
- Source: entries/2026/06/19/wiki-Rollback_data_management.md
- Source URL: https://en.wikipedia.org/wiki/Rollback_(data_management)

### [ACCEPT] rollback-two-mechanisms-log-and-mvcc
Rollback is implemented via two mechanisms: transaction log (most common, recording before-images of changes) and MVCC (retaining old versions instead of undoing via log).
- Source: entries/2026/06/19/wiki-Rollback_data_management.md
- Source URL: https://en.wikipedia.org/wiki/Rollback_(data_management)

### [ACCEPT] cascading-rollback-definition
Cascading rollback occurs when one transaction's abort forces dependent transactions to also abort; production systems use cascadeless schedules to prevent this.
- Source: entries/2026/06/19/wiki-Rollback_data_management.md
- Source URL: https://en.wikipedia.org/wiki/Rollback_(data_management)

### [ACCEPT] rollback-connection-scoped
In most SQL dialects, ROLLBACK is connection-scoped — it affects only the connection that issued it, not other concurrent connections.
- Source: entries/2026/06/19/wiki-Rollback_data_management.md
- Source URL: https://en.wikipedia.org/wiki/Rollback_(data_management)

### [ACCEPT] rollback-releases-savepoints
A ROLLBACK command releases any existing savepoints in the current transaction.
- Source: entries/2026/06/19/wiki-Rollback_data_management.md
- Source URL: https://en.wikipedia.org/wiki/Rollback_(data_management)

### [ACCEPT] rollback-enforces-atomicity
Rollback is the mechanism that enforces the Atomicity property of ACID — ensuring transactions are all-or-nothing.
- Source: entries/2026/06/19/wiki-Rollback_data_management.md
- Source URL: https://en.wikipedia.org/wiki/Rollback_(data_management)

### [ACCEPT] sqlite-embedded-library-not-client-server
SQLite is an embedded C library linked directly into the application — there is no separate server process, network protocol, or IPC overhead.
- Source: entries/2026/06/19/wiki-SQLite.md
- Source URL: https://en.wikipedia.org/wiki/SQLite

### [ACCEPT] sqlite-single-file-max-281tb
An entire SQLite database (schema, tables, indices, data) is stored in a single cross-platform file with a maximum size of 281 terabytes.
- Source: entries/2026/06/19/wiki-SQLite.md
- Source URL: https://en.wikipedia.org/wiki/SQLite

### [ACCEPT] sqlite-dynamic-typing-strict-tables-2021
SQLite uses dynamic (manifest) typing by default where types belong to values not columns; STRICT tables added in 2021 opt into static column-type enforcement.
- Source: entries/2026/06/19/wiki-SQLite.md
- Source URL: https://en.wikipedia.org/wiki/SQLite

### [ACCEPT] sqlite-wal-mode-concurrent-reads-writes
SQLite WAL (Write-Ahead Logging) mode, introduced in v3.7, enables concurrent reads and writes; the default journal mode only allows sequential writes.
- Source: entries/2026/06/19/wiki-SQLite.md
- Source URL: https://en.wikipedia.org/wiki/SQLite

### [ACCEPT] sqlite-foreign-keys-off-by-default
SQLite foreign keys are disabled by default and must be explicitly enabled per-connection via PRAGMA foreign_keys = ON.
- Source: entries/2026/06/19/wiki-SQLite.md
- Source URL: https://en.wikipedia.org/wiki/SQLite

### [ACCEPT] sqlite-integer-primary-key-rowid-alias
In SQLite, an INTEGER PRIMARY KEY column becomes an alias for the implicit rowid, providing auto-increment-like behavior with 64-bit signed integer storage.
- Source: entries/2026/06/19/wiki-SQLite.md
- Source URL: https://en.wikipedia.org/wiki/SQLite

### [ACCEPT] sqlite-100-percent-branch-coverage
SQLite has maintained 100% branch test coverage since v3.6.17, with 92 million lines of test code for 156K lines of source code.
- Source: entries/2026/06/19/wiki-SQLite.md
- Source URL: https://en.wikipedia.org/wiki/SQLite

### [ACCEPT] sqlite-public-domain-license
SQLite is released into the public domain (not GPL, MIT, or any other standard open-source license), and contributors must sign an affidavit dedicating work to public domain.
- Source: entries/2026/06/19/wiki-SQLite.md
- Source URL: https://en.wikipedia.org/wiki/SQLite

### [ACCEPT] sqlite-access-control-filesystem-permissions
SQLite access control relies entirely on filesystem permissions on the database file — there is no SQL GRANT-based access control.
- Source: entries/2026/06/19/wiki-SQLite.md
- Source URL: https://en.wikipedia.org/wiki/SQLite

### [ACCEPT] schema-evolution-affects-structure-data-queries
Schema evolution affects three things simultaneously: the schema structure, the stored data, and all queries/applications that depend on the schema.
- Source: entries/2026/06/19/wiki-Schema_evolution.md
- Source URL: https://en.wikipedia.org/wiki/Schema_evolution

### [ACCEPT] schema-change-invalidates-70-percent-queries
A single schema evolution step can affect up to 70% of queries operating on that schema, as demonstrated by the MediaWiki case study.
- Source: entries/2026/06/19/wiki-Schema_evolution.md
- Source URL: https://en.wikipedia.org/wiki/Schema_evolution

### [ACCEPT] distributed-systems-schema-change-pressure
Web and distributed systems experience 39–500% more schema change pressure than traditional information systems due to cooperative, distributed development.
- Source: entries/2026/06/19/wiki-Schema_evolution.md
- Source URL: https://en.wikipedia.org/wiki/Schema_evolution

### [ACCEPT] schema-evolution-mapping-composition-invertibility
The two core theoretical problems in schema evolution are mapping composition (chaining transformations between versions) and mapping invertibility (reversing a transformation to recover the original view).
- Source: entries/2026/06/19/wiki-Schema_evolution.md
- Source URL: https://en.wikipedia.org/wiki/Schema_evolution

### [ACCEPT] temporal-databases-schema-versioning-prerequisite
Temporal databases have an especially acute schema evolution problem because they must serve historical data under potentially different schema versions.
- Source: entries/2026/06/19/wiki-Schema_evolution.md
- Source URL: https://en.wikipedia.org/wiki/Schema_evolution

### [ACCEPT] scylladb-cpp20-seastar-cassandra-compatible
ScyllaDB is written in C++20 using the Seastar async framework as a ground-up reimplementation of Cassandra — it shares CQL protocol and SSTable storage format but not code.
- Source: entries/2026/06/19/wiki-ScyllaDB.md
- Source URL: https://en.wikipedia.org/wiki/ScyllaDB

### [ACCEPT] scylladb-shared-nothing-per-core-sharding
ScyllaDB uses a shared-nothing per-core sharded architecture where each CPU core owns a disjoint data partition and communicates via explicit message passing, eliminating lock contention.
- Source: entries/2026/06/19/wiki-ScyllaDB.md
- Source URL: https://en.wikipedia.org/wiki/ScyllaDB

### [ACCEPT] scylladb-dynamodb-api-support
ScyllaDB supports both the Cassandra CQL protocol and the Amazon DynamoDB API, enabling migration from either system.
- Source: entries/2026/06/19/wiki-ScyllaDB.md
- Source URL: https://en.wikipedia.org/wiki/ScyllaDB

### [ACCEPT] scylladb-performance-vs-cassandra-2x-to-37x
ScyllaDB's performance improvement over Cassandra is workload- and hardware-dependent: vendor claims 10x, independent benchmarks range from 2x (OCTO) to 37x (Samsung) depending on YCSB workload.
- Source: entries/2026/06/19/wiki-ScyllaDB.md
- Source URL: https://en.wikipedia.org/wiki/ScyllaDB

### [ACCEPT] scylladb-license-agpl-to-source-available-2024
ScyllaDB changed its license from AGPL to source-available in December 2024, requiring a commercial license for clusters beyond a certain size.
- Source: entries/2026/06/19/wiki-ScyllaDB.md
- Source URL: https://en.wikipedia.org/wiki/ScyllaDB

### [ACCEPT] scylladb-founding-team-osv-unikernel
ScyllaDB's founding team (Cloudius Systems) previously built the OSv unikernel, reflecting the same hardware-aware, minimal-overhead systems design philosophy.
- Source: entries/2026/06/19/wiki-ScyllaDB.md
- Source URL: https://en.wikipedia.org/wiki/ScyllaDB

### [ACCEPT] conflict-serializable-iff-precedence-graph-acyclic
A schedule is conflict-serializable if and only if its precedence graph (over committed transactions) is acyclic (a DAG)
- Source: entries/2026/06/19/wiki-Serializability.md
- Source URL: https://en.wikipedia.org/wiki/Serializability

### [ACCEPT] conflicting-actions-three-conditions
Two database operations conflict iff they belong to different transactions, at least one is a write, and they access the same data object — read-read is not a conflict
- Source: entries/2026/06/19/wiki-Serializability.md
- Source URL: https://en.wikipedia.org/wiki/Serializability

### [ACCEPT] view-serializability-np-complete
Determining view-serializability is NP-complete, which is why practical database systems use conflict-serializability instead
- Source: entries/2026/06/19/wiki-Serializability.md
- Source URL: https://en.wikipedia.org/wiki/Serializability

### [ACCEPT] serializability-containment-hierarchy
The serializability containment hierarchy is: serial ⊂ conflict-serializable ⊂ view-serializable ⊂ all schedules
- Source: entries/2026/06/19/wiki-Serializability.md
- Source URL: https://en.wikipedia.org/wiki/Serializability

### [ACCEPT] recoverability-containment-hierarchy
The recoverability containment hierarchy is: serial ⊂ strict ⊂ cascadeless (ACA) ⊂ recoverable ⊂ all schedules
- Source: entries/2026/06/19/wiki-Serializability.md
- Source URL: https://en.wikipedia.org/wiki/Serializability

### [ACCEPT] serializability-recoverability-orthogonal
Serializability and recoverability are orthogonal properties — a schedule can be serializable but not recoverable, and vice versa
- Source: entries/2026/06/19/wiki-Serializability.md
- Source URL: https://en.wikipedia.org/wiki/Serializability

### [ACCEPT] ss2pl-enforces-conflict-serializable-and-strict
Strong strict two-phase locking (SS2PL) produces schedules that are both conflict-serializable and strict
- Source: entries/2026/06/19/wiki-Serializability.md
- Source URL: https://en.wikipedia.org/wiki/Serializability

### [ACCEPT] snapshot-isolation-permits-write-skew
Snapshot isolation prevents dirty reads, non-repeatable reads, and phantom reads, but permits write skew anomalies, making it strictly weaker than serializability
- Source: entries/2026/06/19/wiki-Serializable_snapshot_isolation.md
- Source URL: https://en.wikipedia.org/wiki/Serializable_snapshot_isolation

### [ACCEPT] si-write-write-conflict-only
Snapshot isolation detects only write-write conflicts (first-committer-wins rule); it does not detect read-write conflicts (rw-antidependencies), which is why write skew can occur
- Source: entries/2026/06/19/wiki-Serializable_snapshot_isolation.md
- Source URL: https://en.wikipedia.org/wiki/Serializable_snapshot_isolation

### [ACCEPT] ssi-postgresql-9-1
Serializable Snapshot Isolation (SSI) was introduced by Cahill et al. (2008) and adopted in PostgreSQL 9.1, providing true serializability on top of MVCC
- Source: entries/2026/06/19/wiki-Serializable_snapshot_isolation.md
- Source URL: https://en.wikipedia.org/wiki/Serializable_snapshot_isolation

### [ACCEPT] oracle-si-mislabeled-serializable
Oracle labels snapshot isolation as 'serializable' mode, which is misleading because it does not prevent write skew and is not true serializability
- Source: entries/2026/06/19/wiki-Snapshot_isolation.md
- Source URL: https://en.wikipedia.org/wiki/Snapshot_isolation

### [ACCEPT] write-skew-workarounds-materialize-or-promote
Two workarounds for write skew under snapshot isolation are: (1) materialize the conflict via a summary table forcing write-write conflicts, or (2) promote reads to writes using SELECT FOR UPDATE or self-assignment updates
- Source: entries/2026/06/19/wiki-Snapshot_isolation.md
- Source URL: https://en.wikipedia.org/wiki/Snapshot_isolation

### [ACCEPT] shadow-paging-provides-atomicity-durability
Shadow paging provides atomicity and durability (two of four ACID properties) by avoiding in-place updates — pages are copied on write and activated by atomically swapping references
- Source: entries/2026/06/19/wiki-Shadow_paging.md
- Source URL: https://en.wikipedia.org/wiki/Shadow_paging

### [ACCEPT] shadow-paging-recursive-cost-problem
Shadow paging's main performance weakness is the recursive update problem: modifying a leaf page can cascade updates through all ancestor pages up to the root/superblock
- Source: entries/2026/06/19/wiki-Shadow_paging.md
- Source URL: https://en.wikipedia.org/wiki/Shadow_paging

### [ACCEPT] wal-more-popular-than-shadow-paging
Write-ahead logging (WAL) is described as more widely adopted in practice than shadow paging for database crash recovery
- Source: entries/2026/06/19/wiki-Shadow_paging.md
- Source URL: https://en.wikipedia.org/wiki/Shadow_paging

### [ACCEPT] skip-list-olog-n-average-on-worst
Skip lists provide O(log n) average-case complexity for search, insertion, and deletion, but O(n) worst case for all three operations
- Source: entries/2026/06/19/wiki-Skip_list.md
- Source URL: https://en.wikipedia.org/wiki/Skip_list

### [ACCEPT] skip-list-probabilistic-promotion
Skip list elements are promoted to higher layers with fixed probability p (commonly 1/2 or 1/4); p=1/e minimizes average search time while p=1/2 simplifies implementation
- Source: entries/2026/06/19/wiki-Skip_list.md
- Source URL: https://en.wikipedia.org/wiki/Skip_list

### [ACCEPT] skip-list-real-world-usage
Skip lists are used in production systems including Redis (sorted sets), RocksDB (memtable), Java ConcurrentSkipListMap, and Lucene (posting lists)
- Source: entries/2026/06/19/wiki-Skip_list.md
- Source URL: https://en.wikipedia.org/wiki/Skip_list

### [ACCEPT] skip-list-concurrency-advantage-over-trees
Skip lists support lock-free concurrent implementations and parallel insertions without global rebalancing, giving them a concurrency advantage over balanced trees
- Source: entries/2026/06/19/wiki-Skip_list.md
- Source URL: https://en.wikipedia.org/wiki/Skip_list

### [ACCEPT] si-satisfies-all-sql92-anomaly-prohibitions
Snapshot isolation satisfies all anomaly prohibitions defined in the ANSI SQL-92 standard yet is not serializable, demonstrating the inadequacy of the standard's anomaly-based isolation level definitions (Berenson et al., 1995)
- Source: entries/2026/06/19/wiki-Snapshot_isolation.md
- Source URL: https://en.wikipedia.org/wiki/Snapshot_isolation

### [ACCEPT] interbase-first-known-si-implementation
InterBase (1985) was the first known implementation of snapshot isolation, predating the formal definition of the concept
- Source: entries/2026/06/19/wiki-Snapshot_isolation.md
- Source URL: https://en.wikipedia.org/wiki/Snapshot_isolation

### [ACCEPT] sort-merge-join-two-phase
The sort-merge join algorithm works in two phases: (1) sort both relations on the join key, (2) merge the sorted relations with interleaved linear scans.
- Source: entries/2026/06/19/wiki-Sort-merge_join.md
- Source URL: https://en.wikipedia.org/wiki/Sort-merge_join

### [ACCEPT] sort-merge-join-presorted-io-complexity
Sort-merge join on pre-sorted inputs has I/O complexity O(P_r + P_s), linear in the number of pages for both relations.
- Source: entries/2026/06/19/wiki-Sort-merge_join.md
- Source URL: https://en.wikipedia.org/wiki/Sort-merge_join

### [ACCEPT] sort-merge-join-unsorted-io-complexity
Sort-merge join on unsorted inputs has I/O complexity O(P_r·log(P_r) + P_s·log(P_s)), dominated by external sorting cost.
- Source: entries/2026/06/19/wiki-Sort-merge_join.md
- Source URL: https://en.wikipedia.org/wiki/Sort-merge_join

### [ACCEPT] sort-merge-join-interesting-order-optimization
A query optimizer may choose a locally suboptimal operator if it produces an interesting order (pre-sorted output) that benefits downstream sort-merge joins, yielding a globally better plan.
- Source: entries/2026/06/19/wiki-Sort-merge_join.md
- Source URL: https://en.wikipedia.org/wiki/Sort-merge_join

### [ACCEPT] sort-merge-join-mark-restore-duplicates
Sort-merge join uses a mark/restore mechanism to handle duplicate join keys, replaying the left relation's matching group for each new matching right row to produce the Cartesian product of matching groups.
- Source: entries/2026/06/19/wiki-Sort-merge_join.md
- Source URL: https://en.wikipedia.org/wiki/Sort-merge_join

### [ACCEPT] sort-merge-join-is-symmetric
Sort-merge join is symmetric: unlike nested loop join, neither relation is designated as inner or outer — both are scanned linearly.
- Source: entries/2026/06/19/wiki-Sort-merge_join.md
- Source URL: https://en.wikipedia.org/wiki/Sort-merge_join

### [ACCEPT] clustered-index-one-per-table
Only one clustered index is allowed per table because it defines the physical storage order of the data rows.
- Source: entries/2026/06/19/wiki-Sparse_index.md
- Source URL: https://en.wikipedia.org/wiki/Sparse_index

### [ACCEPT] dense-vs-sparse-index-definition
A dense index has one entry per record in the data file; a sparse index has one entry per block and requires the data to be sorted/clustered.
- Source: entries/2026/06/19/wiki-Sparse_index.md
- Source URL: https://en.wikipedia.org/wiki/Sparse_index

### [ACCEPT] composite-index-leftmost-prefix-rule
Only the leftmost prefix of columns in a composite index can be used efficiently; queries that skip leading columns require scanning the index.
- Source: entries/2026/06/19/wiki-Sparse_index.md
- Source URL: https://en.wikipedia.org/wiki/Sparse_index

### [ACCEPT] leading-wildcard-not-sargable
A LIKE predicate with a leading wildcard (e.g., LIKE '%value') is not sargable and forces a full table or index scan.
- Source: entries/2026/06/19/wiki-Sparse_index.md
- Source URL: https://en.wikipedia.org/wiki/Sparse_index

### [ACCEPT] covering-index-avoids-table-lookup
A covering index contains all columns needed by a query, enabling an index-only scan that eliminates access to the base table.
- Source: entries/2026/06/19/wiki-Sparse_index.md
- Source URL: https://en.wikipedia.org/wiki/Sparse_index

### [ACCEPT] sql-include-clause-leaf-only
The INCLUDE clause in CREATE INDEX stores non-key columns only at the leaf level of the index, reducing index size while enabling index-only scans.
- Source: entries/2026/06/19/wiki-Sparse_index.md
- Source URL: https://en.wikipedia.org/wiki/Sparse_index

### [ACCEPT] bitmap-index-low-cardinality
Bitmap indexes are optimized for low-cardinality columns (e.g., gender, boolean flags) where B-tree indexes are inefficient.
- Source: entries/2026/06/19/wiki-Sparse_index.md
- Source URL: https://en.wikipedia.org/wiki/Sparse_index

### [ACCEPT] no-iso-sql-create-index-standard
There is no ISO SQL standard for CREATE INDEX — index creation syntax is vendor-specific.
- Source: entries/2026/06/19/wiki-Sparse_index.md
- Source URL: https://en.wikipedia.org/wiki/Sparse_index

### [ACCEPT] sql-server-clustered-index-leaf-contains-data
In SQL Server, clustered index leaf nodes contain the actual data rows, not just pointers; non-clustered index leaf nodes contain pointers.
- Source: entries/2026/06/19/wiki-Sparse_index.md
- Source URL: https://en.wikipedia.org/wiki/Sparse_index

### [ACCEPT] split-brain-definition
Split-brain occurs when cluster nodes lose communication but continue operating independently, each believing it is the sole active node, leading to divergent data sets.
- Source: entries/2026/06/19/wiki-Split-brain_computing.md
- Source URL: https://en.wikipedia.org/wiki/Split-brain_(computing)

### [ACCEPT] split-brain-optimistic-vs-pessimistic
The optimistic approach to split-brain lets partitioned nodes continue operating (favoring availability, requiring reconciliation); the pessimistic approach uses quorum voting to restrict writes to the majority partition (favoring consistency).
- Source: entries/2026/06/19/wiki-Split-brain_computing.md
- Source URL: https://en.wikipedia.org/wiki/Split-brain_(computing)

### [ACCEPT] two-node-cluster-split-brain-vulnerability
Two-node clusters without a quorum witness have at least a 50% probability of total cluster failure when heartbeat communication is lost.
- Source: entries/2026/06/19/wiki-Split-brain_computing.md
- Source URL: https://en.wikipedia.org/wiki/Split-brain_(computing)

### [ACCEPT] mongodb-pessimistic-hazelcast-optimistic
MongoDB uses a pessimistic (quorum-based) approach to split-brain; Hazelcast uses an optimistic (auto-reconciliation) approach.
- Source: entries/2026/06/19/wiki-Split-brain_computing.md
- Source URL: https://en.wikipedia.org/wiki/Split-brain_(computing)

### [ACCEPT] split-brain-dns-deliberate-design
Split-brain DNS (split-horizon DNS) is a deliberate design choice providing separate internal and external DNS namespaces, not an error condition.
- Source: entries/2026/06/19/wiki-Split-brain_computing.md
- Source URL: https://en.wikipedia.org/wiki/Split-brain_(computing)

### [ACCEPT] quorum-requires-majority-odd-preferred
Quorum-based partition handling requires a majority of votes, which is why odd-numbered node counts or witness devices are preferred in cluster design.
- Source: entries/2026/06/19/wiki-Split-brain_computing.md
- Source URL: https://en.wikipedia.org/wiki/Split-brain_(computing)

### [ACCEPT] stable-storage-atomicity-guarantee
Stable storage guarantees that a read after a write returns either the new data or the old data — never corrupted, partial, or torn results.
- Source: entries/2026/06/19/wiki-Stable_storage.md
- Source URL: https://en.wikipedia.org/wiki/Stable_storage

### [ACCEPT] conventional-disks-not-stable-storage
Most conventional disk drives are not stable storage because they do not guarantee atomic writes — a read after write could return an error rather than either old or new data.
- Source: entries/2026/06/19/wiki-Stable_storage.md
- Source URL: https://en.wikipedia.org/wiki/Stable_storage

### [ACCEPT] stable-storage-implementation-dual-write-vs-raid
Stable storage can be implemented via software dual-write (two locations on the same disk, protects against bad sectors) or RAID mirroring (separate disks, protects against entire disk failures); RAID level 1 or greater is required.
- Source: entries/2026/06/19/wiki-Stable_storage.md
- Source URL: https://en.wikipedia.org/wiki/Stable_storage

### [ACCEPT] smr-2f-plus-1-replicas
State machine replication tolerating F arbitrary failures requires 2F+1 replicas; fail-stop failures require only F+1; malicious Byzantine faults without cryptographic signatures require 3F+1.
- Source: entries/2026/06/19/wiki-State_machine_replication.md
- Source URL: https://en.wikipedia.org/wiki/State_machine_replication

### [ACCEPT] smr-determinism-requirement
State machine replication requires all replicas to be deterministic: the same inputs in the same order must produce identical states and outputs across all replicas.
- Source: entries/2026/06/19/wiki-State_machine_replication.md
- Source URL: https://en.wikipedia.org/wiki/State_machine_replication

### [ACCEPT] smr-three-replicas-minimum-fault-tolerance
Three replicas is the minimum for any fault tolerance in state machine replication — two copies cannot identify which one is faulty.
- Source: entries/2026/06/19/wiki-State_machine_replication.md
- Source URL: https://en.wikipedia.org/wiki/State_machine_replication

### [ACCEPT] smr-consensus-vs-causal-ordering
In state machine replication, causal ordering works only when all communication channels are visible to the protocol; hidden channels (e.g., out-of-band client communication) require consensus-based ordering.
- Source: entries/2026/06/19/wiki-State_machine_replication.md
- Source URL: https://en.wikipedia.org/wiki/State_machine_replication

### [ACCEPT] paxos-leader-liveness-not-safety
In Paxos, a leader is required for liveness but not safety — multiple replicas may simultaneously believe they are leader without violating correctness.
- Source: entries/2026/06/19/wiki-State_machine_replication.md
- Source URL: https://en.wikipedia.org/wiki/State_machine_replication

### [ACCEPT] smr-checkpoint-bounds-log-growth
In state machine replication, checkpoints snapshot current state so that log entries before the checkpoint can be discarded, bounding log growth.
- Source: entries/2026/06/19/wiki-State_machine_replication.md
- Source URL: https://en.wikipedia.org/wiki/State_machine_replication

### [ACCEPT] flp-impossibility-result
The Fischer-Lynch-Paterson (FLP) impossibility result proves that consensus is impossible in purely asynchronous systems with even one faulty process; practical SMR protocols work around this via eventual leader assumptions or partial synchrony.
- Source: entries/2026/06/19/wiki-State_machine_replication.md
- Source URL: https://en.wikipedia.org/wiki/State_machine_replication

### [ACCEPT] stream-processing-kernel-function-applied-to-each-element
In stream processing, a kernel function (compute kernel) is applied to each element in a stream, which is the fundamental abstraction of the paradigm.
- Source: entries/2026/06/19/wiki-Stream_processing.md
- Source URL: https://en.wikipedia.org/wiki/Stream_processing

### [ACCEPT] stream-processing-three-suitability-criteria
Three characteristics make applications suitable for stream processing: compute intensity (high arithmetic-to-I/O ratio), data parallelism (same function applied independently to all records), and data locality (data produced once, read once or twice, never again).
- Source: entries/2026/06/19/wiki-Stream_processing.md
- Source URL: https://en.wikipedia.org/wiki/Stream_processing

### [ACCEPT] stream-processing-write-only-output-constraint
Stream processing enforces a write-only output constraint: for each record, you can read input and write output, but no memory region is both readable and writable simultaneously.
- Source: entries/2026/06/19/wiki-Stream_processing.md
- Source URL: https://en.wikipedia.org/wiki/Stream_processing

### [ACCEPT] soa-preferred-over-aos-for-simd-stream
Structure of Arrays (SoA) layout is preferred over Array of Structures (AoS) for SIMD/stream processing because it keeps like-typed data contiguous and aligned for vectorized access.
- Source: entries/2026/06/19/wiki-Stream_processing.md
- Source URL: https://en.wikipedia.org/wiki/Stream_processing

### [ACCEPT] stream-register-file-shared-cache
The Stream Register File (SRF) is a large on-chip shared cache between ALU clusters and external memory, with allocation automated by the compiler.
- Source: entries/2026/06/19/wiki-Stream_processing.md
- Source URL: https://en.wikipedia.org/wiki/Stream_processing

### [ACCEPT] dedicated-stream-processors-10x-speedup
Dedicated stream processors achieve greater than 10x speedup over sequential execution, while generic CPUs see only approximately 1.5x from stream processing techniques.
- Source: entries/2026/06/19/wiki-Stream_processing.md
- Source URL: https://en.wikipedia.org/wiki/Stream_processing

### [ACCEPT] short-stream-effect-penalty
The short stream effect is a performance penalty incurred when streams are too small to amortize kernel-switching and setup costs.
- Source: entries/2026/06/19/wiki-Stream_processing.md
- Source URL: https://en.wikipedia.org/wiki/Stream_processing

### [ACCEPT] stream-processor-90pct-work-on-chip
Approximately 90% of stream processor work is done on-chip, requiring only about 1% of global data to be stored to external memory.
- Source: entries/2026/06/19/wiki-Stream_processing.md
- Source URL: https://en.wikipedia.org/wiki/Stream_processing

### [ACCEPT] continuous-sql-range-interval-for-stream-joins
Continuous SQL queries use RANGE INTERVAL and OVER clauses with time windows to join event streams in stream processing systems.
- Source: entries/2026/06/19/wiki-Stream_processing.md
- Source URL: https://en.wikipedia.org/wiki/Stream_processing

### [ACCEPT] 3pc-adds-precommit-phase-to-2pc
The three-phase commit protocol (3PC) extends 2PC by adding a PreCommit (Prepared to commit) phase between the voting and commit phases, which eliminates indefinite blocking when both the coordinator and a cohort fail during commit.
- Source: entries/2026/06/19/wiki-Three-phase_commit_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Three-phase_commit_protocol

### [ACCEPT] 3pc-three-phases-cancommit-precommit-docommit
The three phases of 3PC are: (1) CanCommit (voting), (2) PreCommit (prepared to commit), and (3) DoCommit (actual commit).
- Source: entries/2026/06/19/wiki-Three-phase_commit_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Three-phase_commit_protocol

### [ACCEPT] 3pc-requires-at-least-3-round-trips
3PC requires at least 3 round trips (RTTs), making it higher latency than 2PC.
- Source: entries/2026/06/19/wiki-Three-phase_commit_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Three-phase_commit_protocol

### [ACCEPT] 3pc-cannot-guarantee-atomicity-unbounded-delay
3PC cannot guarantee atomicity in systems with unbounded network delay and process pauses, which makes it impractical for most real-world distributed systems.
- Source: entries/2026/06/19/wiki-Three-phase_commit_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Three-phase_commit_protocol

### [ACCEPT] 3pc-coordinator-waits-all-precommit-acks
In 3PC, the coordinator will not send doCommit until all cohort members have acknowledged PreCommit, which prevents ambiguous states during recovery.
- Source: entries/2026/06/19/wiki-Three-phase_commit_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Three-phase_commit_protocol

### [ACCEPT] e3pc-keidar-dolev-quorum-progress
E3PC (Keidar and Dolev) is a refinement of Skeen's original 3PC that allows a quorum to always make progress even during network partitioning.
- Source: entries/2026/06/19/wiki-Three-phase_commit_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Three-phase_commit_protocol

### [ACCEPT] tombstone-prevents-deleted-data-resurrection
A tombstone is a marker record in an eventually consistent data store that prevents deleted data from being resurrected by replicas that missed the delete operation.
- Source: entries/2026/06/19/wiki-Tombstone_data_store.md
- Source URL: https://en.wikipedia.org/wiki/Tombstone_(data_store)

### [ACCEPT] tombstone-resurrection-problem-mechanism
Without tombstones, a node that missed a delete would interpret the absence of data on other nodes as a missed insert and re-propagate the deleted data (the resurrection problem).
- Source: entries/2026/06/19/wiki-Tombstone_data_store.md
- Source URL: https://en.wikipedia.org/wiki/Tombstone_(data_store)

### [ACCEPT] cassandra-gcgraceseconds-tombstone-retention
In Apache Cassandra, GCGraceSeconds controls how long tombstones are retained before being eligible for garbage collection during compaction.
- Source: entries/2026/06/19/wiki-Tombstone_data_store.md
- Source URL: https://en.wikipedia.org/wiki/Tombstone_(data_store)

### [ACCEPT] tombstones-consume-storage-until-compaction
Tombstones are not returned to clients but still consume storage and I/O until compacted, and excessive tombstones degrade read performance because the system must skip over them.
- Source: entries/2026/06/19/wiki-Tombstone_data_store.md
- Source URL: https://en.wikipedia.org/wiki/Tombstone_(data_store)

### [ACCEPT] tombstone-removal-tied-to-lsm-compaction
Tombstone removal is tied to the LSM-tree compaction process in systems like Apache Cassandra.
- Source: entries/2026/06/19/wiki-Tombstone_data_store.md
- Source URL: https://en.wikipedia.org/wiki/Tombstone_(data_store)

### [ACCEPT] transaction-log-guarantees-atomicity-durability
Transaction logs guarantee the atomicity and durability properties of ACID by enabling rollback of uncommitted transactions and re-application of committed-but-unmaterialized transactions after a crash.
- Source: entries/2026/06/19/wiki-Transaction_log.md
- Source URL: https://en.wikipedia.org/wiki/Transaction_log

### [ACCEPT] lsn-monotonically-increasing-identifier
A Log Sequence Number (LSN) is a unique, monotonically increasing identifier for each log record, essential for recovery algorithms like ARIES.
- Source: entries/2026/06/19/wiki-Transaction_log.md
- Source URL: https://en.wikipedia.org/wiki/Transaction_log

### [ACCEPT] log-records-linked-list-via-prev-lsn
Transaction log records form a linked list via Prev LSN pointers, enabling navigation through the log chain.
- Source: entries/2026/06/19/wiki-Transaction_log.md
- Source URL: https://en.wikipedia.org/wiki/Transaction_log

### [ACCEPT] clr-one-to-one-with-update-records
Compensation Log Records (CLRs) have a 1:1 correspondence with Update Log Records and contain an undoNextLSN field to record the rollback of a specific update.
- Source: entries/2026/06/19/wiki-Transaction_log.md
- Source URL: https://en.wikipedia.org/wiki/Transaction_log

### [ACCEPT] checkpoint-redo-lsn-and-undo-lsn
Checkpoint log records contain two critical LSNs: redoLSN (first update not yet flushed to disk, where redo begins) and undoLSN (oldest record of the oldest in-progress transaction, needed for undo).
- Source: entries/2026/06/19/wiki-Transaction_log.md
- Source URL: https://en.wikipedia.org/wiki/Transaction_log

### [ACCEPT] transaction-logs-stored-stable-storage
Transaction logs are stored in stable storage, and this physical guarantee is what makes the durability promise possible.
- Source: entries/2026/06/19/wiki-Transaction_log.md
- Source URL: https://en.wikipedia.org/wiki/Transaction_log

### [ACCEPT] 2pc-is-blocking-protocol
Two-phase commit (2PC) is a blocking protocol: if the coordinator fails permanently after participants have voted Yes, those participants cannot unilaterally commit or abort and must wait indefinitely.
- Source: entries/2026/06/19/wiki-Two-phase_commit_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Two-phase_commit_protocol

### [ACCEPT] 2pc-commit-only-if-all-vote-yes
In 2PC, the commit decision rule is: commit only if all participants vote Yes; abort if any participant votes No or times out.
- Source: entries/2026/06/19/wiki-Two-phase_commit_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Two-phase_commit_protocol

### [ACCEPT] 2pc-coordinator-plus-participant-failure-unrecoverable
A simultaneous coordinator and participant failure during the 2PC commit phase is not safely recoverable because the system cannot determine whether the failed participant had already committed.
- Source: entries/2026/06/19/wiki-Two-phase_commit_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Two-phase_commit_protocol

### [ACCEPT] 2pc-force-write-log-before-sending-messages
In 2PC, all protocol state transitions must be force-written to stable storage before sending protocol messages; without this, crash recovery cannot determine the node's vote or decision.
- Source: entries/2026/06/19/wiki-Two-phase_commit_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Two-phase_commit_protocol

### [ACCEPT] 2pc-presumed-abort-optimization
The presumed abort optimization in 2PC assumes abort when no commit evidence is found in the log during recovery, saving the need to log abort decisions.
- Source: entries/2026/06/19/wiki-Two-phase_commit_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Two-phase_commit_protocol

### [ACCEPT] 2pc-not-2pl-distinct-concepts
Two-phase commit (2PC, atomicity across nodes) is entirely distinct from two-phase locking (2PL, concurrency control within a database), though they are frequently confused.
- Source: entries/2026/06/19/wiki-Two-phase_commit_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Two-phase_commit_protocol

### [ACCEPT] dynamic-2pc-no-predetermined-coordinator
Dynamic 2PC (D2PC) has no predetermined coordinator; agreement messages race from leaves inward and the coordinator is determined at the collision point, achieving time-optimal commit for any tree topology.
- Source: entries/2026/06/19/wiki-Two-phase_commit_protocol.md
- Source URL: https://en.wikipedia.org/wiki/Two-phase_commit_protocol

### [ACCEPT] 2pl-no-lock-after-release
Two-phase locking requires that a transaction never acquire a lock after it has released any lock, dividing lock management into an expanding phase (acquire only) and a shrinking phase (release only)
- Source: entries/2026/06/19/wiki-Two-phase_locking.md
- Source URL: https://en.wikipedia.org/wiki/Two-phase_locking

### [ACCEPT] 2pl-guarantees-conflict-serializability
All two-phase locking variants guarantee conflict-serializability, and all conflict-serializable schedules are also view-serializable (but not vice versa)
- Source: entries/2026/06/19/wiki-Two-phase_locking.md
- Source URL: https://en.wikipedia.org/wiki/Two-phase_locking

### [ACCEPT] basic-2pl-not-recoverable
Basic 2PL guarantees conflict-serializability but does not guarantee recoverability, strictness, or prevent phantom/dirty reads
- Source: entries/2026/06/19/wiki-Two-phase_locking.md
- Source URL: https://en.wikipedia.org/wiki/Two-phase_locking

### [ACCEPT] c2pl-only-variant-preventing-deadlocks
Conservative 2PL (C2PL) is the only 2PL variant that prevents deadlocks, by requiring all locks to be acquired before execution begins, but it is rarely used because transactions must declare their complete read/write set in advance
- Source: entries/2026/06/19/wiki-Two-phase_locking.md
- Source URL: https://en.wikipedia.org/wiki/Two-phase_locking

### [ACCEPT] s2pl-holds-write-locks-until-commit
Strict 2PL (S2PL) holds write (exclusive) locks until transaction commits or aborts but releases read (shared) locks during the shrinking phase, guaranteeing recoverability and strictness
- Source: entries/2026/06/19/wiki-Two-phase_locking.md
- Source URL: https://en.wikipedia.org/wiki/Two-phase_locking

### [ACCEPT] ss2pl-holds-all-locks-until-commit
Strong Strict 2PL (SS2PL / Rigorous 2PL) holds both read and write locks until transaction ends (commit or abort), effectively having no shrinking phase until that point
- Source: entries/2026/06/19/wiki-Two-phase_locking.md
- Source URL: https://en.wikipedia.org/wiki/Two-phase_locking

### [ACCEPT] 2pl-variant-set-inclusion
The 2PL variants form a strict inclusion hierarchy: SS2PL ⊂ S2PL ⊂ 2PL — every SS2PL schedule is S2PL, and every S2PL schedule is 2PL
- Source: entries/2026/06/19/wiki-Two-phase_locking.md
- Source URL: https://en.wikipedia.org/wiki/Two-phase_locking

### [ACCEPT] 2pl-not-2pc
Two-phase locking (2PL) is a concurrency control protocol, distinct from two-phase commit (2PC) which is a distributed transaction consensus protocol — the 'two phases' in each refer to different things
- Source: entries/2026/06/19/wiki-Two-phase_locking.md
- Source URL: https://en.wikipedia.org/wiki/Two-phase_locking

### [ACCEPT] vlq-base128-continuation-bit
Variable-length quantity (VLQ) encoding uses base-128 representation where each byte carries 7 bits of payload and the MSB (bit 7) serves as a continuation flag: 1 means more bytes follow, 0 means last byte
- Source: entries/2026/06/19/wiki-Variable-length_quantity.md
- Source URL: https://en.wikipedia.org/wiki/Variable-length_quantity

### [ACCEPT] vlq-big-endian-leb128-little-endian
VLQ is big-endian (most significant group first) while LEB128 is little-endian (least significant group first); this byte order is the only difference between them
- Source: entries/2026/06/19/wiki-Variable-length_quantity.md
- Source URL: https://en.wikipedia.org/wiki/Variable-length_quantity

### [ACCEPT] vlq-basic-redundancy-git-bijective
Basic VLQ is redundant (multiple encodings per value via zero-padding with 0x80 octets); Git's pack format uses a bijective variant that eliminates redundancy by adding an offset so each integer has exactly one encoding
- Source: entries/2026/06/19/wiki-Variable-length_quantity.md
- Source URL: https://en.wikipedia.org/wiki/Variable-length_quantity

### [ACCEPT] zigzag-encoding-formula
Zigzag encoding (used in Protocol Buffers) maps signed integers to unsigned via (n << 1) ^ (n >> (k-1)), interleaving positives and negatives (0→0, -1→1, 1→2, -2→3) so small-magnitude values always use few bytes
- Source: entries/2026/06/19/wiki-Variable-length_quantity.md
- Source URL: https://en.wikipedia.org/wiki/Variable-length_quantity

### [ACCEPT] vlq-max-values-per-byte-count
VLQ maximum values by byte count: 1 byte = 127, 2 bytes = 16383, 3 bytes = 2097151, 4 bytes = 268435455 (each step is 2^7 times the previous range)
- Source: entries/2026/06/19/wiki-Variable-length_quantity.md
- Source URL: https://en.wikipedia.org/wiki/Variable-length_quantity

### [ACCEPT] group-varint-encoding-reduces-branches
Group Varint Encoding (GVE) uses a 1-byte header to describe the lengths of 4 following uint32 values, eliminating per-byte continuation-bit checks and reducing CPU branch mispredictions
- Source: entries/2026/06/19/wiki-Variable-length_quantity.md
- Source URL: https://en.wikipedia.org/wiki/Variable-length_quantity

### [ACCEPT] vector-clock-structure-n-logical-clocks
A vector clock for a system of n processes is an array of n logical clocks (one per process), where each process maintains its own clock and tracks the largest known value of every other process's clock
- Source: entries/2026/06/19/wiki-Vector_clock.md
- Source URL: https://en.wikipedia.org/wiki/Vector_clock

### [ACCEPT] vector-clocks-detect-concurrency-lamport-cannot
Vector clocks can distinguish between causally related and concurrent events, while Lamport timestamps cannot — if neither VC(a) < VC(b) nor VC(b) < VC(a), the events are concurrent
- Source: entries/2026/06/19/wiki-Vector_clock.md
- Source URL: https://en.wikipedia.org/wiki/Vector_clock

### [ACCEPT] vector-clock-merge-is-elementwise-max
The vector clock merge operation on message receive is element-wise maximum (not addition): VC_i[k] ← max(VC_i[k], VC_j[k]) for all k, after incrementing the receiver's own clock
- Source: entries/2026/06/19/wiki-Vector_clock.md
- Source URL: https://en.wikipedia.org/wiki/Vector_clock

### [ACCEPT] vector-clock-comparison-rule
VC(x) < VC(y) iff every component of VC(x) is ≤ the corresponding component of VC(y) and at least one component is strictly less
- Source: entries/2026/06/19/wiki-Vector_clock.md
- Source URL: https://en.wikipedia.org/wiki/Vector_clock

### [ACCEPT] vector-clocks-o-n-space-per-process
Vector clocks use O(n) space per process where n is the number of processes, which is a key scalability limitation
- Source: entries/2026/06/19/wiki-Vector_clock.md
- Source URL: https://en.wikipedia.org/wiki/Vector_clock

### [ACCEPT] vector-clocks-fail-under-byzantine-faults
Vector clocks are ineffective under Byzantine failures — causality detection is fundamentally impossible when processes behave arbitrarily or maliciously
- Source: entries/2026/06/19/wiki-Vector_clock.md
- Source URL: https://en.wikipedia.org/wiki/Vector_clock

### [ACCEPT] vector-clocks-fidge-mattern-1988
Vector clocks are canonically attributed to Fidge and Mattern (both 1988, independently), though the concept appeared in at least 6 earlier papers from 1982–1987
- Source: entries/2026/06/19/wiki-Vector_clock.md
- Source URL: https://en.wikipedia.org/wiki/Vector_clock

### [ACCEPT] virtual-nodes-consistent-hash-ring
Virtual nodes in distributed systems (e.g., Amazon Dynamo) map a single physical node to multiple positions in a consistent hash ring to handle heterogeneous node capacity
- Source: entries/2026/06/19/wiki-Virtual_node.md
- Source URL: https://en.wikipedia.org/wiki/Virtual_node

### [ACCEPT] passive-devices-not-nodes
Passive distribution points such as patch panels and distribution frames are explicitly not network nodes — a node must be an electronic device capable of creating, receiving, or transmitting information
- Source: entries/2026/06/19/wiki-Virtual_node.md
- Source URL: https://en.wikipedia.org/wiki/Virtual_node

### [ACCEPT] internet-hosts-subset-physical-nodes
All Internet hosts are physical network nodes, but not all physical network nodes are Internet hosts — switches and bridges lack IP addresses and are not Internet nodes
- Source: entries/2026/06/19/wiki-Virtual_node.md
- Source URL: https://en.wikipedia.org/wiki/Virtual_node

### [ACCEPT] watermark-enables-incremental-sync
A watermark in data synchronization is a point-in-time reference that enables incremental/delta synchronization — only objects created, modified, or deleted after the watermark are transferred
- Source: entries/2026/06/19/wiki-Watermark_data_synchronization.md
- Source URL: https://en.wikipedia.org/wiki/Watermark_(data_synchronization)

### [ACCEPT] dirsync-first-query-empty-cookie
In LDAP DirSync, the first query uses an empty cookie and returns the full result set; subsequent queries pass the previous cookie and receive only changes since that cookie was issued
- Source: entries/2026/06/19/wiki-Watermark_data_synchronization.md
- Source URL: https://en.wikipedia.org/wiki/Watermark_(data_synchronization)

### [ACCEPT] watermark-analogous-to-kafka-offset
Watermarks in data synchronization serve an analogous role to offsets in log-based replication systems such as Kafka consumer offsets
- Source: entries/2026/06/19/wiki-Watermark_data_synchronization.md
- Source URL: https://en.wikipedia.org/wiki/Watermark_(data_synchronization)

### [ACCEPT] flash-nand-erase-cycle-limit-3k-5k
Standard NAND flash memory segments have a write endurance limit of approximately 3,000–5,000 erase cycles
- Source: entries/2026/06/19/wiki-Wear_leveling.md
- Source URL: https://en.wikipedia.org/wiki/Wear_leveling

### [ACCEPT] wear-leveling-logical-to-physical-indirection-map
Wear leveling uses an indirection map linking logical block addresses (LBAs) to physical flash addresses, allowing writes to be redirected to less-worn blocks
- Source: entries/2026/06/19/wiki-Wear_leveling.md
- Source URL: https://en.wikipedia.org/wiki/Wear_leveling

### [ACCEPT] dynamic-wear-leveling-only-remaps-written-blocks
Dynamic wear leveling only remaps blocks that receive new writes; static/cold data blocks never move and never share the wear burden
- Source: entries/2026/06/19/wiki-Wear_leveling.md
- Source URL: https://en.wikipedia.org/wiki/Wear_leveling

### [ACCEPT] static-wear-leveling-relocates-cold-data
Static wear leveling extends dynamic wear leveling by periodically relocating cold data blocks so their low-usage cells can be repurposed for active writes, enabling longer device life at the cost of higher complexity and lower performance
- Source: entries/2026/06/19/wiki-Wear_leveling.md
- Source URL: https://en.wikipedia.org/wiki/Wear_leveling

### [ACCEPT] traditional-filesystems-harm-flash-metadata-rewrites
Traditional file systems (FAT, NTFS, EXT, HFS+, UFS) harm flash storage by repeatedly overwriting metadata structures (directories, timestamps) to the same physical locations, concentrating wear
- Source: entries/2026/06/19/wiki-Wear_leveling.md
- Source URL: https://en.wikipedia.org/wiki/Wear_leveling

### [ACCEPT] jffs2-yaffs-f2fs-software-wear-leveling
Log-structured file systems JFFS2, YAFFS, and flash-aware file system F2FS implement wear leveling in software for raw flash, while SD cards and USB drives implement it in hardware transparently to the OS
- Source: entries/2026/06/19/wiki-Wear_leveling.md
- Source URL: https://en.wikipedia.org/wiki/Wear_leveling

### [ACCEPT] wear-leveling-write-amplification-tradeoff
Wear leveling can increase write amplification (more physical writes per logical write), creating a tradeoff between even wear distribution and write efficiency
- Source: entries/2026/06/19/wiki-Wear_leveling.md
- Source URL: https://en.wikipedia.org/wiki/Wear_leveling

### [ACCEPT] wal-log-before-write-rule
The write-ahead logging invariant requires that every operation modifying database state must be logged to stable storage before the corresponding data pages are modified on disk
- Source: entries/2026/06/19/wiki-Write-ahead_logging.md
- Source URL: https://en.wikipedia.org/wiki/Write-ahead_logging

### [ACCEPT] wal-provides-atomicity-and-durability
Write-ahead logging provides atomicity and durability (the A and D of ACID), not isolation or consistency
- Source: entries/2026/06/19/wiki-Write-ahead_logging.md
- Source URL: https://en.wikipedia.org/wiki/Write-ahead_logging

### [ACCEPT] wal-stores-redo-and-undo-records
WAL log stores both redo records (to replay committed operations) and undo records (to roll back incomplete operations) for crash recovery
- Source: entries/2026/06/19/wiki-Write-ahead_logging.md
- Source URL: https://en.wikipedia.org/wiki/Write-ahead_logging

### [ACCEPT] wal-enables-in-place-updates
WAL enables in-place data updates, avoiding the overhead of updating indexes and block lists, unlike shadow paging which uses copy-on-write
- Source: entries/2026/06/19/wiki-Write-ahead_logging.md
- Source URL: https://en.wikipedia.org/wiki/Write-ahead_logging

### [ACCEPT] wal-checkpointing-bounds-recovery-time
WAL checkpointing periodically flushes all logged changes to the database and truncates the log, bounding crash recovery time and reclaiming log space
- Source: entries/2026/06/19/wiki-Write-ahead_logging.md
- Source URL: https://en.wikipedia.org/wiki/Write-ahead_logging

### [ACCEPT] aries-canonical-wal-recovery-algorithm
ARIES (Algorithms for Recovery and Isolation Exploiting Semantics) is the most widely referenced WAL-based recovery algorithm, using a three-phase recovery process: analysis, redo, undo
- Source: entries/2026/06/19/wiki-Write-ahead_logging.md
- Source URL: https://en.wikipedia.org/wiki/Write-ahead_logging

### [ACCEPT] filesystem-journaling-is-wal-for-metadata
Journaling file systems (ext4, NTFS, XFS) use WAL variants for metadata consistency, applying the log-before-write principle at the filesystem layer
- Source: entries/2026/06/19/wiki-Write-ahead_logging.md
- Source URL: https://en.wikipedia.org/wiki/Write-ahead_logging

### [ACCEPT] sqlite-wal-mode-pragma
SQLite enables WAL mode via PRAGMA journal_mode=WAL
- Source: entries/2026/06/19/wiki-Write-ahead_logging.md
- Source URL: https://en.wikipedia.org/wiki/Write-ahead_logging

### [ACCEPT] zfs-copy-on-write-never-overwrites-in-place
ZFS uses copy-on-write: it never overwrites data in place, instead writing new data to a new location and atomically updating pointers, which eliminates the RAID write hole and enables cheap snapshots
- Source: entries/2026/06/19/wiki-ZFS.md
- Source URL: https://en.wikipedia.org/wiki/ZFS

### [ACCEPT] zfs-checksums-stored-in-parent-block-pointer
ZFS stores every block's checksum in its parent block pointer (not alongside the data), creating a Merkle tree from leaves to root that detects corruption co-located checksums would miss
- Source: entries/2026/06/19/wiki-ZFS.md
- Source URL: https://en.wikipedia.org/wiki/ZFS

### [ACCEPT] zfs-self-healing-automatic-repair
When ZFS detects a checksum mismatch on read, it automatically reconstructs correct data from redundant copies or parity, repairs the damaged copy, and returns good data transparently
- Source: entries/2026/06/19/wiki-ZFS.md
- Source URL: https://en.wikipedia.org/wiki/ZFS

### [ACCEPT] raidz-dynamic-stripe-width-eliminates-write-hole
RAID-Z uses dynamic stripe width (each block is its own stripe), eliminating the read-modify-write penalty and the RAID write hole without requiring NVRAM or write buffering
- Source: entries/2026/06/19/wiki-ZFS.md
- Source URL: https://en.wikipedia.org/wiki/ZFS

### [ACCEPT] zfs-avoid-hardware-raid-use-hba-jbod
Hardware RAID controllers should not be used with ZFS because they interfere with ZFS's algorithms and reduce reliability; HBA in JBOD passthrough mode should be used instead
- Source: entries/2026/06/19/wiki-ZFS.md
- Source URL: https://en.wikipedia.org/wiki/ZFS

### [ACCEPT] zfs-scrub-online-replaces-fsck
ZFS scrub runs on mounted live filesystems (unlike fsck which requires offline/unmounted), traversing all data and metadata, verifying checksums and repairing corruption
- Source: entries/2026/06/19/wiki-ZFS.md
- Source URL: https://en.wikipedia.org/wiki/ZFS

### [ACCEPT] zfs-io-pipeline-order
The ZFS I/O pipeline processes data in the order: compress, encrypt, checksum, dedup
- Source: entries/2026/06/19/wiki-ZFS.md
- Source URL: https://en.wikipedia.org/wiki/ZFS

### [ACCEPT] zfs-128-bit-addressing-max-sizes
ZFS uses 128-bit addressing with a theoretical max pool size of 2^128 bytes and max file size of 16 EiB (2^64 bytes)
- Source: entries/2026/06/19/wiki-ZFS.md
- Source URL: https://en.wikipedia.org/wiki/ZFS

### [ACCEPT] zfs-requires-ecc-ram-no-in-memory-checksums
ZFS does not checksum in-memory (ARC) data by default, assuming enterprise hardware with ECC RAM; ECC RAM is strongly recommended for ZFS deployments
- Source: entries/2026/06/19/wiki-ZFS.md
- Source URL: https://en.wikipedia.org/wiki/ZFS

### [ACCEPT] zfs-encryption-key-change-without-offline
ZFS encryption wrapping keys can be changed without taking the filesystem offline; data encryption keys are generated at dataset creation and shared only with descendant snapshots and clones
- Source: entries/2026/06/19/wiki-ZFS.md
- Source URL: https://en.wikipedia.org/wiki/ZFS

