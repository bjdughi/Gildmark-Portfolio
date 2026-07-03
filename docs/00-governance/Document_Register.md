# Document_Register.md

**Document Type:** Source
**Knowledge Domain:** Governance
**Status:** Draft
**Authority:** Documentation_Architecture.md
**Question Answered:** *What documents comprise the Gildmark Portfolio?*

---

# Purpose

This document is the authoritative register of all governed documents within the Gildmark Portfolio.

It provides a single source of truth for document identity, ownership, lifecycle status, and architectural placement.

The Document Register governs the existence of documents rather than their contents.

---

# Objectives

The Document Register exists to:

* establish the canonical inventory of portfolio documents
* assign architectural ownership
* prevent duplicate or orphaned documents
* support navigation
* track document maturity
* provide traceability throughout the documentation architecture

---

# Register Structure

Each registered document shall include the following information.

| Field              | Description                                             |
| ------------------ | ------------------------------------------------------- |
| Document ID        | Unique identifier                                       |
| Title              | Canonical document title                                |
| Knowledge Domain   | Owning knowledge domain                                 |
| Parent Document    | Immediate architectural parent                          |
| Knowledge Type     | Concept, Principle, Decision, Evidence, etc.            |
| Governing Question | The single question answered                            |
| Authority          | Source, Portfolio, Evidence                             |
| Status             | Draft, Working, Reviewed, Accepted, Canonical, Archived |
| Dependencies       | Required supporting documents                           |
| Evidence Required  | Yes / No                                                |
| Notes              | Optional governance notes                               |

---

# Authority Levels

Documents belong to one of three authority levels.

## Source

Defines the portfolio architecture itself.

Examples:

* Documentation Architecture
* Knowledge Architecture
* Repository Architecture
* Knowledge Domain Register
* Document Register
* Evidence Model

---

## Portfolio

Communicates the architecture, engineering, and philosophy of Gildmark.

Most documents within the portfolio belong to this authority level.

---

## Evidence

Provides objective support for portfolio claims.

Evidence documents should remain descriptive rather than interpretive.

---

# Document Register

## Source Documents

| ID      | Title                      | Domain     | Parent  | Status  |
| ------- | -------------------------- | ---------- | ------- | ------- |
| SRC-001 | Documentation_Architecture | Governance | —       | Draft   |
| SRC-002 | Knowledge_Architecture     | Governance | SRC-001 | Draft   |
| SRC-003 | Repository_Architecture    | Governance | SRC-001 | Draft   |
| SRC-004 | Knowledge_Domain_Register  | Governance | SRC-002 | Draft   |
| SRC-005 | Document_Register          | Governance | SRC-001 | Draft   |
| SRC-006 | Evidence_Model             | Governance | SRC-001 | Planned |

---

## Portfolio Documents

Initially empty.

Documents are added only through governance.

---

## Evidence Documents

Initially empty.

Evidence is registered when promoted into the governed portfolio.

---

# Registration Rules

Every governed document shall:

* appear exactly once in this register
* possess a unique identifier
* belong to exactly one knowledge domain
* have exactly one architectural parent
* declare one governing question
* declare one authority level
* possess one lifecycle status

Documents not present within this register are not considered part of the governed portfolio.

---

# Lifecycle Status

Every document shall exist in exactly one lifecycle state.

* Planned
* Draft
* Working
* Reviewed
* Accepted
* Canonical
* Archived

Status reflects governance maturity rather than writing completeness.

---

# Identifier Convention

Identifiers are permanent.

Identifiers shall never be reused.

Suggested prefixes include:

| Prefix | Purpose                  |
| ------ | ------------------------ |
| SRC    | Source documents         |
| GOV    | Governance documents     |
| EXE    | Executive Narrative      |
| ARC    | Architectural Foundation |
| PLA    | Platform Architecture    |
| ENG    | Engineering              |
| EVD    | Evidence                 |
| PRO    | Professional Assets      |

Identifiers remain stable regardless of filename changes.

---

# Register Maintenance

The Document Register shall be updated whenever:

* a document is introduced
* a document changes status
* a document is superseded
* a document is archived
* a document changes architectural ownership

Changes to this register shall follow the governance process defined by the Documentation Architecture.

---

# Register Invariants

The Document Register shall satisfy the following invariants:

1. Every governed document appears exactly once.
2. Every document possesses a permanent identifier.
3. Every document belongs to exactly one knowledge domain.
4. Every document has exactly one architectural parent.
5. Every document answers exactly one governing question.
6. Every document exists in exactly one lifecycle state.
7. The register is the authoritative inventory of the portfolio.
