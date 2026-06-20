---
source: sources/wiki-Apache_Wave.md
source_url: https://en.wikipedia.org/wiki/Apache_Wave
---

## Google Wave / Apache Wave: Real-Time Collaborative Editing Framework

Google Wave (later Apache Wave) was a software framework for real-time collaborative online editing, announced by Google in May 2009. It attempted to merge email, instant messaging, wikis, and social networking into a single web-based platform using operational transformation for concurrent editing. Despite initial excitement, it was discontinued by Google in 2010 due to low adoption, handed to the Apache Software Foundation, and ultimately retired in January 2018 without ever leaving incubator status.

## Key Concepts

- **Wave**: A hosted XML document containing a complete thread of multimedia messages (blips), stored on a central server rather than distributed to individual inboxes
- **Blip**: An individual message or edit within a wave; users could reply to specific blips anywhere in the thread
- **Operational Transformation (OT)**: The concurrency control algorithm enabling multiple users to simultaneously edit the same document with low latency and consistency
- **Real-time collaboration**: All edits were visible letter-by-letter as typed, blurring the line between email and instant messaging depending on how many participants were online
- **Federation**: Waves were distributed across providers using the Wave Federation Protocol (an XMPP extension), analogous to how email works across providers
- **Wavelets**: Sub-components of waves that could be federated independently; supported private reply wavelets invisible to other participants
- **Playback**: Complete edit history was stored within each wave, allowing users to replay the chronological sequence of all changes
- **Extensions**: Two types — **Robots** (automated server-side participants that respond to events) and **Gadgets** (client-side interactive applications embedded in waves, often built on OpenSocial)
- **Wave in a Box**: The Apache-era server implementation intended for self-hosted deployment
- **SwellRT**: A fork that re-engineered Wave into a backend-as-a-service for building collaborative and federated apps; IP transferred to Apache in 2017

## Commands and Syntax

No CLI commands or configuration syntax survive from the project. Key technical components that were open-sourced:

1. Operational transformation (OT) code
2. Underlying wave model
3. Basic client/server prototype using the wave protocol
4. Testing and verification suite for custom implementations

The project was written in **Java** using **OpenJDK**, with the web UI built on **Google Web Toolkit (GWT)**. The federation protocol extended **XMPP**. Security used **TLS** for authentication and encrypted connections. Waves and wavelets were identified by **domain name + ID strings**.

## Relationships

- **Operational Transformation**: Core algorithm also used by Google Docs, SharePoint, and other collaborative editors — the foundational consistency mechanism for concurrent editing
- **XMPP**: Wave Federation Protocol was an extension of XMPP, connecting Wave to the broader real-time messaging ecosystem
- **Collaborative real-time editing**: Wave is a predecessor to modern tools like **Google Docs**, **Microsoft Loop**, **Slack**, and **Microsoft Teams** (all listed as "see also")
- **Fluid Framework**: Microsoft's modern equivalent — a framework for distributed real-time collaboration using similar principles
- **CRDTs vs. OT**: Wave used OT (server-mediated), while newer systems like Fluid Framework increasingly use CRDTs (conflict-free replicated data types) for peer-to-peer scenarios
- **Email replacement ambition**: Wave was explicitly designed to replace email protocol, mirroring email's federated provider model but adding real-time collaboration
- **SwellRT / Backend-as-a-Service**: The evolution from monolithic platform to composable backend service foreshadowed modern real-time backend services (Firebase, Supabase)

## Exam-Relevant Points

- Wave used **Operational Transformation (OT)** for concurrent editing — not CRDTs. This is a critical distinction in distributed systems design
- The **federation model** stored waves on the originating provider's servers and replicated copies to other providers — the originating server was responsible for hosting, processing, and concurrency control
- Wave demonstrated the challenge of **convergent communication tools**: merging email, IM, wikis, and social networking into one interface led to "dismal usability" — a cautionary tale about product scope
- The **federation protocol** was built as an XMPP extension, illustrating the pattern of extending existing protocols rather than building from scratch
- User data was **not federated** (not shared across providers), while wave content was — an important privacy/architecture distinction
- Security relied on **TLS authentication** with domain-name-based identification
- Wave's failure is commonly cited as evidence that **protocol-level ambition** (replacing email) requires both technical excellence and user experience simplicity
- The transition from Google to Apache to retirement (2009–2018) illustrates the lifecycle challenges of open-source projects that lose their corporate sponsor
- Wave's core innovations (real-time collaborative editing, operational transformation) survived in Google Docs and influenced the entire collaborative editing space
