---
source: https://en.wikipedia.org/wiki/External_sorting
fetched: 2026-06-19
---

Class of sorting algorithms that can handle massive amounts of data [![](//upload.wikimedia.org/wikipedia/commons/thumb/a/ad/External_sorting_algorithm.png/250px-External_sorting_algorithm.png)](./File:External_sorting_algorithm.png)External implementation of the [merge sort](./Merge_sort) algorithm. 

**External sorting** is a class of [sorting algorithms](./Sorting_algorithm) that can handle massive amounts of [data](./Data). External sorting is required when the data being sorted do not fit into the [main memory](./Main_memory) of a computing device (usually [RAM](./RAM)) and instead they must reside in the slower [external memory](./Auxiliary_memory), usually a [disk drive](./Disk_drive). Thus, external sorting algorithms are [external memory algorithms](./External_memory_algorithm) and thus applicable in the [external memory](./External_memory_model) [model of computation](./Model_of_computation).

 

External sorting algorithms generally fall into two types, distribution sorting, which resembles [quicksort](./Quicksort), and external merge sort, which resembles [merge sort](./Merge_sort). External merge sort typically uses a [hybrid](./Hybrid_algorithm) sort-merge strategy.  In the sorting phase, chunks of data small enough to fit in main memory are read, sorted, and written out to a temporary file.  In the merge phase, the sorted subfiles are combined into a single larger file.

 

## Model

 See also: [External memory model](./External_memory_model) 

External sorting algorithms can be analyzed in the [external memory model](./External_memory_model). In this model, a [cache](./Cache_(computing)) or internal memory of size M and an unbounded external memory are divided into [blocks](./Blocking_(data_storage)) of size B, and the [running time](./Running_time) of an algorithm is determined by the number of memory transfers between internal and external memory. Like their [cache-oblivious](./Cache-oblivious_algorithm) counterparts, [asymptotically optimal](./Asymptotically_optimal) external sorting algorithms achieve a [running time](./Running_time) (in [Big O notation](./Big_O_notation)) of     O  (     N B     log    M B     ⁡ ⁡     N B     )    {\displaystyle O\left({\tfrac {N}{B}}\log _{\tfrac {M}{B}}{\tfrac {N}{B}}\right)}  ![{\displaystyle O\left({\tfrac {N}{B}}\log _{\tfrac {M}{B}}{\tfrac {N}{B}}\right)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/496ff85a291f2a81b89ac3b14929c774ad5c0035).

 

## External merge sort

 

One example of external sorting is the external [merge sort](./Merge_sort) algorithm, which uses a [K-way merge algorithm](./K-way_merge_algorithm). It sorts chunks that each fit in RAM, then merges the sorted chunks together.[[1]](./External_sorting#cite_note-1)[[2]](./External_sorting#cite_note-2)

 

The algorithm first sorts M items at a time and puts the sorted lists back into external memory. It does a [       M B      {\displaystyle {\tfrac {M}{B}}}  ![{\displaystyle {\tfrac {M}{B}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/860c96a1698eb35072253cf373ad394015efe974)-way merge](./K-way_merge_algorithm) on those sorted lists, [recursing](./Recursion) if there is not enough main memory to merge efficiently in one pass. During a merge pass, B elements from each sorted list are in internal memory, and the minimum is repeatedly outputted.

 

For example, for sorting 900 [megabytes](./Megabyte) of data using only 100 megabytes of RAM:

 
1. Read 100 MB of the data in main memory and sort by some conventional method, like [quicksort](./Quicksort).
2. Write the sorted data to disk.
3. Repeat steps 1 and 2 until all of the data is in sorted 100 MB chunks (there are 900MB / 100MB = 9 chunks), which now need to be merged into one single output file.
4. Read the first 10 MB (= 100MB / (9 chunks + 1)) of each sorted chunk into input buffers in main memory and allocate the remaining 10 MB for an output buffer.  (In practice, it might provide better performance to make the output buffer larger and the input buffers slightly smaller.)
5. Perform a [9-way merge](./K-way_merging) and store the result in the output buffer. Whenever the output buffer fills, write it to the final sorted file and empty it. Whenever any of the 9 input buffers empties, fill it with the next 10 MB of its associated 100 MB sorted chunk until no more data from the chunk is available.

 

The merge pass is key to making external merge sort work externally. The merge algorithm only makes one pass through each chunk, so chunks do not have to be loaded all at once; rather, sequential parts of the chunk are loaded as needed. And as long as the blocks read are relatively large (like the 10 MB in this example), the reads can be relatively efficient even on media with low random-read performance, like hard drives.

 

Historically, instead of a sort, sometimes a replacement-selection algorithm[[3]](./External_sorting#cite_note-3) was used to perform the initial distribution, to produce on average half as many output chunks of double the length.

 

### Additional passes

 

The previous example is a two-pass sort: first sort, then merge. The sort ends with a single *k*-way merge, rather than a series of two-way merge passes as in a typical in-memory merge sort. This is because each merge pass reads and writes *every value* from and to disk, so reducing the number of passes more than compensates for the additional cost of a *k*-way merge.

 

The limitation to single-pass merging is that as the number of chunks increases, memory will be divided into more buffers, so each buffer is smaller. Eventually, the reads become so small that more time is spent on [disk seeks](./Disk_seek) than data transfer.  A typical magnetic [hard disk drive](./Hard_disk_drive) might have a 10 ms access time and 100 MB/s data transfer rate, so each seek takes as much time as transferring 1 MB of data.

 

Thus, for sorting, say, 50 GB in 100 MB of RAM, using a single 500-way merge pass isn't efficient: we can only read 100 MB / 501 ≈ 200 KB from each chunk at once, so 5/6 of the disk's time is spent seeking.  Using two merge passes solves the problem.  Then the sorting process might look like this:

 
1. Run the initial chunk-sorting pass as before to create 500×100 MB sorted chunks.
2. Run a first merge pass combining 25×100 MB chunks at a time, resulting in 20×2.5 GB sorted chunks.
3. Run a second merge pass to merge the 20×2.5 GB sorted chunks into a single 50 GB sorted result

 

Although this requires an additional pass over the data, each read is now 4 MB long, so only 1/5 of the disk's time is spent seeking.  The improvement in data transfer efficiency during the merge passes (16.6% to 80% is almost a 5× improvement) more than makes up for the doubled number of merge passes.

 

Variations include using an intermediate medium like [solid-state disk](./Solid-state_disk) for some stages; the fast temporary storage needn't be big enough to hold the whole dataset, just substantially larger than available main memory. Repeating the example above with 1 GB of temporary SSD storage, the first pass could merge 10×100 MB sorted chunks read from that temporary space to write 50x1 GB sorted chunks to HDD. The high bandwidth and random-read throughput of SSDs help speed the first pass, and the HDD reads for the second pass can then be 2 MB, large enough that seeks will not take up most of the read time. SSDs can also be used as read buffers in a merge phase, allowing fewer larger reads (20MB reads in this example) from HDD storage. Given the lower cost of SSD capacity relative to RAM, SSDs can be an economical tool for sorting large inputs with very limited memory.

 

Like in-memory sorts, efficient external sorts require [O](./Big_O_notation)(*n* log *n*) time: exponentially growing datasets require linearly increasing numbers of passes that each take O(n) time.[[4]](./External_sorting#cite_note-4) Under reasonable assumptions at least 500 GB of data stored on a hard drive can be sorted using 1 GB of main memory before a third pass becomes advantageous, and many times that much data can be sorted before a fourth pass becomes useful.[[5]](./External_sorting#cite_note-5)

 

Main memory size is important. Doubling memory dedicated to sorting halves the number of chunks *and* the number of reads per chunk, reducing the number of seeks required by about three-quarters. The ratio of RAM to disk storage on servers often makes it convenient to do huge sorts on a cluster of machines[[6]](./External_sorting#cite_note-6) rather than on one machine with multiple passes. Media with high random-read performance like [solid-state drives](./Solid-state_drive) (SSDs) also increase the amount that can be sorted before additional passes improve performance.

 

## External distribution sort

 

External distribution sort is analogous to [quicksort](./Quicksort). The algorithm finds approximately        M B      {\displaystyle {\tfrac {M}{B}}}  ![{\displaystyle {\tfrac {M}{B}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/860c96a1698eb35072253cf373ad394015efe974) pivots and uses them to divide the N elements into approximately equally sized subarrays, each of whose elements are all smaller than the next, and then recurse until the sizes of the subarrays are less than the [block size](./Blocking_(data_storage)). When the subarrays are less than the block size, sorting can be done quickly because all reads and writes are done in the [cache](./Cache_(computing)), and in the [external memory model](./External_memory_model) requires     O ( 1 )   {\displaystyle O(1)}  ![{\displaystyle O(1)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e66384bc40452c5452f33563fe0e27e803b0cc21) operations.

 

However, finding exactly        M B      {\displaystyle {\tfrac {M}{B}}}  ![{\displaystyle {\tfrac {M}{B}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/860c96a1698eb35072253cf373ad394015efe974) pivots would not be fast enough to make the external distribution sort [asymptotically optimal](./Asymptotically_optimal). Instead, we find slightly fewer pivots. To find these pivots, the algorithm splits the N input elements into        N M      {\displaystyle {\tfrac {N}{M}}}  ![{\displaystyle {\tfrac {N}{M}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b5d5ee01c2981ba95017bd5bdb588cb2316ca3e3) chunks, and takes every         M  16 B        {\displaystyle {\sqrt {\tfrac {M}{16B}}}}  ![{\displaystyle {\sqrt {\tfrac {M}{16B}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/224e39237bb73c547dcdd5569ceb993dd36bc062) elements, and [recursively](./Recursion) uses the [median of medians](./Median_of_medians) algorithm to find         M B       {\displaystyle {\sqrt {\tfrac {M}{B}}}}  ![{\displaystyle {\sqrt {\tfrac {M}{B}}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d831ae852c648eaefbe9c1336a15bdb6cc2d8ef1) pivots.[[7]](./External_sorting#cite_note-Aggarwal88-7)

 

There is a [duality](./Duality_(mathematics)), or fundamental similarity, between merge- and distribution-based algorithms.[[8]](./External_sorting#cite_note-8)

 

## Performance

 

The Sort Benchmark, created by [computer scientist](./Computer_scientist) [Jim Gray](./Jim_Gray_(computer_scientist)), compares external sorting algorithms implemented using finely tuned hardware and software.  Winning implementations use several techniques:

 
- **Using parallelism** 
- Multiple disk drives can be used in parallel in order to improve sequential read and write speed.  This can be a very cost-efficient improvement: a Sort Benchmark winner in the cost-centric Penny Sort category uses six hard drives in an otherwise midrange machine.[[9]](./External_sorting#cite_note-9)
- Sorting software can use [multiple threads](./Thread_(computer_science)), to speed up the process on modern multicore computers.
- Software can use [asynchronous I/O](./Asynchronous_I/O) so that one run of data can be sorted or merged while other runs are being read from or written to disk.
- Multiple machines connected by fast network links can each sort part of a huge dataset in parallel.[[10]](./External_sorting#cite_note-10)

- **Increasing hardware speed** 
- Using more RAM for sorting can reduce the number of disk seeks and avoid the need for more passes.
- Fast external memory like [solid-state drives](./Solid-state_drives) can speed sorts, either if the data is small enough to fit entirely on SSDs or, more rarely, to accelerate sorting SSD-sized chunks in a three-pass sort.
- *Many* other factors can affect hardware's maximum sorting speed: CPU speed and number of cores, RAM access latency, input/output bandwidth, disk read/write speed, disk seek time, and others. "Balancing" the hardware to minimize bottlenecks is an important part of designing an efficient sorting system.
- Cost-efficiency as well as absolute speed can be critical, especially in cluster environments where lower node costs allow purchasing more nodes.

- **Increasing software speed** 
- Some Sort Benchmark entrants use a variation on [radix sort](./Radix_sort) for the first phase of sorting: they separate data into one of many "bins" based on the beginning of its value.  Sort Benchmark data is random and especially well-suited to this optimization.
- Compacting the input, intermediate files, and output can reduce time spent on I/O, but is not allowed in the Sort Benchmark.
- Because the Sort Benchmark sorts long (100-byte) records using short (10-byte) keys, sorting software sometimes rearranges the keys separately from the values to reduce memory I/O volume.

 

## See also

 
- [Mainframe sort merge](./Mainframe_sort_merge)
- [External memory algorithm](./External_memory_algorithm)
- [Funnelsort](./Funnelsort)
- [Cache-oblivious distribution sort](./Cache-oblivious_distribution_sort)

 

## References

 
1. [↑](./External_sorting#cite_ref-1) [Donald Knuth](./Donald_Knuth), *[The Art of Computer Programming](./The_Art_of_Computer_Programming)*, Volume 3: *Sorting and Searching*, Second Edition. Addison-Wesley, 1998, [ISBN](./ISBN_(identifier)) [0-201-89685-0](./Special:BookSources/0-201-89685-0), Section 5.4: External Sorting, pp.248–379.
2. [↑](./External_sorting#cite_ref-2) [Ellis Horowitz](./Ellis_Horowitz) and [Sartaj Sahni](./Sartaj_Sahni), *Fundamentals of Data Structures*, H. Freeman & Co., [ISBN](./ISBN_(identifier)) [0-7167-8042-9](./Special:BookSources/0-7167-8042-9).
3. [↑](./External_sorting#cite_ref-3) [Donald Knuth](./Donald_Knuth), *The Art of Computer Programming*, Volume 3: *Sorting and Searching*, Second Edition. Addison-Wesley, 1998, [ISBN](./ISBN_(identifier)) [0-201-89685-0](./Special:BookSources/0-201-89685-0), Section 5.4: External Sorting, pp.254–ff.
4. [↑](./External_sorting#cite_ref-4) One way to see this is that given a fixed amount of memory (say, 1GB) and a minimum read size (say, 2MB), each merge pass can merge a certain number of runs (such as 500) into one, creating a divide-and-conquer situation similar to in-memory merge sort. The size of each main-memory sort and number of ways in each merge have a constant upper bound, so they don't contribute to the big-O.
5. [↑](./External_sorting#cite_ref-5) For an example, assume 500 GB of data to sort, 1 GB of buffer memory, and a single disk with 200 MB/s transfer rate and 20 ms seek time.  A single 500-way merging phase will use buffers of 2 MB each, and need to do 250 K seeks while reading then writing 500 GB. It will spend 5,000 seconds seeking and 5,000 s transferring. Doing two merge passes as described above would nearly eliminate the seek time but add an additional 5,000 s of data transfer time, so this is approximately the break-even point between a two-pass and three-pass sort.
6. [↑](./External_sorting#cite_ref-6) Chris Nyberg, Mehul Shah, [Sort Benchmark Home Page](http://sortbenchmark.org/) (links to examples of parallel sorts)
7. [↑](./External_sorting#cite_ref-Aggarwal88_7-0) Aggarwal, Alok; [Vitter, Jeffrey](./Jeffrey_Vitter) (1988). ["The input/output complexity of sorting and related problems"](https://hal.inria.fr/inria-00075827/file/RR-0725.pdf) (PDF). *[Communications of the ACM](./Communications_of_the_ACM)*. **31** (9): 1116–1127. [doi](./Doi_(identifier)):[10.1145/48529.48535](https://doi.org/10.1145%2F48529.48535).
8. [↑](./External_sorting#cite_ref-8) [J. S. Vitter](./J._S._Vitter), *[Algorithms and Data Structures for External Memory](http://www.ittc.ku.edu/~jsv/Papers/Vit.IO_book.pdf)*, Series on Foundations and Trends in Theoretical Computer Science, now Publishers, Hanover, MA, 2008, [ISBN](./ISBN_(identifier)) [978-1-60198-106-6](./Special:BookSources/978-1-60198-106-6).
9. [↑](./External_sorting#cite_ref-9) Nikolas Askitis, [OzSort 2.0: Sorting up to 252GB for a Penny](http://sortbenchmark.org/ozsort-2010.pdf)
10. [↑](./External_sorting#cite_ref-10) Rasmussen et al., [TritonSort](http://sortbenchmark.org/tritonsort_2010_May_15.pdf)

 

## External links

 
- [STXXL, an algorithm toolkit including external mergesort](https://stxxl.sourceforge.net/)
- [An external mergesort example](http://cis.stvincent.edu/html/tutorials/swd/extsort/extsort.html)
- [A K-Way Merge Implementation](https://code.google.com/p/kway)
- [External-Memory Sorting in Java](https://code.google.com/p/externalsortinginjava/)
- [A sample pennysort implementation using Judy Arrays](https://code.google.com/p/judyarray)
- [Sort Benchmark](http://sortbenchmark.org/)

   
- [External Sorting in C#](https://ysemenenko.github.io/external-sorting/)
-