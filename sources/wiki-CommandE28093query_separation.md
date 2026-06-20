---
source: https://en.wikipedia.org/wiki/Command%E2%80%93query_separation
fetched: 2026-06-19
---

IT architecture separating actions and reads 
|  | This articleneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sources. Unsourced material may be challenged and removed.Find sources:"Command–query separation"–news·newspapers·books·scholar·JSTOR(February 2008)(Learn how and when to remove this message) |
| --- | --- |

 

**Command-query separation** (**CQS**) is a principle of [imperative](./Imperative_programming) [computer programming](./Computer_programming). It was devised by [Bertrand Meyer](./Bertrand_Meyer) as part of his pioneering work on the [Eiffel programming language](./Eiffel_(programming_language)).

 

It states that every [method](./Method_(computer_science)) should either be a *command* that performs an action, or a *query* that returns data to the caller, but not both. In other words, *asking a question should not change the answer*.[[1]](./Command–query_separation#cite_note-1) More formally, methods should return a value only if they are [referentially transparent](./Referential_transparency) and hence possess no [side effects](./Side_effect_(computer_science)).

 

## Connection with design by contract

 

Command-query separation is particularly well suited to a [design by contract](./Design_by_contract) (DbC) methodology, in which the design of a [program](./Computer_program) is expressed as [assertions](./Assertion_(software_development)) embedded in the [source code](./Source_code), describing the [state](./State_(computer_science)) of the program at certain critical times.  In DbC, assertions are considered design annotations—not program logic—and as such, their execution should not affect the program state. CQS is beneficial to DbC because any value-returning method (any query) can be called by any assertion without fear of modifying program state.

 

In theoretical terms, this establishes a measure of sanity, whereby one can reason about a program's state without simultaneously modifying that state. In practical terms, CQS allows all assertion checks to be bypassed in a working system to improve its performance without inadvertently modifying its behaviour. CQS may also prevent the occurrence of certain kinds of [heisenbugs](./Heisenbug).

 

## Broader impact on software engineering

 

Even beyond the connection with design by contract, CQS is considered by its adherents to have a simplifying effect on a program, making its states (via queries) and state changes (via commands) more comprehensible.[*[citation needed](./Wikipedia:Citation_needed)*]

 

CQS is well-suited to the [object-oriented](./Object-oriented_programming) methodology, but can also be applied outside of object-oriented programming.  Since the separation of side effects and return values is not inherently object-oriented, CQS can be profitably applied to any programming paradigm that requires reasoning about side effects.[*[citation needed](./Wikipedia:Citation_needed)*]

 

## Command Query Responsibility Segregation

 

[**Command query responsibility segregation** (**CQRS**)](./Command_Query_Responsibility_Segregation) generalises CQS to services, at the architectures level: it applies the CQS principle by using separate *Query* and *Command* interfaces and usually data models to *retrieve* and *modify* data, respectively.[[2]](./Command–query_separation#cite_note-2)[[3]](./Command–query_separation#cite_note-FowlerCQRS-3)

 

## Other architectural patterns

 
- As we move away from a single representation that we interact with via [CRUD](./CRUD), we can easily move to a task-based UI.
- CQRS fits well with event-based programming models. It's common to see a CQRS system split into separate services communicating with Event Collaboration. This allows these services to easily take advantage of [Event Driven Architecture](./Event_Driven_Architecture).
- Having separate models raises questions about how hard it is to keep those models consistent, which raises the likelihood of using eventual consistency.
- For many domains, much of the logic required is needed when you're updating, so it may make sense to use Eager Read Derivation to simplify your query-side models.
- If the write model generates events for all updates, you can structure read models as Event Posters, allowing them to be Memory Images and thus avoiding a lot of database interactions.
- CQRS is suited to complex domains, the kind that also benefits from [Domain-Driven Design](./Domain-driven_design).[[3]](./Command–query_separation#cite_note-FowlerCQRS-3)

 

## Limitations

 

CQS can introduce complexities for implementing [reentrant](./Reentrant_(subroutine)) and [multithreaded](./Multithreading_(software)) software correctly. This usually occurs when a non-thread-safe pattern is used to implement the command-query separation.

 

Here is a simple example that does not follow CQS, but is useful for multi-threaded software because it solves the complexity of locking for all other parts of the program, but by doing so it doesn't follow CQS because the function both mutates state and returns it:

 
```
private int x;
public int incrementAndReturnX() {
    lock x;   // by some mechanism
    x = x + 1;
    int x_copy = x;
    unlock x; // by some mechanism
    return x_copy;
}

```
 

Here is a CQS-compliant version. Note that it is safely usable only in single-threaded applications. In a multithreaded program, there is a race condition in the caller, between where `increment()` and `value()` would be called:

 
```
private int x;
public int value() {
    return x;
}
void increment() {
    x = x + 1;
}

```
 

Even in single-threaded programs, it is sometimes arguably significantly more convenient to have a method that is a combined query and command. [Martin Fowler](./Martin_Fowler_(software_engineer)) cites the `pop()` method of a [stack](./Stack_(abstract_data_type)) as an example.[[4]](./Command–query_separation#cite_note-4)

 

## See also

 
- [Idempotence](./Idempotence#Computer_science_meaning)
- [Domain-driven design](./Domain-driven_design)
- [Create, read, update and delete](./Create,_read,_update_and_delete) (CRUD)

 

## References

  
1. [↑](./Command–query_separation#cite_ref-1) Meyer, Bertrand. ["Eiffel: a language for software engineering"](http://laser.inf.ethz.ch/2012/slides/Meyer/eiffel_laser_2012.pdf) (PDF). p. 22. Retrieved 16 December 2014.
2. [↑](./Command–query_separation#cite_ref-2) Young, Greg. ["CQRS Documents"](http://cqrs.files.wordpress.com/2010/11/cqrs_documents.pdf) (PDF). Retrieved 2012-12-28.
3. [1](./Command–query_separation#cite_ref-FowlerCQRS_3-0) [2](./Command–query_separation#cite_ref-FowlerCQRS_3-1) Fowler, Martin. ["CQRS"](http://martinfowler.com/bliki/CQRS.html). Retrieved 2011-07-14.
4. [↑](./Command–query_separation#cite_ref-4) Fowler, Martin. ["CommandQuerySeparation"](http://martinfowler.com/bliki/CommandQuerySeparation.html). Retrieved 5 December 2005.

 

## Further reading

 
- [Meyer, Bertrand](./Bertrand_Meyer) (September 1994) [1988]. *Object-oriented Software Construction*. Prentice Hall. [ISBN](./ISBN_(identifier)) [0-13-629049-3](./Special:BookSources/0-13-629049-3).

 

## External links

 
- [Explanation on Martin Fowler's Bliki](http://martinfowler.com/bliki/CommandQuerySeparation.html)