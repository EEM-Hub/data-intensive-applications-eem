---
source: https://en.wikipedia.org/wiki/Cuckoo_filter
fetched: 2026-06-19
---

Data structure for approximate set membership 

A **cuckoo filter** is a space-efficient [probabilistic](./Probabilistic) [data structure](./Data_structure) that is used to test whether an [element](./Element_(mathematics)) is a member of a [set](./Set_(computer_science)), like a [Bloom filter](./Bloom_filter) does. [False positive](./Type_I_and_type_II_errors) matches are possible, but [false negatives](./Type_I_and_type_II_errors) are not – in other words, a query returns either "possibly in set" or "definitely not in set". A cuckoo filter can also delete existing items, which is
not supported by Bloom filters.
In addition, for applications that store many items and
target moderately low false positive rates, cuckoo filters can achieve
lower space overhead than space-optimized Bloom filters.[[1]](./Cuckoo_filter#cite_note-1)

 

Cuckoo filters were first described in 2014.[[2]](./Cuckoo_filter#cite_note-CuckooFilter-2)

 

## Algorithm description

 

A cuckoo filter uses a [hash table](./Hash_table) based on [cuckoo hashing](./Cuckoo_hashing) to store the [fingerprints](./Fingerprint_(computing)) of items.[[2]](./Cuckoo_filter#cite_note-CuckooFilter-2) The data structure is broken into buckets of some size     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3). To insert the fingerprint of an item     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4), one first computes two potential buckets      h  1   ( x )   {\displaystyle h_{1}(x)}  ![{\displaystyle h_{1}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5a54192749baa8ca6069d3c58b30722fd7eae55d) and      h  2   ( x )   {\displaystyle h_{2}(x)}  ![{\displaystyle h_{2}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d4960c74f885bc90838e4ed3abc4ae97ae838948) where     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) could go. These buckets are calculated using the formula

      h  1   ( x ) =  hash  ( x )   {\displaystyle h_{1}(x)={\text{hash}}(x)}  ![{\displaystyle h_{1}(x)={\text{hash}}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e51e461ab35b3d70a776adf7d1e8cf7d3558ce3f)      h  2   ( x ) =  h  1   ( x ) ⊕ ⊕   hash  (  fingerprint  ( x ) )   {\displaystyle h_{2}(x)=h_{1}(x)\oplus {\text{hash}}({\text{fingerprint}}(x))}  ![{\displaystyle h_{2}(x)=h_{1}(x)\oplus {\text{hash}}({\text{fingerprint}}(x))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5966395dc87893ec398a67e9c4f06001e878d970) 

Note that, due to the symmetry of the [XOR](./XOR) operation, one can compute      h  2   ( x )   {\displaystyle h_{2}(x)}  ![{\displaystyle h_{2}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d4960c74f885bc90838e4ed3abc4ae97ae838948) from      h  1   ( x )   {\displaystyle h_{1}(x)}  ![{\displaystyle h_{1}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5a54192749baa8ca6069d3c58b30722fd7eae55d), and      h  1   ( x )   {\displaystyle h_{1}(x)}  ![{\displaystyle h_{1}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5a54192749baa8ca6069d3c58b30722fd7eae55d) from      h  2   ( x )   {\displaystyle h_{2}(x)}  ![{\displaystyle h_{2}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d4960c74f885bc90838e4ed3abc4ae97ae838948). As defined above,      h  2   ( x ) =  h  1   ( x ) ⊕ ⊕   hash  (  fingerprint  ( x ) )   {\displaystyle h_{2}(x)=h_{1}(x)\oplus {\text{hash}}({\text{fingerprint}}(x))}  ![{\displaystyle h_{2}(x)=h_{1}(x)\oplus {\text{hash}}({\text{fingerprint}}(x))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5966395dc87893ec398a67e9c4f06001e878d970); it follows that      h  1   ( x ) =  h  2   ( x ) ⊕ ⊕   hash  (  fingerprint  ( x ) )   {\displaystyle h_{1}(x)=h_{2}(x)\oplus {\text{hash}}({\text{fingerprint}}(x))}  ![{\displaystyle h_{1}(x)=h_{2}(x)\oplus {\text{hash}}({\text{fingerprint}}(x))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cb7df14fb242d4a2852e3354a6248babeeee8084). These properties are what make it possible to store the fingerprints with cuckoo hashing.

 

The fingerprint of     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) is placed into one of buckets      h  1   ( x )   {\displaystyle h_{1}(x)}  ![{\displaystyle h_{1}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5a54192749baa8ca6069d3c58b30722fd7eae55d) and      h  2   ( x )   {\displaystyle h_{2}(x)}  ![{\displaystyle h_{2}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d4960c74f885bc90838e4ed3abc4ae97ae838948). If the buckets are full, then one of the fingerprints in the bucket is evicted using cuckoo hashing, and placed into the other bucket where it can go. If that bucket, in turn, is also full, then that may trigger another eviction, etc.

 

The hash table can achieve both high utilization (thanks to [cuckoo hashing](./Cuckoo_hashing)), and compactness because only fingerprints are stored. Lookup and delete operations of a cuckoo filter are straightforward.[[2]](./Cuckoo_filter#cite_note-CuckooFilter-2)

 

There are a maximum of two buckets to check by      h  1   ( x )   {\displaystyle h_{1}(x)}  ![{\displaystyle h_{1}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5a54192749baa8ca6069d3c58b30722fd7eae55d) and      h  2   ( x )   {\displaystyle h_{2}(x)}  ![{\displaystyle h_{2}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d4960c74f885bc90838e4ed3abc4ae97ae838948). If found, the appropriate lookup or delete operation can be performed in     O ( b )   {\displaystyle O(b)}  ![{\displaystyle O(b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/617e0fcc33be0730c40d7c458cd4951c60b4d66a) time. Often, in practice,     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3) is a constant.

 

In order for the hash table to offer theoretical guarantees, the fingerprint size     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) must be at least     Ω Ω  ( ( log ⁡ ⁡  n )  /  b )   {\displaystyle \Omega ((\log n)/b)}  ![{\displaystyle \Omega ((\log n)/b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/94905321b7398823add475e1562d88c869bea128) bits.[[2]](./Cuckoo_filter#cite_note-CuckooFilter-2)[[3]](./Cuckoo_filter#cite_note-3)[[4]](./Cuckoo_filter#cite_note-4) Subject to this constraint, cuckoo filters guarantee a false-positive rate of at most     ϵ ϵ  ≤ ≤  b  /   2  f − −  1     {\displaystyle \epsilon \leq b/2^{f-1}}  ![{\displaystyle \epsilon \leq b/2^{f-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a25f5e35a055e0079a11bf04e85acfee8859aae8).[[2]](./Cuckoo_filter#cite_note-CuckooFilter-2)

 

## Comparison to Bloom filters

 

A cuckoo filter is similar to a [Bloom filter](./Bloom_filter) in that they both are fast and compact, and they may both return false positives as answers to set-membership queries:

 
- Space-optimal Bloom filters use     1.44  log  2   ⁡ ⁡  ( 1  /  ϵ ϵ  )   {\displaystyle 1.44\log _{2}(1/\epsilon )}  ![{\displaystyle 1.44\log _{2}(1/\epsilon )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a4ba497b884703b3553bd3a57fa7c525f7c0093a) bits of space per inserted key, where     ϵ ϵ    {\displaystyle \epsilon }  ![{\displaystyle \epsilon }](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3837cad72483d97bcdde49c85d3b7b859fb3fd2) is the false positive rate. A cuckoo filter requires     (  log  2   ⁡ ⁡  ( 1  /  ϵ ϵ  ) + 1 +  log  2   ⁡ ⁡  b )  /  α α    {\displaystyle (\log _{2}(1/\epsilon )+1+\log _{2}b)/\alpha }  ![{\displaystyle (\log _{2}(1/\epsilon )+1+\log _{2}b)/\alpha }](https://wikimedia.org/api/rest_v1/media/math/render/svg/70768c939dd3e2308525fe38c2d5a0fd7d86db27) space per key[[2]](./Cuckoo_filter#cite_note-CuckooFilter-2) where     α α    {\displaystyle \alpha }  ![{\displaystyle \alpha }](https://wikimedia.org/api/rest_v1/media/math/render/svg/b79333175c8b3f0840bfb4ec41b8072c83ea88d3) is the hash table load factor, which can be     95.5 % %    {\displaystyle 95.5\%}  ![{\displaystyle 95.5\%}](https://wikimedia.org/api/rest_v1/media/math/render/svg/154b73c390d662af1d31d4e01a81a3f669cc6e58) based on the cuckoo filter's setting. Note that the information theoretical lower bound requires      log  2   ⁡ ⁡  ( 1  /  ϵ ϵ  )   {\displaystyle \log _{2}(1/\epsilon )}  ![{\displaystyle \log _{2}(1/\epsilon )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1d1c3851fee5c60aca706de5ab3899378474d1d1) bits for each item. Both bloom filters and cuckoo filters with low load can be compressed when not in use.
- On a positive lookup, a space-optimal Bloom filter requires a constant      log  2   ⁡ ⁡  ( 1  /  ϵ ϵ  )   {\displaystyle \log _{2}(1/\epsilon )}  ![{\displaystyle \log _{2}(1/\epsilon )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1d1c3851fee5c60aca706de5ab3899378474d1d1) memory accesses into the [bit array](./Bit_array), whereas a cuckoo filter requires at most     2 b   {\displaystyle 2b}  ![{\displaystyle 2b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3da45af0250645a54cab2ef45483c4399e4a40df) memory accesses, which can be a constant in practice.
- Cuckoo filters have degraded insertion speed after reaching a load threshold, when table expanding is recommended. In contrast, Bloom filters can keep inserting new items at the cost of a higher false positive rate before expansion.
- Bloom filters offer fast union and approximate intersection operations using cheap bitwise operations, which can also be applied to compressed bloom filters if streaming compression is used.

 

## Limitations

 
- A cuckoo filter can only delete items that are known to be inserted before.
- Insertion can fail and rehashing is required like other cuckoo hash tables. Note that the amortized insertion complexity is still     O ( 1 )   {\displaystyle O(1)}  ![{\displaystyle O(1)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21).[[5]](./Cuckoo_filter#cite_note-CuckooHashing-5)
- Cuckoo filters require a fingerprint size     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) of at least     Ω Ω  ( ( log ⁡ ⁡  n )  /  b )   {\displaystyle \Omega ((\log n)/b)}  ![{\displaystyle \Omega ((\log n)/b)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/94905321b7398823add475e1562d88c869bea128) bits. This means that the space per key must be at least     ( log ⁡ ⁡  n )  /  b   {\displaystyle (\log n)/b}  ![{\displaystyle (\log n)/b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cd5a8cec20a7c5c2236bd382d1384ba75b8959dc) bits, even if     ϵ ϵ    {\displaystyle \epsilon }  ![{\displaystyle \epsilon }](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3837cad72483d97bcdde49c85d3b7b859fb3fd2) is large. In practice,     b   {\displaystyle b}  ![{\displaystyle b}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f11423fbb2e967f986e36804a8ae4271734917c3) is chosen to be large enough that this is not a major issue.[[2]](./Cuckoo_filter#cite_note-CuckooFilter-2)

 

## References

 
- [![icon](//upload.wikimedia.org/wikipedia/commons/thumb/6/6f/Octicons-terminal.svg/40px-Octicons-terminal.svg.png)](./File:Octicons-terminal.svg)[Computer programming portal](./Portal:Computer_programming)

  
1. [↑](./Cuckoo_filter#cite_ref-1)  [Michael D. Mitzenmacher](./Michael_Mitzenmacher). ["Bloom Filters, Cuckoo Hashing, Cuckoo Filters, Adaptive Cuckoo Filters, and Learned Bloom Filters"](https://smartech.gatech.edu/handle/1853/60577).
2. [1](./Cuckoo_filter#cite_ref-CuckooFilter_2-0) [2](./Cuckoo_filter#cite_ref-CuckooFilter_2-1) [3](./Cuckoo_filter#cite_ref-CuckooFilter_2-2) [4](./Cuckoo_filter#cite_ref-CuckooFilter_2-3) [5](./Cuckoo_filter#cite_ref-CuckooFilter_2-4) [6](./Cuckoo_filter#cite_ref-CuckooFilter_2-5) [7](./Cuckoo_filter#cite_ref-CuckooFilter_2-6)  Fan, Bin; Andersen, Dave G.; Kaminsky, Michael; [Mitzenmacher, Michael D.](./Michael_Mitzenmacher) (2014). *Cuckoo filter: Practically better than Bloom*. Proc. 10th ACM International on Conference on Emerging Networking Experiments and Technologies (CoNEXT '14). Sydney, Australia. pp. 75–88. [doi](./Doi_(identifier)):[10.1145/2674005.2674994](https://doi.org/10.1145%2F2674005.2674994). [ISBN](./ISBN_(identifier)) [9781450332798](./Special:BookSources/9781450332798).
3. [↑](./Cuckoo_filter#cite_ref-3)  [Eppstein, David](./David_Eppstein) (22 June 2016). *Cuckoo filter: Simplification and analysis*. Proc. 15th Scandinavian Symposium and Workshops on Algorithm Theory (SWAT 2016). Leibniz International Proceedings in Informatics (LIPIcs). Vol. 53. Reykjavik, Iceland. pp. 8:1–8:12. [arXiv](./ArXiv_(identifier)):[1604.06067](https://arxiv.org/abs/1604.06067). [doi](./Doi_(identifier)):[10.4230/LIPIcs.SWAT.2016.8](https://doi.org/10.4230%2FLIPIcs.SWAT.2016.8).
4. [↑](./Cuckoo_filter#cite_ref-4)  Fleming, Noah (17 May 2018). [*Cuckoo Hashing and Cuckoo Filters*](http://www.cs.toronto.edu/~noahfleming/CuckooHashing.pdf) (PDF) (Technical report). University of Toronto.
5. [↑](./Cuckoo_filter#cite_ref-CuckooHashing_5-0) [Pagh, Rasmus](./Rasmus_Pagh); Rodler, Flemming Friche (2001). "Cuckoo hashing". *Proc. 9th Annual European Symposium on Algorithms (ESA 2001)*. Lecture Notes in Computer Science. Vol. 2161. Århus, Denmark. pp. 121–133. [doi](./Doi_(identifier)):[10.1007/3-540-44676-1_10](https://doi.org/10.1007%2F3-540-44676-1_10). [ISBN](./ISBN_(identifier)) [978-3-540-42493-2](./Special:BookSources/978-3-540-42493-2).

 

## External links

 
- [Probabilistic Filters By Example – A tutorial comparing Cuckoo and Bloom filters.](https://bdupras.github.io/filter-tutorial/)