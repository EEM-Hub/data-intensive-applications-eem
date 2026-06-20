---
source: sources/wiki-Associative_array.md
source_url: https://en.wikipedia.org/wiki/Associative_array
---

## Associative Arrays: The Dictionary Problem and Its Implementations

An associative array (also called map, dictionary, symbol table, or key-value store) is an abstract data type that stores key/value pairs where each key appears at most once. It supports three core operations: lookup, insert, and remove. The "dictionary problem" — designing efficient data structures to implement associative arrays — is one of the classic problems in computer science, with hash tables and search trees as the two major solutions.

## Key Concepts

- **Abstract data type**: Mathematically, an associative array is a function with finite domain — it maps keys to values, with each key mapping to at most one value
- **Core operations**: Insert (add/overwrite a mapping), Remove (delete a mapping by key), Lookup (find value by key — may throw exception or return default if absent)
- **The dictionary problem**: The classic CS problem of designing efficient structures for associative arrays; two major solutions are hash tables and search trees
- **Multimap**: Generalization allowing multiple values per key
- **Bidirectional map**: Variant where values are also unique, enabling reverse lookup (value → key)
- **Ordered dictionary** has two meanings: (1) sorted by key (tree-based, e.g., C++ `std::map`), or (2) ordered by insertion (e.g., Python `dict`, Java `LinkedHashMap`)
- **Name origin**: "Associative" refers to the association of values with keys, not the associative property from mathematics

## Commands and Syntax

**Algebraic properties of operations:**
```
lookup(k, insert(j, v, D)) = if k == j then v else lookup(k, D)
lookup(k, new()) = fail
remove(k, insert(j, v, D)) = if k == j then remove(k, D) else insert(j, v, remove(k, D))
remove(k, new()) = new()
```

**JSON/Python literal notation:**
```json
{
    "Pride and Prejudice": "Alice",
    "Wuthering Heights": "Alice",
    "Great Expectations": "John"
}
```

**Performance comparison table:**

| Implementation | Avg Lookup/Remove | Worst Lookup/Remove | Avg Insert | Worst Insert | Ordered |
|---|---|---|---|---|---|
| Hash table | O(1) | O(n) | O(1) | O(n) | No |
| Self-balancing BST | O(log n) | O(log n) | O(log n) | O(log n) | Yes |
| Unbalanced BST | O(log n) | O(n) | O(log n) | O(n) | Yes |
| Association list | O(n) | O(n) | O(1) | O(1) | No |

## Relationships

- **Hash tables**: Primary implementation; uses hash function to map keys to array buckets. Collision strategies: separate chaining (pointer to list) vs. open addressing (probe for empty slot). Open addressing has better cache performance when table is sparse but degrades exponentially as it fills
- **Search trees**: Self-balancing BSTs (AVL, red-black) give O(log n) worst-case and maintain order. Specialized trees (radix trees, tries, Judy arrays, van Emde Boas trees) optimize for specific key types
- **Key-value stores**: The persistent/distributed form of associative arrays — post-2010 renaissance driven by cloud computing needs and object-relational impedance mismatch in RDBMs
- **Serialization**: Standard mechanism for persisting associative arrays to files
- **Content-addressable memory (CAM)**: Hardware-level support for associative lookup
- **Programming patterns**: Enables memoization and the decorator pattern
- **Direct addressing**: Degenerate case — when keyspace is small, store values at `A[k]` directly for O(1) everything, but space = keyspace size

## Exam-Relevant Points

- Hash tables average O(1) for all operations but degrade to O(n) worst case; self-balancing BSTs guarantee O(log n) for all operations
- Open addressing has lower cache miss ratio than separate chaining when table is mostly empty, but degrades exponentially as load increases
- Separate chaining uses less memory unless entries are very small (< 4× pointer size)
- Trees support range queries and ordered traversal; hash tables do not
- Association lists are O(n) for lookup but O(1) for insert — viable only for very small collections
- A hybrid approach (BST-backed buckets in a hash table) gives O(1) average with O(log n) worst case, but adds overhead that hurts small tables
- Language terminology varies: "dictionary" (Python, .NET, Swift), "hash" (Perl, Ruby), "map" (C++, Java, Go, Haskell), "table" (Lua, Maple)
- SNOBOL4 (1969) introduced the first built-in syntactic support for associative arrays; AWK was the first scripting language to follow
- Python dicts and Java LinkedHashMap preserve insertion order; C++ `std::map` preserves sorted key order — these are distinct semantics
