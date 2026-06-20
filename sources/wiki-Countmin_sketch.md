---
source: https://en.wikipedia.org/wiki/Count–min_sketch
fetched: 2026-06-19
---

Probabilistic data structure in computer science 
| Part ofa serieson |
| --- |
| Probabilisticdata structures |
| Bloom filterCount sketchCount–min sketchQuotient filterSkip list |
| Random trees |
| Random binary treeTreapRapidly exploring random tree |
| Related |
| Randomized algorithmHyperLogLog |
| vte |

 

In [computing](./Computing), the **count–min sketch** (**CM sketch**) is a [probabilistic](./Randomized_algorithm) [data structure](./Data_structure) that serves as a frequency table of events in a [stream of data](./Streaming_algorithm). It uses [hash functions](./Hash_function) to map events to frequencies, but unlike a [hash table](./Hash_table) uses only [sub-linear space](./Space_complexity), at the expense of overcounting some events due to [collisions](./Hash_collision). The count–min sketch was invented in 2003 by Graham Cormode and [S. Muthu Muthukrishnan](./S._Muthu_Muthukrishnan)[[1]](./Count–min_sketch#cite_note-ency-1) and described by them in a 2005 paper.[[2]](./Count–min_sketch#cite_note-2)

 

Count–min sketch is an alternative to [count sketch](./Count_sketch) and AMS sketch and can be considered an implementation of a [counting Bloom filter](./Counting_Bloom_filter) (Fan et al., 1998[[3]](./Count–min_sketch#cite_note-3)) or multistage-filter.[[1]](./Count–min_sketch#cite_note-ency-1)  However, they are used differently and therefore sized differently: a count–min sketch typically has a sublinear number of cells, related to the desired approximation quality of the sketch, while a counting Bloom filter is more typically sized to match the number of elements in the set.

 

## Data structure

 

The goal of the basic version of the count–min sketch is to consume a stream of events, one at a time, and count the frequency of the different types of events in the stream. At any time, the sketch can be queried for the frequency of a particular event type i from a universe of event types       U     {\displaystyle {\mathcal {U}}}  ![{\displaystyle {\mathcal {U}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4e63ea009de5efbca2fc285b8550daaed577c6b8), and will return an estimate of this frequency that is within a certain distance of the true frequency, with a certain probability.[[a]](./Count–min_sketch#cite_note-4)

 

The actual sketch data structure is a two-dimensional array of w columns and d rows. The parameters w and d are fixed when the sketch is created, and determine the time and space needs and the probability of error when the sketch is queried for a frequency or [inner product](./Inner_product). Associated with each of the d rows is a separate hash function; the hash functions must be [pairwise independent](./Pairwise_independence). The parameters w and d can be chosen by setting *w* = ⌈*e*/*ε*⌉ and *d* = ⌈ln 1/*δ*⌉, where the error in answering a query is within an additive factor of ε with probability  1 − *δ* (see below), and *e* is [Euler's number](./Euler's_number).

 

When a new event of type i arrives we update as follows: for each row j of the table, apply the corresponding hash function to obtain a column index *k* = *h**j*(*i*). Then increment the value in row j, column k by one.

 

### Point Query

 

The *point query* asks for the count of an event type i. The estimated count is given by the least value in the table for i, namely         a ^ ^      i   =  min  j    c o u n t  [ j ,  h  j   ( i ) ]   {\displaystyle {\hat {a}}_{i}=\min _{j}\mathrm {count} [j,h_{j}(i)]}  ![{\displaystyle {\hat {a}}_{i}=\min _{j}\mathrm {count} [j,h_{j}(i)]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/12f24e88e904481b525a7a814a131ae51d838d80), where      c o u n t    {\displaystyle \mathrm {count} }  ![{\displaystyle \mathrm {count} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/f6ebfffcac182517c78a996ae1093d0c194228fb) is the table.

 

Obviously, for each i, one has      a  i   ≤ ≤      a ^ ^      i     {\displaystyle a_{i}\leq {\hat {a}}_{i}}  ![{\displaystyle a_{i}\leq {\hat {a}}_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2a393854c5deaad1ec8f078671d88a6bd6a616d6), where      a  i     {\displaystyle a_{i}}  ![{\displaystyle a_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0bc77764b2e74e64a63341054fa90f3e07db275f) is the true frequency with which i occurred in the stream.

 

Additionally, this estimate has the guarantee that         a ^ ^      i   ≤ ≤   a  i   + ε ε  N   {\displaystyle {\hat {a}}_{i}\leq a_{i}+\varepsilon N}  ![{\displaystyle {\hat {a}}_{i}\leq a_{i}+\varepsilon N}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5e0bd75c5d6544ed0e7f183bd75166331bbd7dbf) with probability     1 − −  δ δ    {\displaystyle 1-\delta }  ![{\displaystyle 1-\delta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/e7fc18b68a939b8f9eb465e354a64164a1202901), where     N =  ∑ ∑   i ∈ ∈    U      a  i     {\displaystyle N=\sum _{i\in {\mathcal {U}}}a_{i}}  ![{\displaystyle N=\sum _{i\in {\mathcal {U}}}a_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d5b64b521c82d9567bcc56ae157084c5f6aeb0f5) is the stream size, i.e. the total number of items seen by the sketch.

 

### Inner Product

 

An *inner product query* asks for the [inner product](./Inner_product) between the histograms represented by two count–min sketches,       c o u n t   a     {\displaystyle \mathrm {count} _{a}}  ![{\displaystyle \mathrm {count} _{a}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e37ecb8a1d516dd5613236288c613f0cdcb8d756) and       c o u n t   b     {\displaystyle \mathrm {count} _{b}}  ![{\displaystyle \mathrm {count} _{b}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e97873f91e09cc88d5f2182e6ce8942d225f9b6b).

 

Let          a ⋅ ⋅  b  ^ ^      j   =  ∑ ∑   k = 0   w     c o u n t   a   [ j , k ] ⋅ ⋅    c o u n t   b   [ j , k ]   {\displaystyle {\widehat {a\cdot b}}_{j}=\sum _{k=0}^{w}\mathrm {count} _{a}[j,k]\cdot \mathrm {count} _{b}[j,k]}  ![{\displaystyle {\widehat {a\cdot b}}_{j}=\sum _{k=0}^{w}\mathrm {count} _{a}[j,k]\cdot \mathrm {count} _{b}[j,k]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/12964472799680c102996fe00200838f8aa4b732). The inner product can then be estimated as         a ⋅ ⋅  b  ^ ^     =  min  j        a ⋅ ⋅  b  ^ ^      j     {\displaystyle {\widehat {a\cdot b}}=\min _{j}{\widehat {a\cdot b}}_{j}}  ![{\displaystyle {\widehat {a\cdot b}}=\min _{j}{\widehat {a\cdot b}}_{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b363b3febf2f1a02f643acb308f50917843841de).

 

One can show that     a ⋅ ⋅  b ≤ ≤      a ⋅ ⋅  b  ^ ^       {\displaystyle a\cdot b\leq {\widehat {a\cdot b}}}  ![{\displaystyle a\cdot b\leq {\widehat {a\cdot b}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3a3b33f223ce6015d1dea8d8e2f05ddbe3577cb), and with probability     1 − −  δ δ    {\displaystyle 1-\delta }  ![{\displaystyle 1-\delta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/e7fc18b68a939b8f9eb465e354a64164a1202901),         a ⋅ ⋅  b  ^ ^     ≤ ≤  a ⋅ ⋅  b + ε ε   |   |  a  |    |   1    |   |  b  |    |   1     {\displaystyle {\widehat {a\cdot b}}\leq a\cdot b+\varepsilon ||a||_{1}||b||_{1}}  ![{\displaystyle {\widehat {a\cdot b}}\leq a\cdot b+\varepsilon ||a||_{1}||b||_{1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c63612aa1052a5a477b59e5352198bc4e1cbee88).

 

### Merging Streams

 

Like the [count sketch](./Count_sketch), the Count–min sketch is a linear sketch. That is, given two streams, constructing a sketch on each stream and summing the sketches yields the same result as concatenating the streams and constructing a sketch on the concatenated streams. This makes the sketch mergeable and appropriate for use in distributed settings in addition to streaming ones.

 

## Reducing bias and error

 

One potential problem with the usual min estimator for count–min sketches is that they are [biased estimators](./Bias_of_an_estimator) of the true frequency of events: they may overestimate, but never underestimate the true count in a point query. Furthermore, while the min estimator works well when the distribution is highly skewed, other sketches such as the Count sketch based on means are more accurate when the distribution is not sufficiently skewed. Several variations on the sketch have been proposed to reduce error and reduce or eliminate bias.[[4]](./Count–min_sketch#cite_note-goyal-5)

 

To remove bias, the `hCount*` estimator
[[5]](./Count–min_sketch#cite_note-6)
repeatedly randomly selects d random entries in the sketch and takes the minimum to obtain an unbiased estimate of the bias and subtracts it off.

 

A [maximum likelihood estimator](./Maximum_likelihood_estimation) (MLE) was derived in Ting.[[6]](./Count–min_sketch#cite_note-Ting2018-7) By using the MLE, the estimator is always able to match or better the min estimator and works well even if the distribution is not skewed. This paper also showed the hCount* debiasing operation is a bootstrapping procedure that can be efficiently computed without random sampling and can be generalized to any estimator.

 

Since errors arise from hash collisions with unknown items from the universe, several approaches correct for the collisions when multiple elements of the universe are known or queried for simultaneously [[7]](./Count–min_sketch#cite_note-8) [[8]](./Count–min_sketch#cite_note-LuMontanari2008-9) [[6]](./Count–min_sketch#cite_note-Ting2018-7). For each of these, a large proportion of the universe must be known to observe a significant benefit.

 

*Conservative updating* changes the update, but not the query algorithms. To count c instances of event type i, one first computes an estimate         a ^ ^      i   =  min  j    c o u n t  [ j ,  h  j   ( i ) ]   {\displaystyle {\hat {a}}_{i}=\min _{j}\mathrm {count} [j,h_{j}(i)]}  ![{\displaystyle {\hat {a}}_{i}=\min _{j}\mathrm {count} [j,h_{j}(i)]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/12f24e88e904481b525a7a814a131ae51d838d80), then updates      c o u n t  [ j ,  h  j   ( i ) ] ← ←  max {  c o u n t  [ j ,  h  j   ( i ) ] ,     a  i   ^ ^     + c }   {\displaystyle \mathrm {count} [j,h_{j}(i)]\leftarrow \max\{\mathrm {count} [j,h_{j}(i)],{\hat {a_{i}}}+c\}}  ![{\displaystyle \mathrm {count} [j,h_{j}(i)]\leftarrow \max\{\mathrm {count} [j,h_{j}(i)],{\hat {a_{i}}}+c\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/90d2b8fbfaafb793895ddda34a4a43eee448f9f7) for each row j. While this update procedure makes the sketch not a linear sketch, it is still mergeable.

 

## See also

 
- [Feature hashing](./Feature_hashing)
- [Locality-sensitive hashing](./Locality-sensitive_hashing)
- [MinHash](./MinHash)

 

## Notes

  
1. [↑](./Count–min_sketch#cite_ref-4) The following discussion assumes that only "positive" events occur, i.e., the frequency of the various types cannot decrease over time. Modifications of the following algorithms exist for the more general case where frequencies are allowed to decrease.

 

## References

  
1. [1](./Count–min_sketch#cite_ref-ency_1-0) [2](./Count–min_sketch#cite_ref-ency_1-1) Cormode, Graham (2009). ["Count-min sketch"](http://dimacs.rutgers.edu/~graham/pubs/papers/cmencyc.pdf) (PDF). *Encyclopedia of Database Systems*. Springer. pp. 511–516.
2. [↑](./Count–min_sketch#cite_ref-2) Cormode, Graham; S. Muthukrishnan (2005). ["An Improved Data Stream Summary: The Count-Min Sketch and its Applications"](https://web.archive.org/web/20230525144650/http://dimacs.rutgers.edu/~graham/pubs/papers/cm-full.pdf) (PDF). *J. Algorithms*. **55**: 29–38. [doi](./Doi_(identifier)):[10.1016/j.jalgor.2003.12.001](https://doi.org/10.1016%2Fj.jalgor.2003.12.001). Archived from [the original](http://dimacs.rutgers.edu/~graham/pubs/papers/cm-full.pdf) (PDF) on 2023-05-25.
3. [↑](./Count–min_sketch#cite_ref-3) Fan, Li; [Cao, Pei](./Pei_Cao); [Almeida, Jussara](./Jussara_M._Almeida); [Broder, Andrei](./Andrei_Broder) (2000), "Summary Cache: A Scalable Wide-Area Web Cache Sharing Protocol", *IEEE/ACM Transactions on Networking*, **8** (3): 281–293, [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.41.1487](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.41.1487), [doi](./Doi_(identifier)):[10.1109/90.851975](https://doi.org/10.1109%2F90.851975), [S2CID](./S2CID_(identifier)) [4779754](https://api.semanticscholar.org/CorpusID:4779754). A preliminary version appeared at SIGCOMM '98.
4. [↑](./Count–min_sketch#cite_ref-goyal_5-0) Goyal, Amit; Daumé, Hal III; Cormode, Graham (2012). [*Sketch algorithms for estimating point queries in NLP*](http://www.aclweb.org/anthology/D12-1100). Proc. EMNLP/CoNLL.
5. [↑](./Count–min_sketch#cite_ref-6) Jin, C.; Qian, W.; Xu, X.; Zhou, A. (2003), *Dynamically maintaining frequent items over a data stream*, [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.151.5909](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.151.5909)
6. [1](./Count–min_sketch#cite_ref-Ting2018_7-0) [2](./Count–min_sketch#cite_ref-Ting2018_7-1) Ting, Daniel (2018). "Count-Min". *Proceedings of the 24th ACM SIGKDD International Conference on Knowledge Discovery & Data Mining*. pp. 2319–2328. [doi](./Doi_(identifier)):[10.1145/3219819.3219975](https://doi.org/10.1145%2F3219819.3219975). [ISBN](./ISBN_(identifier)) [9781450355520](./Special:BookSources/9781450355520).
7. [↑](./Count–min_sketch#cite_ref-8) Deng, Fan; Rafiei, Davood (2007), *New estimation algorithms for streaming data: Count-min can do more*, [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.552.1283](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.552.1283)
8. [↑](./Count–min_sketch#cite_ref-LuMontanari2008_9-0) Lu, Yi; Montanari, Andrea; Prabhakar, Balaji; Dharmapurikar, Sarang; Kabbani, Abdul (2008). "Counter braids". *ACM SIGMETRICS Performance Evaluation Review*. **36** (1): 121–132. [doi](./Doi_(identifier)):[10.1145/1384529.1375472](https://doi.org/10.1145%2F1384529.1375472). [ISSN](./ISSN_(identifier)) [0163-5999](https://search.worldcat.org/issn/0163-5999).

 

## Further reading

 
- Dwork, Cynthia; Naor, Moni; Pitassi, Toniann; Rothblum, Guy N.; Yekhanin, Sergey (2010). *Pan-private streaming algorithms*. Proc. ICS. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.165.5923](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.165.5923).
- Schechter, Stuart; Herley, Cormac; Mitzenmacher, Michael (2010). *Popularity is everything: A new approach to protecting passwords from statistical-guessing attacks*. USENIX Workshop on Hot Topics in Security. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.170.9356](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.170.9356).

 

## External links

 
- [Count–min FAQ](https://sites.google.com/site/countminsketch/home/faq)