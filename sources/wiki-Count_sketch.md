---
source: https://en.wikipedia.org/wiki/Count_sketch
fetched: 2026-06-19
---

Method of a dimension reduction 
| Part of a series on |
| --- |
| Machine learninganddata mining |
| ParadigmsSupervised learningUnsupervised learningSemi-supervised learningSelf-supervised learningReinforcement learningMeta-learningOnline learningBatch learningCurriculum learningRule-based learningNeuro-symbolic AINeuromorphic engineeringQuantum machine learning |
| ProblemsClassificationGenerative modelingRegressionClusteringDimensionality reductionDensity estimationAnomaly detectionData cleaningAutoMLAssociation rulesSemantic analysisStructured predictionFeature engineeringFeature learningLearning to rankGrammar inductionOntology learningMultimodal learning |
| Supervised learning(classification•regression)Apprenticeship learningDecision treesEnsemblesBaggingBoostingRandom forestk-NNLinear regressionNaive BayesArtificial neural networksLogistic regressionPerceptronRelevance vector machine (RVM)Support vector machine (SVM) |
| ClusteringBIRCHCUREHierarchicalk-meansFuzzyExpectation–maximization (EM)DBSCANOPTICSMean shift |
| Dimensionality reductionFactor analysisCCAICALDANMFPCAPGDt-SNESDL |
| Structured predictionGraphical modelsBayes netConditional random fieldHidden Markov |
| Anomaly detectionRANSACk-NNLocal outlier factorIsolation forest |
| Neural networksAutoencoderDeep learningFeedforward neural networkRecurrent neural networkLSTMGRUESNreservoir computingBoltzmann machineRestrictedGANDiffusion modelSOMConvolutional neural networkU-NetLeNetAlexNetDeepDreamNeural fieldNeural radiance fieldPhysics-informed neural networksTransformerVisionMambaSpiking neural networkMemtransistorElectrochemical RAM(ECRAM) |
| Reinforcement learningQ-learningPolicy gradientSARSATemporal difference (TD)Multi-agentSelf-play |
| Learning with humansActive learningCrowdsourcingHuman-in-the-loopMechanistic interpretabilityRLHF |
| Model diagnosticsCoefficient of determinationConfusion matrixLearning curveROC curve |
| Mathematical foundationsKernel machinesBias–variance tradeoffComputational learning theoryEmpirical risk minimizationOccam learningPAC learningStatistical learningVC theoryTopological deep learning |
| Journals and conferencesAAAICVPRECCVECML PKDDEMNLPICCVNeurIPSICMLICLRIJCAIMLJMLR |
| Related articlesGlossary of artificial intelligenceList of datasets for machine-learning researchList of datasets in computer vision and image processingOutline of machine learning |
| vte |

 

