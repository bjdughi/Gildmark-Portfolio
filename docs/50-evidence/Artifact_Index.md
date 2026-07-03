# Artifact_Index.md

**Document Type:** Portfolio Governance
**Knowledge Domain:** Evidence
**Status:** Draft
**Authority:** Representative_Artifacts.md
**Question Answered:** *How are portfolio artifacts governed and traced throughout the documentation architecture?*

---

# Purpose

This document defines the Artifact Index for the Gildmark portfolio.

The Artifact Index provides the authoritative inventory of governed portfolio artifacts and their relationships within the documentation architecture.

Its purpose is to make every significant artifact discoverable, classifiable, and traceable.

Unlike a directory listing, the Artifact Index records the architectural role of each artifact within the portfolio knowledge model.

---

# Artifact Philosophy

Portfolio artifacts exist to communicate evidence.

Each artifact answers one architectural question.

Each artifact occupies one defined position within the documentation hierarchy.

Each artifact contributes to one or more capability claims.

Artifacts therefore function as governed knowledge assets rather than independent documents.

---

# Artifact Record

Every governed artifact should contain sufficient metadata to support discovery, navigation, and traceability.

Each record should include:

| Attribute               | Description                                                             |
| ----------------------- | ----------------------------------------------------------------------- |
| Identifier              | Unique portfolio identifier                                             |
| Title                   | Canonical document title                                                |
| Knowledge Domain        | Governing knowledge domain                                              |
| Document Type           | Governance, Narrative, Architecture, Engineering, Evidence, etc.        |
| Question Answered       | The single architectural question addressed                             |
| Authority               | Immediate parent document                                               |
| Child Documents         | Direct descendants, if any                                              |
| Status                  | Draft, Review, Approved, Archived, Superseded                           |
| Version                 | Current governed version                                                |
| Evidence Classification | Architectural, Engineering, Implementation, Validation, Evolution       |
| Capability Claims       | Professional capabilities supported                                     |
| Source Artifacts        | Documents or implementations from which the artifact derives            |
| Representative          | Indicates whether the artifact is designated as representative evidence |

These attributes provide the governance metadata necessary to manage the portfolio as a coherent knowledge architecture.

---

# Artifact Relationships

Artifacts participate in several relationship types.

## Hierarchical Relationships

Define parent and child relationships within the documentation architecture.

These relationships establish conceptual dependency.

---

## Authority Relationships

Identify the document from which architectural authority is derived.

Authority establishes governance rather than ownership.

---

## Traceability Relationships

Connect:

* concepts
* principles
* decisions
* patterns
* implementations
* evidence

These relationships allow readers to move naturally from abstract architectural ideas to concrete implementation evidence.

---

## Evidence Relationships

Associate artifacts with the capability claims they substantiate.

Evidence relationships enable reviewers to evaluate professional capability through representative artifacts.

---

# Artifact Classification

Artifacts are classified according to their primary purpose.

Recognized classifications include:

* Governance
* Executive Narrative
* Architectural Foundation
* Platform Architecture
* Domain Architecture
* Engineering
* Evidence
* Professional Assets

Each artifact belongs to exactly one primary knowledge domain.

Cross-domain references should be established through traceability rather than duplicate ownership.

---

# Portfolio Navigation

The Artifact Index serves as the primary navigation model for the portfolio.

Readers should be able to locate artifacts by:

* knowledge domain
* architectural concept
* capability claim
* evidence classification
* governing authority
* document title

Multiple navigation paths improve accessibility while preserving a single authoritative artifact.

---

# Governance Rules

Every governed artifact should satisfy the following requirements.

* Answer exactly one question.
* Possess one governing authority.
* Occupy one position within the documentation hierarchy.
* Maintain explicit parent and child relationships.
* Preserve traceability to supporting evidence where applicable.
* Avoid duplication of architectural responsibility.

These rules preserve the conceptual integrity of the documentation architecture.

---

# Lifecycle

Artifacts progress through a governed lifecycle.

```text
Proposed
    │
    ▼
Draft
    │
    ▼
Review
    │
    ▼
Approved
    │
    ▼
Representative (optional)
    │
    ▼
Archived or Superseded
```

Historical artifacts remain part of the architectural record.

The portfolio preserves lineage rather than replacing history.

---

# Example Artifact Record

The following illustrates the intended structure of an artifact record.

| Attribute               | Example                                                                   |
| ----------------------- | ------------------------------------------------------------------------- |
| Identifier              | PA-030-004                                                                |
| Title                   | State_Machine_Architecture                                                |
| Knowledge Domain        | Platform Architecture                                                     |
| Question Answered       | How are governed business lifecycles represented within the architecture? |
| Authority               | Architectural_Contexts                                                    |
| Evidence Classification | Architectural                                                             |
| Capability Claims       | Enterprise Architecture, Systems Thinking                                 |
| Status                  | Approved                                                                  |
| Representative          | Yes                                                                       |

This example is illustrative only.

The authoritative Artifact Index records the complete portfolio inventory.

---

# Relationship to the Documentation Architecture

The Documentation Architecture defines the governance model for portfolio documentation.

The Artifact Index operationalizes that model.

Together they ensure that every portfolio artifact occupies a governed position within the overall knowledge architecture.

---

# Relationship to the Portfolio

The Evidence domain concludes by establishing a governed inventory of portfolio artifacts.

Where the preceding documents explain how evidence is defined, organized, and interpreted, the Artifact Index provides the authoritative registry through which that evidence is managed.

It forms the operational backbone of the documentation architecture, enabling every architectural concept, engineering practice, implementation artifact, and capability claim to be located, governed, and traced throughout the portfolio.
