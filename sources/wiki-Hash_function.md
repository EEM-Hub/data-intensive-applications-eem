---
source: https://en.wikipedia.org/wiki/Hash_function
fetched: 2026-06-19
---

Mapping arbitrary data to fixed-size values "hashlink" redirects here. For the Haxe virtual machine, see [HashLink](./HashLink). "Hash code" redirects here. For the programming competition, see [Hash Code (programming competition)](./Hash_Code_(programming_competition)). This article is about a computer programming construct. For other meanings of "hash" and "hashing", see [Hash (disambiguation)](./Hash_(disambiguation)). 
|  | This sectionneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sourcesin this section. Unsourced material may be challenged and removed.Find sources:"Hash function"–news·newspapers·books·scholar·JSTOR(July 2010)(Learn how and when to remove this message) |
| --- | --- |

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/5/58/Hash_table_4_1_1_0_0_1_0_LL.svg/250px-Hash_table_4_1_1_0_0_1_0_LL.svg.png)](./File:Hash_table_4_1_1_0_0_1_0_LL.svg)A hash function that maps names to integers from 0 to 15. There is a [collision](./Hash_collision) between keys "John Smith" and "Sandra Dee". 

A **hash function** is any [function](./Function_(mathematics)) that can be used to map [data](./Digital_data) of arbitrary size to fixed-size values, though there are some hash functions that support variable-length output.[[1]](./Hash_function#cite_note-1) The values returned by a hash function are called *hash values*, *hash codes*, (*hash/message*) *digests*,[[2]](./Hash_function#cite_note-2) or simply *hashes*.  The values are usually used to index a fixed-size table called a *[hash table](./Hash_table)*. Use of a hash function to index a hash table is called *hashing* or *scatter-storage addressing*.

 

Hash functions and their associated hash tables are used in data storage and retrieval applications to access data in a small and nearly constant time per retrieval. They require an amount of storage space only fractionally greater than the total space required for the data or records themselves. Hashing is a way to access data quickly and efficiently. Unlike lists or trees, it provides near-constant access time. It also uses much less storage than trying to store all possible keys directly, especially when keys are large or variable in length.

 

Use of hash functions relies on statistical properties of key and function interaction: worst-case behavior is intolerably bad but rare, and average-case behavior can be nearly optimal (minimal [collision](./Hash_collision)).[[3]](./Hash_function#cite_note-knuth-1973-3): 527 

 

Hash functions are related to (and often confused with) [checksums](./Checksums), [check digits](./Check_digit), [fingerprints](./Fingerprint_(computing)), [lossy compression](./Lossy_compression), [randomization functions](./Randomization_function), [error-correcting codes](./Error_correction_code), and [ciphers](./Cipher). Although the concepts overlap to some extent, each one has its own uses and requirements and is designed and optimized differently. The hash function differs from these concepts mainly in terms of [data integrity](./Data_integrity). Hash tables may use [non-cryptographic hash functions](./Non-cryptographic_hash_function), while [cryptographic hash functions](./Cryptographic_hash_function) are used in cybersecurity to secure sensitive data such as passwords.

 

## Overview

 
|  | This sectiondoes notciteanysources.Please helpimprove this sectionbyadding citations to reliable sources. Unsourced material may be challenged andremoved.(March 2026)(Learn how and when to remove this message) |
| --- | --- |

 

In a hash table, a hash function takes a key as an input, which is associated with a datum or record and used to identify it to the data storage and retrieval application. The keys may be fixed-length, like an integer, or variable-length, like a name.  In some cases, the key is the datum itself.  The output is a hash code used to index a hash table holding the data or records, or pointers to them.

 

A hash function may be considered to perform three functions:

 
- Convert variable-length keys into fixed-length (usually [machine-word](./Machine_word)-length or less) values, by folding them by words or other units using a [parity-preserving operator](./Parity_function) like ADD or XOR,
- Scramble the bits of the key so that the resulting values are uniformly distributed over the [keyspace](./Key_space_(cryptography)), and
- Map the key values into ones less than or equal to the size of the table.

 

A good hash function satisfies two basic properties: it should be very fast to compute, and it should minimize duplication of output values ([collisions](./Hash_collision)).  Hash functions rely on generating favorable [probability distributions](./Probability_distribution) for their effectiveness, reducing access time to nearly constant.  High table loading factors, [pathological](./Pathological_(mathematics)) key sets, and poorly designed hash functions can result in access times approaching linear in the number of items in the table. Hash functions can be designed to give the best worst-case performance,[[Notes 1]](./Hash_function#cite_note-4) good performance under high table loading factors, and in special cases, perfect (collisionless) mapping of keys into hash codes. Implementation is based on parity-preserving bit operations (XOR and ADD), multiply, or divide. A necessary adjunct to the hash function is a collision-resolution method that employs an auxiliary data structure like [linked lists](./Linked_list), or systematic probing of the table to find an empty slot.

 

## Hash tables

 Main article: [Hash table](./Hash_table) 

Hash functions are used in conjunction with [hash tables](./Hash_tables) to store and retrieve data items or data records. The hash function translates the key associated with each datum or record into a hash code, which is used to index the hash table. When an item is to be added to the table, the hash code may index an empty slot (also called a bucket), in which case the item is added to the table there.  If the hash code indexes a full slot, then some kind of collision resolution is required: the new item may be omitted (not added to the table), or replace the old item, or be added to the table in some other location by a specified procedure.  That procedure depends on the structure of the hash table.  In *chained hashing*, each slot is the head of a linked list or chain, and items that collide at the slot are added to the chain.  Chains may be kept in random order and searched linearly, or in serial order, or as a self-ordering list by frequency to speed up access.  In *open address hashing*, the table is probed starting from the occupied slot in a specified manner, usually by [linear probing](./Linear_probing), [quadratic probing](./Quadratic_probing), or [double hashing](./Double_hashing) until an open slot is located or the entire table is probed (overflow).  Searching for the item follows the same procedure until the item is located, an open slot is found, or the entire table has been searched (item not in table).

 

### Specialized uses

 

Hash functions are also used to build [caches](./Cache_(computing)) for large data sets stored in slow media. A cache is generally simpler than a hashed search table, since any collision can be resolved by discarding or writing back the older of the two colliding items.[[4]](./Hash_function#cite_note-5)

 

Hash functions are an essential ingredient of the [Bloom filter](./Bloom_filter), a space-efficient [probabilistic](./Probability) [data structure](./Data_structure) that is used to test whether an [element](./Element_(mathematics)) is a member of a [set](./Set_(computer_science)).

 

A special case of hashing  is known as [geometric hashing](./Geometric_hashing) or the *grid method*. In these applications, the set of all inputs is some sort of [metric space](./Metric_space), and the hashing function can be interpreted as a [partition](./Partition_(mathematics)) of that space into a grid of *cells*. The table is often an array with two or more indices (called a *[grid file](./Grid_file)*, *grid index*, *bucket grid*, and similar names), and the hash function returns an index [tuple](./Tuple).  This principle is widely used in [computer graphics](./Computer_graphics), [computational geometry](./Computational_geometry), and many other disciplines, to solve many [proximity problems](./Proximity_problem) in the [plane](./Plane_(geometry)) or in [three-dimensional space](./Three-dimensional_space), such as finding [closest pairs](./Closest_pair_problem) in a set of points, similar shapes in a list of shapes, similar [images](./Image_processing) in an [image database](./Image_retrieval), and so on.

 

Hash tables are also used to implement [associative arrays](./Associative_array) and [dynamic sets](./Set_(abstract_data_type)).[[5]](./Hash_function#cite_note-handbook_of_applied_cryptography-6)

 

## Properties

 
|  | This sectionneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sourcesin this section. Unsourced material may be challenged and removed.Find sources:"Hash function"–news·newspapers·books·scholar·JSTOR(October 2017)(Learn how and when to remove this message) |
| --- | --- |

 

### Uniformity

 

A good hash function should map the expected inputs as evenly as possible over its output range. That is, every hash value in the output range should be generated with roughly the same [probability](./Probability). The reason for this requirement is that the cost of hashing-based methods goes up sharply as the number of *collisions* — pairs of inputs that are mapped to the same hash value — increases.  If some hash values are more likely to occur than others, then a larger fraction of the lookup operations will have to search through a larger set of colliding table entries.

 

This criterion only requires the value to be *uniformly distributed*, not *random* in any sense. A good randomizing function is (barring computational efficiency concerns) generally a good choice as a hash function, but the converse need not be true.

 

Hash tables often contain only a small subset of the valid inputs. For instance, a club membership list may contain only a hundred or so member names, out of the very large set of all possible names. In these cases, the uniformity criterion should hold for almost all typical subsets of entries that may be found in the table, not just for the global set of all possible entries.

 

In other words, if a typical set of *m* records is hashed to *n* table slots, then the probability of a bucket receiving many more than *m*/*n* records should be vanishingly small. In particular, if *m* < *n*, then very few buckets should have more than one or two records.  A small number of collisions is virtually inevitable, even if *n* is much larger than *m*—see the [birthday problem](./Birthday_problem).

 

In special cases when the keys are known in advance and the key set is static, a hash function can be found that achieves absolute (or collisionless) uniformity.  Such a hash function is said to be *[perfect](./Perfect_hash_function)*.  There is no algorithmic way of constructing such a function—searching for one is a [factorial](./Factorial) function of the number of keys to be mapped versus the number of table slots that they are mapped into.  Finding a perfect hash function over more than a very small set of keys is usually computationally infeasible; the resulting function is likely to be more computationally complex than a standard hash function and provides only a marginal advantage over a function with good statistical properties that yields a minimum number of collisions. See [universal hash function](./Universal_hashing).

 

### Testing and measurement

 

When testing a hash function, the uniformity of the distribution of hash values can be evaluated by the [chi-squared test](./Chi-squared_test).   This test is a goodness-of-fit measure: it is the actual distribution of items in buckets versus the expected (or uniform) distribution of items. The formula is

 

        ∑ ∑   j = 0   m − −  1   (  b  j   ) (  b  j   + 1 )  /  2   ( n  /  2 m ) ( n + 2 m − −  1 )    ,   {\displaystyle {\frac {\sum _{j=0}^{m-1}(b_{j})(b_{j}+1)/2}{(n/2m)(n+2m-1)}},}  ![{\displaystyle {\frac {\sum _{j=0}^{m-1}(b_{j})(b_{j}+1)/2}{(n/2m)(n+2m-1)}},}](https://wikimedia.org/api/rest_v1/media/math/render/svg/20683f81d6348d2f2448b18ea4bf80d06242cff8)[*[dubious](./Wikipedia:Accuracy_dispute#Disputed_statement) – [discuss](./Talk:Hash_function#Dubious)*][*[citation needed](./Wikipedia:Citation_needed)*]

 

where n is the number of keys, m is the number of buckets, and *b**j* is the number of items in bucket j.

 

A ratio within one [confidence interval](./Confidence_interval) (such as 0.95 to 1.05) is indicative that the hash function evaluated has an expected uniform distribution.

 

Hash functions can have some technical properties that make it more likely that they will have a uniform distribution when applied.  One is the [strict avalanche criterion](./Strict_avalanche_criterion): whenever a single input bit is complemented, each of the output bits changes with a 50% probability.  The reason for this property is that selected subsets of the keyspace may have low variability.  For the output to be uniformly distributed, a low amount of variability, even one bit, should translate into a high amount of variability (i.e. distribution over the tablespace) in the output.  Each bit should change with a probability of 50% because, if some bits are reluctant to change, then the keys become clustered around those values.  If the bits want to change too readily, then the mapping is approaching a fixed XOR function of a single bit.  Standard tests for this property have been described in the literature.[[6]](./Hash_function#cite_note-7)  The relevance of the criterion to a multiplicative hash function is assessed here.[[7]](./Hash_function#cite_note-fibonacci-hashing-8)

 

### Efficiency

 

In data storage and retrieval applications, the use of a hash function is a trade-off between search time and data storage space.  If search time were unbounded, then a very compact unordered linear list would be the best medium; if storage space were unbounded, then a randomly accessible structure indexable by the key-value would be very large and very sparse, but very fast.  A hash function takes a finite amount of time to map a potentially large keyspace to a feasible amount of storage space searchable in a bounded amount of time regardless of the number of keys.  In most applications, the hash function should be computable with minimum latency and secondarily in a minimum number of instructions.

 

Computational complexity varies with the number of instructions required and latency of individual instructions, with the simplest being the bitwise methods (folding), followed by the multiplicative methods, and the most complex (slowest) are the division-based methods.

 

Because collisions should be infrequent, and cause a marginal delay but are otherwise harmless, it is usually preferable to choose a faster hash function over one that needs more computation but saves a few collisions.

 

Division-based implementations can be of particular concern because a division requires multiple cycles on nearly all processor [microarchitectures](./Microarchitecture).  Division ([modulo](./Modulo_operation)) by a constant can be inverted to become a multiplication by the word-size multiplicative-inverse of that constant.  This can be done by the programmer, or by the [compiler](./Compiler).  Division can also be reduced directly into a series of shift-subtracts and shift-adds, though minimizing the number of such operations required is a daunting problem; the number of machine-language instructions resulting may be more than a dozen and swamp the pipeline.  If the microarchitecture has [hardware multiply](./Hardware_multiply) [functional units](./Functional_unit), then the multiply-by-inverse is likely a better approach.

 

We can allow the table size *n* to not be a power of 2 and still not have to perform any remainder or division operation, as these computations are sometimes costly. For example, let *n* be significantly less than 2*b*. Consider a [pseudorandom number generator](./Pseudorandom_number_generator) function *P*(key) that is uniform on the interval [0, 2*b* − 1]. A hash function uniform on the interval [0, *n* − 1] is *n* *P*(key) / 2*b*. We can replace the division by a (possibly faster) right [bit shift](./Bit_shifting): *n P*(key) >> *b*.

 

If keys are being hashed repeatedly, and the hash function is costly, then computing time can be saved by precomputing the hash codes and storing them with the keys.  Matching hash codes almost certainly means that the keys are identical.  This technique is used for the transposition table in game-playing programs, which stores a 64-bit hashed representation of the board position.

 

### Universality

 Main article: [Universal hashing](./Universal_hashing) 

A *universal hashing* scheme is a [randomized algorithm](./Randomized_algorithm) that selects a hash function *h* among a family of such functions, in such a way that the probability of a collision of any two distinct keys is 1/*m*, where *m* is the number of distinct hash values desired—independently of the two keys. Universal hashing ensures (in a probabilistic sense) that the hash [function application](./Function_application) will behave as well as if it were using a random function, for any distribution of the input data. It will, however, have more collisions than perfect hashing and may require more operations than a special-purpose hash function.

 

### Applicability

 

A hash function that allows only certain table sizes or strings only up to a certain length, or cannot accept a seed (i.e. allow double hashing) is less useful than one that does.[*[citation needed](./Wikipedia:Citation_needed)*]

 

A hash function is applicable in a variety of situations. Particularly within cryptography, notable applications include:[[8]](./Hash_function#cite_note-9)

 
- [Integrity checking](./File_verification): Identical hash values for different files imply equality, providing a reliable means to detect file modifications.
- [Key derivation](./Key_derivation_function): Minor input changes result in a random-looking output alteration, known as the diffusion property. Thus, hash functions are valuable for key derivation functions.
- [Message authentication codes](./Message_authentication_code) (MACs): Through the integration of a confidential key with the input data, hash functions can generate MACs ensuring the genuineness of the data, such as in [HMACs](./HMAC).
- Password storage: The password's hash value does not expose any password details, emphasizing the importance of securely storing hashed passwords on the server.
- [Signatures](./Digital_signature): Message hashes are signed rather than the whole message.

 

### Deterministic

 

A hash procedure must be [deterministic](./Deterministic_algorithm)—for a given input value, it must always generate the same hash value. In other words, it must be a [function](./Function_(mathematics)) of the data to be hashed, in the mathematical sense of the term. This requirement excludes hash functions that depend on external variable parameters, such as [pseudo-random number generators](./Pseudo-random_number_generator) or the time of day. It also excludes functions that depend on the [memory address](./Memory_address) of the object being hashed, because the address may change during execution (as may happen on systems that use certain methods of [garbage collection](./Garbage_collection_(computer_science))), although sometimes rehashing of the item is possible.

 

The determinism is in the context of the reuse of the function. For example, [Python](./Python_(programming_language)) adds the feature that hash functions make use of a randomized seed that is generated once when the Python process starts in addition to the input to be hashed.[[9]](./Hash_function#cite_note-10) The Python hash ([SipHash](./SipHash)) is still a valid hash function when used within a single run, but if the values are persisted (for example, written to disk), they can no longer be treated as valid hash values, since in the next run the random value might differ.

 

### Defined range

 

It is often desirable that the output of a hash function have fixed size (but see below). If, for example, the output is constrained to 32-bit integer values, then the hash values can be used to index into an array. Such hashing is commonly used to accelerate data searches.[[10]](./Hash_function#cite_note-algorithms_in_java-11) Producing fixed-length output from variable-length input can be accomplished by breaking the input data into chunks of specific size. Hash functions used for data searches use some arithmetic expression that iteratively processes chunks of the input (such as the characters in a string) to produce the hash value.[[10]](./Hash_function#cite_note-algorithms_in_java-11)

 

### Variable range

 

In many applications, the range of hash values may be different for each run of the program or may change along the same run (for instance, when a hash table needs to be expanded). In those situations, one needs a hash function which takes two parameters—the input data *z*, and the number *n* of allowed hash values.

 

A common solution is to compute a fixed hash function with a very large range (say, 0 to 232 − 1), divide the result by *n*, and use the division's [remainder](./Modulo_operation). If *n* is itself a power of 2, this can be done by [bit masking](./Mask_(computing)) and [bit shifting](./Bit_shifting). When this approach is used, the hash function must be chosen so that the result has fairly uniform distribution between 0 and *n* − 1, for any value of *n* that may occur in the application. Depending on the function, the remainder may be uniform only for certain values of *n*, e.g. [odd](./Odd_number) or [prime numbers](./Prime_number).

 

### Variable range with minimal movement (dynamic hash function)

 

When the hash function is used to store values in a hash table that outlives the run of the program, and the hash table needs to be expanded or shrunk, the hash table is referred to as a dynamic hash table.

 

A hash function that will relocate the minimum number of records when the table is resized is desirable. What is needed is a hash function *H*(*z*,*n*) (where *z* is the key being hashed and *n* is the number of allowed hash values) such that *H*(*z*,*n* + 1) = *H*(*z*,*n*) with probability close to *n*/(*n* + 1).

 

[Linear hashing](./Linear_hashing) and [spiral hashing](./Spiral_hashing) are examples of dynamic hash functions that execute in constant time but relax the property of uniformity to achieve the minimal movement property. [Extendible hashing](./Extendible_hashing) uses a dynamic hash function that requires space proportional to *n* to compute the hash function, and it becomes a function of the previous keys that have been inserted. Several algorithms that preserve the uniformity property but require time proportional to *n* to compute the value of *H*(*z*,*n*) have been invented.[*[clarification needed](./Wikipedia:Please_clarify)*]

 

A hash function with minimal movement is especially useful in [distributed hash tables](./Distributed_hash_table).

 

### Data normalization

 

In some applications, the input data may contain features that are irrelevant for comparison purposes. For example, when looking up a personal name, it may be desirable to ignore the distinction between upper and lower case letters. For such data, one must use a hash function that is compatible with the data [equivalence](./Equivalence_relation) criterion being used: that is, any two inputs that are considered equivalent must yield the same hash value. This can be accomplished by normalizing the input before hashing it, as by upper-casing all letters.

 

## Hashing integer data types

 

There are several common algorithms for hashing integers.  The method giving the best distribution is data-dependent.  One of the simplest and most common methods in practice is the modulo division method.

 

### Identity hash function

 

If the data to be hashed is small enough, then one can use the data itself (reinterpreted as an integer) as the hashed value. The cost of computing this *[identity](./Identity_function)* hash function is effectively zero. This hash function is [perfect](./Perfect_hash_function), as it maps each input to a distinct hash value.

 

The meaning of "small enough" depends on the size of the type that is used as the hashed value. For example, in [Java](./Java_(programming_language)), the hash code is a 32-bit integer. Thus the 32-bit integer `Integer` and 32-bit floating-point `Float` objects can simply use the value directly, whereas the 64-bit integer `Long` and 64-bit floating-point `Double` cannot.

 

Other types of data can also use this hashing scheme. For example, when mapping [character strings](./Character_string) between [upper and lower case](./Letter_case), one can use the binary encoding of each character, interpreted as an integer, to index a table that gives the alternative form of that character ("A" for "a", "8" for "8", etc.).  If each character is stored in 8 bits (as in [extended ASCII](./Extended_ASCII)[[Notes 2]](./Hash_function#cite_note-12) or [ISO Latin 1](./ISO_Latin_1)), the table has only 28 = 256 entries; in the case of [Unicode](./Unicode) characters, the table would have 17 × 216 = 1114112 entries.

 

The same technique can be used to map [two-letter country codes](./ISO_3166-1_alpha-2) like "us" or "za" to country names (262 = 676 table entries), 5-digit [ZIP codes](./ZIP_Code) like 13083 to city names (100000 entries), etc. Invalid data values (such as the country code "xx" or the ZIP code 00000) may be left undefined in the table or mapped to some appropriate "null" value.

 

### Trivial hash function

 

If the keys are uniformly or sufficiently uniformly distributed over the key space, so that the key values are essentially random, then they may be considered to be already "hashed". In this case, any number of any bits in the key may be extracted and collated as an index into the hash table. For example, a simple hash function might mask off the m least significant bits and use the result as an index into a hash table of size 2*m*.

 

### Mid-squares

 

A mid-squares hash code is produced by squaring the input and extracting an appropriate number of middle digits or bits.  For example, if the input is 123456789 and the hash table size 10000, then squaring the key produces 15241578750190521, so the hash code is taken as the middle 4 digits of the 17-digit number (ignoring the high digit) 8750.  The mid-squares method produces a reasonable hash code if there is not a lot of leading or trailing zeros in the key.  This is a variant of multiplicative hashing, but not as good because an arbitrary key is not a good multiplier.

 

### Division hashing

 

A standard technique is to use a modulo function on the key, by selecting a divisor M which is a prime number close to the table size, so *h*(*K*) ≡ *K* (mod *M*). The table size is usually a power of 2.  This gives a distribution from {0, *M* − 1}.  This gives good results over a large number of key sets.  A significant drawback of division hashing is that division requires multiple cycles on most modern architectures (including [x86](./X86)) and can be 10 times slower than multiplication. A second drawback is that it will not break up clustered keys. For example, the keys 123000, 456000, 789000, etc. modulo 1000 all map to the same address.  This technique works well in practice because many key sets are sufficiently random already, and the probability that a key set will be cyclical by a large prime number is small.

 

### Algebraic coding

 

Algebraic coding is a variant of the division method of hashing which uses division by a polynomial modulo 2 instead of an integer to map n bits to m bits.[[3]](./Hash_function#cite_note-knuth-1973-3): 512–513  In this approach, *M* = 2*m*, and we postulate an mth-degree polynomial *Z*(*x*) = *x**m* + ζ*m*−1*x**m*−1 + ⋯ + ζ0.  A key *K* = (*k**n*−1…*k*1*k*0)2 can be regarded as the polynomial *K*(*x*) = *k**n*−1*x**n*−1 + ⋯ + *k*1*x* + *k*0. The remainder using polynomial arithmetic modulo 2 is *K*(*x*) mod *Z*(*x*) = *h**m*−1*x**m*−1 + ⋯ *h*1*x* + *h*0. Then *h*(*K*) = (*h**m*−1…*h*1*h*0)2. If *Z*(*x*) is constructed to have t or fewer non-zero coefficients, then keys which share fewer than t bits are guaranteed to not collide.

 

Z is a function of k, t, and n (the last of which is a divisor of 2*k* − 1) and is constructed from the [finite field](./Finite_field) GF(2*k*).  [Knuth](./Donald_Knuth) gives an example: taking (*n*,*m*,*t*) = (15,10,7) yields *Z*(*x*) = *x*10 + *x*8 + *x*5 + *x*4 + *x*2 + *x* + 1. The derivation is as follows:

 

Let S be the smallest set of integers such that {1,2,…,*t*} ⊆ *S* and (2*j* mod *n*) ∈ *S* ∀*j* ∈ *S*.[[Notes 3]](./Hash_function#cite_note-13)

 

Define     P ( x ) =  ∏ ∏   j ∈ ∈  S   ( x − −   α α   j   )   {\displaystyle P(x)=\prod _{j\in S}(x-\alpha ^{j})}  ![{\displaystyle P(x)=\prod _{j\in S}(x-\alpha ^{j})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8ec503eae00278775be2b42f7e2b873f8c6fb063) where α ∈*n* GF(2*k*) and where the coefficients of *P*(*x*) are computed in this field.  Then the degree of *P*(*x*) = |*S*|. Since α2*j* is a root of *P*(*x*) whenever α*j* is a root, it follows that the coefficients *pi* of *P*(*x*) satisfy *p*2
*i* = *p*i, so they are all 0 or 1. If *R*(*x*) = *r**n*−1*x**n*−1 + ⋯ + *r*1*x* + *r*0 is any nonzero polynomial modulo 2 with at most t nonzero coefficients, then *R*(*x*) is not a multiple of *P*(*x*) modulo 2.[[Notes 4]](./Hash_function#cite_note-14)  If follows that the corresponding hash function will map keys with fewer than t bits in common to unique indices.[[3]](./Hash_function#cite_note-knuth-1973-3): 542–543 

 

The usual outcome is that either n will get large, or t will get large, or both, for the scheme to be computationally feasible.  Therefore, it is more suited to hardware or microcode implementation.[[3]](./Hash_function#cite_note-knuth-1973-3): 542–543 

 

### Unique permutation hashing

 

Unique permutation hashing has a guaranteed best worst-case insertion time.[[11]](./Hash_function#cite_note-15)

 

### Multiplicative hashing

 

Standard multiplicative hashing uses the formula *h**a*(*K*) = ⌊(*aK* mod *W*) / (*W*/*M*)⌋, which produces a hash value in {0, …, *M* − 1}.  The value a is an appropriately chosen value that should be [relatively prime](./Coprime_integers) to W; it should be large,[*[clarification needed](./Wikipedia:Please_clarify)*] and its binary representation a random mix[*[clarification needed](./Wikipedia:Please_clarify)*] of 1s and 0s.   An important practical special case occurs when *W* = 2*w* and *M* = 2*m* are powers of 2 and w is the machine [word size](./Word_size). In this case, this formula becomes *h**a*(*K*) = ⌊(*aK* mod 2*w*) / 2*w*−*m*⌋.  This is special because arithmetic modulo 2*w* is done by default in low-level programming languages and integer division by a power of 2 is simply a right-shift, so, in [C](./C_(programming_language)), for example, this function becomes

 
```
unsigned hash(unsigned K) { 
    return (a * K) >> (w - m);
}

```
 

and for fixed m and w this translates into a single integer multiplication and right-shift, making it one of the fastest hash functions to compute.

 

Multiplicative hashing is susceptible to a "common mistake" that leads to poor diffusion—higher-value input bits do not affect lower-value output bits.[[12]](./Hash_function#cite_note-16)  A transmutation on the input which shifts the span of retained top bits down and XORs or ADDs them to the key before the multiplication step corrects for this. The resulting function looks like:[[7]](./Hash_function#cite_note-fibonacci-hashing-8)

 
```
unsigned hash(unsigned K) {
    K ^= K >> (w - m); 
    return (a * K) >> (w - m);
}

```
 

### Fibonacci hashing

 

[Fibonacci](./Fibonacci_number) hashing is a form of multiplicative hashing in which the multiplier is 2*w* / ϕ, where w is the machine word length and ϕ (phi) is the [golden ratio](./Golden_ratio) (approximately 1.618). A property of this multiplier is that it uniformly distributes over the table space, [blocks](./Blockchain) of consecutive keys with respect to any block of bits in the key.  Consecutive keys within the high bits or low bits of the key (or some other field) are relatively common.  The multipliers for various word lengths are:

 
- 16:  *a* = 9E3716 = 4050310
- 32:  *a* = 9E3779B916 = 265443576910
- 48:  *a* = 9E3779B97F4B16 = 17396110258977110[[Notes 5]](./Hash_function#cite_note-17)
- 64:  *a* = 9E3779B97F4A7C1516 = 1140071481932319848510

  

The multiplier should be odd, so the least significant bit of the output is invertible modulo 2*w*.  The last two values given above are rounded (up and down, respectively) by more than 1/2 of a least-significant bit to achieve this.

 

### Zobrist hashing

 Main articles: [Tabulation hashing](./Tabulation_hashing) and [Zobrist hashing](./Zobrist_hashing) 

*Zobrist hashing*, named after [Albert Zobrist](./Albert_Lindsey_Zobrist), is a form of [tabulation hashing](./Tabulation_hashing), which is a method for constructing universal families of hash functions by combining table lookup with XOR operations. This algorithm has proven to be very fast and of high quality for hashing purposes (especially hashing of integer-number keys).[[13]](./Hash_function#cite_note-18)

 

Zobrist hashing was originally introduced as a means of compactly representing chess positions in computer game-playing programs.  A unique random number was assigned to represent each type of piece (six each for black and white) on each space of the board.  Thus a table of 64×12 such numbers is initialized at the start of the program.  The random numbers could be any length, but 64 bits was natural due to the 64 squares on the board.  A position was transcribed by cycling through the pieces in a position, indexing the corresponding random numbers (vacant spaces were not included in the calculation) and XORing them together (the starting value could be 0 (the identity value for XOR) or a [random seed](./Random_seed)).  The resulting value was reduced by modulo, folding, or some other operation to produce a hash table index.  The original Zobrist hash was stored in the table as the representation of the position.

 

Later, the method was extended to hashing integers by representing each byte in each of 4 possible positions in the word by a unique 32-bit random number.  Thus, a table of 28×4 random numbers is constructed. A 32-bit hashed integer is transcribed by successively indexing the table with the value of each byte of the plain text integer and XORing the loaded values together (again, the starting value can be the identity value or a random seed). The natural extension to 64-bit integers is by use of a table of 28×8 64-bit random numbers.

 

This kind of function has some nice theoretical properties, one of which is called *3-tuple independence*, meaning that every 3-tuple of keys is equally likely to be mapped to any 3-tuple of hash values.

 

### Customized hash function

 

A hash function can be designed to exploit existing entropy in the keys.  If the keys have leading or trailing zeros, or particular fields that are unused, always zero or some other constant, or generally vary little, then masking out only the volatile bits and hashing on those will provide a better and possibly faster hash function.  Selected divisors or multipliers in the division and multiplicative schemes may make more uniform hash functions if the keys are cyclic or have other redundancies.

 

## Hashing variable-length data

 

When the data values are long (or variable-length) [character strings](./Character_string)—such as personal names, [web page addresses](./URL), or mail messages—their distribution is usually very uneven, with complicated dependencies. For example, text in any [natural language](./Natural_language) has highly non-uniform distributions of [characters](./Character_(computing)), and [character pairs](./Digraph_(computing)), characteristic of the language. For such data, it is prudent to use a hash function that depends on all characters of the string—and depends on each character in a different way.[*[clarification needed](./Wikipedia:Please_clarify)*]

 

### Middle and ends

 

Simplistic hash functions may add the first and last *n* characters of a string along with the length, or form a word-size hash from the middle 4 characters of a string.  This saves iterating over the (potentially long) string, but hash functions that do not hash on all characters of a string can readily become linear due to redundancies, clustering, or other pathologies in the key set.  Such strategies may be effective as a custom hash function if the structure of the keys is such that either the middle, ends, or other fields are zero or some other invariant constant that does not differentiate the keys; then the invariant parts of the keys can be ignored.

 

### Character folding

 

The paradigmatic example of folding by characters is to add up the integer values of all the characters in the string.   A better idea is to multiply the hash total by a constant, typically a sizable prime number, before adding in the next character, ignoring overflow.  Using exclusive-or instead of addition is also a plausible alternative. The final operation would be a modulo, mask, or other function to reduce the word value to an index the size of the table. The weakness of this procedure is that information may cluster in the upper or lower bits of the bytes; this clustering will remain in the hashed result and cause more collisions than a proper randomizing hash. ASCII byte codes, for example, have an upper bit of 0, and printable strings do not use the last byte code or most of the first 32 byte codes, so the information, which uses the remaining byte codes, is clustered in the remaining bits in an unobvious manner.

 

The classic approach, dubbed the [PJW hash](./PJW_hash_function) based on the work of [Peter J. Weinberger](./Peter_J._Weinberger) at [Bell Labs](./Bell_Labs) in the 1970s, was originally designed for hashing identifiers into compiler symbol tables as given in the ["Dragon Book"](./Compilers:_Principles,_Techniques,_and_Tools).[[14]](./Hash_function#cite_note-19) This hash function offsets the bytes 4 bits before adding them together.  When the quantity wraps, the high 4 bits are shifted out and if non-zero, [xored](./Exclusive_or) back into the low byte of the cumulative quantity.  The result is a word-size hash code to which a modulo or other reducing operation can be applied to produce the final hash index.

 

Today, especially with the advent of 64-bit word sizes, much more efficient variable-length string hashing by word chunks is available.

 

### Word length folding

 See also: [Universal hashing § Hashing strings](./Universal_hashing#Hashing_strings) 

Modern microprocessors will allow for much faster processing if 8-bit character strings are not hashed by processing one character at a time, but by interpreting the string as an array of 32-bit or 64-bit integers and hashing/accumulating these "wide word" integer values by means of arithmetic operations (e.g. multiplication by constant and bit-shifting). The final word, which may have unoccupied byte positions, is filled with zeros or a specified randomizing value before being folded into the hash.  The accumulated hash code is reduced by a final modulo or other operation to yield an index into the table.

 

### Radix conversion hashing

 

Analogous to the way an ASCII or [EBCDIC](./EBCDIC) character string representing a decimal number is converted to a numeric quantity for computing, a variable-length string can be converted as *x**k*−1a*k*−1 + *x**k*−2a*k*−2 + ⋯ + *x*1*a* + *x*0. This is simply a polynomial in a [radix](./Radix) *a* > 1 that takes the components (*x*0,*x*1,...,*x**k*−1) as the characters of the input string of length *k*. It can be used directly as the hash code, or a hash function applied to it to map the potentially large value to the hash table size. The value of *a* is usually a prime number large enough to hold the number of different characters in the character set of potential keys. Radix conversion hashing of strings minimizes the number of collisions.[[15]](./Hash_function#cite_note-20) Available data sizes may restrict the maximum length of string that can be hashed with this method.  For example, a 128-bit word will hash only a 26-character alphabetic string (ignoring case) with a radix of 29; a printable ASCII string is limited to 9 characters using radix 97 and a 64-bit word.  However, alphabetic keys are usually of modest length, because keys must be stored in the hash table. Numeric character strings are usually not a problem; 64 bits can count up to 1019, or 19 decimal digits with radix 10.

 

### Rolling hash

 Main article: [Rolling hash](./Rolling_hash) See also: [Linear congruential generator](./Linear_congruential_generator) 

In some applications, such as [substring search](./String_searching_algorithm), one can compute a hash function *h* for every *k*-character [substring](./Substring) of a given *n*-character string by advancing a window of width *k* characters along the string, where  *k* is a fixed integer, and *n* > *k*. The straightforward solution, which is to extract such a substring at every character position in the text and compute *h* separately, requires a number of operations proportional to *k*·*n*. However, with the proper choice of *h*, one can use the technique of rolling hash to compute all those hashes with an effort proportional to *mk* + *n* where *m* is the number of occurrences of the substring.[[16]](./Hash_function#cite_note-21)[*[what is the choice of h?](./Wikipedia:Cleanup)*]

 

The most familiar algorithm of this type is [Rabin-Karp](./Rabin-Karp) with best and average case performance *O*(*n*+*mk*) and worst case *O*(*n*·*k*) (in all fairness, the worst case here is gravely pathological: both the text string and substring are composed of a repeated single character, such as *t*="AAAAAAAAAAA", and *s*="AAA").  The hash function used for the algorithm is usually the [Rabin fingerprint](./Rabin_fingerprint), designed to avoid collisions in 8-bit character strings, but other suitable hash functions are also used.

 

### Fuzzy hash

 This section is an excerpt from [Fuzzy hashing](./Fuzzy_hashing).[[edit](https://en.wikipedia.org/w/index.php?title=Fuzzy_hashing&action=edit)] 

[Fuzzy hashing](./Fuzzy_hashing), also known as similarity hashing,[[17]](./Hash_function#cite_note-Fuzzy_hashing_NIST.SP.800-168-22) is a technique for [detecting data that is similar](./Content_similarity_detection), but not exactly the same, as other data. This is in contrast to [cryptographic hash functions](./Cryptographic_hash_function), which are designed to have significantly different hashes for even minor differences. Fuzzy hashing has been used to identify malware[[18]](./Hash_function#cite_note-Fuzzy_hashing_Beyond_Precision_and_Recall:_Understanding_Uses_(and_Misuses)_of_Similarity_Hashes_in_Binary_Analysis-23)[[19]](./Hash_function#cite_note-Fuzzy_hashing_Forensic_Malware_Analysis:_The_Value_of_Fuzzy_Hashing_Algorithms_in_Identifying_Similarities-24) and has potential for other applications, like [data loss prevention](./Data_loss_prevention) and detecting multiple versions of code.[[20]](./Hash_function#cite_note-Fuzzy_hashing_ssdeep-25)[[21]](./Hash_function#cite_note-Fuzzy_hashing_tlsh-26)

   

### Perceptual hash

 This section is an excerpt from [Perceptual hashing](./Perceptual_hashing).[[edit](https://en.wikipedia.org/w/index.php?title=Perceptual_hashing&action=edit)] 

[Perceptual hashing](./Perceptual_hashing) is the use of a [fingerprinting algorithm](./Fingerprint_(computing)) that produces a snippet,  hash, or [fingerprint](./Fingerprint_(computing)) of various forms of [multimedia](./Multimedia).[[22]](./Hash_function#cite_note-Perceptual_hashing_buldas13-27)[[23]](./Hash_function#cite_note-Perceptual_hashing_klinger-28) A perceptual hash is a type of [locality-sensitive hash](./Locality-sensitive_hash), which is analogous if [features](./Feature_vector) of the multimedia are similar. This is in contrast to [cryptographic hashing](./Cryptographic_hash_function), which relies on the [avalanche effect](./Avalanche_effect) of a small change in input value creating a drastic change in output value. Perceptual hash functions are widely used in finding cases of online [copyright infringement](./Copyright_infringement) as well as in [digital forensics](./Digital_Forensics_Framework) because of the ability to have a correlation between hashes so similar data can be found (for instance with a differing [watermark](./Digital_watermark)).

   

## Analysis

 

Worst case results for a hash function can be assessed two ways: theoretical and practical. The theoretical worst case is the probability that all keys map to a single slot.  The practical worst case is the expected longest probe sequence (hash function + collision resolution method).  This analysis considers uniform hashing, that is, any key will map to any particular slot with probability 1/*m*, a characteristic of universal hash functions.

 

While [Knuth](./Donald_Knuth) worries about adversarial attack on real time systems,[[24]](./Hash_function#cite_note-29) Gonnet has shown that the probability of such a case is "ridiculously small". His representation was that the probability of *k* of *n* keys mapping to a single slot is α*k* / (*e*α *k*!), where *α* is the load factor, *n*/*m*.[[25]](./Hash_function#cite_note-30)

 

## History

 

The term *hash* offers a natural analogy with its non-technical meaning (to chop up or make a mess out of something), given how hash functions scramble their input data to derive their output.[[26]](./Hash_function#cite_note-knuth-2000-31): 514  In his research for the precise origin of the term, [Donald Knuth](./Donald_Knuth) notes that, while [Hans Peter Luhn](./Hans_Peter_Luhn) of [IBM](./IBM) appears to have been the first to use the concept of a hash function in a memo dated January 1953, the term itself did not appear in published literature until the late 1960s, in Herbert Hellerman's *Digital Computer System Principles*, even though it was already widespread jargon by then.[[26]](./Hash_function#cite_note-knuth-2000-31): 547–548 

 

## See also

   [![Wiktionary logo](//upload.wikimedia.org/wikipedia/commons/thumb/9/99/Wiktionary-logo-en-v2.svg/40px-Wiktionary-logo-en-v2.svg.png)](./File:Wiktionary-logo-en-v2.svg) Look up ***[hash](https://en.wiktionary.org/wiki/hash)*** in Wiktionary, the free dictionary.   
- [List of hash functions](./List_of_hash_functions)
- [Nearest neighbor search](./Nearest_neighbor_search)
- [Distributed hash table](./Distributed_hash_table)
- [Identicon](./Identicon)
- [Low-discrepancy sequence](./Low-discrepancy_sequence)
- [Transposition table](./Transposition_table)

 

## Notes

  
1. [↑](./Hash_function#cite_ref-4) This is useful in cases where keys are devised by a malicious agent, for example in pursuit of a DOS attack.
2. [↑](./Hash_function#cite_ref-12) Plain [ASCII](./ASCII) is a 7-bit character encoding, although it is often stored in 8-bit bytes with the highest-order bit always clear (zero).  Therefore, for plain ASCII, the bytes have only 27 = 128 valid values, and the character translation table has only this many entries.
3. [↑](./Hash_function#cite_ref-13) For example, for n=15, k=4, t=6,     S = { 1 , 2 , 3 , 4 , 5 , 6 , 8 , 10 , 12 , 9 }   {\displaystyle S=\{1,2,3,4,5,6,8,10,12,9\}}  ![{\displaystyle S=\{1,2,3,4,5,6,8,10,12,9\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/19e42b87c2ae112644686a3cf5e4c95adfa56d9d) [Knuth]
4. [↑](./Hash_function#cite_ref-14) Knuth conveniently leaves the proof of this to the reader.
5. [↑](./Hash_function#cite_ref-17) Unisys large systems.

 

## References

  
1. [↑](./Hash_function#cite_ref-1) Aggarwal, Kirti; Verma, Harsh K. (March 19, 2015). *Hash_RC6 — Variable length Hash algorithm using RC6*. 2015 International Conference on Advances in Computer Engineering and Applications (ICACEA). [doi](./Doi_(identifier)):[10.1109/ICACEA.2015.7164747](https://doi.org/10.1109%2FICACEA.2015.7164747).
2. [↑](./Hash_function#cite_ref-2)  
- ["hash digest"](https://csrc.nist.gov/glossary/term/hash_digest). *Computer Security Resource Center - Glossary*. [NIST](./NIST).
- ["message digest"](https://csrc.nist.gov/glossary/term/message_digest). *Computer Security Resource Center - Glossary*. [NIST](./NIST).

3. [1](./Hash_function#cite_ref-knuth-1973_3-0) [2](./Hash_function#cite_ref-knuth-1973_3-1) [3](./Hash_function#cite_ref-knuth-1973_3-2) [4](./Hash_function#cite_ref-knuth-1973_3-3) [Knuth, Donald E.](./Donald_Knuth) (1973). *The Art of Computer Programming, Vol. 3, Sorting and Searching*. Reading, MA., United States: [Addison-Wesley](./Addison-Wesley). [Bibcode](./Bibcode_(identifier)):[1973acp..book.....K](https://ui.adsabs.harvard.edu/abs/1973acp..book.....K). [ISBN](./ISBN_(identifier)) [978-0-201-03803-3](./Special:BookSources/978-0-201-03803-3).
4. [↑](./Hash_function#cite_ref-5) Stokes, Jon (2002-07-08). ["Understanding CPU caching and performance"](https://arstechnica.com/gadgets/reviews/2002/07/caching.ars). *Ars Technica*. Retrieved 2022-02-06.
5. [↑](./Hash_function#cite_ref-handbook_of_applied_cryptography_6-0) Menezes, Alfred J.; van Oorschot, Paul C.; Vanstone, Scott A (1996). [*Handbook of Applied Cryptography*](https://archive.org/details/handbookofapplie0000mene). CRC Press. [ISBN](./ISBN_(identifier)) [978-0849385230](./Special:BookSources/978-0849385230).
6. [↑](./Hash_function#cite_ref-7) Castro, Julio Cesar Hernandez; et al. (3 February 2005). "The strict avalanche criterion randomness test". *Mathematics and Computers in Simulation*. **68** (1). [Elsevier](./Elsevier): 1–7. [doi](./Doi_(identifier)):[10.1016/j.matcom.2004.09.001](https://doi.org/10.1016%2Fj.matcom.2004.09.001). [S2CID](./S2CID_(identifier)) [18086276](https://api.semanticscholar.org/CorpusID:18086276).
7. [1](./Hash_function#cite_ref-fibonacci-hashing_8-0) [2](./Hash_function#cite_ref-fibonacci-hashing_8-1) Sharupke, Malte (16 June 2018). ["Fibonacci Hashing: The Optimization that the World Forgot"](https://probablydance.com/2018/06/16/fibonacci-hashing-the-optimization-that-the-world-forgot-or-a-better-alternative-to-integer-modulo/). *Probably Dance*.
8. [↑](./Hash_function#cite_ref-9) Wagner, Urs; Lugrin, Thomas (2023), Mulder, Valentin; Mermoud, Alain; Lenders, Vincent; Tellenbach, Bernhard (eds.), "Hash Functions", *Trends in Data Protection and Encryption Technologies*, Cham: Springer Nature Switzerland, pp. 21–24, [doi](./Doi_(identifier)):[10.1007/978-3-031-33386-6_5](https://doi.org/10.1007%2F978-3-031-33386-6_5), [ISBN](./ISBN_(identifier)) [978-3-031-33386-6](./Special:BookSources/978-3-031-33386-6)`{{citation}}`:  CS1 maint: work parameter with ISBN ([link](./Category:CS1_maint:_work_parameter_with_ISBN))
9. [↑](./Hash_function#cite_ref-10) ["3. Data model — Python 3.6.1 documentation"](https://docs.python.org/3/reference/datamodel.html#object.__hash__). *docs.python.org*. Retrieved 2017-03-24.
10. [1](./Hash_function#cite_ref-algorithms_in_java_11-0) [2](./Hash_function#cite_ref-algorithms_in_java_11-1) Sedgewick, Robert (2002). "14. Hashing". *Algorithms in Java* (3 ed.). Addison Wesley. [ISBN](./ISBN_(identifier)) [978-0201361209](./Special:BookSources/978-0201361209).
11. [↑](./Hash_function#cite_ref-15) Dolev, Shlomi; Lahiani, Limor; Haviv, Yinnon (2013). ["Unique permutation hashing"](https://doi.org/10.1016%2Fj.tcs.2012.12.047). *Theoretical Computer Science*. **475**: 59–65. [doi](./Doi_(identifier)):[10.1016/j.tcs.2012.12.047](https://doi.org/10.1016%2Fj.tcs.2012.12.047).
12. [↑](./Hash_function#cite_ref-16)  ["CS 3110 Lecture 21: Hash functions"](https://www.cs.cornell.edu/courses/cs3110/2008fa/lectures/lec21.html). Section "Multiplicative hashing".
13. [↑](./Hash_function#cite_ref-18) [Zobrist, Albert L.](./Albert_Lindsey_Zobrist) (April 1970), [*A New Hashing Method with Application for Game Playing*](https://www.cs.wisc.edu/techreports/1970/TR88.pdf) (PDF), Tech. Rep. 88, Madison, Wisconsin: Computer Sciences Department, University of Wisconsin.
14. [↑](./Hash_function#cite_ref-19) [Aho, A.](./Alfred_Aho); [Sethi, R.](./Ravi_Sethi); [Ullman, J. D.](./Jeffrey_Ullman) (1986). *Compilers: Principles, Techniques and Tools*. Reading, MA: [Addison-Wesley](./Addison-Wesley). p. 435. [ISBN](./ISBN_(identifier)) [0-201-10088-6](./Special:BookSources/0-201-10088-6).
15. [↑](./Hash_function#cite_ref-20) Ramakrishna, M. V.; Zobel, Justin (1997). ["Performance in Practice of String Hashing Functions"](https://citeseer.ist.psu.edu/viewdoc/download?doi=10.1.1.18.7520&rep=rep1&type=pdf). *Database Systems for Advanced Applications '97*. DASFAA 1997. pp. 215–224. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.18.7520](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.18.7520). [doi](./Doi_(identifier)):[10.1142/9789812819536_0023](https://doi.org/10.1142%2F9789812819536_0023). [ISBN](./ISBN_(identifier)) [981-02-3107-5](./Special:BookSources/981-02-3107-5). [S2CID](./S2CID_(identifier)) [8250194](https://api.semanticscholar.org/CorpusID:8250194). Retrieved 2021-12-06.
16. [↑](./Hash_function#cite_ref-21) Singh, N. B. [*A Handbook of Algorithms*](https://books.google.com/books?id=ALIMEQAAQBAJ&dq=rolling+hash&pg=PT102). N.B. Singh.
17. [↑](./Hash_function#cite_ref-Fuzzy_hashing_NIST.SP.800-168_22-0) Breitinger, Frank (May 2014). ["NIST Special Publication 800-168"](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-168.pdf) (PDF). *NIST Publications*. [doi](./Doi_(identifier)):[10.6028/NIST.SP.800-168](https://doi.org/10.6028%2FNIST.SP.800-168). Retrieved January 11, 2023.
18. [↑](./Hash_function#cite_ref-Fuzzy_hashing_Beyond_Precision_and_Recall:_Understanding_Uses_(and_Misuses)_of_Similarity_Hashes_in_Binary_Analysis_23-0) Pagani, Fabio; Dell'Amico, Matteo; Balzarotti, Davide (2018-03-13). ["Beyond Precision and Recall"](https://pagabuc.me/docs/codaspy18_pagani.pdf) (PDF). *Proceedings of the Eighth ACM Conference on Data and Application Security and Privacy*. New York, NY, USA: ACM. pp. 354–365. [doi](./Doi_(identifier)):[10.1145/3176258.3176306](https://doi.org/10.1145%2F3176258.3176306). [ISBN](./ISBN_(identifier)) [9781450356329](./Special:BookSources/9781450356329). Retrieved December 12, 2022.
19. [↑](./Hash_function#cite_ref-Fuzzy_hashing_Forensic_Malware_Analysis:_The_Value_of_Fuzzy_Hashing_Algorithms_in_Identifying_Similarities_24-0) Sarantinos, Nikolaos; Benzaïd, Chafika; Arabiat, Omar (2016). ["Forensic Malware Analysis: The Value of Fuzzy Hashing Algorithms in Identifying Similarities"](https://ieeexplore.ieee.org/document/7847157). [*2016 IEEE Trustcom/BigDataSE/ISPA*](http://roar.uel.ac.uk/5710/1/Forensic%20Malware%20Analysis.pdf) (PDF). pp. 1782–1787. [doi](./Doi_(identifier)):[10.1109/TrustCom.2016.0274](https://doi.org/10.1109%2FTrustCom.2016.0274). [ISBN](./ISBN_(identifier)) [978-1-5090-3205-1](./Special:BookSources/978-1-5090-3205-1). [S2CID](./S2CID_(identifier)) [32568938](https://api.semanticscholar.org/CorpusID:32568938). 10.1109/TrustCom.2016.0274.
20. [↑](./Hash_function#cite_ref-Fuzzy_hashing_ssdeep_25-0) Kornblum, Jesse (2006). ["Identifying almost identical files using context triggered piecewise hashing"](https://doi.org/10.1016%2Fj.diin.2006.06.015). *Digital Investigation*. 3, Supplement (September 2006): 91–97. [doi](./Doi_(identifier)):[10.1016/j.diin.2006.06.015](https://doi.org/10.1016%2Fj.diin.2006.06.015).
21. [↑](./Hash_function#cite_ref-Fuzzy_hashing_tlsh_26-0) Oliver, Jonathan; Cheng, Chun; Chen, Yanggui (2013). ["TLSH -- A Locality Sensitive Hash"](https://github.com/trendmicro/tlsh/blob/master/TLSH_CTC_final.pdf) (PDF). *2013 Fourth Cybercrime and Trustworthy Computing Workshop*. IEEE. pp. 7–13. [doi](./Doi_(identifier)):[10.1109/ctc.2013.9](https://doi.org/10.1109%2Fctc.2013.9). [ISBN](./ISBN_(identifier)) [978-1-4799-3076-0](./Special:BookSources/978-1-4799-3076-0). Retrieved December 12, 2022.
22. [↑](./Hash_function#cite_ref-Perceptual_hashing_buldas13_27-0) Buldas, Ahto; Kroonmaa, Andres; Laanoja, Risto (2013). "Keyless Signatures' Infrastructure: How to Build Global Distributed Hash-Trees". In Riis, Nielson H.; Gollmann, D. (eds.). *Secure IT Systems. NordSec 2013*. Lecture Notes in Computer Science. Vol. 8208. Berlin, Heidelberg: Springer. [doi](./Doi_(identifier)):[10.1007/978-3-642-41488-6_21](https://doi.org/10.1007%2F978-3-642-41488-6_21). [ISBN](./ISBN_(identifier)) [978-3-642-41487-9](./Special:BookSources/978-3-642-41487-9). Keyless Signatures Infrastructure (KSI) is a globally distributed system for providing time-stamping and server-supported digital signature services. Global per-second hash trees are created and their root hash values published. We discuss some service quality issues that arise in practical implementation of the service and present solutions for avoiding single points of failure and guaranteeing a service with reasonable and stable delay. Guardtime AS has been operating a KSI Infrastructure for 5 years. We summarize how the KSI Infrastructure is built, and the lessons learned during the operational period of the service.
23. [↑](./Hash_function#cite_ref-Perceptual_hashing_klinger_28-0) Klinger, Evan; Starkweather, David. ["pHash.org: Home of pHash, the open source perceptual hash library"](http://www.phash.org/). *pHash.org*. Retrieved 2018-07-05. pHash is an open source software library released under the GPLv3 license that implements several perceptual hashing algorithms, and provides a C-like API to use those functions in your own programs. pHash itself is written in C++.
24. [↑](./Hash_function#cite_ref-29) [Knuth, Donald E.](./Donald_Knuth) (1975). *The Art of Computer Programming, Vol. 3, Sorting and Searching*. Reading, MA: [Addison-Wesley](./Addison-Wesley). p. 540.
25. [↑](./Hash_function#cite_ref-30) Gonnet, G. (1978). *Expected Length of the Longest Probe Sequence in Hash Code Searching* (Technical report). Ontario, Canada: [University of Waterloo](./University_of_Waterloo). CS-RR-78-46.
26. [1](./Hash_function#cite_ref-knuth-2000_31-0) [2](./Hash_function#cite_ref-knuth-2000_31-1) [Knuth, Donald E.](./Donald_Knuth) (2000). *The Art of Computer Programming, Vol. 3, Sorting and Searching* (2. ed., 6. printing, newly updated and rev. ed.). Boston [u.a.]: Addison-Wesley. [ISBN](./ISBN_(identifier)) [978-0-201-89685-5](./Special:BookSources/978-0-201-89685-5).

 

## External links

   [![Wiktionary logo](//upload.wikimedia.org/wikipedia/commons/thumb/9/99/Wiktionary-logo-en-v2.svg/40px-Wiktionary-logo-en-v2.svg.png)](./File:Wiktionary-logo-en-v2.svg) Look up ***[hash](https://en.wiktionary.org/wiki/hash)*** in Wiktionary, the free dictionary.  
- [The Goulburn Hashing Function](http://www.sinfocol.org/archivos/2009/11/Goulburn06.pdf)  ([PDF](./Portable_Document_Format)) by Mayur Patel
- [Hash Function Construction for Textual and Geometrical Data Retrieval](https://dspace5.zcu.cz/bitstream/11025/11784/1/Skala_2010_Corfu-NAUN-Hash.pdf)  ([PDF](./Portable_Document_Format)) Latest Trends on Computers, Vol.2, pp. 483–489, CSCC Conference, Corfu, 2010

 
| vteData structuresandalgorithms |
| --- |
| Data structures | ArrayAssociative arrayBinary search treeFenwick treeGraphHash tableHeapLinked listQueueSegment treeStackStringTreeTrie |
| Algorithms andalgorithmic paradigms | BacktrackingBinary searchBreadth-first searchBrute-force searchDepth-first searchDivide and conquerDynamic programmingGraph traversalFoldGreedyHash functionMinimaxOnlineRandomizedRecursionRoot-findingSortingStreamingSweep lineString-searchingTopological sorting |
| List of data structuresList of algorithms |