# Learning Roadmap

## Purpose

This roadmap defines the intended learning progression of the Distributed Systems Engineering Lab.

It is not a fixed implementation plan and it is not a commitment to introduce every technology or architectural pattern listed in this document.

The roadmap describes capabilities to develop, questions to answer, and engineering situations to reproduce.

Each stage should be entered only when the previous one has produced enough evidence, documentation, and understanding.

The system should evolve because a new problem justifies the next step, not because the roadmap says that a particular technology must be used.

---

## Learning Strategy

The project follows a problem-driven learning process.

For every significant topic:

1. Start from a working and understandable system.
2. Introduce or identify a concrete limitation.
3. Reproduce the limitation consistently.
4. Define relevant metrics.
5. Formulate a hypothesis.
6. Evaluate multiple solutions.
7. Select the smallest justified intervention.
8. Implement it.
9. Repeat the original experiment.
10. Document the outcome and remaining limitations.

The main learning unit is therefore not a technology.

The main learning unit is an engineering decision supported by evidence.

---

## Progression Model

The roadmap is divided into learning stages.

Each stage introduces a different type of engineering concern.

The exact number and order of challenges inside each stage may change as the project evolves.

---

# Stage 0 — Establish a Trustworthy Baseline

## Goal

Build the simplest system that can support reliable engineering experiments.

## Questions to answer

- Can another engineer run the system locally?
- Can the system be built and tested with a small number of commands?
- Is the initial architecture easy to understand?
- Can test data be generated deterministically?
- Can experiments be repeated under similar conditions?
- Are results stored in a consistent format?

## Expected capabilities

By the end of this stage, the repository should include:

- a minimal working backend application;
- a relational database;
- an automated test suite;
- a reproducible local environment;
- deterministic seed data;
- basic documentation;
- a repeatable load-testing process;
- a known initial performance baseline.

## Exit criteria

This stage is complete when:

- the application can be started from documented instructions;
- automated tests pass consistently;
- a basic load test can be executed repeatedly;
- baseline results are stored in the repository;
- the architecture contains no unjustified distributed components.

---

# Stage 1 — Measure Before Optimizing

## Goal

Develop the ability to identify and explain performance problems using evidence.

## Topics

- latency;
- throughput;
- percentiles;
- CPU-bound and I/O-bound workloads;
- database query behavior;
- connection pooling;
- serialization cost;
- allocation and memory pressure;
- synchronous and asynchronous execution;
- resource contention.

## Questions to answer

- Which part of a request consumes the most time?
- Is the bottleneck located in the application, database, network, or external dependency?
- Are average response times hiding slow requests?
- Does an optimization improve latency, throughput, or both?
- Does the optimization introduce a new cost elsewhere?
- Is the observed improvement repeatable?

## Expected capabilities

- define relevant performance metrics;
- produce a measurable baseline;
- inspect application and database behavior;
- distinguish symptoms from causes;
- propose multiple optimization strategies;
- validate results under the same test conditions;
- avoid premature optimization.

## Possible challenge areas

- inefficient database projections;
- missing or ineffective indexes;
- N+1 queries;
- loading unnecessary data;
- blocking operations;
- unbounded result sets;
- database connection exhaustion;
- excessive object allocation.

## Exit criteria

This stage is complete when several performance problems have been:

- reproduced;
- measured;
- diagnosed;
- improved;
- measured again;
- documented with trade-offs.

---

# Stage 2 — Understand Concurrency and Shared State

## Goal

Understand how concurrent execution affects correctness, performance, and resource usage.

## Topics

- race conditions;
- optimistic concurrency;
- pessimistic locking;
- transaction isolation;
- deadlocks;
- thread safety;
- atomic operations;
- connection and thread pool saturation;
- concurrent request handling.

## Questions to answer

