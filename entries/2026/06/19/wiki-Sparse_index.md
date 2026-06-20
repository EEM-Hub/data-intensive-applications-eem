---
source: sources/wiki-Sparse_index.md
source_url: https://en.wikipedia.org/wiki/Sparse_index
---

## Database Indexes: Structure, Types, and Query Optimization

A database index is a data structure that improves the speed of data retrieval operations on a database table at the cost of additional writes and storage space. Indexes allow the database to locate data without scanning every row, providing the basis for rapid random lookups and efficient ordered access. This page covers index architecture (clustered vs. non-clustered), column ordering in composite indexes, index types (bitmap, dense, sparse, inverted, etc.), covering indexes, and the trade-offs between read performance and write overhead.

## Key Concepts

- **Index fundamentals**: An index is a copy of selected columns with a key/pointer back to the original row, enabling sub-linear time lookup instead of O(N) full table scans
- **Clustered index**: Reorders the physical data rows to match the index order; only one per table; best for sequential access and range queries
- **Non-clustered index**: Maintains a separate structure with pointers to data rows; physical row order is independent of index order; multiple allowed per table
- **Cluster (multi-table)**: Stores records from multiple tables sharing a cluster key value together in the same or nearby data blocks, reducing I/O for joins
- **Composite index column order**: Only the leftmost prefix of columns in a composite index can be used efficiently; searching on non-leading columns requires scanning
- **Sargability**: A WHERE clause is sargable if the database can use an index to accelerate it; leading wildcards (`LIKE '%value'`) are not sargable
- **Covering index**: An index that contains all columns needed by a query, eliminating the need to access the base table (index-only scan)
- **Dense index**: One index entry per record in the data file
- **Sparse index**: One index entry per block in the data file (requires sorted/clustered data)
- **Index trade-off**: Indexes speed reads but slow writes (inserts, updates, deletes) and consume additional storage
- **Constraint enforcement**: Indexes are used to police UNIQUE, PRIMARY KEY, FOREIGN KEY, and EXCLUSION constraints

## Commands and Syntax

- **Creating a covering index with included columns**:
  ```sql
  CREATE INDEX my_index ON my_table (id) INCLUDE (name);
  ```
  Non-key fields in INCLUDE are stored only at the leaf level, reducing index size while enabling index-only scans.

- **Expression index** (e.g., PostgreSQL):
  ```sql
  CREATE INDEX idx_upper_name ON people (upper(last_name));
  ```

- **Reverse index trick for trailing wildcard searches**:
  ```sql
  -- Instead of: WHERE email LIKE '%@wikipedia.org' (not sargable)
  SELECT email_address FROM customers
  WHERE reverse(email_address) LIKE reverse('%@wikipedia.org');
  -- Combined with: CREATE INDEX idx_rev_email ON customers (reverse(email_address));
  ```

- **Full-text indexing with trigrams** (e.g., PostgreSQL pg_trgm + GIN):
  Splits text into 3-character chunks stored in a Generalized Inverted Index, reducing `%word%` searches from O(N) to approximately O(log N).

## Relationships

- **B-tree / B+ tree**: The most common index implementation data structure; provides O(log N) lookup
- **Hash index / Linear hashing**: Alternative implementation for equality lookups, potentially O(1)
- **Bitmap index**: Optimized for low-cardinality columns; uses bitwise operations for query processing
- **Inverted index**: Maps content words to documents; foundation of full-text search and search engine indexing
- **Query optimizer**: Decides whether and which index to use for a given query; index design directly affects query plan selection
- **Concurrency control / Index locking**: Specialized locking methods exist for indexes accessed concurrently by multiple transactions
- **Normalization and table design**: Index effectiveness depends on schema design, column selection, and data distribution
- **Transaction processing**: Index maintenance is part of transaction overhead on INSERT/UPDATE/DELETE

## Exam-Relevant Points

- **Only one clustered index per table** — because it defines the physical storage order of rows
- **Multiple non-clustered indexes are allowed** per table
- **Composite index column order matters**: queries can use the leftmost prefix but not skip leading columns efficiently (the phone book analogy: city, last_name, first_name)
- **Leading wildcards prevent index use**: `LIKE '%value'` forces a full scan; this is the definition of a non-sargable predicate
- **Covering indexes avoid table lookups entirely** — the INCLUDE clause adds non-key columns at leaf level without increasing the sort key
- **Dense vs. sparse index**: dense has one entry per record; sparse has one entry per block (sparse requires clustered/sorted data)
- **Bitmap indexes excel on low-cardinality columns** (e.g., gender, boolean flags) where B-trees are inefficient
- **Expression/functional indexes** allow indexing on transformed values (e.g., `upper(last_name)`)
- **Partial indexes** create entries only for rows matching a condition, reducing index size
- **Indexes enforce constraints**: PRIMARY KEY and UNIQUE constraints typically create implicit indexes; FOREIGN KEY columns should be indexed for performance
- **No ISO SQL standard for CREATE INDEX** — index creation syntax is vendor-specific
- **In SQL Server, clustered index leaf nodes contain the actual data**, not just pointers; non-clustered leaf nodes contain pointers
- **Reverse-key indexes** help with monotonically increasing values (e.g., sequences) by distributing entries more evenly across the index structure
