# GildMark — The Problem Worth Solving

*A domain perspective from the architect*

---

For decades, the software industry has sold specialty contractors on the same promise: organize your business into modules, and the modules will tell you the truth about your business.

Accounting. Purchasing. Inventory. Payroll. Projects. Service. Each module became the system of record for its portion of the business. The ERP's job was to coordinate them.

It was a reasonable architecture for its time.

But it created a permanent problem that every contractor CFO and owner I have worked with has learned to live with, usually without recognizing it as an architectural failure rather than a software limitation.

The business experiences a purchase order, a receipt, an invoice, a payment, a project, and a service visit as a single continuous process. The ERP experiences those same events as a series of transactions crossing module boundaries. Each module maintains its own records, its own workflow, and its own interpretation of reality.

As organizations grow, the cost of maintaining consistency between those interpretations grows with them.

Reconciliation becomes a business process. Synchronization becomes a business process. Data correction becomes a business process.

Organizations spend enormous effort proving that multiple systems agree with one another — effort that produces nothing, creates no value, and exists entirely because the governing model was wrong from the start.

I spent more than two decades inside this problem, implementing and supporting ERP software for specialty contractors across the United States and Canada. HVAC, refrigeration, plumbing, electrical, mechanical — organizations operating simultaneously across construction, field service, and preventive maintenance. I watched the same failures repeat, in different software, at different scales, with different teams. After long enough, the pattern becomes impossible to ignore.

The failures are not random. They are structural. And they trace back to the same root: a system organized around modules cannot reliably govern the lifecycle of operational reality.

---

## The WIP Schedule Nobody Trusts

Every specialty contractor with a bonding relationship produces a WIP schedule. Most of them spend the better part of a week getting it right.

The problem is not that the data is hard to gather. The problem is that the underlying cost-to-date figures — the numbers the WIP schedule is built on — are wrong in ways the system cannot detect.

A subcontract invoice posts without a job code. An inventory issue loses its cost code in transit. A labor burden leg strips its job dimension somewhere between the timesheet and the ledger. A field purchase gets coded to overhead because the technician didn't know the job number. Each one is a cost that exists in the ledger but doesn't appear on the job.

The WIP schedule shows what the system captured. It does not show what the job actually cost. The gap between those two numbers is what the accounting team spends three days closing — manually, every month, under deadline pressure, knowing they will do it again next month.

This is not a discipline problem. I have watched disciplined accounting teams fight this battle for years without winning it. It is an architectural problem. The system has no mechanism to ensure that a cost posting reaches the job it belongs to. That responsibility falls entirely on the user at the point of entry, and no user-dependent control survives contact with the operational pace of a busy contractor.

The correct solution is not a better checklist. It is a system where a cost that belongs to a job cannot reach the ledger without the job attached. Where cost dimensioning is enforced at the posting gate, not requested at the data entry screen. Where the WIP schedule is a report, not a reconciliation exercise.

---

## The Month-End Scramble

Ask any contractor controller what month-end close looks like. The answer is usually some version of the same story.

There is a checklist. The checklist has items that depend on other people — project managers who haven't updated their forecasts, field supervisors who haven't approved timesheets, accounts payable clerks who are waiting on vendor invoices that may or may not arrive before the cutoff. The controller works through the list, makes judgment calls about what to accrue and what to defer, closes the period, and then waits.

The waiting is for the reconciling items. The subcontract invoice that arrived a week after close and has to go into next month. The payroll accrual that was slightly wrong because the cutoff was a day off. The WIP adjustment that changes a job's percentage of completion and requires a revenue correction.

None of this is avoidable in the conventional model, because the conventional model puts the controller in the position of manually verifying conditions that the system should be tracking automatically. Is every open job properly dispositioned? Has every unvouchered payable been recorded? Are payroll accruals complete? The controller has to know the answers to these questions, and find them, and verify them, under time pressure, every single month.

The cost of this is real and it compounds. Reconciling items consume time. Late adjustments create restatements. Restatements create questions from lenders, bonding companies, and owners. And none of it produces anything — it is pure overhead created by a governing model that treats period close as a procedure rather than a state.

A period that is ready to close is in a different state than a period that is not. That difference should be visible to the system — not reconstructed by the controller from a checklist.

---

## The Field Purchase Black Hole

A technician is on a job site. A part fails. The supply house is four miles away. The technician goes, buys the part, puts it on the company card, and finishes the job.

In a well-run contractor organization, this happens dozens of times a week. It is not an exception to the process. It is the process — the operational reality of field service, where the dispatch model requires technicians to make purchasing decisions without time to go through a procurement workflow.

The accounting problem starts when that field purchase tries to make it back to the job.

Sometimes it doesn't. The receipt goes in a glove compartment. The expense report arrives three weeks later, coded to a general overhead account because the technician didn't remember the job number. The cost lands somewhere in the ledger, but not on the job it belongs to. The job closes with understated cost. The margin looks better than it was.

Sometimes it arrives late and coded wrong. The AP clerk processes it against the closest job they can find. The job it actually belongs to never sees the cost.

Sometimes it gets coded correctly but too late — after the period closed, after the WIP schedule was produced, after the billing went out. The cost appears in the next period's job cost report as a prior-period item that nobody can explain.

