---
source: sources/wiki-Array_data_structure.md
source_url: https://en.wikipedia.org/wiki/Array_data_structure
---

## Array Data Structure: Memory Layout and Addressing

An array is a data structure that stores a fixed-size collection of same-type elements in contiguous memory, where each element's address is computable from its index via a linear formula. This page covers the byte-level layout of arrays (not the abstract data type), including addressing formulas for one-dimensional and multidimensional arrays, memory layout strategies (row-major vs. column-major), and performance characteristics compared to other data structures.

## Key Concepts

- An array stores elements of **uniform size** so that any element's memory address can be calculated from its index in constant time: `address = B + c * i` (base address + stride * index)
- The **base address** (also called foundation or first address) is the memory address of the first element
- **Dope vector** (descriptor/stride vector): a record packing dimension, base address, and per-dimension increments — serves as a complete handle for the array and enables efficient slicing operations
- **Row-major order** (C, C++): elements of each row are contiguous in memory; the last index varies fastest
- **Column-major order** (Fortran): elements of each column are contiguous; the first index varies fastest
- **Dimension** (rank) of an array = number of indices needed to select an element — not the total number of elements
- **Iliffe vector**: alternative to true multidimensional arrays — uses an array of pointers to sub-arrays, enabling jagged arrays where rows can differ in size
- **Packed arrays**: multiple elements stored in a single machine word (e.g., bit arrays where one octet holds 8 boolean values)
- Static arrays have fixed size at creation; **dynamic arrays** allow growth by allocating a new backing array and copying, achieving amortized O(1) insertion at the end
- **Spatial locality**: sequential array iteration is fast because successive elements occupy consecutive cache lines — scanning requires only ceil(nk/B) cache misses

## Commands and Syntax

```c
// One-dimensional array declaration (C)
int a[10];    // 10 integers, indices 0–9
a[0];         // first element (zero-based)
a[9];         // last element

// Two-dimensional array (C)
int a[2][3];  // 2 rows, 3 columns — stored row-major: a[0][0], a[0][1], a[0][2], a[1][0], ...

// Element access for 2D array (zero-based)
A[1][3]       // row 2, column 4
```

**Addressing formulas:**
- 1D: `address = B + c * i`
- 2D: `address = B + c * i + d * j`
- kD: `address = B + c1*i1 + c2*i2 + ... + ck*ik` (requires k multiplications + k additions)

## Relationships

- **Dynamic arrays**: extend static arrays with insert/delete; amortized O(1) append but O(n) extra space
- **Hash tables, linked lists, search trees**: alternative implementations of the array data type in some languages
- **Lists, heaps, stacks, queues, deques, strings**: often implemented on top of arrays (implicit data structures)
- **Associative arrays** (Patricia tries, Judy arrays, van Emde Boas trees): efficient when index values are sparse
- **Locality of reference / cache behavior**: arrays exploit spatial locality; choosing row-major vs. column-major layout should match the algorithm's access pattern (e.g., for matrix multiply A·B, store A row-major and B column-major)
- **Bit arrays**: extreme case of packed arrays, one bit per element

## Exam-Relevant Points

- Array element access (read/write) is **O(1)** — constant time in the worst case
- Arrays use **O(n) space with zero per-element overhead** (unlike linked lists)
- **Indexing conventions**: zero-based (C, Java, Lisp), one-based (Fortran 77, Lua), n-based (Pascal, Algol)
- Row-major vs. column-major determines cache performance for multidimensional traversal — iterating against the storage order causes cache thrashing
- Comparison table: arrays have O(1) access but no insert/delete; linked lists have O(1) insert/delete at known position but O(n) access; dynamic arrays have O(1) amortized append but O(n) insert at beginning; balanced trees have O(log n) for all operations
- **Hashed array trees** achieve O(1) amortized append with only O(sqrt(n)) excess space — better than dynamic arrays' O(n)
- **John von Neumann** wrote the first array-sorting program (merge sort) in 1945 for EDVAC
- A k-dimensional addressing formula uses k multiplications and k additions; if any coefficient is a power of 2, the multiplication can be replaced by a **bit shift**
- Dynamic arrays that track a count without reallocating (fixed capacity) are exemplified by **Pascal strings**
