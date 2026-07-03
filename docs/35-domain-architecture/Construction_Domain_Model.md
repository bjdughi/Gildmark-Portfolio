# Construction_Domain_Model.md

**Document Type:** Portfolio
**Knowledge Domain:** Domain Architecture
**Status:** Draft
**Authority:** Business_Lifecycle_Model.md
**Question Answered:** *How is the specialty contractor business represented within the Gildmark architecture?*

---

# Purpose

This document defines how the specialty contractor business is represented within the Gildmark architecture.

The Construction Domain Model applies the general architectural concepts established throughout the portfolio to a specific enterprise domain.

Rather than treating construction accounting, project management, procurement, labor, and financial reporting as independent applications, the architecture represents them as cooperating operational responsibilities participating in a common business lifecycle.

---

# Architectural Philosophy

Construction businesses exist to deliver projects.

Every operational activity ultimately supports that objective.

Contracts authorize work.

Projects organize execution.

Resources perform work.

Materials are consumed.

Labor is applied.

Costs accumulate.

Revenue is earned.

Cash is collected.

Financial reporting communicates the consequences.

The architecture therefore models project delivery as the organizing principle of the enterprise rather than accounting or departmental structure.

---

# Business Objective

The primary business objective is successful project delivery.

Every operational domain contributes to that objective through governed responsibilities.

No individual domain represents the business in isolation.

Operational success emerges through coordinated lifecycle progression across multiple domains.

---

# Core Business Domains

The specialty contractor enterprise is represented through several cooperating business domains.

## Customer Relationship

Represents prospective and existing customer relationships.

Provides the business opportunity from which contractual work originates.

---

## Contract Administration

Governs contractual obligations, pricing, amendments, and commercial commitments.

Contracts establish the operational authority to perform work.

---

## Project Delivery

Represents the execution of contracted work.

Projects coordinate operational activity while remaining governed by explicit lifecycle progression.

Project delivery serves as the operational center of the enterprise.

---

## Resource Management

Represents the operational resources required to execute projects.

Resources include:

* labor
* materials
* equipment
* subcontractors

Resource consumption reflects operational progress rather than accounting activity.

---

## Procurement

Obtains the resources necessary to execute projects.

Procurement converts operational demand into governed purchasing activity.

---

## Operational Cost

Represents the accumulation and attribution of costs resulting from governed operational activity.

Cost follows operations.

It does not define them.

---

## Financial Representation

Communicates the financial consequences of project execution.

Financial representation includes:

* receivables
* payables
* payroll
* inventory valuation
* general ledger
* financial reporting

Financial representation remains downstream of operational reality.

---

# Operational Progression

Construction work evolves through a governed lifecycle.

A simplified progression may resemble:

```text
Business Opportunity
        │
        ▼
Contract
        │
        ▼
Project
        │
        ▼
Resource Planning
        │
        ▼
Operational Execution
        │
        ▼
Progress Recognition
        │
        ▼
Financial Recognition
        │
        ▼
Project Close
```

Each stage contributes to Operational Truth.

Each stage is independently governed.

---

# Operational Documents

Business progression is expressed through governed operational documents.

Examples include:

* contracts
* change orders
* purchase orders
* receiving documents
* labor entries
* equipment usage
* production records
* applications for payment
* customer invoices
* vendor invoices
* payment records

These documents collectively describe the operational history of the enterprise.

---

# Operational Truth

Operational Truth represents the authoritative understanding of project execution.

Examples include:

* what work has been authorized
* what work has been performed
* what resources have been consumed
* what obligations have been created
* what revenue has been earned
* what costs have been incurred

Operational Truth therefore reflects project reality rather than accounting balances.

---

# Relationship to Financial Representation

Financial reporting is derived from governed operational activity.

Project execution produces:

* costs
* revenue
* receivables
* payables
* payroll obligations
* inventory movement
* general ledger activity

Financial information communicates the economic consequences of project execution.

It does not govern project execution.

---

# Architectural Characteristics

The Construction Domain Model exhibits several defining characteristics.

It is:

* project-centric
* lifecycle-governed
* document-driven
* operationally authoritative
* financially derived
* state-governed
* traceable

These characteristics reflect the architecture rather than the accounting practices of the construction industry.

---

# Scope

This document defines the enterprise business model for specialty contractors.

It does not define:

* accounting procedures
* estimating methodology
* scheduling practices
* implementation details
* service architecture
* individual lifecycle models

Those concerns are addressed within subsequent Platform Architecture, Engineering, and Evidence documentation.

---

# Relationship to the Portfolio

The preceding Domain Architecture documents establish how businesses, documents, and lifecycles are represented within Gildmark.

This document applies those concepts to the specialty contractor industry, demonstrating how the architectural model realizes a complex enterprise domain without altering its governing principles.

Subsequent Engineering and Evidence documents illustrate how these architectural concepts are implemented and validated throughout the platform.
