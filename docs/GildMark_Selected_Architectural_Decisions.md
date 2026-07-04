# GildMark — Selected Architectural Decisions

This document presents four architectural decisions that illustrate GildMark's governing design philosophy. They are drawn from the full Architectural Decision Register, which contains 73 locked decisions across the platform.

These four were selected because they are simultaneously non-obvious, consequential, and grounded in the operational reality of contractor accounting. Each one represents a place where the conventional ERP approach was considered and rejected.

---

## On Operational Friction

A reasonable concern with state-governed architecture is that enforced gates will block legitimate transactions that don't conform to the expected sequence. Contractor operations are inherently messy — field purchases happen without prior authorization, subcontract invoices arrive after period close, scope changes add cost codes that weren't in the original budget. Does a system that enforces state transitions at the database level accommodate this reality, or does it impose an idealized process model that breaks under normal operating conditions?

GildMark's answer is not to soften the gates but to design the exception paths explicitly.

A field purchase that bypasses the stock pull doesn't override the negative stock constraint — it routes through a named `STOCK_OUT_VARIANCE` mechanism that preserves inventory integrity while acknowledging that the purchase happened. A late invoice that arrives after period close doesn't get a silent backdoor — it routes through a soft-close tier that requires explicit authorization and leaves a traceable record. An unbudgeted cost code on a fixed-price project doesn't get quietly accepted — it is rejected with a specific reason code, and the override hierarchy (job-level flag → company-level configuration → hard reject) gives organizations the ability to tune the gate to their operational tolerance.

The distinction the architecture enforces is not between clean operations and messy ones. It is between a named exception and an undetected error. In conventional ERP, these two things look identical — both produce a posting. In GildMark, they are different by construction. A legitimate exception routes through a named path that the system understands and records. An error is rejected at the gate with a reason code that identifies exactly what the system expected and what it received instead.

This is the property that makes the operational state model defensible in practice, not just in theory.

---

## ADR-ARCH-002 — The Single Write Path

**The decision:** `kernel.post_journal()` is the only path by which a journal entry may be written to the general ledger. No application code, stored procedure, migration script, or administrative fix may write directly to journal or posting tables. This is a constitutional constraint, not a convention.

**Why it matters:** In most ERP systems, the general ledger is a database that application code writes to through whatever path is convenient. Over time this produces a ledger that is technically balanced but not reliably auditable — because the provenance of any given entry depends on which code path wrote it, and those paths accumulate inconsistencies.

GildMark treats the posting function as a constitutional boundary. Everything that reaches the ledger passes through a single, validated, instrumented gate. The kernel does not know what kind of transaction it is processing — that is intentionally kept in the application layer — but it enforces every structural invariant on every posting regardless of source.

**The practical consequence:** There are no backdoors. An accounts payable accrual, a payroll distribution, an inventory issue-to-job, and a manual journal entry all travel the same path and face the same enforcement. A posting that would fail a structural check fails regardless of who submitted it or why.

---

## ADR-GL-001 — Posting Line Immutability

**The decision:** Once a journal entry is posted, it cannot be modified. No update, no correction, no reclassification may touch a posted line. The only correction path is reversal — an exact-negation journal with full lineage attribution — followed by a new posting.

**Why it matters:** Ledger mutability is a common ERP design compromise made in the name of operational convenience. The accounting manager who coded a transaction to the wrong job wants a simple fix. The ERP that allows it produces a ledger where the balance at any historical point in time cannot be proven to match the original posting intent.

GildMark enforces immutability at the database level via trigger — not as policy, but as physical constraint. `UPDATE` and `DELETE` on posting tables are blocked. There is no administrative override. When a correction is needed, the audit trail shows both the original error and the correction, in sequence, permanently.

**The practical consequence for contractors:** WIP schedules, job cost reports, and percentage-of-completion calculations can be trusted to reflect what was actually posted, not what someone may have quietly adjusted after the fact. This is the accounting property that makes the system's operational state model defensible.

---

## ADR-GL-005 — Default-Deny Enforcement

