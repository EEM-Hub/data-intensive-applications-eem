---
source: sources/wiki-Schema_evolution.md
source_url: https://en.wikipedia.org/wiki/Schema_evolution
---

## Schema Evolution and Versioning

Schema evolution and schema versioning address the challenge of modifying a database's structure while preserving existing data, application functionality, and query compatibility. This is a fundamental problem in data-intensive systems where schemas inevitably change over time, and the cost of those changes ripples through every query and application that depends on the schema.

## Key Concepts

- **Schema evolution** — the process of altering a database schema while retaining current data and system functionality; affects not just structure but also stored data and all queries/applications against that schema
- **Schema versioning** — maintaining multiple versions of a schema so that historical data remains accessible under the schema it was written with
- **Attribute volatility** — the tendency for schema attributes to change over time; designing for a single "as of now" snapshot ignores this reality
- **Impact amplification** — a single schema evolution step can affect up to 70% of queries operating on that schema, requiring manual rework (demonstrated by the MediaWiki case study)
- **Web/distributed systems intensify the problem** — cooperative, distributed development creates 39–500% more schema change pressure than traditional information systems
- **Temporal databases** are especially affected because they must track data across time under potentially different schema versions
- **Mapping composition and invertibility** — theoretical foundations for transforming queries and data between schema versions; core problems underlying practical schema evolution support

## Commands and Syntax

No standard commands defined. Tools referenced in the literature:

- **PRISM** — supports graceful relational schema evolution by generating migration scripts and rewriting queries across schema versions
- **PRIMA** — extends schema evolution support to transaction-time databases (databases that track when facts were recorded)
- **Pario and deltasql** — development tools providing fully automated schema evolution (version-controlled DDL changes)

## Relationships

- **Temporal databases** — schema versioning is a prerequisite for correct temporal queries; without it, historical queries may return results under the wrong schema
- **Data migration** — schema evolution necessitates data migration strategies (lazy vs. eager, in-place vs. copy)
- **Application coupling** — tight coupling between application queries and schema structure means schema changes cascade into application code; this is the primary practical cost
- **Distributed systems** — decentralized development amplifies schema change frequency, making evolution support critical for web-scale systems
- **Schema mapping** — the theoretical underpinning (mapping composition, invertibility) connects to data integration and ETL problems

## Exam-Relevant Points

- Schema evolution affects three things simultaneously: the schema structure, the stored data, and the queries/applications — not just the DDL
- A single schema change can invalidate up to 70% of dependent queries (MediaWiki benchmark)
- Web and distributed systems experience 39–500% more schema change pressure than traditional systems
- Temporal databases have an especially acute schema evolution problem because they must serve historical data under potentially different schema versions
- The two core theoretical problems are **mapping composition** (chaining transformations between versions) and **mapping invertibility** (reversing a transformation to recover the original view)
- "As of now" schema design — treating the current schema as permanent — is identified as unrealistic for any system retaining historical data
