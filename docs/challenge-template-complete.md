# Challenge Template

## Purpose

This document defines the standard structure for engineering challenges in the Distributed Systems Engineering Lab.

Every challenge must document not only the final implementation, but also the engineering reasoning that led to the decision.

The objective is to preserve:

- the original problem;
- the evidence collected;
- the hypotheses considered;
- the alternatives evaluated;
- the implementation details;
- the measured results;
- the remaining limitations.

A challenge is successful when another engineer can understand:

- what problem existed;
- why it mattered;
- how it was measured;
- why a decision was made;
- what trade-offs were accepted;
- how to reproduce the experiment.

The repository should demonstrate engineering judgement, not only technical execution.

---

# Challenge Metadata

## Title

[Challenge name]

## Status

Possible values:

- Proposed
- In Progress
- Completed
- Superseded
- Rejected

Current status:

```text
[Status]
```

## Timeline

Started:

```text
YYYY-MM-DD
```

Completed:

```text
YYYY-MM-DD
```

## Related Roadmap Stage

```text
Stage X - Name
```

## Related ADRs

```text
ADR-XXXX - Title
```

---

# 1. Context

## Current Situation

Describe the system before any modification.

Include:

- current architecture;
- affected components;
- existing behaviour;
- known limitations;
- relevant constraints.

Do not describe the solution here.

The purpose of this section is to make the initial state understandable without assuming prior knowledge of the repository.

---

# 2. Problem Statement

## Problem

Describe the problem that triggered this challenge.

Explain:

- what is happening;
- how it is observed;
- why it matters;
- who or what is affected.

Avoid solution-oriented descriptions.

Bad example:

```text
We need to add Redis.
```

Better example:

```text
Repeated catalogue reads increase database load and cause response latency to grow under concurrent traffic.
```

## Impact

Explain the consequences of leaving the problem unresolved.

Possible impacts include:

- increased latency;
- reduced throughput;
- resource exhaustion;
- reliability problems;
- operational difficulties;
- increased maintenance cost;
- poor user experience;
- inability to scale under the expected workload.

---

# 3. Constraints

Document the boundaries of the challenge.

Possible constraints include:

- technology restrictions;
- available infrastructure;
- backwards compatibility;
- expected workload;
- learning objectives;
- time limits;
- intentional simplifications;
- laboratory assumptions;
- production requirements that are explicitly out of scope.

Example:

```text
The objective is to understand caching trade-offs, not to build a production-grade caching platform.
```

---

# 4. Initial Hypothesis

## Hypothesis

Describe your current belief about the cause of the problem.

Use this format:

```text
I believe that [problem] happens because [suspected cause].

If we [intervention], then we expect [measurable improvement].
```

Example:

```text
I believe that order retrieval latency is caused by unnecessary database round trips.

If we reduce the number of queries required for each request, then we expect lower p95 latency under the same workload.
```

## Confidence Level

Choose one:

- Low
- Medium
- High

Explain why.

Example:

```text
Medium confidence.

Application logs show repeated database calls, but no controlled measurement has yet isolated their contribution to total request latency.
```

## Evidence Required

Describe what evidence would support or reject the hypothesis.

Examples:

- database query count;
- execution plans;
- distributed trace duration;
- profiler output;
- resource saturation;
- latency comparison after a controlled intervention.

---

# 5. Baseline Measurement

## Objective

Define what will be measured before changing anything.

The baseline represents the current behaviour of the system and must be captured before implementing the proposed solution.

Possible metrics include:

- response latency;
- p50 latency;
- p95 latency;
- p99 latency;
- throughput;
- error rate;
- CPU usage;
- memory consumption;
- allocation rate;
- database execution time;
- database query count;
- connection-pool usage;
- queue depth;
- resource saturation.

Do not collect metrics merely because they are available. Each metric should help answer a relevant question.

## Environment

Document the conditions under which the experiment runs.

```text
Application:
.NET version:
Build configuration:
Application instances:

Database:
MySQL version:
Database configuration:

Infrastructure:
Docker version:
Container resource limits:

Dataset:
Number of customers:
Number of products:
Number of orders:
Number of order lines:

Load profile:
Concurrent clients:
Request rate:
Warm-up duration:
Measurement duration:

Machine:
Operating system:
CPU:
Memory:
```

## Experiment Procedure

Explain exactly how to reproduce the baseline measurement.

Include:

- environment startup commands;
- database initialization;
- test data generation;
- application configuration;
- load-test command;
- warm-up period;
- test duration;
- concurrency;
- assumptions;
- cleanup steps.

The procedure should be sufficiently precise for another engineer to repeat it.

## Baseline Results

| Metric | Value | Notes |
|---|---:|---|
| p50 latency | | |
| p95 latency | | |
| p99 latency | | |
| Requests per second | | |
| Error rate | | |
| CPU usage | | |
| Memory usage | | |
| Database query count per request | | |
| Database execution time | | |

## Raw Results

Reference the location of the unprocessed results.

Example:

```text
benchmarks/challenge-XXX/baseline/
```

Do not store only the final summary. Preserve enough raw evidence to verify the interpretation.

---

# 6. Alternatives Considered