The conventional ERP response to field purchasing is accommodation — a bypass flag, a quick-entry shortcut, a tolerance setting that allows unmatched invoices through. These responses preserve the appearance of procurement process while abandoning the substance of it. The cost is in the system, somewhere. Whether it is on the right job, in the right period, with the right cost code, is another question.

The correct response is to treat the field purchase as a legitimate operational event with its own document type, its own workflow, and its own accounting path — one that acknowledges the bypass while preserving the controls. The field purchase happened. The question is how to bring it into the system with accountability intact, not how to make the system look the other way.

---

## The Tech Profitability Report Nobody Trusts

Every service contractor manager has asked for a tech profitability report. Most have received one. Almost none of them trusted it.

The problem is not the report. The problem is what is underneath it.

A standalone work order gets dispatched. Two techs go out on day one — one diagnoses, one assists. A third returns on day two to complete the repair. Materials get pulled from the truck on both visits. A parts order gets placed specifically for this job. The repair holds, but three weeks later there is a callback — another tech, another visit, warranty cost that has to land somewhere.

The owner wants to know which tech was profitable. The question sounds simple. The data problem underneath it is not.

It actually contains two distinct problems that require separate answers. The first is cost attribution — which costs belong to which tech, at which visit, on which dispatch. Labor is tractable. But materials, field purchases, and subcontractor costs hit the job without a visit or tech reference attached. The attribution is lost before the cost reaches the ledger.

The second is margin credit — even with perfect cost attribution, who gets credit for the non-labor revenue? The tech who diagnosed? Who pulled parts? Who closed the dispatch? This is a policy decision, not a data problem, and different contractors run genuinely different policies based on how they want to drive behavior.

Legacy construction accounting systems were never designed with a dispatch entity — a discrete unit of work assigned to a site, with individual tech visits underneath it. Materials hit the job. Labor hits the job. The dispatch, the visit, the individual tech — these are operational concepts the financial layer has no awareness of.

Every tech profitability report built on a legacy system is built on cost data that has already lost its attribution. Someone wrote a query against aggregated job cost, divided by labor hours, and called it a tech profitability report. It is not. It is an approximation — and every experienced contractor manager knows it.

The prerequisite for a correct tech profitability report is cost data attributed at the right grain before it hits the ledger. That is a design decision, not a reporting decision. It cannot be fixed after the fact.

---

## The Liability Nobody Can See

A salesperson closes a $2M mechanical contract in March. Somewhere in a spreadsheet, a commission accrues. Whether it gets paid — and when — depends on whoever remembers to look at the spreadsheet.

A project manager delivers a job at 14% gross margin against a 10% target. The profit bonus conversation happens at year-end. By then nobody agrees on what the number should have been or what was promised.

A controller reviewing the balance sheet for a bank covenant sees no accrued liability for performance compensation — because there isn't one. The obligation exists. The books don't reflect it.

This is not a reporting problem. It is an accounting problem.

The obligation is real from the moment the trigger fires — contract signed, job closed, dispatch completed. The timing of recognition is not a judgment call. The liability exists whether the system knows about it or not. Every contractor who has navigated an audit, a bank covenant review, or a year-end compensation dispute knows what it costs when that liability is invisible until someone remembers to pay it.

The pattern across all five of these situations is the same. The operational reality exists. The system doesn't know. The gap between what is true and what is recorded is filled by human effort — checklists, spreadsheets, reconciling items, year-end conversations. That effort is not a sign of a disciplined organization. It is the cost of a governing model that was never designed to track operational truth.

---

## A Different Premise

GildMark begins from a different premise.

The objective of an organization is not to maintain modules. The objective is to govern the lifecycle of operational reality.

A purchase order is not an accounts payable event. A material receipt is not an inventory event. A customer invoice is not an accounts receivable event. These are lifecycle events in the evolution of a business process — and the system's job is to govern that lifecycle, not to record transactions against module boundaries.

In a lifecycle-governed system, a job does not close because someone runs a close procedure. The transition to closed cannot occur until every outstanding obligation has reached terminal state — costs recognized, retainage released, warranty reserve established, subcontract and purchase commitments reconciled, unused material returned to inventory. The system enforces the conditions. The user initiates the transition when the conditions are met.

A period does not close because an accounting manager works through a checklist. It closes because the system can verify that every open job is properly dispositioned, every unvouchered payable recorded, every payroll accrual posted, every WIP adjustment made. Incomplete conditions surface as blocking states, not as reconciling items discovered after the fact.

A field purchase does not route through a bypass flag. It routes through a named document type with its own approval workflow, its own accounting path, and its own audit trail — because field purchasing is a legitimate operational event that deserves a legitimate system response.

A tech profitability report is not built on aggregated job cost divided by labor hours. It is built on cost data attributed at the dispatch and visit grain, permanently, at posting time, because the data model was designed with dispatch as a first-class entity from the start.

A performance compensation obligation does not appear on the books when someone remembers to pay it. It appears when the trigger fires — because the liability is real from that moment, and the system's job is to reflect reality.

Accounting is not the objective. Accounting is the consequence.

The primary artifact is operational truth. When the system governs lifecycle reality correctly, accounting emerges from it accurately — not as a module that has to be reconciled against the others, but as a direct expression of what actually happened.

That is what GildMark is designed to be.

---

*Brian J. Dughi is the architect of GildMark. He brings more than twenty-five years of specialty contractor ERP experience to its design — implementing, supporting, and ultimately rethinking the software that serves this market.*