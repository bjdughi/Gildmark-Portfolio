# Operational_Document_Model.md

**Document Type:** Portfolio
**Knowledge Domain:** Domain Architecture
**Status:** Draft
**Authority:** Business_Domain_Model.md
**Question Answered:** *What role do operational documents play within the Gildmark architecture?*

---

# Purpose

This document defines the role of operational documents within the Gildmark architecture.

Operational documents are the primary representation of governed business activity.

They authorize, record, and communicate changes in operational reality throughout the enterprise.

Within Gildmark, operational documents are not merely records of work already performed.

They are governed business entities that actively participate in lifecycle progression and contribute directly to Operational Truth.

---

# Architectural Philosophy

Business operations occur through documents.

Organizations create contracts.

Issue purchase orders.

Receive materials.

Approve invoices.

Record labor.

Submit applications for payment.

Receive customer payments.

These activities are naturally expressed through operational documents.

The architecture therefore treats documents as first-class operational entities rather than transient inputs to accounting systems.

---

# Definition

An operational document is a governed business entity representing a meaningful business action or commitment.

Every operational document:

* possesses an explicit lifecycle
* participates in governed state transitions
* contributes to Operational Truth
* may produce operational consequences
* may generate financial consequences

Documents represent business intent, execution, authorization, and completion.

---

# Operational Documents as Business Entities

Operational documents are not implementation artifacts.

They are business entities with their own operational identity.

Examples include:

* contracts
* change orders
* purchase orders
* receiving documents
* vendor invoices
* customer invoices
* payroll records
* inventory adjustments
* payment applications

Each document progresses through its own governed lifecycle.

---

# Lifecycle Governance

Every operational document is governed by explicit lifecycle state.

The lifecycle determines:

* what operations are permitted
* what approvals are required
* what downstream activities may occur
* what operational consequences result

Business correctness therefore emerges from governed document progression.

---

# Operational Consequences

Document transitions produce operational consequences.

Examples include:

* authorizing procurement
* recognizing project progress
* reserving inventory
* creating payment obligations
* recognizing revenue
* initiating payroll
* authorizing financial derivation

Consequences occur because operational reality changed.

Documents do not merely record those consequences after the fact.

---

# Relationship to Operational Truth

Operational documents contribute directly to Operational Truth.

Each governed lifecycle transition changes the enterprise's understanding of operational reality.

Operational Truth therefore reflects the cumulative progression of governed documents rather than isolated transactions.

Documents become the operational narrative of the enterprise.

---

# Relationship to Financial Representation

Financial activity is derived from operational documents.

Accounting records represent the financial consequences of governed document progression.

Financial journals therefore occupy a supporting role.

Operational documents remain the primary representation of business activity.

The architecture intentionally reverses the traditional relationship between operational documentation and accounting.

---

# Relationship to Business Domains

Each Business Domain governs the documents associated with its operational responsibility.

For example:

* Contract Administration governs contracts and amendments.
* Procurement governs purchase orders.
* Inventory governs receipts and inventory movements.
* Accounts Payable governs vendor invoices and payments.
* Accounts Receivable governs customer invoices and receipts.

Document ownership follows operational responsibility.

---

# Relationship to State Machines

Each operational document possesses an explicit lifecycle.

State machines govern document progression.

Lifecycle transitions determine:

* document validity
* operational authority
* downstream consequences
* financial derivation

State machines therefore govern documents rather than workflows.

---

# Architectural Characteristics

Operational documents exhibit several recurring characteristics.

They are:

* governed
* lifecycle-aware
* operationally significant
* traceable
* state-driven
* consequence-producing

These characteristics distinguish operational documents from reports, forms, or database records.

---

# Architectural Benefits

Treating operational documents as first-class business entities provides several advantages.

These include:

* explicit business governance
* improved operational traceability
* consistent lifecycle management
* simplified financial derivation
* reduced duplication of business logic
* explainable business history
* stronger automation opportunities
* AI-friendly operational semantics

The architecture follows the natural progression of business activity rather than reconstructing it from financial transactions.

---

# Scope

This document defines the architectural role of operational documents.

It does not specify individual document types, lifecycle models, approval policies, or service implementations.

Those concerns are defined within their respective Business Domains and Architectural Contexts.

---

# Relationship to the Portfolio

The Business Domain Model explains how enterprise responsibilities are organized.

This document explains how business activity is represented within those responsibilities.

Subsequent documents build upon this foundation by describing:

* Business Lifecycle Model
* Financial Lifecycle Model
* Construction Domain Model

Together, these documents explain how governed business activity evolves from operational intent to operational truth and ultimately to financial representation.
