# Architectural_Decision_Model.md

**Document Type:** Portfolio
**Knowledge Domain:** Architectural Foundation
**Status:** Draft
**Authority:** Architectural_Principles.md
**Question Answered:** *How are architectural decisions made and governed within Gildmark?*

---

# Purpose

This document defines the architectural decision model used within Gildmark.

The model explains how architectural principles are translated into concrete decisions, how those decisions constrain future work, and how decision quality is preserved over time.

Architectural decisions are not treated as isolated design preferences. They are governed commitments that shape the evolution of the platform.

---

# Definition

An architectural decision is a durable design commitment that constrains future implementation.

A decision is architectural when changing it would affect the structure, behavior, governance, or coherence of the platform.

Architectural decisions differ from implementation choices.

Implementation choices may change as the system evolves.

Architectural decisions define the boundaries within which implementation choices occur.

---

# Decision Philosophy

Architectural decisions exist to reduce ambiguity.

They make trade-offs explicit.

They preserve reasoning.

They prevent the same question from being repeatedly reopened without cause.

They allow the architecture to accumulate coherence over time.

A decision is valuable not only because of what it permits, but because of what it prevents.

---

# Decision Lineage

Architectural decisions should trace to governing principles.

The expected lineage is:

```text
Architectural Concept
        ↓
Architectural Principle
        ↓
Architectural Decision
        ↓
Design Pattern
        ↓
Implementation
        ↓
Evidence
```

This lineage ensures that decisions are not arbitrary.

Each decision should be explainable as the application of one or more architectural principles to a concrete design problem.

---

# Decision Criteria

A decision should be recorded as architectural when it meets one or more of the following criteria.

## Structural Consequence

The decision affects system structure, boundaries, or layering.

---

## Behavioral Consequence

The decision affects how the platform behaves or governs business activity.

---

## Data Consequence

The decision affects the meaning, ownership, immutability, or interpretation of data.

---

## Governance Consequence

The decision establishes a rule future work must obey.

---

## Reversal Cost

The decision would be expensive, risky, or conceptually disruptive to reverse.

---

## Cross-Domain Impact

The decision affects multiple services, modules, domains, or architectural layers.

---

# Decision Record

Each architectural decision should record:

* identifier
* title
* status
* domain
* governing principle
* decision statement
* rationale
* consequences
* dependencies
* evidence
* supersession relationship, if any

The purpose of a decision record is not merely to document what was chosen.

It records why the choice was made and what future work must respect.

---

# Decision Status

Architectural decisions may exist in the following states.

## Proposed

The decision is under consideration.

It may guide discussion but is not yet binding.

---

## Accepted

The decision has been reviewed and is active.

Future work should respect it.

---

## Locked

The decision is treated as a durable architectural commitment.

Reversal requires explicit architectural review.

---

## Superseded

The decision has been replaced or amended by a later decision.

It remains part of the historical record but no longer governs future work.

---

## Archived

The decision is retained for historical context but is no longer active within the current architecture.

---

# Decision Governance

Architectural decisions shall be governed explicitly.

A decision should not become binding merely because it was implemented.

Implementation may reveal a decision.

Governance confirms it.

The architecture distinguishes between accidental implementation and intentional architectural commitment.

---

# Decision Review

Architectural decision review evaluates:

* whether the decision is truly architectural
* whether it follows from governing principles
* whether alternatives were considered
* whether consequences are understood
* whether the decision conflicts with existing commitments
* whether evidence can support the decision
* whether future work can reasonably comply with it

Review is intended to preserve coherence rather than slow progress.

---

# Decision Effects

A locked architectural decision may:

* constrain implementation
* define service boundaries
* establish lifecycle rules
* govern data ownership
* prohibit certain design patterns
* require evidence
* create downstream architectural obligations

Decisions therefore function as part of the architecture, not merely commentary about it.

---

# Supersession

Architectural decisions may evolve.

When a decision is replaced, narrowed, expanded, or corrected, the change should be recorded explicitly.

Supersession preserves lineage.

It allows the portfolio to show architectural learning without erasing earlier reasoning.

Superseded decisions remain valuable because they explain how the architecture evolved.

---

# Relationship to Evidence

Architectural decisions are claims about design quality.

They should be supported by evidence.

Evidence may include:

* implementation artifacts
* service contracts
* state models
* tests
* engineering handoff records
* prior decision records
* observed design consequences

The stronger the decision's architectural consequence, the stronger its evidence requirement.

---

# Relationship to the ADR Register

The Architectural Decision Register is the governed inventory of architectural decisions.

This document defines the model.

The register records the decisions.

The model answers:

> How should decisions work?

The register answers:

> What decisions have been made?

---

# Relationship to the Portfolio

Architectural decisions are the bridge between principles and implementation.

They translate abstract architectural commitments into concrete design constraints.

Within the portfolio, architectural decisions provide some of the strongest evidence of architectural judgment because they reveal how trade-offs were identified, governed, documented, and preserved over time.
