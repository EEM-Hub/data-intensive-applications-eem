---
source: https://en.wikipedia.org/wiki/Idempotence
fetched: 2026-06-19
---

Property of operations For the concepts in algebra, see [Idempotent (ring theory)](./Idempotent_(ring_theory)) and [Idempotent matrix](./Idempotent_matrix). [![](//upload.wikimedia.org/wikipedia/commons/thumb/1/18/On_Off_-_Za%C5%82_Wy%C5%82_%283086204137%29.jpg/250px-On_Off_-_Za%C5%82_Wy%C5%82_%283086204137%29.jpg)](./File:On_Off_-_Zał_Wył_(3086204137).jpg)*On*/*Off* buttons of a train's [destination sign](./Destination_sign) control panel. Pressing the *On* button (green) is an idempotent operation, since it has the same effect whether done once or multiple times. Likewise, pressing *Off* is idempotent. 

**Idempotence** ([UK](./British_English): [/ˌɪdɛmˈpoʊtəns/](./Help:IPA/English),[[1]](./Idempotence#cite_note-1) [US](./American_English): [/ˈaɪdəm-/](./Help:IPA/English))[[2]](./Idempotence#cite_note-2) is the property of certain [operations](./Operation_(mathematics)) in [mathematics](./Mathematics) and [computer science](./Computer_science) whereby they can be applied multiple times without changing the result beyond the initial application. The concept of idempotence arises in a number of places in [abstract algebra](./Abstract_algebra) (in particular, in the theory of [projectors](./Projector_(linear_algebra)) and [closure operators](./Closure_operator)) and [functional programming](./Functional_programming) (in which it is connected to the property of [referential transparency](./Referential_transparency)).

 

The term was introduced by American mathematician [Benjamin Peirce](./Benjamin_Peirce) in 1870[[3]](./Idempotence#cite_note-3)[[4]](./Idempotence#cite_note-FOOTNOTEPolcinoSehgal2002[httpsbooksgooglecombooksid7m9P9hM4pCQCqIdempotencepgPA127_127]-4) in the context of elements of algebras that remain invariant when raised to a positive integer power, and literally means "(the quality of having) the same power", from *[idem](https://en.wiktionary.org/wiki/idem#Latin)* + *[potence](https://en.wiktionary.org/wiki/potence)* (same + power).

 

## Definition

 

An element     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) of a set     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) equipped with a [binary operator](./Binary_operator)     ⋅ ⋅    {\displaystyle \cdot }  ![{\displaystyle \cdot }](https://wikimedia.org/api/rest_v1/media/math/render/svg/ba2c023bad1bd39ed49080f729cbf26bc448c9ba) is said to be *idempotent* under     ⋅ ⋅    {\displaystyle \cdot }  ![{\displaystyle \cdot }](https://wikimedia.org/api/rest_v1/media/math/render/svg/ba2c023bad1bd39ed49080f729cbf26bc448c9ba) if[[5]](./Idempotence#cite_note-5)[[6]](./Idempotence#cite_note-6)

     x ⋅ ⋅  x = x   {\displaystyle x\cdot x=x}  ![{\displaystyle x\cdot x=x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2036c5a01da1f20a1d9a581bedb3025fc4464ddd). 

The *binary operation*     ⋅ ⋅    {\displaystyle \cdot }  ![{\displaystyle \cdot }](https://wikimedia.org/api/rest_v1/media/math/render/svg/ba2c023bad1bd39ed49080f729cbf26bc448c9ba) is said to be *idempotent* if[[7]](./Idempotence#cite_note-7)[[8]](./Idempotence#cite_note-8)

     x ⋅ ⋅  x = x   {\displaystyle x\cdot x=x}  ![{\displaystyle x\cdot x=x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2036c5a01da1f20a1d9a581bedb3025fc4464ddd) for all     x ∈ ∈  S   {\displaystyle x\in S}  ![{\displaystyle x\in S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/51186ba8afb2067573a9082d55dd383df1ea9214). 

## Examples

 
- In the [monoid](./Monoid)     (  N  , × ×  )   {\displaystyle (\mathbb {N} ,\times )}  ![{\displaystyle (\mathbb {N} ,\times )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/11b78e2261106e162d117bc41b38f87b0c71d136) of the [natural numbers](./Natural_number) with [multiplication](./Multiplication), only     0   {\displaystyle 0}  ![{\displaystyle 0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2aae8864a3c1fec9585261791a809ddec1489950) and     1   {\displaystyle 1}  ![{\displaystyle 1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/92d98b82a3778f043108d4e20960a9193df57cbf) are idempotent. Indeed,     0 × ×  0 = 0   {\displaystyle 0\times 0=0}  ![{\displaystyle 0\times 0=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4f0e6fbb14cd6906a2003365ea58e14f5b84f25e) and     1 × ×  1 = 1   {\displaystyle 1\times 1=1}  ![{\displaystyle 1\times 1=1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/226eaf9e45eea9a56f6a7f3993a6b20de0abe4bc).
- In the [monoid](./Monoid)     (  N  , + )   {\displaystyle (\mathbb {N} ,+)}  ![{\displaystyle (\mathbb {N} ,+)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0072a6ee0ab943ce24dc44083bd60d50739a0b1f) of the [natural numbers](./Natural_number) with [addition](./Addition), only     0   {\displaystyle 0}  ![{\displaystyle 0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2aae8864a3c1fec9585261791a809ddec1489950) is idempotent. Indeed, 0 + 0 = 0.
- In a [magma](./Magma_(algebra))     ( M , ⋅ ⋅  )   {\displaystyle (M,\cdot )}  ![{\displaystyle (M,\cdot )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8dc86a0f0f83580455b11737df738e30a314e49a), an [identity element](./Identity_element)     e   {\displaystyle e}  ![{\displaystyle e}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cd253103f0876afc68ebead27a5aa9867d927467) or an [absorbing element](./Absorbing_element)     a   {\displaystyle a}  ![{\displaystyle a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ffd2487510aa438433a2579450ab2b3d557e5edc), if it exists, is idempotent. Indeed,     e ⋅ ⋅  e = e   {\displaystyle e\cdot e=e}  ![{\displaystyle e\cdot e=e}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5b43fb6c2e14c5d3c2caeeb797df1cc2ff02a14b) and     a ⋅ ⋅  a = a   {\displaystyle a\cdot a=a}  ![{\displaystyle a\cdot a=a}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5700edc1e0a1d972ccef6badad306db6a97ed8a1).
- In a [group](./Group_(mathematics))     ( G , ⋅ ⋅  )   {\displaystyle (G,\cdot )}  ![{\displaystyle (G,\cdot )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1ccc71a6904c5ab99ecaab1c8ed69e20815d66da), the identity element     e   {\displaystyle e}  ![{\displaystyle e}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cd253103f0876afc68ebead27a5aa9867d927467) is the only idempotent element. Indeed, if     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) is an element of     G   {\displaystyle G}  ![{\displaystyle G}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f5f3c8921a3b352de45446a6789b104458c9f90b) such that     x ⋅ ⋅  x = x   {\displaystyle x\cdot x=x}  ![{\displaystyle x\cdot x=x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2036c5a01da1f20a1d9a581bedb3025fc4464ddd), then     x ⋅ ⋅  x = x ⋅ ⋅  e   {\displaystyle x\cdot x=x\cdot e}  ![{\displaystyle x\cdot x=x\cdot e}](https://wikimedia.org/api/rest_v1/media/math/render/svg/61f6b189793e6f162c1f273c0b76bfad697eb589) and finally     x = e   {\displaystyle x=e}  ![{\displaystyle x=e}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8ba47ab1931fc4886c5da08831962cc141d20655) by multiplying on the left by the [inverse element](./Inverse_element) of     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4).
- In the monoids     (   P   ( E ) , ∪ ∪  )   {\displaystyle ({\mathcal {P}}(E),\cup )}  ![{\displaystyle ({\mathcal {P}}(E),\cup )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ccfbea32f408aac9e7ced60f1d5813c158e2065c) and     (   P   ( E ) , ∩ ∩  )   {\displaystyle ({\mathcal {P}}(E),\cap )}  ![{\displaystyle ({\mathcal {P}}(E),\cap )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/303d2c0a347052d00613270551d502e0c7f446a9) of the [power set](./Power_set)       P   ( E )   {\displaystyle {\mathcal {P}}(E)}  ![{\displaystyle {\mathcal {P}}(E)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fdb9a5a97c7cb3db567ed6d470b51883427bb06a) of the set     E   {\displaystyle E}  ![{\displaystyle E}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4232c9de2ee3eec0a9c0a19b15ab92daa6223f9b) with [set union](./Union_(set_theory))     ∪ ∪    {\displaystyle \cup }  ![{\displaystyle \cup }](https://wikimedia.org/api/rest_v1/media/math/render/svg/e8ff7d0293ad19b43524a133ae5129f3d71f2040) and [set intersection](./Intersection_(set_theory))     ∩ ∩    {\displaystyle \cap }  ![{\displaystyle \cap }](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d4e886e6f5a28a33e073fb108440c152ecfe2d3) respectively,     ∪ ∪    {\displaystyle \cup }  ![{\displaystyle \cup }](https://wikimedia.org/api/rest_v1/media/math/render/svg/e8ff7d0293ad19b43524a133ae5129f3d71f2040) and     ∩ ∩    {\displaystyle \cap }  ![{\displaystyle \cap }](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d4e886e6f5a28a33e073fb108440c152ecfe2d3) are idempotent. Indeed,     x ∪ ∪  x = x   {\displaystyle x\cup x=x}  ![{\displaystyle x\cup x=x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/108f79f8433fddde44ff29507832d855bd03115d) for all     x ∈ ∈    P   ( E )   {\displaystyle x\in {\mathcal {P}}(E)}  ![{\displaystyle x\in {\mathcal {P}}(E)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bed5a3b0e86a77f71cdfe847db130ff9d190906a), and     x ∩ ∩  x = x   {\displaystyle x\cap x=x}  ![{\displaystyle x\cap x=x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6a18b6a50d656e962df7335fbe7d45ae1fdc350c) for all     x ∈ ∈    P   ( E )   {\displaystyle x\in {\mathcal {P}}(E)}  ![{\displaystyle x\in {\mathcal {P}}(E)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bed5a3b0e86a77f71cdfe847db130ff9d190906a).
- In the monoids     ( { 0 , 1 } , ∨ ∨  )   {\displaystyle (\{0,1\},\vee )}  ![{\displaystyle (\{0,1\},\vee )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bc8c7ae9cf935ecd2025a83cd5e9eb5c526d84f1) and     ( { 0 , 1 } , ∧ ∧  )   {\displaystyle (\{0,1\},\wedge )}  ![{\displaystyle (\{0,1\},\wedge )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/076d8ff7f1491d52e81e3d348ae443b16e51f374) of the [Boolean domain](./Boolean_domain) with [logical disjunction](./Logical_disjunction)     ∨ ∨    {\displaystyle \vee }  ![{\displaystyle \vee }](https://wikimedia.org/api/rest_v1/media/math/render/svg/7b76220c6805c9b465d6efbc7686c624f49f3023) and [logical conjunction](./Logical_conjunction)     ∧ ∧    {\displaystyle \wedge }  ![{\displaystyle \wedge }](https://wikimedia.org/api/rest_v1/media/math/render/svg/1caa4004cb216ef2930bb12fe805a76870caed94) respectively,     ∨ ∨    {\displaystyle \vee }  ![{\displaystyle \vee }](https://wikimedia.org/api/rest_v1/media/math/render/svg/7b76220c6805c9b465d6efbc7686c624f49f3023) and     ∧ ∧    {\displaystyle \wedge }  ![{\displaystyle \wedge }](https://wikimedia.org/api/rest_v1/media/math/render/svg/1caa4004cb216ef2930bb12fe805a76870caed94) are idempotent. Indeed,     x ∨ ∨  x = x   {\displaystyle x\vee x=x}  ![{\displaystyle x\vee x=x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d2c2ce55bccff3d2060b45b6ca5d31ffe568f318) for all     x ∈ ∈  { 0 , 1 }   {\displaystyle x\in \{0,1\}}  ![{\displaystyle x\in \{0,1\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/05013ded6c9801acf787923a2b8aa521f3542c57), and     x ∧ ∧  x = x   {\displaystyle x\wedge x=x}  ![{\displaystyle x\wedge x=x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/74a0173a1c4045f8bb3fdaccc2705cca178be122) for all     x ∈ ∈  { 0 , 1 }   {\displaystyle x\in \{0,1\}}  ![{\displaystyle x\in \{0,1\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/05013ded6c9801acf787923a2b8aa521f3542c57).
- In a [GCD domain](./GCD_domain) (for instance in      Z    {\displaystyle \mathbb {Z} }  ![{\displaystyle \mathbb {Z} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/449494a083e0a1fda2b61c62b2f09b6bee4633dc)), the operations of [GCD](./Greatest_common_divisor) and [LCM](./Least_common_multiple) are idempotent.
- In a [Boolean ring](./Boolean_ring), multiplication is idempotent.
- In a [Tropical semiring](./Tropical_semiring), addition is idempotent.
- In a [ring of quadratic matrices](./Matrix_ring), the [determinant](./Determinant) of an [idempotent matrix](./Idempotent_matrix) is either 0 or 1. If the determinant is 1, the matrix necessarily is the [identity matrix](./Identity_matrix).[[9]](./Idempotence#cite_note-9)

 

### Idempotent functions

 

In the monoid     (  E  E   , ∘ ∘  )   {\displaystyle (E^{E},\circ )}  ![{\displaystyle (E^{E},\circ )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5bb7f8c9497723b5de4ec37db7578bf9948fb076) of the functions from a set     E   {\displaystyle E}  ![{\displaystyle E}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4232c9de2ee3eec0a9c0a19b15ab92daa6223f9b) to itself (see [set exponentiation](./Function_(mathematics)#Set_exponentiation)) with [function composition](./Function_composition)     ∘ ∘    {\displaystyle \circ }  ![{\displaystyle \circ }](https://wikimedia.org/api/rest_v1/media/math/render/svg/99add39d2b681e2de7ff62422c32704a05c7ec31), idempotent elements are the functions     f : :  E → →  E   {\displaystyle f\colon E\to E}  ![{\displaystyle f\colon E\to E}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4f00fa197e33d2f97e56b1b7f0ee709a8c9bd8ee) such that     f ∘ ∘  f = f   {\displaystyle f\circ f=f}  ![{\displaystyle f\circ f=f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9172b7a50fccab6c28706005b1a6b8c5b16e9f0d),[[a]](./Idempotence#cite_note-10) that is such that     f ( f ( x ) ) = f ( x )   {\displaystyle f(f(x))=f(x)}  ![{\displaystyle f(f(x))=f(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/38659935ace510e86dba5dcd12812ce033fb3d74) for all     x ∈ ∈  E   {\displaystyle x\in E}  ![{\displaystyle x\in E}](https://wikimedia.org/api/rest_v1/media/math/render/svg/30b1971b01bc31d5b816f03cc7e1d9215d6c2ad8) (in other words, the image     f ( x )   {\displaystyle f(x)}  ![{\displaystyle f(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/202945cce41ecebb6f643f31d119c514bec7a074) of each element     x ∈ ∈  E   {\displaystyle x\in E}  ![{\displaystyle x\in E}](https://wikimedia.org/api/rest_v1/media/math/render/svg/30b1971b01bc31d5b816f03cc7e1d9215d6c2ad8) is a [fixed point](./Fixed_point_(mathematics)) of     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61)). For example:

 
- the [absolute value](./Absolute_value) is idempotent. Indeed,     abs ∘ ∘  abs = abs   {\displaystyle \operatorname {abs} \circ \operatorname {abs} =\operatorname {abs} }  ![{\displaystyle \operatorname {abs} \circ \operatorname {abs} =\operatorname {abs} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/3ea3a7c423bd4ea6d251ac6b74ae57500aa639e5), that is     abs ⁡ ⁡  ( abs ⁡ ⁡  ( x ) ) = abs ⁡ ⁡  ( x )   {\displaystyle \operatorname {abs} (\operatorname {abs} (x))=\operatorname {abs} (x)}  ![{\displaystyle \operatorname {abs} (\operatorname {abs} (x))=\operatorname {abs} (x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fe4976eb768d41a3732f2476a59af9ed54a698c2) for all     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4);
- [constant](./Constant_function) functions are idempotent;
- the [identity function](./Identity_function) is idempotent;
- the [floor](./Floor_and_ceiling_functions), [ceiling](./Floor_and_ceiling_functions) and [fractional part](./Fractional_part) functions are idempotent;
- the real part function      R e  ( z )   {\displaystyle \mathrm {Re} (z)}  ![{\displaystyle \mathrm {Re} (z)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a15375ae37e2b460e62f903dd02f6754bbdc084b) of a [complex number](./Complex_number), is idempotent.
- for most kinds of [average](./Average), taking the average of a set and putting it in a singleton set is idempotent:     { avg ⁡ ⁡  { avg ⁡ ⁡  {  x  1   , … …  ,  x  n   } } } = { avg ⁡ ⁡  {  x  1   , … …  ,  x  n   } }   {\displaystyle \{\operatorname {avg} \{\operatorname {avg} \{x_{1},\dots ,x_{n}\}\}\}=\{\operatorname {avg} \{x_{1},\dots ,x_{n}\}\}}  ![{\displaystyle \{\operatorname {avg} \{\operatorname {avg} \{x_{1},\dots ,x_{n}\}\}\}=\{\operatorname {avg} \{x_{1},\dots ,x_{n}\}\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4efd3c1cfe3fefb254c78bc91f9bc8084a28cab3)
- the [subgroup generated](./Generating_set_of_a_group) function from the power set of a group to itself is idempotent;
- the [convex hull](./Convex_hull) function from the power set of an [affine space](./Affine_space) over the [reals](./Real_number) to itself is idempotent;
- the [closure](./Closure_(topology)) and [interior](./Interior_(topology)) functions of the power set of a [topological space](./Topological_space) to itself are idempotent;
- the [Kleene star](./Kleene_star) and [Kleene plus](./Kleene_plus) functions of the power set of a monoid to itself are idempotent;
- the idempotent [endomorphisms](./Endomorphism) of a [vector space](./Vector_space) are its [projections](./Projection_(linear_algebra)).

 

If the set     E   {\displaystyle E}  ![{\displaystyle E}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4232c9de2ee3eec0a9c0a19b15ab92daa6223f9b) has     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) elements, we can partition it into     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40) chosen fixed points and     n − −  k   {\displaystyle n-k}  ![{\displaystyle n-k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b98e1d6a69bccd09a4b9b69bdf03a08c1706c8c1) non-fixed points under     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61), and then      k  n − −  k     {\displaystyle k^{n-k}}  ![{\displaystyle k^{n-k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/245397778f6c4997dcded72a5aa441a595b4cecf) is the number of different idempotent functions. Hence, taking into account all possible partitions,

      ∑ ∑   k = 0   n      (   n k   )     k  n − −  k     {\displaystyle \sum _{k=0}^{n}{n \choose k}k^{n-k}}  ![{\displaystyle \sum _{k=0}^{n}{n \choose k}k^{n-k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec984897822b87b73e3d4dd4a0ee13bb40163f4e) 

is the total number of possible idempotent functions on the set. The [integer sequence](./Integer_sequence) of the number of idempotent functions as given by the sum above for *n* = 0, 1, 2, 3, 4, 5, 6, 7, 8, ... starts with 1, 1, 3, 10, 41, 196, 1057, 6322, 41393, ... (sequence [A000248](//oeis.org/A000248) in the [OEIS](./On-Line_Encyclopedia_of_Integer_Sequences)).

 

Neither idempotence nor non-idempotence is preserved under function composition.[[b]](./Idempotence#cite_note-11) As an example for the former,     f ( x ) = x   {\displaystyle f(x)=x}  ![{\displaystyle f(x)=x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f690285952308aa49e3c6aac892df31cad6d1b06) [mod](./Modular_arithmetic) 3 and     g ( x ) = max ( x , 5 )   {\displaystyle g(x)=\max(x,5)}  ![{\displaystyle g(x)=\max(x,5)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7928dc5a32e3907d2b19a3a02d74b7dc4e7d2f6a) are both idempotent, but     f ∘ ∘  g   {\displaystyle f\circ g}  ![{\displaystyle f\circ g}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b2f61ca7838709fbae07dce9c0d513770f10cfae) is not,[[c]](./Idempotence#cite_note-12) although     g ∘ ∘  f   {\displaystyle g\circ f}  ![{\displaystyle g\circ f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/10b5ad4985af48d0fb7efa3c8afa5ad7d42bfc92) happens to be.[[d]](./Idempotence#cite_note-13) As an example for the latter, the negation function     ¬ ¬    {\displaystyle \neg }  ![{\displaystyle \neg }](https://wikimedia.org/api/rest_v1/media/math/render/svg/fa78fd02085d39aa58c9e47a6d4033ce41e02fad) on the Boolean domain is not idempotent, but     ¬ ¬  ∘ ∘  ¬ ¬    {\displaystyle \neg \circ \neg }  ![{\displaystyle \neg \circ \neg }](https://wikimedia.org/api/rest_v1/media/math/render/svg/467c2c120f004c69e3683b9cd7b4b90459791b15) is. Similarly, unary negation     − −  ( ⋅ ⋅  )   {\displaystyle -(\cdot )}  ![{\displaystyle -(\cdot )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/43cf0bc7d937b671141669deed30970700efbad9) of real numbers is not idempotent, but      − −  ( ⋅ ⋅  ) ∘ ∘  − −  ( ⋅ ⋅  )   {\displaystyle -(\cdot )\circ -(\cdot )}  ![{\displaystyle -(\cdot )\circ -(\cdot )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cc8ead1c27fff315a6a21bc5ca5d6397b727f296) is. In both cases, the composition is simply the [identity function](./Identity_function), which is idempotent.

 

### Idempotent morphisms

 

A morphism     f : x → →  x   {\displaystyle f:x\to x}  ![{\displaystyle f:x\to x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bc6f03798962baefbb4a1ac938d15154207c98c0) in a category is called *idempotent* if     f ∘ ∘  f = f   {\displaystyle f\circ f=f}  ![{\displaystyle f\circ f=f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9172b7a50fccab6c28706005b1a6b8c5b16e9f0d).[[10]](./Idempotence#cite_note-14) An idempotent is said to *split* if it can be written as     f = h ∘ ∘  g   {\displaystyle f=h\circ g}  ![{\displaystyle f=h\circ g}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8bf9ecaafec0e79beaba94302aa824e2c7de682) for some     g : x → →  y ,  h : y → →  x   {\displaystyle g:x\to y,\,h:y\to x}  ![{\displaystyle g:x\to y,\,h:y\to x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/7be76ff4417038db540b59ac2792785cce27b225) with     g ∘ ∘  h = id   {\displaystyle g\circ h=\operatorname {id} }  ![{\displaystyle g\circ h=\operatorname {id} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/42da680e8ae99d0c5537dcfeb01b9196c87e1cbf).

 

A category is said to be [idempotent complete](./Idempotent_complete) if every idempotent splits. For example,       S e t     {\displaystyle {\mathsf {Set}}}  ![{\displaystyle {\mathsf {Set}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/31488c9fed260a93d36653220c2bd75b771cc440) is idempotent complete.[[11]](./Idempotence#cite_note-15)

 

## Computer science meaning

 See also: [Referential transparency](./Referential_transparency), [Reentrant (subroutine)](./Reentrant_(subroutine)), [Stable sort](./Stable_sort), and [Command query separation](./Command_query_separation) 

In [computer science](./Computer_science), the term *idempotence* may have a different meaning depending on the context in which it is applied:

 
- in [imperative programming](./Imperative_programming), a [subroutine](./Subroutine) with [side effects](./Side_effect_(computer_science)) is idempotent if multiple calls to the subroutine have the same effect on the system state as a single call, in other words if the function from the system state space to itself associated with the subroutine is idempotent in the mathematical sense given in [the definition](./Idempotence#Definition);
- in [functional programming](./Functional_programming), a [pure function](./Pure_function) is idempotent if it is idempotent in the mathematical sense given in [the definition](./Idempotence#Definition).

 

This is a very useful property in many situations, as it means that an operation can be repeated or retried as often as necessary without causing unintended effects. With non-idempotent operations, the algorithm may have to keep track of whether the operation was already performed or not.

 

### Computer science examples

 

A function looking up a customer's name and address in a [database](./Database) is typically idempotent, since this will not cause the database to change. Similarly, a request for changing a customer's address to XYZ is typically idempotent, because the final address will be the same no matter how many times the request is submitted. However, a customer request for placing an order is typically not idempotent since multiple requests will lead to multiple orders being placed. A request for canceling a particular order is idempotent because no matter how many requests are made the order remains canceled.

 

A sequence of idempotent subroutines where at least one subroutine is different from the others, however, is not necessarily idempotent if a later subroutine in the sequence changes a value that an earlier subroutine depends on—*idempotence is not closed under sequential composition*. For example, suppose the initial value of a variable is 3 and there is a subroutine sequence that reads the variable, then changes it to 5, and then reads it again. Each step in the sequence is idempotent: both steps reading the variable have no side effects and the step changing the variable to 5 will always have the same effect no matter how many times it is executed. Nonetheless, executing the entire sequence once produces the output (3, 5), but executing it a second time produces the output (5, 5), so the sequence is not idempotent.

 {{Citation needed|date=December 2017}} please discuss this on talk page before reinstating  
```
int x = 3;
void inspect() { printf("%d\n", x); }
void change() { x = 5; }
void sequence() { inspect(); change(); inspect(); }

int main() {
  sequence();  // prints "3\n5\n"
  sequence();  // prints "5\n5\n"
  return 0;
}

```
 

In the [Hypertext Transfer Protocol](./Hypertext_Transfer_Protocol) (HTTP), idempotence and [safety](./Hypertext_Transfer_Protocol#Safe_methods) are the major attributes that separate [HTTP methods](./Hypertext_Transfer_Protocol#Request_methods). Of the major HTTP methods, GET, PUT, and DELETE should be implemented in an idempotent manner according to the standard, but POST doesn't need to be.[[12]](./Idempotence#cite_note-httpStd-methods-16) GET retrieves the state of a resource; PUT updates the state of a resource; and DELETE deletes a resource. As in the example above, reading data usually has no side effects, so it is idempotent (in fact [*nullipotent*](https://en.wiktionary.org/wiki/nullipotent)). Updating and deleting a given data are each usually idempotent as long as the request uniquely identifies the resource and only that resource again in the future. PUT and DELETE with unique identifiers reduce to the simple case of assignment to a variable of either a value or the null-value, respectively, and are idempotent for the same reason; the end result is always the same as the result of the initial execution, even if the response differs.[[13]](./Idempotence#cite_note-17)

 

Violation of the unique identification requirement in storage or deletion typically causes violation of idempotence.  For example, storing or deleting a given set of content without specifying a unique identifier: POST requests, which do not need to be idempotent, often do not contain unique identifiers, so the creation of the identifier is delegated to the receiving system which then creates a corresponding new record.  Similarly, PUT and DELETE requests with nonspecific criteria may result in different outcomes depending on the state of the system – for example, a request to delete the most recent record. In each case, subsequent executions will further modify the state of the system, so they are not idempotent.

 

In [event stream processing](./Event_stream_processing), idempotence refers to the ability of a system to produce the same outcome, even if the same file, event or message is received more than once.

 

In a [load–store architecture](./Load–store_architecture), instructions that might possibly cause a [page fault](./Page_fault) are idempotent. So if a page fault occurs, the [operating system](./Operating_system) can load the page from disk and then simply re-execute the faulted instruction.  In a processor where such instructions are not idempotent, dealing with page faults is much more complex.[[14]](./Idempotence#cite_note-18)[[15]](./Idempotence#cite_note-19)

 

When reformatting output, [pretty-printing](./Prettyprint) is expected to be idempotent. In other words, if the output is already "pretty", there should be nothing to do for the pretty-printer.[*[citation needed](./Wikipedia:Citation_needed)*]

 

In [service-oriented architecture](./Service-oriented_architecture) (SOA), a multiple-step orchestration process composed entirely of idempotent steps can be replayed without side-effects if any part of that process fails.

 

Many operations that are idempotent often have ways to "resume" a process if it is interrupted –  ways that finish much faster than starting all over from the beginning. For example, [resuming a file transfer](./Upload#Resumability_of_file_transfers), 
[synchronizing files](./Rsync),  creating a [software build](./Software_build), installing an application and all of its dependencies with a [package manager](./Package_manager), etc.

 

## Applied examples

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/6/6b/Colecci%C3%B3n_de_hombres_cruzando.JPG/250px-Colecci%C3%B3n_de_hombres_cruzando.JPG)](./File:Colección_de_hombres_cruzando.JPG)A typical crosswalk button is an example of an idempotent system. 

Applied examples that many people could encounter in their day-to-day lives include [elevator](./Elevator) call buttons and [crosswalk buttons](./Crosswalk_button).[[16]](./Idempotence#cite_note-20) The initial activation of the button moves the system into a requesting state, until the request is satisfied. Subsequent activations of the button between the initial activation and the request being satisfied have no effect, unless the system is designed to adjust the time for satisfying the request based on the number of activations.

 

Similarly, the elevator "close" button may be pressed many times to the same effect as once, since the doors close on a fixed  schedule – unless the "open" button is pressed. The "open" button is not idempotent, because each press adds further delay.

 

## See also

 
- [Biordered set](./Biordered_set)
- [Closure operator](./Closure_operator)
- [Fixed point (mathematics)](./Fixed_point_(mathematics))
- [Idempotent of a code](./Idempotent_of_a_code)
- [Idempotent analysis](./Idempotent_analysis)
- [Idempotent matrix](./Idempotent_matrix)
- [Idempotent relation](./Idempotent_relation) –  a generalization of idempotence to binary relations
- [Idempotent (ring theory)](./Idempotent_(ring_theory))
- [Involution (mathematics)](./Involution_(mathematics))
- [Iterated function](./Iterated_function)
- [List of matrices](./List_of_matrices)
- [Nilpotent](./Nilpotent)
- [Pure function](./Pure_function)
- [Referential transparency](./Referential_transparency)

 

## Notes

  
1. [↑](./Idempotence#cite_ref-10) This is an equation between functions. Two functions are equal if their domains and ranges agree, and their output values agree on their whole domain.
2. [↑](./Idempotence#cite_ref-11) If     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) and     g   {\displaystyle g}  ![{\displaystyle g}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d3556280e66fe2c0d0140df20935a6f057381d77) commute under composition (i.e. if     f ∘ ∘  g = g ∘ ∘  f   {\displaystyle f\circ g=g\circ f}  ![{\displaystyle f\circ g=g\circ f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/49a99c329a3375b7bb3b3074a0383284a5a02401)) then idempotency of both     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) and     g   {\displaystyle g}  ![{\displaystyle g}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d3556280e66fe2c0d0140df20935a6f057381d77) implies that of     f ∘ ∘  g   {\displaystyle f\circ g}  ![{\displaystyle f\circ g}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b2f61ca7838709fbae07dce9c0d513770f10cfae), since     ( f ∘ ∘  g ) ∘ ∘  ( f ∘ ∘  g ) = f ∘ ∘  ( g ∘ ∘  f ) ∘ ∘  g = f ∘ ∘  ( f ∘ ∘  g ) ∘ ∘  g = ( f ∘ ∘  f ) ∘ ∘  ( g ∘ ∘  g ) = f ∘ ∘  g   {\displaystyle (f\circ g)\circ (f\circ g)=f\circ (g\circ f)\circ g=f\circ (f\circ g)\circ g=(f\circ f)\circ (g\circ g)=f\circ g}  ![{\displaystyle (f\circ g)\circ (f\circ g)=f\circ (g\circ f)\circ g=f\circ (f\circ g)\circ g=(f\circ f)\circ (g\circ g)=f\circ g}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a23811b9a5e32a959ef2c7f7e82f584522ccaf4a), using the associativity of composition.
3. [↑](./Idempotence#cite_ref-12) e.g.     f ( g ( 7 ) ) = f ( 7 ) = 1   {\displaystyle f(g(7))=f(7)=1}  ![{\displaystyle f(g(7))=f(7)=1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bd798e9500703a5251ba5bbc4edbc265ca2943ac), but     f ( g ( 1 ) ) = f ( 5 ) = 2 ≠ ≠  1   {\displaystyle f(g(1))=f(5)=2\neq 1}  ![{\displaystyle f(g(1))=f(5)=2\neq 1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2ec9932488b0f4dec73d204db2e4977a7ce6b70c)
4. [↑](./Idempotence#cite_ref-13) Also showing that commutation of     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) and     g   {\displaystyle g}  ![{\displaystyle g}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d3556280e66fe2c0d0140df20935a6f057381d77) is not a [necessary condition](./Necessary_condition) for idempotency preservation.

 

## References

 
1. [↑](./Idempotence#cite_ref-1) ["idempotence"](http://www.oed.com/view/Entry/273873). *[Oxford English Dictionary](./Oxford_English_Dictionary)* (3rd ed.). Oxford University Press. 2010.
2. [↑](./Idempotence#cite_ref-2) ["idempotent"](http://www.merriam-webster.com/dictionary/idempotent). *[Merriam-Webster](./Merriam-Webster)*. [Archived](https://web.archive.org/web/20161019143953/http://www.merriam-webster.com/dictionary/idempotent) from the original on 2016-10-19.
3. [↑](./Idempotence#cite_ref-3) Original manuscript of 1870 lecture before National Academy of Sciences (Washington, DC, USA):  Peirce, Benjamin (1870) ["Linear associative algebra"](https://books.google.com/books?id=HqQKAAAAYAAJ&pg=PA16)  From pages 16–17:  "When an expression which is raised to the square or any higher power vanishes,  it may be called *nilpotent*; but when raised to a square or higher power it gives itself as the result, it may be called *idempotent*.
 
The defining equation of nilpotent and idempotent expressions are respectively An = 0 and An = A; but with reference to idempotent expressions, it will always be assumed that they are of the form An = A unless it be otherwise distinctly stated."

- Printed:  Peirce, Benjamin (1881). ["Linear associative algebra"](https://babel.hathitrust.org/cgi/pt?id=uc1.$b772370&seq=107). *American Journal of Mathematics*. **4** (1): 97–229. [doi](./Doi_(identifier)):[10.2307/2369153](https://doi.org/10.2307%2F2369153). [JSTOR](./JSTOR_(identifier)) [2369153](https://www.jstor.org/stable/2369153).  See p. 104.
- Reprinted:  Peirce, Benjamin (1882). [*Linear Associative Algebra*](https://ia903403.us.archive.org/33/items/linearassocalgeb00pierrich/linearassocalgeb00pierrich_bw.pdf) (PDF). New York, New York, USA: D. Van Nostrand. p. 8.

4. [↑](./Idempotence#cite_ref-FOOTNOTEPolcinoSehgal2002[httpsbooksgooglecombooksid7m9P9hM4pCQCqIdempotencepgPA127_127]_4-0) [Polcino & Sehgal 2002](./Idempotence#CITEREFPolcinoSehgal2002), p. [127](https://books.google.com/books?id=7m9P9hM4pCQC&q=Idempotence&pg=PA127).
5. [↑](./Idempotence#cite_ref-5) Valenza, Robert (2012). [*Linear Algebra: An Introduction to Abstract Mathematics*](https://books.google.com/books?id=7x8MCAAAQBAJ). Berlin: Springer Science & Business Media. p. 22. [ISBN](./ISBN_(identifier)) [9781461209010](./Special:BookSources/9781461209010). An element *s* of a magma such that *ss* = *s* is called *idempotent*.
6. [↑](./Idempotence#cite_ref-6) Doneddu, Alfred (1976). [*Polynômes et algèbre linéaire*](https://books.google.com/books?id=5Ry7AAAAIAAJ) (in French). Paris: Vuibert. p. 180. Soit *M* un magma, noté multiplicativement. On nomme idempotent de *M* tout élément *a* de *M* tel que *a*2 = *a*.
7. [↑](./Idempotence#cite_ref-7) George Grätzer (2003). [*General Lattice Theory*](https://archive.org/details/generallatticeth0000grat). Basel: Birkhäuser. [ISBN](./ISBN_(identifier)) [978-3-7643-6996-5](./Special:BookSources/978-3-7643-6996-5). Here: Sect.1.2, p.5.
8. [↑](./Idempotence#cite_ref-8) [Garrett Birkhoff](./Garrett_Birkhoff) (1967). *Lattice Theory*. Colloquium Publications. Vol. 25. Providence: Am. Math. Soc.. Here: Sect.I.5, p.8.
9. [↑](./Idempotence#cite_ref-9) Balmaceda, Jose Maria. ["Idempotents in Certain Matrix Rings Over Polynomial Rings"](https://dergipark.org.tr/tr/pub/ieja/issue/50849/662942). *International Electronic Journal of Algebra*. [doi](./Doi_(identifier)):[10.24330/IEJA.662942](https://doi.org/10.24330%2FIEJA.662942).
10. [↑](./Idempotence#cite_ref-14) [Mac Lane 1978](./Idempotence#CITEREFMac_Lane1978), Ch. I., § 5.
11. [↑](./Idempotence#cite_ref-15) [Mac Lane 1978](./Idempotence#CITEREFMac_Lane1978), Ch. I., § 5., Exercise 6.
12. [↑](./Idempotence#cite_ref-httpStd-methods_16-0) IETF, [Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](http://tools.ietf.org/html/rfc7231#section-4.2.2) [Archived](https://web.archive.org/web/20140608213403/http://tools.ietf.org/html/rfc7231) 2014-06-08 at the [Wayback Machine](./Wayback_Machine).  See also [HyperText Transfer Protocol](./Hypertext_Transfer_Protocol).
13. [↑](./Idempotence#cite_ref-17) ["Idempotent Methods"](https://datatracker.ietf.org/doc/html/rfc7231#section-4.2.2). [*Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content*](https://www.rfc-editor.org/rfc/rfc7231). [IETF](./Internet_Engineering_Task_Force). sec. 4.2.2. [doi](./Doi_(identifier)):[10.17487/RFC7231](https://doi.org/10.17487%2FRFC7231). [RFC](./Request_for_Comments) [7231](https://datatracker.ietf.org/doc/html/rfc7231). It knows that repeating the request will have the same intended effect, even if the original request succeeded, though the response might differ.
14. [↑](./Idempotence#cite_ref-18)  [John Ousterhout](./John_Ousterhout).
["Demand Paging"](https://web.stanford.edu/~ouster/cgi-bin/cs140-spring14/lecture.php?topic=paging).

15. [↑](./Idempotence#cite_ref-19) 
Marc A. de Kruijf.
["Compiler construction of idempotent regions and applications in architecture design"](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.259.7708&rep=rep1&type=pdf).
2012.
p. 10.

16. [↑](./Idempotence#cite_ref-20) ["Geared Traction Passenger Elevator Specification Guide Information/Instructions"](https://web.archive.org/web/20110523081716/http://www.nclabor.com/elevator/geartrac.pdf) (PDF). *NC Department Of Labor, Elevator Bureau*. 2002. Archived from [the original](http://www.nclabor.com/elevator/geartrac.pdf) (PDF) on 2011-05-23. For example, this design specification includes detailed algorithm for when elevator cars will respond to subsequent calls for service

 

## Further reading

  
- Goodearl, K. R. (1991), *von Neumann regular rings* (2 ed.), Malabar, FL: Robert E. Krieger Publishing Co. Inc., pp. xviii+412, [ISBN](./ISBN_(identifier)) [978-0-89464-632-4](./Special:BookSources/978-0-89464-632-4), [MR](./MR_(identifier)) [1150975](https://mathscinet.ams.org/mathscinet-getitem?mr=1150975)
- Gunawardena, Jeremy (1998), ["An introduction to idempotency"](http://www.hpl.hp.com/techreports/96/HPL-BRIMS-96-24.pdf) (PDF), in Gunawardena, Jeremy (ed.), *Idempotency. Based on a workshop, Bristol, UK, October 3–7, 1994*, Cambridge: [Cambridge University Press](./Cambridge_University_Press), pp. 1–49, [Zbl](./Zbl_(identifier)) [0898.16032](https://zbmath.org/?format=complete&q=an:0898.16032)
- ["Idempotent"](https://www.encyclopediaofmath.org/index.php?title=Idempotent), *[Encyclopedia of Mathematics](./Encyclopedia_of_Mathematics)*, [EMS Press](./European_Mathematical_Society), 2001 [1994]
- [Hazewinkel, Michiel](./Hazewinkel,_Michiel); Gubareni, Nadiya; Kirichenko, V. V. (2004), *Algebras, rings and modules. vol. 1*, Mathematics and its Applications, vol. 575, Dordrecht: Kluwer Academic Publishers, pp. xii+380, [ISBN](./ISBN_(identifier)) [978-1-4020-2690-4](./Special:BookSources/978-1-4020-2690-4), [MR](./MR_(identifier)) [2106764](https://mathscinet.ams.org/mathscinet-getitem?mr=2106764)
- [Lam, T. Y.](./Tsit_Yuen_Lam) (2001), *A first course in noncommutative rings*, Graduate Texts in Mathematics, vol. 131 (2 ed.), New York: Springer-Verlag, pp. xx+385, [doi](./Doi_(identifier)):[10.1007/978-1-4419-8616-0](https://doi.org/10.1007%2F978-1-4419-8616-0), [ISBN](./ISBN_(identifier)) [978-0-387-95183-6](./Special:BookSources/978-0-387-95183-6), [MR](./MR_(identifier)) [1838439](https://mathscinet.ams.org/mathscinet-getitem?mr=1838439)
- [Lang, Serge](./Serge_Lang) (1993), *[Algebra](./Algebra_(Lang))* (Third ed.), Reading, Mass.: Addison-Wesley, [ISBN](./ISBN_(identifier)) [978-0-201-55540-0](./Special:BookSources/978-0-201-55540-0), [Zbl](./Zbl_(identifier)) [0848.13001](https://zbmath.org/?format=complete&q=an:0848.13001) p. 443
- Peirce, Benjamin. [*Linear Associative Algebra*](http://legacy-www.math.harvard.edu/history/peirce_algebra/) 1870.
- Polcino Milies, César; Sehgal, Sudarshan K. (2002), [*An Introduction to Group Rings*](https://books.google.com/books?id=7m9P9hM4pCQC&q=Idempotence&pg=PA127), Algebras and Applications, vol. 1, Kluwer Academic Publishers, pp. [127](https://books.google.com/books?id=7m9P9hM4pCQC&q=Idempotence&pg=PA127), [ISBN](./ISBN_(identifier)) [978-1-4020-0238-0](./Special:BookSources/978-1-4020-0238-0), [MR](./MR_(identifier)) [1896125](https://mathscinet.ams.org/mathscinet-getitem?mr=1896125)
- [Mac Lane, Saunders](./Saunders_Mac_Lane) (1978). *[Categories for the Working Mathematician](./Categories_for_the_Working_Mathematician)* (Second ed.). New York, NY: Springer. [ISBN](./ISBN_(identifier)) [1441931236](./Special:BookSources/1441931236). [OCLC](./OCLC_(identifier)) [851741862](https://search.worldcat.org/oclc/851741862).

  

## External links

   [![Wikibooks logo](//upload.wikimedia.org/wikipedia/commons/thumb/f/fa/Wikibooks-logo.svg/40px-Wikibooks-logo.svg.png)](./File:Wikibooks-logo.svg) Wikibooks has more on the topic of: ***[Idempotence](https://en.wikibooks.org/wiki/Special:Search/Idempotence)***    [![Wikiversity logo](//upload.wikimedia.org/wikipedia/commons/thumb/0/0b/Wikiversity_logo_2017.svg/40px-Wikiversity_logo_2017.svg.png)](./File:Wikiversity_logo_2017.svg) Wikiversity has learning resources about ***[Portal:Computer Science](https://en.wikiversity.org/wiki/Portal:Computer%20Science)***  
- "[idempotent](http://foldoc.org/idempotent)" at the [Free On-line Dictionary of Computing](./Free_On-line_Dictionary_of_Computing)

 [Portal](./Wikipedia:Contents/Portals):
- [![icon](//upload.wikimedia.org/wikipedia/commons/thumb/3/3e/Nuvola_apps_edu_mathematics_blue-p.svg/20px-Nuvola_apps_edu_mathematics_blue-p.svg.png)](./File:Nuvola_apps_edu_mathematics_blue-p.svg) [Mathematics](./Portal:Mathematics)

**Idempotence** at Wikipedia's [sister projects](./Wikipedia:Wikimedia_sister_projects):
- [![Wiktionary logo](//upload.wikimedia.org/wikipedia/commons/thumb/9/99/Wiktionary-logo-en-v2.svg/20px-Wiktionary-logo-en-v2.svg.png)](./File:Wiktionary-logo-en-v2.svg)[**Definitions**](https://en.wiktionary.org/wiki/idempotence) from Wiktionary