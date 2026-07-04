# GildMark ERP

**An alternative architecture for contractor enterprise software.**

---

## What GildMark Is

GildMark is an ERP platform designed from the ground up for specialty contractors — HVAC, refrigeration, plumbing, electrical, and mechanical organizations operating simultaneously across construction, field service, and preventive maintenance.

It is not a reimplementation of conventional ERP. It is an alternative to it.

---

## The Architectural Premise

Conventional ERP governs operations through journal entries and screens. A job closes because someone runs a close procedure. A period closes because an accounting manager initiates it. The system has no opinion about whether the business is actually ready. The consequences of acting prematurely — unrecognized costs, unreleased retainage, open purchase commitments, unposted accruals — surface later as reconciling problems.

GildMark inverts that model. Operations are governed by state awareness, gates, and constraints that ensure landed postings are truthful and accurate.

Job close is a governed state transition. The transition cannot occur until every outstanding obligation has reached terminal state: costs recognized, retainage released, warranty reserve established, subcontract and purchase commitments reconciled, unused material returned to inventory. Incomplete conditions surface as blocking states at the point of transition — not as reconciling items discovered after the fact.

The same principle governs period close. The transition to a closed period cannot occur until every open job has been properly dispositioned, every unvouchered payable recorded, every payroll accrual posted, and every WIP adjustment made. The period doesn't close because someone initiates it — it closes because the system can verify that it is ready.

This is not a workflow layer built on top of a conventional ledger. It is a different governing model entirely.

---

## Where the Insight Comes From

GildMark was not designed in the abstract. It emerged from more than two decades of implementing and supporting ERP software for specialty contractors across the United States and Canada — organizations where the gap between what the system reports and what is operationally true is not a configuration problem. It is an architectural one.

Conventional ERP architecture doesn't fail these organizations because of missing features. It fails because the governing model is wrong. Journal entries and screens cannot represent the operational reality of a contractor job. GildMark is an attempt to build from a model that can.

---

## Current Implementation Status

GildMark is in architectural and design phase — there is no UI. The foundation is built as infrastructure: schema, seed, APIs, and test coverage for well-defined core subsystems.

Completed subsystems include accounts receivable, accounts payable, and inventory. The accounting kernel — double-entry ledger, immutable journal entries, and mechanically enforced posting invariants — underlies all of them.

**Current build metrics (as of July 2026):**

- 213 executed schema migrations
- 1,042 passing tests against a live database
- 73 registered architectural decisions

These numbers reflect sustained, deliberate construction — not a design exercise.

---

## Portfolio Documents

Start here for context on the problem GildMark addresses:
- [The Problem Worth Solving](docs/GildMark_Domain_Narrative.md) — a domain perspective from the architect

For the architectural reasoning behind key design decisions:
- [Selected Architectural Decisions](docs/GildMark_Selected_Architectural_Decisions.md)

For build state and evidence:
- [Technical Evidence Summary](docs/GildMark_Technical_Evidence_Summary.md)

---

## A Note on Methodology

GildMark was built using a disciplined AI-assisted engineering methodology — Claude for architectural reasoning and decision governance, Claude Code for database-grounded migration authoring. Every architectural decision is documented, every schema change is traceable, and every implementation is test-verified before it is locked.

The methodology is part of what the portfolio demonstrates.

---

*GildMark is an independent architectural initiative. It is not affiliated with any employer, past or present.*