**The decision:** The kernel rejects by default. Any posting that fails a validation check is rejected with an explicit, stable reason code. Silent acceptance — passing a check that should fail, auto-correcting a malformed submission, or accepting ambiguous input — is prohibited.

**Why it matters:** Silent fixes in an accounting system are silent errors. An engine that accepts a structurally malformed journal and quietly adjusts it to pass validation produces a ledger that cannot be reconciled to the submitter's intent. The fix happens invisibly, the original error is gone, and the audit trail reflects a transaction that was never what anyone actually submitted.

The explicit prohibition list includes: silent auto-balancing without trace, report-time corrections, implicit default-allow behavior, and hard deletes of accounting truth. These are not edge cases — they are the standard toolkit of conventional ERP "flexibility."

**The practical consequence:** Errors surface at the source, with a specific reason code, where the submitting service has full context to correct them. The test suite requirement that reject-path tests outnumber accept-path tests reflects this discipline — the system is proven correct on failure cases, not just on the happy path.

---

## ADR-COST-001 — Per-Job Cost Dimensioning Law

**The decision:** Every cost-recognition posting leg must carry both a job identifier and a cost code. Control accounts, clearing accounts, liability accounts, and settlement accounts remain organization-level only. This is enforced at the database level via account-scoped posting rules — a posting to a direct cost account that lacks job and cost code dimensioning is rejected.

**Why it matters:** This decision closes the single most common source of WIP distortion in contractor accounting: costs that belong to a job but don't reach it.

In conventional ERP, the responsibility for attaching a job to a cost falls entirely on the user at the point of entry. A subcontract invoice posted without a job code, an inventory issue with a missing cost code, a labor burden leg that strips dimensioning in transit — each one is a cost that exists in the ledger but doesn't appear on the job. The WIP schedule is wrong. The cost-to-date figure used in percentage-of-completion calculations is wrong. The project profitability report is wrong. And none of it is visible until someone reconciles manually.

GildMark enforces job dimensioning as an architectural invariant. The six cost-recognition paths — labor, equipment, inventory issue-to-job, PO receipt direct-to-job, subcontract invoice cost leg, and landed cost on direct-to-job lines — are all required to carry job and cost code. The kernel enforces this at the posting gate; it cannot be bypassed by the application layer.

**The practical consequence:** Cost-to-date figures are complete by construction, not by discipline. A WIP schedule produced from GildMark reflects every cost that has been recognized against a job — because a cost that isn't job-dimensioned cannot reach the ledger at all.

---


---

## ADR-INV-002 — Negative Stock Hard Block

**The decision:** Negative stock is prohibited. `quantity_available` on every inventory location carries a database-level CHECK constraint (`quantity_available >= 0`). This cannot be overridden by application code, configuration, or administrative action. When a field purchase bypasses the stock pull — a technician buys material directly at a supply house — the transaction is recorded as a `STOCK_OUT_VARIANCE` shadow movement, not as a decrement below zero.

**Why it matters:** Negative stock is a common ERP accommodation made in the name of operational flexibility. The system allows a location to go negative, trusts that a receipt will arrive to correct it, and defers the cost question until reconciliation. For weighted average costing, this is not a flexibility tradeoff — it is a correctness failure. There is no mathematically valid formula for a weighted average unit cost when total quantity on hand is negative. Any system that permits negative stock under weighted average costing is producing inventory valuations that cannot be defended.

The database-level enforcement is deliberate. An application-layer check can be bypassed — by a migration, a data fix, a service that skips the validation path. A CHECK constraint cannot. The block is physical, not procedural.

**The practical consequence for contractors:** Field purchases — technicians buying materials at supply houses, from customer stockrooms, or at emergency walk-in counters — are a structural feature of contractor operations. GildMark doesn't pretend otherwise. The `STOCK_OUT_VARIANCE` mechanism handles the field purchase case explicitly: the transaction is recorded, the cost is tracked, and the variance surfaces for resolution. The inventory integrity guarantee holds regardless.

---

## ADR-INV-006 — Post-Facto PO as a First-Class Document

