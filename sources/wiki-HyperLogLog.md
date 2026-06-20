---
source: https://en.wikipedia.org/wiki/HyperLogLog
fetched: 2026-06-19
---

Approximate distinct counting algorithm 
| Part ofa serieson |
| --- |
| Probabilisticdata structures |
| Bloom filterCount sketchCount–min sketchQuotient filterSkip list |
| Random trees |
| Random binary treeTreapRapidly exploring random tree |
| Related |
| Randomized algorithmHyperLogLog |
| vte |

 

**HyperLogLog** is an algorithm for the [count-distinct problem](./Count-distinct_problem), approximating the number of distinct elements in a [multiset](./Multiset).[[1]](./HyperLogLog#cite_note-flajolet07-1) Calculating the *exact* [cardinality](./Cardinality) of the distinct elements of a multiset requires an amount of memory proportional to the cardinality, which is impractical for very large data sets. Probabilistic cardinality estimators, such as the HyperLogLog algorithm, use significantly less memory than this, but can only approximate the cardinality. The HyperLogLog algorithm is able to estimate cardinalities of > 109 with a typical accuracy (standard error) of 2%, using 1.5 kB of memory.[[1]](./HyperLogLog#cite_note-flajolet07-1) HyperLogLog is an extension of the earlier LogLog algorithm,[[2]](./HyperLogLog#cite_note-2) itself deriving from the 1984 [Flajolet–Martin algorithm](./Flajolet–Martin_algorithm).[[3]](./HyperLogLog#cite_note-3)

 

## Terminology

 

In the original paper by Flajolet *et al.*[[1]](./HyperLogLog#cite_note-flajolet07-1) and in related literature on the [count-distinct problem](./Count-distinct_problem), the term "cardinality" is used to mean the number of distinct elements in a data stream with repeated elements. However in the theory of [multisets](./Multiset) the term refers to the sum of multiplicities of each member of a multiset. This article chooses to use Flajolet's definition for consistency with the sources.

 

## Algorithm

 
|  | This section includes a list ofgeneral references, butit lacks sufficient correspondinginline citations.Please help toimprovethis section byintroducingmore precise citations.(March 2014)(Learn how and when to remove this message) |
| --- | --- |

 

The basis of the HyperLogLog algorithm is the observation that the cardinality of a multiset of uniformly distributed random numbers can be estimated by calculating the maximum number of leading zeros in the binary representation of each number in the set. If the maximum number of leading zeros observed is *n*, an estimate for the number of distinct elements in the set is 2*n*.[[1]](./HyperLogLog#cite_note-flajolet07-1)

 

In the HyperLogLog algorithm, a [hash function](./Hash_function) is applied to each element in the original multiset to obtain a multiset of uniformly distributed random numbers with the same cardinality as the original multiset. The cardinality of this randomly distributed set can then be estimated using the algorithm above.

 

The simple estimate of cardinality obtained using the algorithm above has the disadvantage of a large [variance](./Variance). In the HyperLogLog algorithm, the variance is minimised by splitting the multiset into numerous subsets, calculating the maximum number of leading zeros in the numbers in each of these subsets, and using a [harmonic mean](./Harmonic_mean) to combine these estimates for each subset into an estimate of the cardinality of the whole set.[[4]](./HyperLogLog#cite_note-4)

 

## Operations

 

The HyperLogLog has three main operations: **add** to add a new element to the set, **count** to obtain the cardinality of the set and **merge** to obtain the union of two sets. Some derived operations can be computed using the [inclusion–exclusion principle](./Inclusion–exclusion_principle) like the **cardinality of the intersection** or the **cardinality of the difference** between two HyperLogLogs combining the merge and count operations.

 

The data of the HyperLogLog is stored in an array M of m counters (or "registers") that are initialized to 0. Array M initialized from a multiset S is called *HyperLogLog* *sketch of S.*

 

### Add

 

The add operation consists of computing the hash of the input data v with a hash function h, getting the first b bits (where b is      log  2   ⁡ ⁡  ( m )   {\textstyle \log _{2}(m)}  ![{\textstyle \log _{2}(m)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/95735c3a3c5a568b42111f1451d101a2b861c127)), and adding 1 to them to obtain the address of the register to modify (assuming 1-based indexing). With the remaining bits as w, compute     ρ ρ  ( w )   {\textstyle \rho (w)}  ![{\textstyle \rho (w)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fafb04c8aab1309752c24c827f0f0d1c507ac0e8) which returns the position of the leftmost 1, where leftmost position is 1 (in other words: number of leading zeros plus 1). The new value of the register will be the maximum between the current value of the register and     ρ ρ  ( w )   {\textstyle \rho (w)}  ![{\textstyle \rho (w)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fafb04c8aab1309752c24c827f0f0d1c507ac0e8).

         x    := h ( v )     j    := 1 + ⟨ ⟨   x  1    x  2   . . .  x  b    ⟩ ⟩   2       w    :=  x  b + 1    x  b + 2   . . .     M [ j ]    := max ( M [ j ] , ρ ρ  ( w ) )       {\displaystyle {\begin{aligned}x&:=h(v)\\j&:=1+\langle x_{1}x_{2}...x_{b}\rangle _{2}\\w&:=x_{b+1}x_{b+2}...\\M[j]&:=\max(M[j],\rho (w))\\\end{aligned}}}  ![{\displaystyle {\begin{aligned}x&:=h(v)\\j&:=1+\langle x_{1}x_{2}...x_{b}\rangle _{2}\\w&:=x_{b+1}x_{b+2}...\\M[j]&:=\max(M[j],\rho (w))\\\end{aligned}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3b96a38f25aa94d1094aa1f8b8ab35b4e68bdc1a) 

### Count

 

The count algorithm consists in computing the harmonic mean of the m registers, and using a constant to derive an estimate     E   {\textstyle E}  ![{\textstyle E}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6d934f67126f64e9c061b598b8941b8767a8d343) of the count:

     Z =   (    ∑ ∑   j = 1   m     2  − −  M [ j ]       )    − −  1     {\displaystyle Z={\Bigg (}\sum _{j=1}^{m}{2^{-M[j]}}{\Bigg )}^{-1}}  ![{\displaystyle Z={\Bigg (}\sum _{j=1}^{m}{2^{-M[j]}}{\Bigg )}^{-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ba02bb284d4653aa7bf6dc5699889991e6206978)      α α   m   =   (  m  ∫ ∫   0   ∞ ∞      (   log  2   ⁡ ⁡   (    2 + u   1 + u    )   )   m    d u  )   − −  1     {\displaystyle \alpha _{m}=\left(m\int _{0}^{\infty }\left(\log _{2}\left({\frac {2+u}{1+u}}\right)\right)^{m}\,du\right)^{-1}}  ![{\displaystyle \alpha _{m}=\left(m\int _{0}^{\infty }\left(\log _{2}\left({\frac {2+u}{1+u}}\right)\right)^{m}\,du\right)^{-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e68865b48f91a302624ca310c75f127ce64871ac)     E =  α α   m    m  2   Z   {\displaystyle E=\alpha _{m}m^{2}Z}  ![{\displaystyle E=\alpha _{m}m^{2}Z}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c6d0e1a31f1b07fae4a18356e5f5a32fcefd9ba2) 

The intuition is that n being the unknown cardinality of M, each subset      M  j     {\textstyle M_{j}}  ![{\textstyle M_{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e533cedf4b286ac7c493ac24d10ae582ca754ea4) will have     n  /  m   {\textstyle n/m}  ![{\textstyle n/m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d81869fb7f63283b9a28c1a5e81cebafdd4c2191) elements. Then 
     max  x ∈ ∈   M  j     ρ ρ  ( x )   {\textstyle \max _{x\in M_{j}}\rho (x)}  ![{\textstyle \max _{x\in M_{j}}\rho (x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a701e349c1222186e156f08a1bcf328eb67ef1aa) should be close to      log  2   ⁡ ⁡  ( n  /  m )   {\textstyle \log _{2}(n/m)}  ![{\textstyle \log _{2}(n/m)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3f8701d795ad9dcef11d1c659bfa59866cd7c2a0). The harmonic mean of 2 to these quantities is     m Z   {\textstyle mZ}  ![{\textstyle mZ}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2e76dde2f234215b77d33e82008911e43fbc6f72) which should be near     n  /  m   {\textstyle n/m}  ![{\textstyle n/m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d81869fb7f63283b9a28c1a5e81cebafdd4c2191). Thus,      m  2   Z   {\textstyle m^{2}Z}  ![{\textstyle m^{2}Z}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1c1d4d4b2bf3a6c3dfd79b1990dd24119cf857f4) should be n approximately.

 

Finally, the constant      α α   m     {\textstyle \alpha _{m}}  ![{\textstyle \alpha _{m}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/026a6f1a8e558ba29c844e2fa5e8794a449fd780) is introduced to correct a systematic multiplicative bias present in      m  2   Z   {\textstyle m^{2}Z}  ![{\textstyle m^{2}Z}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1c1d4d4b2bf3a6c3dfd79b1990dd24119cf857f4) due to hash collisions.

 

### Practical considerations

 

The constant      α α   m     {\textstyle \alpha _{m}}  ![{\textstyle \alpha _{m}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/026a6f1a8e558ba29c844e2fa5e8794a449fd780) is not simple to calculate, and can be approximated with the formula[[1]](./HyperLogLog#cite_note-flajolet07-1)

      α α   m   ≈ ≈    {    0.673 ,    for   m = 16 ;     0.697 ,    for   m = 32 ;     0.709 ,    for   m = 64 ;       0.7213  1 + 1.079  /  m    ,    for   m ≥ ≥  128.         {\displaystyle \alpha _{m}\approx {\begin{cases}0.673,&{\text{for }}m=16;\\0.697,&{\text{for }}m=32;\\0.709,&{\text{for }}m=64;\\{\frac {0.7213}{1+1.079/m}},&{\text{for }}m\geq 128.\end{cases}}}  ![{\displaystyle \alpha _{m}\approx {\begin{cases}0.673,&{\text{for }}m=16;\\0.697,&{\text{for }}m=32;\\0.709,&{\text{for }}m=64;\\{\frac {0.7213}{1+1.079/m}},&{\text{for }}m\geq 128.\end{cases}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e6b71afdcb75d8c389c2f72dc7c76b3bf1fb5f20) 

The HyperLogLog technique, though, is biased for small cardinalities below a threshold of       5 2   m   {\textstyle {\frac {5}{2}}m}  ![{\textstyle {\frac {5}{2}}m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65a4a43d22b8bcb342570e87220016b921c13a12). The original paper proposes using a different algorithm for small cardinalities known as Linear Counting.[[5]](./HyperLogLog#cite_note-5) In the case where the estimate provided above is less than the threshold     E <   5 2   m   {\textstyle E<{\frac {5}{2}}m}  ![{\textstyle E<{\frac {5}{2}}m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a7dcd3f5ef9ab555e38ee51a0b88621a0458dec3), the alternative calculation can be used:

 
1. Let     V   {\textstyle V}  ![{\textstyle V}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d67b50b7ba03a56fea637093cf80e12807852d19) be the count of registers equal to 0.
2. If     V = 0   {\textstyle V=0}  ![{\textstyle V=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/018df3d1710b7b88b6ba9e5dc72ba35667fb15ad), use the standard HyperLogLog estimator     E   {\textstyle E}  ![{\textstyle E}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6d934f67126f64e9c061b598b8941b8767a8d343) above.
3. Otherwise, use Linear Counting:      E  ⋆ ⋆    = m log ⁡ ⁡   (   m V   )    {\textstyle E^{\star }=m\log \left({\frac {m}{V}}\right)}  ![{\textstyle E^{\star }=m\log \left({\frac {m}{V}}\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4687cc3fd6dc8966e3e77c7218f8e8a824dbbc18)

 

Additionally, for very large cardinalities approaching the limit of the size of the registers (    E >    2  32   30     {\textstyle E>{\frac {2^{32}}{30}}}  ![{\textstyle E>{\frac {2^{32}}{30}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6fecb8904e0af1215dab635cd115a1f5313a636c) for 32-bit registers), the cardinality can be estimated with:

      E  ⋆ ⋆    = − −   2  32   log ⁡ ⁡   (  1 − −    E  2  32      )    {\displaystyle E^{\star }=-2^{32}\log \left(1-{\frac {E}{2^{32}}}\right)}  ![{\displaystyle E^{\star }=-2^{32}\log \left(1-{\frac {E}{2^{32}}}\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/04ce7a6f50a506ffafac15d85fdcc3c9e8e20364) 

With the above corrections for lower and upper bounds, the error can be estimated as     σ σ  = 1.04  /    m     {\textstyle \sigma =1.04/{\sqrt {m}}}  ![{\textstyle \sigma =1.04/{\sqrt {m}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0bf2803a3aff4ac13b057608e026fc32e97baecd).

 

### Merge

 

The merge operation for two HLLs (       h l l    1   ,    h l l    2     {\textstyle {\mathit {hll}}_{1},{\mathit {hll}}_{2}}  ![{\textstyle {\mathit {hll}}_{1},{\mathit {hll}}_{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88f402d4cde476659e5d5241a4b56f90aea1bce9)) consists in obtaining the maximum for each pair of registers     j : 1.. m   {\textstyle j:1..m}  ![{\textstyle j:1..m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/851875e3e85115aa6724d58ae33eebe8bf4b0238)

        h l l    union   [ j ] = max (    h l l    1   [ j ] ,    h l l    2   [ j ] )   {\displaystyle {\mathit {hll}}_{\text{union}}[j]=\max({\mathit {hll}}_{1}[j],{\mathit {hll}}_{2}[j])}  ![{\displaystyle {\mathit {hll}}_{\text{union}}[j]=\max({\mathit {hll}}_{1}[j],{\mathit {hll}}_{2}[j])}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fb32b58cc9d72c72eaac7e775ed9906df9b6de02) 

## Complexity

 

To analyze the complexity, the data streaming     ( ϵ ϵ  , δ δ  )   {\displaystyle (\epsilon ,\delta )}  ![{\displaystyle (\epsilon ,\delta )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7c713274f5fc4c0c8a1a8e561c72314c0c5f0db6) model[[6]](./HyperLogLog#cite_note-Heule13-6) is used, which analyzes the space necessary to get a     1 ± ±  ϵ ϵ    {\displaystyle 1\pm \epsilon }  ![{\displaystyle 1\pm \epsilon }](https://wikimedia.org/api/rest_v1/media/math/render/svg/d37e6d69e1298c45393222e17a2909a067e64737) approximation with a fixed success probability     1 − −  δ δ    {\displaystyle 1-\delta }  ![{\displaystyle 1-\delta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/e7fc18b68a939b8f9eb465e354a64164a1202901). The relative error of HLL is     1.04  /    m     {\displaystyle 1.04/{\sqrt {m}}}  ![{\displaystyle 1.04/{\sqrt {m}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/523a2a189149d7e0197e1002652d14115d9836d8) and it needs     O (  ϵ ϵ   − −  2   log ⁡ ⁡  log ⁡ ⁡  n + log ⁡ ⁡  n )   {\displaystyle O(\epsilon ^{-2}\log \log n+\log n)}  ![{\displaystyle O(\epsilon ^{-2}\log \log n+\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b91dbc7fede840194b0056177e025e5dc472a1ef) space, where n is the set cardinality and m is the number of registers (usually less than one byte size).

 

The **add** operation depends on the size of the output of the hash function. As this size is fixed, we can consider the running time for the add operation to be     O ( 1 )   {\displaystyle O(1)}  ![{\displaystyle O(1)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21).

 

The **count** and **merge** operations depend on the number of registers m and have a theoretical cost of     O ( m )   {\displaystyle O(m)}  ![{\displaystyle O(m)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a0ffd498cf521ce19814e6b7053f1f8ebb1d3c88). In some implementations ([Redis](./Redis))[[7]](./HyperLogLog#cite_note-7) the number of registers is fixed and the cost is considered to be     O ( 1 )   {\displaystyle O(1)}  ![{\displaystyle O(1)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) in the documentation.

 

## HLL++

 

The HyperLogLog++ algorithm proposes several improvements in the HyperLogLog algorithm to reduce memory requirements and increase accuracy in some ranges of cardinalities:[[6]](./HyperLogLog#cite_note-Heule13-6)

 
- 64-bit hash function is used instead of the 32 bits used in the original paper. This reduces the hash collisions for large cardinalities allowing to remove the large range correction.
- Some bias is found for small cardinalities when switching from linear counting to the HLL counting. An empirical bias correction is proposed to mitigate the problem.
- A sparse representation of the registers is proposed to reduce memory requirements for small cardinalities, which can be later transformed to a dense representation if the cardinality grows.

 

## Streaming HLL

 

When the data arrives in a single stream, the Historic [Inverse Probability](./Inverse_probability) or martingale estimator[[8]](./HyperLogLog#cite_note-8)[[9]](./HyperLogLog#cite_note-9)
significantly improves the accuracy of the HLL sketch and uses 36% less memory to achieve a given error level. This estimator is provably optimal for any duplicate insensitive approximate distinct counting sketch on a single stream.

 

The single stream scenario also leads to variants in the HLL sketch construction.
HLL-TailCut+ uses 45% less memory than the original HLL sketch but at the cost of being dependent on the data insertion order and not being able to merge sketches.[[10]](./HyperLogLog#cite_note-10)

 

## Further reading

 
- ["New cardinality estimation algorithms for HyperLogLog sketches"](https://oertl.github.io/hyperloglog-sketch-estimation-paper/paper/paper.pdf) (PDF). Retrieved 2016-10-29.

 

## References

  
1. [1](./HyperLogLog#cite_ref-flajolet07_1-0) [2](./HyperLogLog#cite_ref-flajolet07_1-1) [3](./HyperLogLog#cite_ref-flajolet07_1-2) [4](./HyperLogLog#cite_ref-flajolet07_1-3) [5](./HyperLogLog#cite_ref-flajolet07_1-4) Flajolet, Philippe; Fusy, Éric; Gandouet, Olivier; Meunier, Frédéric (2007). ["Hyperloglog: The analysis of a near-optimal cardinality estimation algorithm"](http://algo.inria.fr/flajolet/Publications/FlFuGaMe07.pdf) (PDF). *Discrete Mathematics and Theoretical Computer Science Proceedings*. **AH**. [Nancy, France](./Nancy,_France): 137–156. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.76.4286](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.76.4286). Retrieved 2016-12-11.  Note DMTCS published this in their conference proc. instead of their main journal, but the specific conference is not relevant – not like that's where it was first presented before submission, or where the algorithm got used: conf=AOFA '07: Proceedings of the 2007 International Conference on the Analysis of Algorithms 
2. [↑](./HyperLogLog#cite_ref-2) Durand, M.; Flajolet, P. (2003). ["LogLog counting of large cardinalities."](http://algo.inria.fr/flajolet/Publications/DuFl03-LNCS.pdf) (PDF). In G. Di Battista and U. Zwick (ed.). *Lecture Notes in Computer Science*. Annual European Symposium on Algorithms (ESA03). Vol. 2832. Springer. pp. 605–617.
3. [↑](./HyperLogLog#cite_ref-3) Flajolet, Philippe; Martin, G. Nigel (1985). ["Probabilistic counting algorithms for data base applications"](http://algo.inria.fr/flajolet/Publications/FlMa85.pdf) (PDF). *Journal of Computer and System Sciences*. **31** (2): 182–209. [doi](./Doi_(identifier)):[10.1016/0022-0000(85)90041-8](https://doi.org/10.1016%2F0022-0000%2885%2990041-8).
4. [↑](./HyperLogLog#cite_ref-4) S Heule; M Nunkesser; A Hall (2013). ["HyperLogLog in Practice: Algorithmic Engineering of a State of The Art Cardinality Estimation Algorithm"](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/40671.pdf) (PDF). sec 4.
5. [↑](./HyperLogLog#cite_ref-5) Whang, Kyu-Young; Vander-Zanden, Brad T; Taylor, Howard M (1990). ["A linear-time probabilistic counting algorithm for database applications"](https://doi.org/10.1145%2F78922.78925). *ACM Transactions on Database Systems*. **15** (2): 208–229. [doi](./Doi_(identifier)):[10.1145/78922.78925](https://doi.org/10.1145%2F78922.78925). [S2CID](./S2CID_(identifier)) [2939101](https://api.semanticscholar.org/CorpusID:2939101).
6. [1](./HyperLogLog#cite_ref-Heule13_6-0) [2](./HyperLogLog#cite_ref-Heule13_6-1) ["HyperLogLog in Practice: Algorithmic Engineering of a State of The Art Cardinality Estimation Algorithm"](http://research.google.com/pubs/pub40671.html). Retrieved 2014-04-19.
7. [↑](./HyperLogLog#cite_ref-7) ["PFCOUNT – Redis"](https://redis.io/commands/pfcount).
8. [↑](./HyperLogLog#cite_ref-8) Cohen, E. (March 2015). "All-distances sketches, revisited: HIP estimators for massive graphs analysis". *IEEE Transactions on Knowledge and Data Engineering*. **27** (9): 2320–2334. [arXiv](./ArXiv_(identifier)):[1306.3284](https://arxiv.org/abs/1306.3284). [doi](./Doi_(identifier)):[10.1109/TKDE.2015.2411606](https://doi.org/10.1109%2FTKDE.2015.2411606).
9. [↑](./HyperLogLog#cite_ref-9)  Ting, D. (August 2014). ["Streamed approximate counting of distinct elements"](https://research.fb.com/publications/streamed-approximate-counting-of-distinct-elements/). *Proceedings of the 20th ACM SIGKDD international conference on Knowledge discovery and data mining*. pp. 442–451. [doi](./Doi_(identifier)):[10.1145/2623330.2623669](https://doi.org/10.1145%2F2623330.2623669). [ISBN](./ISBN_(identifier)) [978-1-4503-2956-9](./Special:BookSources/978-1-4503-2956-9). [S2CID](./S2CID_(identifier)) [13179875](https://api.semanticscholar.org/CorpusID:13179875).
10. [↑](./HyperLogLog#cite_ref-10) Xiao, Q.; Zhou, Y.; Chen, S. (May 2017). "Better with fewer bits: Improving the performance of cardinality estimation of large data streams". *IEEE INFOCOM 2017 - IEEE Conference on Computer Communications*. pp. 1–9. [doi](./Doi_(identifier)):[10.1109/INFOCOM.2017.8057088](https://doi.org/10.1109%2FINFOCOM.2017.8057088). [ISBN](./ISBN_(identifier)) [978-1-5090-5336-0](./Special:BookSources/978-1-5090-5336-0). [S2CID](./S2CID_(identifier)) [27159273](https://api.semanticscholar.org/CorpusID:27159273).