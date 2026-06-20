---
source: https://en.wikipedia.org/wiki/Skip_list
fetched: 2026-06-19
---

Probabilistic data structure 
| Skip list |
| --- |
| Type | List |
| Invented | 1989 |
| Invented by | W. Pugh |
| Time complexityinbig O notationOperationAverageWorst caseSearchO(log⁡n){\displaystyle {\mathcal {O}}(\log n)}O(n){\displaystyle {\mathcal {O}}(n)}[1]InsertO(log⁡n){\displaystyle {\mathcal {O}}(\log n)}O(n){\displaystyle {\mathcal {O}}(n)}DeleteO(log⁡n){\displaystyle {\mathcal {O}}(\log n)}O(n){\displaystyle {\mathcal {O}}(n)}Space complexitySpaceO(n){\displaystyle {\mathcal {O}}(n)}O(nlog⁡n){\displaystyle {\mathcal {O}}(n\log n)}[1] | Time complexityinbig O notation | Operation | Average | Worst case | Search | O(log⁡n){\displaystyle {\mathcal {O}}(\log n)} | O(n){\displaystyle {\mathcal {O}}(n)}[1] | Insert | O(log⁡n){\displaystyle {\mathcal {O}}(\log n)} | O(n){\displaystyle {\mathcal {O}}(n)} | Delete | O(log⁡n){\displaystyle {\mathcal {O}}(\log n)} | O(n){\displaystyle {\mathcal {O}}(n)} | Space complexity | Space | O(n){\displaystyle {\mathcal {O}}(n)} | O(nlog⁡n){\displaystyle {\mathcal {O}}(n\log n)}[1] |
| Time complexityinbig O notation |
| Operation | Average | Worst case |
| Search | O(log⁡n){\displaystyle {\mathcal {O}}(\log n)} | O(n){\displaystyle {\mathcal {O}}(n)}[1] |
| Insert | O(log⁡n){\displaystyle {\mathcal {O}}(\log n)} | O(n){\displaystyle {\mathcal {O}}(n)} |
| Delete | O(log⁡n){\displaystyle {\mathcal {O}}(\log n)} | O(n){\displaystyle {\mathcal {O}}(n)} |
| Space complexity |
| Space | O(n){\displaystyle {\mathcal {O}}(n)} | O(nlog⁡n){\displaystyle {\mathcal {O}}(n\log n)}[1] |

 
| Part ofa serieson |
| --- |
| Probabilisticdata structures |
| Bloom filterCount sketchCount–min sketchQuotient filterSkip list |
| Random trees |
| Random binary treeTreapRapidly exploring random tree |
| Related |
| Randomized algorithmHyperLogLog |
| vte |

 

