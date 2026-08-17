# Selected project case studies

These short case studies explain the engineering behind my private source repositories. Metrics are project-level measurements recorded during development, not production claims.

## Aligo: Multi-Agent Travel Assistant

**Problem.** Travel planning mixes real-time information, personal preferences, historical context, policy documents, and tasks that can run in parallel. A single prompt chain quickly becomes slow and difficult to reason about.

**Approach.** I built a Plan-and-Execute system in which an intention agent produces a typed plan, an orchestration agent schedules work by priority, and specialized agents handle memory, preference updates, RAG, live information, event collection, and itinerary generation.

**Architecture.**

- AgentScope and Python for agent orchestration
- Redis for short-term session memory; PostgreSQL for durable memory
- Milvus with BGE-m3 embeddings for document retrieval and source attribution
- Lazy skill discovery and progressive disclosure to reduce startup and prompt overhead
- Retry with exponential backoff, circuit breaking, and health checks around LLM calls

**Measured development results.**

- Semantic intent classification improved from 65% to 90%+ on the project's evaluation set.
- Priority-based parallel execution reduced a representative workflow from 30 seconds to 15 seconds.
- The RAG evaluation reached 95% accuracy on the project's policy-document question set.
- Lazy loading reduced measured startup time to approximately 3 seconds.

**What I learned.** Agent systems become easier to improve when planning, execution, memory, and tool reliability are separate concerns with visible interfaces.

## Easy Trans: Zero-Config LAN File Transfer

**Problem.** Moving a large file between nearby devices should not require cloud storage, accounts, or manually finding IP addresses.

**Approach.** I built a single-binary Go CLI. A sender advertises an `_et._tcp.local.` service over mDNS with a short room code; a receiver discovers it and downloads files directly over the local network.

**Engineering details.**

- HTTP Range requests and temporary progress files for resumable transfers
- Streaming SHA-256 calculation through `io.TeeReader`, avoiding a second disk read
- Directory packaging with preserved structure and timestamps
- Concurrent support for multiple receivers
- Cross-platform builds for Windows, macOS, and Linux
- Explicit conflict handling: existing files are skipped rather than overwritten

**What I learned.** A small tool feels dependable when discovery, recovery, integrity, and failure messages are treated as core product features.

## Backend Learning Systems

**Problem.** Backend concepts are easy to memorize and hard to internalize without executable examples.

**Approach.** I created a set of focused learning repositories that turn theory into code, tests, diagrams, and repeatable exercises.

**Coverage.**

- 56 runnable Java backend topics across collections, JUC, JVM, MySQL, Redis, and Spring
- All 23 Gang of Four design patterns with Java implementations, tests, and Mermaid UML diagrams
- Spring Boot exercises for Kafka, RabbitMQ, Elasticsearch, and MongoDB
- A 25-exercise Neovim curriculum spanning editing, LSP, refactoring, and Git workflows

**What I learned.** Teaching material improves when each concept has a minimal executable example, a concrete analogy, and a clear path from observation to explanation.

---

[Back to profile](./README.md)
