---
source: sources/wiki-CommandE28093query_separation.md
source_url: https://en.wikipedia.org/wiki/Command%E2%80%93query_separation
---

## Command-Query Separation (CQS) and CQRS

Command-Query Separation is a principle of imperative programming, devised by Bertrand Meyer as part of the Eiffel programming language. It states that every method should either be a **command** (performs an action, modifies state) or a **query** (returns data), but never both. The architectural extension, CQRS, applies this principle at the service/system level by using separate interfaces and data models for reads and writes.

## Key Concepts

- **CQS Principle**: "Asking a question should not change the answer" — methods should either return a value (query) or produce a side effect (command), not both
- **Queries** must be referentially transparent — calling them produces no side effects
- **Commands** perform actions/state changes but do not return values
- **CQRS** generalizes CQS from method-level to architecture-level, using separate read and write models, interfaces, and often separate data stores
- CQS aligns naturally with **Design by Contract (DbC)** — assertions (queries) can be evaluated without altering program state, so they can be safely bypassed in production for performance
- CQS helps prevent **heisenbugs** — bugs that change behavior when you try to observe them
- The principle is not limited to OOP; it applies to any paradigm where reasoning about side effects matters

## Commands and Syntax

**Non-CQS (combined mutation + return — useful for thread safety):**
```java
public int incrementAndReturnX() {
    lock x;
    x = x + 1;
    int x_copy = x;
    unlock x;
    return x_copy;
}
```

**CQS-compliant (separate command and query — not thread-safe without external synchronization):**
```java
public int value() { return x; }    // query
void increment() { x = x + 1; }    // command
```

## Relationships

- **Design by Contract**: CQS enables safe assertion checking without side effects
- **CQRS → Event-Driven Architecture**: CQRS systems commonly split into services communicating via events, enabling Event Collaboration and Event Sourcing patterns
- **CQRS → Eventual Consistency**: Separate read/write models raise consistency questions, making eventual consistency a natural fit
- **CQRS → Domain-Driven Design**: CQRS suits complex domains where DDD also applies
- **CQRS → Task-Based UI**: Moving away from CRUD toward separate read/write models enables task-oriented interfaces
- **Eager Read Derivation**: When update logic dominates, query-side models can be simplified by pre-computing read views
- **Event Posters / Memory Images**: If the write model emits events for all updates, read models can be structured as in-memory projections, reducing database interactions
- **Idempotence**: Related concept — queries are inherently idempotent; commands may or may not be

## Exam-Relevant Points

- CQS was devised by **Bertrand Meyer** for the **Eiffel** programming language
- The core rule: methods either **return data** (query) or **change state** (command), never both
- CQS is a **method-level** principle; CQRS is the **architecture-level** generalization
- CQRS uses **separate read and write models/interfaces** and often separate data stores
- **Limitation**: CQS introduces complexity in multithreaded/reentrant code — separating a combined atomic operation (like `incrementAndReturn`) into two calls creates a **race condition** between the command and query
- Classic CQS violation example: `stack.pop()` both removes and returns — Martin Fowler cites this as a case where combining command and query is pragmatically justified
- CQRS pairs naturally with **event-based architectures**, **eventual consistency**, and **DDD**
