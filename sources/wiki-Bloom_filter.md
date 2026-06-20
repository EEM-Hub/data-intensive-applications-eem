---
source: https://en.wikipedia.org/wiki/Bloom_filter
fetched: 2026-06-19
---

Data structure for approximate set membership Not to be confused with [Bloom shader effect](./Bloom_(shader_effect)). 
| Part ofa serieson |
| --- |
| Probabilisticdata structures |
| Bloom filterCount sketchCount–min sketchQuotient filterSkip list |
| Random trees |
| Random binary treeTreapRapidly exploring random tree |
| Related |
| Randomized algorithmHyperLogLog |
| vte |

 

In [computing](./Computing), a **Bloom filter** is a space-efficient [probabilistic](./Probabilistic) [data structure](./Data_structure), conceived by [Burton Howard Bloom](./Burton_Howard_Bloom) in 1970, that is used to test whether an [element](./Element_(mathematics)) is a member of a [set](./Set_(computer_science)). [False positive](./Type_I_and_type_II_errors) matches are possible, but [false negatives](./Type_I_and_type_II_errors) are not – in other words, a query returns either "possibly in set" or "definitely not in set". Elements can be added to the set, but not removed (though this can be addressed with the [counting Bloom filter](./Bloom_filter#Counting_Bloom_filters) variant); the more items added, the larger the probability of false positives.

 

Bloom proposed the technique for applications where the amount of source data would require an impractically large amount of memory if "conventional" error-free [hashing](./Hash_function) techniques were applied. He gave the example of a [hyphenation algorithm](./Hyphenation_algorithm) for a dictionary of 500,000 words, out of which 90% follow simple hyphenation rules, but the remaining 10% require expensive disk accesses to retrieve specific hyphenation patterns. With sufficient [core memory](./Core_memory), an error-free hash could be used to eliminate all unnecessary disk accesses; on the other hand, with limited core memory, Bloom's technique uses a smaller hash area but still eliminates most unnecessary accesses. For example, a hash area only 18% of the size needed by an ideal error-free hash still eliminates 87% of the disk accesses.[[1]](./Bloom_filter#cite_note-FOOTNOTEBloom1970-1)

 

More generally, fewer than 10 [bits](./Bit) per element are required for a 1% false positive probability, independent of the size or number of elements in the set.[[2]](./Bloom_filter#cite_note-FOOTNOTEBonomiMitzenmacherPanigrahySingh2006-2)

 

## Algorithm description

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/a/ac/Bloom_filter.svg/500px-Bloom_filter.svg.png)](./File:Bloom_filter.svg)An example of a Bloom filter, representing the set {*x*, *y*, *z*} . The colored arrows show the positions in the bit array that each set element is mapped to. The element w is not in the set {*x*, *y*, *z*} , because it hashes to one bit-array position containing 0. For this figure, *m* = 18 and k = 3. 

An *empty Bloom filter* is a [bit array](./Bit_array) of m bits, all set to 0. It is equipped with k different [hash functions](./Hash_function), which map set elements to one of the m possible array positions. To be optimal, the hash functions should be [uniformly distributed](./Discrete_uniform_distribution) and [independent](./Independence_(probability_theory)). Typically, k is a small constant which depends on the desired false error rate  ε, while m is proportional to k and the number of elements to be added.

 

To *add* an element, feed it to each of the k hash functions to get k array positions. Set the bits at all these positions to 1.

 

To *test* whether an element is in the set, feed it to each of the k hash functions to get k array positions. If *any* of the bits at these positions is 0, the element is definitely not in the set; if it were, then all the bits would have been set to 1 when it was inserted. If all are 1, then either the element is in the set, *or* the bits have by chance been set to 1 during the insertion of other elements, resulting in a [false positive](./False_positive). In a simple Bloom filter, there is no way to distinguish between the two cases, but more advanced techniques can address this problem.

 

The requirement of designing k different independent hash functions can be prohibitive for large k. For a good hash function with a wide output, there should be little if any correlation between different bit-fields of such a hash, so this type of hash can be used to generate multiple "different" hash functions by slicing its output into multiple bit fields.  Alternatively, one can pass k different initial values (such as 0, 1, ..., k − 1) to a hash function that takes an initial value; or add (or append) these values to the key. For larger m and/or k, independence among the hash functions can be relaxed with negligible increase in false positive rate.[[3]](./Bloom_filter#cite_note-3) (Specifically, [Dillinger & Manolios (2004b)](./Bloom_filter#CITEREFDillingerManolios2004b) show the effectiveness of deriving the k indices using [enhanced double hashing](./Double_hashing#Enhanced_double_hashing)
and [triple hashing](./Double_hashing#Triple_hashing), variants of [double hashing](./Double_hashing) that are effectively simple random number generators seeded with the two or three hash values.)

 

Removing an element from this simple Bloom filter is impossible because there is no way to tell which of the k bits it maps to should be cleared.  Although setting any one of those k bits to zero suffices to remove the element, it would also remove any other elements that happen to map onto that bit. Since the simple algorithm provides no way to determine whether any other elements have been added that affect the bits for the element to be removed, clearing any of the bits would introduce the possibility of false negatives.

 

One-time removal of an element from a Bloom filter can be simulated by having a second Bloom filter that contains items that have been removed.  However, false positives in the second filter become false negatives in the composite filter, which may be undesirable.  In this approach re-adding a previously removed item is not possible, as one would have to remove it from the "removed" filter.

 

It is often the case that all the keys are available but are expensive to enumerate (for example, requiring many disk reads).  When the false positive rate gets too high, the filter can be regenerated; this should be a relatively rare event.

 

## Space and time advantages

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/c/c4/Bloom_filter_speed.svg/500px-Bloom_filter_speed.svg.png)](./File:Bloom_filter_speed.svg)Bloom filter used to speed up answers in a key-value storage system. Values are stored on a disk which has slow access times. Bloom filter decisions are much faster. However some unnecessary disk accesses are made when the filter reports a positive (in order to weed out the false positives). Overall answer speed is better with the Bloom filter than without the Bloom filter. Use of a Bloom filter for this purpose, however, does increase memory usage.[*[citation needed](./Wikipedia:Citation_needed)*] 

While risking false positives, Bloom filters have a substantial space advantage over other data structures for representing sets, such as [self-balancing binary search trees](./Self-balancing_binary_search_tree), [tries](./Trie), [hash tables](./Hash_table), or simple [arrays](./Array_data_structure) or [linked lists](./Linked_list) of the entries. Most of these require storing at least the data items themselves, which can require anywhere from a small number of bits, for small integers, to an arbitrary number of bits, such as for strings ([tries](./Trie) are an exception since they can share storage between elements with equal prefixes).  However, Bloom filters do not store the data items at all, and a separate solution must be provided for the actual storage. Linked structures incur an additional linear space overhead for pointers. A Bloom filter with a 1% error and an optimal value of k, in contrast, requires only about 9.6 bits per element, regardless of the size of the elements. This advantage comes partly from its compactness, inherited from arrays, and partly from its probabilistic nature. The 1% false-positive rate can be reduced by a factor of ten by adding only about 4.8 bits per element.

 

However, if the number of potential values is small and many of them can be in the set, the Bloom filter is easily surpassed by the deterministic [bit array](./Bit_array), which requires only one bit for each potential element. Hash tables gain a space and time advantage if they begin ignoring collisions and store only whether each bucket contains an entry; in this case, they have effectively become Bloom filters with k = 1.[[4]](./Bloom_filter#cite_note-FOOTNOTEMitzenmacherUpfal2005-4)

 

Bloom filters also have the unusual property that the time needed either to add items or to check whether an item is in the set is a fixed constant, O(k), completely independent of the number of items already in the set. No other constant-space set data structure has this property, but the average [access time](./Access_time) of sparse [hash tables](./Hash_table) can make them faster in practice than some Bloom filters.  In a hardware implementation, however, the Bloom filter shines because its k lookups are independent and can be parallelized.

 

To understand its space efficiency, it is instructive to compare the general Bloom filter with its special case when k = 1.  If k = 1, then in order to keep the false positive rate sufficiently low, a small fraction of bits should be set, which means the array must be very large and contain long runs of zeros.  The [information content](./Information_content) of the array relative to its size is low.  The generalized Bloom filter (k greater than 1) allows many more bits to be set while still maintaining a low false positive rate; if the parameters (k and m) are chosen well, about half of the bits will be set,[[5]](./Bloom_filter#cite_note-5) and these will be apparently random, minimizing redundancy and maximizing information content.

 

## Probability of false positives

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/e/ef/Bloom_filter_fp_probability.svg/500px-Bloom_filter_fp_probability.svg.png)](./File:Bloom_filter_fp_probability.svg)The false positive probability p as a function of number of elements n in the filter and the filter size m. An optimal number of hash functions *k* = (*m* / *n*) ln 2 has been assumed. 

Assume that a [hash function](./Hash_function) selects each array position with equal probability. If *m* is the number of bits in the array, the probability that a certain bit is not set to 1 by a certain hash function during the insertion of an element is

     1 − −    1 m   .   {\displaystyle 1-{\frac {1}{m}}.}  ![{\displaystyle 1-{\frac {1}{m}}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ba586e62be77ee25ad8bd3be82b5e301befca2b1) 

If *k* is the number of hash functions and each has no significant correlation between each other, then the probability that the bit is not set to 1 by any of the hash functions is

       (  1 − −    1 m    )   k   .   {\displaystyle \left(1-{\frac {1}{m}}\right)^{k}.}  ![{\displaystyle \left(1-{\frac {1}{m}}\right)^{k}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bcc44b7c01b3f7bf7cdb01fe3da407e38bf123c0) 

We can use the well-known identity for [*e*](./E_(mathematical_constant))−1

      lim  m → →  ∞ ∞      (  1 − −    1 m    )   m   =   1 e     {\displaystyle \lim _{m\to \infty }\left(1-{\frac {1}{m}}\right)^{m}={\frac {1}{e}}}  ![{\displaystyle \lim _{m\to \infty }\left(1-{\frac {1}{m}}\right)^{m}={\frac {1}{e}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3c6fd9b82d1fa7934249f5cac36403a7e5fbea3f) 

to conclude that, for large *m*,

       (  1 − −    1 m    )   k   =   (   (  1 − −    1 m    )   m   )   k  /  m   ≈ ≈   e  − −  k  /  m   .   {\displaystyle \left(1-{\frac {1}{m}}\right)^{k}=\left(\left(1-{\frac {1}{m}}\right)^{m}\right)^{k/m}\approx e^{-k/m}.}  ![{\displaystyle \left(1-{\frac {1}{m}}\right)^{k}=\left(\left(1-{\frac {1}{m}}\right)^{m}\right)^{k/m}\approx e^{-k/m}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0ec9efb407968ddc7e0a9d929c873bca8d88d087) 

If we have inserted *n* elements, the probability that a certain bit is still 0 is

       (  1 − −    1 m    )   k n   ≈ ≈   e  − −  k n  /  m   ;   {\displaystyle \left(1-{\frac {1}{m}}\right)^{kn}\approx e^{-kn/m};}  ![{\displaystyle \left(1-{\frac {1}{m}}\right)^{kn}\approx e^{-kn/m};}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c04360eeef1bc5c97623d14053e8330ee68d8ba0) 

the probability that it is 1 is therefore

     1 − −    (  1 − −    1 m    )   k n   ≈ ≈  1 − −   e  − −  k n  /  m   .   {\displaystyle 1-\left(1-{\frac {1}{m}}\right)^{kn}\approx 1-e^{-kn/m}.}  ![{\displaystyle 1-\left(1-{\frac {1}{m}}\right)^{kn}\approx 1-e^{-kn/m}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a2720907b6427121c450deb800c1f7de40e7bd5f) 

Now test membership of an element that is not in the set. Each of the *k* array positions computed by the hash functions is 1 with a probability as above. The probability of all of them being 1, which would cause the [algorithm](./Algorithm) to erroneously claim that the element is in the set, is often given as

     ε ε  =   (  1 − −    [  1 − −    1 m    ]   k n    )   k   ≈ ≈    (  1 − −   e  − −  k n  /  m    )   k   .   {\displaystyle \varepsilon =\left(1-\left[1-{\frac {1}{m}}\right]^{kn}\right)^{k}\approx \left(1-e^{-kn/m}\right)^{k}.}  ![{\displaystyle \varepsilon =\left(1-\left[1-{\frac {1}{m}}\right]^{kn}\right)^{k}\approx \left(1-e^{-kn/m}\right)^{k}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/de73929baec5fd76dde95874189051648c635b1d) 

This is not strictly correct as it assumes independence for the probabilities of each bit being set. However, assuming it is a close approximation we have that the probability of false positives decreases as *m* (the number of bits in the array) increases, and increases as *n* (the number of inserted elements) increases.

 

The true probability of a false positive, without assuming independence, is

       1  m  k ( n + 1 )      ∑ ∑   i = 1   m    i  k   i !    (   m i   )     {    k n  i   }    {\displaystyle {\frac {1}{m^{k(n+1)}}}\sum _{i=1}^{m}i^{k}i!{m \choose i}\left\{{kn \atop i}\right\}}  ![{\displaystyle {\frac {1}{m^{k(n+1)}}}\sum _{i=1}^{m}i^{k}i!{m \choose i}\left\{{kn \atop i}\right\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ba4d33acf4427158c541d5bbdabf30b337a9b358) 

where the {braces} denote [Stirling numbers of the second kind](./Stirling_numbers_of_the_second_kind).[[6]](./Bloom_filter#cite_note-6)

 

An alternative analysis arriving at the same approximation without the assumption of independence is given by Mitzenmacher and Upfal.[[7]](./Bloom_filter#cite_note-7) After all *n* items have been added to the Bloom filter, let *q* be the fraction of the *m* bits that are set to 0. (That is, the number of bits still set to 0 is *qm*.) Then, when testing membership of an element not in the set, for the array position given by any of the *k* hash functions, the probability that the bit is found set to 1 is     1 − −  q   {\displaystyle 1-q}  ![{\displaystyle 1-q}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3ccb1d1caf362976d80524abd2c5b3d9e58b1344). So the probability that all *k* hash functions find their bit set to 1 is     ( 1 − −  q  )  k     {\displaystyle (1-q)^{k}}  ![{\displaystyle (1-q)^{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5f384f3cdf2549d253b9666353746bf10cfd1e0e).  Further, the expected value of *q* is the probability that a given array position is left untouched by each of the *k* hash functions for each of the *n* items, which is (as above)

     E [ q ] =   (  1 − −    1 m    )   k n     {\displaystyle E[q]=\left(1-{\frac {1}{m}}\right)^{kn}}  ![{\displaystyle E[q]=\left(1-{\frac {1}{m}}\right)^{kn}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c213b5ac119f9c4f695469b512545fc5b49ef8c1). 

It is possible to prove, without the independence assumption, that *q* is very strongly concentrated around its expected value.  In particular, from the [Azuma–Hoeffding inequality](./Azuma–Hoeffding_inequality), they prove that[[8]](./Bloom_filter#cite_note-8)

     Pr (  |  q − −  E [ q ]  |  ≥ ≥    λ λ  m   ) ≤ ≤  2 exp ⁡ ⁡  ( − −  2  λ λ   2    /  k n )   {\displaystyle \Pr(\left|q-E[q]\right|\geq {\frac {\lambda }{m}})\leq 2\exp(-2\lambda ^{2}/kn)}  ![{\displaystyle \Pr(\left|q-E[q]\right|\geq {\frac {\lambda }{m}})\leq 2\exp(-2\lambda ^{2}/kn)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b63e23e0badb4182e147f75aa18b011421c014dc) 

Because of this, we can say that the exact probability of false positives is

      ∑ ∑   t   Pr ( q = t ) ( 1 − −  t  )  k   ≈ ≈  ( 1 − −  E [ q ]  )  k   =   (  1 − −    [  1 − −    1 m    ]   k n    )   k   ≈ ≈    (  1 − −   e  − −  k n  /  m    )   k     {\displaystyle \sum _{t}\Pr(q=t)(1-t)^{k}\approx (1-E[q])^{k}=\left(1-\left[1-{\frac {1}{m}}\right]^{kn}\right)^{k}\approx \left(1-e^{-kn/m}\right)^{k}}  ![{\displaystyle \sum _{t}\Pr(q=t)(1-t)^{k}\approx (1-E[q])^{k}=\left(1-\left[1-{\frac {1}{m}}\right]^{kn}\right)^{k}\approx \left(1-e^{-kn/m}\right)^{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c6ec47c32d7acc2aef7c673b9f891f26ec425c5f) 

as before.

 

### Optimal number of hash functions

 

The number of hash functions, *k*, must be a positive integer.  Putting this constraint aside, for a given *m* and *n*, the value of *k* that minimizes the false positive probability is

     k =   m n   ln ⁡ ⁡  2.   {\displaystyle k={\frac {m}{n}}\ln 2.}  ![{\displaystyle k={\frac {m}{n}}\ln 2.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fabc2770225ac59fe42a78f75ea89de650f0130c) 

The required number of bits, *m*, given *n* (the number of inserted elements) and a desired false positive probability *ε* (and assuming the optimal value of *k* is used) can be computed by substituting the optimal value of *k* in the probability expression above:

     ε ε  =   (  1 − −   e  − −  (   m n   ln ⁡ ⁡  2 )   n m      )     m n   ln ⁡ ⁡  2   =   (   1 2   )     m n   ln ⁡ ⁡  2     {\displaystyle \varepsilon =\left(1-e^{-({\frac {m}{n}}\ln 2){\frac {n}{m}}}\right)^{{\frac {m}{n}}\ln 2}=\left({\frac {1}{2}}\right)^{{\frac {m}{n}}\ln 2}}  ![{\displaystyle \varepsilon =\left(1-e^{-({\frac {m}{n}}\ln 2){\frac {n}{m}}}\right)^{{\frac {m}{n}}\ln 2}=\left({\frac {1}{2}}\right)^{{\frac {m}{n}}\ln 2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/96f5286dc7a886b0a32c5e1e16274d61c3926fa0) 

which can be simplified to:

     ln ⁡ ⁡  ( ε ε  ) = − −    m n   ln ⁡ ⁡  ( 2  )  2   .   {\displaystyle \ln(\varepsilon )=-{\frac {m}{n}}\ln(2)^{2}.}  ![{\displaystyle \ln(\varepsilon )=-{\frac {m}{n}}\ln(2)^{2}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/555abfd0f5559505c189884eb49d6b099a078a6e) 

This results in:

     m = − −     n ln ⁡ ⁡  ( ε ε  )   ln ⁡ ⁡  ( 2  )  2        {\displaystyle m=-{\frac {n\ln(\varepsilon )}{\ln(2)^{2}}}}  ![{\displaystyle m=-{\frac {n\ln(\varepsilon )}{\ln(2)^{2}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5a90ab21c84c30f655ae6b0b9ea78a407738a487) 

So the optimal number of bits per element is

       m n   = − −     ln ⁡ ⁡  ( ε ε  )   ln ⁡ ⁡  ( 2  )  2      ≈ ≈  − −  2.08 ln ⁡ ⁡  ( ε ε  )   {\displaystyle {\frac {m}{n}}=-{\frac {\ln(\varepsilon )}{\ln(2)^{2}}}\approx -2.08\ln(\varepsilon )}  ![{\displaystyle {\frac {m}{n}}=-{\frac {\ln(\varepsilon )}{\ln(2)^{2}}}\approx -2.08\ln(\varepsilon )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e1d161b39408fa2bacff4205a1b37da3a6eaf480) 

with the corresponding number of hash functions *k* (ignoring integrality):

     k = − −     ln ⁡ ⁡  ( ε ε  )   ln ⁡ ⁡  ( 2 )    .   {\displaystyle k=-{\frac {\ln(\varepsilon )}{\ln(2)}}.}  ![{\displaystyle k=-{\frac {\ln(\varepsilon )}{\ln(2)}}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a0a309739f774b3d8f84fdd092a8faaf6af59706) 

This means that for a given false positive probability *ε*, the length of a Bloom filter *m* is proportionate to the number of elements being filtered *n* and the required number of hash functions only depends on the target false positive probability *ε*.[[9]](./Bloom_filter#cite_note-9)

 

The formula     m = − −     n ln ⁡ ⁡  ε ε    ( ln ⁡ ⁡  2  )  2        {\displaystyle m=-{\frac {n\ln \varepsilon }{(\ln 2)^{2}}}}  ![{\displaystyle m=-{\frac {n\ln \varepsilon }{(\ln 2)^{2}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/72c259d2b3b44ed3ae5b761887f87c220e039468) is approximate for three reasons.  First, and of least concern, it approximates
    1 − −    1 m     {\displaystyle 1-{\frac {1}{m}}}  ![{\displaystyle 1-{\frac {1}{m}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac7138ac40c1a9e28c3d38e4461803563bef6443) as      e  − −    1 m       {\displaystyle e^{-{\frac {1}{m}}}}  ![{\displaystyle e^{-{\frac {1}{m}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/49f584f9392be51e3e80790a81162c22c855a652), which is a good asymptotic approximation (i.e., which holds as *m* →∞).  Second, of more concern, it assumes that during the membership test the event that one tested bit is set to 1 is independent of the event that any other tested bit is set to 1.  Third, of most concern, it assumes that     k =   m n   ln ⁡ ⁡  2   {\displaystyle k={\frac {m}{n}}\ln 2}  ![{\displaystyle k={\frac {m}{n}}\ln 2}](https://wikimedia.org/api/rest_v1/media/math/render/svg/76b2ffcb64af4db830273f5b73ac67b91dace6ac) is fortuitously integral.

 

Goel and Gupta,[[10]](./Bloom_filter#cite_note-10) however, give a rigorous upper bound that makes no approximations and requires no assumptions.  They show that the false positive probability for a finite Bloom filter with *m* bits (    m > 1   {\displaystyle m>1}  ![{\displaystyle m>1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7f27527902d05e4c32bcbe28d425d7790f8ae191)), *n* elements, and *k* hash functions is at most

     ε ε  ≤ ≤    (  1 − −   e  − −     k ( n + 0.5 )   m − −  1       )   k   .   {\displaystyle \varepsilon \leq \left(1-e^{-{\frac {k(n+0.5)}{m-1}}}\right)^{k}.}  ![{\displaystyle \varepsilon \leq \left(1-e^{-{\frac {k(n+0.5)}{m-1}}}\right)^{k}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a13e33b3b0df269e740d47fb7719e1f7d0647ddf) 

This bound can be interpreted as saying that the approximate formula       (  1 − −   e  − −     k n  m      )   k     {\displaystyle \left(1-e^{-{\frac {kn}{m}}}\right)^{k}}  ![{\displaystyle \left(1-e^{-{\frac {kn}{m}}}\right)^{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/54f345dc43a24c39bf0a0f4d22afa34c1adc2308) can be applied at a penalty of at most half an extra element and at most one less bit.

 

## Approximating the number of items in a Bloom filter

 

The number of items in a Bloom filter can be approximated with the following formula,

      n  ∗ ∗    = − −    m k   ln ⁡ ⁡   [  1 − −    X m    ]  ,   {\displaystyle n^{*}=-{\frac {m}{k}}\ln \left[1-{\frac {X}{m}}\right],}  ![{\displaystyle n^{*}=-{\frac {m}{k}}\ln \left[1-{\frac {X}{m}}\right],}](https://wikimedia.org/api/rest_v1/media/math/render/svg/61a0f3398b96f0e26aa0935aba89096dcc22fc5f) 

where      n  ∗ ∗      {\displaystyle n^{*}}  ![{\displaystyle n^{*}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9615e0726d9d6cc58d117a844dca1ca84bb81f7e) is an estimate of the number of items in the filter, m is the length (size) of the filter, k is the number of hash functions, and X is the number of bits set to one.[[11]](./Bloom_filter#cite_note-Swamidass_2007-11)

 

### The union and intersection of sets

 

Bloom filters are a way of compactly representing a set of items. It is common to try to compute the size of the intersection or union between two sets. Bloom filters can be used to approximate the size of the intersection and union of two sets. For two Bloom filters of length m, their counts, respectively can be estimated as

     n (  A  ∗ ∗    ) = − −    m k   ln ⁡ ⁡   [  1 − −      |  A  |   m    ]    {\displaystyle n(A^{*})=-{\frac {m}{k}}\ln \left[1-{\frac {|A|}{m}}\right]}  ![{\displaystyle n(A^{*})=-{\frac {m}{k}}\ln \left[1-{\frac {|A|}{m}}\right]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fd27c870de822d6032469dda4b6eccf4ba4ac9eb) 

and

     n (  B  ∗ ∗    ) = − −    m k   ln ⁡ ⁡   [  1 − −      |  B  |   m    ]  .   {\displaystyle n(B^{*})=-{\frac {m}{k}}\ln \left[1-{\frac {|B|}{m}}\right].}  ![{\displaystyle n(B^{*})=-{\frac {m}{k}}\ln \left[1-{\frac {|B|}{m}}\right].}](https://wikimedia.org/api/rest_v1/media/math/render/svg/dbcc1699bb04b9dcb909cd136210db798526bbf1) 

The size of their union can be estimated as

     n (  A  ∗ ∗    ∪ ∪   B  ∗ ∗    ) = − −    m k   ln ⁡ ⁡   [  1 − −      |  A ∪ ∪  B  |   m    ]  ,   {\displaystyle n(A^{*}\cup B^{*})=-{\frac {m}{k}}\ln \left[1-{\frac {|A\cup B|}{m}}\right],}  ![{\displaystyle n(A^{*}\cup B^{*})=-{\frac {m}{k}}\ln \left[1-{\frac {|A\cup B|}{m}}\right],}](https://wikimedia.org/api/rest_v1/media/math/render/svg/af258dc11fd3f7cc5eda98e4a4d8552c3f418e48) 

where     n ( A ∪ ∪  B )   {\displaystyle n(A\cup B)}  ![{\displaystyle n(A\cup B)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/72c7781e1018b592ed33a97f54968d90b35a35fe) is the number of bits set to one in either of the two Bloom filters.  Finally, the intersection can be estimated as

     n (  A  ∗ ∗    ∩ ∩   B  ∗ ∗    ) = n (  A  ∗ ∗    ) + n (  B  ∗ ∗    ) − −  n (  A  ∗ ∗    ∪ ∪   B  ∗ ∗    ) ,   {\displaystyle n(A^{*}\cap B^{*})=n(A^{*})+n(B^{*})-n(A^{*}\cup B^{*}),}  ![{\displaystyle n(A^{*}\cap B^{*})=n(A^{*})+n(B^{*})-n(A^{*}\cup B^{*}),}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b2ff1e4a1d473af3188fa29bca6f3a7ea74544b9) 

using the three formulas together.[[11]](./Bloom_filter#cite_note-Swamidass_2007-11)

 

## Properties

 
|  | This section mayrequirecleanupto meet Wikipedia'squality standards. The specific problem is:These entries should be cited and moved into other sections, or expanded into their own subsections.Please helpimprove this sectionif you can.(May 2024)(Learn how and when to remove this message) |
| --- | --- |

 
- Unlike a standard [hash table](./Hash_table) using [open addressing](./Hash_table#Open_addressing) for [collision resolution](./Collision_resolution_scheme), a Bloom filter of a fixed size can represent a set with an arbitrarily large number of elements; adding an element never fails due to the data structure "filling up". However, the false positive rate increases steadily as elements are added until all bits in the filter are set to 1, at which point *all* queries yield a positive result. With open addressing hashing, false positives are never produced, but performance steadily deteriorates until it approaches [linear search](./Linear_search).
- [Union](./Union_(set_theory)) and [intersection](./Intersection_(set_theory)) of Bloom filters with the same size and set of hash functions can be implemented with [bitwise](./Bitwise_operation) OR and AND operations, respectively. The union operation on Bloom filters is lossless in the sense that the resulting Bloom filter is the same as the Bloom filter created from scratch using the union of the two sets. The intersect operation satisfies a weaker property: the false positive probability in the resulting Bloom filter is at most the false-positive probability in one of the constituent Bloom filters, but may be larger than the false positive probability in the Bloom filter created from scratch using the intersection of the two sets.
- Some kinds of [superimposed code](./Superimposed_code) can be seen as a Bloom filter implemented with physical [edge-notched cards](./Edge-notched_card). An example is [Zatocoding](./Zatocoding), invented by [Calvin Mooers](./Calvin_Mooers) in 1947, in which the set of categories associated with a piece of information is represented by notches on a card, with a random pattern of four notches for each category.

 

## Examples

 
- [Fruit flies](./Drosophila_melanogaster) use a modified version of Bloom filters to detect novelty of odors, with additional features including similarity of novel odor to that of previously experienced examples, and time elapsed since previous experience of the same odor.[[12]](./Bloom_filter#cite_note-12)
- The servers of [Akamai Technologies](./Akamai_Technologies), a [content delivery](./Content_delivery) provider, use Bloom filters to prevent "one-hit-wonders" from being stored in its disk caches. One-hit-wonders are web objects requested by users just once, something that Akamai found applied to nearly three-quarters of their caching infrastructure. Using a Bloom filter to detect the second request for a web object and caching that object only on its second request prevents one-hit wonders from entering the disk cache, significantly reducing disk workload and increasing disk cache hit rates.[[13]](./Bloom_filter#cite_note-FOOTNOTEMaggsSitaraman2015-13)
- Google [Bigtable](./Bigtable), [Apache HBase](./Apache_HBase), [Apache Cassandra](./Apache_Cassandra), [ScyllaDB](./ScyllaDB) and [PostgreSQL](./PostgreSQL)[[14]](./Bloom_filter#cite_note-14) use Bloom filters to reduce the disk lookups for non-existent rows or columns. Avoiding costly disk lookups considerably increases the performance of a database query operation.[[15]](./Bloom_filter#cite_note-15)
- The [Google Chrome](./Google_Chrome) [web browser](./Web_browser) previously used a Bloom filter to identify malicious [URLs](./URL). Any URL was first checked against a local Bloom filter, and only if the Bloom filter returned a positive result was a full check of the URL performed (and the user warned, if that too returned a positive result).[[16]](./Bloom_filter#cite_note-16)[[17]](./Bloom_filter#cite_note-17)
- Mozilla [Firefox](./Firefox) uses cascading Bloom filters for Certificate Revocation[[18]](./Bloom_filter#cite_note-18)[[19]](./Bloom_filter#cite_note-19) and for blocking malicious addons.[[20]](./Bloom_filter#cite_note-20)
- Microsoft [Bing (search engine)](./Bing_(search_engine)) uses multi-level hierarchical Bloom filters for its search index, [BitFunnel](./BitFunnel). Bloom filters provided lower cost than the previous Bing index, which was based on [inverted files](./Inverted_files).[[21]](./Bloom_filter#cite_note-21)
- The [Squid](./Squid_(software)) [Web](./World_Wide_Web) Proxy [Cache](./Web_cache) uses Bloom filters for cache digests.[[22]](./Bloom_filter#cite_note-FOOTNOTEWessels2004-22)
- [Bitcoin](./Bitcoin) used Bloom filters to speed up wallet synchronization until privacy vulnerabilities with the implementation of Bloom filters were discovered.[[23]](./Bloom_filter#cite_note-23)
- The [Venti](./Venti_(software)) archival storage system uses Bloom filters to detect previously stored data.[[24]](./Bloom_filter#cite_note-24)
- The [SPIN model checker](./SPIN_model_checker) uses Bloom filters to track the reachable state space for large verification problems.[[25]](./Bloom_filter#cite_note-25)
- The [Cascading](./Cascading_(software)) analytics framework uses Bloom filters to speed up asymmetric joins, where one of the joined data sets is significantly larger than the other (often called Bloom join in the database literature).[[26]](./Bloom_filter#cite_note-FOOTNOTEMullin1990-26)
- The [Exim](./Exim) mail transfer agent (MTA) uses Bloom filters in its rate-limit feature.[*[citation needed](./Wikipedia:Citation_needed)*]
- [Medium](./Medium_(publishing_platform)) uses Bloom filters to avoid recommending articles a user has previously read.[[27]](./Bloom_filter#cite_note-27)
- [Ethereum](./Ethereum) uses Bloom filters for quickly finding logs on the Ethereum [blockchain](./Blockchain).
- [Grafana](./Grafana) Tempo uses Bloom filters to improve query performance by storing bloom filters for each backend block. These are accessed on each query to determine the blocks containing data that meets the supplied search criteria[[28]](./Bloom_filter#cite_note-28)

 

## Alternatives

 

Classic Bloom filters use     1.44  log  2   ⁡ ⁡  ( 1  /  ε ε  )   {\displaystyle 1.44\log _{2}(1/\varepsilon )}  ![{\displaystyle 1.44\log _{2}(1/\varepsilon )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/42e558468e74f0a363f9195b028cccfc6815dd4f) bits of space per inserted key, where     ε ε    {\displaystyle \varepsilon }  ![{\displaystyle \varepsilon }](https://wikimedia.org/api/rest_v1/media/math/render/svg/a30c89172e5b88edbd45d3e2772c7f5e562e5173) is the false positive rate of the Bloom filter. However, the space that is strictly necessary for any data structure playing the same role as a Bloom filter is only      log  2   ⁡ ⁡  ( 1  /  ε ε  )   {\displaystyle \log _{2}(1/\varepsilon )}  ![{\displaystyle \log _{2}(1/\varepsilon )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/85064930d70b016ae1fab4a755ba68645114a560) per key.[[29]](./Bloom_filter#cite_note-:1-29) Hence Bloom filters use 44% more space than an equivalent optimal data structure.

 

Pagh et al. provide a data structure that uses     ( 1 + o ( 1 ) ) n  log  2   ⁡ ⁡  ( 1  /  ϵ ϵ  ) + O ( n )   {\textstyle (1+o(1))n\log _{2}(1/\epsilon )+O(n)}  ![{\textstyle (1+o(1))n\log _{2}(1/\epsilon )+O(n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/18e83416b0f16964ec3ae6001a237bfc62d33f19) bits while supporting constant amortized expected-time operations.[[30]](./Bloom_filter#cite_note-FOOTNOTEPaghPaghRao2005-30) Their data structure is primarily theoretical, but it is closely related to the widely-used [quotient filter](./Quotient_filter), which can be parameterized to use    ( 1 + δ δ  ) n log ⁡ ⁡   ϵ ϵ   − −  1   + 3 n   {\displaystyle (1+\delta )n\log \epsilon ^{-1}+3n}  ![{\displaystyle (1+\delta )n\log \epsilon ^{-1}+3n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4dffe2a6bd1d71c0d31f3ecb1b130434ad1868f0) bits of space, for an arbitrary parameter     δ δ  > 0   {\displaystyle \delta >0}  ![{\displaystyle \delta >0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/595d5cea06fdcaf2642caf549eda2cfc537958a9), while supporting     O (  δ δ   − −  2   )   {\displaystyle O(\delta ^{-2})}  ![{\displaystyle O(\delta ^{-2})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bd9040cb1f7dbcaa4c2df29023fcf9cc6f6d7572)-time operations.[[31]](./Bloom_filter#cite_note-31) Advantages of the quotient filter, when compared to the Bloom filter, include its [locality of reference](./Locality_of_reference) and the ability to support deletions.

 

Another alternative to classic Bloom filter is the [cuckoo filter](./Cuckoo_filter), based on space-efficient variants of [cuckoo hashing](./Cuckoo_hashing). In this case, a hash table is constructed, holding neither keys nor values, but short fingerprints (small hashes) of the keys.  If looking up the key finds a matching fingerprint, then key is probably in the set.  Cuckoo filters support deletions and have better [locality of reference](./Locality_of_reference) than Bloom filters.[[32]](./Bloom_filter#cite_note-:0-32) Additionally, in some parameter regimes, cuckoo filters can be parameterized to offer nearly optimal space guarantees.[[32]](./Bloom_filter#cite_note-:0-32)

 

Many alternatives to Bloom filters, including [quotient filters](./Quotient_filter) and [cuckoo filters](./Cuckoo_filter), are based on the idea of hashing keys to random     ( log ⁡ ⁡  n + log ⁡ ⁡   ϵ ϵ   − −  1   )   {\displaystyle (\log n+\log \epsilon ^{-1})}  ![{\displaystyle (\log n+\log \epsilon ^{-1})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a7fc471c148cca7fea2739e0c5e86bebf817fcf6)-bit fingerprints, and then storing those fingerprints in a compact hash table. This technique, which was first introduced by Carter et al. in 1978,[[29]](./Bloom_filter#cite_note-:1-29) relies on the fact that compact hash tables can be implemented to use roughly     n log ⁡ ⁡  n   {\displaystyle n\log n}  ![{\displaystyle n\log n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/560dfdce0353a330e03e4b3e0b7ca6e484bb40fb) bits less space than their non-compact counterparts. Using [succinct](./Succinct_data_structure) hash tables, the space usage can be reduced to as little as     n  log  2   ⁡ ⁡  ( e  /  ϵ ϵ  ) + o ( n )   {\displaystyle n\log _{2}(e/\epsilon )+o(n)}  ![{\displaystyle n\log _{2}(e/\epsilon )+o(n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9a86e44e0710b94023a7b4e177402248e031aef6) bits[[33]](./Bloom_filter#cite_note-33) while supporting constant-time operations in a wide variety of parameter regimes.

 

[Putze, Sanders & Singler (2007)](./Bloom_filter#CITEREFPutzeSandersSingler2007) have studied some variants of Bloom filters that are either faster or use less space than classic Bloom filters. The basic idea of the fast variant is to locate the k hash values associated with each key into one or two blocks having the same size as processor's memory cache blocks (usually 64 bytes). This will presumably improve performance by reducing the number of potential memory [cache misses](./Cache_misses). The proposed variants have however the drawback of using about 32% more space than classic Bloom filters.

 

The space efficient variant relies on using a single hash function that generates for each key a value in the range      [  0 , n  /  ε ε   ]    {\displaystyle \left[0,n/\varepsilon \right]}  ![{\displaystyle \left[0,n/\varepsilon \right]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/08fc8018675c0d5ae415f476b94085ff896d18d4) where     ε ε    {\displaystyle \varepsilon }  ![{\displaystyle \varepsilon }](https://wikimedia.org/api/rest_v1/media/math/render/svg/a30c89172e5b88edbd45d3e2772c7f5e562e5173) is the requested false positive rate. The sequence of values is then sorted and compressed using [Golomb coding](./Golomb_coding) (or some other compression technique) to occupy a space close to     n  log  2   ⁡ ⁡  ( 1  /  ε ε  )   {\displaystyle n\log _{2}(1/\varepsilon )}  ![{\displaystyle n\log _{2}(1/\varepsilon )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b9398d00ca80429b8f6cf8111628fe5e5ed927dd) bits. To query the Bloom filter for a given key, it will suffice to check if its corresponding value is stored in the Bloom filter. Decompressing the whole Bloom filter for each query would make this variant totally unusable. To overcome this problem the sequence of  values is divided into small blocks of equal size that are compressed separately. At query time only half a block will need to be decompressed on average. Because of decompression overhead, this variant may be slower than classic Bloom filters but this may be compensated by the fact that a single hash function needs to be computed.

 

[Graf & Lemire (2020)](./Bloom_filter#CITEREFGrafLemire2020) describes an approach called an *xor filter*, where they store fingerprints in a particular type of [perfect hash](./Perfect_hash) table, producing a filter which is more memory efficient (    1.23  log  2   ⁡ ⁡  ( 1  /  ε ε  )   {\displaystyle 1.23\log _{2}(1/\varepsilon )}  ![{\displaystyle 1.23\log _{2}(1/\varepsilon )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/76bfbc0d8fd310413c3bd618731d04a3e595ebb1) bits per key) and faster than Bloom or cuckoo filters.  (The time saving comes from the fact that a lookup requires exactly three memory accesses, which can all execute in parallel.)  However, filter creation is more complex than Bloom and cuckoo filters, and it is not possible to modify the set after creation.

 

## Extensions and applications

 

There are over 60 variants of Bloom filters, many surveys of the field, and a continuing churn of applications (see e.g., Luo, *et al* [[34]](./Bloom_filter#cite_note-autogenerated1-34)). Some of the variants differ sufficiently from the original proposal to be breaches from or forks of the original data structure and its philosophy.[[34]](./Bloom_filter#cite_note-autogenerated1-34) A treatment which unifies Bloom filters with other work on [random projections](./Random_projections), [compressive sensing](./Compressive_sensing), and [locality sensitive hashing](./Locality_sensitive_hashing) remains to be done (though see Dasgupta, *et al*[[35]](./Bloom_filter#cite_note-35) for one attempt inspired by neuroscience).

 

### Cache filtering

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/6/61/BloomFilterDisk.png/500px-BloomFilterDisk.png)](./File:BloomFilterDisk.png)Using a Bloom filter to prevent one-hit-wonders from being stored in a web cache decreased the rate of disk writes by nearly one half, reducing the load on the disks and potentially increasing disk performance.[[13]](./Bloom_filter#cite_note-FOOTNOTEMaggsSitaraman2015-13) 

[Content delivery networks](./Content_delivery_network) deploy [web caches](./Web_cache) around the world to cache and serve web content to users with greater performance and reliability. A key application of Bloom filters is their use in efficiently determining which web objects to store in these web caches.  Nearly three-quarters of the URLs accessed from a typical web cache are "one-hit-wonders" that are accessed by users only once and never again. It is clearly wasteful of disk resources to store one-hit-wonders in a web cache, since they will never be accessed again. To prevent caching one-hit-wonders, a Bloom filter is used to keep track of all URLs that are accessed by users.  A web object is cached only when it has been accessed at least once before, i.e., the object is cached on its second request. The use of a Bloom filter in this fashion significantly reduces the disk write workload, since most one-hit-wonders are not written to the disk cache. Further, filtering out the one-hit-wonders also saves cache space on disk, increasing the cache hit rates.[[13]](./Bloom_filter#cite_note-FOOTNOTEMaggsSitaraman2015-13)

 

### Avoiding false positives in a finite universe

 

Kiss *et al* described a new construction for the Bloom filter that avoids false positives in addition to the typical non-existence of false negatives.[[36]](./Bloom_filter#cite_note-36) The construction applies to a finite universe from which set elements are taken. It relies on existing non-adaptive combinatorial [group testing](./Group_testing) scheme by Eppstein, Goodrich and Hirschberg. Unlike the typical Bloom filter, elements are hashed to a bit array through deterministic, fast and simple-to-calculate functions. The maximal set size for which false positives are completely avoided is a function of the universe size and is controlled by the amount of allocated memory.

 

Alternatively, an initial Bloom filter can be constructed in the standard way and then, with a finite and tractably-enumerable domain, all false positives can be exhaustively found and then a second Bloom filter constructed from that list; false positives in the second filter are similarly handled by constructing a third, and so on. As the universe is finite and the set of false positives strictly shrinks with each step, this procedure results in a finite *cascade* of Bloom filters that (on this closed, finite domain) will produce only true positives and true negatives. To check for membership in the filter cascade, the initial filter is queried, and, if the result is positive, the second filter is then consulted, and so on. This construction is used in [CRLite](./CRLite), a proposed [certificate revocation status](./Certificate_revocation_status) distribution mechanism for the [Web PKI](./Web_PKI?action=edit&redlink=1), and [Certificate Transparency](./Certificate_Transparency) is exploited to close the set of extant certificates.[[37]](./Bloom_filter#cite_note-37)

 

### Counting Bloom filters

 Main article: [Counting Bloom filter](./Counting_Bloom_filter) 

Counting filters provide a way to implement a *delete* operation on a Bloom filter without recreating the filter afresh. In a counting filter, the array positions (buckets) are extended from being a single bit to being a multibit counter. In fact, regular Bloom filters can be considered as counting filters with a bucket size of one bit. Counting filters were introduced by [Fan et al. (2000)](./Bloom_filter#CITEREFFanCaoAlmeidaBroder2000).

 

The insert operation is extended to *increment* the value of the buckets, and the lookup operation checks that each of the required buckets is non-zero. The delete operation then consists of decrementing the value of each of the respective buckets.

 

[Arithmetic overflow](./Arithmetic_overflow) of the buckets is a problem and the buckets should be sufficiently large to make this case rare. If it does occur then the increment and decrement operations must leave the bucket set to the maximum possible value in order to retain the properties of a Bloom filter.

 

The size of counters is usually 3 or 4 bits. Hence counting Bloom filters use 3 to 4 times more space than static Bloom filters. In contrast, the data structures of [Pagh, Pagh & Rao (2005)](./Bloom_filter#CITEREFPaghPaghRao2005) and [Fan et al. (2014)](./Bloom_filter#CITEREFFanAndersenKaminskyMitzenmacher2014) also allow deletions but use less space than a static Bloom filter.

 

Another issue with counting filters is limited scalability. Because the counting Bloom filter table cannot be expanded, the maximal number of keys to be stored simultaneously in the filter must be known in advance. Once the designed capacity of the table is exceeded, the false positive rate will grow rapidly as more keys are inserted.

 

[Bonomi et al. (2006)](./Bloom_filter#CITEREFBonomiMitzenmacherPanigrahySingh2006) introduced a data structure based on d-left hashing that is functionally equivalent  but uses approximately half as much space as counting Bloom filters. The scalability issue does not occur in this data structure. Once the designed capacity is exceeded, the keys could be reinserted in a new hash table of double size.

 

The space efficient variant by [Putze, Sanders & Singler (2007)](./Bloom_filter#CITEREFPutzeSandersSingler2007) could also be used to implement counting filters by supporting insertions and deletions.

 

[Rottenstreich, Kanizo & Keslassy (2012)](./Bloom_filter#CITEREFRottenstreichKanizoKeslassy2012) introduced a new general method based on variable increments that significantly improves the false positive probability of counting Bloom filters and their variants, while still supporting deletions. Unlike counting Bloom filters, at each element insertion, the hashed counters are incremented by a hashed variable increment instead of a unit increment. To query an element, the exact values of the counters are considered and not just their positiveness. If a sum represented by a counter value cannot be composed of the corresponding variable increment for the queried element, a negative answer can be returned to the query.

 

[Kim et al. (2019)](https://www.mdpi.com/2079-9292/8/7/779) shows that false positive of Counting Bloom filter decreases from k=1 to a point defined      k  o p t     {\displaystyle k_{opt}}  ![{\displaystyle k_{opt}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6780d4f16c1df91b33e954ad94651eca4fa1c9d2), and increases from      k  o p t     {\displaystyle k_{opt}}  ![{\displaystyle k_{opt}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6780d4f16c1df91b33e954ad94651eca4fa1c9d2)to positive infinity, and finds      k  o p t     {\displaystyle k_{opt}}  ![{\displaystyle k_{opt}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6780d4f16c1df91b33e954ad94651eca4fa1c9d2)as a function of count threshold.[[38]](./Bloom_filter#cite_note-38)

 

### Decentralized aggregation

 

Bloom filters can be organized in distributed [data structures](./Data_structures) to perform fully decentralized computations of [aggregate functions](./Aggregate_function). Decentralized aggregation makes collective measurements locally available in every node of a distributed network without involving a centralized computational entity for this purpose.[[39]](./Bloom_filter#cite_note-FOOTNOTEPournarasWarnierBrazier2013-39)

 

### Distributed Bloom filters

 [![](//upload.wikimedia.org/wikipedia/commons/5/5a/DistributedBloomFilterExample.png)](./File:DistributedBloomFilterExample.png)Distributed Single Shot Bloom filter for duplicate detection with false positive rate: 6 elements are distributed over 3 PEs, each with a bit array of length 4. During the first communication step PE 1 receives the hash '2' twice and sends it back to either PE 2 or 3, depending on who sent it later. The PE that receives the hash '2' then searches for the element with that hash and marks it as possible duplicate. 

Parallel Bloom filters can be implemented to take advantage of the multiple [processing elements](./Processing_element) (PEs) present in [parallel shared-nothing machines](./Shared-nothing_architecture). One of the main obstacles for a parallel Bloom filter is the organization and communication of the unordered data which is, in general, distributed evenly over all PEs at the initiation or at batch insertions. To order the data two approaches can be used, either resulting in a Bloom filter over all data being stored on each PE, called replicating bloom filter, or the Bloom filter over all data being split into equal parts, each PE storing one part of it.[[40]](./Bloom_filter#cite_note-40) For both approaches a "Single Shot" Bloom filter is used which only calculates one hash, resulting in one flipped bit per element, to reduce the communication volume.

 

**Distributed Bloom filters** are initiated by first hashing all elements on their local PE and then sorting them by their hashes locally. This can be done in linear time using e.g. [Bucket sort](./Bucket_sort) and also allows local duplicate detection. The sorting is used to group the hashes with their assigned PE as separator to create a Bloom filter for each group. After encoding these Bloom filters using e.g. [Golomb coding](./Golomb_coding) each bloom filter is sent as packet to the PE responsible for the hash values that where inserted into it. A PE p is responsible for all hashes between the values     p ∗ ∗  ( s  /   |   PE   |  )   {\displaystyle p*(s/|{\text{PE}}|)}  ![{\displaystyle p*(s/|{\text{PE}}|)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6786c822734bfe7f8e8c9ee0bc48ee4a26492e28) and     ( p + 1 ) ∗ ∗  ( s  /   |   PE   |  )   {\displaystyle (p+1)*(s/|{\text{PE}}|)}  ![{\displaystyle (p+1)*(s/|{\text{PE}}|)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fa10a725d0f72bd66294a701aa1635640c802728), where s is the total size of the Bloom filter over all data. Because each element is only hashed once and therefore only a single bit is set, to check if an element was inserted into the Bloom filter only the PE responsible for the hash value of the element needs to be operated on. Single insertion operations can also be done efficiently because the Bloom filter of only one PE has to be changed, compared to Replicating Bloom filters where every PE would have to update its Bloom filter. 
By distributing the global Bloom filter over all PEs instead of storing it separately on each PE the Bloom filters size can be far larger, resulting in a larger capacity and lower false positive rate. 

Distributed Bloom filters can be used to improve duplicate detection algorithms[[41]](./Bloom_filter#cite_note-41) by filtering out the most 'unique' elements. These can be calculated by communicating only the hashes of elements, not the elements themselves which are far larger in volume, and removing them from the set, reducing the workload for the duplicate detection algorithm used afterwards.

 

During the communication of the hashes the PEs search for bits that are set in more than one of the receiving packets, as this would mean that two elements had the same hash and therefore could be duplicates. If this occurs a message containing the index of the bit, which is also the hash of the element that could be a duplicate, is sent to the PEs which sent a packet with the set bit. If multiple indices are sent to the same PE by one sender it can be advantageous to encode the indices as well. All elements that didn't have their hash sent back are now guaranteed to not be a duplicate and won't be evaluated further, for the remaining elements a Repartitioning algorithm[[42]](./Bloom_filter#cite_note-42) can be used. First all the elements that had their hash value sent back are sent to the PE that their hash is responsible for. Any element and its duplicate is now guaranteed to be on the same PE. In the second step each PE uses a [sequential algorithm](./Sequential_algorithm) for duplicate detection on the receiving elements, which are only a fraction of the amount of starting elements. By allowing a false positive rate for the duplicates, the communication volume can be reduced further as the PEs don't have to send elements with duplicated hashes at all and instead any element with a duplicated hash can simply be marked as a duplicate. As a result, the false positive rate for duplicate detection is the same as the false positive rate of the used bloom filter.

 

The process of filtering out the most 'unique' elements can also be repeated multiple times by changing the hash function in each filtering step. If only a single filtering step is used it has to archive a small false positive rate, however if the filtering step is repeated once the first step can allow a higher false positive rate while the latter one has a higher one but also works on less elements as many have already been removed by the earlier filtering step. While using more than two repetitions can reduce the communication volume further if the number of duplicates in a set is small, the payoff for the additional complications is low.

 

**Replicating Bloom filters** organize their data by using a well known [hypercube](./Hypercube) algorithm for gossiping, e.g.[[43]](./Bloom_filter#cite_note-43) First each PE calculates the Bloom filter over all local elements and stores it. By repeating a loop where in each step i the PEs send their local Bloom filter over dimension i and merge the Bloom filter they receive over the dimension with their local Bloom filter, it is possible to double the elements each Bloom filter contains in every iteration. After sending and receiving Bloom filters over all     log ⁡ ⁡   |   PE   |    {\displaystyle \log |{\text{PE}}|}  ![{\displaystyle \log |{\text{PE}}|}](https://wikimedia.org/api/rest_v1/media/math/render/svg/77aaef845ab84f603f6d3ccc0be201786d17ffac) dimensions each PE contains the global Bloom filter over all elements.

 

Replicating Bloom filters are more efficient when the number of queries is much larger than the number of elements that the Bloom filter contains, the break even point compared to Distributed Bloom filters is approximately after      |   PE   |  ∗ ∗   |   Elements   |   /   log   f  +     ⁡ ⁡   |   PE   |    {\displaystyle |{\text{PE}}|*|{\text{Elements}}|/\log _{f^{\text{+}}}|{\text{PE}}|}  ![{\displaystyle |{\text{PE}}|*|{\text{Elements}}|/\log _{f^{\text{+}}}|{\text{PE}}|}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c805858cf0b197e637608dd351878b9271a5c7e7) accesses, with      f  +     {\displaystyle f^{\text{+}}}  ![{\displaystyle f^{\text{+}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5186b019abbafe4420e9650c7e80072f522738e9) as the false positive rate of the bloom filter.

 

### Data synchronization

 

Bloom filters can be used for approximate [data synchronization](./Data_synchronization) as in [Byers et al. (2004)](./Bloom_filter#CITEREFByersConsidineMitzenmacherRost2004).  Counting Bloom filters can be used to approximate the number of differences between two sets and this approach is described in [Agarwal & Trachtenberg (2006)](./Bloom_filter#CITEREFAgarwalTrachtenberg2006).

 

### Bloom filters for streaming data

 

Bloom filters can be adapted to the context of streaming data. For instance, [Deng & Rafiei (2006)](./Bloom_filter#CITEREFDengRafiei2006) proposed Stable Bloom filters, which consist of a counting Bloom filter where insertion of a new element sets the associated counters to a value c, and then only a fixed amount s of counters are decreased by 1, hence the memory mostly contains information about recent elements (intuitively, one could assume that the lifetime of an element inside a SBF of N counters is around     c    s N      {\displaystyle c{\tfrac {s}{N}}}  ![{\displaystyle c{\tfrac {s}{N}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4dc142b7d41be8223239a4cfded3ee0156b307c4)). Another solution is the Aging Bloom filter, that consists of two Bloom filter each occupying half the total available memory: when one filter is full, the second filter is erased and newer elements are then added to this newly empty filter.[[44]](./Bloom_filter#cite_note-AgingBloom-44)

 

However, it has been shown[[45]](./Bloom_filter#cite_note-45) that no matter the filter, after n insertions, the sum of the false positive     F P   {\displaystyle FP}  ![{\displaystyle FP}](https://wikimedia.org/api/rest_v1/media/math/render/svg/79879ec9236e6d6a087517c11e2638827c09595a) and false negative     F N   {\displaystyle FN}  ![{\displaystyle FN}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4e1c5b779dac08ca6c5a0bb2cc3d64e8375b5941) probabilities is bounded below by     F P + F N ≥ ≥  1 − −     1 − −    (  1 − −    1 L    )   m     1 − −    (  1 − −    1 L    )   n        {\displaystyle FP+FN\geq 1-{\frac {1-\left(1-{\frac {1}{L}}\right)^{m}}{1-\left(1-{\frac {1}{L}}\right)^{n}}}}  ![{\displaystyle FP+FN\geq 1-{\frac {1-\left(1-{\frac {1}{L}}\right)^{m}}{1-\left(1-{\frac {1}{L}}\right)^{n}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ebe449291a953f8f777b1e91c61e31296c0527f9) where L is the amount of all possible elements (the alphabet size), m the memory size (in bits), assuming     n > m   {\displaystyle n>m}  ![{\displaystyle n>m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e64e2a4a5b6cb58f1553c6a65551b4898bb82403). This result shows that for L big enough and n going to infinity, then the lower bound converges to     F P + F N = 1   {\displaystyle FP+FN=1}  ![{\displaystyle FP+FN=1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3e3bd559e525984b8e54b4573a92281772002bba), which is the characteristic relation of a random filter. Hence, after enough insertions, and if the alphabet is too big to be stored in memory (which is assumed in the context of probabilistic filters), it is impossible for a filter to perform better than randomness. This result can be leveraged by only expecting a filter to operate on a sliding window rather than the whole stream. In this case, the exponent n in the formula above is replaced by w, which gives a formula that might deviate from 1, if w is not too small.

 

### Bloomier filters

 

[Chazelle et al. (2004)](./Bloom_filter#CITEREFChazelleKilianRubinfeldTal2004) designed a generalization of Bloom filters that could associate a value with each element that had been inserted, implementing an [associative array](./Associative_array). Like Bloom filters, these structures achieve a small space overhead by accepting a small probability of false positives. In the case of "Bloomier filters", a *false positive* is defined as returning a result when the key is not in the map. The map will never return the wrong value for a key that *is* in the map.

  too wordy for an alternative to the article topic. commented out in case someone wants to move it to a new article.
The simplest Bloomier filter is near&#x2D;optimal and fairly simple to describe. Suppose initially that the only possible values are 0 and 1. We create a pair of Bloom filters ''A''<sub&#x3E;0</sub&#x3E; and ''B''<sub&#x3E;0</sub&#x3E; which contain, respectively, all keys mapping to 0 and all keys mapping to 1. Then, to determine which value a given key maps to, we look it up in both filters. If it is in neither, then the key is not in the map. If the key is in ''A''<sub&#x3E;0</sub&#x3E; but not ''B''<sub&#x3E;0</sub&#x3E;, then it does not map to 1, and has a high probability of mapping to 0. Conversely, if the key is in ''B''<sub&#x3E;0</sub&#x3E; but not ''A''<sub&#x3E;0</sub&#x3E;, then it does not map to 0 and has a high probability of mapping to 1.

A problem arises, however, when ''both'' filters claim to contain the key. We never insert a key into both, so one or both of the filters is lying (producing a false positive), but we don't know which. To determine this, we have another, smaller pair of filters ''A''<sub&#x3E;1</sub&#x3E; and ''B''<sub&#x3E;1</sub&#x3E;. ''A''<sub&#x3E;1</sub&#x3E; contains keys that map to 0 and which are false positives in ''B''<sub&#x3E;0</sub&#x3E;; ''B''<sub&#x3E;1</sub&#x3E; contains keys that map to 1 and which are false positives in ''A''<sub&#x3E;0</sub&#x3E;. But whenever ''A''<sub&#x3E;0</sub&#x3E; and ''B''<sub&#x3E;0</sub&#x3E; both produce positives, at most one of these cases must occur, and so we simply have to determine which if any of the two filters ''A''<sub&#x3E;1</sub&#x3E; and ''B''<sub&#x3E;1</sub&#x3E; contains the key, another instance of our original problem.

It may so happen again that both filters produce a positive; we apply the same idea recursively to solve this problem. Because each pair of filters only contains keys that are in the map ''and'' produced false positives on all previous filter pairs, the number of keys is extremely likely to quickly drop to a very small quantity that can be easily stored in an ordinary deterministic map, such as a pair of small arrays with linear search. Moreover, the average total search time is low, because almost all queries will be resolved by the first pair, almost all remaining queries by the second pair, and so on. The total space required is in practice independent of ''n'', and is almost entirely occupied by the first filter pair.

Now that we have the structure and a search algorithm, we also need to know how to insert new key/value pairs. The program must not attempt to insert the same key with both values. If the value is 0, insert the key into ''A''<sub&#x3E;0</sub&#x3E; and then test if the key is in ''B''<sub&#x3E;0</sub&#x3E;. If so, this is a false positive for ''B''<sub&#x3E;0</sub&#x3E;, and the key must also be inserted into ''A''<sub&#x3E;1</sub&#x3E; recursively in the same manner. If we reach the last level, we simply insert it. When the value is 1, the operation is similar but with ''A'' and ''B'' reversed.

Now that we can map a key to the value 0 or 1, how does this help us map to general values? This is simple. We create a single such Bloomier filter for each bit of the result. If the values are large, we can instead map keys to hash values that can be used to retrieve the actual values. The space required for a Bloomier filter with ''n''&#x2D;bit values is typically slightly more than the space for 2''n'' Bloom filters.

A very simple way to implement Bloomier filters is by means of minimal [[perfect hashing]]. A minimal perfect hash function h is first generated for the set of n keys. Then an array is filled with n pairs (signature,value) associated with each key at the positions given by function h when applied on each key. The signature of a key is a string of r bits computed by applying a hash function g of range <math&#x3E;2^r</math&#x3E; on the key. The value of r is chosen such that <math&#x3E;2^r&#x3E;=1/\varepsilon</math&#x3E;, where <math&#x3E;\varepsilon</math&#x3E; is the requested false positive rate. To query for a given key, hash function h is first applied on the key. This will give a position into the array from which we retrieve a pair (signature,value). Then we compute the signature of the key using function g. If the computed signature is the same as retrieved signature we return the retrieved value. The probability of false positive is <math&#x3E;1/2^r</math&#x3E;.

Another alternative to implement static Bloomier and Bloom filters based on matrix solving has been simultaneously proposed in {{harvtxt|Porat|2008}}, {{harvtxt|Dietzfelbinger|Pagh|2008}} and {{harvtxt|Charles|Chellapilla|2008}}. The space usage of this method is optimal as it needs only <math&#x3E;\log_2(\varepsilon)</math&#x3E; bits per key for a Bloom filter. However time to generate the Bloom or Bloomier filter can be very high. The generation  time can be reduced to a reasonable value at the price of a small increase in space usage.

Dynamic Bloomier filters have been studied by {{harvtxt|Mortensen|Pagh|Pătrașcu|2005}}. They proved that any dynamic Bloomier filter needs at least around
<math&#x3E;\log(l)</math&#x3E; bits per key where l is the length of the key. A simple dynamic version of Bloomier filters can be implemented using two dynamic data structures. Let the two data structures be noted S1 and S2. S1 will store keys with their associated data while S2 will only store signatures of keys with their associated data. Those signatures are simply hash values of keys in the range <math&#x3E;[0,n/\varepsilon]</math&#x3E; where n is the maximal number of keys to be stored in the Bloomier filter and <math&#x3E;\varepsilon</math&#x3E; is the requested false positive rate. To insert a key in the Bloomier filter, its hash value is first computed. Then the algorithm checks if a key with the same hash value already exists in S2. If this is not the case, the hash value is inserted in S2 along with data associated with the key. If the same hash value already exists in S2 then the key is inserted into S1 along with its associated data. The deletion is symmetric: if the key already exists in S1 it will be deleted from there, otherwise the hash value associated with the key is deleted from S2. An issue with this algorithm is on how to store efficiently S1 and S2. For S1 any hash algorithm can be used. To store S2 [[golomb coding]] could be applied to compress signatures to use a space close to <math&#x3E;\log2(1/\varepsilon)</math&#x3E; per key.  

### Compact approximators

 

[Boldi & Vigna (2005)](./Bloom_filter#CITEREFBoldiVigna2005) proposed a [lattice](./Lattice_(order))-based generalization of Bloom filters. A **compact approximator** associates to each key an element of a lattice (the standard Bloom filters being the case of the Boolean two-element lattice). Instead of a bit array, they have an array of lattice elements. When adding a new association between a key and an element of the lattice, they compute the maximum of the current contents of the k array locations associated to the key with the lattice element. When reading the value associated to a key, they compute the minimum of the values found in the k locations associated to the key. The resulting value approximates from above the original value.

 

### Parallel-partitioned Bloom filters

 

This implementation used a separate array for each hash function. This method allows for parallel hash calculations for both insertions and inquiries.[[46]](./Bloom_filter#cite_note-46)

 

### Scalable Bloom filters

 

[Almeida et al. (2007)](./Bloom_filter#CITEREFAlmeidaBaqueroPreguicaHutchison2007) proposed a variant of Bloom filters that can adapt dynamically to the number of elements stored, while assuring a minimum false positive probability. The technique is based on sequences of standard Bloom filters with increasing capacity and tighter false positive probabilities, so as to ensure that a maximum false positive probability can be set beforehand, regardless of the number of elements to be inserted.

 

### Spatial Bloom filters

 

Spatial Bloom filters (SBF) were originally proposed by [Palmieri, Calderoni & Maio (2014)](./Bloom_filter#CITEREFPalmieriCalderoniMaio2014) as a data structure designed to store [location information](./Location_information), especially in the context of cryptographic protocols for location [privacy](./Information_privacy). However, the main characteristic of SBFs is their ability to store **multiple sets** in a single data structure, which makes them suitable for a number of different application scenarios.[[47]](./Bloom_filter#cite_note-FOOTNOTECalderoniPalmieriMaio2015-47) Membership of an element to a specific set can be queried, and the false positive probability depends on the set: the first sets to be entered into the filter during construction have higher false positive probabilities than sets entered at the end.[[48]](./Bloom_filter#cite_note-FOOTNOTECalderoniPalmieriMaio2018-48) This property allows a prioritization of the sets, where sets containing more "important" elements can be preserved.

 

### Layered Bloom filters

 

A layered Bloom filter consists of multiple Bloom filter layers. Layered Bloom filters allow keeping track of how many times an item was added to the Bloom filter by checking how many layers contain the item. With a layered Bloom filter a check operation will normally return the deepest layer number the item was found in.[[49]](./Bloom_filter#cite_note-FOOTNOTEZhiwangJungangJian2010-49)

 

### Attenuated Bloom filters

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/d/d8/AttenuatedBloomFilter2.png/250px-AttenuatedBloomFilter2.png)](./File:AttenuatedBloomFilter2.png)Attenuated Bloom filter example: Search for pattern 11010, starting from node n1. 

An attenuated Bloom filter of depth D can be viewed as an array of D normal Bloom filters. In the context of [service discovery](./Service_discovery) in a network, each node stores regular and attenuated Bloom filters locally. The regular or local Bloom filter indicates which services are offered by the node itself. The attenuated filter of level i indicates which services can be found on nodes that are i-hops away from the current node. The i-th value is constructed by taking a union of local Bloom filters for nodes i-hops away from the node.[[50]](./Bloom_filter#cite_note-FOOTNOTEKoucheryavyGiambeneStaehleBarcelo-Arroyo2009-50)

 

For example, consider a small network, shown on the graph below. Say we are searching for a service A whose id hashes to bits 0,1, and 3 (pattern 11010). Let n1 node to be the starting point. First, we check whether service A is offered by n1 by checking its local filter. Since the patterns don't match, we check the attenuated Bloom filter in order to determine which node should be the next hop. We see that n2 doesn't offer service A but lies on the path to nodes that do. Hence, we move to n2 and repeat the same procedure. We quickly find that n3 offers the service, and hence the destination is located.[[51]](./Bloom_filter#cite_note-FOOTNOTEKubiatowiczBindelCzerwinskiGeels2000-51)

 

By using attenuated Bloom filters consisting of multiple layers, services at more than one hop distance can be discovered while avoiding saturation of the Bloom filter by attenuating (shifting out) bits set by sources further away.[[50]](./Bloom_filter#cite_note-FOOTNOTEKoucheryavyGiambeneStaehleBarcelo-Arroyo2009-50)

 

### Chemical structure searching

 

Bloom filters are often used to search large chemical structure databases (see [chemical similarity](./Chemical_similarity)). In the simplest case, the elements added to the filter (called a *fingerprint* in this field) are just the atomic numbers present in the molecule, or a hash based on the [atomic number](./Atomic_number) of each atom and the number and type of its bonds. This case is too simple to be useful. More advanced filters also encode atom counts, larger substructure features like carboxyl groups, and graph properties like the number of rings. In hash-based fingerprints, a hash function based on atom and bond properties is used to turn a subgraph into a [PRNG](./Pseudorandom_number_generator) seed, and the first output values used to set bits in the Bloom filter.

 

Molecular fingerprints started in the late 1940s as way to search for chemical structures searched on punched cards. However, it wasn't until around 1990 that Daylight Chemical Information Systems, Inc. introduced a hash-based method to generate the bits, rather than use a precomputed table. Unlike the dictionary approach, the hash method can assign bits for substructures which hadn't previously been seen. In the early 1990s, the term "fingerprint" was considered different from "structural keys", but the term has since grown to encompass most molecular characteristics which can be used for a similarity comparison, including structural keys, sparse count fingerprints, and 3D fingerprints. Unlike Bloom filters, the Daylight hash method allows the number of bits assigned per feature to be a function of the feature size, but most implementations of Daylight-like fingerprints use a fixed number of bits per feature, which makes them a Bloom filter. The original Daylight fingerprints could be used for both similarity and screening purposes. Many other fingerprint types, like the popular ECFP2, can be used for similarity but not for screening because they include local environmental characteristics that introduce false negatives when used as a screen. Even if these are constructed with the same mechanism, these are not Bloom filters because they cannot be used to filter.

 

## See also

 
- [![icon](//upload.wikimedia.org/wikipedia/commons/thumb/6/6f/Octicons-terminal.svg/40px-Octicons-terminal.svg.png)](./File:Octicons-terminal.svg)[Computer programming portal](./Portal:Computer_programming)

 
- [Count–min sketch](./Count–min_sketch) – Probabilistic data structure in computer science
- [Feature hashing](./Feature_hashing) – Vectorizing features using a hash function
- [MinHash](./MinHash) – Data mining technique
- [Quotient filter](./Quotient_filter)
- [Skip list](./Skip_list) – Probabilistic data structure
- [Bloom filters in bioinformatics](./Bloom_filters_in_bioinformatics)
- [Cuckoo filter](./Cuckoo_filter) – Data structure for approximate set membership

 

## References

 
|  | This articlehas an unclearcitation style.The references used may be made clearer with a different or consistent style ofcitationandfootnoting.(August 2023)(Learn how and when to remove this message) |
| --- | --- |

 

### Citations

 
1. [↑](./Bloom_filter#cite_ref-FOOTNOTEBloom1970_1-0) [Bloom (1970)](./Bloom_filter#CITEREFBloom1970).
2. [↑](./Bloom_filter#cite_ref-FOOTNOTEBonomiMitzenmacherPanigrahySingh2006_2-0) [Bonomi et al. (2006)](./Bloom_filter#CITEREFBonomiMitzenmacherPanigrahySingh2006).
3. [↑](./Bloom_filter#cite_ref-3) [Dillinger & Manolios (2004a)](./Bloom_filter#CITEREFDillingerManolios2004a); [Kirsch & Mitzenmacher (2006)](./Bloom_filter#CITEREFKirschMitzenmacher2006).
4. [↑](./Bloom_filter#cite_ref-FOOTNOTEMitzenmacherUpfal2005_4-0) [Mitzenmacher & Upfal (2005)](./Bloom_filter#CITEREFMitzenmacherUpfal2005).
5. [↑](./Bloom_filter#cite_ref-5) [Blustein & El-Maazawi (2002)](./Bloom_filter#CITEREFBlusteinEl-Maazawi2002), pp. 21–22
6. [↑](./Bloom_filter#cite_ref-6) Gopinathan, Kiran; Sergey, Ilya (2020-07-21). "Certifying Certainty and Uncertainty in Approximate Membership Query Structures". *Computer Aided Verification*. Lecture Notes in Computer Science. Vol. 12225. Springer, Cham. pp. 279–303. [doi](./Doi_(identifier)):[10.1007/978-3-030-53291-8_16](https://doi.org/10.1007%2F978-3-030-53291-8_16). [ISBN](./ISBN_(identifier)) [978-3-030-53290-1](./Special:BookSources/978-3-030-53290-1). [PMC](./PMC_(identifier)) [7363400](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7363400).
7. [↑](./Bloom_filter#cite_ref-7) [Mitzenmacher & Upfal (2005)](./Bloom_filter#CITEREFMitzenmacherUpfal2005), pp. 109–111, 308.
8. [↑](./Bloom_filter#cite_ref-8) [Mitzenmacher & Upfal (2005)](./Bloom_filter#CITEREFMitzenmacherUpfal2005), p. 308.
9. [↑](./Bloom_filter#cite_ref-9) [Starobinski, Trachtenberg & Agarwal (2003)](./Bloom_filter#CITEREFStarobinskiTrachtenbergAgarwal2003)
10. [↑](./Bloom_filter#cite_ref-10) [Goel & Gupta (2010)](./Bloom_filter#CITEREFGoelGupta2010)
11. [1](./Bloom_filter#cite_ref-Swamidass_2007_11-0) [2](./Bloom_filter#cite_ref-Swamidass_2007_11-1) Swamidass, S. Joshua; Baldi, Pierre (2007). "Mathematical correction for fingerprint similarity measures to improve chemical retrieval". *Journal of Chemical Information and Modeling*. **47** (3): 952–964. [doi](./Doi_(identifier)):[10.1021/ci600526a](https://doi.org/10.1021%2Fci600526a). [PMID](./PMID_(identifier)) [17444629](https://pubmed.ncbi.nlm.nih.gov/17444629).
12. [↑](./Bloom_filter#cite_ref-12) Dasgupta, Sanjoy; Sheehan, Timothy C.; Stevens, Charles F.; Navlakha, Saket (2018-12-18). ["A neural data structure for novelty detection"](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6304992). *Proceedings of the National Academy of Sciences*. **115** (51): 13093–13098. [Bibcode](./Bibcode_(identifier)):[2018PNAS..11513093D](https://ui.adsabs.harvard.edu/abs/2018PNAS..11513093D). [doi](./Doi_(identifier)):[10.1073/pnas.1814448115](https://doi.org/10.1073%2Fpnas.1814448115). [ISSN](./ISSN_(identifier)) [0027-8424](https://search.worldcat.org/issn/0027-8424). [PMC](./PMC_(identifier)) [6304992](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6304992). [PMID](./PMID_(identifier)) [30509984](https://pubmed.ncbi.nlm.nih.gov/30509984).
13. [1](./Bloom_filter#cite_ref-FOOTNOTEMaggsSitaraman2015_13-0) [2](./Bloom_filter#cite_ref-FOOTNOTEMaggsSitaraman2015_13-1) [3](./Bloom_filter#cite_ref-FOOTNOTEMaggsSitaraman2015_13-2) [Maggs & Sitaraman (2015)](./Bloom_filter#CITEREFMaggsSitaraman2015).
14. [↑](./Bloom_filter#cite_ref-14) ["Bloom index contrib module"](https://web.archive.org/web/20180909043421/https://git.postgresql.org/gitweb/?p=postgresql.git;a=commitdiff;h=9ee014fc899a28a198492b074e32b60ed8915ea9). Postgresql.org. 2016-04-01. Archived from [the original](https://git.postgresql.org/gitweb/?p=postgresql.git;a=commitdiff;h=9ee014fc899a28a198492b074e32b60ed8915ea9) on 2018-09-09. Retrieved 2016-06-18.
15. [↑](./Bloom_filter#cite_ref-15) [Chang et al. (2006)](./Bloom_filter#CITEREFChangDeanGhemawatHsieh2006); [Apache Software Foundation (2012)](./Bloom_filter#CITEREFApache_Software_Foundation2012).
16. [↑](./Bloom_filter#cite_ref-16) Yakunin, Alex (2010-03-25). ["Alex Yakunin's blog: Nice Bloom filter application"](https://web.archive.org/web/20101027012345/http://blog.alexyakunin.com/2010/03/nice-bloom-filter-application.html). Blog.alexyakunin.com. Archived from [the original](http://blog.alexyakunin.com/2010/03/nice-bloom-filter-application.html) on 2010-10-27. Retrieved 2014-05-31.
17. [↑](./Bloom_filter#cite_ref-17) ["Issue 10896048: Transition safe browsing from bloom filter to prefix set. - Code Review"](https://chromiumcodereview.appspot.com/10896048/). Chromiumcodereview.appspot.com. Retrieved 2014-07-03.
18. [↑](./Bloom_filter#cite_ref-18) Jones, J. C. (2020-01-09). ["Introducing CRLite: All of the Web PKI's revocations, compressed"](https://blog.mozilla.org/security/2020/01/09/crlite-part-1-all-web-pki-revocations-compressed). *Mozilla Security Blog*. Retrieved 2026-01-12.
19. [↑](./Bloom_filter#cite_ref-19) Jones, J. C. (2020-01-09). ["The End-to-End Design of CRLite"](https://blog.mozilla.org/security/2020/01/09/crlite-part-2-end-to-end-design). *Mozilla Security Blog*. Retrieved 2026-01-12.
20. [↑](./Bloom_filter#cite_ref-20) Colville, Stuart (2020-08-24). ["Introducing a scalable add-ons blocklist"](https://blog.mozilla.org/addons/2020/08/24/introducing-a-scalable-add-ons-blocklist). *Mozilla Add-ons Community Blog*. Retrieved 2026-01-12.
21. [↑](./Bloom_filter#cite_ref-21) Goodwin, Bob; Hopcroft, Michael; Luu, Dan; Clemmer, Alex; Curmei, Mihaela; Elnikety, Sameh; Yuxiong, He (2017). ["BitFunnel: Revisiting Signatures for Search"](https://danluu.com/bitfunnel-sigir.pdf) (PDF). *Proceedings of the 40th International ACM SIGIR Conference on Research and Development in Information Retrieval*. pp. 605–614. [doi](./Doi_(identifier)):[10.1145/3077136.3080789](https://doi.org/10.1145%2F3077136.3080789). [ISBN](./ISBN_(identifier)) [978-1-4503-5022-8](./Special:BookSources/978-1-4503-5022-8). [S2CID](./S2CID_(identifier)) [20123252](https://api.semanticscholar.org/CorpusID:20123252).
22. [↑](./Bloom_filter#cite_ref-FOOTNOTEWessels2004_22-0) [Wessels (2004)](./Bloom_filter#CITEREFWessels2004).
23. [↑](./Bloom_filter#cite_ref-23) ["Bloom Filter | River Glossary"](https://river.com/learn/terms/b/bloom-filter/). *River Financial*. Retrieved 2020-11-14.
24. [↑](./Bloom_filter#cite_ref-24) ["Plan 9 /sys/man/8/venti"](https://web.archive.org/web/20140828071451/http://plan9.bell-labs.com/magic/man2html/8/venti). Plan9.bell-labs.com. Archived from [the original](http://plan9.bell-labs.com/magic/man2html/8/venti) on 2014-08-28. Retrieved 2014-05-31.
25. [↑](./Bloom_filter#cite_ref-25) ["Spin - Formal Verification"](http://spinroot.com/).
26. [↑](./Bloom_filter#cite_ref-FOOTNOTEMullin1990_26-0) [Mullin (1990)](./Bloom_filter#CITEREFMullin1990).
27. [↑](./Bloom_filter#cite_ref-27) ["What are Bloom filters?"](https://medium.com/the-story/what-are-bloom-filters-1ec2a50c68ff#.xlkqtn1vy). Medium. 2015-07-15. Retrieved 2015-11-01.
28. [↑](./Bloom_filter#cite_ref-28) ["Grafana Tempo Documentation - Caching"](https://grafana.com/docs/tempo/latest/operations/caching/). Grafana. Retrieved 2022-11-16.
29. [1](./Bloom_filter#cite_ref-:1_29-0) [2](./Bloom_filter#cite_ref-:1_29-1) Carter, Larry; Floyd, Robert; Gill, John; Markowsky, George; Wegman, Mark (1978). ["Exact and approximate membership testers"](https://dx.doi.org/10.1145/800133.804332). *Proceedings of the tenth annual ACM symposium on Theory of computing - STOC '78*. New York, New York, USA: ACM Press. pp. 59–65. [doi](./Doi_(identifier)):[10.1145/800133.804332](https://doi.org/10.1145%2F800133.804332). [S2CID](./S2CID_(identifier)) [6465743](https://api.semanticscholar.org/CorpusID:6465743).
30. [↑](./Bloom_filter#cite_ref-FOOTNOTEPaghPaghRao2005_30-0) [Pagh, Pagh & Rao (2005)](./Bloom_filter#CITEREFPaghPaghRao2005).
31. [↑](./Bloom_filter#cite_ref-31) Bender, Michael A.; Farach-Colton, Martin; Johnson, Rob; Kraner, Russell; Kuszmaul, Bradley C.; Medjedovic, Dzejla; Montes, Pablo; Shetty, Pradeep; Spillane, Richard P.; Zadok, Erez (July 2012). ["Don't thrash"](https://dx.doi.org/10.14778/2350229.2350275). *Proceedings of the VLDB Endowment*. **5** (11): 1627–1637. [doi](./Doi_(identifier)):[10.14778/2350229.2350275](https://doi.org/10.14778%2F2350229.2350275). [ISSN](./ISSN_(identifier)) [2150-8097](https://search.worldcat.org/issn/2150-8097). [S2CID](./S2CID_(identifier)) [47180056](https://api.semanticscholar.org/CorpusID:47180056).
32. [1](./Bloom_filter#cite_ref-:0_32-0) [2](./Bloom_filter#cite_ref-:0_32-1) Even, Tomer; Even, Guy; Morrison, Adam (March 2022). ["Prefix filter"](https://dx.doi.org/10.14778/3523210.3523211). *Proceedings of the VLDB Endowment*. **15** (7): 1311–1323. [doi](./Doi_(identifier)):[10.14778/3523210.3523211](https://doi.org/10.14778%2F3523210.3523211). [ISSN](./ISSN_(identifier)) [2150-8097](https://search.worldcat.org/issn/2150-8097).
33. [↑](./Bloom_filter#cite_ref-33) Bender, Michael A.; Farach-Colton, Martín; Kuszmaul, John; Kuszmaul, William; Liu, Mingmou (2022-06-09). ["On the optimal time/Space tradeoff for hash tables"](https://dx.doi.org/10.1145/3519935.3519969). *Proceedings of the 54th Annual ACM SIGACT Symposium on Theory of Computing*. New York, NY, USA: ACM. pp. 1284–1297. [arXiv](./ArXiv_(identifier)):[2111.00602](https://arxiv.org/abs/2111.00602). [doi](./Doi_(identifier)):[10.1145/3519935.3519969](https://doi.org/10.1145%2F3519935.3519969). [hdl](./Hdl_(identifier)):[1721.1/146419](https://hdl.handle.net/1721.1%2F146419). [ISBN](./ISBN_(identifier)) [9781450392648](./Special:BookSources/9781450392648). [S2CID](./S2CID_(identifier)) [240354692](https://api.semanticscholar.org/CorpusID:240354692).
34. [1](./Bloom_filter#cite_ref-autogenerated1_34-0) [2](./Bloom_filter#cite_ref-autogenerated1_34-1) Luo, Lailong; Guo, Deke; Ma, Richard T.B.; Rottenstreich, Ori; Luo, Xueshan (13 Apr 2018). "Optimizing Bloom filter: Challenges, solutions, and comparisons". [arXiv](./ArXiv_(identifier)):[1804.04777](https://arxiv.org/abs/1804.04777) [[cs.DS](https://arxiv.org/archive/cs.DS)].
35. [↑](./Bloom_filter#cite_ref-35) Dasgupta, Sanjoy; Sheehan, Timothy C.; Stevens, Charles F.; Navlakhae, Saket (2018). ["A neural data structure for novelty detection"](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6304992). *Proceedings of the National Academy of Sciences*. **115** (51): 13093–13098. [Bibcode](./Bibcode_(identifier)):[2018PNAS..11513093D](https://ui.adsabs.harvard.edu/abs/2018PNAS..11513093D). [doi](./Doi_(identifier)):[10.1073/pnas.1814448115](https://doi.org/10.1073%2Fpnas.1814448115). [PMC](./PMC_(identifier)) [6304992](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6304992). [PMID](./PMID_(identifier)) [30509984](https://pubmed.ncbi.nlm.nih.gov/30509984).
36. [↑](./Bloom_filter#cite_ref-36) Kiss, S. Z.; Hosszu, E.; Tapolcai, J.; Rónyai, L.; Rottenstreich, O. (2018). ["Bloom filter with a false positive free zone"](http://lendulet.tmit.bme.hu/lendulet_website/wp-content/papercite-data/pdf/kiss2018bloom.pdf) (PDF). *IEEE Proceedings of INFOCOM*. Retrieved 4 December 2018.
37. [↑](./Bloom_filter#cite_ref-37) Larisch, James; Choffnes, David; Levin, Dave; Maggs, Bruce M.; Mislove, Alan; Wilson, Christo (2017). "CRLite: A Scalable System for Pushing All TLS Revocations to All Browsers". *2017 IEEE Symposium on Security and Privacy (SP)*. pp. 539–556. [doi](./Doi_(identifier)):[10.1109/sp.2017.17](https://doi.org/10.1109%2Fsp.2017.17). [ISBN](./ISBN_(identifier)) [978-1-5090-5533-3](./Special:BookSources/978-1-5090-5533-3). [S2CID](./S2CID_(identifier)) [3926509](https://api.semanticscholar.org/CorpusID:3926509).
38. [↑](./Bloom_filter#cite_ref-38) Kim, Kibeom; Jeong, Yongjo; Lee, Youngjoo; Lee, Sunggu (2019-07-11). ["Analysis of Counting Bloom Filters Used for Count Thresholding"](https://doi.org/10.3390%2Felectronics8070779). *Electronics*. **8** (7): 779. [doi](./Doi_(identifier)):[10.3390/electronics8070779](https://doi.org/10.3390%2Felectronics8070779). [ISSN](./ISSN_(identifier)) [2079-9292](https://search.worldcat.org/issn/2079-9292).
39. [↑](./Bloom_filter#cite_ref-FOOTNOTEPournarasWarnierBrazier2013_39-0) [Pournaras, Warnier & Brazier (2013)](./Bloom_filter#CITEREFPournarasWarnierBrazier2013).
40. [↑](./Bloom_filter#cite_ref-40) Sanders, Peter; Schlag, Sebastian; Müller, Ingo (2013). "Communication efficient algorithms for fundamental big data problems". *2013 IEEE International Conference on Big Data*. pp. 15–23. [doi](./Doi_(identifier)):[10.1109/BigData.2013.6691549](https://doi.org/10.1109%2FBigData.2013.6691549). [ISBN](./ISBN_(identifier)) [978-1-4799-1293-3](./Special:BookSources/978-1-4799-1293-3). [S2CID](./S2CID_(identifier)) [15968541](https://api.semanticscholar.org/CorpusID:15968541).
41. [↑](./Bloom_filter#cite_ref-41) Schlag, Sebastian (2013). "Distributed duplicate removal". *Karlsruhe Institute of Technology*.
42. [↑](./Bloom_filter#cite_ref-42) Shatdal, Ambuj; Jeffrey F. Naughton (1994). "Processing aggregates in parallel database systems". *University of Wisconsin-Madison Department of Computer Sciences*: 8.
43. [↑](./Bloom_filter#cite_ref-43) V. Kumar; A. Grama; A. Gupta; G. Karypis (1994). *Introduction to Parallel Computing. Design and Analysis of Algorithms*. Benjamin/Cummings.
44. [↑](./Bloom_filter#cite_ref-AgingBloom_44-0) Yoon, MyungKeun (2010). "Aging Bloom Filter with Two Active Buffers for Dynamic Sets". *IEEE Transactions on Knowledge and Data Engineering*. **22** (1): 134–138. [Bibcode](./Bibcode_(identifier)):[2010ITKDE..22..134Y](https://ui.adsabs.harvard.edu/abs/2010ITKDE..22..134Y). [doi](./Doi_(identifier)):[10.1109/TKDE.2009.136](https://doi.org/10.1109%2FTKDE.2009.136). [S2CID](./S2CID_(identifier)) [15922054](https://api.semanticscholar.org/CorpusID:15922054).
45. [↑](./Bloom_filter#cite_ref-45) Géraud-Stewart, Rémi; Lombard-Platet, Marius; Naccache, David (2020). "Approaching Optimal Duplicate Detection in a Sliding Window". *Computing and Combinatorics*. Lecture Notes in Computer Science. Vol. 12273. pp. 64–84. [arXiv](./ArXiv_(identifier)):[2005.04740](https://arxiv.org/abs/2005.04740). [doi](./Doi_(identifier)):[10.1007/978-3-030-58150-3_6](https://doi.org/10.1007%2F978-3-030-58150-3_6). [ISBN](./ISBN_(identifier)) [978-3-030-58149-7](./Special:BookSources/978-3-030-58149-7). [S2CID](./S2CID_(identifier)) [218581915](https://api.semanticscholar.org/CorpusID:218581915).
46. [↑](./Bloom_filter#cite_ref-46) Kirsch, Adam; Mitzenmacher†, Michael. ["Less Hashing, Same Performance: Building a Better Bloom Filter"](https://www.eecs.harvard.edu/~michaelm/postscripts/rsa2008.pdf) (PDF). *Harvard School of Engineering and Applied Sciences*. Wiley InterScience.
47. [↑](./Bloom_filter#cite_ref-FOOTNOTECalderoniPalmieriMaio2015_47-0) [Calderoni, Palmieri & Maio (2015)](./Bloom_filter#CITEREFCalderoniPalmieriMaio2015).
48. [↑](./Bloom_filter#cite_ref-FOOTNOTECalderoniPalmieriMaio2018_48-0) [Calderoni, Palmieri & Maio (2018)](./Bloom_filter#CITEREFCalderoniPalmieriMaio2018).
49. [↑](./Bloom_filter#cite_ref-FOOTNOTEZhiwangJungangJian2010_49-0) [Zhiwang, Jungang & Jian (2010)](./Bloom_filter#CITEREFZhiwangJungangJian2010).
50. [1](./Bloom_filter#cite_ref-FOOTNOTEKoucheryavyGiambeneStaehleBarcelo-Arroyo2009_50-0) [2](./Bloom_filter#cite_ref-FOOTNOTEKoucheryavyGiambeneStaehleBarcelo-Arroyo2009_50-1) [Koucheryavy et al. (2009)](./Bloom_filter#CITEREFKoucheryavyGiambeneStaehleBarcelo-Arroyo2009).
51. [↑](./Bloom_filter#cite_ref-FOOTNOTEKubiatowiczBindelCzerwinskiGeels2000_51-0) [Kubiatowicz et al. (2000)](./Bloom_filter#CITEREFKubiatowiczBindelCzerwinskiGeels2000).

 

### Works cited

  
- Agarwal, Sachin; Trachtenberg, Ari (2006). "Approximating the number of differences between remote sets". [*2006 IEEE Information Theory Workshop*](http://ipsit.bu.edu/documents/wrap-web.pdf) (PDF). Punta del Este, Uruguay. p. 217. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.69.1033](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.69.1033). [doi](./Doi_(identifier)):[10.1109/ITW.2006.1633815](https://doi.org/10.1109%2FITW.2006.1633815). [ISBN](./ISBN_(identifier)) [978-1-4244-0035-5](./Special:BookSources/978-1-4244-0035-5). [S2CID](./S2CID_(identifier)) [2048278](https://api.semanticscholar.org/CorpusID:2048278).`{{cite book}}`:  CS1 maint: location missing publisher ([link](./Category:CS1_maint:_location_missing_publisher))
- Ahmadi, Mahmood; Wong, Stephan (2007), "A Cache Architecture for Counting Bloom Filters", *15th international Conference on Networks (ICON-2007)*, p. 218, [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.125.2470](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.125.2470), [doi](./Doi_(identifier)):[10.1109/ICON.2007.4444089](https://doi.org/10.1109%2FICON.2007.4444089), [ISBN](./ISBN_(identifier)) [978-1-4244-1229-7](./Special:BookSources/978-1-4244-1229-7), [S2CID](./S2CID_(identifier)) [2967865](https://api.semanticscholar.org/CorpusID:2967865)
- Almeida, Paulo; Baquero, Carlos; Preguica, Nuno; Hutchison, David (2007), ["Scalable Bloom Filters"](http://gsd.di.uminho.pt/members/cbm/ps/dbloom.pdf) (PDF), *Information Processing Letters*, **101** (6): 255–261, [doi](./Doi_(identifier)):[10.1016/j.ipl.2006.10.007](https://doi.org/10.1016%2Fj.ipl.2006.10.007), [hdl](./Hdl_(identifier)):[1822/6627](https://hdl.handle.net/1822%2F6627)
- Apache Software Foundation (2012), ["11.6. Schema Design"](https://hbase.apache.org/0.94/book/perf.schema.html), *The Apache HBase Reference Guide, Revision 0.94.27*
- Bloom, Burton H. (1970), "Space/Time Trade-offs in Hash Coding with Allowable Errors", *[Communications of the ACM](./Communications_of_the_ACM)*, **13** (7): 422–426, [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.641.9096](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.641.9096), [doi](./Doi_(identifier)):[10.1145/362686.362692](https://doi.org/10.1145%2F362686.362692), [S2CID](./S2CID_(identifier)) [7931252](https://api.semanticscholar.org/CorpusID:7931252)
- Blustein, James; El-Maazawi, Amal (2002), "optimal case for general Bloom filters", [*Bloom Filters — A Tutorial, Analysis, and Survey*](https://www.cs.dal.ca/research/techreports/cs-2002-10), Dalhousie University Faculty of Computer Science, pp. 1–31
- Boldi, Paolo; Vigna, Sebastiano (2005), ["Mutable strings in Java: design, implementation and lightweight text-search algorithms"](https://web.archive.org/web/20250207144613/https://www.openaccessrepository.it/record/192228), *Science of Computer Programming*, **54** (1): 3–23, [doi](./Doi_(identifier)):[10.1016/j.scico.2004.05.003](https://doi.org/10.1016%2Fj.scico.2004.05.003), archived from [the original](https://www.openaccessrepository.it/record/192228) on February 7, 2025
- Bonomi, Flavio; [Mitzenmacher, Michael](./Michael_Mitzenmacher); Panigrahy, Rina; Singh, Sushil; [Varghese, George](./George_Varghese) (2006), "An Improved Construction for Counting Bloom Filters", [*Algorithms – ESA 2006, 14th Annual European Symposium*](http://theory.stanford.edu/~rinap/papers/esa2006b.pdf) (PDF), [Lecture Notes in Computer Science](./Lecture_Notes_in_Computer_Science), vol. 4168, pp. 684–695, [doi](./Doi_(identifier)):[10.1007/11841036_61](https://doi.org/10.1007%2F11841036_61), [ISBN](./ISBN_(identifier)) [978-3-540-38875-3](./Special:BookSources/978-3-540-38875-3)
- [Broder, Andrei](./Andrei_Broder); [Mitzenmacher, Michael](./Michael_Mitzenmacher) (2005), ["Network Applications of Bloom Filters: A Survey"](http://www.eecs.harvard.edu/~michaelm/postscripts/im2005b.pdf) (PDF), *Internet Mathematics*, **1** (4): 485–509, [doi](./Doi_(identifier)):[10.1080/15427951.2004.10129096](https://doi.org/10.1080%2F15427951.2004.10129096), [S2CID](./S2CID_(identifier)) [1560675](https://api.semanticscholar.org/CorpusID:1560675)
- Byers, John W.; Considine, Jeffrey; [Mitzenmacher, Michael](./Michael_Mitzenmacher); Rost, Stanislav (2004), "Informed content delivery across adaptive overlay networks", *[IEEE/ACM Transactions on Networking](./IEEE/ACM_Transactions_on_Networking)*, **12** (5): 767, [Bibcode](./Bibcode_(identifier)):[2004ITNet..12..767B](https://ui.adsabs.harvard.edu/abs/2004ITNet..12..767B), [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.207.1563](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.207.1563), [doi](./Doi_(identifier)):[10.1109/TNET.2004.836103](https://doi.org/10.1109%2FTNET.2004.836103), [S2CID](./S2CID_(identifier)) [47088273](https://api.semanticscholar.org/CorpusID:47088273)
- Calderoni, Luca; Palmieri, Paolo; Maio, Dario (2015), ["Location privacy without mutual trust: The spatial Bloom filter"](http://eprints.bournemouth.ac.uk/22802/4/Palmieri.pdf) (PDF), *Computer Communications*, **68**: 4–16, [doi](./Doi_(identifier)):[10.1016/j.comcom.2015.06.011](https://doi.org/10.1016%2Fj.comcom.2015.06.011), [hdl](./Hdl_(identifier)):[10468/4762](https://hdl.handle.net/10468%2F4762), [ISSN](./ISSN_(identifier)) [0140-3664](https://search.worldcat.org/issn/0140-3664)
- Calderoni, Luca; Palmieri, Paolo; Maio, Dario (2018), "Probabilistic Properties of the Spatial Bloom Filters and Their Relevance to Cryptographic Protocols", *IEEE Transactions on Information Forensics and Security*, **13** (7): 1710–1721, [Bibcode](./Bibcode_(identifier)):[2018ITIF...13.1710C](https://ui.adsabs.harvard.edu/abs/2018ITIF...13.1710C), [doi](./Doi_(identifier)):[10.1109/TIFS.2018.2799486](https://doi.org/10.1109%2FTIFS.2018.2799486), [hdl](./Hdl_(identifier)):[10468/5767](https://hdl.handle.net/10468%2F5767), [ISSN](./ISSN_(identifier)) [1556-6013](https://search.worldcat.org/issn/1556-6013), [S2CID](./S2CID_(identifier)) [3693354](https://api.semanticscholar.org/CorpusID:3693354)
- Chang, Fay; Dean, Jeffrey; Ghemawat, Sanjay; Hsieh, Wilson; Wallach, Deborah; Burrows, Mike; Chandra, Tushar; Fikes, Andrew; Gruber, Robert (2006), "Bigtable: A Distributed Storage System for Structured Data", [*Seventh Symposium on Operating System Design and Implementation*](http://research.google.com/archive/bigtable.html)
- Charles, Denis Xavier; Chellapilla, Kumar (2008), "Bloomier filters: A second look", in Halperin, Dan; Mehlhorn, Kurt (eds.), *Algorithms: ESA 2008, 16th Annual European Symposium, Karlsruhe, Germany, September 15–17, 2008, Proceedings*, Lecture Notes in Computer Science, vol. 5193, Springer, pp. 259–270, [arXiv](./ArXiv_(identifier)):[0807.0928](https://arxiv.org/abs/0807.0928), [doi](./Doi_(identifier)):[10.1007/978-3-540-87744-8_22](https://doi.org/10.1007%2F978-3-540-87744-8_22), [ISBN](./ISBN_(identifier)) [978-3-540-87743-1](./Special:BookSources/978-3-540-87743-1), [S2CID](./S2CID_(identifier)) [643445](https://api.semanticscholar.org/CorpusID:643445)
- [Chazelle, Bernard](./Bernard_Chazelle); Kilian, Joe; [Rubinfeld, Ronitt](./Ronitt_Rubinfeld); [Tal, Ayellet](./Ayellet_Tal) (2004), "The Bloomier filter: an efficient data structure for static support lookup tables", [*Proceedings of the Fifteenth Annual ACM-SIAM Symposium on Discrete Algorithms*](http://www.ee.technion.ac.il/~ayellet/Ps/nelson.pdf) (PDF), pp. 30–39
- Cohen, Saar; Matias, Yossi (2003), "Spectral Bloom Filters", [*Proceedings of the 2003 ACM SIGMOD International Conference on Management of Data*](https://web.archive.org/web/20210310041118/https://whiteblock.io/wp-content/uploads/2019/10/sbf-sigmod-03.pdf) (PDF), pp. 241–252, [doi](./Doi_(identifier)):[10.1145/872757.872787](https://doi.org/10.1145%2F872757.872787), [ISBN](./ISBN_(identifier)) [978-1581136340](./Special:BookSources/978-1581136340), [S2CID](./S2CID_(identifier)) [1058187](https://api.semanticscholar.org/CorpusID:1058187), archived from [the original](https://whiteblock.io/wp-content/uploads/2019/10/sbf-sigmod-03.pdf) (PDF) on 2021-03-10, retrieved 2019-10-24
- Deng, Fan; Rafiei, Davood (2006), "Approximately Detecting Duplicates for Streaming Data using Stable Bloom Filters", [*Proceedings of the ACM SIGMOD Conference*](http://webdocs.cs.ualberta.ca/~drafiei/papers/DupDet06Sigmod.pdf) (PDF), pp. 25–36
- Dharmapurikar, Sarang; Song, Haoyu; Turner, Jonathan; Lockwood, John (2006), "Fast packet classification using Bloom filters", [*Proceedings of the 2006 ACM/IEEE Symposium on Architecture for Networking and Communications Systems*](https://web.archive.org/web/20070202202510/http://www.arl.wustl.edu/~sarang/ancs6819-dharmapurikar.pdf) (PDF), pp. 61–70, [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.78.9584](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.78.9584), [doi](./Doi_(identifier)):[10.1145/1185347.1185356](https://doi.org/10.1145%2F1185347.1185356), [ISBN](./ISBN_(identifier)) [978-1595935809](./Special:BookSources/978-1595935809), [S2CID](./S2CID_(identifier)) [7848110](https://api.semanticscholar.org/CorpusID:7848110), archived from [the original](http://www.arl.wustl.edu/~sarang/ancs6819-dharmapurikar.pdf) (PDF) on 2007-02-02
- Dietzfelbinger, Martin; [Pagh, Rasmus](./Rasmus_Pagh) (2008), "Succinct data structures for retrieval and approximate membership", in Aceto, Luca; Damgård, Ivan; Goldberg, Leslie Ann; Halldórsson, Magnús M.; Ingólfsdóttir, Anna; Walukiewicz, Igor (eds.), *Automata, Languages and Programming: 35th International Colloquium, ICALP 2008, Reykjavik, Iceland, July 7–11, 2008, Proceedings, Part I, Track A: Algorithms, Automata, Complexity, and Games*, Lecture Notes in Computer Science, vol. 5125, Springer, pp. 385–396, [arXiv](./ArXiv_(identifier)):[0803.3693](https://arxiv.org/abs/0803.3693), [doi](./Doi_(identifier)):[10.1007/978-3-540-70575-8_32](https://doi.org/10.1007%2F978-3-540-70575-8_32), [ISBN](./ISBN_(identifier)) [978-3-540-70574-1](./Special:BookSources/978-3-540-70574-1), [S2CID](./S2CID_(identifier)) [1699996](https://api.semanticscholar.org/CorpusID:1699996)
- Dillinger, Peter C.; Manolios, Panagiotis (2004a), "Fast and Accurate Bitstate Verification for SPIN", [*Proceedings of the 11th International Spin Workshop on Model Checking Software*](http://www.ccs.neu.edu/home/pete/research/spin-3spin.html), Springer-Verlag, Lecture Notes in Computer Science 2989
- Dillinger, Peter C.; Manolios, Panagiotis (2004b), "Bloom Filters in Probabilistic Verification", [*Proceedings of the 5th International Conference on Formal Methods in Computer-Aided Design*](http://www.ccs.neu.edu/home/pete/research/bloom-filters-verification.html), Springer-Verlag, Lecture Notes in Computer Science 3312
- Donnet, Benoit; Baynat, Bruno; Friedman, Timur (2006), "Retouched Bloom Filters: Allowing Networked Applications to Flexibly Trade Off False Positives Against False Negatives", [*CoNEXT 06 – 2nd Conference on Future Networking Technologies*](https://web.archive.org/web/20090517023058/http://adetti.iscte.pt/events/CONEXT06/Conext06_Proceedings/papers/13.html), archived from [the original](http://www.adetti.iscte.pt/events/CONEXT06/Conext06_Proceedings/papers/13.html) on 2009-05-17
- [Eppstein, David](./David_Eppstein); [Goodrich, Michael T.](./Michael_T._Goodrich) (2007), "Space-efficient straggler identification in round-trip data streams via Newton's identities and invertible Bloom filters", [*Algorithms and Data Structures, 10th International Workshop, WADS 2007*](./Workshop_on_Algorithms_and_Data_Structures), Lecture Notes in Computer Science, vol. 4619, Springer-Verlag, pp. 637–648, [arXiv](./ArXiv_(identifier)):[0704.3313](https://arxiv.org/abs/0704.3313), [Bibcode](./Bibcode_(identifier)):[2007arXiv0704.3313E](https://ui.adsabs.harvard.edu/abs/2007arXiv0704.3313E)
- Fan, Bin; Andersen, Dave G.; Kaminsky, Michael; [Mitzenmacher, Michael D.](./Michael_Mitzenmacher) (2014), "Cuckoo filter: Practically better than Bloom", *Proceedings of the 10th ACM International on Conference on emerging Networking Experiments and Technologies*, pp. 75–88, [doi](./Doi_(identifier)):[10.1145/2674005.2674994](https://doi.org/10.1145%2F2674005.2674994), [ISBN](./ISBN_(identifier)) [9781450332798](./Special:BookSources/9781450332798). Open source implementation [available on github](https://github.com/efficient/cuckoofilter).
- Fan, Li; [Cao, Pei](./Pei_Cao); [Almeida, Jussara](./Jussara_M._Almeida); [Broder, Andrei](./Andrei_Broder) (2000), ["Summary Cache: A Scalable Wide-Area Web Cache Sharing Protocol"](https://web.archive.org/web/20170922002708/http://www.ece.eng.wayne.edu/~sjiang/ECE7995-07-fall/slides/summary-cache.pdf) (PDF), *IEEE/ACM Transactions on Networking*, **8** (3): 281–293, [Bibcode](./Bibcode_(identifier)):[2000ITNet...8..281L](https://ui.adsabs.harvard.edu/abs/2000ITNet...8..281L), [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.41.1487](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.41.1487), [doi](./Doi_(identifier)):[10.1109/90.851975](https://doi.org/10.1109%2F90.851975), [S2CID](./S2CID_(identifier)) [4779754](https://api.semanticscholar.org/CorpusID:4779754), archived from [the original](http://www.ece.eng.wayne.edu/~sjiang/ECE7995-07-fall/slides/summary-cache.pdf) (PDF) on 2017-09-22, retrieved 2018-07-30. A preliminary version appeared at SIGCOMM '98.
- Goel, Ashish; Gupta, Pankaj (2010), ["Small subset queries and bloom filters using ternary associative memories, with applications"](http://www.stanford.edu/~ashishg/papers/inverted.pdf) (PDF), *ACM SIGMETRICS Performance Evaluation Review*, **38**: 143, [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.296.6513](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.296.6513), [doi](./Doi_(identifier)):[10.1145/1811099.1811056](https://doi.org/10.1145%2F1811099.1811056)
- Graf, Thomas Mueller; Lemire, Daniel (2020), "Xor Filters", *ACM Journal of Experimental Algorithmics*, **25**: 1–16, [arXiv](./ArXiv_(identifier)):[1912.08258](https://arxiv.org/abs/1912.08258), [Bibcode](./Bibcode_(identifier)):[2019arXiv191208258M](https://ui.adsabs.harvard.edu/abs/2019arXiv191208258M), [doi](./Doi_(identifier)):[10.1145/3376122](https://doi.org/10.1145%2F3376122), [S2CID](./S2CID_(identifier)) [209405019](https://api.semanticscholar.org/CorpusID:209405019)
- Grandi, Fabio (2018), ["On the analysis of Bloom filters"](http://www-db.disi.unibo.it/~fgrandi/papers/IPL2017_accepted.pdf) (PDF), *Information Processing Letters*, **129**: 35–39, [doi](./Doi_(identifier)):[10.1016/j.ipl.2017.09.004](https://doi.org/10.1016%2Fj.ipl.2017.09.004)
- Kirsch, Adam; [Mitzenmacher, Michael](./Michael_Mitzenmacher) (2006), "Less Hashing, Same Performance: Building a Better Bloom Filter", in Azar, Yossi; Erlebach, Thomas (eds.), [*Algorithms – ESA 2006, 14th Annual European Symposium*](https://web.archive.org/web/20090131053735/http://www.eecs.harvard.edu/~kirsch/pubs/bbbf/esa06.pdf) (PDF), Lecture Notes in Computer Science, vol. 4168, Springer-Verlag, Lecture Notes in Computer Science 4168, pp. 456–467, [doi](./Doi_(identifier)):[10.1007/11841036](https://doi.org/10.1007%2F11841036), [ISBN](./ISBN_(identifier)) [978-3-540-38875-3](./Special:BookSources/978-3-540-38875-3), archived from [the original](http://www.eecs.harvard.edu/~kirsch/pubs/bbbf/esa06.pdf) (PDF) on 2009-01-31
- Koucheryavy, Y.; Giambene, G.; Staehle, D.; Barcelo-Arroyo, F.; Braun, T.; Siris, V. (2009), "Traffic and QoS Management in Wireless Multimedia Networks", *COST 290 Final Report*: 111
- Kubiatowicz, J.; Bindel, D.; Czerwinski, Y.; Geels, S.; Eaton, D.; Gummadi, R.; Rhea, S.; Weatherspoon, H.; et al. (2000), ["Oceanstore: An architecture for global-scale persistent storage"](https://web.archive.org/web/20120311063707/http://ftp.csd.uwo.ca/courses/CS9843b/papers/OceanStore.pdf) (PDF), *ACM SIGPLAN Notices*: 190–201, archived from [the original](http://ftp.csd.uwo.ca/courses/CS9843b/papers/OceanStore.pdf) (PDF) on 2012-03-11, retrieved 2011-12-01
- [Maggs, Bruce M.](./Bruce_Maggs); [Sitaraman, Ramesh K.](./Ramesh_Sitaraman) (July 2015), ["Algorithmic nuggets in content delivery"](https://web.archive.org/web/20210814193152/https://www.akamai.com/us/en/multimedia/documents/technical-publication/algorithmic-nuggets-in-content-delivery-technical-publication.pdf) (PDF), *ACM SIGCOMM Computer Communication Review*, **45** (3): 52–66, [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.696.9236](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.696.9236), [doi](./Doi_(identifier)):[10.1145/2805789.2805800](https://doi.org/10.1145%2F2805789.2805800), [S2CID](./S2CID_(identifier)) [65760](https://api.semanticscholar.org/CorpusID:65760), archived from [the original](https://www.akamai.com/us/en/multimedia/documents/technical-publication/algorithmic-nuggets-in-content-delivery-technical-publication.pdf) (PDF) on 2021-08-14
- [Mitzenmacher, Michael](./Michael_Mitzenmacher); [Upfal, Eli](./Eli_Upfal) (2005), [*Probability and computing: Randomized algorithms and probabilistic analysis*](https://books.google.com/books?id=0bAYl6d7hvkC&pg=PA110), Cambridge University Press, pp. 107–112, [ISBN](./ISBN_(identifier)) [9780521835404](./Special:BookSources/9780521835404)
- Mortensen, Christian Worm; [Pagh, Rasmus](./Rasmus_Pagh); [Pătrașcu, Mihai](./Mihai_Pătrașcu_(computer_scientist)) (2005), "On dynamic range reporting in one dimension", *Proceedings of the Thirty-Seventh Annual ACM Symposium on Theory of Computing*, pp. 104–111, [arXiv](./ArXiv_(identifier)):[cs/0502032](https://arxiv.org/abs/cs/0502032), [doi](./Doi_(identifier)):[10.1145/1060590.1060606](https://doi.org/10.1145%2F1060590.1060606), [ISBN](./ISBN_(identifier)) [978-1581139600](./Special:BookSources/978-1581139600), [S2CID](./S2CID_(identifier)) [56473](https://api.semanticscholar.org/CorpusID:56473)
- Mullin, James K. (1990), "Optimal semijoins for distributed database systems", *IEEE Transactions on Software Engineering*, **16** (5): 558–560, [Bibcode](./Bibcode_(identifier)):[1990ITSEn..16..558M](https://ui.adsabs.harvard.edu/abs/1990ITSEn..16..558M), [doi](./Doi_(identifier)):[10.1109/32.52778](https://doi.org/10.1109%2F32.52778)
- Pagh, Anna; [Pagh, Rasmus](./Rasmus_Pagh); Rao, S. Srinivasa (2005), "An optimal Bloom filter replacement", [*Proceedings of the Sixteenth Annual ACM-SIAM Symposium on Discrete Algorithms*](https://www.itu.dk/people/pagh/papers/bloom.pdf) (PDF), pp. 823–829
- Palmieri, Paolo; Calderoni, Luca; Maio, Dario (2014), "Spatial Bloom Filters: Enabling Privacy in Location-Aware Applications", *Proc. 10th International Conference on Information Security and Cryptology (Inscrypt 2014)*, vol. 8957, Springer-Verlag, Lecture Notes in Computer Science, pp. 16–36, [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.471.4759](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.471.4759), [doi](./Doi_(identifier)):[10.1007/978-3-319-16745-9_2](https://doi.org/10.1007%2F978-3-319-16745-9_2), [ISBN](./ISBN_(identifier)) [978-3-319-16744-2](./Special:BookSources/978-3-319-16744-2)
- Porat, Ely (2009), "An optimal Bloom filter replacement based on matrix solving", in Frid, Anna E.; Morozov, Andrey; Rybalchenko, Andrey; Wagner, Klaus W. (eds.), *Computer Science, Theory and Applications: Fourth International Computer Science Symposium in Russia, CSR 2009, Novosibirsk, Russia, August 18–23, 2009, Proceedings*, Lecture Notes in Computer Science, vol. 5675, Springer, pp. 263–273, [arXiv](./ArXiv_(identifier)):[0804.1845](https://arxiv.org/abs/0804.1845), [doi](./Doi_(identifier)):[10.1007/978-3-642-03351-3_25](https://doi.org/10.1007%2F978-3-642-03351-3_25), [ISBN](./ISBN_(identifier)) [978-3-642-03350-6](./Special:BookSources/978-3-642-03350-6), [S2CID](./S2CID_(identifier)) [3205108](https://api.semanticscholar.org/CorpusID:3205108)
- Pournaras, E.; Warnier, M.; [Brazier, F. M. T.](./Frances_Brazier) (2013), "A generic and adaptive aggregation service for large-scale decentralized networks", *Complex Adaptive Systems Modeling*, **1** (19): 19, [doi](./Doi_(identifier)):[10.1186/2194-3206-1-19](https://doi.org/10.1186%2F2194-3206-1-19). Prototype implementation [available on github](https://github.com/epournaras/DIAS).
- Putze, F.; [Sanders, P.](./Peter_Sanders_(computer_scientist)); Singler, J. (2007), "Cache-, Hash- and Space-Efficient Bloom Filters", in Demetrescu, Camil (ed.), [*Experimental Algorithms, 6th International Workshop, WEA 2007*](https://web.archive.org/web/20070623102632/http://algo2.iti.uni-karlsruhe.de/singler/publications/cacheefficientbloomfilters-wea2007.pdf) (PDF), Lecture Notes in Computer Science, vol. 4525, Springer-Verlag, Lecture Notes in Computer Science 4525, pp. 108–121, [doi](./Doi_(identifier)):[10.1007/978-3-540-72845-0](https://doi.org/10.1007%2F978-3-540-72845-0), [ISBN](./ISBN_(identifier)) [978-3-540-72844-3](./Special:BookSources/978-3-540-72844-3), archived from [the original](http://algo2.iti.uni-karlsruhe.de/singler/publications/cacheefficientbloomfilters-wea2007.pdf) (PDF) on 2007-06-23, retrieved 2007-07-18
- Rottenstreich, Ori; Kanizo, Yossi; Keslassy, Isaac (2012), "The Variable-Increment Counting Bloom Filter", [*31st Annual IEEE International Conference on Computer Communications, 2012, Infocom 2012*](http://webee.technion.ac.il/~isaac/p/infocom12_variable.pdf) (PDF), pp. 1880–1888, [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.174.7165](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.174.7165), [doi](./Doi_(identifier)):[10.1109/INFCOM.2012.6195563](https://doi.org/10.1109%2FINFCOM.2012.6195563), [ISBN](./ISBN_(identifier)) [978-1-4673-0773-4](./Special:BookSources/978-1-4673-0773-4)
- Sethumadhavan, Simha; Desikan, Rajagopalan; Burger, Doug; Moore, Charles R.; Keckler, Stephen W. (2003), "Scalable hardware memory disambiguation for high ILP processors", [*36th Annual IEEE/ACM International Symposium on Microarchitecture, 2003, MICRO-36*](https://web.archive.org/web/20070114035556/http://www.cs.utexas.edu/users/simha/publications/lsq.pdf) (PDF), pp. 399–410, [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.229.1254](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.229.1254), [doi](./Doi_(identifier)):[10.1109/MICRO.2003.1253244](https://doi.org/10.1109%2FMICRO.2003.1253244), [ISBN](./ISBN_(identifier)) [978-0-7695-2043-8](./Special:BookSources/978-0-7695-2043-8), [S2CID](./S2CID_(identifier)) [195881068](https://api.semanticscholar.org/CorpusID:195881068), archived from [the original](http://www.cs.utexas.edu/users/simha/publications/lsq.pdf) (PDF) on 2007-01-14
- Starobinski, David; Trachtenberg, Ari; Agarwal, Sachin (2003), ["Efficient PDA Synchronization"](http://people.bu.edu/staro/efficient_pda.pdf) (PDF), *IEEE Transactions on Mobile Computing*, **2** (1): 40, [Bibcode](./Bibcode_(identifier)):[2003ITMC....2...40S](https://ui.adsabs.harvard.edu/abs/2003ITMC....2...40S), [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.71.7833](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.71.7833), [doi](./Doi_(identifier)):[10.1109/TMC.2003.1195150](https://doi.org/10.1109%2FTMC.2003.1195150)
- Stern, Ulrich; Dill, David L. (1996), "A New Scheme for Memory-Efficient Probabilistic Verification", *Proceedings of Formal Description Techniques for Distributed Systems and Communication Protocols, and Protocol Specification, Testing, and Verification: IFIP TC6/WG6.1 Joint International Conference*, Chapman & Hall, IFIP Conference Proceedings, pp. 333–348, [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.47.4101](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.47.4101)
- Wessels, Duane (January 2004), "10.7 Cache Digests", *Squid: The Definitive Guide* (1st ed.), O'Reilly Media, p. 172, [ISBN](./ISBN_(identifier)) [978-0-596-00162-9](./Special:BookSources/978-0-596-00162-9), Cache Digests are based on a technique first published by [Pei Cao](./Pei_Cao), called Summary Cache. The fundamental idea is to use a Bloom filter to represent the cache contents.
- Tarkoma, Sasu; Rothenberg, Christian Esteve; Lagerspetz, Eemil (2012), "Theory and practice of bloom filters for distributed systems", [*IEEE Communications Surveys & Tutorials, no. 1.*](https://git.gnunet.org/bibliography.git/plain/docs/TheoryandPracticeBloomFilter2011Tarkoma.pdf) (PDF), vol. 14, pp. 131–155
- Zhiwang, Cen; Jungang, Xu; Jian, Sun (2010), "A multi-layer Bloom filter for duplicated URL detection", *Proc. 3rd International Conference on Advanced Computer Theory and Engineering (ICACTE 2010)*, vol. 1, pp. V1–586–V1–591, [doi](./Doi_(identifier)):[10.1109/ICACTE.2010.5578947](https://doi.org/10.1109%2FICACTE.2010.5578947), [ISBN](./ISBN_(identifier)) [978-1-4244-6539-2](./Special:BookSources/978-1-4244-6539-2), [S2CID](./S2CID_(identifier)) [3108985](https://api.semanticscholar.org/CorpusID:3108985)

  

## External links

   [![Wikimedia Commons logo](//upload.wikimedia.org/wikipedia/en/thumb/4/4a/Commons-logo.svg/40px-Commons-logo.svg.png)](./File:Commons-logo.svg) Wikimedia Commons has media related to [Bloom filter](https://commons.wikimedia.org/wiki/Category:Bloom%20filter).  
- ["Using Bloom Filters"](http://www.perl.com/pub/2004/04/08/bloom_filters.html) Detailed Bloom Filter explanation using [Perl](./Perl)
- [Why Bloom filters work the way they do (Michael Nielsen, 2012)](http://www.michaelnielsen.org/ddi/why-bloom-filters-work-the-way-they-do/)
- [Bloom Filters — A Tutorial, Analysis, and Survey (Blustein & El-Maazawi, 2002)](https://www.cs.dal.ca/research/techreports/cs-2002-10) at Dalhousie University
- [Table of false-positive rates for different configurations](http://www.cs.wisc.edu/~cao/papers/summary-cache/node8.html) from a [University of Wisconsin–Madison](./University_of_Wisconsin–Madison) website
- ["More Optimal Bloom Filters", Ely Porat (Nov/2007) Google TechTalk video](https://www.youtube.com/watch?v=947gWqwkhu0) on [YouTube](./YouTube)