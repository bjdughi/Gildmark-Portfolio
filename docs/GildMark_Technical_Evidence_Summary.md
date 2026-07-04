# GildMark — Technical Evidence Summary

**As of July 2026**

---

## What This Document Is

GildMark is an independently developed specialty contractor ERP architecture. This document summarizes the current state of the build — what is complete, what the evidence looks like, and how the work was done. It is intended for a technically sophisticated reader who wants to verify that the architectural claims made elsewhere in this portfolio are grounded in real, executed work.

---

## Build Metrics

| Metric | Value |
|---|---|
| Schema migrations executed | 213 |
| Passing tests against live database | 1,042 |
| Registered architectural decisions | 73 |
| Defined API endpoints | 322 |
| Schema tables | 238 |

These numbers reflect the state of the build at DDL head v1.1.213, test baseline 2026-07-03. The 3 non-passing tests in the full suite of 1,047 are non-regression: 2 are temporal drift artifacts (period boundary conditions that shift with calendar time) and 1 is a cosmetic wipe-header label. No functional regression exists at current head.

---

## Completed Subsystems

The following subsystems are schema-complete, API-defined, seeded, and covered by passing test suites.

**Accounting Kernel**
The foundational layer. Double-entry ledger with immutable posting lines, mechanically enforced posting invariants, single write path via `kernel.post_journal()`, period lock enforcement, reversal engine, allocation engine, and FX revaluation engine. The kernel has no knowledge of contractor business logic — domain rules live exclusively in the application layer above it.

**General Ledger Infrastructure**
Chart of accounts, accounting periods, dimensions, posting profiles, policy rules, and parties. These are the configuration surfaces the kernel operates against.

**AR Subledger**
Full accounts receivable lifecycle — invoice creation, approval routing, posting, percentage-of-completion revenue recognition, retainage split, cash receipt application, void and reversal. State machine enforced. Append-only status log. 

**AP Subledger**
Full accounts payable lifecycle — vendor invoice, three-way match, retainage split, payment run, GR/IR clearing, post-facto PO, void and reversal. 78 endpoints complete. State machine enforced. Append-only status log.

**Inventory**
Company-level weighted average costing, negative stock hard block, inventory transactions (receipt, issue-to-job, transfer, count adjustment, write-off), landed cost allocation (three trigger scenarios), reorder advice, and inventory count service. Inventory invariant gate live — account-grain GL rollup verified at every seed.

**Procurement**
Purchase order lifecycle, three-way match, vendor invoice integration, post-facto PO, commitment journal category, GR/IR clearing.

**Labor Charging**
Labor charge runs, burden engine integration, standard cost path, overhead labor charging, pay period service, payroll accrual service.

**Equipment Charging**
Equipment classes, units, rates, usage entries, and charge runs. 28 endpoints complete.

**Incentive Compensation**
Plan structure, assignment, trigger events, accrual, hold, and release. Covers salesperson commissions, project manager profit bonuses, technician productivity bonuses, estimator bid bonuses, and upsell credits. W-2 and 1099 payee paths.

**Job Module**
Job creation, lifecycle, org assignment, cost code activation (budget-as-activation gate), job type immutability, reclassification path.

**Reporting**
Trial balance, job cost summary, WIP precondition check, and WIP schedule. All four endpoints verified against live posted data.

**Infrastructure**
Auth0 M2M authentication, API versioning, idempotency enforcement, event emission (outbox pattern, Redis Streams), approval routing engine, reorg engine, tenant provisioning.

---

## What Is Not Complete

There is no UI. Four demo screens exist (Dashboard, AR Aging, Trial Balance, WIP Schedule) for demonstration purposes, but the platform has no production-ready user interface.

The service domain — field service orchestration, dispatch, visit management, and service agreements — is schema-designed and partially implemented but not complete. Technician profitability reporting depends on service domain completion.

Multi-entity consolidation, mobile/offline, and search/lineage UX are defined in the backlog but not started.

---

## How the Work Was Done

GildMark was built using a disciplined AI-assisted engineering methodology.

**Claude** (claude.ai) was used for architectural reasoning, domain intelligence sessions, decision governance, and documentation. Every architectural decision was pressure-tested in conversation before being registered in the ADR register. Domain intelligence documents — covering job types, AR, AP, inventory, procurement, payroll, incentive compensation, and approval routing — were produced through structured sessions that worked through operational reality before committing to schema decisions.

**Claude Code** was used for database-grounded migration authoring, service implementation, test authoring, and seed script development. Every migration was authored against the live schema baseline, executed, and verified before the session was closed. No migration was written speculatively.

**The governing discipline:** fix at source, never compensate. When a schema error was found, it was corrected in the source migration rather than patched by a subsequent migration. This discipline is documented in the Engineering Handoff as a standing lesson (Lesson 46 and related entries) and is reflected in the migration history — the archive contains no compensating migrations for errors that should have been caught at authoring time.

**Session close protocol:** every working session produced a session-close document capturing decisions made, migrations executed, tests passing, open items registered, and document versions updated. The Engineering Handoff is a rolling accumulation of these records, providing a complete traceable history of every build decision from the first migration to the current head.

---

## Verification

The schema baseline, migration history, ADR register, and endpoint inventory are available in this repository. The test suite runs against a live PostgreSQL database and cannot be fabricated — passing tests require a correctly provisioned schema, correctly seeded reference data, and correctly implemented service logic.

A technically sophisticated reader who wants to verify the architectural claims in this portfolio should start with the Architectural Decision Register, which contains the reasoning behind 73 locked decisions, and the Engineering Handoff, which contains the complete build history. The session-close documents referenced throughout the Handoff are the primary evidence artifacts — they record what was built, what was found, and what was decided, at the session level, throughout the construction of the platform.

---

*GildMark is an independent architectural initiative. It is not affiliated with any employer, past or present.*
