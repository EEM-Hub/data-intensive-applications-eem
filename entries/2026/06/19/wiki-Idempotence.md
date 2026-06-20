---
source: sources/wiki-Idempotence.md
source_url: https://en.wikipedia.org/wiki/Idempotence
---

## Idempotence: Property of Operations in Mathematics and Computer Science

Idempotence is the property of certain operations whereby they can be applied multiple times without changing the result beyond the initial application. The term comes from Latin *idem* (same) + *potence* (power), introduced by Benjamin Peirce in 1870. The concept spans abstract algebra, functional programming, distributed systems, and HTTP protocol design, making it foundational for both theoretical computer science and practical system design.

## Key Concepts

- **Formal definition**: An element *x* is idempotent under binary operator · if x·x = x. A binary operation is idempotent if this holds for all elements in the set.
- **Idempotent function**: A function f where f(f(x)) = f(x) for all x — every output is a fixed point of f. Examples: absolute value, floor, ceiling, identity, constant functions.
- **In imperative programming**: A subroutine with side effects is idempotent if multiple calls produce the same system state as a single call.
- **In functional programming**: A pure function is idempotent if it satisfies the mathematical definition (f∘f = f).
- **Idempotence is NOT closed under sequential composition**: A sequence of individually idempotent operations may not itself be idempotent if later operations affect values earlier operations depend on.
- **Neither idempotence nor non-idempotence is preserved under function composition**: Two idempotent functions composed may not be idempotent; two non-idempotent functions composed may be idempotent.
- **Nullipotent**: A stronger property — the operation has no side effects at all (e.g., GET requests).
- **Splitting idempotents**: In category theory, an idempotent morphism f = h∘g "splits" if g∘h = id. A category where every idempotent splits is called idempotent complete.

## Commands and Syntax

No CLI commands per se, but critical protocol-level rules:

- **HTTP methods and idempotence**:
  - `GET` — idempotent and safe (nullipotent); retrieves state without modification
  - `PUT` — idempotent; updates resource state to a specified value (assignment semantics)
  - `DELETE` — idempotent; removes a uniquely identified resource
  - `POST` — NOT required to be idempotent; typically creates new resources with server-generated identifiers

- **C example showing non-idempotent composition**:
  ```c
  int x = 3;
  void inspect() { printf("%d\n", x); }
  void change() { x = 5; }
  void sequence() { inspect(); change(); inspect(); }
  // First call: prints 3, 5. Second call: prints 5, 5. Not idempotent.
  ```

- **Counting idempotent functions**: On a set of n elements, the number of idempotent functions is Σ(k=0 to n) C(n,k) · k^(n-k) — sequence A000248 in OEIS (1, 1, 3, 10, 41, 196, 1057, ...).

## Relationships

- **Distributed systems & event processing**: Idempotence enables safe retries and at-least-once delivery semantics — a message/event processed multiple times yields the same outcome.
- **Service-oriented architecture (SOA)**: Orchestration flows composed entirely of idempotent steps can be safely replayed on failure.
- **Load-store architectures**: Idempotent instructions simplify page fault recovery — the OS can simply re-execute a faulted instruction after loading the page.
- **Resumable operations**: File transfers, rsync, package managers, and build systems leverage idempotence to resume interrupted processes efficiently.
- **Abstract algebra**: Connected to projectors, closure operators, Boolean rings, tropical semirings, GCD/LCM operations, and idempotent matrices (determinant is 0 or 1).
- **Category theory**: Idempotent morphisms and idempotent-complete categories (e.g., Set).
- **Referential transparency**: In functional programming, idempotence relates to but is distinct from referential transparency and pure functions.

## Exam-Relevant Points

- **GET, PUT, DELETE are idempotent; POST is not** — this is the most commonly tested fact about HTTP idempotence.
- **Idempotence ≠ safety**: Safe methods (GET) have no side effects; idempotent methods (PUT, DELETE) may have side effects on first call but repeated calls don't change outcome further.
- **Unique identification is required** for PUT/DELETE idempotence — requests targeting "the most recent record" rather than a specific ID break idempotence.
- **Sequential composition of idempotent operations is NOT necessarily idempotent** — a classic exam trap.
- **In a group, the only idempotent element is the identity** — provable by left-multiplying x·x = x by x⁻¹.
- **Set union and set intersection are idempotent operations** (x∪x = x, x∩x = x).
- **Logical AND and OR are idempotent**; logical NOT is not.
- **An idempotent matrix has determinant 0 or 1**; if determinant is 1, it must be the identity matrix.
- **In natural numbers**: under multiplication, only 0 and 1 are idempotent; under addition, only 0 is idempotent.
- **Practical system design implication**: Idempotent operations can be retried without tracking whether they were already performed, which is critical for fault tolerance in distributed systems.