- What happens when two requests modify the same resource?
- Which operations must be atomic?
- How are conflicting updates detected?
- When is locking necessary?
- What are the costs of stronger isolation?
- How can concurrency reduce throughput instead of increasing it?
- How should the system behave when a conflict occurs?

## Expected capabilities

- reproduce race conditions;
- identify unsafe shared state;
- choose an appropriate concurrency strategy;
- reason about transaction boundaries;
- detect and handle conflicts;
- explain consistency guarantees to another engineer.

## Possible challenge areas

- simultaneous order updates;
- overselling limited stock;
- duplicate requests;
- lost updates;
- database deadlocks;
- concurrent background processing.

## Exit criteria

This stage is complete when the system can handle selected concurrent operations predictably and the chosen guarantees are explicitly documented.

---

# Stage 3 — Design for Dependency Failure

## Goal

Stop assuming that dependencies are fast, reliable, or permanently available.

## Topics

- timeouts;
- transient failures;
- retries;
- exponential backoff;
- jitter;
- circuit breakers;
- bulkheads;
- fallbacks;
- graceful degradation;
- failure propagation.

## Questions to answer

- What happens when a dependency becomes slow?
- What happens when it becomes unavailable?
- How long should a caller wait?
- Which failures are safe to retry?
- Can retries make the incident worse?
- How can a local failure become a system-wide failure?
- Which features can degrade without making the whole system unavailable?

## Expected capabilities

- simulate slow and unavailable dependencies;
- define explicit timeout policies;
- distinguish retryable and non-retryable operations;
- prevent uncontrolled retry storms;
- isolate failures;
- measure recovery behavior;
- document degraded modes.

## Possible challenge areas

- a slow external payment provider;
- an unavailable notification service;
- repeated database connection failures;
- dependency latency causing request accumulation;
- cascading failures between components.

## Exit criteria

This stage is complete when dependency failures produce controlled and observable system behavior rather than unpredictable collapse.

---

# Stage 4 — Introduce Asynchronous Processing

## Goal

Understand when asynchronous communication solves a real problem and what new problems it introduces.

## Topics

- commands and events;
- queues and topics;
- producers and consumers;
- background workers;
- delivery guarantees;
- acknowledgements;
- duplicate delivery;
- ordering;
- dead-letter queues;
- backpressure.

## Questions to answer

- Which work must complete before responding to the client?
- Which work can be processed later?
- What happens if the producer succeeds but message publication fails?
- What happens if the same message is delivered twice?
- Does message order matter?
- How should failed messages be handled?
- How does the system behave when consumers fall behind?

## Expected capabilities

- justify asynchronous processing based on measured needs;
- separate immediate and deferred work;
- design message contracts;
- handle duplicate delivery;
- define failure and retry policies;
- monitor queues and consumers;
- explain the operational cost of messaging.

## Possible challenge areas

- asynchronous notifications;
- delayed order processing;
- workload spikes;
- unreliable event publication;
- poison messages;
- slow consumers.

## Exit criteria

This stage is complete when asynchronous processing has been introduced for a justified use case and its delivery, failure, and recovery behavior are documented.

---

# Stage 5 — Manage Consistency Across Boundaries

## Goal

Understand the consequences of updating data across multiple transactional boundaries.

## Topics

- local transactions;
- eventual consistency;
- idempotency;
- transactional outbox;
- inbox pattern;
- sagas;
- compensating actions;
- reconciliation;
- consistency models.

## Questions to answer

- What must be strongly consistent?
- What can become consistent later?
- What happens when one operation succeeds and another fails?
- How can lost events be prevented?
- How are repeated operations detected?
- When is compensation preferable to rollback?
- How can inconsistent state be detected and repaired?

## Expected capabilities

- define consistency requirements explicitly;
- identify transactional boundaries;
- implement idempotent operations;
- explain eventual consistency to technical and non-technical stakeholders;
- select an appropriate coordination strategy;
- design reconciliation mechanisms.

## Possible challenge areas

