---
source: https://en.wikipedia.org/wiki/Rendezvous_hashing
fetched: 2026-06-19
---

Algorithm [![](//upload.wikimedia.org/wikipedia/en/thumb/d/d1/Rendezvous_Hash_Schematic.png/250px-Rendezvous_Hash_Schematic.png)](./File:Rendezvous_Hash_Schematic.png)Rendezvous Hashing with *n=12, k=4.* Clients *C1* and *C4* independently pick the same random subset of four sites *{S2, S5, S6, S10}* from among the twelve options *S1, S2, ..., S12,* for placing replicas or shares of object *O.* 

**Rendezvous **or **highest random weight (HRW) hashing**[[1]](./Rendezvous_hashing#cite_note-:0-1)[[2]](./Rendezvous_hashing#cite_note-:1-2) is an algorithm that allows clients to achieve distributed agreement on a set of     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40) options out of a possible set of     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) options. A typical application is when clients need to agree on which sites (or proxies) objects are assigned to.

 

[Consistent hashing](./Consistent_hashing) addresses the special case      k = 1   {\displaystyle k=1}  ![{\displaystyle k=1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6c035ffa69b5bca8bf2d16c3da3aaad79a8bcbfa) using a different method. Rendezvous hashing is both much simpler and more general than consistent hashing (see below).

 

## History

 

Rendezvous hashing was invented  by David Thaler and Chinya Ravishankar at the [University of Michigan](./University_of_Michigan) in 1996.[[1]](./Rendezvous_hashing#cite_note-:0-1) [Consistent hashing](./Consistent_hashing) appeared a year later in the literature.

 

Given its simplicity and generality, rendezvous hashing is now being preferred to consistent hashing in real-world applications.[[3]](./Rendezvous_hashing#cite_note-3)[[4]](./Rendezvous_hashing#cite_note-4)[[5]](./Rendezvous_hashing#cite_note-5)  Rendezvous hashing was used very early on in many applications including mobile caching,[[6]](./Rendezvous_hashing#cite_note-6) router design,[[7]](./Rendezvous_hashing#cite_note-7) secure [key establishment](./Key_establishment),[[8]](./Rendezvous_hashing#cite_note-foisting-8) and [sharding](./Shard_(database_architecture)) and [distributed databases](./Distributed_database).[[9]](./Rendezvous_hashing#cite_note-:5-9) Other examples of real-world systems that use Rendezvous Hashing include the GitHub load balancer,[[10]](./Rendezvous_hashing#cite_note-:2-10) the [Apache Ignite](./Apache_Ignite) distributed database,[[11]](./Rendezvous_hashing#cite_note-:3-11) the Tahoe-LAFS file store,[[12]](./Rendezvous_hashing#cite_note-:6-12) the CoBlitz large-file distribution service,[[13]](./Rendezvous_hashing#cite_note-:7-13) Apache Druid,[[14]](./Rendezvous_hashing#cite_note-:8-14) IBM's Cloud Object Store,[[15]](./Rendezvous_hashing#cite_note-:9-15) the Arvados Data Management System,[[16]](./Rendezvous_hashing#cite_note-:10-16) Apache Kafka,[[17]](./Rendezvous_hashing#cite_note-:11-17) and the Twitter EventBus pub/sub platform.[[18]](./Rendezvous_hashing#cite_note-:4-18)

 

One of the first applications of rendezvous hashing was to enable [multicast](./Multicast) clients on the Internet (in contexts such as the [MBONE](./MBONE)) to identify multicast rendezvous points in a distributed fashion.[[19]](./Rendezvous_hashing#cite_note-19)[[20]](./Rendezvous_hashing#cite_note-20) It was used in 1998 by Microsoft's [Cache Array Routing Protocol](./Cache_Array_Routing_Protocol) (CARP) for distributed cache coordination and routing.[[21]](./Rendezvous_hashing#cite_note-carp-21)[[22]](./Rendezvous_hashing#cite_note-22) Some [Protocol Independent Multicast](./Protocol_Independent_Multicast) routing protocols use rendezvous hashing to pick a rendezvous point.[[1]](./Rendezvous_hashing#cite_note-:0-1)

 

## Problem definition and approach

 

### Algorithm

 

Rendezvous hashing solves a general version of the [distributed hash table](./Distributed_hash_table) problem: We are given a set of     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) sites (servers or proxies, say). How can any set of clients, given an object     O   {\displaystyle O}  ![{\displaystyle O}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d70e1d0d87e2ef1092ea1ffe2923d9933ff18fc), agree on a *k-*subset of sites to assign to     O   {\displaystyle O}  ![{\displaystyle O}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d70e1d0d87e2ef1092ea1ffe2923d9933ff18fc)? The standard version of the problem uses *k = 1.* Each client is to make its selection independently, but all clients must end up picking the same subset of sites. This is non-trivial if we add a *minimal disruption* constraint, and require that when a site fails or is removed, only objects mapping to that site need be reassigned to other sites.

 

The basic idea is to give each site      S  j     {\displaystyle S_{j}}  ![{\displaystyle S_{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/222db49df2eefdb67737ba2d2dbd221a1bae0bf0) a score (a *weight*) for each object      O  i     {\displaystyle O_{i}}  ![{\displaystyle O_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/907f89d54862168ae54a66e6835115df7587954f), and assign the object to the highest scoring site. All clients first agree on a hash function     h ( ⋅ ⋅  )   {\displaystyle h(\cdot )}  ![{\displaystyle h(\cdot )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3a4e42ce33810cdad2ae2f1f5695206f73000a34). For object      O  i     {\displaystyle O_{i}}  ![{\displaystyle O_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/907f89d54862168ae54a66e6835115df7587954f), the site      S  j     {\displaystyle S_{j}}  ![{\displaystyle S_{j}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/222db49df2eefdb67737ba2d2dbd221a1bae0bf0) is defined to have weight      w  i , j   = h (  O  i   ,  S  j   )   {\displaystyle w_{i,j}=h(O_{i},S_{j})}  ![{\displaystyle w_{i,j}=h(O_{i},S_{j})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/bd0f1838186dcfbeb9d43a0d384ec21b9bbe81d7). Each client independently computes these weights      w  i , 1   ,  w  i , 2   … …   w  i , n     {\displaystyle w_{i,1},w_{i,2}\dots w_{i,n}}  ![{\displaystyle w_{i,1},w_{i,2}\dots w_{i,n}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/de150f1f7ed4beabcca3d5349f084ac925bf249d) and picks the *k* sites that yield the *k* largest hash values. The clients have thereby achieved distributed     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40)-agreement.

 

If a site     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) is added or removed, only the objects mapping to     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) are remapped to different sites, satisfying the minimal disruption constraint above. The HRW assignment can be computed independently by any client, since it depends only on the identifiers for the set of sites      S  1   ,  S  2   … …   S  n     {\displaystyle S_{1},S_{2}\dots S_{n}}  ![{\displaystyle S_{1},S_{2}\dots S_{n}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3239a81e86f12ba9f4b3cc40d3cdab6a3c9e7891) and the object being assigned.

 

HRW easily accommodates different capacities among sites. If site      S  k     {\displaystyle S_{k}}  ![{\displaystyle S_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fd1325d812cf88e5341ac097d8bda175723da887) has twice the capacity of the other sites, we simply represent      S  k     {\displaystyle S_{k}}  ![{\displaystyle S_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fd1325d812cf88e5341ac097d8bda175723da887) twice in the list, say, as      S  k , 1   ,  S  k , 2     {\displaystyle S_{k,1},S_{k,2}}  ![{\displaystyle S_{k,1},S_{k,2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8fd79f7ee4315c8979dbe0977bdd3e0bbc777050). Clearly, twice as many objects will now map to      S  k     {\displaystyle S_{k}}  ![{\displaystyle S_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fd1325d812cf88e5341ac097d8bda175723da887) as to the other sites.

 

### Properties

 

Consider the simple version of the problem, with *k = 1,* where all clients are to agree on a single site for an object *O.* Approaching the problem naively, it might appear sufficient to treat the *n* sites as buckets in a [hash table](./Hash_table) and hash the object name *O* into this table. Unfortunately, if any of the sites fails or is unreachable, the hash table size changes, forcing all objects to be remapped. This massive disruption makes such direct hashing unworkable.

 

Under rendezvous hashing, however, clients handle site failures by picking the site that yields the next largest weight. Remapping is required only for objects currently mapped to the failed site, and disruption is minimal.[[1]](./Rendezvous_hashing#cite_note-:0-1)[[2]](./Rendezvous_hashing#cite_note-:1-2)

 

Rendezvous hashing has the following properties:

 
1. **Low overhead:** The hash function used is efficient, so overhead at the clients is very low.
2. **[Load balancing](./Load_balancing_(computing)):** Since the hash function is randomizing, each of the *n *sites is equally likely to receive the object *O*. Loads are uniform across the sites.

1. **Site capacity:** Sites with different capacities can be represented in the site list with multiplicity in proportion to capacity. A site with twice the capacity of the other sites will be represented twice in the list, while every other site is represented once.

3. **High [hit rate](./Hit_rate):** Since all clients agree on placing an object *O* into the same site *SO*, each fetch or placement of *O* into *SO* yields the maximum utility in terms of hit rate. The object *O* will always be found unless it is evicted by some replacement algorithm at *SO*.
4. **Minimal disruption:** When a site fails, only the objects mapped to that site need to be remapped. Disruption is at the minimal possible level.[[1]](./Rendezvous_hashing#cite_note-:0-1)[[2]](./Rendezvous_hashing#cite_note-:1-2)
5. **Distributed *k*-agreement:** Clients can reach distributed agreement on *k* sites simply by selecting the top *k* sites in the ordering.[[8]](./Rendezvous_hashing#cite_note-foisting-8)

 

## *O*(log *n*) running time via skeleton-based hierarchical rendezvous hashing

 

The standard version of Rendezvous Hashing described above works quite well for moderate *n,* but when     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) is extremely large, the hierarchical use of Rendezvous Hashing achieves     O ( log ⁡ ⁡  n )   {\displaystyle O(\log n)}  ![{\displaystyle O(\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/aae0f22048ba6b7c05dbae17b056bfa16e21807d) running time.[[23]](./Rendezvous_hashing#cite_note-CSE_Technical_Report_UCR-CS_2001-05062-23)[[24]](./Rendezvous_hashing#cite_note-24)[[25]](./Rendezvous_hashing#cite_note-25) This approach creates a virtual hierarchical structure (called a "skeleton"), and achieves     O ( log ⁡ ⁡  n )   {\displaystyle O(\log n)}  ![{\displaystyle O(\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/aae0f22048ba6b7c05dbae17b056bfa16e21807d) running time by applying HRW at each level while descending the hierarchy. The idea is to first choose some constant     m   {\displaystyle m}  ![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc) and organize the     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) sites into     c = ⌈ ⌈  n  /  m ⌉ ⌉    {\displaystyle c=\lceil n/m\rceil }  ![{\displaystyle c=\lceil n/m\rceil }](https://wikimedia.org/api/rest_v1/media/math/render/svg/05045a6cebf5f6c2bfceb9161765ecae4eca548a) clusters      C  1   =  {   S  1   ,  S  2   … …   S  m    }  ,  C  2   =  {   S  m + 1   ,  S  m + 2   … …   S  2 m    }  … …    {\displaystyle C_{1}=\left\{S_{1},S_{2}\dots S_{m}\right\},C_{2}=\left\{S_{m+1},S_{m+2}\dots S_{2m}\right\}\dots }  ![{\displaystyle C_{1}=\left\{S_{1},S_{2}\dots S_{m}\right\},C_{2}=\left\{S_{m+1},S_{m+2}\dots S_{2m}\right\}\dots }](https://wikimedia.org/api/rest_v1/media/math/render/svg/608c077cc676eecd1c6d96f74828d310059d732a) Next, build a virtual hierarchy by choosing a constant     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) and imagining these     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455) clusters placed at the leaves of a tree     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) of virtual nodes, each with fanout     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61).

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/b/b1/Rendezvous_Hashing_skeleton%2C_animated.gif/250px-Rendezvous_Hashing_skeleton%2C_animated.gif)](./File:Rendezvous_Hashing_skeleton,_animated.gif)Using a skeleton to achieve *log(n)* execution time. The real nodes appear as squares at the leaf level. The virtual nodes of the skeleton appear as dotted circles. The leaf-level clusters are of size  *m = 4,* and the skeleton has fanout *f = 3.* 

In the accompanying diagram, the cluster size is     m = 4   {\displaystyle m=4}  ![{\displaystyle m=4}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0002ab187a5f0920f4c5eff6741f9964cbe2abfd), and the skeleton fanout is     f = 3   {\displaystyle f=3}  ![{\displaystyle f=3}](https://wikimedia.org/api/rest_v1/media/math/render/svg/258e6924646c4f1f5cb0a6f3b1c9092acbe78d2a). Assuming 108 sites (real nodes) for convenience, we get a three-tier virtual hierarchy. Since     f = 3   {\displaystyle f=3}  ![{\displaystyle f=3}](https://wikimedia.org/api/rest_v1/media/math/render/svg/258e6924646c4f1f5cb0a6f3b1c9092acbe78d2a), each virtual node has a natural numbering in octal. Thus, the 27 virtual nodes at the lowest tier would be numbered     000 , 001 , 002 , . . . , 221 , 222   {\displaystyle 000,001,002,...,221,222}  ![{\displaystyle 000,001,002,...,221,222}](https://wikimedia.org/api/rest_v1/media/math/render/svg/45eeed5b63f9f43c027e1aacb13f896699d99848) in octal (we can, of course, vary the fanout at each level - in that case, each node will be identified with the corresponding mixed-radix number).

 

The easiest way to understand the virtual hierarchy is by starting at the top, and descending the virtual hierarchy. We successively apply Rendezvous Hashing to the set of virtual nodes at each level of the hierarchy, and descend the branch defined by the winning virtual node. We can in fact start at any level in the virtual hierarchy. Starting lower in the hierarchy requires more hashes, but may improve load distribution in the case of failures.

 

For example, instead of applying HRW to all 108 real nodes in the diagram, we can first apply HRW to the 27 lowest-tier virtual nodes, selecting one. We then apply HRW to the four real nodes in its cluster, and choose the winning site. We only need     27 + 4 = 31   {\displaystyle 27+4=31}  ![{\displaystyle 27+4=31}](https://wikimedia.org/api/rest_v1/media/math/render/svg/92c690f8e556f80e1ed631aa81d79fdb8aa1adde) hashes, rather than 108. If we apply this method starting one level higher in the hierarchy, we would need     9 + 3 + 4 = 16   {\displaystyle 9+3+4=16}  ![{\displaystyle 9+3+4=16}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f22fa964e0117164edbe4d9076b8225a8e7013f2) hashes to get to the winning site. The figure shows how, if we proceed starting from the root of the skeleton, we may successively choose the virtual nodes     ( 2  )  3     {\displaystyle (2)_{3}}  ![{\displaystyle (2)_{3}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/43ca19c44ba6948ed95137287feac42e655fda51),     ( 20  )  3     {\displaystyle (20)_{3}}  ![{\displaystyle (20)_{3}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2ca6095534c22afd45794e57c05f4dd1db048558), and     ( 200  )  3     {\displaystyle (200)_{3}}  ![{\displaystyle (200)_{3}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/66aa43894b728bcb14a1cb76e38e406bd66643a5), and finally end up with site 74.

 

The virtual hierarchy need not be stored, but can be created on demand, since the virtual nodes names are simply prefixes of base-    f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) (or mixed-radix) representations. We can easily create appropriately sorted strings from the digits, as required. In the example, we would be working with the strings     0 , 1 , 2   {\displaystyle 0,1,2}  ![{\displaystyle 0,1,2}](https://wikimedia.org/api/rest_v1/media/math/render/svg/6a61d4d16c56c710fac0eee20d1a12f4097e46fd) (at tier 1),     20 , 21 , 22   {\displaystyle 20,21,22}  ![{\displaystyle 20,21,22}](https://wikimedia.org/api/rest_v1/media/math/render/svg/958123935cb10406b3818c6254c40b5fc0365d5c) (at tier 2), and     200 , 201 , 202   {\displaystyle 200,201,202}  ![{\displaystyle 200,201,202}](https://wikimedia.org/api/rest_v1/media/math/render/svg/496de1ebfc80bb737ddaeaff530aa90cb26c3e75) (at tier 3). Clearly,     T   {\displaystyle T}  ![{\displaystyle T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0) has height     h = O ( log ⁡ ⁡  c ) = O ( log ⁡ ⁡  n )   {\displaystyle h=O(\log c)=O(\log n)}  ![{\displaystyle h=O(\log c)=O(\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/750dd2e520e7f374bdeec8b2cec326f2498850f0), since     m   {\displaystyle m}  ![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc) and     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) are both constants. The work done at each level is     O ( 1 )   {\displaystyle O(1)}  ![{\displaystyle O(1)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21), since     f   {\displaystyle f}  ![{\displaystyle f}](https://wikimedia.org/api/rest_v1/media/math/render/svg/132e57acb643253e7810ee9702d9581f159a1c61) is a constant.

 

The value of     m   {\displaystyle m}  ![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc) can be chosen based on factors like the anticipated failure rate and the degree of desired load balancing. A higher value of     m   {\displaystyle m}  ![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc) leads to less load skew in the event of failure at the cost of higher search overhead.

 

The choice     m = n   {\displaystyle m=n}  ![{\displaystyle m=n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/69c9d8e54796e7de7d4738510cc10bc3fc55d48e) is equivalent to non-hierarchical rendezvous hashing. In practice, the hash function     h ( ⋅ ⋅  )   {\displaystyle h(\cdot )}  ![{\displaystyle h(\cdot )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3a4e42ce33810cdad2ae2f1f5695206f73000a34) is very cheap, so     m = n   {\displaystyle m=n}  ![{\displaystyle m=n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/69c9d8e54796e7de7d4738510cc10bc3fc55d48e) can work quite well unless     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) is very high.

 

For any given object, it is clear that each leaf-level cluster, and hence each of the     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) sites, is chosen with equal probability.

 

### Replication, site failures, and site additions

 

One can enhance resiliency to failures by replicating each object *O* across the highest ranking *r < m* sites for *O,* choosing *r* based on the level of resiliency desired. The simplest strategy is to replicate only within the leaf-level cluster.

 

If the leaf-level site selected for *O* is unavailable, we select the next-ranked site for *O* within the same leaf-level cluster. If *O* has been replicated within the leaf-level cluster, we are sure to find *O* in the next available site in the ranked order of *r* sites. All objects that were held by the failed server appear in some other site in its cluster. (Another option is to go up one or more tiers in the skeleton and select an alternate from among the sibling virtual nodes at that tier. We then descend the hierarchy to the real nodes, as above.)

 

When a site is added to the system, it may become the winning site for some objects already assigned to other sites. Objects mapped to other clusters will never map to this new site, so we need to only consider objects held by other sites in its cluster. If the sites are caches, attempting to access an object mapped to the new site will result in a cache miss, the corresponding object will be fetched and cached, and operation returns to normal.

 

If sites are servers, some objects must be remapped to this newly added site.  As before, objects mapped to other clusters will never map to this new site, so we need to only consider objects held by sites in its cluster. That is, we need only remap objects currently present in the *m* sites in this local cluster, rather than the entire set of objects in the system. New objects mapping to this site will of course be automatically assigned to it.

 

## Comparison with consistent hashing

 

Because of its simplicity, lower overhead, and generality (it works for any *k < n*), rendezvous hashing is increasingly being preferred over consistent hashing. Recent examples of its use include the GitHub load balancer,[[10]](./Rendezvous_hashing#cite_note-:2-10) the Apache Ignite distributed database,[[11]](./Rendezvous_hashing#cite_note-:3-11) and by the Twitter EventBus pub/sub platform.[[18]](./Rendezvous_hashing#cite_note-:4-18)

 

Consistent hashing operates by mapping each site uniformly and randomly to multiple points on a unit circle called tokens. Objects are also mapped to the unit circle and placed in the site owning the token that is first encountered traveling clockwise from the object's location. When a site is removed, each of its objects is transferred to the site owning the next token encountered moving clockwise. Provided each site is mapped to a large number of tokens (100–200, say), this will reassign objects in a relatively uniform fashion among the remaining sites.

 

If a site's tokens are placed on the unit circle by hashing 200 variants of the site ID, say, then the assignment of any object requires storing or recalculating 200 hash values for each site. However, the tokens associated with a given site can be precomputed and stored in a sorted list, requiring only a single application of the hash function to the object, and a binary search to compute the assignment. Even with many tokens per site, however, the basic version of consistent hashing may not balance objects uniformly over sites, since when a site is removed each object assigned to it is distributed only over as many other sites as the site has tokens (say 100–200).

 

Variants of consistent hashing (such as Amazon's [Dynamo](./Dynamo_(storage_system))) that use more complex logic to distribute tokens on the unit circle offer better [load balancing](./Load_balancing_(computing)) than basic consistent hashing, reduce the overhead of adding new sites, and reduce metadata overhead and offer other benefits.[[26]](./Rendezvous_hashing#cite_note-Amazon2007-26)

 

### Advantages of Rendezvous hashing over consistent hashing

 

Rendezvous hashing (HRW) is much simpler conceptually and in practice. It also distributes objects uniformly over all sites, given a uniform hash function. Unlike consistent hashing, HRW requires no precomputing or storage of tokens. Consider *k =1.* An object      O  i     {\displaystyle O_{i}}  ![{\displaystyle O_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/907f89d54862168ae54a66e6835115df7587954f) is placed into one of     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) sites      S  1   ,  S  2   … …   S  n     {\displaystyle S_{1},S_{2}\dots S_{n}}  ![{\displaystyle S_{1},S_{2}\dots S_{n}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3239a81e86f12ba9f4b3cc40d3cdab6a3c9e7891) by computing the     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) hash values     h (  O  i   ,  S  j   )   {\displaystyle h(O_{i},S_{j})}  ![{\displaystyle h(O_{i},S_{j})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/01600cad6572db81ceeddfd1b26aa9f1541c7851) and picking the site      S  k     {\displaystyle S_{k}}  ![{\displaystyle S_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fd1325d812cf88e5341ac097d8bda175723da887) that yields the highest hash value. If a new site      S  n + 1     {\displaystyle S_{n+1}}  ![{\displaystyle S_{n+1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f8b0ac107028f431bb7698eeab7c508d3fe1a976) is added, new object placements or requests will compute     n + 1   {\displaystyle n+1}  ![{\displaystyle n+1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2a135e65a42f2d73cccbfc4569523996ca0036f1) hash values, and pick the largest of these. If an object already in the system at      S  k     {\displaystyle S_{k}}  ![{\displaystyle S_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fd1325d812cf88e5341ac097d8bda175723da887) maps to this new site      S  n + 1     {\displaystyle S_{n+1}}  ![{\displaystyle S_{n+1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f8b0ac107028f431bb7698eeab7c508d3fe1a976), it will be fetched afresh and cached at      S  n + 1     {\displaystyle S_{n+1}}  ![{\displaystyle S_{n+1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f8b0ac107028f431bb7698eeab7c508d3fe1a976). All clients will henceforth obtain it from this site, and the old cached copy at      S  k     {\displaystyle S_{k}}  ![{\displaystyle S_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fd1325d812cf88e5341ac097d8bda175723da887) will ultimately be replaced by the local cache management algorithm. If      S  k     {\displaystyle S_{k}}  ![{\displaystyle S_{k}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fd1325d812cf88e5341ac097d8bda175723da887) is taken offline, its objects will be remapped uniformly to the remaining     n − −  1   {\displaystyle n-1}  ![{\displaystyle n-1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fbd0b0f32b28f51962943ee9ede4fb34198a2521) sites.

 

Variants of the HRW algorithm, such as the use of a skeleton (see below), can reduce the     O ( n )   {\displaystyle O(n)}  ![{\displaystyle O(n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a) time for object location to     O ( log ⁡ ⁡  n )   {\displaystyle O(\log n)}  ![{\displaystyle O(\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/aae0f22048ba6b7c05dbae17b056bfa16e21807d), at the cost of less global uniformity of placement. When     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) is not too large, however, the     O ( n )   {\displaystyle O(n)}  ![{\displaystyle O(n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a) placement cost of basic HRW is not likely to be a problem. HRW completely avoids all the overhead and complexity associated with correctly handling multiple tokens for each site and associated metadata.

 

Rendezvous hashing also has the great advantage that it provides simple solutions to other important problems, such as distributed     k   {\displaystyle k}  ![{\displaystyle k}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40)-agreement.

 

### Consistent hashing is a special case of Rendezvous hashing

 

Rendezvous hashing is both simpler and more general than consistent hashing. Consistent hashing can be shown to be a special case of HRW by an appropriate choice of a two-place hash function. From the site identifier     S   {\displaystyle S}  ![{\displaystyle S}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2) the simplest version of consistent hashing computes a list of token positions, e.g.,      t  s   =  h  c   ( S )   {\displaystyle t_{s}=h_{c}(S)}  ![{\displaystyle t_{s}=h_{c}(S)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/90aceb9fd2a78ab01847731bedfa46e584b66b75) where      h  c     {\displaystyle h_{c}}  ![{\displaystyle h_{c}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d06972075e10d9390c826454530d3e2a6351dc45) hashes values to locations on the unit circle. Define the two place hash function     h ( S , O )   {\displaystyle h(S,O)}  ![{\displaystyle h(S,O)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5e4e356b2a7fcc48168c0d92a5a65a8ae064e019) to be       1   min  S   (  h  c   ( O ) − −   t  s   )      {\displaystyle {\frac {1}{\min _{S}(h_{c}(O)-t_{s})}}}  ![{\displaystyle {\frac {1}{\min _{S}(h_{c}(O)-t_{s})}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2738d0b1a90f50a3238115b8c772c4ec284a5fe5) where      h  c   ( O ) − −   t  s     {\displaystyle h_{c}(O)-t_{s}}  ![{\displaystyle h_{c}(O)-t_{s}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f3def495c1f238c41ab75e59bcb023b4b3b1e0ce) denotes the distance along the unit circle from      h  c   ( O )   {\displaystyle h_{c}(O)}  ![{\displaystyle h_{c}(O)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/859fb7772a23c0f239d1fe74e187d58d4a5dbc0f) to      t  s     {\displaystyle t_{s}}  ![{\displaystyle t_{s}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ddf19ec057a1467dc4b6c7452aaa9a35bb099fea) (since      h  c   ( O ) − −   t  s     {\displaystyle h_{c}(O)-t_{s}}  ![{\displaystyle h_{c}(O)-t_{s}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/f3def495c1f238c41ab75e59bcb023b4b3b1e0ce) has some minimal non-zero value there is no problem translating this value to a unique integer in some bounded range). This will duplicate exactly the assignment produced by consistent hashing.

 

It is not possible, however, to [reduce](./Reduction_(complexity)) HRW to consistent hashing (assuming the number of tokens per site is bounded), since HRW potentially reassigns the objects from a removed site to an unbounded number of other sites.

 

## Weighted variations

 

In the standard implementation of rendezvous hashing, every node receives a statically equal proportion of the keys. This behavior, however, is undesirable when the nodes have different capacities for processing or holding their assigned keys. For example, if one of the nodes had twice the storage capacity as the others, it would be beneficial if the algorithm could take this into account such that this more powerful node would receive twice the number of keys as each of the others.

 

A straightforward mechanism to handle this case is to assign two virtual locations to this node, so that if either of that larger node's virtual locations has the highest hash, that node receives the key. But this strategy does not work when the relative weights are not integer multiples. For example, if one node had 42% more storage capacity, it would require adding many virtual nodes in different proportions, leading to greatly reduced performance. Several modifications to rendezvous hashing have been proposed to overcome this limitation.

 

### Cache Array Routing Protocol

 

The [Cache Array Routing Protocol](./Cache_Array_Routing_Protocol) (CARP) is a 1998 IETF draft that describes a method for computing *load factors* which can be multiplied by each node's hash score to yield an arbitrary level of precision for weighting nodes differently.[[21]](./Rendezvous_hashing#cite_note-carp-21) However, one disadvantage of this approach is that when any node's weight is changed, or when any node is added or removed, all the load factors must be re-computed and relatively scaled. When the load factors change relative to one another, it triggers movement of keys between nodes whose weight was not changed, but whose load factor did change relative to other nodes in the system. This results in excess movement of keys.[[27]](./Rendezvous_hashing#cite_note-wrh-27)

 

### Controlled replication

 

Controlled replication under scalable hashing or CRUSH[[28]](./Rendezvous_hashing#cite_note-crush-28) is an extension to RUSH[[29]](./Rendezvous_hashing#cite_note-rush-29) that improves upon rendezvous hashing by constructing a tree where a pseudo-random function (hash) is used to navigate down the tree to find which node is ultimately responsible for a given key. It permits perfect stability for adding nodes; however, it is not perfectly stable when removing or re-weighting nodes, with the excess movement of keys being proportional to the height of the tree.

 

The CRUSH algorithm is used by the [ceph](./Ceph_(software)) data storage system to map data objects to the nodes responsible for storing them.[[30]](./Rendezvous_hashing#cite_note-30)

 

### Other variants

 

In 2005, Christian Schindelhauer and Gunnar Schomaker described a logarithmic method for re-weighting hash scores in a way that does not require relative scaling of load factors when a node's weight changes or when nodes are added or removed.[[31]](./Rendezvous_hashing#cite_note-31) This enabled the dual benefits of perfect precision when weighting nodes, along with perfect stability, as only a minimum number of keys needed to be remapped to new nodes.

 

A similar logarithm-based hashing strategy is used to assign data to storage nodes in [Cleversafe](./Cleversafe_Inc.)'s data storage system, now [IBM Cloud Object Storage](./IBM_Cloud_Object_Storage).[[27]](./Rendezvous_hashing#cite_note-wrh-27)

 

## Systems using Rendezvous hashing

 

Rendezvous hashing is being used widely in real-world systems. A partial list includes Oracle's Database in-memory,[[9]](./Rendezvous_hashing#cite_note-:5-9) the GitHub load balancer,[[10]](./Rendezvous_hashing#cite_note-:2-10) the Apache Ignite distributed database,[[11]](./Rendezvous_hashing#cite_note-:3-11) the Tahoe-LAFS file store,[[12]](./Rendezvous_hashing#cite_note-:6-12) the CoBlitz large-file distribution service,[[13]](./Rendezvous_hashing#cite_note-:7-13) Apache Druid,[[14]](./Rendezvous_hashing#cite_note-:8-14) IBM's Cloud Object Store,[[15]](./Rendezvous_hashing#cite_note-:9-15) the Arvados Data Management System,[[16]](./Rendezvous_hashing#cite_note-:10-16) Apache Kafka,[[17]](./Rendezvous_hashing#cite_note-:11-17) and by the Twitter EventBus pub/sub platform.[[18]](./Rendezvous_hashing#cite_note-:4-18)

 

## Implementation

 

Implementation is straightforward once a [hash function](./Hash_function)     h ( ⋅ ⋅  )   {\displaystyle h(\cdot )}  ![{\displaystyle h(\cdot )}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3a4e42ce33810cdad2ae2f1f5695206f73000a34) is chosen (the original work on the HRW method makes a hash function recommendation).[[1]](./Rendezvous_hashing#cite_note-:0-1)[[2]](./Rendezvous_hashing#cite_note-:1-2) Each client only needs to compute a hash value for each of the     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) sites, and then pick the largest. This algorithm runs in     O ( n )   {\displaystyle O(n)}  ![{\displaystyle O(n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a) time. If the hash function is efficient, the     O ( n )   {\displaystyle O(n)}  ![{\displaystyle O(n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a) running time is not a problem unless     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) is very large. A logarithmic transformation of the uniform score (unit interval) is applied, when multiplied by the node weights the probability of a node winning is proportional to its weight relative to the total weight of all nodes. Note the magnitude of the scores vary greatly but the probabilities remain constant.

 

### Weighted rendezvous hash

 

Python code implementing a weighted rendezvous hash:[[27]](./Rendezvous_hashing#cite_note-wrh-27)

 
```
import mmh3
import math
from dataclasses import dataclass

def hash_to_unit_interval(s: str) -> float:
    """Hashes a string onto the unit interval (0, 1]"""
    return (mmh3.hash128(s) + 1) / 2**128

@dataclass
class Node:
    """Class representing a node that is assigned keys as part of a weighted rendezvous hash."""
    name: str
    weight: float

    def compute_weighted_score(self, key: str) -> float:
        score: float = hash_to_unit_interval(f"{self.name}: {key}")
        log_score: float = 1.0 / -math.log(score)
        return self.weight * log_score

def determine_responsible_node(nodes: list[Node], key: str) -> Node:
    """Determines which node of a set of nodes of various weights is responsible for the provided key."""
    return max(nodes, key=lambda node: node.compute_weighted_score(key), default=None)

```
 

Example outputs of WRH:

 
```
import wrh
from collections import Counter
from wrh import Node

node1: Node = Node("node1", 100)
node2: Node = Node("node2", 200)
node3: Node = Node("node3", 300)
print(str(wrh.determine_responsible_node([node1, node2, node3], "foo")))
# prints: "Node(name='node1', weight=100)"
print(str(wrh.determine_responsible_node([node1, node2, node3], "bar")))
# prints: "Node(name='node2', weight=300)"
print(str(wrh.determine_responsible_node([node1, node2, node3], "hello")))
# prints: "Node(name='node2', weight=300)"
nodes: list[Node] = [node1, node2, node3]
responsible_nodes: list[Node] = [wrh.determine_responsible_node(
    nodes, f"key: {key}").name for key in range(45_000)]
print(Counter(responsible_nodes))
# prints: Counter({'node3': 22487, 'node2': 15020, 'node1': 7493})

```
 

## References

  
1. [1](./Rendezvous_hashing#cite_ref-:0_1-0) [2](./Rendezvous_hashing#cite_ref-:0_1-1) [3](./Rendezvous_hashing#cite_ref-:0_1-2) [4](./Rendezvous_hashing#cite_ref-:0_1-3) [5](./Rendezvous_hashing#cite_ref-:0_1-4) [6](./Rendezvous_hashing#cite_ref-:0_1-5) Thaler, David; Chinya Ravishankar. ["A Name-Based Mapping Scheme for Rendezvous"](http://www.eecs.umich.edu/techreports/cse/96/CSE-TR-316-96.pdf) (PDF). University of Michigan Technical Report CSE-TR-316-96. Retrieved 2013-09-15.
2. [1](./Rendezvous_hashing#cite_ref-:1_2-0) [2](./Rendezvous_hashing#cite_ref-:1_2-1) [3](./Rendezvous_hashing#cite_ref-:1_2-2) [4](./Rendezvous_hashing#cite_ref-:1_2-3) Thaler, David; Chinya Ravishankar (February 1998). "Using Name-Based Mapping Schemes to Increase Hit Rates". *IEEE/ACM Transactions on Networking*. **6** (1): 1–14. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.416.8943](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.416.8943). [doi](./Doi_(identifier)):[10.1109/90.663936](https://doi.org/10.1109%2F90.663936). [S2CID](./S2CID_(identifier)) [936134](https://api.semanticscholar.org/CorpusID:936134).
3. [↑](./Rendezvous_hashing#cite_ref-3) ["Rendezvous Hashing Explained - Randorithms"](https://randorithms.com/2020/12/26/rendezvous-hashing.html). *randorithms.com*. Retrieved 2021-03-29.
4. [↑](./Rendezvous_hashing#cite_ref-4) ["Rendezvous hashing: my baseline "consistent" distribution method - Paul Khuong: some Lisp"](https://pvk.ca/Blog/2017/09/24/rendezvous-hashing-my-baseline-consistent-distribution-method/). *pvk.ca*. Retrieved 2021-03-29.
5. [↑](./Rendezvous_hashing#cite_ref-5) Aniruddha (2020-01-08). ["Rendezvous Hashing"](https://medium.com/i0exception/rendezvous-hashing-8c00e2fb58b0). *Medium*. Retrieved 2021-03-29.
6. [↑](./Rendezvous_hashing#cite_ref-6) Mayank, Anup; Ravishankar, Chinya (2006). ["Supporting mobile device communications in the presence of broadcast servers"](http://www.cs.ucr.edu/~ravi/Papers/Jrnl/Mayank.pdf) (PDF). *International Journal of Sensor Networks*. **2** (1/2): 9–16. [doi](./Doi_(identifier)):[10.1504/IJSNET.2007.012977](https://doi.org/10.1504%2FIJSNET.2007.012977).
7. [↑](./Rendezvous_hashing#cite_ref-7) Guo, Danhua; Bhuyan, Laxmi; Liu, Bin (October 2012). "An efficient parallelized L7-filter design for multicore servers". *IEEE/ACM Transactions on Networking*. **20** (5): 1426–1439. [doi](./Doi_(identifier)):[10.1109/TNET.2011.2177858](https://doi.org/10.1109%2FTNET.2011.2177858). [S2CID](./S2CID_(identifier)) [1982193](https://api.semanticscholar.org/CorpusID:1982193).
8. [1](./Rendezvous_hashing#cite_ref-foisting_8-0) [2](./Rendezvous_hashing#cite_ref-foisting_8-1) Wang, Peng; Ravishankar, Chinya (2015). ["Key Foisting and Key Stealing Attacks in Sensor Networks'"](http://www.cs.ucr.edu/~ravi/Papers/Jrnl/foisting.pdf) (PDF). *International Journal of Sensor Networks*.
9. [1](./Rendezvous_hashing#cite_ref-:5_9-0) [2](./Rendezvous_hashing#cite_ref-:5_9-1) Mukherjee, Niloy; et al. (August 2015). "Distributed Architecture of Oracle Database In-memory". *Proceedings of the VLDB Endowment*. **8** (12): 1630–1641. [doi](./Doi_(identifier)):[10.14778/2824032.2824061](https://doi.org/10.14778%2F2824032.2824061).
10. [1](./Rendezvous_hashing#cite_ref-:2_10-0) [2](./Rendezvous_hashing#cite_ref-:2_10-1) [3](./Rendezvous_hashing#cite_ref-:2_10-2) GitHub Engineering (22 September 2016). ["Introducing the GitHub Load Balancer"](https://github.blog/2016-09-22-introducing-glb/). *GitHub Blog*. Retrieved 1 February 2022.
11. [1](./Rendezvous_hashing#cite_ref-:3_11-0) [2](./Rendezvous_hashing#cite_ref-:3_11-1) [3](./Rendezvous_hashing#cite_ref-:3_11-2) ["Apache Ignite"](https://en.wikipedia.org/w/index.php?title=Apache_Ignite&oldid=1105175435), *Wikipedia*, 2022-08-18, retrieved 2022-12-09
12. [1](./Rendezvous_hashing#cite_ref-:6_12-0) [2](./Rendezvous_hashing#cite_ref-:6_12-1) ["Tahoe-LAFS"](https://tahoe-lafs.org/trac/tahoe-lafs). *tahoe-lafs.org*. Retrieved 2023-01-02.
13. [1](./Rendezvous_hashing#cite_ref-:7_13-0) [2](./Rendezvous_hashing#cite_ref-:7_13-1) Park, KyoungSoo; Pai, Vivek S. (2006). "Scale and performance in the CoBlitz large-file distribution service". *Usenix Nsdi*.
14. [1](./Rendezvous_hashing#cite_ref-:8_14-0) [2](./Rendezvous_hashing#cite_ref-:8_14-1) ["Router Process · Apache Druid"](https://druid.apache.org/index.html). *druid.apache.org*. Retrieved 2023-01-02.
15. [1](./Rendezvous_hashing#cite_ref-:9_15-0) [2](./Rendezvous_hashing#cite_ref-:9_15-1) ["IBM Cloud Object Storage System, Version 3.14.11, Storage Pool Expansion Guide"](https://www.ibm.com/docs/STXNRM_3.15.3/coss.doc/pdfs/storagePoolExpansion_bookmap.pdf) (PDF). *IBM Cloud Object Storage SystemTM Version*. Retrieved January 2, 2023.
16. [1](./Rendezvous_hashing#cite_ref-:10_16-0) [2](./Rendezvous_hashing#cite_ref-:10_16-1) ["Arvados | Keep clients"](https://doc.arvados.org/v2.5/architecture/keep-clients.html). *doc.arvados.org*. Retrieved 2023-01-02.
17. [1](./Rendezvous_hashing#cite_ref-:11_17-0) [2](./Rendezvous_hashing#cite_ref-:11_17-1) ["Horizontally scaling Kafka consumers with rendezvous hashing"](https://www.tinybird.co/blog-posts/kafka-horizontal-scaling). *Tinybird.co*. Retrieved 2023-02-15.
18. [1](./Rendezvous_hashing#cite_ref-:4_18-0) [2](./Rendezvous_hashing#cite_ref-:4_18-1) [3](./Rendezvous_hashing#cite_ref-:4_18-2) Aniruddha (2020-01-08). ["Rendezvous Hashing"](https://medium.com/i0exception/rendezvous-hashing-8c00e2fb58b0). *i0exception*. Retrieved 2022-12-09.
19. [↑](./Rendezvous_hashing#cite_ref-19) Blazevic, Ljubica (21 June 2000). ["Distributed Core Multicast (DCM): a routing protocol for many small groups with application to mobile IP telephony"](http://tools.ietf.org/html/draft-blazevic-dcm-mobility-01). *IETF Draft*. IETF. Retrieved September 17, 2013.
20. [↑](./Rendezvous_hashing#cite_ref-20) Fenner, B. (August 2006). ["Protocol Independent Multicast - Sparse Mode (PIM-SM): Protocol Specification (Revised)"](http://tools.ietf.org/html/rfc4601). *IETF RFC*. IETF. Retrieved September 17, 2013.
21. [1](./Rendezvous_hashing#cite_ref-carp_21-0) [2](./Rendezvous_hashing#cite_ref-carp_21-1) Valloppillil, Vinod; Kenneth Ross (27 February 1998). ["Cache Array Routing Protocol v1.0"](http://tools.ietf.org/html/draft-vinod-carp-v1-03). Internet Draft. Retrieved September 15, 2013.
22. [↑](./Rendezvous_hashing#cite_ref-22) ["Cache Array Routing Protocol and Microsoft Proxy Server 2.0"](https://web.archive.org/web/20140918115447/http://oldsite.mcoecn.org/WhitePapers/Mscarp.pdf) (PDF). Microsoft. Archived from [the original](http://oldsite.mcoecn.org/WhitePapers/Mscarp.pdf) (PDF) on September 18, 2014. Retrieved September 15, 2013.
23. [↑](./Rendezvous_hashing#cite_ref-CSE_Technical_Report_UCR-CS_2001-05062_23-0) Yao, Zizhen; Ravishankar, Chinya; Tripathi, Satish (May 13, 2001). [*Hash-Based Virtual Hierarchies for Caching in Hybrid Content-Delivery Networks*](https://web.archive.org/web/20201116215127/http://static.cs.ucr.edu/store/techreports/UCR-CS-2001-05062.pdf) (PDF). Riverside, CA: CSE Department, University of California, Riverside. Archived from [the original](http://static.cs.ucr.edu/store/techreports/UCR-CS-2001-05062.pdf) (PDF) on 16 November 2020. Retrieved 15 November 2015.
24. [↑](./Rendezvous_hashing#cite_ref-24) Wang, Wei; Chinya Ravishankar (January 2009). "Hash-Based Virtual Hierarchies for Scalable Location Service in Mobile Ad-hoc Networks". *Mobile Networks and Applications*. **14** (5): 625–637. [doi](./Doi_(identifier)):[10.1007/s11036-008-0144-3](https://doi.org/10.1007%2Fs11036-008-0144-3). [S2CID](./S2CID_(identifier)) [2802543](https://api.semanticscholar.org/CorpusID:2802543).
25. [↑](./Rendezvous_hashing#cite_ref-25) Mayank, Anup; Phatak, Trivikram; Ravishankar, Chinya (2006), [*Decentralized Hash-Based Coordination of Distributed Multimedia Caches*](http://www.cs.ucr.edu/~ravi/Papers/NWConf/ICN2006.pdf) (PDF), Proc. 5th IEEE International Conference on Networking (ICN'06), Mauritius: IEEE
26. [↑](./Rendezvous_hashing#cite_ref-Amazon2007_26-0) DeCandia, G.; Hastorun, D.; Jampani, M.; Kakulapati, G.; Lakshman, A.; Pilchin, A.; Sivasubramanian, S.; Vosshall, P.; Vogels, W. (2007). ["Dynamo"](http://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf) (PDF). *ACM SIGOPS Operating Systems Review*. **41** (6): 205–220. [doi](./Doi_(identifier)):[10.1145/1323293.1294281](https://doi.org/10.1145%2F1323293.1294281). Retrieved 2018-06-07.
27. [1](./Rendezvous_hashing#cite_ref-wrh_27-0) [2](./Rendezvous_hashing#cite_ref-wrh_27-1) [3](./Rendezvous_hashing#cite_ref-wrh_27-2) Jason Resch. ["New Hashing Algorithms for Data Storage"](http://www.snia.org/sites/default/files/SDC15_presentations/dist_sys/Jason_Resch_New_Consistent_Hashings_Rev.pdf) (PDF).
28. [↑](./Rendezvous_hashing#cite_ref-crush_28-0) Sage A. Weil; et al. ["CRUSH: Controlled, Scalable, Decentralized Placement of Replicated Data"](https://web.archive.org/web/20190220002858/https://www.crss.ucsc.edu/media/papers/weil-sc06.pdf) (PDF). Archived from [the original](http://www.crss.ucsc.edu/media/papers/weil-sc06.pdf) (PDF) on February 20, 2019.
29. [↑](./Rendezvous_hashing#cite_ref-rush_29-0) R. J. Honicky, Ethan L. Miller. ["Replication Under Scalable Hashing: A Family of Algorithms for Scalable Decentralized Data Distribution"](https://web.archive.org/web/20170226050158/http://www.ssrc.ucsc.edu/media/papers/honicky-ipdps04.pdf) (PDF). Archived from [the original](http://www.ssrc.ucsc.edu/media/papers/honicky-ipdps04.pdf) (PDF) on 2017-02-26. Retrieved 2017-02-25.
30. [↑](./Rendezvous_hashing#cite_ref-30) Ceph. ["Crush Maps"](http://docs.ceph.com/docs/master/rados/operations/crush-map/).
31. [↑](./Rendezvous_hashing#cite_ref-31) Christian Schindelhauer, Gunnar Schomaker (2005). "Weighted Distributed Hash Tables": 218. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.414.9353](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.414.9353). `{{cite journal}}`: Cite journal requires `|journal=` ([help](./Help:CS1_errors#missing_periodical))

 

## External links

 
- [Rendezvous Hashing: an alternative to Consistent Hashing](https://medium.com/i0exception/rendezvous-hashing-8c00e2fb58b0)