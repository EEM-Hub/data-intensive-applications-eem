---
source: https://en.wikipedia.org/wiki/Three-phase_commit_protocol
fetched: 2026-06-19
---

Distributed algorithm 

In [computer networking](./Computer_networking) and distributed [databases](./Database), the **three-phase commit protocol** (**3PC**)[[1]](./Three-phase_commit_protocol#cite_note-3PC-1) is a [distributed algorithm](./Distributed_algorithm) that ensures all nodes in a [system](./Distributed_system) agree to [commit](./Commit_(data_management)) or abort a [transaction](./Database_transaction). It improves upon the [two-phase commit protocol](./Two-phase_commit_protocol) (2PC) by eliminating the possibility of indefinite blocking caused by a specific type of failure during the commit phase.

 

## Motivation

 

A [two-phase commit protocol](./Two-phase_commit_protocol) cannot dependably recover from a failure of both the coordinator and a cohort member during the **Commit phase**.  If only the coordinator had failed, and no cohort members had received a commit message, it could safely be inferred that no commit had happened.  If, however, both the coordinator and a cohort member failed, it is possible that the failed cohort member was the first to be notified, and had actually done the commit.  Even if a new coordinator is selected, it cannot confidently proceed with the operation until it has received an agreement from all cohort members, and hence must block until all cohort members respond.

 

The three-phase commit protocol eliminates this problem by introducing the Prepared to commit state.  If the coordinator fails before sending preCommit messages, the cohort will unanimously agree that the operation was aborted.  The coordinator will not send out a doCommit message until all cohort members have **ACK**ed that they are **Prepared to commit**. This eliminates the possibility that any cohort member actually completed the transaction before all cohort members were aware of the decision to do so (an ambiguity that necessitated indefinite blocking in the [two-phase commit protocol](./Two-phase_commit_protocol)).

 

## Solution

 

The pre-commit phase introduced above helps the system to recover when a participant or both the coordinator and a participant failed during the commit phase. When the recovery coordinator takes over after the coordinator failed during a commit phase of [two-phase commit](./Two-phase_commit), the new pre-commit comes handy as follows: On querying participants, if it learns that some nodes are in commit phase then it assumes that the previous coordinator before crashing has made the decision to commit. Hence it can shepherd the protocol to commit. Similarly, if a participant says that it had not received a PrepareToCommit message, then the new coordinator can assume that the previous coordinator failed even before it completed the PrepareToCommit phase. Hence it can safely assume that no participant has committed the changes, and hence safely abort the transaction.

 

## Extensions

 

Using Skeen's original three-phase commit protocol, it is possible that a quorum becomes connected without being able to make progress (this is not a deadlock situation; the system will still progress if the network partitioning is resolved). Keidar and Dolev's E3PC[[2]](./Three-phase_commit_protocol#cite_note-E3PC-2) refines Skeen's three-phase commit protocol and solves this problem in a way which *always* allows a quorum to make progress.

 

## Disadvantages

 

Three-phase commit assumes a network with bounded delay and nodes with bounded response times; In most practical systems with unbounded network delay and process pauses, it cannot guarantee atomicity. The other drawback of the protocol is it requires at least three round trips to complete, needing a minimum of three round trip times (RTTs). This is potentially a long latency to complete each transaction.

 

## References

  
1. [↑](./Three-phase_commit_protocol#cite_ref-3PC_1-0) Skeen, Dale (February 1982). [*A Quorum-Based Commit Protocol*](https://ecommons.cornell.edu/handle/1813/6323) (Technical report). Department of Computer Science, Cornell University.
2. [↑](./Three-phase_commit_protocol#cite_ref-E3PC_2-0) [Keidar, Idit](./Idit_Keidar); Danny Dolev (December 1998). ["Increasing the Resilience of Distributed and Replicated Database Systems"](https://iditkeidar.com/wp-content/uploads/files/Abstracts/jcss.html). *Journal of Computer and System Sciences*. **57** (3): 309–324. [doi](./Doi_(identifier)):[10.1006/jcss.1998.1566](https://doi.org/10.1006%2Fjcss.1998.1566).

 

## See also

 
- [Two-phase commit protocol](./Two-phase_commit_protocol)
- [Paxos algorithm](./Paxos_algorithm)