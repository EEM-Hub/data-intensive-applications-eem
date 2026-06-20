---
source: sources/wiki-Abstract_data_type.md
source_url: https://en.wikipedia.org/wiki/Abstract_data_type
---

## Abstract Data Types (ADTs): Mathematical Models for Data Behavior

An abstract data type (ADT) is a mathematical model for data types defined entirely by its behavior — possible values, operations, and constraints on those operations — rather than by its concrete representation. ADTs are a foundational concept in computer science that separates the *what* (user's view) from the *how* (implementer's view), enabling interchangeable implementations behind stable interfaces.

## Key Concepts

- **ADT vs Data Structure**: An ADT defines behavior (semantics) from the user's perspective; a data structure is a concrete representation from the implementer's perspective. A stack ADT can be implemented by a linked list or an array.
- **Formal definition**: An ADT consists of a domain, a collection of operations, and a set of constraints the operations must satisfy — analogous to an algebraic structure in mathematics.
- **Two specification styles**:
  - **Axiomatic semantics** (functional style): Each state is a separate immutable value; operations are pure mathematical functions with no side effects. Constraints are expressed as algebraic laws (e.g., `fetch(store(V,x)) = x`).
  - **Operational semantics** (imperative style): The ADT is a mutable entity with a notion of time; operations change state over time; order of evaluation matters. Constraints are typically specified in prose.
- **Interface vs behavior**: The interface exposes the domain and operations (plus pre/post-conditions), but the behavioral constraints (e.g., LIFO vs FIFO) are what distinguish otherwise similar ADTs like stacks and queues.
- **Aliasing**: In operational semantics, care must be taken to specify that operations on one instance do not affect other instances. The aliasing axiom states that `create()` yields an instance distinct from all existing instances.
- **Complexity guarantees**: Some authors (notably Alexander Stepanov with the C++ STL) argue complexity assertions must be part of the ADT interface, since interchangeable modules must share similar complexity behavior. Others argue ADT specifications should be implementation-independent.
- **History**: First proposed by Barbara Liskov and Stephen Zilles in 1974, during CLU language development. Algebraic specification became nearly synonymous with ADTs around 1980, grounded in universal algebra.

## Commands and Syntax

**Axiomatic specification of an abstract variable:**
```
fetch : V → X
store : V × X → V
fetch(store(V, x)) = x              -- fetch returns most recent store
store(store(V, x1), x2) = store(V, x2)  -- store fully overwrites
```

**Axiomatic specification of an abstract stack:**
```
push : S → X → S
pop  : S → (S, X)
top  : S → X
create : S
empty  : S → Boolean

pop(push(S, v)) = (S, v)       -- pop undoes push
top(push(S, v)) = v            -- top reveals last pushed
empty(create) = true           -- new stack is empty
empty(push(S, x)) = false      -- pushed stack is non-empty
```

**Boom hierarchy** — four data types from three operations (`null`, `single`, `append`):
```
Tree:  append(null, A) = A; append(A, null) = A        (identity)
List:  + associativity: append(append(A,B),C) = append(A,append(B,C))
Bag:   + commutativity: append(B,A) = append(A,B)
Set:   + idempotence: append(A,A) = A
```

**Auxiliary operations** commonly defined on ADTs:
- `create()`, `compare(s, t)`, `hash(s)`, `print(s)` / `show(s)`
- Imperative-style additions: `initialize(s)`, `copy(s, t)`, `clone(t)`, `free(s)` / `destroy(s)`

## Relationships

- **Data structures** are concrete implementations of ADTs (linked lists, arrays, hash tables implement list, stack, map ADTs).
- **Abstract types / opaque data types** in programming languages are implementation mechanisms that approximate ADTs but are not formally equivalent.
- **Information hiding** and **modular programming** use ADT concepts to allow implementation changes without disturbing clients.
- **Object-oriented programming**: Classes serve as ADT implementations; each instance is an object. However, OOP can undermine extensibility when classes (representations) are used as types rather than interfaces (behaviors).
- **Algebraic specification** and **universal algebra** provide the mathematical foundation for ADTs.
- **Design by contract** relates to ADTs through pre-conditions, post-conditions, and invariants.
- **Boom hierarchy** shows how tree, list, bag, and set ADTs form a lattice by progressively adding algebraic laws (associativity, commutativity, idempotence).

## Exam-Relevant Points

- An ADT is defined by its **behavior (semantics)**, not by its implementation — this is the fundamental distinction from data structures.
- **Stack vs Queue**: Both have add/remove interfaces; the constraints (LIFO vs FIFO) are what distinguish them. This illustrates that constraints, not just operations, define an ADT.
- The two formal specification styles: **axiomatic** (functional, pure, order-independent) vs **operational** (imperative, mutable, order-dependent).
- `fetch(store(V, x)) = x` is the canonical axiom for an abstract variable.
- `pop(push(S, v)) = (S, v)` is the canonical axiom for an abstract stack.
- **Stepanov's argument**: Complexity guarantees must be part of the ADT interface for modules to be truly interchangeable.
- ADTs were introduced by **Barbara Liskov and Stephen Zilles (1974)** as part of CLU language development.
- Common ADTs: Collection, List, Set, Multiset (Bag), Map, Stack, Queue, Priority Queue, Graph, Tree.
- **Implementation flexibility**: Multiple concrete data structures can implement the same ADT; code using the ADT interface continues working when the implementation changes.
- The **Boom hierarchy** demonstrates how adding algebraic properties (identity → associativity → commutativity → idempotence) transforms trees into lists, bags, and sets.
- In OOP, using **interfaces as types** (behaviors) rather than classes (representations) is more faithful to ADT principles and better supports extensibility.
