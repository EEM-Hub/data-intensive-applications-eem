---
source: sources/wiki-Watermark_data_synchronization.md
source_url: https://en.wikipedia.org/wiki/Watermark_(data_synchronization)
---

## Watermarks for Data Synchronization (DirSync)

Watermarks provide a reference point enabling incremental/delta synchronization between two systems. Any object created, modified, or deleted after the watermark value is considered "above watermark" and returned to the requesting client. This mechanism avoids full dataset transfers and supports resumable synchronization after pauses or downtime.

## Key Concepts

- **Watermark**: A predefined-format object that marks a point-in-time reference for synchronization between two datasets
- **Above watermark**: Objects created, modified, or deleted after the watermark value — these are the delta to be synced
- **Cookie**: Alternative term for a watermark object; used in LDAP DirSync implementations
- **DirSync control**: An LDAP server extension that uses watermarks to poll a directory partition for changed objects
- **Incremental synchronization**: Only transferring changes since the last known state, rather than the full dataset
- **Resumability**: Watermarks allow a sync job to pick up where it left off after downtime or failure

## Commands and Syntax

No specific CLI commands, but the DirSync protocol flow is:

1. Client sends a DirSync search with an **empty cookie** on first run
2. Server returns all matching objects + an **updated cookie**
3. Client stores the cookie and sends it with the **next search**
4. Server returns only objects changed since that cookie was issued
5. Repeat for each subsequent sync cycle

This is an LDAP control extension — the cookie is passed as part of the LDAP search request/response.

## Relationships

- **Data synchronization**: Watermarks are a core mechanism for implementing incremental sync
- **LDAP / Directory services**: Primary domain where DirSync watermarks are used (Active Directory, iPlanet, CUCM)
- **Change Data Capture (CDC)**: Watermarks are conceptually similar to CDC log sequence numbers or change tokens
- **Event sourcing / replication logs**: Watermarks serve an analogous role to offsets in log-based replication (e.g., Kafka consumer offsets)
- **High-water mark (computer security)**: Related but distinct concept in security classification contexts

## Exam-Relevant Points

- A watermark enables **delta/incremental** sync — not full replication
- The first DirSync query uses an **empty cookie** and returns the **full result set**
- Subsequent queries pass the **previous cookie** and receive only **changes since that cookie**
- Watermarks support **resumability** — a client can restart from its last known watermark after failure
- The terms **watermark** and **cookie** are used interchangeably in DirSync contexts
- DirSync is an **LDAP server extension**, not a standalone protocol
- Products using DirSync watermarks include: Active Directory, Exchange Server, ADAM, MIIS/ILM, Cisco CUCM, iPlanet