In [computer science](./Computer_science), a **skip list** (or **skiplist**) is a [probabilistic](./Randomized_algorithm) [data structure](./Data_structure) that allows       O   ( log ⁡ ⁡  n )   {\displaystyle {\mathcal {O}}(\log n)}  ![{\displaystyle {\mathcal {O}}(\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/74a9dfea91c47d1c6563e89bbcd891771b91acfa) [average complexity](./Average-case_complexity) for search as well as       O   ( log ⁡ ⁡  n )   {\displaystyle {\mathcal {O}}(\log n)}  ![{\displaystyle {\mathcal {O}}(\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/74a9dfea91c47d1c6563e89bbcd891771b91acfa) average complexity for insertion within an [ordered sequence](./Ordered_sequence) of     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) elements. Thus it can get the best features of a sorted [array](./Array_data_structure) (for searching) while maintaining a [linked list](./Linked_list)-like structure that allows insertion, which is not possible with a static array. Fast search is made possible by maintaining a linked hierarchy of subsequences, with each successive subsequence skipping over fewer elements than the previous one *(see the picture below)*. Searching starts in the sparsest subsequence until two consecutive elements have been found, one smaller and one larger than or equal to the element searched for. Via the linked hierarchy, these two elements link to elements of the next sparsest subsequence, where searching is continued until finally searching in the full sequence. The elements that are skipped over may be chosen probabilistically[[2]](./Skip_list#cite_note-pugh-2) or deterministically,[[3]](./Skip_list#cite_note-3) with the former being more common.

 

## Description

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/8/86/Skip_list.svg/500px-Skip_list.svg.png)](./File:Skip_list.svg)A schematic picture of the skip list data structure. Each box with an arrow represents a pointer and a row is a [linked list](./Linked_list) giving a sparse subsequence; the numbered boxes (in yellow) at the bottom represent the ordered data sequence. Searching proceeds downwards from the sparsest subsequence at the top until consecutive elements bracketing the search element are found. 

A skip list is built in layers.  The bottom layer     1   {\displaystyle 1}  ![{\displaystyle 1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/92d98b82a3778f043108d4e20960a9193df57cbf) is an ordinary ordered [linked list](./Linked_list).  Each higher layer acts as an "express lane" for the lists below, where an element in layer     i   {\displaystyle i}  ![{\displaystyle i}](https://wikimedia.org/api/rest_v1/media/math/render/svg/add78d8608ad86e54951b8c8bd6c8d8416533d20) appears in layer     i + 1   {\displaystyle i+1}  ![{\displaystyle i+1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2fe1bfc8314922e4c3fdb4e8eceb20a00b4f011d) with some fixed probability     p   {\displaystyle p}  ![{\displaystyle p}](https://wikimedia.org/api/rest_v1/media/math/render/svg/81eac1e205430d1f40810df36a0edffdc367af36) (two commonly used values for     p   {\displaystyle p}  ![{\displaystyle p}](https://wikimedia.org/api/rest_v1/media/math/render/svg/81eac1e205430d1f40810df36a0edffdc367af36) are     1  /  2   {\displaystyle 1/2}  ![{\displaystyle 1/2}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e308a3a46b7fdce07cc09dcab9e8d8f73e37d935) or     1  /  4   {\displaystyle 1/4}  ![{\displaystyle 1/4}](https://wikimedia.org/api/rest_v1/media/math/render/svg/4d3cf1ef33695c3d98cb09f01e5700f927ce928c)).  On average, each element appears in     1  /  ( 1 − −  p )   {\displaystyle 1/(1-p)}  ![{\displaystyle 1/(1-p)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/212e9859c8d055e32c9a1b32fd6d3490a4bb84db) lists, and the tallest element (usually a special head element at the front of the skip list) appears in all the lists.  The skip list contains      log  1  /  p   ⁡ ⁡  n    {\displaystyle \log _{1/p}n\,}  ![{\displaystyle \log _{1/p}n\,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/909fb0d0b25ebd96ecfab41e93ce5ee2c1e2df79) (i.e. logarithm base     1  /  p   {\displaystyle 1/p}  ![{\displaystyle 1/p}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2cdfd6eb8d2c6f424b698d06aa99d31895c47e91) of     n   {\displaystyle n}  ![{\displaystyle n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b)) lists.

 

A search for a target element begins at the head element in the top list, and proceeds horizontally until the current element is greater than or equal to the target. If the current element is equal to the target, it has been found. If the current element is greater than the target, or the search reaches the end of the linked list, the procedure is repeated after returning to the previous element and dropping down vertically to the next lower list. The expected number of steps in each linked list is at most     1  /  p   {\displaystyle 1/p}  ![{\displaystyle 1/p}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2cdfd6eb8d2c6f424b698d06aa99d31895c47e91), which can be seen by tracing the search path backwards from the target until reaching an element that appears in the next higher list or reaching the beginning of the current list.  Therefore, the total *expected* cost of a search is        1 p     log  1  /  p   ⁡ ⁡  n   {\displaystyle {\tfrac {1}{p}}\log _{1/p}n}  ![{\displaystyle {\tfrac {1}{p}}\log _{1/p}n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c963a559c75713f6b587853c9f6bce09683debc2) which is       O   ( log ⁡ ⁡  n )    {\displaystyle {\mathcal {O}}(\log n)\,}  ![{\displaystyle {\mathcal {O}}(\log n)\,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d4564f8652da4d6bc379228c67a2e1f86214ae8), when     p   {\displaystyle p}  ![{\displaystyle p}](https://wikimedia.org/api/rest_v1/media/math/render/svg/81eac1e205430d1f40810df36a0edffdc367af36) is a constant. By choosing different values of     p   {\displaystyle p}  ![{\displaystyle p}](https://wikimedia.org/api/rest_v1/media/math/render/svg/81eac1e205430d1f40810df36a0edffdc367af36), it is possible to trade search costs against storage costs. For example, the value     p = 1  /  e   {\displaystyle p=1/e}  ![{\displaystyle p=1/e}](https://wikimedia.org/api/rest_v1/media/math/render/svg/383f81e1ab5142d1678b7198b15a658bad6d2de2) minimizes the average search time of skip lists, whereas the value     p = 1  /  2   {\displaystyle p=1/2}  ![{\displaystyle p=1/2}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c4a77b7a2e96414f0214f2d6ee49e462ccf33af0) simplifies their implementation. 

 

### Implementation details

 [![](//upload.wikimedia.org/wikipedia/commons/thumb/2/2c/Skip_list_add_element-en.gif/500px-Skip_list_add_element-en.gif)](./File:Skip_list_add_element-en.gif)Inserting elements into a skip list 

The elements used for a skip list can contain more than one pointer since they can participate in more than one list.

 

Insertions and deletions are implemented much like the corresponding linked-list operations, except that "tall" elements must be inserted into or deleted from more than one linked list.

 

      O   ( n )   {\displaystyle {\mathcal {O}}(n)}  ![{\displaystyle {\mathcal {O}}(n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3c7bbe0124ae81792773344bc8709fc2f9c9910d) operations, which force us to visit every node in ascending order (such as printing the entire list), provide the opportunity to perform a behind-the-scenes derandomization of the level structure of the skip-list in an optimal way, bringing the skip list to       O   ( log ⁡ ⁡  n )   {\displaystyle {\mathcal {O}}(\log n)}  ![{\displaystyle {\mathcal {O}}(\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/74a9dfea91c47d1c6563e89bbcd891771b91acfa) search time. (Choose the level of the i'th finite node to be 1 plus the number of times it is possible to repeatedly divide i by 2 before it becomes odd.  Also, i=0 for the negative infinity header as there is the usual special case of choosing the highest possible level for negative and/or positive infinite nodes.) However this also allows someone to know where all of the higher-than-level 1 nodes are and delete them.

 

Alternatively, the level structure could be made quasi-random in the following way:

 
```
make all nodes level 1
j ← 1
while the number of nodes at level j > 1 do
    for each i'th node at level j do
        if i is odd and i is not the last node at level j
            randomly choose whether to promote it to level j+1
        else if i is even and node i-1 was not promoted
            promote it to level j+1
        end if
    repeat
    j ← j + 1
repeat
```
 

Like the derandomized version, quasi-randomization is only done when there is some other reason to be running an       O   ( n )   {\displaystyle {\mathcal {O}}(n)}  ![{\displaystyle {\mathcal {O}}(n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3c7bbe0124ae81792773344bc8709fc2f9c9910d) operation (which visits every node).

 

The advantage of this quasi-randomness is that it doesn't give away nearly as much level-structure related information to an [adversarial user](./Adversary_(online_algorithm)) as the de-randomized one.  This is desirable because an adversarial user who is able to tell which nodes are not at the lowest level can pessimize performance by simply deleting higher-level nodes. (Bethea and Reiter however argue that nonetheless an adversary can use probabilistic and timing methods to force performance degradation.[[4]](./Skip_list#cite_note-4)) The search performance is still guaranteed to be logarithmic.

 

It would be tempting to make the following "optimization":  In the part which says "Next, for each *i*th...", forget about doing a coin-flip for each even-odd pair.  Just flip a coin once to decide whether to promote only the even ones or only the odd ones.  Instead of       O   ( n log ⁡ ⁡  n )   {\displaystyle {\mathcal {O}}(n\log n)}  ![{\displaystyle {\mathcal {O}}(n\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/9981ede263cbf28215d3a70bf30f55db41a6e692) coin flips, there would only be       O   ( log ⁡ ⁡  n )   {\displaystyle {\mathcal {O}}(\log n)}  ![{\displaystyle {\mathcal {O}}(\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/74a9dfea91c47d1c6563e89bbcd891771b91acfa) of them.  Unfortunately, this gives the adversarial user a 50/50 chance of being correct upon guessing that all of the even numbered nodes (among the ones at level 1 or higher) are higher than level one.  This is despite the property that there is a very low probability of guessing that a particular node is at level *N* for some integer *N*.

 

A skip list does not provide the same absolute worst-case performance guarantees as more traditional [balanced tree](./Balanced_tree) data structures, because it is always possible (though with very low probability[[5]](./Skip_list#cite_note-5)) that the coin-flips used to build the skip list will produce a badly balanced structure.  However, they work well in practice, and the randomized balancing scheme has been argued to be easier to implement than the deterministic balancing schemes used in balanced binary search trees.  Skip lists are also useful in [parallel computing](./Parallel_computing), where insertions can be done in different parts of the skip list in parallel without any global rebalancing of the data structure. Such parallelism can be especially advantageous for resource discovery in an ad-hoc [wireless network](./Wireless_network) because a randomized skip list can be made robust to the loss of any single node.[[6]](./Skip_list#cite_note-6)

 

### Indexable skiplist

 

As described above, a skip list is capable of fast       O   ( log ⁡ ⁡  n )   {\displaystyle {\mathcal {O}}(\log n)}  ![{\displaystyle {\mathcal {O}}(\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/74a9dfea91c47d1c6563e89bbcd891771b91acfa) insertion and removal of values from a sorted sequence, but it has only slow       O   ( n )   {\displaystyle {\mathcal {O}}(n)}  ![{\displaystyle {\mathcal {O}}(n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3c7bbe0124ae81792773344bc8709fc2f9c9910d) lookups of values at a given position in the sequence (i.e. return the 500th value); however, with a minor modification the speed of [random access](./Random_access) indexed lookups can be improved to        O   ( log ⁡ ⁡  n )   {\displaystyle {\mathcal {O}}(\log n)}  ![{\displaystyle {\mathcal {O}}(\log n)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/74a9dfea91c47d1c6563e89bbcd891771b91acfa).

 

For every link, also store the width of the link.  The width is defined as the number of bottom layer links being traversed by each of the higher layer "express lane" links.

 

For example, here are the widths of the links in the example at the top of the page:

 
```
   1                               10
 o---> o---------------------------------------------------------> o    Top level
   1           3              2                    5
 o---> o---------------> o---------> o---------------------------> o    Level 3
   1        2        1        2              3              2
 o---> o---------> o---> o---------> o---------------> o---------> o    Level 2
   1     1     1     1     1     1     1     1     1     1     1 
 o---> o---> o---> o---> o---> o---> o---> o---> o---> o---> o---> o    Bottom level
Head  1st   2nd   3rd   4th   5th   6th   7th   8th   9th   10th  NIL
      Node  Node  Node  Node  Node  Node  Node  Node  Node  Node
```
 

Notice that the width of a higher level link is the sum of the component links below it (i.e. the width 10 link spans the links of widths 3, 2 and 5 immediately below it).  Consequently, the sum of all widths is the same on every level (10 + 1 = 1 + 3 + 2 + 5 = 1 + 2 + 1 + 2 + 3 + 2).

 

To index the skip list and find the i'th value, traverse the skip list while counting down the widths of each traversed link.  Descend a level whenever the upcoming width would be too large.

 

For example, to find the node in the fifth position (Node 5), traverse a link of width 1 at the top level.  Now four more steps are needed but the next width on this level is ten which is too large, so drop one level.  Traverse one link of width 3.  Since another step of width 2 would be too far, drop down to the bottom level.  Now traverse the final link of width 1 to reach the target running total of 5 (1+3+1). 

 
```
function lookupByPositionIndex(i)
    node ← head
    i ← i + 1                           # don't count the head as a step
    for level from top to bottom do
        while i ≥ node.width[level] do # if next step is not too far
            i ← i - node.width[level]  # subtract the current width
            node ← node.next[level]    # traverse forward at the current level
        repeat
    repeat
    return node.value
end function
```
 

This method of implementing indexing is detailed in *"A skip list cookbook"* by William Pugh[[7]](./Skip_list#cite_note-7)

 

## History

 

Skip lists were first described in 1989 by [William Pugh](./William_Pugh_(computer_scientist)).[[8]](./Skip_list#cite_note-8)

 

To quote the author:

 

*Skip lists are a probabilistic data structure that seem likely to supplant balanced trees as the implementation method of choice for many applications. Skip list algorithms have the same asymptotic expected time bounds as balanced trees and are simpler, faster and use less space.*

— William Pugh, *Concurrent Maintenance of Skip Lists* (1989)

 

## Usages

 

List of applications and frameworks that use skip lists:

 
- [Apache Portable Runtime](./Apache_Portable_Runtime) implements skip lists.[[9]](./Skip_list#cite_note-9)
- [MemSQL](./MemSQL) uses lock-free skip lists as its prime indexing structure for its database technology.
- [MuQSS](./MuQSS), for the [Linux kernel](./Linux_kernel), is a [CPU scheduler](./Scheduling_(computing)#SHORT-TERM) built on skip lists.[[10]](./Skip_list#cite_note-10)[[11]](./Skip_list#cite_note-11)
- [Cyrus IMAP server](./Cyrus_IMAP_server) offers a "skiplist" backend DB implementation[[12]](./Skip_list#cite_note-12)
- IBM [DOORS](./DOORS) offers skip lists as a data type in its DOORS/DXL (DOORS eXtension Language) scripting language
- [Lucene](./Lucene) uses skip lists to search delta-encoded posting lists in logarithmic time.[*[citation needed](./Wikipedia:Citation_needed)*]
- The "QMap" key/value dictionary (up to Qt 4) template class of [Qt](./Qt_(framework)) is implemented with skip lists.[[13]](./Skip_list#cite_note-13)
- [Redis](./Redis), an ANSI-C open-source persistent key/value store for Posix systems, uses skip lists in its implementation of ordered sets.[[14]](./Skip_list#cite_note-14)
- [Discord](./Discord) uses skip lists to handle storing and updating the list of members in a [server](./Discord#Servers).[[15]](./Skip_list#cite_note-15)
- [RocksDB](./RocksDB) uses skip lists for its default Memtable implementation.[[16]](./Skip_list#cite_note-16)
- [Java](./Java_(programming_language)) uses skip lists for its [ConcurrentSkipListSet](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/concurrent/ConcurrentSkipListSet.html) and [ConcurrentSkipListMap](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/concurrent/ConcurrentSkipListMap.html).

 

Skip lists are also used in distributed applications (where the nodes represent physical computers, and pointers represent network connections) and for implementing highly scalable concurrent [priority queues](./Priority_queue) with less lock contention,[[17]](./Skip_list#cite_note-17) or even [ without locking](./Non-blocking_algorithm),[[18]](./Skip_list#cite_note-18)[[19]](./Skip_list#cite_note-19)[[20]](./Skip_list#cite_note-20) as well as [lock-free](./Lock-free) concurrent dictionaries.[[21]](./Skip_list#cite_note-21) There are also several US patents for using skip lists to implement (lockless) priority queues and concurrent dictionaries.[[22]](./Skip_list#cite_note-22)

 

## See also

 
- [Bloom filter](./Bloom_filter)
- [Skip graph](./Skip_graph)

 

## References

  
1. [1](./Skip_list#cite_ref-cs.uwaterloo_1-0) [2](./Skip_list#cite_ref-cs.uwaterloo_1-1) Papadakis, Thomas (1993). [*Skip Lists and Probabilistic Analysis of Algorithms*](http://www.cs.uwaterloo.ca/research/tr/1993/28/root2side.pdf) (PDF) (Ph.D.). University of Waterloo.
2. [↑](./Skip_list#cite_ref-pugh_2-0) [Pugh, W.](./William_Pugh_(computer_scientist)) (1990). ["Skip lists: A probabilistic alternative to balanced trees"](https://ftp.cs.umd.edu/pub/skipLists/skiplists.pdf) (PDF). *[Communications of the ACM](./Communications_of_the_ACM)*. **33** (6): 668–676. [doi](./Doi_(identifier)):[10.1145/78973.78977](https://doi.org/10.1145%2F78973.78977). [S2CID](./S2CID_(identifier)) [207691558](https://api.semanticscholar.org/CorpusID:207691558).
3. [↑](./Skip_list#cite_ref-3) [Munro, J. Ian](./Ian_Munro_(computer_scientist)); Papadakis, Thomas; [Sedgewick, Robert](./Robert_Sedgewick_(computer_scientist)) (1992). ["Deterministic skip lists"](https://www.ic.unicamp.br/~celio/peer2peer/skip-net-graph/deterministic-skip-lists-munro.pdf) (PDF). *Proceedings of the third annual ACM-SIAM symposium on Discrete algorithms (SODA '92)*. Orlando, Florida, USA: Society for Industrial and Applied Mathematics, Philadelphia, PA, USA. pp. 367–375. [S2CID](./S2CID_(identifier)) [7477119](https://api.semanticscholar.org/CorpusID:7477119).
4. [↑](./Skip_list#cite_ref-4) Bethea, Darrell; Reiter, Michael K. (September 21–23, 2009). [*Data Structures with Unpredictable Timing*](https://www.cs.unc.edu/~djb/papers/2009-ESORICS.pdf#page=5) (PDF). ESORICS 2009, 14th European Symposium on Research in Computer Security. Saint-Malo, France. pp. 456–471, §4 "Skip Lists". [doi](./Doi_(identifier)):[10.1007/978-3-642-04444-1_28](https://doi.org/10.1007%2F978-3-642-04444-1_28). [ISBN](./ISBN_(identifier)) [978-3-642-04443-4](./Special:BookSources/978-3-642-04443-4).
5. [↑](./Skip_list#cite_ref-5) Sen, Sandeep (1991). "Some observations on skip lists". *Information Processing Letters*. **39** (4): 173–176. [doi](./Doi_(identifier)):[10.1016/0020-0190(91)90175-H](https://doi.org/10.1016%2F0020-0190%2891%2990175-H).
6. [↑](./Skip_list#cite_ref-6) Shah, Gauri (2003). [*Distributed Data Structures for Peer-to-Peer Systems*](http://www.cs.yale.edu/homes/shah/pubs/thesis.pdf) (PDF) (Ph.D. thesis). Yale University.
7. [↑](./Skip_list#cite_ref-7) 
William Pugh.
*"A skip list cookbook"*.
1990.
[Section 3.4 Linear List Operations ](https://drum.lib.umd.edu/items/56c44671-3973-46b6-9e52-f71dc95af178).

8. [↑](./Skip_list#cite_ref-8) [Pugh, William](./William_Pugh_(computer_scientist)) (April 1989). [*Concurrent Maintenance of Skip Lists*](http://drum.lib.umd.edu/handle/1903/542) (PS, PDF) (Technical report). Dept. of Computer Science, U. Maryland. CS-TR-2222.
9. [↑](./Skip_list#cite_ref-9)  [Apache Portable Runtime APR 1.6 documentation](https://apr.apache.org/docs/apr/1.6/group__apr__skiplist.html) 
10. [↑](./Skip_list#cite_ref-10) 
LWN's
[article](https://lwn.net/Articles/720227) 
11. [↑](./Skip_list#cite_ref-11) ["LKML: Con Kolivas: [ANNOUNCE] Multiple Queue Skiplist Scheduler version 0.120"](https://lkml.org/lkml/2016/10/29/4). *lkml.org*. Retrieved 2017-05-11.
12. [↑](./Skip_list#cite_ref-12) 
Cyrus IMAP server.
[skiplist source file](https://github.com/cyrusimap/cyrus-imapd/blob/master/lib/cyrusdb_skiplist.c) 
13. [↑](./Skip_list#cite_ref-13)  [QMap](http://qt-project.org/doc/qt-4.8/qmap.html#details) 
14. [↑](./Skip_list#cite_ref-14) ["Redis ordered set implementation"](https://github.com/antirez/redis/blob/unstable/src/t_zset.c). *[GitHub](./GitHub)*.
15. [↑](./Skip_list#cite_ref-15) Nowack, Matt. ["Using Rust to Scale Elixir for 11 Million Concurrent Users"](https://discord.com/blog/using-rust-to-scale-elixir-for-11-million-concurrent-users). *Discord Blog*. Retrieved 23 July 2023.
16. [↑](./Skip_list#cite_ref-16) ["MemTable"](https://github.com/facebook/rocksdb/wiki/MemTable). *GitHub*. Retrieved 2023-12-12.
17. [↑](./Skip_list#cite_ref-17) Shavit, N.; Lotan, I. (2000). ["Skiplist-based concurrent priority queues"](http://www.cs.tau.ac.il/~shanir/nir-pubs-web/Papers/Priority_Queues.pdf) (PDF). *Proceedings 14th International Parallel and Distributed Processing Symposium. IPDPS 2000*. p. 263. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.116.3489](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.116.3489). [doi](./Doi_(identifier)):[10.1109/IPDPS.2000.845994](https://doi.org/10.1109%2FIPDPS.2000.845994). [ISBN](./ISBN_(identifier)) [978-0-7695-0574-9](./Special:BookSources/978-0-7695-0574-9). [S2CID](./S2CID_(identifier)) [8664407](https://api.semanticscholar.org/CorpusID:8664407).
18. [↑](./Skip_list#cite_ref-18) Sundell, H.; Tsigas, P. (2003). "Fast and lock-free concurrent priority queues for multi-thread systems". *Proceedings International Parallel and Distributed Processing Symposium*. p. 11. [CiteSeerX](./CiteSeerX_(identifier)) [10.1.1.113.4552](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.113.4552). [doi](./Doi_(identifier)):[10.1109/IPDPS.2003.1213189](https://doi.org/10.1109%2FIPDPS.2003.1213189). [ISBN](./ISBN_(identifier)) [978-0-7695-1926-5](./Special:BookSources/978-0-7695-1926-5). [S2CID](./S2CID_(identifier)) [20995116](https://api.semanticscholar.org/CorpusID:20995116).
19. [↑](./Skip_list#cite_ref-19) Fomitchev, Mikhail; Ruppert, Eric (2004). [*Lock-free linked lists and skip lists*](http://www.cse.yorku.ca/~ruppert/papers/lfll.pdf) (PDF). Proc. Annual ACM Symp. on Principles of Distributed Computing (PODC). pp. 50–59. [doi](./Doi_(identifier)):[10.1145/1011767.1011776](https://doi.org/10.1145%2F1011767.1011776). [ISBN](./ISBN_(identifier)) [1581138024](./Special:BookSources/1581138024).
20. [↑](./Skip_list#cite_ref-20) Bajpai, R.; Dhara, K. K.; Krishnaswamy, V. (2008). "QPID: A Distributed Priority Queue with Item Locality". *2008 IEEE International Symposium on Parallel and Distributed Processing with Applications*. p. 215. [doi](./Doi_(identifier)):[10.1109/ISPA.2008.90](https://doi.org/10.1109%2FISPA.2008.90). [ISBN](./ISBN_(identifier)) [978-0-7695-3471-8](./Special:BookSources/978-0-7695-3471-8). [S2CID](./S2CID_(identifier)) [15677922](https://api.semanticscholar.org/CorpusID:15677922).
21. [↑](./Skip_list#cite_ref-21) Sundell, H. K.; Tsigas, P. (2004). ["Scalable and lock-free concurrent dictionaries"](http://www.cse.chalmers.se/~tsigas/papers/Lock-Free_Dictionary.pdf) (PDF). *Proceedings of the 2004 ACM symposium on Applied computing - SAC '04*. p. 1438. [doi](./Doi_(identifier)):[10.1145/967900.968188](https://doi.org/10.1145%2F967900.968188). [ISBN](./ISBN_(identifier)) [978-1581138122](./Special:BookSources/978-1581138122). [S2CID](./S2CID_(identifier)) [10393486](https://api.semanticscholar.org/CorpusID:10393486).
22. [↑](./Skip_list#cite_ref-22) [US patent 7937378](https://worldwide.espacenet.com/textdoc?DB=EPODOC&IDX=US7937378) 

 

## External links

   [![Wikimedia Commons logo](//upload.wikimedia.org/wikipedia/en/thumb/4/4a/Commons-logo.svg/40px-Commons-logo.svg.png)](./File:Commons-logo.svg) Wikimedia Commons has media related to [Skip list](https://commons.wikimedia.org/wiki/Category:Skip%20list).  
- ["Skip list" entry](https://xlinux.nist.gov/dads/HTML/skiplist.html) in the [Dictionary of Algorithms and Data Structures](./Dictionary_of_Algorithms_and_Data_Structures?action=edit&redlink=1)
- [Skip Lists lecture (MIT OpenCourseWare: Introduction to Algorithms) ](http://videolectures.net/mit6046jf05_demaine_lec12/)
- [Open Data Structures - Chapter 4 - Skiplists](http://opendatastructures.org/versions/edition-0.1e/ods-java/4_Skiplists.html), [Pat Morin](./Pat_Morin)
- [Skip tree graphs, a distributed version of skip trees](http://www0.cs.ucl.ac.uk/staff/a.gonzalezbeltran/pubs/icc2007.pdf)
- [More on skip tree graphs, a distributed version of skip trees](http://www0.cs.ucl.ac.uk/staff/a.gonzalezbeltran/pubs/AGB-comcom08.pdf)

 
| vteData structures |
| --- |
| Types | CollectionContainer |
| Abstract | Associative arrayMultimapRetrieval Data StructureListStackQueueDouble-ended queuePriority queueDouble-ended priority queueSetMultisetDisjoint-set |
| Arrays | Bit arrayCircular bufferDynamic arrayHash tableHashed array treeSparse matrix |
| Linked | Association listLinked listSkip listUnrolled linked listXOR linked list |
| Trees | B-treeBinary search treeAA treeAVL treeRed–black treeSelf-balancing treeSplay treeHeapBinary heapBinomial heapFibonacci heapR-treeR* treeR+ treeHilbert R-treeRopeTrieHash tree |
| Graphs | Binary decision diagramDirected acyclic graphDirected acyclic word graph |
| List of data structures |