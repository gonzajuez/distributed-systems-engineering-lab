# Engineering Principles

## Purpose

This document defines the engineering principles that guide the evolution of the Distributed Systems Engineering Lab.

These principles are intended to prevent the project from becoming:

- a collection of disconnected technology demonstrations;
- an overengineered reference architecture;
- a microservices showcase without a real justification;
- a repository where decisions are made based on trends rather than evidence.

The principles apply to architecture, implementation, testing, documentation, experimentation, and the use of artificial intelligence.

They are not rigid laws.

A principle may be intentionally broken when the context justifies it, but the exception should be explicit and documented.

---

# 1. Start With the Simplest Adequate Solution

The initial solution should be the simplest design capable of meeting the current requirements.

Complexity must be earned.

The project should not introduce:

- multiple deployable services;
- message brokers;
- distributed caches;
- API gateways;
- orchestration platforms;
- event-driven workflows;
- distributed transactions;
- advanced abstractions;

unless a concrete challenge demonstrates why they are needed.

A simple monolith is not a temporary failure.

It is the default starting point against which more complex alternatives must justify themselves.

## Guiding question

> What is the simplest solution that satisfies the current requirements and preserves our ability to learn?

---

# 2. Introduce Complexity Only to Solve an Explicit Problem

Every significant technology, pattern, abstraction, or infrastructure component must solve a clearly described problem.

The existence of a technology is not a reason to use it.

Before introducing a new component, the repository should explain:

- the current problem;
- the evidence that the problem exists;
- why the current design is insufficient;
- the alternatives considered;
- the expected benefit;
- the new costs and failure modes;
- how the result will be measured.

Examples of invalid justifications include:

- “This is commonly used in modern architectures.”
- “This will make the project more enterprise.”
- “Microservices are more scalable.”
- “We may need it in the future.”
- “It looks better in a portfolio.”

## Guiding question

> Which measured or reproducible problem justifies this additional complexity?

---

# 3. Measure Before Optimizing

Performance decisions should be based on evidence rather than intuition.

Before applying an optimization:

1. Define the symptom.
2. Identify the relevant metric.
3. Establish a repeatable baseline.
4. Formulate a hypothesis.
5. Apply one controlled intervention.
6. Repeat the original measurement.
7. Compare the results.
8. Document secondary effects.

The project should avoid claiming that something is faster without presenting enough information to support the claim.

Relevant metrics may include:

- response-time percentiles;
- throughput;
- error rate;
- CPU usage;
- memory allocation;
- database execution time;
- connection-pool usage;
- queue depth;
- cache hit rate;
- resource saturation.

The average response time alone is often insufficient.

## Guiding question

> What evidence would prove that this change improved the system?

---

# 4. Prefer Reproducible Experiments

An experiment has limited value if another engineer cannot reproduce it.

Each challenge should aim to document:

- prerequisites;
- environment assumptions;
- data volume;
- seed process;
- commands;
- workload;
- duration;
- configuration;
- measurement method;
- raw results;
- interpretation.

Test data should be deterministic whenever possible.

Performance results should include relevant context because absolute numbers vary between environments.

The objective is not to produce universally valid benchmark numbers.

The objective is to make comparisons under controlled conditions.

## Guiding question

> Could another engineer repeat this experiment and understand why the results may differ?

---

# 5. Change One Important Variable at a Time

When possible, each experiment should isolate the effect of one meaningful change.

A challenge should avoid simultaneously introducing:

- a new database access strategy;
- caching;
- asynchronous processing;
- infrastructure changes;
- major refactoring;
- different test data;
- a different load profile.

Changing several variables at once makes it difficult to understand which change produced the result.

Necessary supporting changes should be kept small and explicitly identified.

## Guiding question

> Can we reasonably attribute the observed result to the decision being evaluated?

---

# 6. Distinguish Symptoms, Causes, and Solutions

A slow endpoint is a symptom.

A missing index, excessive database round trips, connection exhaustion, or blocking I/O may be the cause.

Caching, query optimization, pagination, or capacity changes may be possible solutions.

The project should avoid jumping directly from symptom to preferred solution.

Each challenge should attempt to distinguish:

- what is observed;
- what is believed to cause it;
- what evidence supports that belief;
- what interventions are available.

A failed hypothesis is a valid learning outcome when it is documented honestly.

## Guiding question

> Are we solving the verified cause, or merely treating a visible symptom?

---

# 7. Optimize the System, Not Isolated Code

A local code improvement is not necessarily a system improvement.

A change may reduce execution time in one component while increasing:

- database load;
- memory consumption;
- network traffic;
- operational complexity;
- inconsistency risk;
- maintenance cost;
- failure impact.

The relevant unit of analysis is the user-visible operation and the resources required to complete it.

Microbenchmarks may be useful, but they do not replace end-to-end measurements.

