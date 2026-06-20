---
source: https://en.wikipedia.org/wiki/Counting_Bloom_filter
fetched: 2026-06-19
---

Probabilistic data structure 

A **counting Bloom filter** (**CBF**[[1]](./Counting_Bloom_filter#cite_note-choi-2024-1)) or **spectral Bloom filter**[[2]](./Counting_Bloom_filter#cite_note-cohen-2003-2) is a [probabilistic](./Probabilistic) [data structure](./Data_structure) that is used to test whether the number of occurrences of a given [element](./Element_(mathematics)) in a sequence exceeds a given threshold. As a generalized form of the [Bloom filter](./Bloom_filter), [false positive](./Type_I_and_type_II_errors) matches are possible, but [false negatives](./Type_I_and_type_II_errors) are not – in other words, a query returns either "possibly bigger or equal than the threshold" or "definitely smaller than the threshold".

 

## Algorithm description

 

Most of the parameters are defined same with [Bloom filter](./Bloom_filter), such as *m, k. m* is the number of counters in counting Bloom filter, which is expansion of *m* bits in Bloom filter. An *empty counting Bloom filter* is a *m* counters, all set to 0. Similar to Bloom filter, there must also be *k* different [hash functions](./Hash_function) defined, each of which [maps](./Map_(mathematics)) or hashes some set element to one of the *m* counter array positions, generating a uniform random distribution. It is also similar that *k* is a constant, much smaller than *m*, which is proportional to the number of elements to be added.

 

The main generalization of Bloom filter is adding an element. To *add* an element, feed it to each of the *k* hash functions to get *k* array positions and *increment* the counters 1 at all these positions.

 

To *query* for an element with a threshold *θ* (test whether the count number of an element is smaller than *θ*), feed it to each of the *k* hash functions to get *k* counter positions. If any of the counters at these positions is less than *θ*, the count number of element is definitely less than *θ* – if it were more and equal, then all the corresponding counters would have been greater or equal to *θ*. If all are greater or equal to *θ*, then either the count is really greater or equal to *θ*, or the counters have by chance been greater or equal to *θ*. If all are greater or equal to θ even though the count is smaller than *θ*, this circumstance is defined as [false positive](./False_positive). This also should be minimized like Bloom filter.

 

About hashing problem and advantages, see [Bloom filter](./Bloom_filter).

 

A counting Bloom filter is essentially the same data structure as [count–min sketches](./Count–min_sketch), but are used differently.

 

## Potential for false negatives

 

Several implementations of counting bloom filters allow for deletion, by decrementing each of the *k* counters for a given input.  This will introduce the probability of false negatives during a query if the deleted input has not previously been inserted into the filter.  Guo *et al.* present the problem in great detail, and provide heuristics for the parameters *m*, *k*, and *n* which minimize the probability of false negatives.[[3]](./Counting_Bloom_filter#cite_note-3)

 

## Probability of false positives

 

The same assumptions in [Bloom filter](./Bloom_filter), which hash functions make insertions uniform random, is also assumed here. In the *m* pots, *kn* balls are inserted randomly. So the probability of one of counter in counting Bloom filter counts *l* is

 

    b ( l , k n ,   1 m   ) =    (    k n  l   )    (   1 m    )  l   ( 1 − −    1 m    )  k n − −  l     {\displaystyle b(l,kn,{\frac {1}{m}})={kn \choose l}({\frac {1}{m}})^{l}(1-{\frac {1}{m}})^{kn-l}}  ![{\displaystyle b(l,kn,{\frac {1}{m}})={kn \choose l}({\frac {1}{m}})^{l}(1-{\frac {1}{m}})^{kn-l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/101a52e1309a2dd16a1d0b920fd57aeec2fbbad4),

 

where *b* is [binomial distribution](./Binomial_distribution).[[4]](./Counting_Bloom_filter#cite_note-4) A counting Bloom filter determines an element is greater or equal to *θ* when the corresponding *k* counters are greater or equal to *θ.* Therefore, the probability that counting Bloom filter determines an element is greater or equal to *θ* is

 

     p  f p   ( θ θ  , k , n , m ) = ( 1 − −   ∑ ∑   l < θ θ    b ( l , k n ,   1 m   )  )  k     {\displaystyle p_{fp}(\theta ,k,n,m)=(1-\sum \limits _{l<\theta }b(l,kn,{\frac {1}{m}}))^{k}}  ![{\displaystyle p_{fp}(\theta ,k,n,m)=(1-\sum \limits _{l<\theta }b(l,kn,{\frac {1}{m}}))^{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/77741218ca98001806a0862e64775b319b049e23).

 

This is different from formal definition of [false positive](./False_positive) in counting Bloom filter. However, following the assumption in Bloom filter, above probability is defined as false positive of counting Bloom filter. If *θ*=1, the equation becomes false positive of Bloom filter.

 

### Optimal number of hash functions

 

For large but fixed *n* and *m*, the false positive decreases from *k*=1 to a point defined      k  o p t     {\displaystyle k_{opt}}  ![{\displaystyle k_{opt}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6780d4f16c1df91b33e954ad94651eca4fa1c9d2), and increases from      k  o p t     {\displaystyle k_{opt}}  ![{\displaystyle k_{opt}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6780d4f16c1df91b33e954ad94651eca4fa1c9d2)to positive infinity.[[5]](./Counting_Bloom_filter#cite_note-5)

 

[Kim et al. (2019)](https://www.mdpi.com/2079-9292/8/7/779) shows numerical values of      k  o p t     {\displaystyle k_{opt}}  ![{\displaystyle k_{opt}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6780d4f16c1df91b33e954ad94651eca4fa1c9d2)within     1 ≤ ≤  θ θ  ≤ ≤  30   {\displaystyle 1\leq \theta \leq 30}  ![{\displaystyle 1\leq \theta \leq 30}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b3b8adae7ace8ca3df67b84b503902e1bce7d499). For     θ θ  > 30   {\displaystyle \theta >30}  ![{\displaystyle \theta >30}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac8c701aecadf7fa3596390f55443bc17c1d1d96) they suggested using the floor or ceiling of       m n   ( 0.2037 θ θ  + 0.9176 )   {\displaystyle {\frac {m}{n}}(0.2037\theta +0.9176)}  ![{\displaystyle {\frac {m}{n}}(0.2037\theta +0.9176)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e0e0b08be43ad3f6ae7b7ec7491b14aa0acf2d2f).

 

## Variants

 

### Invertible Bloom filter

 

An invertible Bloom filter (IBF) is a variant of the counting Bloom filter that allows for listing of the remaining element, given there are not too may of them. There is, however, a small chance that multiple hash collisions can render a element unrecoverable.[[1]](./Counting_Bloom_filter#cite_note-choi-2024-1)[[6]](./Counting_Bloom_filter#cite_note-eppstein-2011-6)

 

Like a CBF, an IBF consists of a [hash table](./Hash_table) *B* which uses *k* hash functions *h*1...*h**k* and stores a counter in each of its *m* cells. Alongside each counter, it also stores a sum of elements and a sum of element hashes using a new hash function *g*. There is also a second hash table *C* to recover elements that could not be recovered using *B*, which also has *m* cells but only uses two hash functions *f*1 and *f*2. The total number of elements (*n*) is also stored.

 

To insert an element *x*, do the following:

 
```
 increment n
 for each 1 ≤ i ≤ k do
     increment B[hi(x)].count
     add x to B[hi(x)].idSum
     add g(x) to B[hi(x)].hashSum
 for each i in {1, 2} do
     increment C[fi(x)].count
     add x to C[fi(x)].idSum
     add g(x) to C[fi(x)].hashSum
```
 

Likewise, to remove an element *x*, do the following:

 
```
 decrement n
 for each 1 ≤ i ≤ k do
     decrement B[hi(x)].count
     subtract x from B[hi(x)].idSum
     subtract g(x) from B[hi(x)].hashSum
 for each i in {1, 2} do
     decrement C[fi(x)].count
     subtract x from C[fi(x)].idSum
     subtract g(x) from C[fi(x)].hashSum
```
 

Repeated insertions and removals can be simplified.

 

A cell is considered "pure" if it contains only one distinct element *x*, which can be checked using `g(B[i].idSum/B[i].count) = B[i].hashSum/B[i].count`. If a cell is pure, then *x* can be recovered by dividing the idSum by the count. To list the remaining elements ("stragglers"), do the following:

 
```
 while there is a pure cell i in B do
     let x := B[i].idSum/B[i].count
     if B[i].count > 0 then
         (this is a good element)
         output x
         for 1 ≤ i ≤ B[i].count do
             remove element x from B and C
     else
         (this is a false delete)
         for 1 ≤ i ≤ -B[i].count do
             insert element x into B and C
 if n ≠ 0 then
     (there are conflicts in B)
     repeat the above while loop, but swap B and C
```
 

### Invertible Bloom lookup table

 

An invertible Bloom lookup table (IBLT) is a variant of the invertible Bloom filter that also stores [associated values](./Key-value_pair) with each key. The difference is that an IBLT also stores a `valueSum` in each cell, which can be used to obtain the value for a given key.[[7]](./Counting_Bloom_filter#cite_note-goodrich-2011-7)

 

If there are no extraneous deletions (where a key is deleted without being inserted first) or duplicates (where a key is inserted multiple times), then the `hashkeySum` can be omitted. In this case, pure cells can be detected by checking whether `count = 1`.

 

A `hashvalueSum` may also be stored in each cell to verify that only one value has been inserted for the corresponding key.

 

IBLTs are suitable for use in [databases](./Databases), [networking](./Computer_network)[[7]](./Counting_Bloom_filter#cite_note-goodrich-2011-7) and [compression](./Data_compression).[[8]](./Counting_Bloom_filter#cite_note-8)

 

## References

  Inline citations added to your article will automatically display here. See en.wikipedia.org/wiki/WP:REFB for instructions on how to add citations.   
1. [1](./Counting_Bloom_filter#cite_ref-choi-2024_1-0) [2](./Counting_Bloom_filter#cite_ref-choi-2024_1-1) Choi, Eunji; Lee, Jungwon; Yim, Changhoon; Lim, Hyesook (2024). ["Decoding Errors in Difference-Invertible Bloom Filters: Analysis and Resolution"](https://doi.org/10.1109%2FACCESS.2024.3377222). *IEEE Access*. **12**: 40622–40633. [Bibcode](./Bibcode_(identifier)):[2024IEEEA..1240622C](https://ui.adsabs.harvard.edu/abs/2024IEEEA..1240622C). [doi](./Doi_(identifier)):[10.1109/ACCESS.2024.3377222](https://doi.org/10.1109%2FACCESS.2024.3377222).
2. [↑](./Counting_Bloom_filter#cite_ref-cohen-2003_2-0) Cohen, Saar; Matias, Yossi (2003). "Spectral bloom filters". [*Proceedings of the 2003 ACM SIGMOD international conference on Management of data*](https://web.archive.org/web/20210310041118/https://whiteblock.io/wp-content/uploads/2019/10/sbf-sigmod-03.pdf) (PDF). pp. 241–252. [doi](./Doi_(identifier)):[10.1145/872757.872787](https://doi.org/10.1145%2F872757.872787). [ISBN](./ISBN_(identifier)) [978-1581136340](./Special:BookSources/978-1581136340). [S2CID](./S2CID_(identifier)) [1058187](https://api.semanticscholar.org/CorpusID:1058187). Archived from [the original](https://whiteblock.io/wp-content/uploads/2019/10/sbf-sigmod-03.pdf) (PDF) on 2021-03-10.
3. [↑](./Counting_Bloom_filter#cite_ref-3) Deke Guo; Yunhao Liu; Xiangyang Li; Panlong Yang (2010). ["False Negative Problem of Counting Bloom Filter"](https://doi.org/10.1109/TKDE.2009.209). *IEEE Transactions on Knowledge and Data Engineering*. **22** (5): 651–664. [Bibcode](./Bibcode_(identifier)):[2010ITKDE..22..651G](https://ui.adsabs.harvard.edu/abs/2010ITKDE..22..651G). [doi](./Doi_(identifier)):[10.1109/TKDE.2009.209](https://doi.org/10.1109%2FTKDE.2009.209). [S2CID](./S2CID_(identifier)) [3934679](https://api.semanticscholar.org/CorpusID:3934679).
4. [↑](./Counting_Bloom_filter#cite_ref-4) Tarkoma, Sasu; Rothenberg, Christian Esteve; Lagerspetz, Eemil (2012). "Theory and Practice of Bloom Filters for Distributed Systems". *IEEE Communications Surveys & Tutorials*. **14** (1): 131–155. [Bibcode](./Bibcode_(identifier)):[2012ICST...14..131T](https://ui.adsabs.harvard.edu/abs/2012ICST...14..131T). [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.457.4228](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.457.4228). [doi](./Doi_(identifier)):[10.1109/surv.2011.031611.00024](https://doi.org/10.1109%2Fsurv.2011.031611.00024). [ISSN](./ISSN_(identifier)) [1553-877X](https://search.worldcat.org/issn/1553-877X). [S2CID](./S2CID_(identifier)) [17216682](https://api.semanticscholar.org/CorpusID:17216682).
5. [↑](./Counting_Bloom_filter#cite_ref-5) Lee, Sunggu; Lee, Youngjoo; Jeong, Yongjo; Kim, Kibeom (July 2019). ["Analysis of Counting Bloom Filters Used for Count Thresholding"](https://doi.org/10.3390%2Felectronics8070779). *Electronics*. **8** (7): 779. [doi](./Doi_(identifier)):[10.3390/electronics8070779](https://doi.org/10.3390%2Felectronics8070779).
6. [↑](./Counting_Bloom_filter#cite_ref-eppstein-2011_6-0) Eppstein, David; Goodrich, Michael T. (2011). "Straggler Identification in Round-Trip Data Streams via Newton's Identities and Invertible Bloom Filters". *IEEE Transactions on Knowledge and Data Engineering*. **23** (2): 297–306. [arXiv](./ArXiv_(identifier)):[0704.3313](https://arxiv.org/abs/0704.3313). [Bibcode](./Bibcode_(identifier)):[2011ITKDE..23..297E](https://ui.adsabs.harvard.edu/abs/2011ITKDE..23..297E). [doi](./Doi_(identifier)):[10.1109/TKDE.2010.132](https://doi.org/10.1109%2FTKDE.2010.132).
7. [1](./Counting_Bloom_filter#cite_ref-goodrich-2011_7-0) [2](./Counting_Bloom_filter#cite_ref-goodrich-2011_7-1) Goodrich, Michael T.; Mitzenmacher, Michael (2011). "Invertible bloom lookup tables". *2011 49th Annual Allerton Conference on Communication, Control, and Computing (Allerton)*. pp. 792–799. [arXiv](./ArXiv_(identifier)):[1101.2245](https://arxiv.org/abs/1101.2245). [doi](./Doi_(identifier)):[10.1109/Allerton.2011.6120248](https://doi.org/10.1109%2FAllerton.2011.6120248). [ISBN](./ISBN_(identifier)) [978-1-4577-1817-5](./Special:BookSources/978-1-4577-1817-5).
8. [↑](./Counting_Bloom_filter#cite_ref-8) Fleischhacker, Nils; Larsen, Kasper Green; Obremski, Maciej; Simkin, Mark (2024). ["Invertible Bloom Lookup Tables with Less Memory and Randomness"](https://doi.org/10.4230%2FLIPIcs.ESA.2024.54). *Leibniz International Proceedings in Informatics*. **308**: 54:1–54:17. [doi](./Doi_(identifier)):[10.4230/LIPIcs.ESA.2024.54](https://doi.org/10.4230%2FLIPIcs.ESA.2024.54).