Document realistic alternatives before choosing a solution.

The purpose is not to create artificial options. Include alternatives that a reasonable engineer could genuinely consider under the stated constraints.

## Option A

### Description

Describe the alternative.

### Advantages

Describe its expected benefits.

### Disadvantages

Describe its costs and limitations.

### Risks

Describe possible failure modes or incorrect assumptions.

### Operational Impact

Describe its effect on deployment, monitoring, maintenance, cost, or team responsibilities.

---

## Option B

### Description

Describe the alternative.

### Advantages

Describe its expected benefits.

### Disadvantages

Describe its costs and limitations.

### Risks

Describe possible failure modes or incorrect assumptions.

### Operational Impact

Describe its effect on deployment, monitoring, maintenance, cost, or team responsibilities.

---

## Option C

### Description

Describe the alternative.

### Advantages

Describe its expected benefits.

### Disadvantages

Describe its costs and limitations.

### Risks

Describe possible failure modes or incorrect assumptions.

### Operational Impact

Describe its effect on deployment, monitoring, maintenance, cost, or team responsibilities.

---

## Do Nothing

Explain the consequences of keeping the current implementation.

“Do nothing” is a valid alternative when the problem is not sufficiently important or the proposed complexity is disproportionate.

---

# 7. Decision

## Selected Approach

Describe the chosen solution.

Explain:

- why it was selected;
- why the alternatives were rejected;
- which assumptions make this decision valid;
- why the intervention is proportionate to the problem;
- whether the decision is reversible.

## Expected Benefits

Describe the expected improvements.

Examples:

- reduced latency;
- increased throughput;
- lower database load;
- improved isolation;
- improved resilience;
- simpler operation;
- clearer ownership.

Where possible, define a measurable expectation.

Example:

```text
Reduce p95 response latency by at least 30% under the baseline workload without increasing the error rate.
```

## Expected Costs

Describe the complexity being introduced.

Examples:

- additional infrastructure;
- operational burden;
- new failure modes;
- maintenance requirements;
- consistency implications;
- higher memory usage;
- increased deployment complexity;
- additional cognitive load.

## Accepted Trade-offs

State explicitly what is being sacrificed or relaxed.

Examples:

- fresher data in exchange for lower latency;
- implementation simplicity in exchange for higher database usage;
- lower availability in exchange for stronger consistency.

## ADR Requirement

State whether this decision requires an Architecture Decision Record.

```text
ADR required: Yes / No

Reason:
```

---

# 8. Implementation Plan

Describe the approved implementation before changing the code.

Include:

- affected components;
- expected file or module changes;
- database changes;
- configuration changes;
- infrastructure changes;
- migration requirements;
- test strategy;
- rollback strategy.

Keep the plan scoped to the challenge.

Unrelated refactoring should be excluded or recorded separately.

## Implementation Boundaries

Explicitly state what will not be implemented.

Example:

```text
This challenge will optimize the database access pattern.

It will not introduce Redis, asynchronous processing, service extraction, or changes to the public API.
```

---

# 9. Implementation

Describe what was actually changed.

Focus on engineering decisions rather than producing a commit-by-commit log.

Include:

- important code changes;
- database schema or index changes;
- configuration changes;
- infrastructure changes;
- deviations from the original plan;
- unexpected implementation difficulties.

## Tests Added or Modified

List the tests that protect the relevant behaviour.

Possible test types include:

- unit tests;
- integration tests;
- concurrency tests;
- idempotency tests;
- contract tests;
- load-test smoke checks;
- failure tests.

Explain what property each important test protects.

---

# 10. Validation

Repeat the original experiment after implementing the decision.

The validation conditions should be as close as possible to the baseline.

Any difference in environment, data, configuration, or workload must be documented.

## Validation Procedure

Reference the same procedure used for the baseline and describe any necessary differences.

## Final Results

| Metric | Before | After | Difference |
|---|---:|---:|---:|
| p50 latency | | | |
| p95 latency | | | |
| p99 latency | | | |
| Requests per second | | | |
| Error rate | | | |
| CPU usage | | | |
| Memory usage | | | |
| Database query count per request | | | |
| Database execution time | | | |

## Raw Results

Reference the location of the final unprocessed results.

Example:

```text
benchmarks/challenge-XXX/final/
```

---

# 11. Analysis

Interpret the results.

Answer the following questions:

- Was the initial hypothesis supported or rejected?
- Did the expected improvement occur?
- Was the result repeatable?
- Were there unexpected effects?
- Did another bottleneck become visible?
- Did correctness remain unchanged?
- Was the improvement worth the introduced complexity?
- Are the results large enough to be meaningful?
- Could environmental noise explain part of the difference?

Do not present correlation as causation without sufficient evidence.

A disproven hypothesis is a valid result when it is documented honestly.

---

# 12. Trade-offs

## Improvements

Describe what became better.

Examples:

- lower latency;
- higher throughput;
- reduced resource usage;
- clearer behaviour under failure;
- improved maintainability.

## Costs

Describe what became worse or more complex.

Examples:

- increased memory usage;
- greater operational burden;
- weaker consistency;
- more difficult debugging;
- additional infrastructure;
- more complex deployment.

