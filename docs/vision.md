# Project Vision

## Distributed Systems Engineering Lab

Distributed Systems Engineering Lab is a progressive software engineering laboratory created to study how backend systems behave, scale, degrade, recover, and evolve.

The project starts from a deliberately simple application and introduces new technical challenges one at a time. Each challenge represents a realistic engineering problem involving areas such as performance, concurrency, communication, consistency, resilience, messaging, scalability, or observability.

The purpose is not to build the most feature-rich application possible. The purpose is to develop and demonstrate the reasoning required to make sound technical decisions.

---

## About me

My name is Gonzalo Juez and I'm a software eingineer from Burgos, Spain.

As many, I fell in love with coding because it allowed me to create a solution from scratch with just a computer.

---

## Motivation

Many personal software projects demonstrate that their author can implement features using a particular framework.

This repository aims to demonstrate something different:

- the ability to identify technical problems;
- the discipline to measure before changing a system;
- the ability to formulate and validate hypotheses;
- the evaluation of multiple possible solutions;
- the understanding of architectural trade-offs;
- the capacity to explain why additional complexity is or is not justified;
- the ability to communicate technical decisions clearly.

The project is part of a long-term self-learning process focused on progressing from backend development toward technical leadership and architecture responsibilities.

---

## Core Approach

The system will evolve through a sequence of reproducible engineering challenges.

Each challenge will follow the same general cycle:

1. Introduce or identify a concrete problem.
2. Define the expected impact.
3. Establish a measurable baseline.
4. Formulate a hypothesis about the cause.
5. Consider alternative solutions.
6. Make and document a technical decision.
7. Implement the selected solution.
8. repeat the original experiment;
9. Compare the results.
10. Document trade-offs, limitations, and lessons learned.

New infrastructure, patterns, or technologies will only be introduced when they solve an explicit problem.

The repository will therefore preserve not only the final solution, but also the reasoning and evidence behind its evolution.

---

## What This Repository Should Demonstrate

Over time, the repository should provide evidence of competence in the following areas:

### Engineering reasoning

The ability to move from symptoms to evidence, from evidence to hypotheses, and from hypotheses to validated decisions.

### Performance analysis

The ability to define meaningful metrics, reproduce bottlenecks, identify their causes, and verify whether an optimization has produced the expected result.

### Architectural decision-making

The ability to compare alternatives based on their benefits, costs, risks, operational impact, and suitability for the current context.

### Distributed systems fundamentals

An understanding of the consequences of network communication, partial failure, concurrency, asynchronous processing, message delivery, data consistency, and horizontal scaling.

### Resilience

The ability to design systems that handle latency, transient errors, unavailable dependencies, duplicate operations, and degraded conditions.

### Observability

The ability to understand system behavior through structured logs, metrics, traces, experiments, and reproducible evidence.

### Technical communication

The ability to explain a problem, defend a decision, document trade-offs, and make the experiment understandable to another engineer.

### Incremental design

The discipline to prefer the simplest adequate solution and introduce complexity only when its value can be justified.

---

## Intended Audience

This repository is primarily a learning environment, but it is also designed to be reviewed by:

- backend engineers;
- technical leads;
- software architects;
- engineering managers;
- interviewers evaluating senior engineering capabilities;
- developers interested in distributed systems using .NET.

A reader should be able to understand not only what was implemented, but why the system evolved in that direction.

---

## Scope

The laboratory will use a fictional B2B commerce domain as the context for its experiments.

The initial implementation will be intentionally small and will begin as a single deployable backend application with a relational database.

Possible future challenges may involve:

- latency and throughput;
- database access and indexing;
- concurrency and resource contention;
- caching;
- synchronous and asynchronous communication;
- message delivery guarantees;
- idempotency;
- eventual consistency;
- failure isolation;
- retries, timeouts, and circuit breakers;
- horizontal scaling;
- distributed tracing;
- load testing;
- controlled failure experiments.

This list represents possible areas of exploration, not technologies that must be introduced.

Every addition must be justified by a concrete challenge.

---

## Non-Goals

This repository is not intended to be:

- a production-ready commercial platform;
- a complete B2B commerce product;
- a collection of unrelated technology demonstrations;
- a showcase of the largest possible number of tools;
- a microservices template;
- an attempt to apply every known software pattern;
- a framework-specific reference architecture;
- a substitute for production experience.

The project should not introduce distributed architecture merely to claim that it uses microservices.

A well-designed monolith is preferable to an unjustified distributed system.

---

## Technology Direction

The initial technology stack will be based on:

- C#;
- .NET;
- ASP.NET Core;
- MySQL;
- Docker;
- automated testing;
- reproducible local environments.

Additional technologies may be introduced in later challenges, but they are not part of the project vision by default.

The lessons obtained from the project should remain transferable to other languages, frameworks, database systems, and cloud platforms.

---

## Definition of Success

The project will be considered successful if it progressively demonstrates that its author can:

1. explain the behavior of the system;
2. identify relevant risks and bottlenecks;
3. measure problems instead of relying only on intuition;
4. compare technically valid alternatives;
5. make proportionate architectural decisions;
6. verify the consequences of those decisions;
7. communicate findings clearly;
8. recognize when additional complexity is not justified;
9. reproduce experiments reliably;
10. defend the final decisions in a technical interview or design discussion.

The value of the repository will not be measured by the number of services, dependencies, patterns, or lines of code it contains.

Its value will be measured by the quality of the engineering decisions it records.

There will be no failure in this project, only the chance to learn, adapt and grow.