**Count sketch** is a type of [dimensionality reduction](./Dimensionality_reduction) that is particularly efficient in [statistics](./Statistics), [machine learning](./Machine_learning) and [algorithms](./Algorithms).[[1]](./Count_sketch#cite_note-1)[[2]](./Count_sketch#cite_note-2)
It was invented by Moses Charikar, Kevin Chen and Martin Farach-Colton[[3]](./Count_sketch#cite_note-FOOTNOTECharikarChenFarach-Colton2004-3) in an effort to speed up the [AMS Sketch](./AMS_Sketch?action=edit&redlink=1) by Alon, Matias and Szegedy for approximating the [frequency moments](./Frequency_moments) of streams[[4]](./Count_sketch#cite_note-4) (these calculations require counting of the number of occurrences for the distinct elements of the stream).

 

The sketch is nearly identical[*[citation needed](./Wikipedia:Citation_needed)*] to the [Feature hashing](./Feature_hashing) algorithm by John Moody,[[5]](./Count_sketch#cite_note-5) but differs in its use of hash functions with low dependence, which makes it more practical.
In order to still have a high probability of success, the [median trick](./Median_trick) is used to aggregate multiple count sketches, rather than the mean.

 

These properties allow use for explicit [kernel methods](./Kernel_methods), bilinear [pooling](./Pool_(computer_science)) in [neural networks](./Neural_network) and is a cornerstone in many numerical linear algebra algorithms.[[6]](./Count_sketch#cite_note-woodruff-6)

 

## Intuitive explanation

 

The inventors of this data structure offer the following iterative explanation of its operation:[[3]](./Count_sketch#cite_note-FOOTNOTECharikarChenFarach-Colton2004-3)

 
- at the simplest level, the output of a single [hash function](./Hash_function) s mapping stream elements q into {+1, -1} is feeding a single [up/down counter](./Up/down_counter) C. After a single pass over the data, the frequency     n ( q )   {\displaystyle n(q)}  ![{\displaystyle n(q)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bbd26739abf7d0b2055386c8a43df80e398167be) of a stream element q can be approximated, although extremely poorly, by the [expected value](./Expected_value)       E   [ C ⋅ ⋅  s ( q ) ]   {\displaystyle {\mathbf {E}}[C\cdot s(q)]}  ![{\displaystyle {\mathbf {E}}[C\cdot s(q)]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/549444c44abfd2b49bbd53d5941eeeab5dfbaf24);
- a straightforward way to improve the [variance](./Variance) of the previous estimate is to use an array of different hash functions      s  i     {\displaystyle s_{i}}  ![{\displaystyle s_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cfda82668232cbdc0874ed28ab8b6079420d1ffe), each connected to its own counter      C  i     {\displaystyle C_{i}}  ![{\displaystyle C_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cc49dc02c0ec8c86b67e7d10518ac791eda0bf22). For each i, the       E   [  C  i   ⋅ ⋅   s  i   ( q ) ] = n ( q )   {\displaystyle {\mathbf {E}}[C_{i}\cdot s_{i}(q)]=n(q)}  ![{\displaystyle {\mathbf {E}}[C_{i}\cdot s_{i}(q)]=n(q)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6362a0e4910219ddfc10965c128b06417dcd0234) still holds, so averaging across the i range will tighten the approximation;
- the previous construct still has a major deficiency: if a lower-frequency-but-still-important output element a exhibits a [hash collision](./Hash_collision) with a high-frequency element even for one of the      s  i     {\displaystyle s_{i}}  ![{\displaystyle s_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cfda82668232cbdc0874ed28ab8b6079420d1ffe) hashes,     n ( a )   {\displaystyle n(a)}  ![{\displaystyle n(a)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3c58a59f2e0de273efb93b7789d8be3481c55867) estimate can be significantly affected. Avoiding this requires reducing the frequency of collision counter updates between any two distinct elements. This is achieved by replacing each      C  i     {\displaystyle C_{i}}  ![{\displaystyle C_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cc49dc02c0ec8c86b67e7d10518ac791eda0bf22) in the previous construct with an array of m counters (making the counter set into a two-dimensional matrix      C  i , j     {\displaystyle C_{i,j}}  ![{\displaystyle C_{i,j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9db5b50c7da64c415db32937c1f213d74767d43d)), with index j of a particular counter to be incremented/decremented selected via another set of hash functions      h  i     {\displaystyle h_{i}}  ![{\displaystyle h_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d535f210cbd9b9fe6689e61427b3e213e5b2d547) that map element q into the range {1..m}. Since       E   [  C  i ,  h  i   ( q )   ⋅ ⋅   s  i   ( q ) ] = n ( q )   {\displaystyle {\mathbf {E}}[C_{i,h_{i}(q)}\cdot s_{i}(q)]=n(q)}  ![{\displaystyle {\mathbf {E}}[C_{i,h_{i}(q)}\cdot s_{i}(q)]=n(q)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/16c632865c72f6cfeeb5f4e032e1313122b52875), averaging across all values of i will work.

 

## Mathematical definition

 

1. For constants     w   {\displaystyle w}  ![{\displaystyle w}](https://wikimedia.org/api/rest_v1/media/math/render/svg/88b1e0c8e1be5ebe69d18a8010676fa42d7961e6) and     t   {\displaystyle t}  ![{\displaystyle t}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65658b7b223af9e1acc877d848888ecdb4466560) (to be defined later) independently choose     d = 2 t + 1   {\displaystyle d=2t+1}  ![{\displaystyle d=2t+1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7cf0cdb9f0677156a6e417cbc95504b238632f08) random hash functions
     h  1   , … …  ,  h  d     {\displaystyle h_{1},\dots ,h_{d}}  ![{\displaystyle h_{1},\dots ,h_{d}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5d32b0461278e990a2c4cb1a3dd22b1a27224008) and      s  1   , … …  ,  s  d     {\displaystyle s_{1},\dots ,s_{d}}  ![{\displaystyle s_{1},\dots ,s_{d}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a5cceb9df60465986b6fa27b21f06d5ac7670c6) such that
     h  i   : [ n ] → →  [ w ]   {\displaystyle h_{i}:[n]\to [w]}  ![{\displaystyle h_{i}:[n]\to [w]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6b4b940658be86ca48754ebdebd48542e26c99e5) and
     s  i   : [ n ] → →  { ± ±  1 }   {\displaystyle s_{i}:[n]\to \{\pm 1\}}  ![{\displaystyle s_{i}:[n]\to \{\pm 1\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d6f8f551947983fd6ed59bb8a67c37e5d86aa86a).
It is necessary that the hash families from which      h  i     {\displaystyle h_{i}}  ![{\displaystyle h_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d535f210cbd9b9fe6689e61427b3e213e5b2d547) and      s  i     {\displaystyle s_{i}}  ![{\displaystyle s_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cfda82668232cbdc0874ed28ab8b6079420d1ffe) are chosen be pairwise independent.

 

2. For each item      q  i     {\displaystyle q_{i}}  ![{\displaystyle q_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2752dcbff884354069fe332b8e51eb0a70a531b6) in the stream, add      s  j   (  q  i   )   {\displaystyle s_{j}(q_{i})}  ![{\displaystyle s_{j}(q_{i})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e88a81494065f6e786161d124aaa80f00f86f97e) to the      h  j   (  q  i   )   {\displaystyle h_{j}(q_{i})}  ![{\displaystyle h_{j}(q_{i})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2af81a08542a05152866f7e9a3ade406b6ba1ddf)th bucket of the     j   {\displaystyle j}  ![{\displaystyle j}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2f461e54f5c093e92a55547b9764291390f0b5d0)th hash.

 

At the end of this process, one has     w d   {\displaystyle wd}  ![{\displaystyle wd}](https://wikimedia.org/api/rest_v1/media/math/render/svg/77399091f774aaf60a965f40471ce01254563a60) sums     (  C  i j   )   {\displaystyle (C_{ij})}  ![{\displaystyle (C_{ij})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8c119e3519f8c30dc487addd72deff439f02e755) where

      C  i , j   =  ∑ ∑    h  i   ( k ) = j    s  i   ( k ) .   {\displaystyle C_{i,j}=\sum _{h_{i}(k)=j}s_{i}(k).}  ![{\displaystyle C_{i,j}=\sum _{h_{i}(k)=j}s_{i}(k).}](https://wikimedia.org/api/rest_v1/media/math/render/svg/13b809ee895455398569bc351e67a4ec633147e6) 

To estimate the count of     q   {\displaystyle q}  ![{\displaystyle q}](https://wikimedia.org/api/rest_v1/media/math/render/svg/06809d64fa7c817ffc7e323f85997f783dbdf71d)s one computes the following value:

      r  q   =   median   i = 1   d     s  i   ( q ) ⋅ ⋅   C  i ,  h  i   ( q )   .   {\displaystyle r_{q}={\text{median}}_{i=1}^{d}\,s_{i}(q)\cdot C_{i,h_{i}(q)}.}  ![{\displaystyle r_{q}={\text{median}}_{i=1}^{d}\,s_{i}(q)\cdot C_{i,h_{i}(q)}.}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bb4afd623a762dcd43a589716eebe09f0a71f001) 

The values      s  i   ( q ) ⋅ ⋅   C  i ,  h  i   ( q )     {\displaystyle s_{i}(q)\cdot C_{i,h_{i}(q)}}  ![{\displaystyle s_{i}(q)\cdot C_{i,h_{i}(q)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/853c6f3786ca2367cb95cf910ce5324fa3fa87bb) are unbiased estimates of how many times     q   {\displaystyle q}  ![{\displaystyle q}](https://wikimedia.org/api/rest_v1/media/math/render/svg/06809d64fa7c817ffc7e323f85997f783dbdf71d) has appeared in the stream.

 

The estimate      r  q     {\displaystyle r_{q}}  ![{\displaystyle r_{q}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b0bbfdfb65b656f31ac70a01d6a595e9a685662f) has variance     O (  m i n  {  m  1   2    /   w  2   ,  m  2   2    /  w } )   {\displaystyle O(\mathrm {min} \{m_{1}^{2}/w^{2},m_{2}^{2}/w\})}  ![{\displaystyle O(\mathrm {min} \{m_{1}^{2}/w^{2},m_{2}^{2}/w\})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ee5b2bc2bd3cdf23623d398e98239841a0244073), where
     m  1     {\displaystyle m_{1}}  ![{\displaystyle m_{1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/31aafa60e48d39ccce922404c0b80340b2cc777a) is the length of the stream and      m  2   2     {\displaystyle m_{2}^{2}}  ![{\displaystyle m_{2}^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/08f43502cecc78a19c1d8466d7552328bf8e0c19) is      ∑ ∑   q   (  ∑ ∑   i   [  q  i   = q ]  )  2     {\displaystyle \sum _{q}(\sum _{i}[q_{i}=q])^{2}}  ![{\displaystyle \sum _{q}(\sum _{i}[q_{i}=q])^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cd98d9c58acf155b1c8b68ad27f107174c0569a0).[[7]](./Count_sketch#cite_note-7)

 

Furthermore,      r  q     {\displaystyle r_{q}}  ![{\displaystyle r_{q}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b0bbfdfb65b656f31ac70a01d6a595e9a685662f) is guaranteed to never be more than     2  m  2    /    w     {\displaystyle 2m_{2}/{\sqrt {w}}}  ![{\displaystyle 2m_{2}/{\sqrt {w}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ccc75c695a40aa59ed312a3c5ebdf054ec48f4a1) off from the true value, with probability     1 − −   e  − −  O ( t )     {\displaystyle 1-e^{-O(t)}}  ![{\displaystyle 1-e^{-O(t)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9c2b0b34f8f88cc91f78eebbbdde26f30168cda4).

 

### Vector formulation

 

Alternatively Count-Sketch can be seen as a linear mapping with a non-linear reconstruction function.
Let      M  ( i ∈ ∈  [ d ] )   ∈ ∈  { − −  1 , 0 , 1  }  w × ×  n     {\displaystyle M^{(i\in [d])}\in \{-1,0,1\}^{w\times n}}  ![{\displaystyle M^{(i\in [d])}\in \{-1,0,1\}^{w\times n}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/eec419c2ed140e0dc5886d14ae86082d17c93abc), be a collection of     d = 2 t + 1   {\displaystyle d=2t+1}  ![{\displaystyle d=2t+1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7cf0cdb9f0677156a6e417cbc95504b238632f08) matrices, defined by

      M   h  i   ( j ) , j   ( i )   =  s  i   ( j )   {\displaystyle M_{h_{i}(j),j}^{(i)}=s_{i}(j)}  ![{\displaystyle M_{h_{i}(j),j}^{(i)}=s_{i}(j)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/31a3610e795eb5226c6a4edca43d67fc4ede8346) 

for     j ∈ ∈  [ w ]   {\displaystyle j\in [w]}  ![{\displaystyle j\in [w]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3f35332f39e0e823703ca1fe7eda05138a03ba3e) and 0 everywhere else.

 

Then a vector     v ∈ ∈    R   n     {\displaystyle v\in \mathbb {R} ^{n}}  ![{\displaystyle v\in \mathbb {R} ^{n}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/37576c57a5c8ee1c052cb82a6b88aaa4b41764f4) is sketched by      C  ( i )   =  M  ( i )   v ∈ ∈    R   w     {\displaystyle C^{(i)}=M^{(i)}v\in \mathbb {R} ^{w}}  ![{\displaystyle C^{(i)}=M^{(i)}v\in \mathbb {R} ^{w}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9ee533457d0df598ea9bf6a560ba3802ff971a02).
To reconstruct     v   {\displaystyle v}  ![{\displaystyle v}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e07b00e7fc0847fbd16391c778d65bc25c452597) we take      v  j   ∗ ∗    =   median   i    C  j   ( i )    s  i   ( j )   {\displaystyle v_{j}^{*}={\text{median}}_{i}C_{j}^{(i)}s_{i}(j)}  ![{\displaystyle v_{j}^{*}={\text{median}}_{i}C_{j}^{(i)}s_{i}(j)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cc8f565f6b7e4e8751dd65cfb0ae5592f5e984db).
This gives the same guarantees as stated above, if we take      m  1   = ‖ ‖  v  ‖ ‖   1     {\displaystyle m_{1}=\|v\|_{1}}  ![{\displaystyle m_{1}=\|v\|_{1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5d6e83eeeafb0499bef879894e12ab728a9c2c1b) and      m  2   = ‖ ‖  v  ‖ ‖   2     {\displaystyle m_{2}=\|v\|_{2}}  ![{\displaystyle m_{2}=\|v\|_{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/190b4d2394b5ae80697389a5410ca1d3c9571005).

 

## Relation to Tensor sketch

 

The count sketch projection of the [outer product](./Outer_product) of two vectors is equivalent to the [convolution](./Convolution) of two component count sketches. 

 

The count sketch computes a vector [convolution](./Convolution)

 

     C  ( 1 )   x ∗ ∗   C  ( 2 )    x  T     {\displaystyle C^{(1)}x\ast C^{(2)}x^{T}}  ![{\displaystyle C^{(1)}x\ast C^{(2)}x^{T}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/25606660b8a5303544e5e39decf537852d45519d), where      C  ( 1 )     {\displaystyle C^{(1)}}  ![{\displaystyle C^{(1)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ae3c15e27b657f8b6d30ec698e7d893d4921d700) and      C  ( 2 )     {\displaystyle C^{(2)}}  ![{\displaystyle C^{(2)}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e876190235296e1c619bba0a7f7fb6e81d14d564) are independent count sketch matrices.

 

Pham and Pagh[[8]](./Count_sketch#cite_note-ninh-8)  show that this equals     C ( x ⊗ ⊗   x  T   )   {\displaystyle C(x\otimes x^{T})}  ![{\displaystyle C(x\otimes x^{T})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bcc8c54c15d1d194cdf17c0cfce3bede1842e230) – a count sketch     C   {\displaystyle C}  ![{\displaystyle C}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4fc55753007cd3c18576f7933f6f089196732029) of the [outer product](./Outer_product) of vectors, where     ⊗ ⊗    {\displaystyle \otimes }  ![{\displaystyle \otimes }](https://wikimedia.org/api/rest_v1/media/math/render/svg/de29098f5a34ee296a505681a0d5e875070f2aea) denotes [Kronecker product](./Kronecker_product).

 

The [fast Fourier transform](./Fast_Fourier_transform) can be used to do fast convolution of count sketches.
By using the [face-splitting product](./Khatri–Rao_product#Face-splitting_product)[[9]](./Count_sketch#cite_note-9)[[10]](./Count_sketch#cite_note-10)[[11]](./Count_sketch#cite_note-11) such structures can be  computed much faster than normal matrices.

 

## See also

 
- [Count–min sketch](./Count–min_sketch) is a version of algorithm with smaller memory requirements (and weaker error guarantees as a tradeoff).
- [Tensor sketch](./Tensor_sketch)

 

## References

  
1. [↑](./Count_sketch#cite_ref-1) Faisal M. Algashaam; Kien Nguyen; Mohamed Alkanhal; Vinod Chandran; Wageeh Boles. "Multispectral Periocular Classification WithMultimodal Compact Multi-Linear Pooling" [1]. *IEEE Access*, Vol. 5. 2017.
2. [↑](./Count_sketch#cite_ref-2) Ahle, Thomas; Knudsen, Jakob (2019-09-03). ["Almost Optimal Tensor Sketch"](https://www.researchgate.net/publication/335617805). *[ResearchGate](./ResearchGate)*. Retrieved 2020-07-11.
3. [1](./Count_sketch#cite_ref-FOOTNOTECharikarChenFarach-Colton2004_3-0) [2](./Count_sketch#cite_ref-FOOTNOTECharikarChenFarach-Colton2004_3-1) [Charikar, Chen & Farach-Colton 2004](./Count_sketch#CITEREFCharikarChenFarach-Colton2004).
4. [↑](./Count_sketch#cite_ref-4) [Alon, Noga](./Noga_Alon), Yossi Matias, and Mario Szegedy. "The space complexity of approximating the frequency moments." Journal of Computer and system sciences 58.1 (1999): 137-147.
5. [↑](./Count_sketch#cite_ref-5) Moody, John. "Fast learning in multi-resolution hierarchies." Advances in neural information processing systems. 1989.
6. [↑](./Count_sketch#cite_ref-woodruff_6-0) Woodruff, David P. "Sketching as a Tool for Numerical Linear Algebra." Theoretical Computer Science 10.1-2 (2014): 1–157.
7. [↑](./Count_sketch#cite_ref-7) Larsen, Kasper Green, Rasmus Pagh, and Jakub Tětek. "CountSketches, Feature Hashing and the Median of Three." International Conference on Machine Learning. PMLR, 2021.
8. [↑](./Count_sketch#cite_ref-ninh_8-0) Ninh, Pham; [Pagh, Rasmus](./Rasmus_Pagh) (2013). *Fast and scalable polynomial kernels via explicit feature maps*. SIGKDD international conference on Knowledge discovery and data mining. Association for Computing Machinery. [doi](./Doi_(identifier)):[10.1145/2487575.2487591](https://doi.org/10.1145%2F2487575.2487591). 
9. [↑](./Count_sketch#cite_ref-9) Slyusar, V. I. (1998). ["End products in matrices in radar applications"](http://slyusar.kiev.ua/en/IZV_1998_3.pdf) (PDF). *Radioelectronics and Communications Systems*. **41** (3): 50–53.
10. [↑](./Count_sketch#cite_ref-10) Slyusar, V. I. (1997-05-20). ["Analytical model of the digital antenna array on a basis of face-splitting matrix products"](http://slyusar.kiev.ua/ICATT97.pdf) (PDF). *Proc. ICATT-97, Kyiv*: 108–109.
11. [↑](./Count_sketch#cite_ref-11) Slyusar, V. I. (March 13, 1998). ["A Family of Face Products of Matrices and its Properties"](http://slyusar.kiev.ua/FACE.pdf) (PDF). *Cybernetics and Systems Analysis C/C of Kibernetika I Sistemnyi Analiz.- 1999*. **35** (3): 379–384. [doi](./Doi_(identifier)):[10.1007/BF02733426](https://doi.org/10.1007%2FBF02733426). [S2CID](./S2CID_(identifier)) [119661450](https://api.semanticscholar.org/CorpusID:119661450).

 

## Further reading

 
- Charikar, Moses; Chen, Kevin; Farach-Colton, Martin (2004). ["Finding frequent items in data streams"](https://people.cs.rutgers.edu/~farach/pubs/FrequentStream.pdf) (PDF). *Theoretical Computer Science*. **312** (1). Elsevier BV: 3–15. [doi](./Doi_(identifier)):[10.1016/s0304-3975(03)00400-6](https://doi.org/10.1016%2Fs0304-3975%2803%2900400-6). [ISSN](./ISSN_(identifier)) [0304-3975](https://search.worldcat.org/issn/0304-3975).
- Faisal M. Algashaam; Kien Nguyen; Mohamed Alkanhal; Vinod Chandran; Wageeh Boles. "Multispectral Periocular Classification WithMultimodal Compact Multi-Linear Pooling" [](https://ieeexplore.ieee.org/document/7990127). *IEEE Access*, Vol. 5. 2017.
- Ahle, Thomas; Knudsen, Jakob (2019-09-03). ["Almost Optimal Tensor Sketch"](https://www.researchgate.net/publication/335617805). *[ResearchGate](./ResearchGate)*. Retrieved 2020-07-11.