## Guiding question

> How does this change affect the complete request or workflow?

---

# 8. Make Trade-Offs Explicit

Architecture decisions rarely provide benefits without costs.

The project should not describe solutions as universally better.

Each significant decision should identify trade-offs involving areas such as:

- correctness;
- consistency;
- availability;
- latency;
- throughput;
- complexity;
- operability;
- security;
- cost;
- development speed;
- cognitive load;
- reversibility.

A valid decision is context-dependent.

Two different solutions may both be reasonable under different constraints.

## Guiding question

> What do we gain, what do we lose, and under which assumptions is this decision valid?

---

# 9. Define Correctness Before Performance

A fast incorrect system is not successful.

Before optimizing a workflow, the expected behavior and guarantees should be clear.

Examples include:

- whether duplicate requests are allowed;
- whether updates may be lost;
- whether ordering matters;
- whether stale reads are acceptable;
- whether an operation must be atomic;
- whether partial completion is permitted;
- how conflicts should be handled.

Performance improvements must preserve the required correctness guarantees or explicitly document which guarantees have changed.

## Guiding question

> Which properties must remain true even under concurrency, retries, and failure?

---

# 10. Assume Partial Failure

Once a system communicates across process or network boundaries, components may fail independently.

The project should not assume that dependencies are:

- always available;
- consistently fast;
- called exactly once;
- returning complete responses;
- recovering immediately;
- failing in obvious ways.

Distributed workflows should consider:

- latency;
- timeouts;
- dropped connections;
- duplicate operations;
- delayed messages;
- unavailable dependencies;
- partial completion;
- inconsistent state;
- recovery.

## Guiding question

> What happens if this dependency becomes slow, unavailable, or returns an ambiguous result?

---

# 11. Treat Retries as a Correctness Decision

Retries are not a universal reliability mechanism.

A retry can:

- repeat a non-idempotent operation;
- increase load during an outage;
- amplify latency;
- create duplicate data;
- hide a persistent failure;
- contribute to cascading failure.

Before retrying, the system should define:

- which failures are transient;
- whether the operation is safe to repeat;
- the maximum number of attempts;
- the delay strategy;
- the total time budget;
- what happens after exhaustion.

## Guiding question

> Can this operation be repeated safely, and could retrying make the incident worse?

---

# 12. Prefer Explicit Timeouts

Network calls and dependency interactions should have deliberate time limits.

An absent or excessive timeout allows work to accumulate and may exhaust:

- request threads;
- connections;
- memory;
- worker capacity;
- client patience.

Timeouts should reflect the operation's total latency budget rather than arbitrary defaults.

A timeout is not only a configuration value.

It is part of the system's behavior and user experience.

## Guiding question

> How long is this operation allowed to consume resources before it is considered unsuccessful?

---

# 13. Design for Idempotency Where Repetition Is Possible

Requests and messages may be delivered or executed more than once.

Whenever repetition is possible, the system should determine whether duplicate execution is:

- harmless;
- detectable;
- preventable;
- compensatable.

Idempotency should be designed around business effects, not only HTTP methods or message identifiers.

Examples include:

- creating an order once;
- charging a payment once;
- reserving inventory once;
- processing an event once from the business perspective.

## Guiding question

> What happens if this exact operation is executed twice?

---

# 14. Keep Transaction Boundaries Explicit

A database transaction provides guarantees only within its actual boundary.

The project should clearly distinguish between:

- one local database transaction;
- multiple database transactions;
- message publication;
- external API calls;
- background processing;
- eventual workflows.

The presence of a transaction in one component does not make an entire distributed workflow atomic.

Cross-boundary consistency should be designed explicitly.

## Guiding question

> Which state changes are truly committed together, and what happens between separate boundaries?

---

# 15. Prefer Stateless Application Instances

Application instances should avoid storing correctness-critical state only in local memory.

Local memory may be appropriate for:

- ephemeral computation;
- non-critical local caching;
- process-specific diagnostics;
- immutable configuration.

It should not silently become the authoritative location for:

- user sessions;
- distributed coordination;
- scheduled work ownership;
- workflow progress;
- deduplication state;
- locks shared between instances.

A design that works with one instance should be examined before assuming it works with several.

## Guiding question

> Would this behavior remain correct if another instance handled the next request?

---

# 16. Use Caching as a Consistency Decision

Caching is not merely a way to make reads faster.

A cache introduces questions about:

- freshness;
- invalidation;
- ownership;
- failure behavior;
- memory limits;
- stampedes;
- hot keys;
- fallback to the source of truth.

Before adding a cache, the project should define:

- what data is cached;
- why it is worth caching;
- how stale it may become;
- how it is invalidated;
- what happens when the cache is unavailable;
- how the benefit will be measured.

## Guiding question

> Which consistency guarantee are we relaxing in exchange for lower latency or reduced load?

