---
source: https://en.wikipedia.org/wiki/Log-structured_merge-tree
fetched: 2026-06-19
---

Data structure 
|  | This article includes a list ofgeneral references, butit lacks sufficient correspondinginline citations.Please help toimprovethis article byintroducingmore precise citations.(April 2013)(Learn how and when to remove this message) |
| --- | --- |

 
| Log-structured merge-tree |
| --- |
| Type | Hybrid (two tree-like components) |
| Invented | 1996 |
| Invented by | Patrick O'Neil, Edward Cheng, Dieter Gawlick,Elizabeth O'Neil |
| Time complexityinbig O notationOperationAverageWorst caseInsertO(T * L / B)Find-minO(1)O(L * e^(-M/N))Space complexitySpaceO((T + 1) / T) | Time complexityinbig O notation | Operation | Average | Worst case | Insert | O(T * L / B) |  | Find-min | O(1) | O(L * e^(-M/N)) | Space complexity | Space | O((T + 1) / T) |  |
| Time complexityinbig O notation |
| Operation | Average | Worst case |
| Insert | O(T * L / B) |  |
| Find-min | O(1) | O(L * e^(-M/N)) |
| Space complexity |
| Space | O((T + 1) / T) |  |

 

In [computer science](./Computer_science), the **log-structured merge-tree** (also known as **LSM tree**, or **LSMT**[[1]](./Log-structured_merge-tree#cite_note-1)) is a [data structure](./Data_structure) with performance characteristics that make it attractive for providing [indexed](./Database_index) access to files with high insert volume, such as [transactional log data](./Transaction_log). LSM trees, like other [search trees](./Search_tree), maintain key-value pairs. LSM trees maintain data in two or more separate structures, each of which is optimized for its respective underlying storage medium; data is synchronized between the two structures efficiently, in batches.

 

One simple version of the LSM tree is a two-level LSM tree.[[2]](./Log-structured_merge-tree#cite_note-2) As described by [Patrick O'Neil](./Patrick_O'Neil), a two-level LSM tree comprises two [tree-like](./Tree_(data_structure)) structures, called C0 and C1. C0 is smaller and entirely resident in memory, whereas C1 is resident on disk. New records are inserted into the memory-resident C0 component. If the insertion causes the C0 component to exceed a certain size threshold, a contiguous segment of entries is removed from C0 and merged into C1 on disk. The performance characteristics of LSM trees stem from the fact that each component is tuned to the characteristics of its underlying storage medium, and that data is efficiently migrated across media in rolling batches, using an algorithm reminiscent of [merge sort](./Merge_sort). Such tuning involves writing data in a sequential manner as opposed to as a series of separate random access requests. This optimization reduces total seek time in [hard-disk drives](./Hard_disk_drive) (HDDs) and latency in [solid-state drives](./Solid-state_drive) (SSDs).

 [![Diagram illustrating compaction of data in a log-structured merge tree](//upload.wikimedia.org/wikipedia/commons/thumb/f/f2/LSM_Tree.png/250px-LSM_Tree.png)](./File:LSM_Tree.png)Diagram illustrating compaction of data in a log-structured merge tree 

Most LSM trees used in practice employ multiple levels. Level 0 is kept in main memory, and might be represented using a tree. The on-disk data is organized into sorted *runs* of data. Each run contains data sorted by the index key. A run can be represented on disk as a single file, or alternatively as a collection of files with non-overlapping key ranges. To perform a query on a particular key to get its associated value, one must search in the Level 0 tree and also each run.
The Stepped-Merge version of the LSM tree[[3]](./Log-structured_merge-tree#cite_note-3) is a variant of the LSM tree that supports multiple levels with multiple tree structures at each level.

 

A particular key may appear in several runs, and what that means for a query depends on the application.  Some applications simply want the newest key-value pair with a given key. Some applications must combine the values in some way to get the proper aggregate value to return. For example, in [Apache Cassandra](./Apache_Cassandra), each value represents a row in a database, and different versions of the row may have different sets of columns.[[4]](./Log-structured_merge-tree#cite_note-4)

 

In order to keep down the cost of queries, the system must avoid a situation where there are too many runs.

 

Extensions to the 'leveled' method to incorporate [B+ tree](./B+_tree) structures have been suggested, for example bLSM[[5]](./Log-structured_merge-tree#cite_note-5) and Diff-Index.[[6]](./Log-structured_merge-tree#cite_note-6) LSM-tree was originally designed for write-intensive workloads. As increasingly more read and write workloads co-exist under an LSM-tree storage structure, read data accesses can experience high latency and low throughput due to frequent invalidations of cached data in buffer caches by LSM-tree compaction operations. To re-enable effective buffer caching for fast data accesses, a Log-Structured buffered-Merged tree (LSbM-tree) is proposed and implemented.[[7]](./Log-structured_merge-tree#cite_note-7)

 

## Operations

 

### Write

 

In LSM-trees, write operations are designed to optimize performance by reducing [random I/O](./Random_I/O) and leveraging sequential disk writes. When a write operation is initiated, the data is first buffered in an in-memory component, often implemented using a sorted data structure such as a [Skip list](./Skip_list) or [B+ tree](./B+_tree).

 

Once the in-memory buffer becomes full, it is flushed to the disk as an immutable sorted component at the first level (C1). This flush is performed sequentially, ensuring high I/O efficiency by avoiding the costly random writes typical of traditional indexing methods. To maintain durability, the system may use a [write-ahead log](./Write-ahead_log) (WAL) that records all incoming writes before they are added to the memory buffer. This ensures that no data is lost in the event of a crash during a write.

 

As data accumulates across levels on the disk, LSM trees employ a merge process similar to [merge sort](./Merge_sort) to consolidate entries and maintain a consistent sorted order across levels. This process also handles updates and deletes, removing redundant or obsolete entries. Updates are treated as new writes, while deletes are marked with a tombstone entry, which is a placeholder indicating that the key has been deleted. These tombstones are later removed during the merging process.

 

Two common merging policies govern how data flows through the levels: levelling and tiering. In levelling, only one component exists per level, and merging happens more frequently, reducing the total number of components but increasing write amplification. In tiering, multiple components can coexist within a level, and merging occurs less frequently, reducing write amplification but increasing read costs because more components need to be searched.

 

This design leads to amortized write costs of     O  (    T ⋅ ⋅  L  B   )    {\displaystyle O\left({T\cdot L \over B}\right)}  ![{\displaystyle O\left({T\cdot L \over B}\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2923dfaa44860bea931c6fe390dba13065d76ab1) for leveling merge policies, where     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) is the size ratio between levels,     L   {\displaystyle L}  ![{\displaystyle L}](https://wikimedia.org/api/rest_v1/media/math/render/svg/103168b86f781fe6e9a4a87b8ea1cebe0ad4ede8) is the number of levels, and     B   {\displaystyle B}  ![{\displaystyle B}](https://wikimedia.org/api/rest_v1/media/math/render/svg/47136aad860d145f75f3eed3022df827cee94d7a) is the number of entries per page.[[8]](./Log-structured_merge-tree#cite_note-:0-8)

 

### Point lookup

 

A point lookup operation retrieves the value associated with a specific key. In LSM trees, because of the multi-level structure and the immutability of disk components, point lookups involve checking several levels to ensure the most up-to-date value for the key is returned.

 

The process begins with a search in the in-memory component (C0), which holds the latest data. Since this component is organized as a sorted structure, the search is efficient. If the key is found here, its value is returned right away.

 

If the key isn't found in memory, the search moves to the disk components, starting with the first level (C1) and continuing through deeper levels (C2, C3, etc.). Each disk level is also sorted, allowing for efficient searches using methods like [binary search](./Binary_search) or [tree search](./Tree_search). Newer levels are checked first because they contain the most recent updates and deletions for the key.

 

To make the search faster, LSM trees often use a [bloom filter](./Bloom_filter) for each on-disk component. These filters are probabilistic structures that help quickly determine whether a key is definitely absent from a component. Before accessing any disk component, the system checks the Bloom filter. If the filter indicates the key is not present, the component is skipped, saving time. If the filter suggests the key might be there, the system proceeds to search for the component.

 

The lookup operation stops as soon as the key is found, ensuring the most recent version is returned. If the search reaches the final level without finding the key, the system concludes that the key doesn't exist.

 

Point lookup complexity is     O ( L )   {\displaystyle O(L)}  ![{\displaystyle O(L)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2686f0d98bdf16092324c5519a1497c1f7a3e2fc) without Bloom filters, as each level must be searched. With Bloom filters, the cost for zero-result lookups is significantly reduced to     O  (  L ⋅ ⋅   e  − −    M N      )    {\displaystyle O\left(L\cdot e^{-{\frac {M}{N}}}\right)}  ![{\displaystyle O\left(L\cdot e^{-{\frac {M}{N}}}\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1f0c9cbfb3701e14d3e5b31b6c25f60b535759c9), where M is the total Bloom filter size and N is the number of keys. For existing key lookups, the cost is     O ( 1 )   {\displaystyle O(1)}  ![{\displaystyle O(1)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) due to the presence of Bloom filters.[[8]](./Log-structured_merge-tree#cite_note-:0-8)

 

### Range query

 

A range query retrieves all key-value pairs within a specified range. The operation involves scanning multiple components across the LSM tree's hierarchical structure and consolidating entries to ensure accurate and complete results.

 

A range query begins by searching the in-memory component (C0). Since this component is typically a sorted data structure, range queries can be done efficiently. Once the in-memory component is finished, the query proceeds to the disk components, starting from the first level (C1) and continuing to deeper levels.

 

Each disk component is also stored as a sorted structure allowing efficient range scans within individual components. To perform the range query, the system locates the starting point in each relevant component and scans sequentially until the end of the range is reached. The results from each component are then merged into a priority queue to reconcile duplicates, updates, and deletes, ensuring the final result only includes the latest version of each key.

 

For efficiency, LSM trees often divide disk components into smaller, disjoint key ranges. In this way, when processing a range query, the system can search only the partitions that have overlap ranges to reduce the number of components accessed. Similar to point lookup, Bloom filters are sometimes used to quickly decide whether a disk component contains any keys within the queried range, allowing the system to skip components that are guaranteed to be irrelevant.

 

The performance of a range query in LSM-trees depends on the query's selectivity. For short-range queries, which access fewer keys than twice the number of levels, the query must examine components across all levels, leading to a cost proportional to the number of levels. For long-range queries, which access many keys, the price is dominated by scanning the largest level, as it contains most of the data. For this reason, the runtime for short-range queries is     O ( L )   {\displaystyle O(L)}  ![{\displaystyle O(L)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2686f0d98bdf16092324c5519a1497c1f7a3e2fc) and     O  (   s B   )    {\displaystyle O\left({\frac {s}{B}}\right)}  ![{\displaystyle O\left({\frac {s}{B}}\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1da075489b3fc7469c923361b5db83379a8f53ba) for long-range queries, where     s   {\displaystyle s}  ![{\displaystyle s}](https://wikimedia.org/api/rest_v1/media/math/render/svg/01d131dfd7673938b947072a13a9744fe997e632) is the number of keys in the range.[[8]](./Log-structured_merge-tree#cite_note-:0-8)

 

## References

  
1. [↑](./Log-structured_merge-tree#cite_ref-1) Zhang, Weitao; Xu, Yinlong; Li, Yongkun; Li, Dinglong (December 2016). "Improving Write Performance of LSMT-Based Key-Value Store". *2016 IEEE 22nd International Conference on Parallel and Distributed Systems (ICPADS)*. pp. 553–560. [doi](./Doi_(identifier)):[10.1109/ICPADS.2016.0079](https://doi.org/10.1109%2FICPADS.2016.0079). [ISBN](./ISBN_(identifier)) [978-1-5090-4457-3](./Special:BookSources/978-1-5090-4457-3). [S2CID](./S2CID_(identifier)) [13611447](https://api.semanticscholar.org/CorpusID:13611447).
2. [↑](./Log-structured_merge-tree#cite_ref-2) O’Neil, Patrick; Cheng, Edward; Gawlick, Dieter; O’Neil, Elizabeth (1996-06-01). ["The log-structured merge-tree (LSM-tree)"](https://www.cs.umb.edu/~poneil/lsmtree.pdf) (PDF). *Acta Informatica*. **33** (4): 351–385. [doi](./Doi_(identifier)):[10.1007/s002360050048](https://doi.org/10.1007%2Fs002360050048). [ISSN](./ISSN_(identifier)) [1432-0525](https://search.worldcat.org/issn/1432-0525). [S2CID](./S2CID_(identifier)) [12627452](https://api.semanticscholar.org/CorpusID:12627452).
3. [↑](./Log-structured_merge-tree#cite_ref-3) Jagadish, H.V.; Narayan, P.P.S.; Seshadri, S.; Sudarshan, S.; Kanneganti, Rama (1997). ["Incremental Organization for Data Recording and Warehousing"](https://www.vldb.org/conf/1997/P016.PDF) (PDF). *Proceedings of the VLDB Conference*. VLDB Foundation: 16–25.
4. [↑](./Log-structured_merge-tree#cite_ref-4) ["Leveled Compaction in Apache Cassandra : DataStax"](https://web.archive.org/web/20140213134601/http://www.datastax.com/dev/blog/leveled-compaction-in-apache-cassandra). February 13, 2014. Archived from [the original](http://www.datastax.com/dev/blog/leveled-compaction-in-apache-cassandra) on February 13, 2014.
5. [↑](./Log-structured_merge-tree#cite_ref-5) Sears, Russell; Ramakrishnan, Raghu (2012-05-20). ["BLSM"](https://doi.org/10.1145/2213836.2213862). *Proceedings of the 2012 ACM SIGMOD International Conference on Management of Data*. SIGMOD '12. New York, NY, USA: Association for Computing Machinery. pp. 217–228. [doi](./Doi_(identifier)):[10.1145/2213836.2213862](https://doi.org/10.1145%2F2213836.2213862). [ISBN](./ISBN_(identifier)) [978-1-4503-1247-9](./Special:BookSources/978-1-4503-1247-9). [S2CID](./S2CID_(identifier)) [207194816](https://api.semanticscholar.org/CorpusID:207194816).
6. [↑](./Log-structured_merge-tree#cite_ref-6) Tan, Wei; Tata, Sandeep; Tang, Yuzhe; Fong, Liana (2014), [*Diff-Index: Differentiated Index in Distributed Log-Structured Data Stores*](https://openproceedings.org/EDBT/2014/edbticdt2014industrial_submission_17.pdf) (PDF), OpenProceedings.org, [doi](./Doi_(identifier)):[10.5441/002/edbt.2014.76](https://doi.org/10.5441%2F002%2Fedbt.2014.76), retrieved 2022-05-22
7. [↑](./Log-structured_merge-tree#cite_ref-7) Dejun Teng; Lei Guo; Rubao Lee; Feng Chen; Yanfeng Zhang; Siyuan Ma; Xiaodong Zhang (2018). *"A Low-cost Disk Solution Enabling LSM-tree to Achieve High Performance for Mixed Read/Write Workloads"*. ACM Transactions on Storage. pp. 1–26. [doi](./Doi_(identifier)):[10.1145/3162615](https://doi.org/10.1145%2F3162615).
8. [1](./Log-structured_merge-tree#cite_ref-:0_8-0) [2](./Log-structured_merge-tree#cite_ref-:0_8-1) [3](./Log-structured_merge-tree#cite_ref-:0_8-2) Luo, Chen; [Carey, Michael J.](./Michael_J._Carey_(computer_scientist)) (July 2019). "LSM-based storage techniques: a survey". *The VLDB Journal*. **29**: 393–418. [arXiv](./ArXiv_(identifier)):[1812.07527](https://arxiv.org/abs/1812.07527). [doi](./Doi_(identifier)):[10.1007/s00778-019-00555-y](https://doi.org/10.1007%2Fs00778-019-00555-y). [S2CID](./S2CID_(identifier)) [56178614](https://api.semanticscholar.org/CorpusID:56178614).

 General 
- O'Neil, Patrick E.; Cheng, Edward; Gawlick, Dieter; [O'Neil, Elizabeth](./Elizabeth_O'Neil) (June 1996). "The log-structured merge-tree (LSM-tree)". *Acta Informatica*. **33** (4): 351–385. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.44.2782](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.44.2782). [doi](./Doi_(identifier)):[10.1007/s002360050048](https://doi.org/10.1007%2Fs002360050048). [S2CID](./S2CID_(identifier)) [12627452](https://api.semanticscholar.org/CorpusID:12627452).
- Li, Yinan; He, Bingsheng; Luo, Qiong; Yi, Ke (2009). "Tree Indexing on Flash Disks". *2009 IEEE 25th International Conference on Data Engineering*. pp. 1303–6. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.144.6961](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.144.6961). [doi](./Doi_(identifier)):[10.1109/ICDE.2009.226](https://doi.org/10.1109%2FICDE.2009.226). [ISBN](./ISBN_(identifier)) [978-1-4244-3422-0](./Special:BookSources/978-1-4244-3422-0). [S2CID](./S2CID_(identifier)) [2343303](https://api.semanticscholar.org/CorpusID:2343303).

 

## External links

 
- [An Overview of Log Structured Merge Trees](http://www.benstopford.com/2015/02/14/log-structured-merge-trees)

 
| vteTree data structures |
| --- |
| Search trees(dynamic sets,associative arrays) | 2–32–3–4AA(a,b)AVLBB+K-DimensionalB*BxBinary searchOptimalSelf-balancingDancingHTreeIntervalOrder statisticPalindrome(Left-leaning)Red–blackScapegoatSplayTTreapUBWeight-balanced |
| Heaps | BinaryBinomialBrodald-aryFibonacciLeftistPairingSkew binomialSkewvan Emde BoasWeak |
| Tries | CtrieC-trie(compressed ADT)HashRadixSuffixTernary searchX-fastY-fast |
| Spatialdatapartitioning trees | BallBKBSPCartesianHilbert Rk-d(implicitk-d)MMetricMVPOctreePHPriority RQuadRR+R*SegmentVPX |
| Other trees | CoverExponentialFenwickFingerFractal indexFusionHash calendariDistanceK-aryLeft-child right-siblingLink/cutLog-structured mergeMerklePQRangeSPQRTop |