# ADR-001: Google Sheets as the Initial Data Layer

**Status:** Accepted for MVP  
**Decision type:** Architecture / Infrastructure  
**Project:** Workforce Decision Hub

## Context

Operational applications are not always developed in environments where dedicated databases, cloud infrastructure, or custom backend services are readily available.

In enterprise settings, technical feasibility may be constrained by multiple layers of permissions, security policies, and infrastructure access. A technology can be available within an organization without being authorized for a specific business environment or application.

This project explores a scenario in which the application must be built using a limited set of accessible tools, while anticipating the operational challenges associated with growing usage and transaction volume.

## Decision

Use Google Sheets as the initial data layer and Google Apps Script as the application backend for the MVP.

This is a constraint-driven architecture decision, not an assumption that spreadsheets are the optimal long-term database solution.

## Why This Approach?

- Accessible infrastructure for rapid prototyping
- Low initial infrastructure complexity
- Native integration between Google Sheets and Apps Script
- Ability to validate business rules and workflows before introducing additional infrastructure
- Opportunity to measure the limitations of a constrained architecture

## Known Trade-offs

### Advantages

- Faster initial implementation
- Simple data inspection during development
- Minimal infrastructure setup
- Accessible tools for iterative experimentation

### Risks and Limitations

- Concurrent reads and writes may require coordination
- Execution time and service quotas can constrain throughput
- Spreadsheet operations may become costly as data volume grows
- Data integrity requires explicit application-level safeguards
- Authorization and sensitive-data handling require careful design
- Maintenance complexity may increase as workflows evolve

## Mitigation Strategy

- Centralize data access through backend functions
- Use explicit validation and server-side authorization
- Minimize unnecessary spreadsheet reads and writes
- Implement appropriate locking for conflicting operations
- Separate operational records from audit history
- Measure latency, execution frequency, and error rates
- Keep business rules independent from the storage implementation where practical

## Alternatives Considered

### Dedicated relational database

Potentially stronger transactional guarantees and scalability, but introduces additional infrastructure, configuration, and operational responsibilities.

### Managed cloud backend

May simplify authentication, persistence, and scaling, but requires evaluating access permissions, costs, security, and vendor dependencies.

### Google Sheets + Apps Script

Selected for the initial MVP because it enables the project to explore constrained development while keeping the implementation accessible.

## Review Triggers

Reevaluate the data architecture if measured results indicate:

- Unacceptable response times
- Repeated concurrent-write conflicts
- Execution or quota-related failures
- Increasing maintenance complexity
- Data consistency risks that cannot be adequately mitigated

No specific performance threshold is claimed yet. Baselines and acceptance criteria will be established through testing.

## Decision Outcome

**Accepted for the initial MVP.**

The architecture will be evaluated using synthetic data and documented performance experiments. Future migration decisions will be based on evidence rather than assumptions.

---

This document describes an independent portfolio project's architecture decision. It does not disclose or reproduce any employer or client system, internal policies, or proprietary implementation.