---

# 17. Preserve Service and Data Ownership

If the system eventually introduces independently deployable components, ownership boundaries should be explicit.

A service should not exist merely because a technical layer can be extracted.

A meaningful boundary should consider:

- cohesive business capability;
- independent evolution;
- independent deployment value;
- data ownership;
- team ownership;
- scaling characteristics;
- failure isolation.

Shared databases between independently deployed services should be treated as a strong form of coupling and justified deliberately.

## Guiding question

> What capability and data does this component own, and why should it evolve independently?

---

# 18. Prefer Modularization Before Distribution

When a boundary is unclear, begin by enforcing it inside the existing application.

A modular monolith can provide:

- explicit dependencies;
- clear ownership;
- isolated domain logic;
- replaceable implementations;
- reduced coupling;

without introducing network calls, distributed data, deployment coordination, or additional operational burden.

Extracting a service should be considered only when independent deployment or operation provides enough value to justify those costs.

## Guiding question

> Can this boundary be validated inside the monolith before introducing a network boundary?

---

# 19. Observability Must Answer Questions

Telemetry should be introduced to answer operational or engineering questions.

The project should avoid collecting logs, metrics, and traces without a clear use case.

Examples of useful questions include:

- Which dependency dominates request latency?
- Where are errors occurring?
- Is the database connection pool saturated?
- Are consumers falling behind?
- Which workflow step failed?
- Did the system recover?
- What changed after a deployment?

Observability should balance diagnostic value against:

- storage cost;
- runtime overhead;
- privacy;
- high cardinality;
- signal-to-noise ratio.

## Guiding question

> Which question will this signal help us answer during an experiment or incident?

---

# 20. Tests Should Protect Important Properties

Tests should not exist only to increase coverage percentages.

They should protect behavior and engineering guarantees that matter.

Depending on the challenge, useful tests may include:

- unit tests for business rules;
- integration tests for database behavior;
- concurrency tests;
- contract tests;
- idempotency tests;
- migration tests;
- failure tests;
- performance smoke tests;
- end-to-end workflow tests.

A test that cannot fail for a meaningful reason may not provide meaningful protection.

## Guiding question

> Which important behavior or guarantee would this test detect if it broke?

---

# 21. Keep Infrastructure Reproducible

The local environment should be reproducible with documented and automated commands.

Infrastructure configuration should avoid undocumented manual steps.

The repository should aim to define:

- required services;
- versions;
- ports;
- environment variables;
- initialization;
- health checks;
- test data;
- startup and shutdown commands.

Docker is a tool for reproducibility in this project, not evidence of distributed architecture by itself.

## Guiding question

> Can another engineer create the same environment without relying on hidden local configuration?

---

# 22. Separate Experiment Code From Production Guidance

Some challenges may intentionally introduce bad behavior, artificial latency, random failure, or simplified implementations.

The repository must clearly distinguish:

- code designed to reproduce a problem;
- code proposed as an improvement;
- code suitable only for learning;
- decisions that would require further work before production.

A successful experiment is not automatically a production-ready design.

## Guiding question

> Is this implementation demonstrating a concept, or recommending an operational design?

---

# 23. Document Significant Decisions

Significant and durable decisions should be recorded through Architecture Decision Records.

An ADR should be created when a decision:

- changes system boundaries;
- introduces infrastructure;
- changes consistency guarantees;
- changes communication style;
- introduces substantial operational cost;
- rejects a plausible alternative;
- would be difficult to reverse;
- may need to be revisited later.

Not every code-level choice requires an ADR.

## Guiding question

> Would a future engineer reasonably ask why the system was designed this way?

---

# 24. Prefer Reversible Decisions

When uncertainty is high, prefer decisions that are inexpensive to change.

The system should avoid premature commitment to:

- specific infrastructure;
- proprietary abstractions;
- irreversible data models;
- unnecessary service boundaries;
- broad frameworks that control application structure.

Experiments should be small enough to revert when they do not produce the expected result.

## Guiding question

> How difficult will it be to reverse this decision if our assumptions are wrong?

---

# 25. Avoid Speculative Generality

The project should not create abstractions for hypothetical future requirements without evidence.

Examples include:

- generic repositories for every entity;
- universal event buses;
- provider-independent wrappers with only one provider;
- extension points without a real extension;
- configurable behavior that is never varied;
- base classes created only to remove small amounts of duplication.

Duplication may be temporarily preferable to the wrong abstraction.

## Guiding question

> Which current variations or repeated decisions justify this abstraction?

---

# 26. Prefer Clear Code Over Clever Code

The code should optimize for understanding, review, debugging, and safe change.

The project should prefer:

- explicit behavior;
- small focused components;
- meaningful names;
- visible control flow;
- documented boundaries;
- conventional solutions;

over unnecessary indirection or compact but difficult code.

