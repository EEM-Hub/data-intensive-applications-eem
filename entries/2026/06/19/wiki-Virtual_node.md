---
source: sources/wiki-Virtual_node.md
source_url: https://en.wikipedia.org/wiki/Virtual_node
---

## Network Nodes: Types and Roles Across Network Architectures

A node is any redistribution point or communication endpoint within a telecommunications or computer network. This page defines what constitutes a node across computer networks, telecommunications systems, and distributed systems, distinguishing nodes from passive components and clarifying addressing requirements at different network layers.

## Key Concepts

- A **node** is an electronic device attached to a network capable of creating, receiving, or transmitting information over a communication channel
- Nodes divide into two categories: **Data Communication Equipment (DCE)** — modems, hubs, bridges, switches — and **Data Terminal Equipment (DTE)** — phones, printers, host computers
- **Passive distribution points** (patch panels, distribution frames) are explicitly **not** nodes
- Nodes participating at the **data link layer** in a LAN/WAN must have a **network address**, typically one per network interface controller (NIC)
- Devices operating **below the data link layer** (e.g., Ethernet hubs, serial-interface modems) do not require a network address
- On the Internet, all **hosts** are physical network nodes, but not all physical network nodes are hosts — switches and bridges lack IP addresses and are not Internet nodes
- In distributed systems, nodes are **clients, servers, or peers**; peers may alternate roles
- **Virtual nodes** address heterogeneity in distributed systems — a single physical node maps to multiple positions in a hash ring (e.g., Amazon Dynamo's consistent hashing)
- **End nodes** are peripheral computers that connect transiently to clouds and present the **end node problem** — unmanaged devices introducing security risk to managed infrastructure
- **Supernodes** are peers that actively route data for other devices in overlay or peer-to-peer networks

## Commands and Syntax

No commands or configuration syntax — this is a conceptual/definitional topic.

## Relationships

- **OSI Model layers**: Node addressing requirements depend on the layer — data link layer requires MAC-level addresses; network layer (Internet) requires IP addresses
- **Network topology**: Nodes are fundamental elements alongside links and switches in any network topology
- **Consistent hashing / Dynamo**: Virtual nodes are a key mechanism in distributed hash tables, directly relevant to partitioning and replication strategies
- **Cloud computing**: End nodes connect the end-node problem to security architecture and trust models
- **Telecommunications infrastructure**: Telephone exchanges, base station controllers, HLR, GGSN, and SGSN are all node types in cellular networks; base stations themselves are **not** nodes in this context
- **CATV/fiber optic**: Fiber optic nodes define geographic service areas measured in "homes passed"

## Exam-Relevant Points

- **Passive devices are not nodes** — distribution frames and patch panels do not qualify
- **Layer distinction matters**: A device operating only below the data link layer (hub, serial modem) does not need a network address and is not a LAN node in the addressing sense
- **Internet node vs. physical node**: Switches and bridges are physical network nodes but **not** Internet nodes (no IP address except for management)
- **All Internet hosts are physical network nodes**, but the reverse is not true
- **Virtual nodes in Dynamo**: Each physical node is assigned multiple tokens/positions in the consistent hash ring to handle heterogeneous node performance — a frequently tested distributed systems concept
- **End node problem**: Unmanaged end-user devices connecting to a cloud introduce security risks; remediation requires establishing trust in the end node
- **Cellular network distinction**: Base station controllers, HLR, GGSN, SGSN are nodes; **base stations are not**
- **Supernode**: A peer that routes data for others in a P2P or overlay network — distinct from a regular peer
