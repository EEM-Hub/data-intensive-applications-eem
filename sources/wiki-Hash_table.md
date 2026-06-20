---
source: https://en.wikipedia.org/wiki/Hash_table
fetched: 2026-06-19
---

Associative array for storing key–value pairs Not to be confused with [Hash list](./Hash_list) or [Hash tree](./Hash_tree_(disambiguation)). "Rehash" redirects here. For the *South Park* episode, see [Rehash (South Park)](./Rehash_(South_Park)). 

 THE UNDERSCORE "_" IS SIGNIFICANT, DO NOT CHANGE IT TO SPACE 
| Hash table |
| --- |
| Type | Unorderedassociative array |
| Invented | 1953 |
| Time complexityinbig O notationOperationAverageWorst caseSearchΘ(1)O(n)[a]InsertΘ(1)O(n)DeleteΘ(1)O(n)Space complexitySpaceΘ(n)[2]O(n) | Time complexityinbig O notation | Operation | Average | Worst case | Search | Θ(1) | O(n)[a] | Insert | Θ(1) | O(n) | Delete | Θ(1) | O(n) | Space complexity | Space | Θ(n)[2] | O(n) |
| Time complexityinbig O notation |
| Operation | Average | Worst case |
| Search | Θ(1) | O(n)[a] |
| Insert | Θ(1) | O(n) |
| Delete | Θ(1) | O(n) |
| Space complexity |
| Space | Θ(n)[2] | O(n) |

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/7/7d/Hash_table_3_1_1_0_1_0_0_SP.svg/330px-Hash_table_3_1_1_0_1_0_0_SP.svg.png)](./File:Hash_table_3_1_1_0_1_0_0_SP.svg)A small phone book as a hash table 