- order creation and event publication;
- payment completion and order status;
- inventory reservation;
- repeated consumer execution;
- partial workflow failure.

## Exit criteria

This stage is complete when the system demonstrates at least one cross-boundary workflow with clearly documented consistency guarantees and recovery behavior.

---

# Stage 6 — Scale Stateless Workloads

## Goal

Understand what changes when multiple instances of the same application run simultaneously.

## Topics

- horizontal scaling;
- stateless services;
- load balancing;
- shared state;
- sticky sessions;
- distributed locking;
- cache coordination;
- worker competition;
- leader election concepts.

## Questions to answer

- Can any request be handled by any instance?
- Where does application state live?
- What happens when several workers process the same work?
- Which in-memory assumptions stop being valid?
- How does load balancing affect behavior?
- How can coordinated work be performed safely?
- What is the actual scaling bottleneck?

## Expected capabilities

- run multiple application instances;
- detect hidden local state;
- avoid instance-specific correctness assumptions;
- measure scaling efficiency;
- identify non-scalable dependencies;
- explain why adding instances may not improve throughput.

## Possible challenge areas

- in-memory session state;
- duplicate background work;
- shared scheduled jobs;
- distributed cache;
- database saturation after horizontal scaling;
- uneven load distribution.

## Exit criteria

This stage is complete when the application can run with multiple instances and its remaining scaling constraints are measured and documented.

---

# Stage 7 — Use Caching Deliberately

## Goal

Understand caching as a consistency and operational decision, not merely a performance shortcut.

## Topics

- cache-aside;
- read-through and write-through concepts;
- time-to-live;
- invalidation;
- stale data;
- cache stampede;
- hot keys;
- local and distributed caches;
- cache failure modes.

## Questions to answer

- Is the workload suitable for caching?
- What data can safely become stale?
- How long can it remain stale?
- How is the cache invalidated?
- What happens when the cache is unavailable?
- Can the cache overload the original data source?
- Does the cache improve the relevant metric?

## Expected capabilities

- identify cacheable workloads;
- define freshness requirements;
- design invalidation behavior;
- reproduce cache stampede;
- compare local and distributed caching;
- measure hit rate and downstream load;
- remove a cache when its cost is unjustified.

## Possible challenge areas

- high-volume product reads;
- expensive repeated queries;
- invalidation after product updates;
- concurrent cache misses;
- unavailable cache infrastructure.

## Exit criteria

This stage is complete when caching has been evaluated through a reproducible experiment and its consistency implications are clearly stated.

---

# Stage 8 — Build Observability Across the System

## Goal

Make system behavior understandable without relying on local debugging or intuition.

## Topics

- structured logging;
- correlation identifiers;
- metrics;
- distributed tracing;
- service-level indicators;
- dashboards;
- alerting concepts;
- telemetry cost;
- high-cardinality data.

## Questions to answer

- Can a single request be followed through the system?
- Which signals explain latency and failures?
- Can saturation be detected before an outage?
- Which metrics reflect user impact?
- Are logs useful during an incident?
- Can telemetry itself become expensive or misleading?
- What information is required to validate an architectural decision?

## Expected capabilities

- correlate operations;
- expose meaningful metrics;
- trace cross-component requests;
- distinguish logs, metrics, and traces;
- diagnose injected failures using telemetry;
- define basic service-level indicators;
- avoid unnecessary or high-risk telemetry.

## Possible challenge areas

- locating latency across several components;
- tracing asynchronous workflows;
- detecting queue backlog;
- identifying dependency failures;
- measuring error rates and saturation.

## Exit criteria

This stage is complete when an engineer can diagnose selected failures and bottlenecks primarily through the system's telemetry.

---

# Stage 9 — Evaluate Service Boundaries

## Goal

Decide whether part of the system should remain inside the existing application or become independently deployable.

## Topics

- modular monoliths;
- bounded contexts;
- coupling;
- cohesion;
- independent deployment;
- data ownership;
- synchronous service calls;
- operational complexity;
- organizational boundaries.

