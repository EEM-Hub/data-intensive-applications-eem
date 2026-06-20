---
source: https://en.wikipedia.org/wiki/Consistent_hashing
fetched: 2026-06-19
---

Hashing technique 
|  | This articlemay be too technical for most readers to understand.Pleasehelp improve ittomake it understandable to non-experts, without removing the technical details.(October 2024)(Learn how and when to remove this message) |
| --- | --- |

 

In [computer science](./Computer_science), **consistent hashing**[[1]](./Consistent_hashing#cite_note-KargerEtAl1997-1)[[2]](./Consistent_hashing#cite_note-nuggets-2) is a special kind of [hashing](./Hash_function) technique such that when a [hash table](./Hash_table) is resized, only     n  /  m   {\displaystyle n/m}  ![{\displaystyle n/m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e555a7e118f9dbc0c67bc579d736ce73d94773e3) keys need to be remapped on average where     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) is the number of keys and     m   {\displaystyle m}  ![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc) is the number of slots. Consistent hashing evenly distributes cache keys across [shards](./Shard_(database_architecture)), even if some of the shards crash or become unavailable.[[3]](./Consistent_hashing#cite_note-3) In contrast, in most traditional hash tables, a change in the number of array slots causes nearly all keys to be remapped because the mapping between the keys and the slots is defined by a [modular operation](./Modular_arithmetic).

 

Consistent hashing is used by [Content Delivery Networks](./Content_Delivery_Network) because it is useful for distributing requests for content from a rotating population of web servers. [Tim Berners-Lee](./Tim_Berners-Lee) credits consistent hashing algorithms, and [Daniel Lewin](./Daniel_Lewin) as their inventor, with solving the [slashdotting](./Slashdotting) problem which plagued the [World Wide Web](./World_Wide_Web) in the 1990s.[[4]](./Consistent_hashing#cite_note-4)

 

## History

 

The term "consistent hashing" was introduced by [David Karger](./David_Karger) *et al.* at [MIT](./MIT) for use in [distributed caching](./Distributed_cache), particularly for the [web](./World_Wide_Web).[[5]](./Consistent_hashing#cite_note-FOOTNOTERoughgardenValiant20212-5) This academic paper from 1997 in [Symposium on Theory of Computing](./Symposium_on_Theory_of_Computing) introduced the term "consistent hashing" as a way of distributing requests among a changing population of web servers.[[6]](./Consistent_hashing#cite_note-FOOTNOTERoughgardenValiant20217-6) Each slot is then represented by a server in a distributed system or cluster. The addition of a server and the removal of a server (during scalability or outage) requires only     n u m _ _  k e y s  /  n u m _ _  s l o t s   {\displaystyle num\_keys/num\_slots}  ![{\displaystyle num\_keys/num\_slots}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d54d4de974af2e564dae1463b1f4fbf35ab1c788) items to be re-shuffled when the number of slots (i.e. servers) change. The authors mention [linear hashing](./Linear_hashing) and its ability to handle sequential server addition and removal, while consistent hashing allows servers to be added and removed in an arbitrary order.
[[1]](./Consistent_hashing#cite_note-KargerEtAl1997-1) The paper was later re-purposed to address technical challenge of keeping track of a file in [peer-to-peer networks](./Peer-to-peer) such as a [distributed hash table](./Distributed_hash_table).[[7]](./Consistent_hashing#cite_note-FOOTNOTERoughgardenValiant20218-7)[[8]](./Consistent_hashing#cite_note-8)

 

[Teradata](./Teradata) used this technique in their distributed database[*[citation needed](./Wikipedia:Citation_needed)*], released in 1986, although they did not use this term. Teradata still uses the concept of a [hash table](./Hash_table) to fulfill exactly this purpose. [Akamai Technologies](./Akamai_Technologies) was founded in 1998 by the scientists [Daniel Lewin](./Daniel_Lewin) and [F. Thomson Leighton](./F._Thomson_Leighton) (co-authors of the article coining "consistent hashing"). In Akamai's content delivery network,[[9]](./Consistent_hashing#cite_note-9) consistent hashing is used to balance the load within a cluster of servers, while a [stable marriage](./Stable_marriage_problem) algorithm is used to balance load across clusters.[[2]](./Consistent_hashing#cite_note-nuggets-2)

 

Consistent hashing has also been used to reduce the impact of partial system failures in large web applications to provide robust caching without incurring the system-wide fallout of a failure.[[10]](./Consistent_hashing#cite_note-KargerEtAl1999-10) Consistent hashing is also the cornerstone of [distributed hash tables](./Distributed_hash_table) (DHTs), which employ hash values to partition a keyspace across a distributed set of nodes, then construct an overlay network of connected nodes that provide efficient node retrieval by key.

 

[Rendezvous hashing](./Rendezvous_hashing), designed in 1996, is a simpler and more general technique [*[citation needed](./Wikipedia:Citation_needed)*]. It achieves the goals of consistent hashing using the very different highest random weight (HRW) algorithm.

 should describe here why the "consistency" of consistent hashing is essential to DHTs  

## Basic technique

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/7/71/Consistent_Hashing_Sample_Illustration.png/250px-Consistent_Hashing_Sample_Illustration.png)](./File:Consistent_Hashing_Sample_Illustration.png)In this case, using consistent hashing would result in the "BLOB" getting stored server 139. A BLOB is mapped to the next server that appears on the circle in clockwise order until it reaches a server which is     ζ ζ  ≤ ≤   server ID    {\displaystyle \zeta \leq {\text{server ID}}}  ![{\displaystyle \zeta \leq {\text{server ID}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/12a2f8a234fd44dfff5d04ed5fa31cd36c471bfb) 

In the problem of [load balancing](./Load_balancing_(computing)), for example, when a [BLOB](./Binary_large_object) has to be assigned to one of     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) servers on a [cluster](./Computer_cluster), a standard hash function could be used in such a way that we calculate the hash value for that BLOB, assuming the resultant value of the hash is     β β    {\displaystyle \beta }  ![{\displaystyle \beta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/7ed48a5e36207156fb792fa79d29925d2f7901e8), we perform [modular operation](./Modular_arithmetic) with the number of servers (    n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) in this case) to determine the server in which we can place the BLOB:     ζ ζ  = β β    % %    n   {\displaystyle \zeta =\beta \ \%\ n}  ![{\displaystyle \zeta =\beta \ \%\ n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9f1cae2745f4fb66e1ffd65a724630475d5d7f39); hence the BLOB will be placed in the server whose      server ID    {\displaystyle {\text{server ID}}}  ![{\displaystyle {\text{server ID}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1536bfe5827e3bd28f0c1cf3524d4078ca7ac62c) is successor of     ζ ζ    {\displaystyle \zeta }  ![{\displaystyle \zeta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/d5c3916703cae7938143d38865f78f27faadd4ae) in this case. However, when a server is added or removed during outage or scaling (when     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) changes), all the BLOBs in every server should be reassigned and moved due to [rehashing](./Hash_table#Dynamic_resizing), but this operation is expensive.

 

Consistent hashing was designed to avoid the problem of having to reassign every BLOB when a server is added or removed throughout the cluster. The central idea is to use a hash function that maps both the BLOB and servers to a unit circle, usually     2 π π    {\displaystyle 2\pi }  ![{\displaystyle 2\pi }](https://wikimedia.org/api/rest_v1/media/math/render/svg/73efd1f6493490b058097060a572606d2c550a06) radians. For example,     ζ ζ  = Φ Φ    % %    360   {\displaystyle \zeta =\Phi \ \%\ 360}  ![{\displaystyle \zeta =\Phi \ \%\ 360}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6bed5b344f95897e2336a14ef9a34731f7bbfd33) (where     Φ Φ    {\displaystyle \Phi }  ![{\displaystyle \Phi }](https://wikimedia.org/api/rest_v1/media/math/render/svg/aed80a2011a3912b028ba32a52dfa57165455f24) is hash of a BLOB or server's identifier, like [IP address](./IP_address) or [UUID](./Universally_unique_identifier)). Each BLOB is then assigned to the next server that appears on the circle in clockwise order. Usually, [binary search algorithm](./Binary_search_algorithm) or [linear search](./Linear_search) is used to find a "spot" or server to place that particular BLOB in     O ( log ⁡ ⁡  N )   {\displaystyle O(\log N)}  ![{\displaystyle O(\log N)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/14eea297b4387decf341763c39dc038e05744272) or     O ( N )   {\displaystyle O(N)}  ![{\displaystyle O(N)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/78484c5c26cfc97bb3b915418caa09454421e80b) complexities respectively; and in every iteration, which happens in clockwise manner, an operation     ζ ζ    ≤ ≤    Ψ Ψ    {\displaystyle \zeta \ \leq \ \Psi }  ![{\displaystyle \zeta \ \leq \ \Psi }](https://wikimedia.org/api/rest_v1/media/math/render/svg/12213aa097020ec5710f55848ed8f7a4802154bb) (where     Ψ Ψ    {\displaystyle \Psi }  ![{\displaystyle \Psi }](https://wikimedia.org/api/rest_v1/media/math/render/svg/f5471531a3fe80741a839bc98d49fae862a6439a) is the value of the server within the cluster) is performed to find the server to place the BLOB. This provides an even distribution of BLOBs to servers. But, more importantly, if a server fails and is removed from the circle, only the BLOBs that were mapped to the failed server need to be reassigned to the next server in clockwise order. Likewise, if a new server is added, it is added to the unit circle, and only the BLOBs mapped to that server need to be reassigned.

 

Importantly, when a server is added or removed, the vast majority of the BLOBs maintain their prior server assignments, and the addition of      n  t h     {\displaystyle n^{th}}  ![{\displaystyle n^{th}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5d54f58e8109a3d758d6712278b03f6aea6e696c) server only causes     1  /  n   {\displaystyle 1/n}  ![{\displaystyle 1/n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f0e10667bad240500f5044257143510127e03d69) fraction of the BLOBs to relocate. Although the process of moving BLOBs across cache servers in the cluster depends on the context, commonly, the newly added cache server identifies its "predecessor" and moves all the BLOBs, whose mapping belongs to this server (i.e. whose hash value is less than that of the new server), from it. However, in the case of [web page caches](./Web_cache), in most implementations there is no involvement of moving or copying, assuming the cached BLOB is small enough. When a request hits a newly added cache server, a [cache miss](./Cache_(computing)#CACHE-MISS) happens and a request to the actual [web server](./Web_server) is made and the BLOB is cached locally for future requests. The redundant BLOBs on the previously used cache servers would be removed as per the [cache eviction policies](./Cache_replacement_policies).[[11]](./Consistent_hashing#cite_note-FOOTNOTERoughgardenValiant20216-11)

 

### Implementation

 

Let      h  b   ( x )   {\displaystyle h_{b}(x)}  ![{\displaystyle h_{b}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/42708b0e624c69a13c6f3f495254b9629307b98c) and      h  s   ( x )   {\displaystyle h_{s}(x)}  ![{\displaystyle h_{s}(x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/125e4cc169dcd847da58b17c1d05817264ada21c) be the hash functions used for the BLOB and server's unique identifier respectively. In practice, a [binary search tree](./Binary_search_tree) (BST) is used to dynamically maintain the      server ID    {\displaystyle {\text{server ID}}}  ![{\displaystyle {\text{server ID}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1536bfe5827e3bd28f0c1cf3524d4078ca7ac62c) within a cluster or hashring, and to find the successor or minimum within the BST, [tree traversal](./Tree_traversal) is used.

 Inserting     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) into the cluster Let     β β    {\displaystyle \beta }  ![{\displaystyle \beta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/7ed48a5e36207156fb792fa79d29925d2f7901e8) be the hash value of a BLOB such that,      h  b   ( x ) = β β    % %    360   {\displaystyle h_{b}(x)=\beta \ \%\ 360}  ![{\displaystyle h_{b}(x)=\beta \ \%\ 360}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9a4e0a83960d3a130e89339113f8c9dd85901e25) where     x ∈ ∈   B L O B    {\displaystyle x\in \mathrm {BLOB} }  ![{\displaystyle x\in \mathrm {BLOB} }](https://wikimedia.org/api/rest_v1/media/math/render/svg/b19a040e329b47bed16d46d74e2a3efa4b6681d9) and      h  b   ( x ) = ζ ζ    {\displaystyle h_{b}(x)=\zeta }  ![{\displaystyle h_{b}(x)=\zeta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/524cf3bac2eb6c3266517152597a8c5389957b38). To insert     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4), find the successor of     ζ ζ    {\displaystyle \zeta }  ![{\displaystyle \zeta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/d5c3916703cae7938143d38865f78f27faadd4ae) in the BST of      server ID    {\displaystyle {\text{server ID}}}  ![{\displaystyle {\text{server ID}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1536bfe5827e3bd28f0c1cf3524d4078ca7ac62c)s. If     ζ ζ    {\displaystyle \zeta }  ![{\displaystyle \zeta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/d5c3916703cae7938143d38865f78f27faadd4ae) is larger than all of the      server ID    {\displaystyle {\text{server ID}}}  ![{\displaystyle {\text{server ID}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1536bfe5827e3bd28f0c1cf3524d4078ca7ac62c)s, the BLOB is placed in the server with smallest      server ID    {\displaystyle {\text{server ID}}}  ![{\displaystyle {\text{server ID}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1536bfe5827e3bd28f0c1cf3524d4078ca7ac62c) value. Deleting     x   {\displaystyle x}  ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) from the cluster Find the successor of     ζ ζ    {\displaystyle \zeta }  ![{\displaystyle \zeta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/d5c3916703cae7938143d38865f78f27faadd4ae) in the BST, remove the BLOB from the returned      server ID    {\displaystyle {\text{server ID}}}  ![{\displaystyle {\text{server ID}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1536bfe5827e3bd28f0c1cf3524d4078ca7ac62c). If     ζ ζ    {\displaystyle \zeta }  ![{\displaystyle \zeta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/d5c3916703cae7938143d38865f78f27faadd4ae) has no successor, remove the BLOB from the smallest of the      server ID    {\displaystyle {\text{server ID}}}  ![{\displaystyle {\text{server ID}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1536bfe5827e3bd28f0c1cf3524d4078ca7ac62c)s.[[12]](./Consistent_hashing#cite_note-FOOTNOTEMoitra20162-12) Insert a server into cluster Let     Φ Φ    {\displaystyle \Phi }  ![{\displaystyle \Phi }](https://wikimedia.org/api/rest_v1/media/math/render/svg/aed80a2011a3912b028ba32a52dfa57165455f24) be the hash value of a server's identifier such that,      h  s   ( x ) = Φ Φ    % %    360   {\displaystyle h_{s}(x)=\Phi \ \%\ 360}  ![{\displaystyle h_{s}(x)=\Phi \ \%\ 360}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a2a331427486e33ab5590c35fb66db7d10c13daf) where     x ∈ ∈  {  IP address, UUID  }   {\displaystyle x\in \{{\text{IP address, UUID}}\}}  ![{\displaystyle x\in \{{\text{IP address, UUID}}\}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3a2af232a1840c7d0b5f6a04087e187f160427bf) and      h  s   ( x ) = θ θ    {\displaystyle h_{s}(x)=\theta }  ![{\displaystyle h_{s}(x)=\theta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/b372e4d13102b7efd7c0676cd5bd07d40c6f8b52). Move all the BLOBs, whose hash value is smaller than     θ θ    {\displaystyle \theta }  ![{\displaystyle \theta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/6e5ab2664b422d53eb0c7df3b87e1360d75ad9af), from the server whose      server ID    {\displaystyle {\text{server ID}}}  ![{\displaystyle {\text{server ID}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1536bfe5827e3bd28f0c1cf3524d4078ca7ac62c) is successor of     θ θ    {\displaystyle \theta }  ![{\displaystyle \theta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/6e5ab2664b422d53eb0c7df3b87e1360d75ad9af). If     θ θ    {\displaystyle \theta }  ![{\displaystyle \theta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/6e5ab2664b422d53eb0c7df3b87e1360d75ad9af) is largest of all the      server ID    {\displaystyle {\text{server ID}}}  ![{\displaystyle {\text{server ID}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1536bfe5827e3bd28f0c1cf3524d4078ca7ac62c)s, move the relevant BLOBs from the smallest of the      server ID    {\displaystyle {\text{server ID}}}  ![{\displaystyle {\text{server ID}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1536bfe5827e3bd28f0c1cf3524d4078ca7ac62c)s into     θ θ    {\displaystyle \theta }  ![{\displaystyle \theta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/6e5ab2664b422d53eb0c7df3b87e1360d75ad9af).[[13]](./Consistent_hashing#cite_note-FOOTNOTEMoitra20162–3-13) Delete a server from cluster Find the successor of     θ θ    {\displaystyle \theta }  ![{\displaystyle \theta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/6e5ab2664b422d53eb0c7df3b87e1360d75ad9af) in the BST, move the BLOBs from     θ θ    {\displaystyle \theta }  ![{\displaystyle \theta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/6e5ab2664b422d53eb0c7df3b87e1360d75ad9af) into its successor server. If     θ θ    {\displaystyle \theta }  ![{\displaystyle \theta }](https://wikimedia.org/api/rest_v1/media/math/render/svg/6e5ab2664b422d53eb0c7df3b87e1360d75ad9af) doesn't have a successor, move the BLOBs into the smallest of the      server ID    {\displaystyle {\text{server ID}}}  ![{\displaystyle {\text{server ID}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1536bfe5827e3bd28f0c1cf3524d4078ca7ac62c)s.[[14]](./Consistent_hashing#cite_note-FOOTNOTEMoitra20163-14) 

### Variance reduction

 

To avoid [skewness](./Skewness) of multiple nodes within the radian, which happen due to lack of [uniform distribution](./Discrete_uniform_distribution) of the servers within the cluster, multiple labels are used. Those duplicate labels are called "virtual nodes" i.e. multiple labels which point to a single "real" label or server within the cluster. The amount of virtual nodes or duplicate labels used for a particular server within a cluster is called the "weight" of that particular server.[[15]](./Consistent_hashing#cite_note-FOOTNOTERoughgardenValiant20216–7-15)

 

## Practical extensions

 

A number of extensions to the basic technique are needed for effectively using consistent hashing for load balancing in practice. In the basic scheme above, if a server fails, all its BLOBs are reassigned to the next server in clockwise order, potentially doubling the load of that server. This may not be desirable. To ensure a more even redistribution of BLOBs on server failure, each server can be hashed to multiple locations on the unit circle. When a server fails, the BLOBs assigned to each of its replicas on the unit circle will get reassigned to a different server in clockwise order, thus redistributing the BLOBs more evenly. Another extension concerns a situation where a single BLOB gets "hot" and is accessed a large number of times and will have to be hosted in multiple servers. In this situation, the BLOB may be assigned to multiple contiguous servers by traversing the unit circle in clockwise order. A more complex practical consideration arises when two BLOBs are hashed near each other in the unit circle and both get "hot" at the same time. In this case, both BLOBs will use the same set of contiguous servers in the unit circle. This situation can be ameliorated by each BLOB choosing a different hash function for mapping servers to the unit circle.[[2]](./Consistent_hashing#cite_note-nuggets-2)

 

## Comparison with rendezvous hashing and other alternatives

 Main article: [Rendezvous hashing  §  Comparison with consistent hashing](./Rendezvous_hashing#_Comparison_with_consistent_hashing) 

[Rendezvous hashing](./Rendezvous_hashing), designed in 1996, is a simpler and more general technique, and permits fully distributed agreement on a set of     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40) options out of a possible set of     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) options. [It can in fact be shown](./Rendezvous_hashing#Consistent_hashing_is_a_special_case_of_Rendezvous_hashing) that consistent hashing is a special case of rendezvous hashing. Because of its simplicity and generality, rendezvous hashing is now being used in place of Consistent Hashing in many applications.

 

If key values will always increase [monotonically](./Monotonic), an alternative approach using a [hash table with monotonic keys](./Hash_table#Monotonic_keys) may be more suitable than consistent hashing.[*[citation needed](./Wikipedia:Citation_needed)*]

 

## Complexity

 
|  | Classic hash table | Consistent hashing |
| --- | --- | --- |
| add a node | O(K){\displaystyle O(K)} | O(K/N+log⁡N){\displaystyle O(K/N+\log N)} |
| remove a node | O(K){\displaystyle O(K)} | O(K/N+log⁡N){\displaystyle O(K/N+\log N)} |
| lookup a key | O(1){\displaystyle O(1)} | O(log⁡N){\displaystyle O(\log N)} |
| add a key | O(1){\displaystyle O(1)} | O(log⁡N){\displaystyle O(\log N)} |
| remove a key | O(1){\displaystyle O(1)} | O(log⁡N){\displaystyle O(\log N)} |

 

The     O ( K  /  N )   {\displaystyle O(K/N)}  ![{\displaystyle O(K/N)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/dc1c249b4f2ab04eb9f3a69ecbc3419bd1fdbd9f) is an average cost for redistribution of keys and the     O ( log ⁡ ⁡  N )   {\displaystyle O(\log N)}  ![{\displaystyle O(\log N)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/14eea297b4387decf341763c39dc038e05744272) complexity for consistent hashing comes from the fact that a [binary search](./Binary_search_algorithm) among nodes angles is required to find the next node on the ring.[*[citation needed](./Wikipedia:Citation_needed)*]

 

## Examples

 

Known examples of consistent hashing use include:

 
- [Couchbase](./Couchbase) automated data partitioning [[16]](./Consistent_hashing#cite_note-16)
- [OpenStack's](./OpenStack) Object Storage Service Swift[[17]](./Consistent_hashing#cite_note-17)
- Partitioning component of Amazon's storage system [Dynamo](./Dynamo_(storage_system))[[18]](./Consistent_hashing#cite_note-Amazon2007-18)
- Data partitioning in [Apache Cassandra](./Apache_Cassandra)[[19]](./Consistent_hashing#cite_note-Lakshman2010b-19)
- Data partitioning in [ScyllaDB](./ScyllaDB)[[20]](./Consistent_hashing#cite_note-20)
- Data partitioning in [Voldemort](./Voldemort_(distributed_data_store))[[21]](./Consistent_hashing#cite_note-21)
- [Akka](./Akka_(toolkit))'s consistent hashing router[[22]](./Consistent_hashing#cite_note-akka-routing-22)
- [Riak](./Riak), a distributed key-value database[[23]](./Consistent_hashing#cite_note-riak-consistent-hashing-23)
- [Gluster](./Gluster), a network-attached storage file system[[24]](./Consistent_hashing#cite_note-GlusterFS_Algorithms:_Distribution-24)
- [Akamai](./Akamai_Technologies) content delivery network[[25]](./Consistent_hashing#cite_note-25)
- [Discord](./Discord_(software)) chat application[[26]](./Consistent_hashing#cite_note-how_discord_scaled_elixir_to_5,000,000_concurrent_users-26)
- Load balancing [gRPC](./GRPC) requests to a distributed cache in SpiceDB[[27]](./Consistent_hashing#cite_note-consistent_hash_load_balancing_for_gRPC-27)
- [Chord](./Chord_(peer-to-peer)) algorithm[[28]](./Consistent_hashing#cite_note-ChordTON2003-28)
- [MinIO](./MinIO) object storage system[[29]](./Consistent_hashing#cite_note-MinIO_Versioning,_Metadata_and_Storage_Deep_Dive-29)

 

## References

  
1. [1](./Consistent_hashing#cite_ref-KargerEtAl1997_1-0) [2](./Consistent_hashing#cite_ref-KargerEtAl1997_1-1) Karger, D.; Lehman, E.; [Leighton, T.](./F._Thomson_Leighton); Panigrahy, R.; Levine, M.; [Lewin, D.](./Daniel_M._Lewin) (1997). [*Consistent Hashing and Random Trees: Distributed Caching Protocols for Relieving Hot Spots on the World Wide Web*](http://portal.acm.org/citation.cfm?id=258660). Proceedings of the Twenty-Ninth Annual ACM [Symposium on Theory of Computing](./Symposium_on_Theory_of_Computing). ACM Press New York, NY, USA. pp. 654–663. [doi](./Doi_(identifier)):[10.1145/258533.258660](https://doi.org/10.1145%2F258533.258660).
2. [1](./Consistent_hashing#cite_ref-nuggets_2-0) [2](./Consistent_hashing#cite_ref-nuggets_2-1) [3](./Consistent_hashing#cite_ref-nuggets_2-2) Bruce Maggs and [Ramesh Sitaraman](./Ramesh_Sitaraman) (2015). ["Algorithmic nuggets in content delivery"](http://www.sigcomm.org/sites/default/files/ccr/papers/2015/July/0000000-0000009.pdf) (PDF). *ACM SIGCOMM Computer Communication Review*. **45** (3).
3. [↑](./Consistent_hashing#cite_ref-3) *Designing Distributed Systems Patterns and Paradigms for Scalable, Reliable Services*. O'Reilly Media. 2018. [ISBN](./ISBN_(identifier)) [9781491983607](./Special:BookSources/9781491983607).
4. [↑](./Consistent_hashing#cite_ref-4) Berners-Lee, Tim (2025). *This is for Everyone: the unfinished story of the World Wide Web*. Farrar, Straus and Giroux. p. 156. [ISBN](./ISBN_(identifier)) [978-0-374-61246-7](./Special:BookSources/978-0-374-61246-7).
5. [↑](./Consistent_hashing#cite_ref-FOOTNOTERoughgardenValiant20212_5-0) [Roughgarden & Valiant 2021](./Consistent_hashing#CITEREFRoughgardenValiant2021), p. 2.
6. [↑](./Consistent_hashing#cite_ref-FOOTNOTERoughgardenValiant20217_6-0) [Roughgarden & Valiant 2021](./Consistent_hashing#CITEREFRoughgardenValiant2021), p. 7.
7. [↑](./Consistent_hashing#cite_ref-FOOTNOTERoughgardenValiant20218_7-0) [Roughgarden & Valiant 2021](./Consistent_hashing#CITEREFRoughgardenValiant2021), p. 8.
8. [↑](./Consistent_hashing#cite_ref-8) I. Stoica et al., "Chord: a scalable peer-to-peer lookup protocol for Internet applications," in IEEE/ACM Transactions on Networking, vol. 11, no. 1, pp. 17–32, Feb. 2003, doi: 10.1109/TNET.2002.808407.
9. [↑](./Consistent_hashing#cite_ref-9) Nygren., E.; Sitaraman R. K.; Sun, J. (2010). ["The Akamai Network: A Platform for High-Performance Internet Applications"](https://www.akamai.com/site/en/documents/research-paper/the-akamai-network-a-platform-for-high-performance-internet-applications-technical-publication.pdf) (PDF). *ACM SIGOPS Operating Systems Review*. **44** (3): 2–19. [doi](./Doi_(identifier)):[10.1145/1842733.1842736](https://doi.org/10.1145%2F1842733.1842736). [S2CID](./S2CID_(identifier)) [207181702](https://api.semanticscholar.org/CorpusID:207181702). [Archived](https://web.archive.org/web/20221130124826/https://www.akamai.com/site/en/documents/research-paper/the-akamai-network-a-platform-for-high-performance-internet-applications-technical-publication.pdf) (PDF) from the original on November 30, 2022. Retrieved August 29, 2023.
10. [↑](./Consistent_hashing#cite_ref-KargerEtAl1999_10-0) Karger, D.; Sherman, A.; Berkheimer, A.; Bogstad, B.; Dhanidina, R.; Iwamoto, K.; Kim, B.; Matkins, L.; Yerushalmi, Y. (1999). ["Web Caching with Consistent Hashing"](https://web.archive.org/web/20080721013638/http://www8.org/w8-papers/2a-webserver/caching/paper2.html). *Computer Networks*. **31** (11): 1203–1213. [doi](./Doi_(identifier)):[10.1016/S1389-1286(99)00055-9](https://doi.org/10.1016%2FS1389-1286%2899%2900055-9). Archived from [the original](http://www8.org/w8-papers/2a-webserver/caching/paper2.html) on 2008-07-21. Retrieved 2008-02-05.
11. [↑](./Consistent_hashing#cite_ref-FOOTNOTERoughgardenValiant20216_11-0) [Roughgarden & Valiant 2021](./Consistent_hashing#CITEREFRoughgardenValiant2021), p. 6.
12. [↑](./Consistent_hashing#cite_ref-FOOTNOTEMoitra20162_12-0) [Moitra 2016](./Consistent_hashing#CITEREFMoitra2016), p. 2.
13. [↑](./Consistent_hashing#cite_ref-FOOTNOTEMoitra20162–3_13-0) [Moitra 2016](./Consistent_hashing#CITEREFMoitra2016), p. 2–3.
14. [↑](./Consistent_hashing#cite_ref-FOOTNOTEMoitra20163_14-0) [Moitra 2016](./Consistent_hashing#CITEREFMoitra2016), p. 3.
15. [↑](./Consistent_hashing#cite_ref-FOOTNOTERoughgardenValiant20216–7_15-0) [Roughgarden & Valiant 2021](./Consistent_hashing#CITEREFRoughgardenValiant2021), p. 6–7.
16. [↑](./Consistent_hashing#cite_ref-16) ["What Exactly Is Membase?"](https://blog.couchbase.com/what-exactly-membase/). 16 December 2014. Retrieved 2020-10-29.
17. [↑](./Consistent_hashing#cite_ref-17) Holt, Greg (February 2011). ["Building a Consistent Hashing Ring"](https://docs.openstack.org/swift/latest/ring_background.html). *openstack.org*. Retrieved 2019-11-17.
18. [↑](./Consistent_hashing#cite_ref-Amazon2007_18-0) DeCandia, G.; Hastorun, D.; Jampani, M.; Kakulapati, G.; Lakshman, A.; Pilchin, A.; Sivasubramanian, S.; Vosshall, P.; [Vogels, Werner](./Werner_Vogels) (2007). ["Dynamo"](http://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf) (PDF). *ACM SIGOPS Operating Systems Review*. **41** (6): 205–220. [doi](./Doi_(identifier)):[10.1145/1323293.1294281](https://doi.org/10.1145%2F1323293.1294281). Retrieved 2018-06-07.
19. [↑](./Consistent_hashing#cite_ref-Lakshman2010b_19-0) Lakshman, Avinash; Malik, Prashant (2010). "Cassandra: a decentralized structured storage system". *ACM SIGOPS Operating Systems Review*. **44** (2): 35–40. [doi](./Doi_(identifier)):[10.1145/1773912.1773922](https://doi.org/10.1145%2F1773912.1773922). [S2CID](./S2CID_(identifier)) [916681](https://api.semanticscholar.org/CorpusID:916681).
20. [↑](./Consistent_hashing#cite_ref-20) ["NoSQL Comparison: MongoDB vs ScyllaDB"](https://benchant.com/blog/mongodb-vs-scylladb-comparison). *benchant.com*. Retrieved 21 March 2024.
21. [↑](./Consistent_hashing#cite_ref-21) ["Design -- Voldemort"](https://web.archive.org/web/20150209164650/http://www.project-voldemort.com/voldemort/design.html). *www.project-voldemort.com/*. Archived from [the original](http://www.project-voldemort.com/voldemort/design.html) on 9 February 2015. Retrieved 9 February 2015. Consistent hashing is a technique that avoids these problems, and we use it to compute the location of each key on the cluster.
22. [↑](./Consistent_hashing#cite_ref-akka-routing_22-0) ["Akka Routing"](http://doc.akka.io/docs/akka/snapshot/scala/routing.html). *akka.io*. Retrieved 2019-11-16.
23. [↑](./Consistent_hashing#cite_ref-riak-consistent-hashing_23-0) ["Riak Concepts"](https://web.archive.org/web/20150919042730/http://docs.basho.com/riak/1.4.8/theory/why-riak/). Archived from [the original](http://docs.basho.com/riak/1.4.8/theory/why-riak/) on 2015-09-19. Retrieved 2016-12-06.
24. [↑](./Consistent_hashing#cite_ref-GlusterFS_Algorithms:_Distribution_24-0) ["GlusterFS Algorithms: Distribution"](http://www.gluster.org/2012/03/glusterfs-algorithms-distribution/). *gluster.org*. 2012-03-01. Retrieved 2019-11-16.
25. [↑](./Consistent_hashing#cite_ref-25) Roughgarden, Tim; Valiant, Gregory (2016-03-28). ["Modern Algorithmic Toolbox"](http://theory.stanford.edu/~tim/s16/l/l1.pdf) (PDF). *stanford.edu*. Retrieved 2019-11-17.
26. [↑](./Consistent_hashing#cite_ref-how_discord_scaled_elixir_to_5,000,000_concurrent_users_26-0) Vishnevskiy, Stanislav (2017-07-06). ["How Discord Scaled Elixir to 5,000,000 Concurrent Users"](https://discord.com/blog/how-discord-scaled-elixir-to-5-000-000-concurrent-users). Retrieved 2022-08-16.
27. [↑](./Consistent_hashing#cite_ref-consistent_hash_load_balancing_for_gRPC_27-0) ["Consistent Hash Load Balancing for gRPC"](https://authzed.com/blog/consistent-hash-load-balancing-grpc). 24 November 2021. Retrieved 2023-09-04.
28. [↑](./Consistent_hashing#cite_ref-ChordTON2003_28-0)  [Stoica, I.](./Ion_Stoica); Morris, R.; Liben-Nowell, D.; Karger, D.; Kaashoek, M. F.; Dabek, F.; [Balakrishnan, H.](./Hari_Balakrishnan) (25 Feb 2003). "Chord: a scalable peer-to-peer lookup protocol for Internet applications". *IEEE/ACM Transactions on Networking*. **11** (1): 17–32. [doi](./Doi_(identifier)):[10.1109/TNET.2002.808407](https://doi.org/10.1109%2FTNET.2002.808407). [S2CID](./S2CID_(identifier)) [221276912](https://api.semanticscholar.org/CorpusID:221276912). 
29. [↑](./Consistent_hashing#cite_ref-MinIO_Versioning,_Metadata_and_Storage_Deep_Dive_29-0) ["MinIO Versioning, Metadata and Storage Deep Dive"](https://blog.min.io/minio-versioning-metadata-deep-dive). 3 January 2022. Retrieved 2023-10-24.

 

### Works cited

 
- Moitra, Ankur (10 February 2016). ["Advanced Algorithms, 6.854"](https://people.csail.mit.edu/moitra/docs/6854lec3.pdf) (PDF). [Massachusetts Institute of Technology](./Massachusetts_Institute_of_Technology). [Archived](https://web.archive.org/web/20210413045612/http://people.csail.mit.edu/moitra/docs/6854lec3.pdf) (PDF) from the original on 13 April 2021. Retrieved 8 October 2021.
- Roughgarden, Tim; Valiant, Gregory (28 March 2021). ["The Modern Algorithmic Toolbox, Introduction to Consistent Hashing"](https://web.stanford.edu/class/cs168/l/l1.pdf) (PDF). [Stanford University](./Stanford_University). [Archived](https://web.archive.org/web/20210725194111/https://web.stanford.edu/class/cs168/l/l1.pdf) (PDF) from the original on 25 July 2021. Retrieved 7 October 2021.

 

## External links

 
- [Understanding Consistent hashing](https://web.archive.org/web/20110721203235/http://www.tomkleinpeter.com/2008/03/17/programmers-toolbox-part-3-consistent-hashing/)
- [Consistent hashing by Michael Nielsen on June 3, 2009](http://michaelnielsen.org/blog/consistent-hashing)
- [Consistent Hashing, Danny Lewin, and the Creation of Akamai](https://www.youtube.com/watch?v=apHAqUG3Pi8)
- [Jump Consistent Hashing: A Fast, Minimal Memory, Consistent Hash Algorithm](https://arxiv.org/abs/1406.2294)
- [Rendezvous Hashing: an alternative to Consistent Hashing](https://medium.com/i0exception/rendezvous-hashing-8c00e2fb58b0)
- Implementations in various languages:

- [C](https://github.com/chrismoos/hash-ring)
- [C++](https://web.archive.org/web/20210414205133/http://www.martinbroadhurst.com/consistent-hash-ring.html)
- [C#](https://code.google.com/p/consistent-hash/)
- [Erlang](https://web.archive.org/web/20110711100426/https://github.com/basho/riak_core/blob/master/src/chash.erl)
- [Go](https://github.com/stathat/consistent)
- [Java](https://web.archive.org/web/20120605030524/http://weblogs.java.net/blog/tomwhite/archive/2007/11/consistent_hash.html)
- [PHP](https://github.com/pda/flexihash)
- [Ruby](https://github.com/afirel/consistent_hashr)
- [Python](http://techspot.zzzeek.org/2012/07/07/the-absolutely-simplest-consistent-hashing-example/)
- [Python (again)](http://michaelnielsen.org/blog/consistent-hashing/)
- [Perl](https://metacpan.org/pod/Set::ConsistentHash)
- [Perl6](https://github.com/bradclawsie/Hash-Consistent)

 

 Interwikies 

  Categories