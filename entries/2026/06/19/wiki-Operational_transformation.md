---
source: sources/wiki-Operational_transformation.md
source_url: https://en.wikipedia.org/wiki/Operational_transformation
---

## Operational Transformation: Concurrency Control for Collaborative Editing

Operational Transformation (OT) is a concurrency control technique for real-time collaborative editing systems. It allows multiple users to simultaneously edit shared documents by transforming operations to account for the effects of concurrent changes, ensuring all replicas converge to the same state. Invented in 1989, OT became the core technology behind Google Docs and Google Wave.

## Key Concepts

- **Replicated document storage**: each client holds a full local copy and edits it without locks or blocking, then propagates changes to other clients
- **Transformation**: when a remote operation arrives, it is transformed against locally-executed concurrent operations so its effect remains correct despite changed document state
- **Inclusion Transformation (IT / forward)**: adjusts an operation to *include* the effect of another operation (e.g., shift insertion position right after a prior insert)
- **Exclusion Transformation (ET / backward)**: adjusts an operation to *exclude* the effect of another operation (reverses the positional shift)
- **Consistency models** (increasingly formal):
  - **CC model** (1989): Causality preservation + Convergence
  - **CCI model**: adds Intention preservation — the effect of an operation must match the user's intent regardless of execution order; not achievable by serialization alone
  - **CSM model**: formalizes intention preservation into Single-operation effects + Multi-operation effects (requires total object ordering)
  - **CA model**: Causality + Admissibility — no invocation may violate previously established ordering relations; implies convergence without requiring total order
- **Causality preservation**: causally dependent operations execute in cause-effect order; tracked via vector clocks / state vectors
- **Convergence**: all replicas reach identical state at quiescence
- **Intention preservation**: an operation's effect matches what the user intended when they generated it, even after transformation
- **OT system layering**: control algorithm (determines *which* operations to transform and in what order) sits above transformation functions (determines *how* to transform a pair of operations given their types and parameters)
- **Transformation properties**:
  - **TP1/CP1**: applying op1 then transformed-op2 yields same state as op2 then transformed-op1 (required when operations can execute in different orders)
  - **TP2/CP2**: transforming op3 against two equivalent operation sequences yields the same result (required when IT happens in different document states)
  - **IP1, IP2, IP3**: inverse properties for correct group undo behavior

## Commands and Syntax

**Basic text OT example** — string "abc" with concurrent operations:
```
O1 = Insert[0, "x"]   -- insert "x" at position 0
O2 = Delete[2, "c"]   -- delete "c" at position 2

-- After O1 executes: "abc" → "xabc"
-- O2 must transform: Delete[2,"c"] → Delete[3,"c"] (position shifts +1)
-- Result: "xab" (correct)
```

**Inclusion transformation function** (insert vs insert):
```
func T(ins(p1, c1, sid1), ins(p2, c2, sid2)):
  if (p1 < p2)
    return ins(p1, c1, sid1)
  else if (p1 = p2 and sid1 < sid2)
    return ins(p1, c1, sid1)       // site ID breaks ties
  else
    return ins(p1+1, c1, sid1)     // shift right
```

**Exclusion transformation function** (reverse of above):
```
func T⁻¹(ins(p1, c1, sid1), ins(p2, sid2)):
  if (p1 < p2)
    return ins(p1, c1, sid1)
  else if (p1 = p2 and sid1 < sid2)
    return ins(p1, c1, sid1)
  else
    return ins(p1−1, c1, sid1)     // shift left
```

**Operation models**:
- Generic model: transform three primitives (insert, delete, update) — reusable across apps
- Application-specific model: transform each pair of app operations — requires m x m functions for m operation types

## Relationships

- **Vector clocks / state vectors**: used to track causality and detect concurrency between operations
- **CRDTs (Conflict-free Replicated Data Types)**: alternative approach to the same problem — OT transforms operations, CRDTs design data structures that merge automatically; both target eventual consistency
- **Google Docs / Google Wave**: production systems built on OT (adopted 2009)
- **Lamport's happened-before relation**: formal foundation for the causality ordering that OT preserves
- **Distributed computing**: OT is a specialized concurrency control technique for replicated state in distributed systems
- **CSCW (Computer Supported Cooperative Work)**: the research community where OT originated and evolved
- **Collaborative editing data models**: OT data models range from single linear address space (plain text) to hierarchical multi-level addressing (XML/HTML, structured documents)

## Exam-Relevant Points

- OT operates on **replicated copies** with **lock-free, non-blocking** local execution — optimized for high-latency environments like the web
- The fundamental mechanism: **transform remote operations against locally-executed concurrent operations** before applying them
- **Intention preservation cannot be achieved by serialization** — this is OT's key differentiator from simple locking or serialization protocols
- **TP1 is needed** when operations can execute in different orders; **TP2 is needed** when operations can be transformed in different document states
- The **CC → CCI → CSM → CA** progression represents increasing formalization: CA achieves convergence without requiring total object ordering, reducing algorithmic complexity
- OT systems separate into **control algorithms** (which ops to transform, in what order) and **transformation functions** (how to transform a specific pair) — this separation allows generic algorithms to work across different application domains
- **Site identifiers (sid)** break ties when concurrent insertions target the same position
- For m operation types with application-specific OT, you need **m x m** transformation functions
- The **GROVE system** (Ellis & Gibbs, 1989) was the first OT implementation
