---
source: https://en.wikipedia.org/wiki/Linear_hashing
fetched: 2026-06-19
---

Dynamic data structure 

**Linear hashing** (**LH**) is a dynamic [data structure](./Data_structure) which implements a [hash table](./Hash_table) and grows or shrinks one bucket at a time. It was invented by Witold Litwin in 1980.[[1]](./Linear_hashing#cite_note-WL80-1) [[2]](./Linear_hashing#cite_note-Ellis-2)  It has been analyzed by Baeza-Yates and Soza-Pollman.[[3]](./Linear_hashing#cite_note-BS-3) It is the first in a number of schemes known as dynamic hashing[[3]](./Linear_hashing#cite_note-BS-3) [[4]](./Linear_hashing#cite_note-RD-4) such as Larson's Linear Hashing with Partial Extensions,[[5]](./Linear_hashing#cite_note-AL-5) Linear Hashing with Priority Splitting,[[6]](./Linear_hashing#cite_note-ruchte-6) Linear Hashing with Partial Expansions and Priority Splitting,[[7]](./Linear_hashing#cite_note-7) or Recursive Linear Hashing.[[8]](./Linear_hashing#cite_note-RS-8)

 

The file structure of a dynamic hashing data structure adapts itself to changes in the size of the file, so expensive periodic file reorganization is avoided.[[4]](./Linear_hashing#cite_note-RD-4) A Linear Hashing file expands by splitting a predetermined bucket into two and shrinks by merging two predetermined buckets into one. The trigger for a reconstruction depends on the flavor of the scheme; it could be an overflow at a bucket or [load factor](./Load_factor_(computer_science)) (i.e., the number of records divided by the number of buckets) moving outside of a predetermined range.[[1]](./Linear_hashing#cite_note-WL80-1) In Linear Hashing there are two types of buckets, those that are to be split and those already split. While extendible hashing splits only overflowing buckets, [spiral hashing](./Spiral_Hashing) (a.k.a. spiral storage) distributes records unevenly over the buckets such that buckets with high costs of insertion, deletion, or retrieval are earliest in line for a split.[[5]](./Linear_hashing#cite_note-AL-5)

 

Linear Hashing has also been made into a scalable distributed data structure, **LH***. In LH*, each bucket resides at a different server.[[9]](./Linear_hashing#cite_note-WL93-9) LH* itself has been expanded to provide data availability in the presence of failed buckets.[[10]](./Linear_hashing#cite_note-LMS-10) Key based operations (inserts, deletes, updates, reads) in LH and LH* take maximum constant time independent of the number of buckets and hence of records.[[1]](./Linear_hashing#cite_note-WL80-1)[[10]](./Linear_hashing#cite_note-LMS-10)

 

## Algorithm details

 

Records in LH or LH* consists of a key and a content, the latter basically all the other attributes of the record.[[1]](./Linear_hashing#cite_note-WL80-1)[[10]](./Linear_hashing#cite_note-LMS-10)  They are stored in buckets. For example, in Ellis' implementation, a bucket is a [linked list](./Linked_list) of records.[[2]](./Linear_hashing#cite_note-Ellis-2) The file allows the key based CRUD operations create or insert, read, update, and delete as well as a scan operations that scans all records, for example to do a database select operation on a non-key attribute.[[10]](./Linear_hashing#cite_note-LMS-10) Records are stored in buckets whose numbering starts with 0.[[10]](./Linear_hashing#cite_note-LMS-10)

 

The key distinction from schemes such as Fagin's extendible hashing is that as the file expands due to insertions, only one bucket is split at a time, and the order in which buckets are split is already predetermined.[[11]](./Linear_hashing#cite_note-Fagin-11)

 

### Hash functions

 

The hash function      h  i   ( c )   {\displaystyle h_{i}(c)}  ![{\displaystyle h_{i}(c)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8ac6d83346bab95678e98b37041aaf0a25228af) returns the 0-based index of the bucket that contains the record with key     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455). When a bucket which uses the hash function      h  i     {\displaystyle h_{i}}  ![{\displaystyle h_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d535f210cbd9b9fe6689e61427b3e213e5b2d547) is split into two new buckets, the hash function      h  i     {\displaystyle h_{i}}  ![{\displaystyle h_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d535f210cbd9b9fe6689e61427b3e213e5b2d547) is replaced with      h  i + 1     {\displaystyle h_{i+1}}  ![{\displaystyle h_{i+1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1374c3d7de62031ab388b589a6a736e56b7d487f) for both of those new buckets. At any time, at most two hash functions      h  l     {\displaystyle h_{l}}  ![{\displaystyle h_{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/89eaf90f8ac13f156d1c4fead974e1158d4eee71) and      h  l + 1     {\displaystyle h_{l+1}}  ![{\displaystyle h_{l+1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4525eaf2a2295491cafa75a53e0abee32f5fabd7) are used; such that     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac) corresponds to the current **level**. The family of hash functions      h  i   ( c )   {\displaystyle h_{i}(c)}  ![{\displaystyle h_{i}(c)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8ac6d83346bab95678e98b37041aaf0a25228af) is also referred to as the dynamic [hash function](./Hash_function).

 

Typically, the value of     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20) in      h  i     {\displaystyle h_{i}}  ![{\displaystyle h_{i}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d535f210cbd9b9fe6689e61427b3e213e5b2d547) corresponds to the number of rightmost binary digits of the key     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455) that are used to segregate the buckets. This dynamic hash function can be expressed arithmetically as      h  i   ( c ) ↦ ↦  ( c   mod  2    i   )   {\textstyle h_{i}(c)\mapsto (c{\bmod {2}}^{i})}  ![{\textstyle h_{i}(c)\mapsto (c{\bmod {2}}^{i})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/63ebf2100b0883de1a2a4f98cfaac982b49bfd4c). Note that when the total number of buckets is equal to one,     i = 0   {\displaystyle i=0}  ![{\displaystyle i=0}](https://wikimedia.org/api/rest_v1/media/math/render/svg/31a682d568ee6a5fe51d76423186057f625ada5c).

Complete the calculations below to determine the correct hashing function for the given hashing key     c   {\displaystyle c}  ![{\displaystyle c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/86a67b81c2de995bd608d5b2df50cd8cd7d92455).[[10]](./Linear_hashing#cite_note-LMS-10)

```
# l represents the current level
# s represents the split pointer index
a = h_l(c)
if (a < s): a = h_{l+1}(c)

```
 

### Split control

 

Linear hashing algorithms may use only controlled splits or both controlled and uncontrolled splits.

 

**Controlled splitting** occurs if a split is performed whenever the [load factor](./Load_factor_(computer_science)), which is monitored by the file, exceeds a predetermined threshold.[[10]](./Linear_hashing#cite_note-LMS-10) If the hash index uses controlled splitting, the buckets are allowed to overflow by using linked overflow blocks. When the *load factor* surpasses a set threshold, the *split pointer's* designated bucket is split. Instead of using the load factor, this threshold can also be expressed as an occupancy percentage, in which case, the maximum number of records in the hash index equals (occupancy percentage)*(max records per non-overflowed bucket)*(number of buckets).[[12]](./Linear_hashing#cite_note-:0-12)

 

An **uncontrolled split** occurs when a split is performed whenever a bucket overflows, in which case that bucket would be split into two separate buckets.

 

**File contraction** occurs in some LH algorithm implementations if a controlled split causes the load factor to sink below a threshold. In this case, a merge operation would be triggered which would undo the last split, and reset the file state.[[10]](./Linear_hashing#cite_note-LMS-10)

 

### Split pointer

 

The index of the next bucket to be split is part of the file state and called the **split pointer**     s   {\displaystyle s}  ![{\displaystyle s}](https://wikimedia.org/api/rest_v1/media/math/render/svg/01d131dfd7673938b947072a13a9744fe997e632). The split pointer corresponds to the first bucket that uses the hash function      h  l     {\displaystyle h_{l}}  ![{\displaystyle h_{l}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/89eaf90f8ac13f156d1c4fead974e1158d4eee71) instead of      h  l + 1     {\displaystyle h_{l+1}}  ![{\displaystyle h_{l+1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4525eaf2a2295491cafa75a53e0abee32f5fabd7).[[10]](./Linear_hashing#cite_note-LMS-10)

 

For example, if numerical records are inserted into the hash index according to their farthest right binary digits, the bucket corresponding with the appended bucket will be split. Thus, if we have the buckets labelled as 000, 001, 10, 11, 100, 101, we would split the bucket 10 because we are appending and creating the next sequential bucket 110. This would give us the buckets 000, 001, 010, 11, 100, 101, 110.[[12]](./Linear_hashing#cite_note-:0-12)

When a bucket is split, split pointer and possibly the level are updated according to the following, such that the level is 0 when the linear hashing index only has 1 bucket.[[10]](./Linear_hashing#cite_note-LMS-10)

```
# l represents the current level
# s represents the split pointer index
s = s + 1
if (s >= 2^l): 
    l = l + 1
    s = 0

```
 

### LH*

 

The main contribution of LH* is to allow a client of an LH* file to find the bucket where
the record resides even if the client does not know the file state. Clients in fact store
their version of the file state, which is initially just the knowledge of the first bucket, namely Bucket 0. Based on their file state, a client calculates the address of a
key and sends a request to that bucket. At the bucket, the request is checked and if
the record is not at the bucket, it is forwarded.  In a reasonably stable system, that is, 
if there is only one split or merge going on while the request is processed, it can
be shown that there are at most two forwards. After a forward, the final bucket sends an 
Image Adjustment Message to the client whose state is now closer to the state of the distributed file.[[10]](./Linear_hashing#cite_note-LMS-10)  While forwards are reasonably rare for active clients, 
their number can be even further reduced by additional information exchange between 
servers and clients [[13]](./Linear_hashing#cite_note-CS-13)

 

## Other properties

 

### File state calculation

 

The file state consists of split pointer     s   {\displaystyle s}  ![{\displaystyle s}](https://wikimedia.org/api/rest_v1/media/math/render/svg/01d131dfd7673938b947072a13a9744fe997e632) and level     l   {\displaystyle l}  ![{\displaystyle l}](https://wikimedia.org/api/rest_v1/media/math/render/svg/829091f745070b9eb97a80244129025440a1cfac). If the original file started with     N = 1   {\displaystyle N=1}  ![{\displaystyle N=1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/85982022b9eb1f295b44de55023687a490db0a39) buckets, then the number of buckets     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) and the file state are related via
[[13]](./Linear_hashing#cite_note-CS-13)

 

    n =  2  l   + s   {\displaystyle n=2^{l}+s}  ![{\displaystyle n=2^{l}+s}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d3f5f341d4f42ccce5de1c9d7c51df64b5ec5774).

 

## Adoption in language systems

 

Griswold and Townsend [[14]](./Linear_hashing#cite_note-14) discussed the adoption of linear hashing in the [Icon language](./Icon_language). They discussed the implementation alternatives of [dynamic array](./Dynamic_array) algorithm used in linear hashing, and presented performance comparisons using a list of Icon benchmark applications.

 

## Adoption in database systems

 

Linear hashing is used in the [Berkeley database system (BDB)](./Berkeley_DB), which in turn is used by many software systems, using a C implementation derived from the [CACM](./Communications_of_the_ACM) article and first published on the Usenet in 1988 by Esmond Pitt.

 

## References

  
1. [1](./Linear_hashing#cite_ref-WL80_1-0) [2](./Linear_hashing#cite_ref-WL80_1-1) [3](./Linear_hashing#cite_ref-WL80_1-2) [4](./Linear_hashing#cite_ref-WL80_1-3) Litwin, Witold (1980), ["Linear hashing: A new tool for file and table addressing"](https://www.cs.cmu.edu/afs/cs.cmu.edu/user/christos/www/courses/826-resources/PAPERS+BOOK/linear-hashing.PDF) (PDF), *Proc. 6th Conference on Very Large Databases*: 212–223
2. [1](./Linear_hashing#cite_ref-Ellis_2-0) [2](./Linear_hashing#cite_ref-Ellis_2-1)  Ellis, Carla Schlatter (June 1987), "Concurrency in Linear Hashing", *ACM Transactions on Database Systems*, **12** (2): 195–217, [doi](./Doi_(identifier)):[10.1145/22952.22954](https://doi.org/10.1145%2F22952.22954), [S2CID](./S2CID_(identifier)) [14260177](https://api.semanticscholar.org/CorpusID:14260177) 
3. [1](./Linear_hashing#cite_ref-BS_3-0) [2](./Linear_hashing#cite_ref-BS_3-1) Baeza-Yates, Ricardo; Soza-Pollman, Hector (1998), ["Analysis of Linear Hashing Revised"](https://web.archive.org/web/20190307204217/http://pdfs.semanticscholar.org/e6cd/667fef7cd377ed8d417cc648d3d578675ad5.pdf) (PDF), *Nordic Journal of Computing*: 70–85, [S2CID](./S2CID_(identifier)) [7497598](https://api.semanticscholar.org/CorpusID:7497598), archived from [the original](http://pdfs.semanticscholar.org/e6cd/667fef7cd377ed8d417cc648d3d578675ad5.pdf) (PDF) on 2019-03-07
4. [1](./Linear_hashing#cite_ref-RD_4-0) [2](./Linear_hashing#cite_ref-RD_4-1) Enbody, Richard; Du, HC (June 1988), "Dynamic hashing schemes", *ACM Computing Surveys*, **20** (2): 85–113, [doi](./Doi_(identifier)):[10.1145/46157.330532](https://doi.org/10.1145%2F46157.330532), [S2CID](./S2CID_(identifier)) [1437123](https://api.semanticscholar.org/CorpusID:1437123)
5. [1](./Linear_hashing#cite_ref-AL_5-0) [2](./Linear_hashing#cite_ref-AL_5-1) Larson, Per-Åke (April 1988), "Dynamic Hash Tables", *Communications of the ACM*, **31** (4): 446–457, [doi](./Doi_(identifier)):[10.1145/42404.42410](https://doi.org/10.1145%2F42404.42410), [S2CID](./S2CID_(identifier)) [207548097](https://api.semanticscholar.org/CorpusID:207548097)
6. [↑](./Linear_hashing#cite_ref-ruchte_6-0)  Ruchte, Willard; Tharp, Alan (Feb 1987), "Linear hashing with Priority Splitting: A method for improving the retrieval performance of linear hashing", *IEEE Third International Conference on Data Engineering*: 2–9 
7. [↑](./Linear_hashing#cite_ref-7)  Manolopoulos, Yannis; Lorentzos, N. (1994), "Performance of linear hashing schemes for primary key retrieval", *Information Systems*, **19** (5): 433–446, [doi](./Doi_(identifier)):[10.1016/0306-4379(94)90005-1](https://doi.org/10.1016%2F0306-4379%2894%2990005-1) 
8. [↑](./Linear_hashing#cite_ref-RS_8-0)  Ramamohanarao, K.; Sacks-Davis, R. (Sep 1984), "Recursive linear hashing", *ACM Transactions on Database Systems*, **9** (3): 369–391, [doi](./Doi_(identifier)):[10.1145/1270.1285](https://doi.org/10.1145%2F1270.1285), [S2CID](./S2CID_(identifier)) [18577730](https://api.semanticscholar.org/CorpusID:18577730) 
9. [↑](./Linear_hashing#cite_ref-WL93_9-0)  Litwin, Witold; Neimat, Marie-Anne; Schneider, Donavan A. (1993), "LH: Linear Hashing for distributed files", *ACM SIGMOD Record*, **22** (2): 327–336, [doi](./Doi_(identifier)):[10.1145/170036.170084](https://doi.org/10.1145%2F170036.170084), [S2CID](./S2CID_(identifier)) [259938726](https://api.semanticscholar.org/CorpusID:259938726) 
10. [1](./Linear_hashing#cite_ref-LMS_10-0) [2](./Linear_hashing#cite_ref-LMS_10-1) [3](./Linear_hashing#cite_ref-LMS_10-2) [4](./Linear_hashing#cite_ref-LMS_10-3) [5](./Linear_hashing#cite_ref-LMS_10-4) [6](./Linear_hashing#cite_ref-LMS_10-5) [7](./Linear_hashing#cite_ref-LMS_10-6) [8](./Linear_hashing#cite_ref-LMS_10-7) [9](./Linear_hashing#cite_ref-LMS_10-8) [10](./Linear_hashing#cite_ref-LMS_10-9) [11](./Linear_hashing#cite_ref-LMS_10-10)  Litwin, Witold; Moussa, Rim; Schwarz, Thomas (Sep 2005), ["LH*RS - a highly-available scalable distributed data structure"](https://basepub.dauphine.fr/handle/123456789/15124), *ACM Transactions on Database Systems*, **30** (3): 769–811, [doi](./Doi_(identifier)):[10.1145/1093382.1093386](https://doi.org/10.1145%2F1093382.1093386), [S2CID](./S2CID_(identifier)) [1802386](https://api.semanticscholar.org/CorpusID:1802386) 
11. [↑](./Linear_hashing#cite_ref-Fagin_11-0)  Fagin, Ronald; Nievergelt, Jurg; Pippenger, Nicholas; Strong, Raymond (Sep 1979), ["Extendible Hashing - A Fast Access Method for Dynamic Files"](http://dl.acm.org/citation.cfm?doid=320083.320092), *ACM Transactions on Database Systems*, **4** (2): 315–344, [doi](./Doi_(identifier)):[10.1145/320083.320092](https://doi.org/10.1145%2F320083.320092), [S2CID](./S2CID_(identifier)) [2723596](https://api.semanticscholar.org/CorpusID:2723596) 
12. [1](./Linear_hashing#cite_ref-:0_12-0) [2](./Linear_hashing#cite_ref-:0_12-1) Silberschatz, Abraham; Korth, Henry F.; Sudarshan, S. (2020). *Database system concepts* (Seventh ed.). New York, NY: McGraw-Hill Education. [ISBN](./ISBN_(identifier)) [978-1-260-08450-4](./Special:BookSources/978-1-260-08450-4).
13. [1](./Linear_hashing#cite_ref-CS_13-0) [2](./Linear_hashing#cite_ref-CS_13-1)  Chabkinian, Juan; Schwarz, Thomas (2016), "Fast LH*", *International Journal of Parallel Programming*, **44** (4): 709–734, [doi](./Doi_(identifier)):[10.1007/s10766-015-0371-8](https://doi.org/10.1007%2Fs10766-015-0371-8), [S2CID](./S2CID_(identifier)) [7448240](https://api.semanticscholar.org/CorpusID:7448240) 
14. [↑](./Linear_hashing#cite_ref-14) [Griswold, William G.](./Bill_Griswold); Townsend, Gregg M. (April 1993), ["The Design and Implementation of Dynamic Hashing for Sets and Tables in Icon"](http://citeseer.ist.psu.edu/griswold93design.html), *Software: Practice and Experience*, **23** (4): 351–367, [doi](./Doi_(identifier)):[10.1002/spe.4380230402](https://doi.org/10.1002%2Fspe.4380230402), [S2CID](./S2CID_(identifier)) [11595927](https://api.semanticscholar.org/CorpusID:11595927)

 

## External links

 
- [TommyDS, C implementation of a Linear Hashtable](https://tommyds.sourceforge.net/)
- [An in Memory Go Implementation with Explanation](http://hackthology.com/an-in-memory-go-implementation-of-linear-hashing.html)
- [A C++ Implementation of Linear Hashtable which Supports Both Filesystem and In-Memory storage](https://github.com/KevinStern/index-cpp/blob/master/src/linear_hashing_table.h)

 

## See also

 
- [Extendible hashing](./Extendible_hashing)
- [Consistent hashing](./Consistent_hashing)
- [Spiral Hashing](./Spiral_Hashing)