In [computer science](./Computer_science), a **hash table** is a [data structure](./Data_structure) that implements an [associative array](./Associative_array), also called a **dictionary** or simply **map**; an associative array is an [abstract data type](./Abstract_data_type) that maps [keys](./Unique_key) to [values](./Value_(computer_science)).[[3]](./Hash_table#cite_note-ms-4) A hash table uses a [hash function](./Hash_function) to compute an *index*, also called a *hash code*, into an array of *buckets* or *slots*, from which the desired value can be found. During lookup, the key is hashed and the resulting hash indicates where the corresponding value is stored. A map implemented by a hash table is called a **hash map**.

 

Most hash table designs employ an [imperfect hash function](./Perfect_hash_function). [Hash collisions](./Hash_collision), where the hash function generates the same index for more than one key, therefore typically must be accommodated in some way. Common strategies to handle hash collisions include chaining, which stores multiple elements in the same slot using linked lists, and open addressing, which searches for the next available slot according to a probing sequence.[[4]](./Hash_table#cite_note-knuth-5)

 

In a well-dimensioned hash table, the average time complexity for each lookup is independent of the number of elements stored in the table. Many hash table designs also allow arbitrary insertions and deletions of [key–value pairs](./Name–value_pair), at [amortized](./Amortized_analysis) constant average cost per operation.[[5]](./Hash_table#cite_note-leiser-6)[[4]](./Hash_table#cite_note-knuth-5): 513–558 [[6]](./Hash_table#cite_note-cormen-7)

 

Hashing is an example of a [space–time tradeoff](./Space–time_tradeoff). If [memory](./Computer_memory) is infinite, the entire key can be used directly as an index to locate its value with a single memory access. On the other hand, if infinite time is available, values can be stored without regard for their keys, and a [binary search](./Binary_search) or [linear search](./Linear_search) can be used to retrieve the element.[[7]](./Hash_table#cite_note-algo1rob-8): 458 

 

In many situations, hash tables turn out to be on average more efficient than [search trees](./Search_tree) or any other [table](./Table_(computing)) lookup structure. For this reason, they are widely used in many kinds of computer [software](./Software), particularly for [associative arrays](./Associative_array), [database indexing](./Database_index), [caches](./Cache_(computing)), and [sets](./Set_(abstract_data_type)).[[8]](./Hash_table#cite_note-9) Many programming languages provide built-in hash table structures, such as [Python’s dictionaries](https://docs.python.org/3/tutorial/datastructures.html#dictionaries), [Java’s HashMap](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/util/HashMap.html), [C++’s unordered_map](https://en.cppreference.com/w/cpp/container/unordered_map.html), [Go maps](https://go.dev/blog/maps), which abstract the complexity of hashing from the programmer.[[9]](./Hash_table#cite_note-10)

 

## History

 

The idea of hashing arose independently in different places. In January 1953, [Hans Peter Luhn](./Hans_Peter_Luhn) wrote an internal [IBM](./IBM) memorandum that used hashing with chaining.  The first example of [open addressing](./Open_addressing) was proposed by A. D. Linh, building on Luhn's memorandum.[[4]](./Hash_table#cite_note-knuth-5): 547  Around the same time, [Gene Amdahl](./Gene_Amdahl), [Elaine M. McGraw](./Elaine_M._McGraw), [Nathaniel Rochester](./Nathaniel_Rochester_(computer_scientist)), and [Arthur Samuel](./Arthur_Samuel_(computer_scientist)) of [IBM Research](./IBM_Research) implemented hashing for the [IBM 701](./IBM_701) [assembler](./Assembly_language#Assembler).[[10]](./Hash_table#cite_note-Konheim-11): 124  Open addressing with linear probing is credited to Amdahl, although [Andrey Ershov](./Andrey_Ershov) independently had the same idea.[[10]](./Hash_table#cite_note-Konheim-11): 124–125  The term "open addressing" was coined by [W. Wesley Peterson](./W._Wesley_Peterson) in his article which discusses the problem of search in large files.[[11]](./Hash_table#cite_note-hashhist-12): 15 

 

The first published work on hashing with chaining is credited to [Arnold Dumey](./Arnold_Dumey), who discussed the idea of using remainder modulo a prime as a hash function.[[11]](./Hash_table#cite_note-hashhist-12): 15  The word "hashing" was first published in an article by Robert Morris.[[10]](./Hash_table#cite_note-Konheim-11): 126  A [theoretical analysis](./Analysis_of_algorithms) of linear probing was submitted originally by Konheim and Weiss.[[11]](./Hash_table#cite_note-hashhist-12): 15 

 

## Overview

 

An [associative array](./Associative_array) stores a [set](./Set_(abstract_data_type)) of (key, value) pairs and allows insertion, deletion, and lookup (search), with the constraint of [unique keys](./Unique_key). In the hash table implementation of associative arrays, an array     A   {\displaystyle A}  ![{\displaystyle A}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7daff47fa58cdfd29dc333def748ff5fa4c923e3) of length     m   {\displaystyle m}  ![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc) is partially filled with     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) elements, where     m ≥ ≥  n   {\displaystyle m\geq n}  ![{\displaystyle m\geq n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6b02f25e62da7fe3162ac80446437cdc1c0fd341). A key **    x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4)** is hashed using a hash function     h   {\displaystyle h}  ![{\displaystyle h}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b26be3e694314bc90c3215047e4a2010c6ee184a) to compute an index location     A [ h ( x ) ]   {\displaystyle A[h(x)]}  ![{\displaystyle A[h(x)]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac75d530b12267b829df7cff8b2ff01a24e61ab0) in the hash table, where     h ( x ) < m   {\displaystyle h(x)<m}  ![{\displaystyle h(x)<m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/809d7e044109ace3c1f807ba0679bb18c627d513). The efficiency of a hash table depends on the load factor, defined as the ratio of the number of stored elements to the number of available slots, with lower load factors generally yielding faster operations.[[12]](./Hash_table#cite_note-13) At this index, both the key and its associated value are stored. Storing the key alongside the value ensures that lookups can verify the key at the index to retrieve the correct value, even in the presence of collisions. Under reasonable assumptions, hash tables have better [time complexity](./Time_complexity) bounds on search, delete, and insert operations in comparison to [self-balancing binary search trees](./Self-balancing_binary_search_tree).[[11]](./Hash_table#cite_note-hashhist-12): 1 

 

Hash tables are also commonly used to implement sets, by omitting the stored value for each key and merely tracking whether the key is present.[[11]](./Hash_table#cite_note-hashhist-12): 1 

 

### Load factor

 

A *load factor*     α α    {\displaystyle \alpha }  ![{\displaystyle \alpha }](https://wikimedia.org/api/rest_v1/media/math/render/svg/b79333175c8b3f0840bfb4ec41b8072c83ea88d3) is a critical statistic of a hash table, and is defined as follows:[[2]](./Hash_table#cite_note-Cormen_et_al-3)      load factor    ( α α  ) =   n m   ,   {\displaystyle {\text{load factor}}\ (\alpha )={\frac {n}{m}},}  ![{\displaystyle {\text{load factor}}\ (\alpha )={\frac {n}{m}},}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e3487807884a0c0748869a904c450c6c340f3533)
where

 
-     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) is the number of entries occupied in the hash table.
-     m   {\displaystyle m}  ![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc) is the number of buckets.

 

The performance of the hash table deteriorates in relation to the load factor     α α    {\displaystyle \alpha }  ![{\displaystyle \alpha }](https://wikimedia.org/api/rest_v1/media/math/render/svg/b79333175c8b3f0840bfb4ec41b8072c83ea88d3).[[11]](./Hash_table#cite_note-hashhist-12): 2   In the limit of large     m   {\displaystyle m}  ![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc) and     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b), each bucket statistically has a [Poisson distribution](./Poisson_distribution) with expectation     λ λ  = α α    {\displaystyle \lambda =\alpha }  ![{\displaystyle \lambda =\alpha }](https://wikimedia.org/api/rest_v1/media/math/render/svg/11bf25d8384a389167f48c90e2565cf3c34b80dc) for an ideally random [hash function](./Hash_function).

 

The software typically ensures that the load factor     α α    {\displaystyle \alpha }  ![{\displaystyle \alpha }](https://wikimedia.org/api/rest_v1/media/math/render/svg/b79333175c8b3f0840bfb4ec41b8072c83ea88d3) remains below a certain constant,      α α   max     {\displaystyle \alpha _{\max }}  ![{\displaystyle \alpha _{\max }}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9b0b1e00f2745ac1316702c4aae560ae371cb564). This helps maintain good performance. Therefore, a common approach is to resize or "rehash" the hash table whenever the load factor     α α    {\displaystyle \alpha }  ![{\displaystyle \alpha }](https://wikimedia.org/api/rest_v1/media/math/render/svg/b79333175c8b3f0840bfb4ec41b8072c83ea88d3) reaches      α α   max     {\displaystyle \alpha _{\max }}  ![{\displaystyle \alpha _{\max }}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9b0b1e00f2745ac1316702c4aae560ae371cb564). Similarly the table may also be resized if the load factor drops below      α α   max    /  4   {\displaystyle \alpha _{\max }/4}  ![{\displaystyle \alpha _{\max }/4}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7e9dc23339801e7b502e6f862302bb55e0516bd4).[[13]](./Hash_table#cite_note-cornell08-14)

 

#### Load factor for separate chaining

 

With separate chaining hash tables, each slot of the bucket array stores a pointer to a list or array of data.[[14]](./Hash_table#cite_note-plank-15)

 

Separate chaining hash tables suffer gradually declining performance as the load factor grows, and no fixed point beyond which resizing is absolutely needed.[[13]](./Hash_table#cite_note-cornell08-14)

 

With separate chaining, the value of      α α   max     {\displaystyle \alpha _{\max }}  ![{\displaystyle \alpha _{\max }}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9b0b1e00f2745ac1316702c4aae560ae371cb564) that gives best performance is typically between 1 and 3.[[13]](./Hash_table#cite_note-cornell08-14)

 

#### Load factor for open addressing

 

With open addressing, each slot of the bucket array holds exactly one item. Therefore an open-addressed hash table cannot have a load factor greater than 1.[[14]](./Hash_table#cite_note-plank-15)

 

The performance of open addressing becomes very bad when the load factor approaches 1.[[13]](./Hash_table#cite_note-cornell08-14)

 

Therefore a hash table that uses open addressing *must* be resized or *rehashed* if the load factor     α α    {\displaystyle \alpha }  ![{\displaystyle \alpha }](https://wikimedia.org/api/rest_v1/media/math/render/svg/b79333175c8b3f0840bfb4ec41b8072c83ea88d3) approaches 1.[[13]](./Hash_table#cite_note-cornell08-14)

 

With open addressing, acceptable figures of max load factor      α α   max     {\displaystyle \alpha _{\max }}  ![{\displaystyle \alpha _{\max }}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9b0b1e00f2745ac1316702c4aae560ae371cb564) should range around 0.6 to 0.75.[[15]](./Hash_table#cite_note-16)[[16]](./Hash_table#cite_note-owo03-17): 110 

 

## Hash function

 

A [hash function](./Hash_function)     h : U → →  { 0 , . . . , m − −  1 }   {\displaystyle h:U\rightarrow \{0,...,m-1\}}  ![{\displaystyle h:U\rightarrow \{0,...,m-1\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4a0ce358cd0b459bddf9c03c5effe6afc700185b) maps the universe     U   {\displaystyle U}  ![{\displaystyle U}](https://wikimedia.org/api/rest_v1/media/math/render/svg/458a728f53b9a0274f059cd695e067c430956025) of keys to indices or slots within the table, that is,     h ( x ) ∈ ∈  { 0 , . . . , m − −  1 }   {\displaystyle h(x)\in \{0,...,m-1\}}  ![{\displaystyle h(x)\in \{0,...,m-1\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bca89b54d7d94d29a9785be3b88bf3124387c8b7) for     x ∈ ∈  U   {\displaystyle x\in U}  ![{\displaystyle x\in U}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c32ddcb2941216f2980b950ce969dc15cba26906). The conventional implementations of hash functions are based on the *integer universe assumption* that all elements of the table stem from the universe     U = { 0 , . . . , u − −  1 }   {\displaystyle U=\{0,...,u-1\}}  ![{\displaystyle U=\{0,...,u-1\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/04ab3270bbe2fbecf3426b15516ced184a01311b), where the [bit length](./Bit_length) of     u   {\displaystyle u}  ![{\displaystyle u}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3e6bb763d22c20916ed4f0bb6bd49d7470cffd8) is confined within the [word size](./Word_(computer_architecture)) of a [computer architecture](./Computer_architecture).[[11]](./Hash_table#cite_note-hashhist-12): 2 

 

A hash function     h   {\displaystyle h}  ![{\displaystyle h}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b26be3e694314bc90c3215047e4a2010c6ee184a) is said to be [perfect](./Perfect_hash_function) for a given set     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) if it is [injective](./Injective_function) on     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2), that is, if each element     x ∈ ∈  S   {\displaystyle x\in S}  ![{\displaystyle x\in S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/51186ba8afb2067573a9082d55dd383df1ea9214) maps to a different value in      0 , . . . , m − −  1    {\displaystyle {0,...,m-1}}  ![{\displaystyle {0,...,m-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5b007ad843a070921d2e670c0431ba02f649f16b).[[17]](./Hash_table#cite_note-Yi06-18)[[18]](./Hash_table#cite_note-CHD-19) A perfect hash function can be created if all the keys are known ahead of time.[[17]](./Hash_table#cite_note-Yi06-18)

 

### Integer universe assumption

 

The schemes of hashing used in *integer universe assumption* include hashing by division, hashing by multiplication, [universal hashing](./Universal_hashing), [dynamic perfect hashing](./Dynamic_perfect_hashing), and [static perfect hashing](./Static_Hashing).[[11]](./Hash_table#cite_note-hashhist-12): 2  However, hashing by division is the commonly used scheme.[[19]](./Hash_table#cite_note-cormenalgo01-20): 264 [[16]](./Hash_table#cite_note-owo03-17): 110 

 

#### Hashing by division

 

The scheme in hashing by division is as follows:[[11]](./Hash_table#cite_note-hashhist-12): 2      h ( x )   =   x   mod     m ,   {\displaystyle h(x)\ =\ x\,{\bmod {\,}}m,}  ![{\displaystyle h(x)\ =\ x\,{\bmod {\,}}m,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c22155e49d56ce69ff1b49f37d9f139cd6da7ac6)
where     h ( x )   {\displaystyle h(x)}  ![{\displaystyle h(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/02c07825dae28705df03d15daeb8844d49c4dbd4) is the hash value of     x ∈ ∈  S   {\displaystyle x\in S}  ![{\displaystyle x\in S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/51186ba8afb2067573a9082d55dd383df1ea9214) and     m   {\displaystyle m}  ![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc) is the size of the table.

 

#### Hashing by multiplication

 

The scheme in hashing by multiplication is as follows:[[11]](./Hash_table#cite_note-hashhist-12): 2–3      h ( x ) = ⌊ ⌊  m   (   ( x A )  mod  1     )   ⌋ ⌋    {\displaystyle h(x)=\lfloor m{\bigl (}(xA){\bmod {1}}{\bigr )}\rfloor }  ![{\displaystyle h(x)=\lfloor m{\bigl (}(xA){\bmod {1}}{\bigr )}\rfloor }](https://wikimedia.org/api/rest_v1/media/math/render/svg/cdd58ba648176ddb2a7a3fdabae1d2fc40018dba)
Where     A   {\displaystyle A}  ![{\displaystyle A}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7daff47fa58cdfd29dc333def748ff5fa4c923e3) is a non-integer [real-valued constant](./Real_number) and     m   {\displaystyle m}  ![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc) is the size of the table. An advantage of the hashing by multiplication is that the     m   {\displaystyle m}  ![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc) is not critical.[[11]](./Hash_table#cite_note-hashhist-12): 2–3  Although any value     A   {\displaystyle A}  ![{\displaystyle A}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7daff47fa58cdfd29dc333def748ff5fa4c923e3) produces a hash function, [Donald Knuth](./Donald_Knuth) suggests using the [golden ratio](./Golden_ratio).[[11]](./Hash_table#cite_note-hashhist-12): 3 

 

#### String hashing

 

Commonly a string is used as a key to the hash function. The third edition of *[The C++ Programming Language](./The_C++_Programming_Language)* describes a simple hash function in which an unsigned integer that is initially zero is repeatedly left shifted one bit and then xor'ed with the integer value of the next character.  This hash value is then taken modulo the table size.[[20]](./Hash_table#cite_note-21) If the left shift is not circular, then the string length should be at least eight bits less than the size of the unsigned integer in bits.  Another common way to hash a string to an integer is with a [ polynomial rolling hash function](./Rolling_hash).

 

### Choosing a hash function

 

[Uniform distribution](./Uniform_distribution_(discrete)) of the hash values is a fundamental requirement of a hash function. A non-uniform distribution increases the number of collisions and the cost of resolving them. Uniformity is sometimes difficult to ensure by design, but may be evaluated empirically using statistical tests, e.g., a [Pearson's chi-squared test](./Pearson's_chi-squared_test#Discrete_uniform_distribution) for discrete uniform distributions.[[21]](./Hash_table#cite_note-chernoff-22)[[22]](./Hash_table#cite_note-plackett-23)

 

The distribution needs to be uniform only for table sizes that occur in the application. In particular, if one uses dynamic resizing with exact doubling and halving of the table size, then the hash function needs to be uniform only when the size is a [power of two](./Power_of_two). Here the index can be computed as some range of bits of the hash function. On the other hand, some hashing algorithms prefer to have the size be a [prime number](./Prime_number).[[23]](./Hash_table#cite_note-:0-24)

 

For [open addressing](./Open_addressing) schemes, the hash function should also avoid *[runs](./Primary_clustering)*, the mapping of two or more keys to consecutive slots. Such runs may cause the lookup cost to skyrocket, even if the load factor is low and collisions are infrequent. The popular multiplicative hash is claimed to have particularly poor run behavior.[[23]](./Hash_table#cite_note-:0-24)[[4]](./Hash_table#cite_note-knuth-5)

 

[K-independent hashing](./K-independent_hashing) offers a way to prove a certain hash function does not have bad keysets for a given type of hashtable. A number of K-independence results are known for collision resolution schemes such as linear probing and cuckoo hashing. Since K-independence can prove a hash function works, one can then focus on finding the fastest possible such hash function.[[24]](./Hash_table#cite_note-25)

 

## Collision resolution

 See also: [2-choice hashing](./2-choice_hashing) 

A search algorithm that uses hashing consists of two parts. The first part is computing a [hash function](./Hash_function) which transforms the search key into an [array index](./Array_index). The ideal case is such that no two search keys hash to the same array index. However, this is not always the case and impossible to guarantee for unseen given data.[[4]](./Hash_table#cite_note-knuth-5): 515  Hence the second part of the algorithm is collision resolution. The two common methods for collision resolution are separate chaining and open addressing.[[7]](./Hash_table#cite_note-algo1rob-8): 458 

 

### Separate chaining

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Hash_table_5_0_1_1_1_1_1_LL.svg/500px-Hash_table_5_0_1_1_1_1_1_LL.svg.png)](./File:Hash_table_5_0_1_1_1_1_1_LL.svg)Hash collision resolved by separate chaining [![](//upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Hash_table_5_0_1_1_1_1_0_LL.svg/500px-Hash_table_5_0_1_1_1_1_0_LL.svg.png)](./File:Hash_table_5_0_1_1_1_1_0_LL.svg)Hash collision by separate chaining with head records in the bucket array 

In separate chaining, the process involves building a [linked list](./Linked_list) with [key–value pair](./Key–value_pair) for each search array index. The collided items are chained together through a single linked list, which can be traversed to access the item with a unique search key.[[7]](./Hash_table#cite_note-algo1rob-8): 464  Collision resolution through chaining with linked list is a common method of implementation of hash tables. Let     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) and     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) be the hash table and the node respectively, the operation involves as follows:[[19]](./Hash_table#cite_note-cormenalgo01-20): 258 

  the lines with only a space are significant. don't remove the lines or the spaces  
```
Chained-Hash-Insert(T, k)
  insert x at the head of linked list T[h(k)]

Chained-Hash-Search(T, k)
  search for an element with key k in linked list T[h(k)]

Chained-Hash-Delete(T, k)
  delete x from the linked list T[h(k)]
```
 

If the element is comparable either [numerically](./Sequence#Analysis) or [lexically](./Lexicographic_order), and inserted into the list by maintaining the [total order](./Total_order), it results in faster termination of the unsuccessful searches.[[4]](./Hash_table#cite_note-knuth-5): 520–521 

 

#### Other data structures for separate chaining

 

If the keys are [ordered](./Total_order), it could be efficient to use "[self-organizing](./Optimal_binary_search_tree)" concepts such as using a [self-balancing binary search tree](./Self-balancing_binary_search_tree), through which the [theoretical worst case](./Worst-case_complexity) could be brought down to     O ( log ⁡ ⁡   n  )   {\displaystyle O(\log {n})}  ![{\displaystyle O(\log {n})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/653ab6d6fd99537d220f179d2591955ff4f37b99), although it introduces additional complexities.[[4]](./Hash_table#cite_note-knuth-5): 521 

 

In [dynamic perfect hashing](./Dynamic_perfect_hashing), two-level hash tables are used to reduce the look-up complexity to be a guaranteed     O ( 1 )   {\displaystyle O(1)}  ![{\displaystyle O(1)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) in the worst case. In this technique, the buckets of     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40) entries are organized as [perfect hash tables](./Perfect_hash_function) with      k  2     {\displaystyle k^{2}}  ![{\displaystyle k^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/af6423cd00e3559de92c4bc497066ff1b12bbfc3) slots providing constant worst-case lookup time, and low amortized time for insertion.[[25]](./Hash_table#cite_note-26) A study shows array-based separate chaining to be 97% more performant when compared to the standard linked list method under heavy load.[[26]](./Hash_table#cite_note-nick05-27): 99 

 

Techniques such as using [fusion tree](./Fusion_tree) for each buckets also result in constant time for all operations with high probability.[[27]](./Hash_table#cite_note-28)

 

#### Caching and locality of reference

 

The linked list of separate chaining implementation may not be [cache-conscious](./Cache-oblivious_algorithm) due to [spatial locality](./Spatial_locality)—[locality of reference](./Locality_of_reference)—when the nodes of the linked list are scattered across memory, thus the list traversal during insert and search may entail [CPU cache](./CPU_cache) inefficiencies.[[26]](./Hash_table#cite_note-nick05-27): 91 

 

In [cache-conscious variants](./Cache-oblivious_algorithm) of collision resolution through separate chaining, a [dynamic array](./Dynamic_array) found to be more [cache-friendly](./CPU_cache) is used in the place where a linked list or self-balancing binary search trees is usually deployed, since the [contiguous allocation](./Memory_management_(operating_systems)#Single_contiguous_allocation) pattern of  the array could be exploited by [hardware-cache prefetchers](./Cache_prefetching)—such as [translation lookaside buffer](./Translation_lookaside_buffer)—resulting in reduced access time and memory consumption.[[28]](./Hash_table#cite_note-29)[[29]](./Hash_table#cite_note-30)[[30]](./Hash_table#cite_note-31)

 

### Open addressing

 Main article: [Open addressing](./Open_addressing) [![](//upload.wikimedia.org/wikipedia/commons/thumb/b/bf/Hash_table_5_0_1_1_1_1_0_SP.svg/500px-Hash_table_5_0_1_1_1_1_0_SP.svg.png)](./File:Hash_table_5_0_1_1_1_1_0_SP.svg)Hash collision resolved by open addressing with linear probing (interval=1). Note that "Ted Baker" has a unique hash, but nevertheless collided with "Sandra Dee", that had previously collided with "John Smith". 

[Open addressing](./Open_addressing) is another collision resolution technique in which every entry record is stored in the bucket array itself, and the hash resolution is performed through **probing**. When a new entry has to be inserted, the buckets are examined, starting with the hashed-to slot and proceeding in some *probe sequence*, until an unoccupied slot is found. When searching for an entry, the buckets are scanned in the same sequence,  until either the target record is found, or an unused array slot is found, which indicates an unsuccessful search.[[31]](./Hash_table#cite_note-tenenbaum90-32)

 

Well-known probe sequences include:

 
- [Linear probing](./Linear_probing), in which the interval between probes is fixed (usually 1).[[32]](./Hash_table#cite_note-Cuckoo-33)
- [Quadratic probing](./Quadratic_probing), in which the interval between probes is increased by adding the successive outputs of a quadratic polynomial to the value given by the original hash computation.[[33]](./Hash_table#cite_note-clrs-34): 272 
- [Double hashing](./Double_hashing), in which the interval between probes is computed by a secondary hash function.[[33]](./Hash_table#cite_note-clrs-34): 272–273 

 

The performance of open addressing may be slower compared to separate chaining since the probe sequence increases when the load factor     α α    {\displaystyle \alpha }  ![{\displaystyle \alpha }](https://wikimedia.org/api/rest_v1/media/math/render/svg/b79333175c8b3f0840bfb4ec41b8072c83ea88d3) approaches 1.[[13]](./Hash_table#cite_note-cornell08-14)[[26]](./Hash_table#cite_note-nick05-27): 93  The probing results in an [infinite loop](./Infinite_loop) if the load factor reaches 1, in the case of a completely filled table.[[7]](./Hash_table#cite_note-algo1rob-8): 471  The [average cost](./Average-case_complexity) of linear probing depends on the hash function's ability to [distribute](./Probability_distribution) the elements [uniformly](./Continuous_uniform_distribution) throughout the table to avoid [runs](./Primary_clustering), since formation of runs would result in increased search time.[[7]](./Hash_table#cite_note-algo1rob-8): 472 

 

#### Caching and locality of reference

 

Since the slots are located in successive locations, linear probing could lead to better utilization of [CPU cache](./CPU_cache) due to [locality of references](./Locality_of_reference) resulting in reduced [memory latency](./Memory_latency).[[32]](./Hash_table#cite_note-Cuckoo-33)

 

#### Other collision resolution techniques based on open addressing

 

##### Coalesced hashing

 Main article: [Coalesced hashing](./Coalesced_hashing) 

[Coalesced hashing](./Coalesced_hashing) is a hybrid of both separate chaining and open addressing in which the buckets or nodes link within the table.[[34]](./Hash_table#cite_note-chen87-35): 6–8  The algorithm is ideally suited for [fixed memory allocation](./Memory_pool).[[34]](./Hash_table#cite_note-chen87-35): 4  The collision in coalesced hashing is resolved by identifying the largest-indexed empty slot on the hash table, then the colliding value is inserted into that slot. The bucket is also linked to the inserted node's slot which contains its colliding hash address.[[34]](./Hash_table#cite_note-chen87-35): 8 

 

##### Cuckoo hashing

 Main article: [Cuckoo hashing](./Cuckoo_hashing) 

[Cuckoo hashing](./Cuckoo_hashing) is a form of open addressing collision resolution technique which guarantees     O ( 1 )   {\displaystyle O(1)}  ![{\displaystyle O(1)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) worst-case lookup complexity and constant amortized time for insertions. The collision is resolved through maintaining two hash tables, each having its own hashing function, and collided slot gets replaced with the given item, and the preoccupied element of the slot gets displaced into the other hash table. The process continues until every key has its own spot in the empty buckets of the tables; if the procedure enters into [infinite loop](./Infinite_loop)—which is identified through maintaining a threshold loop counter—both hash tables get rehashed with newer hash functions and the procedure continues.[[35]](./Hash_table#cite_note-36): 124–125 

 

##### Hopscotch hashing

 Main article: [Hopscotch hashing](./Hopscotch_hashing) 

[Hopscotch hashing](./Hopscotch_hashing) is an open addressing based algorithm which combines the elements of [cuckoo hashing](./Cuckoo_hashing), [linear probing](./Linear_probing) and chaining through the notion of a *neighbourhood* of buckets—the subsequent buckets around any given occupied bucket, also called a "virtual" bucket.[[36]](./Hash_table#cite_note-nir08-37): 351–352  The algorithm is designed to deliver better performance when the load factor of the hash table grows beyond 90%; it also provides high throughput in [concurrent settings](./Concurrent_computing), thus well suited for implementing resizable [concurrent hash table](./Concurrent_hash_table).[[36]](./Hash_table#cite_note-nir08-37): 350  The neighbourhood characteristic of hopscotch hashing guarantees a property that, the cost of finding the desired item from any given buckets within the neighbourhood is very close to the cost of finding it in the bucket itself; the algorithm attempts to be an item into its neighbourhood—with a possible cost involved in displacing other items.[[36]](./Hash_table#cite_note-nir08-37): 352 

 

Each bucket within the hash table includes an additional "hop-information"—an *H*-bit [bit array](./Bit_array) for indicating the [relative distance](./Euclidean_distance#One_dimension) of the item which was originally hashed into the current virtual bucket within *H* − 1 entries.[[36]](./Hash_table#cite_note-nir08-37): 352  Let     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40) and     B k   {\displaystyle Bk}  ![{\displaystyle Bk}](https://wikimedia.org/api/rest_v1/media/math/render/svg/82832ae60c54ab770e4d55783e2b14fff85798f3) be the key to be inserted and bucket to which the key is hashed into respectively; several cases are involved in the insertion procedure such that the neighbourhood property of the algorithm is vowed:[[36]](./Hash_table#cite_note-nir08-37): 352–353  if     B k   {\displaystyle Bk}  ![{\displaystyle Bk}](https://wikimedia.org/api/rest_v1/media/math/render/svg/82832ae60c54ab770e4d55783e2b14fff85798f3) is empty, the element is inserted, and the leftmost bit of bitmap is [set](./Bitwise_operation) to 1; if not empty, linear probing is used for finding an empty slot in the table, the bitmap of the bucket gets updated followed by the insertion; if the empty slot is not within the range of the *neighbourhood,* i.e. *H* − 1, subsequent swap and hop-info bit array manipulation of each bucket is performed in accordance with its neighbourhood [invariant properties](./Invariant_(mathematics)).[[36]](./Hash_table#cite_note-nir08-37): 353 

 

##### Robin Hood hashing

 

Robin Hood hashing is an open addressing based collision resolution algorithm; the collisions are resolved through favouring the displacement of the element that is farthest—or longest *probe sequence length* (PSL)—from its "home location" i.e. the bucket to which the item was hashed into.[[37]](./Hash_table#cite_note-waterloo86-38): 12  It is named after [Robin Hood](./Robin_Hood), a mythical [heroic outlaw](./Heroic_outlaw) who stole from the rich to give to the poor.

 

Although Robin Hood hashing does not change the [theoretical search cost](./Computational_complexity_theory), it significantly affects the [variance](./Variance) of the [distribution](./Probability_distribution) of the items on the buckets,[[38]](./Hash_table#cite_note-39): 2  i.e. dealing with [long run](./Primary_clustering) formation in the hash table.[[39]](./Hash_table#cite_note-cornell14-40) Each node within the hash table that uses Robin Hood hashing should be augmented to store an extra PSL value.[[40]](./Hash_table#cite_note-41) Let     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) be the key to be inserted,     x  .   psl    {\displaystyle x{.}{\text{psl}}}  ![{\displaystyle x{.}{\text{psl}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/affd26ef719d0b0e69fe0778fd5447283a895b8b) be the (incremental) PSL length of     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4),     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) be the hash table and     j   {\displaystyle j}  ![{\displaystyle j}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2f461e54f5c093e92a55547b9764291390f0b5d0) be the index, the insertion procedure is as follows:[[37]](./Hash_table#cite_note-waterloo86-38): 12–13 [[41]](./Hash_table#cite_note-indiana88-42): 5 

 
- If     x  .   psl    ≤ ≤    T [ j ]  .   psl    {\displaystyle x{.}{\text{psl}}\ \leq \ T[j]{.}{\text{psl}}}  ![{\displaystyle x{.}{\text{psl}}\ \leq \ T[j]{.}{\text{psl}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/12d235230accf383c8f51fb38521cf936491f57e): the iteration goes into the next bucket without attempting an external probe.
- If     x  .   psl    >   T [ j ]  .   psl    {\displaystyle x{.}{\text{psl}}\ >\ T[j]{.}{\text{psl}}}  ![{\displaystyle x{.}{\text{psl}}\ >\ T[j]{.}{\text{psl}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8b4cd954c87e2db3bc9d3e8871d603177ebc79cc): insert the item     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) into the bucket     j   {\displaystyle j}  ![{\displaystyle j}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2f461e54f5c093e92a55547b9764291390f0b5d0); swap     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) with     T [ j ]   {\displaystyle T[j]}  ![{\displaystyle T[j]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cb1f9ca1ed801caf88d5004aa3685644667099b6)—let it be      x ′    {\displaystyle x'}  ![{\displaystyle x'}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0ac74959896052e160a5953102e4bc3850fe93b2); continue the probe from the     ( j + 1 )   {\displaystyle (j+1)}  ![{\displaystyle (j+1)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4244360b0b6aea8d3b1cfb3ab63b52fcc4be0152)th bucket to insert      x ′    {\displaystyle x'}  ![{\displaystyle x'}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0ac74959896052e160a5953102e4bc3850fe93b2); repeat the procedure until every element is inserted.

 

## Dynamic resizing

 

Repeated insertions cause the number of entries in a hash table to grow, which consequently increases the load factor; to maintain the amortized     O ( 1 )   {\displaystyle O(1)}  ![{\displaystyle O(1)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) performance of the lookup and insertion operations, a hash table is dynamically resized and the items of the tables are *rehashed* into the buckets of the new hash table,[[13]](./Hash_table#cite_note-cornell08-14) since the items cannot be copied over as varying table sizes results in different hash value due to [modulo operation](./Modulo_operation).[[42]](./Hash_table#cite_note-43) If a hash table becomes "too empty" after deleting some elements, resizing may be performed to avoid excessive [memory usage](./Memory_footprint).[[43]](./Hash_table#cite_note-44)

 

### Resizing by moving all entries

 

Generally, a new hash table with a size double that of the original hash table gets [allocated](./Dynamic_memory_allocation) privately and every item in the original hash table gets moved to the newly allocated one by computing the hash values of the items followed by the insertion operation. Rehashing is simple, but computationally expensive.[[44]](./Hash_table#cite_note-45): 478–479 

 

### Alternatives to all-at-once rehashing

 

Some hash table implementations, notably in [real-time systems](./Real-time_system), cannot pay the price of enlarging the hash table all at once, because it may interrupt time-critical operations. If one cannot avoid dynamic resizing, a solution is to perform the resizing gradually to avoid storage blip—typically at 50% of new table's size—during rehashing and to avoid [memory fragmentation](./Fragmentation_(computing)) that triggers [heap compaction](./Mark-compact_algorithm) due to deallocation of large [memory blocks](./Page_(computer_memory)) caused by the old hash table.[[45]](./Hash_table#cite_note-scott03-46): 2–3  In such case, the rehashing operation is done incrementally through extending prior memory block allocated for the old hash table such that the buckets of the hash table remain unaltered. A common approach for amortized rehashing involves maintaining two hash functions      h  old     {\displaystyle h_{\text{old}}}  ![{\displaystyle h_{\text{old}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c72c36cbf0b0ae5fd714538904b790d38b8cfa53) and      h  new     {\displaystyle h_{\text{new}}}  ![{\displaystyle h_{\text{new}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ba01548b798b9054a25186dbe1ef27b87ceb0dac). The process of rehashing a bucket's items in accordance with the new hash function is termed as *cleaning*, which is implemented through [command pattern](./Command_pattern) by encapsulating the operations such as      A d d  (  k e y  )   {\displaystyle \mathrm {Add} (\mathrm {key} )}  ![{\displaystyle \mathrm {Add} (\mathrm {key} )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a73a1fd15fdccdeab3cb64bd91fa59b3fa8caaee),      G e t  (  k e y  )   {\displaystyle \mathrm {Get} (\mathrm {key} )}  ![{\displaystyle \mathrm {Get} (\mathrm {key} )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3e8e203ff86dac772ed426a7fbb7c1577b742310) and      D e l e t e  (  k e y  )   {\displaystyle \mathrm {Delete} (\mathrm {key} )}  ![{\displaystyle \mathrm {Delete} (\mathrm {key} )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b40bdf150fd9f01bcd54e04bf6d988e63fb1d68b) through a      L o o k u p  (  k e y  ,  command  )   {\displaystyle \mathrm {Lookup} (\mathrm {key} ,{\text{command}})}  ![{\displaystyle \mathrm {Lookup} (\mathrm {key} ,{\text{command}})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/85606b65edcf34822d5e57bbaad7d33b867bdb7a) [wrapper](./Wrapper_function) such that each element in the bucket gets rehashed and its procedure involve as follows:[[45]](./Hash_table#cite_note-scott03-46): 3 

 
- Clean      T a b l e  [  h  old   (  k e y  ) ]   {\displaystyle \mathrm {Table} [h_{\text{old}}(\mathrm {key} )]}  ![{\displaystyle \mathrm {Table} [h_{\text{old}}(\mathrm {key} )]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/afcb195bb40a51be98c16b6d9b930061f3c11682) bucket.
- Clean      T a b l e  [  h  new   (  k e y  ) ]   {\displaystyle \mathrm {Table} [h_{\text{new}}(\mathrm {key} )]}  ![{\displaystyle \mathrm {Table} [h_{\text{new}}(\mathrm {key} )]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d8097baf3c9220a1be057b3c86395debce381845) bucket.
- The *command* gets executed.

 

#### Linear hashing

 Main article: [Linear hashing](./Linear_hashing) 

[Linear hashing](./Linear_hashing) is an implementation of the hash table which enables dynamic growths or shrinks of the table one bucket at a time.[[46]](./Hash_table#cite_note-47)

 

## Performance

 

The performance of a hash table is dependent on the hash function's ability in generating [quasi-random numbers](./Low-discrepancy_sequence) (    σ σ    {\displaystyle \sigma }  ![{\displaystyle \sigma }](https://wikimedia.org/api/rest_v1/media/math/render/svg/59f59b7c3e6fdb1d0365a494b81fb9a696138c36)) for entries in the hash table where     K   {\displaystyle K}  ![{\displaystyle K}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2b76fce82a62ed5461908f0dc8f037de4e3686b0),     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) and     h ( x )   {\displaystyle h(x)}  ![{\displaystyle h(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/02c07825dae28705df03d15daeb8844d49c4dbd4) denotes the key, number of buckets and the hash function such that     σ σ    =   h ( K )   % %    n   {\displaystyle \sigma \ =\ h(K)\ \%\ n}  ![{\displaystyle \sigma \ =\ h(K)\ \%\ n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/40a6e5ff8682623f42354703a2ab865b4560eb2d). If the hash function generates the same     σ σ    {\displaystyle \sigma }  ![{\displaystyle \sigma }](https://wikimedia.org/api/rest_v1/media/math/render/svg/59f59b7c3e6fdb1d0365a494b81fb9a696138c36) for distinct keys (     K  1   ≠ ≠   K  2   ,   h (  K  1   )   =   h (  K  2   )   {\displaystyle K_{1}\neq K_{2},\ h(K_{1})\ =\ h(K_{2})}  ![{\displaystyle K_{1}\neq K_{2},\ h(K_{1})\ =\ h(K_{2})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d7a3a322b4d101e383b226705366b3b0b8f95f5a)), this results in *collision*, which is dealt with in a variety of ways. The constant time complexity (    O ( 1 )   {\displaystyle O(1)}  ![{\displaystyle O(1)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21)) of the operation in a hash table is presupposed on the condition that the hash function doesn't generate colliding indices; thus, the performance of the hash table is [directly proportional](./Proportionality_(mathematics)#Direct_proportionality) to the chosen hash function's ability to [disperse](./Statistical_dispersion) the indices.[[47]](./Hash_table#cite_note-dijk10-48): 1  However, construction of such a hash function is [practically infeasible](./NP-hardness), that being so, implementations depend on [case-specific](./Use_case) [collision resolution techniques](./Hash_table#Collision_resolution) in achieving higher performance.[[47]](./Hash_table#cite_note-dijk10-48): 2 

 

The best performance is obtained in the case that the hash function distributes the elements of the universe uniformaly, and the elements stored at the table are drawn at random from the universe. In this case, in hashing with chaining, the expected time for a successful search is     1 +   α α  2   + Θ Θ   (   1 m   )    {\textstyle 1+{\frac {\alpha }{2}}+\Theta \left({\frac {1}{m}}\right)}  ![{\textstyle 1+{\frac {\alpha }{2}}+\Theta \left({\frac {1}{m}}\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f5c89452b6089f4f212f1ff259c5c0a51587d18d), and the expected time for an unsuccessful search is      e  − −  α α    + α α  + Θ Θ   (   1 m   )    {\textstyle e^{-\alpha }+\alpha +\Theta \left({\frac {1}{m}}\right)}  ![{\textstyle e^{-\alpha }+\alpha +\Theta \left({\frac {1}{m}}\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c9e1ddeceaa8e3613fcc65c3401d8f6ab8c4bd7f).[[48]](./Hash_table#cite_note-49)

 

## Applications

 

### Associative arrays

 Main article: [Associative array](./Associative_array) 

Hash tables are commonly used to implement many types of in-memory tables. They are used to implement [associative arrays](./Associative_array).[[33]](./Hash_table#cite_note-clrs-34)

 

### Database indexing

 

Hash tables may also be used as [disk](./Disk_drive)-based data structures and [database indices](./Index_(database)) (such as in [dbm](./DBM_(computing))) although [B-trees](./B-tree) are more popular in these applications.[[49]](./Hash_table#cite_note-50)

 

### Caches

 Main article: [Cache (computing)](./Cache_(computing)) 

Hash tables can be used to implement [caches](./Cache_(computing)), auxiliary data tables that are used to speed up the access to data that is primarily stored in slower media. In this application, hash collisions can be handled by discarding one of the two colliding entries—usually erasing the old item that is currently stored in the table and overwriting it with the new item, so every item in the table has a unique hash value.[[50]](./Hash_table#cite_note-51)[[51]](./Hash_table#cite_note-52)

 

### Sets

 Main article: [Set data structure](./Set_data_structure) 

Hash tables can be used in the implementation of [set data structure](./Set_data_structure), which can store unique values without any particular order; set is typically used in testing the membership of a value in the collection, rather than element retrieval.[[52]](./Hash_table#cite_note-53)

 

### Transposition table

 Main article: [Transposition table](./Transposition_table) 

A [transposition table](./Transposition_table) to a complex Hash Table which stores information about each section that has been searched.[[53]](./Hash_table#cite_note-54)

 

## Implementations

 

Many programming languages provide hash table functionality, either as built-in associative arrays or as [standard library](./Standard_library) modules.

 
- In [JavaScript](./JavaScript), an "object" is a mutable collection of key–value pairs (called "properties"), where each key is either a string or a guaranteed-unique "symbol"; any other value, when used as a key, is first [coerced](./Type_conversion) to a string. Aside from the seven "primitive" data types, every value in JavaScript is an object.[[54]](./Hash_table#cite_note-55) ECMAScript 2015 also added the `Map` data structure, which accepts arbitrary values as keys.[[55]](./Hash_table#cite_note-56)
- [C++11](./C++11) includes `unordered_map` in its standard library for storing keys and values of [arbitrary types](./Template_(C++)).[[56]](./Hash_table#cite_note-57)
- [Go](./Go_(programming_language))'s built-in `map` implements a map type in the form of a [type](./Primitive_data_type), which is often (but not guaranteed to be) a hash table.[[57]](./Hash_table#cite_note-58)
- [Java](./Java_(programming_language)) programming language includes the `HashSet`, `HashMap`, `LinkedHashSet`, and `LinkedHashMap` [generic](./Generics_in_Java) collections.[[58]](./Hash_table#cite_note-59)
- [Python](./Python_(programming_language))'s built-in `dict` implements a hash table in the form of a [type](./Primitive_data_type).[[59]](./Hash_table#cite_note-60)
- [Ruby](./Ruby_(programming_language))'s built-in `Hash` uses the open addressing model from Ruby 2.4 onwards.[[60]](./Hash_table#cite_note-61)
- [Rust](./Rust_(programming_language)) programming language includes `HashMap`, `HashSet` as part of the Rust Standard Library.[[61]](./Hash_table#cite_note-62)
- The [.NET](./.NET) standard library includes `HashSet` and `Dictionary`,[[62]](./Hash_table#cite_note-63)[[63]](./Hash_table#cite_note-64) so it can be used from languages such as [C#](./C_Sharp_(programming_language)) and [VB.NET](./VB.NET).[[64]](./Hash_table#cite_note-65)

 

## See also

  
- [Bloom filter](./Bloom_filter)
- [Consistent hashing](./Consistent_hashing)
- [Distributed hash table](./Distributed_hash_table)
- [Extendible hashing](./Extendible_hashing)
- [Hash array mapped trie](./Hash_array_mapped_trie)
- [Lazy deletion](./Lazy_deletion)
- [Pearson hashing](./Pearson_hashing)
- [PhotoDNA](./PhotoDNA)
- [Rabin–Karp string search algorithm](./Rabin–Karp_string_search_algorithm)
- [Search data structure](./Search_data_structure)
- [Stable hashing](./Stable_hashing)
- [Succinct hash table](./Succinct_hash_table)
- [Hash function](./Hash_function)

  

## Notes

  
1. [↑](./Hash_table#cite_ref-2) There are approaches with a worst-case *expected* time complexity of O(log2 (1 - *α*)−1) where *α* is the load factor.[[1]](./Hash_table#cite_note-Farach-Colton_2024-1)

 

## References

  
1. [↑](./Hash_table#cite_ref-Farach-Colton_2024_1-0) Martin Farach-Colton; Andrew Krapivin; William Kuszmaul. *Optimal Bounds for Open Addressing Without Reordering*. 2024 IEEE 65th Annual Symposium on Foundations of Computer Science (FOCS). [arXiv](./ArXiv_(identifier)):[2501.02305](https://arxiv.org/abs/2501.02305). [doi](./Doi_(identifier)):[10.1109/FOCS61266.2024.00045](https://doi.org/10.1109%2FFOCS61266.2024.00045).
2. [1](./Hash_table#cite_ref-Cormen_et_al_3-0) [2](./Hash_table#cite_ref-Cormen_et_al_3-1)  [Cormen, Thomas H.](./Thomas_H._Cormen); [Leiserson, Charles E.](./Charles_E._Leiserson); [Rivest, Ronald L.](./Ronald_L._Rivest); [Stein, Clifford](./Clifford_Stein) (2009). [*Introduction to Algorithms*](./Introduction_to_Algorithms) (3rd ed.). Massachusetts Institute of Technology. pp. 253–280. [ISBN](./ISBN_(identifier)) [978-0-262-03384-8](./Special:BookSources/978-0-262-03384-8). 
3. [↑](./Hash_table#cite_ref-ms_4-0) [Mehlhorn, Kurt](./Kurt_Mehlhorn); [Sanders, Peter](./Peter_Sanders_(computer_scientist)) (2008). ["Hash Tables and Associative Arrays"](https://people.mpi-inf.mpg.de/~mehlhorn/ftp/Toolbox/HashTables.pdf) (PDF). *Algorithms and Data Structures*. Springer. pp. 81–98. [doi](./Doi_(identifier)):[10.1007/978-3-540-77978-0_4](https://doi.org/10.1007%2F978-3-540-77978-0_4). [ISBN](./ISBN_(identifier)) [978-3-540-77977-3](./Special:BookSources/978-3-540-77977-3).
4. [1](./Hash_table#cite_ref-knuth_5-0) [2](./Hash_table#cite_ref-knuth_5-1) [3](./Hash_table#cite_ref-knuth_5-2) [4](./Hash_table#cite_ref-knuth_5-3) [5](./Hash_table#cite_ref-knuth_5-4) [6](./Hash_table#cite_ref-knuth_5-5) [7](./Hash_table#cite_ref-knuth_5-6) [Knuth, Donald E.](./Donald_E._Knuth) (April 24, 1998). [*The Art of Computer Programming: Volume 3: Sorting and Searching*](https://dl.acm.org/doi/10.5555/280635) (2nd ed.). [Addison-Wesley Professional](./Addison-Wesley_Professional). [ISBN](./ISBN_(identifier)) [978-0-201-89685-5](./Special:BookSources/978-0-201-89685-5).
5. [↑](./Hash_table#cite_ref-leiser_6-0) [Leiserson, Charles E.](./Charles_E._Leiserson) (Fall 2005). ["Lecture 13: Amortized Algorithms, Table Doubling, Potential Method"](https://videolectures.net/mit6046jf05_leiserson_lec13/). *course MIT 6.046J/18.410J Introduction to Algorithms*. [Archived](https://web.archive.org/web/20090807022046/http://videolectures.net/mit6046jf05_leiserson_lec13/) from the original on August 7, 2009.
6. [↑](./Hash_table#cite_ref-cormen_7-0) [Cormen, Thomas H.](./Thomas_H._Cormen); [Leiserson, Charles E.](./Charles_E._Leiserson); [Rivest, Ronald L.](./Ronald_L._Rivest); [Stein, Clifford](./Clifford_Stein) (2001). "Chapter 11: Hash Tables". [*Introduction to Algorithms*](./Introduction_to_Algorithms) (2nd ed.). MIT Press and McGraw-Hill. pp. [221](https://archive.org/details/introductiontoal00corm_691/page/n243)–252. [ISBN](./ISBN_(identifier)) [978-0-262-53196-2](./Special:BookSources/978-0-262-53196-2).
7. [1](./Hash_table#cite_ref-algo1rob_8-0) [2](./Hash_table#cite_ref-algo1rob_8-1) [3](./Hash_table#cite_ref-algo1rob_8-2) [4](./Hash_table#cite_ref-algo1rob_8-3) [5](./Hash_table#cite_ref-algo1rob_8-4) [Sedgewick, Robert](./Robert_Sedgewick_(computer_scientist)); Wayne, Kevin (2011). [*Algorithms*](https://algs4.cs.princeton.edu/). Vol. 1 (4 ed.). Addison-Wesley Professional – via [Princeton University](./Princeton_University), Department of Computer Science.
8. [↑](./Hash_table#cite_ref-9) Silberschatz, A.; Korth, H. F.; Sudarshan, S. (2020). *Database System Concepts* (7th ed.). [McGraw-Hill](./McGraw-Hill).
9. [↑](./Hash_table#cite_ref-10) Goodrich, M. T.; Tamassia, R.; Goldwasser, M. H. (2014). *Data Structures and Algorithms in Java* (6th ed.). [Wiley](./Wiley_(publisher)).
10. [1](./Hash_table#cite_ref-Konheim_11-0) [2](./Hash_table#cite_ref-Konheim_11-1) [3](./Hash_table#cite_ref-Konheim_11-2) Konheim, Alan G. (2010). *Hashing in Computer Science*. [doi](./Doi_(identifier)):[10.1002/9780470630617](https://doi.org/10.1002%2F9780470630617). [ISBN](./ISBN_(identifier)) [978-0-470-34473-6](./Special:BookSources/978-0-470-34473-6).
11. [1](./Hash_table#cite_ref-hashhist_12-0) [2](./Hash_table#cite_ref-hashhist_12-1) [3](./Hash_table#cite_ref-hashhist_12-2) [4](./Hash_table#cite_ref-hashhist_12-3) [5](./Hash_table#cite_ref-hashhist_12-4) [6](./Hash_table#cite_ref-hashhist_12-5) [7](./Hash_table#cite_ref-hashhist_12-6) [8](./Hash_table#cite_ref-hashhist_12-7) [9](./Hash_table#cite_ref-hashhist_12-8) [10](./Hash_table#cite_ref-hashhist_12-9) [11](./Hash_table#cite_ref-hashhist_12-10) [12](./Hash_table#cite_ref-hashhist_12-11) Mehta, Dinesh P.; Mehta, Dinesh P.; Sahni, Sartaj, eds. (2004). *Handbook of Data Structures and Applications*. [doi](./Doi_(identifier)):[10.1201/9781420035179](https://doi.org/10.1201%2F9781420035179). [ISBN](./ISBN_(identifier)) [978-0-429-14701-2](./Special:BookSources/978-0-429-14701-2).
12. [↑](./Hash_table#cite_ref-13) Cormen, T. H.; Leiserson, C. E.; [Rivest, R. L.](./Ronald_Rivest); Stein, C. (2009). *Introduction to Algorithms* (3rd ed.). [MIT Press](./MIT_Press).
13. [1](./Hash_table#cite_ref-cornell08_14-0) [2](./Hash_table#cite_ref-cornell08_14-1) [3](./Hash_table#cite_ref-cornell08_14-2) [4](./Hash_table#cite_ref-cornell08_14-3) [5](./Hash_table#cite_ref-cornell08_14-4) [6](./Hash_table#cite_ref-cornell08_14-5) [7](./Hash_table#cite_ref-cornell08_14-6) Mayers, Andrew (2008). ["CS 312: Hash tables and amortized analysis"](https://www.cs.cornell.edu/courses/cs312/2008sp/lectures/lec20.html). [Cornell University](./Cornell_University), Department of Computer Science. [Archived](https://web.archive.org/web/20210426052033/http://www.cs.cornell.edu/courses/cs312/2008sp/lectures/lec20.html) from the original on April 26, 2021. Retrieved October 26, 2021 – via cs.cornell.edu.
14. [1](./Hash_table#cite_ref-plank_15-0) [2](./Hash_table#cite_ref-plank_15-1) 
James S. Plank and Brad Vander Zanden.
["CS140 Lecture notes -- Hashing"](https://web.eecs.utk.edu/~bvanderz/teaching/cs140Sp15/Notes/Hashing/).

15. [↑](./Hash_table#cite_ref-16) Maurer, W. D.; Lewis, T. G. (March 1975). "Hash Table Methods". *ACM Computing Surveys*. **7** (1): 5–19. [doi](./Doi_(identifier)):[10.1145/356643.356645](https://doi.org/10.1145%2F356643.356645). [S2CID](./S2CID_(identifier)) [17874775](https://api.semanticscholar.org/CorpusID:17874775).
16. [1](./Hash_table#cite_ref-owo03_17-0) [2](./Hash_table#cite_ref-owo03_17-1) Owolabi, Olumide (February 2003). "Empirical studies of some hashing functions". *Information and Software Technology*. **45** (2): 109–112. [doi](./Doi_(identifier)):[10.1016/S0950-5849(02)00174-X](https://doi.org/10.1016%2FS0950-5849%2802%2900174-X).
17. [1](./Hash_table#cite_ref-Yi06_18-0) [2](./Hash_table#cite_ref-Yi06_18-1) Lu, Yi; Prabhakar, Balaji; Bonomi, Flavio (2006). *Perfect Hashing for Network Applications*. 2006 IEEE International Symposium on Information Theory. pp. 2774–2778. [doi](./Doi_(identifier)):[10.1109/ISIT.2006.261567](https://doi.org/10.1109%2FISIT.2006.261567). [ISBN](./ISBN_(identifier)) [1-4244-0505-X](./Special:BookSources/1-4244-0505-X). [S2CID](./S2CID_(identifier)) [1494710](https://api.semanticscholar.org/CorpusID:1494710).
18. [↑](./Hash_table#cite_ref-CHD_19-0) Belazzougui, Djamal; Botelho, Fabiano C.; Dietzfelbinger, Martin (2009). ["Hash, displace, and compress"](https://cmph.sourceforge.net/papers/esa09.pdf) (PDF). *Algorithms—ESA 2009: 17th Annual European Symposium, Copenhagen, Denmark, September 7–9, 2009, Proceedings*. [Lecture Notes in Computer Science](./Lecture_Notes_in_Computer_Science). Vol. 5757. Berlin: Springer. pp. 682–693. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.568.130](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.568.130). [doi](./Doi_(identifier)):[10.1007/978-3-642-04128-0_61](https://doi.org/10.1007%2F978-3-642-04128-0_61). [MR](./MR_(identifier)) [2557794](https://mathscinet.ams.org/mathscinet-getitem?mr=2557794).
19. [1](./Hash_table#cite_ref-cormenalgo01_20-0) [2](./Hash_table#cite_ref-cormenalgo01_20-1) [Cormen, Thomas H.](./Thomas_H._Cormen); [Leiserson, Charles E.](./Charles_E._Leiserson); [Rivest, Ronald L.](./Ronald_L._Rivest); [Stein, Clifford](./Clifford_Stein) (2001). "Chapter 11: Hash Tables". [*Introduction to Algorithms*](./Introduction_to_Algorithms) (2nd ed.). [Massachusetts Institute of Technology](./Massachusetts_Institute_of_Technology). [ISBN](./ISBN_(identifier)) [978-0-262-53196-2](./Special:BookSources/978-0-262-53196-2).
20. [↑](./Hash_table#cite_ref-21)  Stroustrup, Bjarne (1997). *The C++ Programming Language Third Edition*. Reading Massachusetts: Addison-Wesley. p. 503. [ISBN](./ISBN_(identifier)) [0-201-88954-4](./Special:BookSources/0-201-88954-4). 
21. [↑](./Hash_table#cite_ref-chernoff_22-0) [Pearson, Karl](./Karl_Pearson) (1900). ["On the criterion that a given system of deviations from the probable in the case of a correlated system of variables is such that it can be reasonably supposed to have arisen from random sampling"](https://zenodo.org/record/1430618). *Philosophical Magazine*. Series 5. **50** (302): 157–175. [doi](./Doi_(identifier)):[10.1080/14786440009463897](https://doi.org/10.1080%2F14786440009463897).
22. [↑](./Hash_table#cite_ref-plackett_23-0) [Plackett, Robin](./Robin_Plackett) (1983). "Karl Pearson and the Chi-Squared Test". *International Statistical Review*. **51** (1): 59–72. [doi](./Doi_(identifier)):[10.2307/1402731](https://doi.org/10.2307%2F1402731). [JSTOR](./JSTOR_(identifier)) [1402731](https://www.jstor.org/stable/1402731).
23. [1](./Hash_table#cite_ref-:0_24-0) [2](./Hash_table#cite_ref-:0_24-1) Wang, Thomas (March 1997). ["Prime Double Hash Table"](https://web.archive.org/web/19990903133921/http://www.concentric.net/~Ttwang/tech/primehash.htm). Archived from [the original](https://www.concentric.net/~Ttwang/tech/primehash.htm) on September 3, 1999. Retrieved May 10, 2015.
24. [↑](./Hash_table#cite_ref-25) Wegman, Mark N.; Carter, J.Lawrence (June 1981). ["New hash functions and their use in authentication and set equality"](https://doi.org/10.1016%2F0022-0000%2881%2990033-7). *Journal of Computer and System Sciences*. **22** (3): 265–279. [Bibcode](./Bibcode_(identifier)):[1981JCoSS..22..265W](https://ui.adsabs.harvard.edu/abs/1981JCoSS..22..265W). [doi](./Doi_(identifier)):[10.1016/0022-0000(81)90033-7](https://doi.org/10.1016%2F0022-0000%2881%2990033-7).
25. [↑](./Hash_table#cite_ref-26) Demaine, Erik; Lind, Jeff (Spring 2003). ["Lecture 2"](https://courses.csail.mit.edu/6.897/spring03/scribe_notes/L2/lecture2.pdf) (PDF). *6.897: Advanced Data Structures. MIT Computer Science and Artificial Intelligence Laboratory*. [Archived](https://web.archive.org/web/20100615203901/http://courses.csail.mit.edu/6.897/spring03/scribe_notes/L2/lecture2.pdf) (PDF) from the original on June 15, 2010. Retrieved June 30, 2008.
26. [1](./Hash_table#cite_ref-nick05_27-0) [2](./Hash_table#cite_ref-nick05_27-1) [3](./Hash_table#cite_ref-nick05_27-2) Culpepper, J. Shane; Moffat, Alistair (2005). "Enhanced Byte Codes with Restricted Prefix Properties". *String Processing and Information Retrieval*. Lecture Notes in Computer Science. Vol. 3772. pp. 1–12. [doi](./Doi_(identifier)):[10.1007/11575832_1](https://doi.org/10.1007%2F11575832_1). [ISBN](./ISBN_(identifier)) [978-3-540-29740-6](./Special:BookSources/978-3-540-29740-6).
27. [↑](./Hash_table#cite_ref-28) [Willard, Dan E.](./Dan_Willard) (2000). "Examining computational geometry, van Emde Boas trees, and hashing from the perspective of the fusion tree". *[SIAM Journal on Computing](./SIAM_Journal_on_Computing)*. **29** (3): 1030–1049. [doi](./Doi_(identifier)):[10.1137/S0097539797322425](https://doi.org/10.1137%2FS0097539797322425). [MR](./MR_(identifier)) [1740562](https://mathscinet.ams.org/mathscinet-getitem?mr=1740562)..
28. [↑](./Hash_table#cite_ref-29) Askitis, Nikolas; Sinha, Ranjan (October 2010). "Engineering scalable, cache and space efficient tries for strings". *The VLDB Journal*. **19** (5): 633–660. [doi](./Doi_(identifier)):[10.1007/s00778-010-0183-9](https://doi.org/10.1007%2Fs00778-010-0183-9).
29. [↑](./Hash_table#cite_ref-30) Askitis, Nikolas; Zobel, Justin (October 2005). "Cache-conscious Collision Resolution in String Hash Tables". *Proceedings of the 12th International Conference, String Processing and Information Retrieval (SPIRE 2005)*. Vol. 3772/2005. pp. 91–102. [doi](./Doi_(identifier)):[10.1007/11575832_11](https://doi.org/10.1007%2F11575832_11). [ISBN](./ISBN_(identifier)) [978-3-540-29740-6](./Special:BookSources/978-3-540-29740-6).
30. [↑](./Hash_table#cite_ref-31) Askitis, Nikolas (2009). ["Fast and Compact Hash Tables for Integer Keys"](https://web.archive.org/web/20110216180225/http://crpit.com/confpapers/CRPITV91Askitis.pdf) (PDF). *Proceedings of the 32nd Australasian Computer Science Conference (ACSC 2009)*. Vol. 91. pp. 113–122. [ISBN](./ISBN_(identifier)) [978-1-920682-72-9](./Special:BookSources/978-1-920682-72-9). Archived from [the original](https://crpit.com/confpapers/CRPITV91Askitis.pdf) (PDF) on February 16, 2011. Retrieved June 13, 2010.
31. [↑](./Hash_table#cite_ref-tenenbaum90_32-0) Tenenbaum, Aaron M.; Langsam, Yedidyah; Augenstein, Moshe J. (1990). *Data Structures Using C*. Prentice Hall. pp. 456–461, p. 472. [ISBN](./ISBN_(identifier)) [978-0-13-199746-2](./Special:BookSources/978-0-13-199746-2).
32. [1](./Hash_table#cite_ref-Cuckoo_33-0) [2](./Hash_table#cite_ref-Cuckoo_33-1) [Pagh, Rasmus](./Rasmus_Pagh); Rodler, Flemming Friche (2001). "Cuckoo Hashing". *Algorithms — ESA 2001*. Lecture Notes in Computer Science. Vol. 2161. pp. 121–133. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.25.4189](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.25.4189). [doi](./Doi_(identifier)):[10.1007/3-540-44676-1_10](https://doi.org/10.1007%2F3-540-44676-1_10). [ISBN](./ISBN_(identifier)) [978-3-540-42493-2](./Special:BookSources/978-3-540-42493-2).
33. [1](./Hash_table#cite_ref-clrs_34-0) [2](./Hash_table#cite_ref-clrs_34-1) [3](./Hash_table#cite_ref-clrs_34-2) [Cormen, Thomas H.](./Thomas_H._Cormen); [Leiserson, Charles E.](./Charles_E._Leiserson); [Rivest, Ronald L.](./Ron_Rivest); [Stein, Clifford](./Clifford_Stein) (2001), "11 Hash Tables", *[Introduction to Algorithms](./Introduction_to_Algorithms)* (2nd ed.), [MIT Press](./MIT_Press) and [McGraw-Hill](./McGraw-Hill), pp. 221–252, [ISBN](./ISBN_(identifier)) [0-262-03293-7](./Special:BookSources/0-262-03293-7).
34. [1](./Hash_table#cite_ref-chen87_35-0) [2](./Hash_table#cite_ref-chen87_35-1) [3](./Hash_table#cite_ref-chen87_35-2) Vitter, Jeffery S.; Chen, Wen-Chin (1987). [*The design and analysis of coalesced hashing*](https://archive.org/details/designanalysisof0000vitt/). New York, United States: [Oxford University Press](./Oxford_University_Press). [ISBN](./ISBN_(identifier)) [978-0-19-504182-8](./Special:BookSources/978-0-19-504182-8) – via [Archive.org](./Archive.org).
35. [↑](./Hash_table#cite_ref-36) [Pagh, Rasmus](./Rasmus_Pagh); Rodler, Flemming Friche (2001). "Cuckoo Hashing". *Algorithms — ESA 2001*. Lecture Notes in Computer Science. Vol. 2161. pp. 121–133. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.25.4189](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.25.4189). [doi](./Doi_(identifier)):[10.1007/3-540-44676-1_10](https://doi.org/10.1007%2F3-540-44676-1_10). [ISBN](./ISBN_(identifier)) [978-3-540-42493-2](./Special:BookSources/978-3-540-42493-2).
36. [1](./Hash_table#cite_ref-nir08_37-0) [2](./Hash_table#cite_ref-nir08_37-1) [3](./Hash_table#cite_ref-nir08_37-2) [4](./Hash_table#cite_ref-nir08_37-3) [5](./Hash_table#cite_ref-nir08_37-4) [6](./Hash_table#cite_ref-nir08_37-5) Herlihy, Maurice; Shavit, Nir; Tzafrir, Moran (2008). "Hopscotch Hashing". *Distributed Computing*. Lecture Notes in Computer Science. Vol. 5218. pp. 350–364. [doi](./Doi_(identifier)):[10.1007/978-3-540-87779-0_24](https://doi.org/10.1007%2F978-3-540-87779-0_24). [ISBN](./ISBN_(identifier)) [978-3-540-87778-3](./Special:BookSources/978-3-540-87778-3).
37. [1](./Hash_table#cite_ref-waterloo86_38-0) [2](./Hash_table#cite_ref-waterloo86_38-1) Celis, Pedro (1986). [*Robin Hood Hashing*](https://cs.uwaterloo.ca/research/tr/1986/CS-86-14.pdf) (PDF). Ontario, Canada: [University of Waterloo](./University_of_Waterloo), Dept. of Computer Science. [ISBN](./ISBN_(identifier)) [978-0-315-29700-5](./Special:BookSources/978-0-315-29700-5). [OCLC](./OCLC_(identifier)) [14083698](https://search.worldcat.org/oclc/14083698). [Archived](https://web.archive.org/web/20211101071032/https://cs.uwaterloo.ca/research/tr/1986/CS-86-14.pdf) (PDF) from the original on November 1, 2021. Retrieved November 2, 2021.
38. [↑](./Hash_table#cite_ref-39) Poblete, P. V.; Viola, A. (July 2019). ["Analysis of Robin Hood and Other Hashing Algorithms Under the Random Probing Model, With and Without Deletions"](https://doi.org/10.1017%2FS0963548318000408). *Combinatorics, Probability and Computing*. **28** (4): 600–617. [doi](./Doi_(identifier)):[10.1017/S0963548318000408](https://doi.org/10.1017%2FS0963548318000408). [S2CID](./S2CID_(identifier)) [125374363](https://api.semanticscholar.org/CorpusID:125374363).
39. [↑](./Hash_table#cite_ref-cornell14_40-0) Clarkson, Michael (2014). ["Lecture 13: Hash tables"](https://www.cs.cornell.edu/courses/cs3110/2014fa/lectures/13/lec13.html). [Cornell University](./Cornell_University), Department of Computer Science. [Archived](https://web.archive.org/web/20211007011300/https://www.cs.cornell.edu/courses/cs3110/2014fa/lectures/13/lec13.html) from the original on October 7, 2021. Retrieved November 1, 2021 – via cs.cornell.edu.
40. [↑](./Hash_table#cite_ref-41) Gries, David (2017). ["JavaHyperText and Data Structure: Robin Hood Hashing"](https://www.cs.cornell.edu/courses/JavaAndDS/files/hashing_RobinHood.pdf) (PDF). [Cornell University](./Cornell_University), Department of Computer Science. [Archived](https://web.archive.org/web/20210426051503/http://www.cs.cornell.edu/courses/JavaAndDS/files/hashing_RobinHood.pdf) (PDF) from the original on April 26, 2021. Retrieved November 2, 2021 – via cs.cornell.edu.
41. [↑](./Hash_table#cite_ref-indiana88_42-0) Celis, Pedro (March 28, 1988). [*External Robin Hood Hashing*](https://legacy.cs.indiana.edu/ftp/techreports/TR246.pdf) (PDF) (Technical report). Bloomington, Indiana: [Indiana University](./Indiana_University), Department of Computer Science. 246. [Archived](https://web.archive.org/web/20211103013505/https://legacy.cs.indiana.edu/ftp/techreports/TR246.pdf) (PDF) from the original on November 3, 2021. Retrieved November 2, 2021.
42. [↑](./Hash_table#cite_ref-43) Goddard, Wayne (2021). ["Chapter C5: Hash Tables"](https://people.computing.clemson.edu/~goddard/texts/algor/C5.pdf) (PDF). [Clemson University](./Clemson_University). pp. 15–16. Retrieved December 4, 2023.
43. [↑](./Hash_table#cite_ref-44) Devadas, Srini; Demaine, Erik (February 25, 2011). ["Intro to Algorithms: Resizing Hash Tables"](https://courses.csail.mit.edu/6.006/spring11/rec/rec07.pdf) (PDF). [Massachusetts Institute of Technology](./Massachusetts_Institute_of_Technology), Department of Computer Science. [Archived](https://web.archive.org/web/20210507102944/https://courses.csail.mit.edu/6.006/spring11/rec/rec07.pdf) (PDF) from the original on May 7, 2021. Retrieved November 9, 2021 – via [MIT OpenCourseWare](./MIT_OpenCourseWare).
44. [↑](./Hash_table#cite_ref-45) Thareja, Reema (2014). "Hashing and Collision". *Data Structures Using C*. Oxford University Press. pp. 464–488. [ISBN](./ISBN_(identifier)) [978-0-19-809930-7](./Special:BookSources/978-0-19-809930-7).
45. [1](./Hash_table#cite_ref-scott03_46-0) [2](./Hash_table#cite_ref-scott03_46-1) Friedman, Scott; Krishnan, Anand; Leidefrost, Nicholas (March 18, 2003). ["Hash Tables for Embedded and Real-time systems"](https://users.cs.northwestern.edu/~sef318/docs/hashtables.pdf) (PDF). *All Computer Science and Engineering Research*. [Washington University in St. Louis](./Washington_University_in_St._Louis). [doi](./Doi_(identifier)):[10.7936/K7WD3XXV](https://doi.org/10.7936%2FK7WD3XXV). [Archived](https://web.archive.org/web/20210609163643/https://users.cs.northwestern.edu/~sef318/docs/hashtables.pdf) (PDF) from the original on June 9, 2021. Retrieved November 9, 2021 – via [Northwestern University](./Northwestern_University), Department of Computer Science.
46. [↑](./Hash_table#cite_ref-47) Litwin, Witold (1980). ["Linear hashing: A new tool for file and table addressing"](https://www.cs.cmu.edu/afs/cs.cmu.edu/user/christos/www/courses/826-resources/PAPERS+BOOK/linear-hashing.PDF) (PDF). *Proc. 6th Conference on Very Large Databases*. [Carnegie Mellon University](./Carnegie_Mellon_University). pp. 212–223. [Archived](https://web.archive.org/web/20210506233325/http://www.cs.cmu.edu/afs/cs.cmu.edu/user/christos/www/courses/826-resources/PAPERS+BOOK/linear-hashing.PDF) (PDF) from the original on May 6, 2021. Retrieved November 10, 2021 – via cs.cmu.edu.
47. [1](./Hash_table#cite_ref-dijk10_48-0) [2](./Hash_table#cite_ref-dijk10_48-1) Dijk, Tom Van (2010). ["Analysing and Improving Hash Table Performance"](https://www.tvandijk.nl/pdf/bscthesis.pdf) (PDF). [Netherlands](./Netherlands): [University of Twente](./University_of_Twente). [Archived](https://web.archive.org/web/20211106094558/http://www.tvandijk.nl/pdf/bscthesis.pdf) (PDF) from the original on November 6, 2021. Retrieved December 31, 2021.
48. [↑](./Hash_table#cite_ref-49)  Baeza-Yates, Ricardo; Poblete, Patricio V. (1999). "Chapter 2: Searching". In Atallah (ed.). *Algorithms and Theory of Computation Handbook*. CRC Press. pp. 2–6. [ISBN](./ISBN_(identifier)) [0849326494](./Special:BookSources/0849326494). 
49. [↑](./Hash_table#cite_ref-50) Lech Banachowski. ["Indexes and external sorting"](https://ghostarchive.org/archive/HW0hp). [pl:Polsko-Japońska Akademia Technik Komputerowych](https://pl.wikipedia.org/wiki/Polsko-Japońska%20Akademia%20Technik%20Komputerowych). Archived from [the original](https://edux.pjwstk.edu.pl/mat/262/lec/rW9.htm) on March 26, 2022. Retrieved March 26, 2022.
50. [↑](./Hash_table#cite_ref-51) Zhong, Liang; Zheng, Xueqian; Liu, Yong; Wang, Mengting; Cao, Yang (February 2020). "Cache hit ratio maximization in device-to-device communications overlaying cellular networks". *China Communications*. **17** (2): 232–238. [Bibcode](./Bibcode_(identifier)):[2020CComm..17b.232Z](https://ui.adsabs.harvard.edu/abs/2020CComm..17b.232Z). [doi](./Doi_(identifier)):[10.23919/jcc.2020.02.018](https://doi.org/10.23919%2Fjcc.2020.02.018). [S2CID](./S2CID_(identifier)) [212649328](https://api.semanticscholar.org/CorpusID:212649328).
51. [↑](./Hash_table#cite_ref-52) Bottommley, James (January 1, 2004). ["Understanding Caching"](https://www.linuxjournal.com/article/7105). [Linux Journal](./Linux_Journal). [Archived](https://web.archive.org/web/20201204195114/https://www.linuxjournal.com/article/7105) from the original on December 4, 2020. Retrieved April 16, 2022.
52. [↑](./Hash_table#cite_ref-53) Jill Seaman (2014). ["Set & Hash Tables"](https://web.archive.org/web/20220401134706/https://userweb.cs.txstate.edu/~js236/201412/cs5301/week13.pdf) (PDF). [Texas State University](./Texas_State_University). Archived from the original on April 1, 2022. Retrieved March 26, 2022.`{{cite web}}`:  CS1 maint: bot: original URL status unknown ([link](./Category:CS1_maint:_bot:_original_URL_status_unknown))
53. [↑](./Hash_table#cite_ref-54) ["Transposition Table - Chessprogramming wiki"](https://www.chessprogramming.org/Transposition_Table). *chessprogramming.org*. [Archived](https://web.archive.org/web/20210214110941/https://www.chessprogramming.org/Transposition_Table) from the original on February 14, 2021. Retrieved May 1, 2020.
54. [↑](./Hash_table#cite_ref-55) ["JavaScript data types and data structures - JavaScript | MDN"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Data_structures#objects). *developer.mozilla.org*. Retrieved July 24, 2022.
55. [↑](./Hash_table#cite_ref-56) ["Map - JavaScript | MDN"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map). *developer.mozilla.org*. June 20, 2023. Retrieved July 15, 2023.
56. [↑](./Hash_table#cite_ref-57) ["Programming language C++ - Technical Specification"](https://web.archive.org/web/20220121061142/http://www.open-std.org/JTC1/SC22/WG21/docs/papers/2013/n3690.pdf) (PDF). [International Organization for Standardization](./International_Organization_for_Standardization). pp. 812–813. Archived from [the original](https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2013/n3690.pdf) (PDF) on January 21, 2022. Retrieved February 8, 2022.
57. [↑](./Hash_table#cite_ref-58) ["The Go Programming Language Specification"](https://go.dev/ref/spec#Map_types). *go.dev*. Retrieved January 1, 2023.
58. [↑](./Hash_table#cite_ref-59) ["Lesson: Implementations (The Java™ Tutorials > Collections)"](https://docs.oracle.com/javase/tutorial/collections/implementations/index.html). *docs.oracle.com*. [Archived](https://web.archive.org/web/20170118041252/https://docs.oracle.com/javase/tutorial/collections/implementations/index.html) from the original on January 18, 2017. Retrieved April 27, 2018.
59. [↑](./Hash_table#cite_ref-60) Zhang, Juan; Jia, Yunwei (2020). ["Redis rehash optimization based on machine learning"](https://doi.org/10.1088%2F1742-6596%2F1453%2F1%2F012048). *[Journal of Physics: Conference Series](./Journal_of_Physics:_Conference_Series)*. **1453** (1): 3. [Bibcode](./Bibcode_(identifier)):[2020JPhCS1453a2048Z](https://ui.adsabs.harvard.edu/abs/2020JPhCS1453a2048Z). [doi](./Doi_(identifier)):[10.1088/1742-6596/1453/1/012048](https://doi.org/10.1088%2F1742-6596%2F1453%2F1%2F012048). [S2CID](./S2CID_(identifier)) [215943738](https://api.semanticscholar.org/CorpusID:215943738).
60. [↑](./Hash_table#cite_ref-61) Jonan Scheffler (December 25, 2016). ["Ruby 2.4 Released: Faster Hashes, Unified Integers and Better Rounding"](https://blog.heroku.com/ruby-2-4-features-hashes-integers-rounding#hash-changes). *heroku.com*. [Archived](https://web.archive.org/web/20190703145530/https://blog.heroku.com/ruby-2-4-features-hashes-integers-rounding#hash-changes) from the original on July 3, 2019. Retrieved July 3, 2019.
61. [↑](./Hash_table#cite_ref-62) ["doc.rust-lang.org"](https://doc.rust-lang.org/std/index.html). [Archived](https://web.archive.org/web/20221208155205/https://doc.rust-lang.org/std/index.html) from the original on December 8, 2022. Retrieved December 14, 2022.
62. [↑](./Hash_table#cite_ref-63) ["HashSet Class (System.Collections.Generic)"](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.hashset-1?view=net-7.0). *learn.microsoft.com*. Retrieved July 1, 2023.
63. [↑](./Hash_table#cite_ref-64) dotnet-bot. ["Dictionary Class (System.Collections.Generic)"](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=net-8.0). *learn.microsoft.com*. Retrieved January 16, 2024.
64. [↑](./Hash_table#cite_ref-65) ["VB.NET HashSet Example"](https://www.dotnetperls.com/hashset-vbnet). *Dot Net Perls*.

 

## Further reading

 
- Tamassia, Roberto; Goodrich, Michael T. (2006). "Chapter Nine: Maps and Dictionaries". [*Data structures and algorithms in Java : [updated for Java 5.0]*](https://archive.org/details/datastructuresal00good_183) (4th ed.). Hoboken, NJ: Wiley. pp. [369](https://archive.org/details/datastructuresal00good_183/page/n368)–418. [ISBN](./ISBN_(identifier)) [978-0-471-73884-8](./Special:BookSources/978-0-471-73884-8).
- McKenzie, B. J.; Harries, R.; Bell, T. (February 1990). "Selecting a hashing algorithm". *Software: Practice and Experience*. **20** (2): 209–224. [doi](./Doi_(identifier)):[10.1002/spe.4380200207](https://doi.org/10.1002%2Fspe.4380200207). [hdl](./Hdl_(identifier)):[10092/9691](https://hdl.handle.net/10092%2F9691). [S2CID](./S2CID_(identifier)) [12854386](https://api.semanticscholar.org/CorpusID:12854386).

 

## External links

   [![Wikimedia Commons logo](//upload.wikimedia.org/wikipedia/en/thumb/4/4a/Commons-logo.svg/40px-Commons-logo.svg.png)](./File:Commons-logo.svg) Wikimedia Commons has media related to [Hash tables](https://commons.wikimedia.org/wiki/Category:Hash%20tables).    [![Wikibooks logo](//upload.wikimedia.org/wikipedia/commons/thumb/f/fa/Wikibooks-logo.svg/40px-Wikibooks-logo.svg.png)](./File:Wikibooks-logo.svg) Wikibooks has a book on the topic of: ***[Data Structures/Hash Tables](https://en.wikibooks.org/wiki/Data%20Structures/Hash%20Tables)***  
- [NIST](./NIST) entry on [hash tables](https://xlinux.nist.gov/dads/HTML/hashtab.html)
- [Open Data Structures – Chapter 5 – Hash Tables](https://opendatastructures.org/versions/edition-0.1e/ods-java/5_Hash_Tables.html), [Pat Morin](./Pat_Morin)
- [MIT's Introduction to Algorithms: Hashing 1](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-046j-introduction-to-algorithms-sma-5503-fall-2005/video-lectures/lecture-7-hashing-hash-functions/) MIT OCW lecture Video
- [MIT's Introduction to Algorithms: Hashing 2](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-046j-introduction-to-algorithms-sma-5503-fall-2005/video-lectures/lecture-8-universal-hashing-perfect-hashing/) MIT OCW lecture Video

 
| vteData structures |
| --- |
| Types | CollectionContainer |
| Abstract | Associative arrayMultimapRetrieval Data StructureListStackQueueDouble-ended queuePriority queueDouble-ended priority queueSetMultisetDisjoint-set |
| Arrays | Bit arrayCircular bufferDynamic arrayHash tableHashed array treeSparse matrix |
| Linked | Association listLinked listSkip listUnrolled linked listXOR linked list |
| Trees | B-treeBinary search treeAA treeAVL treeRed–black treeSelf-balancing treeSplay treeHeapBinary heapBinomial heapFibonacci heapR-treeR* treeR+ treeHilbert R-treeRopeTrieHash tree |
| Graphs | Binary decision diagramDirected acyclic graphDirected acyclic word graph |
| List of data structures |

 
| Authority control databases | GND |
| --- | --- |