Advanced patterns should be used only when they improve the current design.

## Guiding question

> Will another engineer understand this decision and its consequences without reconstructing hidden behavior?

---

# 27. Treat Security as a Baseline Requirement

Security is not the main learning objective of every challenge, but unsafe defaults should not be accepted casually.

The repository should avoid:

- committed credentials;
- real customer data;
- sensitive data in logs;
- unrestricted administrative endpoints;
- unvalidated external input;
- containers running with unnecessary privileges;
- undocumented public ports;
- outdated dependencies without awareness.

Secrets should be supplied through appropriate local configuration and never committed.

## Guiding question

> Are we introducing an avoidable security risk merely because this is a laboratory?

---

# 28. Keep the Repository Understandable

A reviewer should be able to understand:

- the current architecture;
- how to run the system;
- which challenge is active;
- what changed between iterations;
- where results are stored;
- why significant decisions were made.

Documentation should not depend entirely on chat history or personal memory.

Git is the permanent source of truth.

## Guiding question

> Could an external reviewer understand the project without speaking to its author first?

---

# 29. Use Artificial Intelligence for Leverage, Not Substitution

Artificial intelligence may be used to reduce repetitive work and increase the speed of experimentation.

Appropriate uses include:

- generating scaffolding;
- preparing scripts;
- creating test data;
- drafting documentation;
- proposing test cases;
- reviewing code;
- identifying edge cases;
- explaining unfamiliar implementation details;
- transforming notes into structured documents;
- executing approved mechanical changes.

AI should not replace the author's responsibility to:

- define the problem;
- formulate the hypothesis;
- choose relevant metrics;
- evaluate trade-offs;
- make architectural decisions;
- interpret results;
- defend the final design;
- understand submitted code.

Before delegating an important implementation, the author should be able to state:

1. The problem I observe is...
2. I believe it happens because...
3. I will measure it using...
4. The alternatives I am considering are...
5. My provisional decision is... because...

## Guiding principle

> AI produces volume. The engineer remains responsible for judgment.

---

# 30. Record Failures and Negative Results

The repository should preserve useful failures.

Examples include:

- an optimization that produced no measurable benefit;
- a hypothesis that was disproven;
- a cache that reduced correctness;
- retries that increased saturation;
- an abstraction that made the code harder to evolve;
- horizontal scaling that moved the bottleneck to the database.

Negative results demonstrate engineering maturity when they are analyzed honestly.

They prevent repeated mistakes and show that decisions are based on evidence rather than confirmation bias.

## Guiding question

> What did this failed approach teach us, and under which conditions might it still be valid?

---

# 31. Distinguish Laboratory Constraints From Business Constraints

A laboratory can simplify concerns that a production system cannot ignore.

Examples include:

- availability requirements;
- compliance;
- operational staffing;
- cloud cost;
- disaster recovery;
- support procedures;
- data retention;
- regulatory obligations;
- deployment frequency;
- organizational structure.

Every significant conclusion should acknowledge whether it is based on:

- a technical experiment;
- a laboratory assumption;
- a simulated business requirement;
- a realistic production constraint.

## Guiding question

> Would this decision remain valid in production, and which additional constraints would need to be evaluated?

---

# 32. Stop When the Learning Objective Has Been Met

A challenge should not continue indefinitely.

Once the intended capability has been demonstrated, remaining improvements should be recorded rather than automatically implemented.

Possible follow-up work may belong to:

- another challenge;
- a future roadmap stage;
- a documented limitation;
- an intentionally rejected improvement.

Finishing a small, well-documented experiment is more valuable than continuously expanding its scope.

## Guiding question

> Has this challenge already produced enough evidence to support its intended conclusion?

---

## Decision Checklist

Before approving a significant change, answer the following questions:

1. What problem are we solving?
2. What evidence proves that the problem exists?
3. What are the current constraints?
4. What alternatives were considered?
5. Why is this the smallest adequate intervention?
6. What new complexity does it introduce?
7. What failure modes does it create?
8. Which correctness guarantees must be preserved?
9. How will the result be measured?
10. How reversible is the decision?
11. Does the change belong in this challenge?
12. Can the final decision be explained clearly to another engineer?

A change that cannot answer these questions may not be ready for implementation.

---

## Principle Enforcement

These principles should be used during:

- challenge design;
- architecture discussions;
- pull-request reviews;
- ADR creation;
- performance analysis;
- retrospectives;
- AI-assisted implementation.

Pull-request reviews should identify which principle is affected when raising an architectural concern.

Examples:

> This introduces speculative generality and conflicts with Principle 25.

> The optimization has no reproducible baseline and conflicts with Principle 3.

> The retry policy does not establish idempotency and conflicts with Principles 11 and 13.

The principles themselves may evolve.

Any substantial change should be justified by experience gained during the laboratory.