**The decision:** A Post-Facto PO is a purchase order created after the purchase has already occurred — to document a field purchase that bypassed the procurement workflow. It is a first-class document type with its own table and lifecycle, not a status flag on a standard purchase order and not a workaround. A single approval event satisfies all three axes of three-way match simultaneously, because for a field purchase, quantity, price, and receipt collapse to a single moment. No GR-IR accrual is created.

**Why it matters:** Every ERP that targets contractors eventually confronts the field purchase problem. A technician is on a job site, needs a part, and buys it. The standard procurement model — requisition, PO approval, receipt, invoice match — assumes a sequence that has already been violated before the system is even involved.

Most ERP responses to this problem are accommodations: a bypass flag, a "quick PO" shortcut, a tolerance setting that allows unmatched invoices through. These responses preserve the appearance of procurement process while abandoning the substance of it. The accountability structure — who approved what, at what price, against what budget — is lost.

GildMark treats the Post-Facto PO as a legitimate document type because it *is* one. The field purchase happened. The accounting question is how to bring it into the system with the appropriate controls intact. Post-Facto PO does that: it requires approval, it closes three-way match as a single event, it preserves the audit trail, and it routes the cost to the correct job and cost code. The procurement bypass is acknowledged and governed, not hidden.

**The practical consequence:** Budget overruns from field purchasing become visible and attributable. The approval requirement creates accountability without blocking the dispatch model. Job cost reports reflect field purchases at the correct cost, against the correct job, with a traceable document behind them.

---
---

## ADR-GL-003 — Period Lock Enforcement

**The decision:** Fiscal periods have three states: Open, Soft-Closed, and Hard-Closed. Period lock enforcement is the *first* step of every posting and reversal operation — before balance checks, before dimension validation, before anything else. A posting to a Hard-Closed period is rejected unconditionally. No application engine, no administrative path, and no override mechanism can bypass this check.

**Why it matters:** Period lock is the control that ensures financial statements are not retroactively altered after reporting. In most ERP systems this control lives in the application layer — which means it can be bypassed by a service that takes a different code path, a data fix that writes directly to posting tables, or an administrative function that elevates past normal controls. When the control is application-layer policy, its integrity depends on every code path respecting it.

GildMark enforces period lock at the kernel level, before any application logic runs. A closed period is physically closed — not closed-by-convention. The consequence for period close is direct: once a period transitions to Hard-Closed, the financial statements for that period are stable. Not stable-unless-someone-finds-a-workaround. Stable.

**The practical consequence for contractors:** WIP schedules and percentage-of-completion calculations depend on period integrity. A job's cost-to-date figure used in a March POC calculation must reflect March costs — not costs that were retroactively posted into March in April because the lock wasn't enforced. Period lock enforcement at the kernel level is what makes the historical record defensible.

---

## ADR-APP-007 — Budget-as-Activation: Cost Code Gate for Project Jobs

**The decision:** For project-type jobs, a cost code must be explicitly activated — budgeted — before any cost may be posted against it. The activation record is the budget entry itself. A cost code that has not been budgeted is not a valid cost destination for that job. The gate is enforced in the application layer before the posting reaches the kernel; it cannot be bypassed by posting directly.

**Why it matters:** Unbudgeted cost postings on fixed-price projects are one of the most common sources of cost overrun obscurity in contractor accounting. A technician charges labor to a cost code the project manager didn't scope. A subcontract invoice lands against a line item that wasn't in the contract. The cost reaches the job, the job cost report shows it, but the budget-vs-actual comparison is meaningless because the budget never included it.

Most ERP systems treat unbudgeted postings as a reporting problem — the cost goes in, a variance appears, someone investigates later. GildMark treats it as a state problem: the cost code isn't an active destination for this job, so the posting is rejected at the gate. The project manager's explicit budget entry is what opens the cost code for posting. No activation, no posting.

**The practical consequence:** Budget-vs-actual reporting is meaningful from day one — because the budget structure had to exist before any costs could accumulate against it. Cost overruns are visible as they happen, not reconstructed after the fact. And the state-governance model is consistent: just as a period can't receive postings it isn't open for, a cost code can't receive postings it hasn't been activated for.

---

*These decisions are drawn from GildMark's Architectural Decision Register (ADR Register v1.26, 73 locked decisions). The full register is available in this repository.*