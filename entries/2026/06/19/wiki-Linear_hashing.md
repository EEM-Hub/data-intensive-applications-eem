---
source: sources/wiki-Linear_hashing.md
source_url: https://en.wikipedia.org/wiki/Linear_hashing
---

## Linear Hashing: Dynamic Hash Table Growth

Linear hashing (LH) is a dynamic data structure that implements a hash table capable of growing or shrinking one bucket at a time, avoiding expensive periodic reorganization. Invented by Witold Litwin in 1980, it is the foundational scheme in a family of dynamic hashing algorithms. Unlike extendible hashing which splits only overflowing buckets, linear hashing splits buckets in a predetermined order, decoupling the split decision from which bucket actually overflowed.

## Key Concepts

- **One-bucket-at-a-time growth**: The file expands by splitting a single predetermined bucket into two, and shrinks by merging two predetermined buckets into one.
- **Split pointer (`s`)**: An index tracking which bucket will be split next. It advances sequentially through buckets at each level.
- **Level (`l`)**: Tracks the current round of splits. The number of buckets is `n = 2^l + s`. When `s` reaches `2^l`, the level increments and `s` resets to 0.
- **Two hash functions active at once**: At any time, only `h_l` and `h_{l+1}` are in use. Buckets before the split pointer use `h_{l+1}` (already split); buckets at or after the split pointer use `h_l`.
- **Dynamic hash function family**: Typically `h_i(c) = c mod 2^i`, using the `i` rightmost binary digits of the key.
- **Split triggers**:
  - **Controlled split**: Triggered when the load factor (records/buckets) exceeds a threshold. Overflow is handled via linked overflow blocks.
  - **Uncontrolled split**: Triggered immediately when any bucket overflows.
- **File contraction**: Some implementations merge buckets (undoing the last split) when the load factor drops below a lower threshold.
- **Constant-time operations**: Key-based inserts, deletes, updates, and reads take O(1) time regardless of the number of buckets or records.
- **LH\* (distributed variant)**: Each bucket resides on a different server. Clients maintain an approximate file state and forward requests; at most two forwards occur in a reasonably stable system. Image Adjustment Messages correct client state after forwards.

## Commands and Syntax

**Bucket address calculation:**
```
# l = current level, s = split pointer
a = h_l(c)            # hash with current-level function
if (a < s):            # bucket already split this round
    a = h_{l+1}(c)     # re-hash with next-level function
```

**Split pointer and level update after a split:**
```
s = s + 1
if (s >= 2^l):
    l = l + 1
    s = 0
```

**Hash function formula:**
```
h_i(c) = c mod 2^i
```

**File state relationship:**
```
n = 2^l + s    # total number of buckets
```

## Relationships

- **Extendible hashing**: Splits only overflowing buckets (non-predetermined order); linear hashing splits in predetermined order regardless of which bucket overflowed.
- **Spiral hashing**: Distributes records unevenly so that buckets with highest access costs split first — a contrast to linear hashing's sequential splitting.
- **Consistent hashing**: Another dynamic hashing scheme, but designed for distributed caching/routing rather than file-level storage.
- **Load factor**: The primary metric governing controlled splits; shared concept with general hash table design.
- **Berkeley DB (BDB)**: Real-world adoption — uses a C implementation of linear hashing derived from Litwin's CACM work.
- **Variants**: Linear Hashing with Partial Extensions (Larson), Priority Splitting (Ruchte/Tharp), and Recursive Linear Hashing (Ramamohanarao/Sacks-Davis) all extend the base algorithm.

## Exam-Relevant Points

- Linear hashing grows **one bucket at a time** in a **predetermined order** — this is the key differentiator from extendible hashing.
- The bucket address algorithm requires checking `if (a < s)` to determine whether to use `h_l` or `h_{l+1}` — understanding this two-function scheme is essential.
- The file state is fully captured by just two values: **level `l`** and **split pointer `s`**, with `n = 2^l + s`.
- The split pointer resets to 0 and the level increments when `s >= 2^l`, completing a full round of splits.
- Operations are **O(1)** with respect to the number of records and buckets.
- Controlled splitting uses **load factor thresholds** and allows overflow chains; uncontrolled splitting triggers on any bucket overflow.
- LH\* extends linear hashing to distributed systems with **at most two forwards** per misrouted request, and clients self-correct via **Image Adjustment Messages**.
- The standard hash function family is `h_i(c) = c mod 2^i`, using progressively more bits of the key as the table grows.