## Questions to answer

- What problem would service extraction solve?
- Can the same problem be solved within the monolith?
- Does the candidate component have clear ownership?
- Can its data be separated?
- What new failure modes would extraction introduce?
- Does independent deployment provide measurable value?
- Is the organization capable of operating the additional service?

## Expected capabilities

- identify meaningful boundaries;
- compare modularization with service extraction;
- quantify operational costs;
- avoid technology-driven decomposition;
- design explicit contracts;
- reason about data ownership.

## Possible challenge areas

- isolating a notification capability;
- independently scaling a read-heavy workload;
- extracting a slow external integration;
- separating a background processing component.

## Exit criteria

This stage is complete when a service boundary has been evaluated through a documented decision, whether the result is extraction or remaining inside the monolith.

Remaining monolithic is a valid and potentially preferable outcome.

---

# Stage 10 — Operate Under Controlled Failure

## Goal

Evaluate the complete system under realistic stress and failure conditions.

## Topics

- load testing;
- stress testing;
- soak testing;
- fault injection;
- chaos experiments;
- recovery time;
- capacity limits;
- operational readiness;
- incident analysis.

## Questions to answer

- At what point does the system degrade?
- Does it fail gradually or suddenly?
- Which dependency reaches its limit first?
- Can the system recover automatically?
- Is data correctness preserved during failure?
- Are failures visible through telemetry?
- Are documented recovery procedures effective?

## Expected capabilities

- design safe failure experiments;
- define expected steady-state behavior;
- inject controlled faults;
- measure degradation and recovery;
- identify capacity limits;
- produce incident-style reports;
- recommend prioritized improvements.

## Possible challenge areas

- dependency shutdown;
- artificial latency;
- message broker interruption;
- database connection exhaustion;
- consumer backlog;
- instance termination during processing;
- sustained high load.

## Exit criteria

This stage is complete when the repository includes controlled experiments that demonstrate how the system degrades, recovers, and preserves or compromises correctness.

---

## Cross-Cutting Competencies

The following competencies apply to every stage.

### Technical decision records

Significant decisions should be recorded through Architecture Decision Records.

Each record should explain:

- context;
- decision;
- alternatives;
- consequences;
- limitations;
- conditions that could justify revisiting the decision.

### Reproducibility

Every experiment should document:

- environment assumptions;
- setup commands;
- test data;
- workload;
- measurement method;
- raw results;
- interpretation.

### Testing

Tests should protect both functional behavior and the engineering property being studied.

Depending on the challenge, this may include:

- unit tests;
- integration tests;
- concurrency tests;
- contract tests;
- load tests;
- failure tests.

### Security

Security should not become the main subject of every challenge, but the project must avoid unsafe defaults such as:

- committed secrets;
- unvalidated input;
- sensitive data in logs;
- insecure container configuration;
- undocumented exposed services.

### Communication

Each completed challenge should be understandable without reading the full commit history.

The documentation should allow a reviewer to answer:

- What was the problem?
- Why did it matter?
- How was it measured?
- What alternatives were considered?
- What decision was made?
- What evidence supports the result?
- What trade-offs remain?

---

## Roadmap Governance

This roadmap may evolve as knowledge increases.

Changes are acceptable when they are justified and recorded.

A stage may be:

- reordered;
- divided into smaller stages;
- combined with another stage;
- postponed;
- removed.

The roadmap should never force the project to introduce complexity that is not supported by a real learning objective.

Before starting a new challenge, the following question must be answered:

> What specific engineering capability will this challenge develop or demonstrate?

If that question cannot be answered clearly, the challenge should not begin.

---

## Current Position

The project is currently in:

> Stage 0 — Establish a Trustworthy Baseline

No distributed infrastructure should be introduced at this point.

The immediate objective is to define and construct the smallest reliable system capable of supporting future experiments.