## Conditions

Under what circumstances would this decision stop being appropriate?

Examples:

- a much larger dataset;
- a different read/write ratio;
- multiple application instances;
- stronger consistency requirements;
- limited operational capacity;
- a different failure model.

---

# 13. Limitations

Document what the experiment does not prove or solve.

Possible limitations include:

- unrealistic workload;
- simplified domain;
- limited test duration;
- hardware-specific results;
- small dataset;
- missing production traffic patterns;
- absent network latency;
- unavailable cloud infrastructure;
- lack of long-running stability tests;
- simplified security constraints.

A limitation is not a failure.

It defines the boundary within which the conclusion is valid.

---

# 14. Negative Results and Failed Attempts

Record approaches that did not work or did not produce meaningful improvement.

For each failed attempt, explain:

- what was tried;
- why it appeared reasonable;
- what result was observed;
- why it was rejected;
- under which conditions it might still be appropriate.

Negative evidence should not be removed merely to make the final result look cleaner.

---

# 15. Lessons Learned

Summarize the engineering knowledge gained.

Answer:

- What did we learn about the system?
- What did we learn about the chosen technique?
- Which assumptions were wrong?
- What would we do differently?
- Which engineering principles were reinforced?
- Which questions remain unanswered?
- Could the learning transfer to another language or platform?

Avoid reducing this section to a list of tools used.

---

# 16. Production Considerations

Clearly separate laboratory conclusions from production recommendations.

Discuss additional concerns such as:

- authentication and authorization;
- secrets management;
- sensitive data;
- monitoring and alerting;
- deployment strategy;
- rollback;
- capacity planning;
- disaster recovery;
- cloud cost;
- operational ownership;
- compliance;
- support procedures;
- service-level objectives;
- long-running reliability;
- data migration.

State explicitly whether the resulting implementation would require further work before production use.

---

# 17. Reproduction Guide

Provide everything required to repeat the experiment.

## Prerequisites

List required tools and versions.

## Setup

Provide the commands needed to prepare the environment.

```bash
# Add setup commands
```

## Generate Test Data

```bash
# Add data-generation commands
```

## Run the Baseline

```bash
# Add baseline commands
```

## Apply the Change

Explain how to switch to or build the final implementation.

## Run the Validation

```bash
# Add validation commands
```

## Clean Up

```bash
# Add cleanup commands
```

## Expected Outcome

Describe the expected shape of the results without promising exact machine-independent numbers.

---

# 18. Final Summary

Complete this section only after the challenge has finished.

## Problem

What problem was addressed?

## Hypothesis

What did we initially believe?

## Decision

What solution was selected?

## Evidence

What measurements support or reject the decision?

## Trade-offs

What costs were accepted?

## Limitations

Within which boundaries is the conclusion valid?

## Main Learning

What engineering capability was developed or demonstrated?

---

# Review Checklist

## Problem

- [ ] The current state is understandable.
- [ ] The problem is clearly described.
- [ ] The impact is explained.
- [ ] The problem is not confused with a preferred solution.
- [ ] Constraints and assumptions are explicit.

## Hypothesis

- [ ] A falsifiable hypothesis is documented.
- [ ] The expected measurable outcome is stated.
- [ ] The required evidence is identified.

## Measurement

- [ ] A baseline exists before implementation.
- [ ] Relevant metrics are defined.
- [ ] Percentiles are used where appropriate.
- [ ] The environment is documented.
- [ ] The workload is documented.
- [ ] Raw results are preserved.
- [ ] The experiment can be reproduced.

## Alternatives

- [ ] Multiple reasonable alternatives were considered.
- [ ] Doing nothing was evaluated.
- [ ] Benefits, costs, and risks are documented.
- [ ] Operational impact was considered.

## Decision

- [ ] The selected approach is justified.
- [ ] Rejected alternatives are explained.
- [ ] Expected benefits are measurable where possible.
- [ ] Introduced complexity is explicit.
- [ ] Accepted trade-offs are documented.
- [ ] ADR requirements were evaluated.

## Implementation

- [ ] The implementation remains within the challenge scope.
- [ ] Unrelated refactoring was avoided or documented.
- [ ] Important decisions are understandable.
- [ ] Tests protect relevant behaviour.
- [ ] No unnecessary technology was introduced.

## Validation

- [ ] The original experiment was repeated.
- [ ] Baseline and final conditions are comparable.
- [ ] Results are presented before and after.
- [ ] Correctness was preserved or changes were documented.
- [ ] Unexpected results were investigated.

## Conclusions

- [ ] The hypothesis was supported or rejected explicitly.
- [ ] Trade-offs are documented.
- [ ] Limitations are acknowledged.
- [ ] Negative results are preserved.
- [ ] Laboratory conclusions are separated from production guidance.
- [ ] Lessons are transferable beyond the specific technology.

## Communication

- [ ] Another engineer can reproduce the challenge.
- [ ] Another engineer can understand the decision without reading the full commit history.
- [ ] The final decision could be defended in a technical discussion.
- [ ] The challenge demonstrates engineering judgement rather than only implementation effort.
