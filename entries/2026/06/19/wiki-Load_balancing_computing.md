---
source: sources/wiki-Load_balancing_computing.md
source_url: https://en.wikipedia.org/wiki/Load_balancing_(computing)
---

## Load Balancing in Distributed Systems

Load balancing is the process of distributing tasks across computing resources to optimize response time and prevent uneven utilization. It is a fundamental technique in both parallel computing and internet-scale services. Two primary approaches exist: **static algorithms** (no runtime state awareness) and **dynamic algorithms** (adapt to current system load, more efficient but costlier in communication overhead).

## Key Concepts

- **Static load balancing**: Assigns tasks without considering current system state; relies on assumptions about task arrival times and resource requirements. Centralized around a router or master node. Works well for homogeneous, predictable workloads (e.g., HTTP requests).
- **Dynamic load balancing**: Monitors current load on each node and migrates tasks from overloaded to underloaded nodes at runtime. More complex but handles variable execution times well.
- **Unique vs. dynamic assignment**: Unique assignment fixes tasks to processors at a point in time; dynamic assignment continuously redistributes based on evolving system state.
- **Task dependencies**: When tasks form a directed acyclic graph (DAG), finding optimal execution order is NP-hard; metaheuristic job schedulers approximate solutions.
- **Moldable vs. malleable algorithms**: Moldable algorithms adapt to different processor counts but require fixing the count before execution; malleable algorithms handle fluctuating processor counts during execution.
- **Work stealing**: Idle processors "steal" tasks from busy processors. When the network is heavily loaded, least-loaded units should offer availability; when lightly loaded, overloaded units should request help.
- **Session persistence (stickiness)**: Routing all requests in a user session to the same backend server. Trades simplicity for lack of automatic failover.
- **Single point of failure**: Load balancers themselves must avoid becoming SPOFs; typically deployed in high-availability pairs.

## Commands and Syntax

**DNS delegation for geographic load balancing:**
```
one.example.org  A   192.0.2.1
two.example.org  A   203.0.113.2
www.example.org  NS  one.example.org
www.example.org  NS  two.example.org
```
Each server's zone file resolves `www.example.org` to its own IP, achieving geo-sensitive distribution with automatic failover (unresponsive DNS = no traffic).

**Scheduling algorithms for server-side load balancers:**
- Random choice
- Round-robin (optionally weighted by server capacity)
- Least connections (optionally weighted)
- Hash-based allocation
- Power of two choices (pick two random servers, choose the better one)

## Relationships

- **Prefix sum algorithm**: Enables optimal static distribution of divisible tasks in logarithmic time across processors.
- **Parallel computing architectures**: Shared memory (PRAM) vs. distributed memory with message passing fundamentally shapes which load balancing strategies are viable.
- **Master-worker pattern**: Simple dynamic scheme where a master distributes work; suffers from bottleneck/scalability problems at scale. Replacing the single master with a shared task queue improves scalability.
- **Work stealing**: Addresses scalability limits of master-worker by decentralizing task assignment. Related to tree-shaped computation for recursive task subdivision.
- **Session management**: Connects to database replication, Memcached, browser cookies, and URL rewriting as strategies for maintaining state across load-balanced backends.
- **Fault tolerance**: Critical in large clusters; algorithms must detect processor failures and recover computation.
- **DNS (Round-robin DNS, DNS delegation)**: DNS-layer load balancing avoids dedicated hardware but has caching issues that can skew distribution.

## Exam-Relevant Points

- Static algorithms are simple and efficient for homogeneous tasks but cannot adapt to variable workloads; dynamic algorithms adapt but incur communication overhead.
- Optimal task scheduling with dependencies (DAG) is **NP-hard**.
- The prefix sum algorithm achieves optimal load distribution in **logarithmic time** when tasks are divisible and execution times are known.
- Master-worker is a **scalability bottleneck** — the master becomes overloaded with communication as processor count grows.
- Work stealing rule of thumb: heavily loaded network → least-loaded nodes offer availability; lightly loaded network → overloaded nodes request help. This minimizes message exchange.
- Round-robin DNS suffers from **DNS caching skew**; client-side random selection is unaffected by caching and provides better distribution.
- Server-side load balancers must be deployed in **high-availability pairs** to avoid becoming a single point of failure.
- Session persistence approaches: sticky sessions (simple but no failover), shared database (adds DB load), browser-side storage via cookies (preferred — any backend can serve any request), URL rewriting (security concerns).
- **Moldable** = adapts to processor count fixed before execution. **Malleable** = handles processor count changes during execution.
- Power of two choices: a simple randomized algorithm that dramatically improves over pure random selection by picking the better of two random servers.
