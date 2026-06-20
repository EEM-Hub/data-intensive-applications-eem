---
source: https://en.wikipedia.org/wiki/Hash_join
fetched: 2026-06-19
---

Algorithm used in relational databases 

The **hash join** is an example of a [join algorithm](./Join_(SQL)) and is used in the implementation of a [relational](./Relational_database) [database management system](./Database_management_system). All variants of hash join algorithms involve building [hash tables](./Hash_table) from the tuples of one or both of the joined relations, and subsequently probing those tables so that only tuples with the same hash code need to be compared for equality in equijoins.

 

Hash joins are typically more efficient than nested loops joins, except when the probe side of the join is very small. They require an [equijoin](./Equijoin) predicate (a [predicate](./Syntactic_predicate) comparing records from one table with those from the other table using a conjunction of equality operators '=' on one or more columns).

 

## Classic hash join

 

The classic hash join algorithm for an [inner join](./Join_(SQL)#Inner_join) of two relations proceeds as follows:

 
- First, prepare a [hash table](./Hash_table) using the contents of one relation, ideally whichever one is smaller after applying local predicates. This relation is called the build side of the join. The [hash table](./Hash_table) entries are mappings from the value of the (composite) join attribute to the remaining attributes of that row (whichever ones are needed).
- Once the [hash table](./Hash_table) is built, scan the other relation (the probe side). For each row of the probe relation, find the relevant rows from the build relation by looking in the [hash table](./Hash_table).

 

The first phase is usually called the **"build" phase**, while the second is called the **"probe" phase**. Similarly, the join relation on which the hash table is built is called the "build" input, whereas the other input is called the "probe" input.

 

This algorithm is simple, but it requires that the smaller join relation fits into memory, which is sometimes not the case. A simple approach to handling this situation proceeds as follows:

 
1. For each tuple     r   {\displaystyle r}  ![{\displaystyle r}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d1ecb613aa2984f0576f70f86650b7c2a132538) in the build input     R   {\displaystyle R}  ![{\displaystyle R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33) 
1. Add     r   {\displaystyle r}  ![{\displaystyle r}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d1ecb613aa2984f0576f70f86650b7c2a132538) to the in-memory hash table
2. If the size of the hash table equals the maximum in-memory size:

1. Scan the probe input     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2), and add matching join tuples to the output relation
2. Reset the hash table, and continue scanning the build input     R   {\displaystyle R}  ![{\displaystyle R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33)

2. Do a final scan of the probe input     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) and add the resulting join tuples to the output relation

 

This is essentially the same as the [block nested loop](./Block_nested_loop) join algorithm. This algorithm may scan     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) more times than necessary.

 

## Grace hash join

 

A better approach is known as the "grace hash join", after the GRACE database machine for which it was first implemented.

 

This algorithm avoids rescanning the entire     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) relation by first partitioning both     R   {\displaystyle R}  ![{\displaystyle R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33) and     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) via a [hash function](./Hash_function), and writing these partitions out to disk. The algorithm then loads pairs of partitions into memory, builds a hash table for the smaller partitioned relation, and probes the other relation for matches with the current hash table. Because the partitions were formed by hashing on the join key, it must be the case that any join output tuples must belong to the same partition.

 

It is possible that one or more of the partitions still does not fit into the available memory, in which case the algorithm is recursively applied: an additional orthogonal hash function is chosen to hash the large partition into sub-partitions, which are then processed as before. Since this is expensive, the algorithm tries to reduce the chance that it will occur by forming the smallest partitions possible during the initial partitioning phase.

 

## Hybrid hash join

 

The hybrid hash join algorithm[[1]](./Hash_join#cite_note-1) is a combination of the classical hash join and grace hash join. It uses minimal amount of memory for partitioning like in grace hash join and uses the remaining memory to initialize a classical hash join during partitioning phase. During the partitioning phase, the hybrid hash join uses the available memory for two purposes:

 
1. To partition both relations     R   {\displaystyle R}  ![{\displaystyle R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33) and     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) and
2. To hold an entire partition from     R   {\displaystyle R}  ![{\displaystyle R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33) in-memory, known as "partition 0"

 

Because partition 0 is never written to disk, hybrid hash join typically performs fewer I/O operations than grace hash join. When     R   {\displaystyle R}  ![{\displaystyle R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33) fits nearly fully into memory hybrid hash join has a similar behavior like the classical hash join which is more beneficial. Otherwise hybrid hash join imitates grace hash join.

 

Note that this algorithm is memory-sensitive, because there are two competing demands for memory (the hash table for partition 0, and the output buffers for the remaining partitions). Choosing too large a hash table for partition 0 might cause the algorithm to recurse because one of the non-zero partitions is too large to fit into memory.

 

## Hash anti-join

 

Hash joins can also be evaluated for an anti-join predicate (a predicate selecting values from one table when no related values are found in the other). Depending on the sizes of the tables, different algorithms can be applied:

 

### Hash left anti-join

 
- Prepare a [hash table](./Hash_table) for the **NOT IN** side of the join.
- Scan the other table, selecting any rows where the join attribute hashes to an empty entry in the hash table.

 

This is more efficient when the **NOT IN** table is smaller than the **FROM** table.

 

### Hash right anti-join

 
- Prepare a hash table for the **FROM** side of the join.
- Scan the **NOT IN** table, removing the corresponding records from the hash table on each hash hit.
- Return everything that left in the hash table.

 

This is more efficient when the **NOT IN** table is larger than the **FROM** table.

 

## Hash semi-join

 

Hash semi-join is used to return the records found in the other table. Unlike the plain join, it returns each matching record from the leading table only once, regardless of how many matches there are in the **IN** table.

 

As with the anti-join, semi-join can also be left and right:

 

### Hash left semi-join

 
- Prepare a hash table for the **IN** side of the join.
- Scan the other table, returning any rows that produce a hash hit.

 

The records are returned right after they produced a hit. The actual records from the hash table are ignored.

 

This is more efficient when the **IN** table is smaller than the **FROM** table.

 

### Hash right semi-join

 
- Prepare a hash table for the **FROM** side of the join.
- Scan the **IN** table, returning the corresponding records from the hash table and removing them.

 

With this algorithm, each record from the hash table (that is, **FROM** table) can only be returned once, since it is removed after being returned.

 

This is more efficient when the **IN** table is larger than the **FROM** table.

 

## See also

 
- [Symmetric hash join](./Symmetric_hash_join)
- [Nested loop join](./Nested_loop_join)
- [Sort-merge join](./Sort-merge_join)

 

## References

 
1. [↑](./Hash_join#cite_ref-1) DeWitt, D.J.; Katz, R.; Olken, F.; Shapiro, L.; Stonebraker, M.; Wood, D. (June 1984). "Implementation techniques for main memory database systems". *Proc. ACM SIGMOD Conf*. **14** (4): 1–8. [doi](./Doi_(identifier)):[10.1145/971697.602261](https://doi.org/10.1145%2F971697.602261).

 

## External links

 
- Hansjörg Zeller; [Jim Gray](./Jim_Gray_(computer_scientist)) (1990). ["An Adaptive Hash Join Algorithm for Multiuser Environments"](https://web.archive.org/web/20120311211953/http://www.vldb.org/conf/1990/P186.PDF) (PDF). *Proceedings of the 16th VLDB conference*. Brisbane: 186–197. Archived from [the original](http://www.vldb.org/conf/1990/P186.PDF) (PDF) on 2012-03-11. Retrieved 2008-09-21.