---
source: sources/wiki-Database_index.md
source_url: https://en.wikipedia.org/wiki/Database_index
---

## Database Indexes: Structure, Types, and Query Optimization

A database index is a data structure that improves the speed of data retrieval operations on a database table at the cost of additional writes and storage space. Indexes allow the database to locate data without scanning every row, providing the basis for rapid random lookups and efficient ordered access. This page covers index architecture (clustered vs. non-clustered), column ordering in composite indexes, index types (bitmap, dense, sparse, inverted, etc.), covering indexes, and the trade-offs between read performance and write overhead.

## Key Concepts

- **Index fundamentals**: An index is a copy of selected columns with a key/pointer back to the original row, enabling sub-linear time lookup instead of O(N) full table scans
- **Clustered index**: Reorders the physical data rows to match the index order; only one per table; best for sequential access and range queries
- **Non-clustered index**: Maintains a separate structure with pointers to data rows; physical row order is independent of index order; multiple allowed per table
- **Cluster (multi-table)**: Stores records from multiple tables sharing a cluster key value together in the same or nearby data blocks, reducing I/O for joins
- **Composite index column order**: Only the leftmost prefix of columns in a composite index can be used efficiently; searching on non-leading columns requires scanning
- **Covering index**: An index that contains all columns needed by a query, eliminating the need to read the base table row — dramatically speeds up reads but increases index size
- **INCLUDE columns**: Non-key fields stored only at the leaf level of an index, enabling covering behavior with smaller overall index size
- **Sargability**: A WHERE clause is sargable if the database can use an index to accelerate it; leading wildcards (`LIKE '%value'`) are not sargable on standard indexes
- **Expression indexes**: Indexes built on functions or expressions (e.g., `upper(last_name)`, `reverse(email_address)`) to support transformed lookups
- **Partial indexes**: Indexes created only for rows satisfying a conditional expression, reducing index size and maintenance cost
- **Index trade-off**: Indexes speed reads but slow writes (INSERT, UPDATE, DELETE) due to maintenance overhead

## Commands and Syntax

- **Standard index creation** (vendor-specific, no ISO SQL standard for indexes):
  ```sql
  CREATE INDEX my_index ON my_table (column1, column2);
  ```
- **Covering index with INCLUDE** (PostgreSQL, SQL Server):
  ```sql
  CREATE INDEX my_index ON my_table (id) INCLUDE (name);
  ```
- **Expression index** (e.g., for case-insensitive search):
  ```sql
  CREATE INDEX idx_upper_lastname ON people (upper(last_name));
  ```
- **Reverse expression index** (to handle leading-wildcard searches):
  ```sql
  CREATE INDEX idx_rev_email ON customers (reverse(email_address));
  SELECT email_address FROM customers
    WHERE reverse(email_address) LIKE reverse('%@wikipedia.org');
  ```
- **Trigram / GIN index** (PostgreSQL, for substring search):
  Splits text into trigrams and stores in a Generalized Inverted Index, reducing `%value%` lookups from O(N) to approximately O(log N)

## Relationships

- **B-tree / B+ tree**: The most common underlying data structure for indexes; provides O(log N) lookup
- **Hash tables**: Alternative index implementation offering O(1) lookup for equality queries but not range queries
- **Bitmap indexes**: Optimized for low-cardinality columns; use bitwise operations for combining conditions
- **Inverted indexes**: Map content words to documents; foundational for full-text search and search engine indexing
- **Concurrency control**: Indexes require specialized concurrency control (index locking) since they are accessed by multiple transactions simultaneously
- **Constraint enforcement**: Indexes underpin UNIQUE, PRIMARY KEY, FOREIGN KEY, and EXCLUSION constraints
- **Query optimizer**: Decides whether to use an index or perform a full table scan based on selectivity, statistics, and query structure
- **Normalization and schema design**: Index strategy is tightly coupled to table structure and access patterns

## Exam-Relevant Points

- **Only one clustered index per table** because it defines the physical row order; multiple non-clustered indexes are allowed
- **Composite index column order matters**: the index on (city, last_name, first_name) can efficiently search by city alone or city+last_name, but NOT by last_name alone — the leftmost prefix rule
- **Leading wildcards defeat index usage**: `LIKE '%value'` forces a full scan; workaround is a reverse expression index
- **Dense index** has an entry for every record; **sparse index** has an entry for every block — sparse requires data to be sorted
- **Covering index** eliminates table lookups entirely when the index contains all queried columns
- **INCLUDE clause** adds non-key columns at the leaf level only, enabling covering without enlarging the index key
- **Bitmap indexes** are optimal for low-cardinality columns (few distinct values); B-trees are better for high cardinality
- **Indexes enforce constraints**: PRIMARY KEY and UNIQUE constraints implicitly create indexes; FOREIGN KEY constraints often require indexes on both sides for performance
- **No ISO SQL standard for CREATE INDEX** — syntax is vendor-specific
- **Index maintenance cost**: every INSERT/UPDATE/DELETE must update all affected indexes, so over-indexing degrades write performance
- **In SQL Server**, clustered index leaf nodes contain the actual data rows, not pointers; non-clustered index leaf nodes contain pointers
- **Partial indexes** reduce storage and maintenance by indexing only rows matching a predicate
- **Reverse-key indexes** help with monotonically increasing values (e.g., sequences) by distributing entries more evenly across the index structure
