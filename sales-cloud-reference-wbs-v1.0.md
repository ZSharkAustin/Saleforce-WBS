# A Reference Work Breakdown Structure for Salesforce Sales Cloud Implementations

*A cloud-agnostic delivery core with a Sales Cloud capability module*

Version 1.0 · September 2026

---

## Why this exists

Most Sales Cloud implementations that struggle do not struggle with Salesforce. The platform work gets done. What fails is the work that was never anyone's task: the client data cleansing that was assumed, the go/no-go criteria nobody wrote until the morning of the decision, the integration user that was given administrator access because least privilege was not a line item, the success metrics that were never measured because measuring them belonged to no one.

Those are not execution failures. They are scoping failures, and they are made weeks or months before they become visible. A project plan cannot fix them, because a plan only schedules the work that someone thought to list.

A work breakdown structure is the tool that addresses this. It is a hierarchical statement of everything the project must produce, decomposed until each piece can be owned, estimated, and accepted. Its discipline comes from two rules: the children of any element add up to the whole of that element, and every piece of work lives in exactly one place. If something is not in the WBS, it is not in the project.

This document is a reference WBS: a complete starting structure to be cut down to fit an engagement, which is safer than building one up from memory. It is organized in two parts. The **core** (sections 1–9) contains the work common to any Salesforce cloud implementation. The **Sales Cloud module** (section S) contains the capability work specific to Sales Cloud. The separation is deliberate. Roughly two thirds of the effort in a typical implementation has nothing to do with which cloud is being implemented, and treating that work as reusable is what lets a delivery practice improve from one project to the next.

## How to read it

**Structure.** Three levels throughout. Level 1 is a major element of the project, level 2 a named group, level 3 a work package. Each work package is named for the thing that exists when the work is complete, not for the activity that produces it.

**A WBS is not a schedule.** Numbering implies no sequence. Change management (section 7) begins during discovery (section 2). Capability work (section S) runs alongside data migration and integration. The lifecycle view below shows how the elements overlap in time.

**Type.** `D` marks a discrete deliverable, estimated as a quantity of work. `LOE` marks level-of-effort work such as status reporting or hypercare triage, estimated as a rate sustained over a duration. Mixing the two in one estimate is a common source of overruns, because LOE work grows whenever the schedule slips.

**Side.** `P` is partner-owned, `C` is client-owned, `J` is joint. Client-owned packages are shown in bold. They are where schedules most often slip, and they are the ones most often missing from a statement of work.

**Roles.**

| Code | Role | Side |
|---|---|---|
| EL | Engagement lead | Partner |
| PM | Project manager | Partner |
| SA | Solution architect | Partner |
| BA | Business analyst | Partner |
| CON | Functional consultant or administrator | Partner |
| DEV | Developer | Partner |
| DATA | Data migration lead | Partner |
| QA | Test lead | Partner |
| OCM | Change and training lead | Either |
| SPON | Executive sponsor | Client |
| PO | Product owner with decision authority | Client |
| SME | Sales, sales operations, and IT subject matter experts | Client |
| CADM | Client Salesforce administrator, the future owner | Client |

**Sizing tiers.** Scaling notes refer to three project sizes.

| Tier | Users | Sales processes | Integrations | Data sources |
|---|---|---|---|---|
| S | Under 50 | One | Email and calendar only | One simple source |
| M | 50 to 250 | Two or three | One or two systems | One or two legacy systems |
| L | Over 250, or multiple business units | Four or more, or regional variants | Three or more, including ERP | Several, with history |

**Work package size.** At tier M, a work package should represent roughly 40 to 80 hours. Larger packages hide risk and should be split; Build packages in section S are the usual candidates, split by scope item. Much smaller packages should be merged with a sibling, because a WBS that tracks four-hour tasks has become a to-do list.

## Lifecycle view

The WBS is organized by what is produced. This view shows when.

| Stage | What is happening | Packages active |
|---|---|---|
| Mobilize | The project is set up to be governable | 1.1, 1.2, 3.1.1, 3.1.2 |
| Discover | Requirements are gathered and baselined; change work begins | 2.1–2.3, all S.n.1, 4.1, 5.1, 7.1 |
| Design | Decisions are made and recorded | All S.n.2, 3.2.1–3.2.5, 3.4, 5.2.x.1, 1.4.1 |
| Build | The solution is configured, migrated, and integrated | 3.2.6, 3.3, all S.n.3 and S.n.4, 4.2, 4.3.1, 5.2.x.2–3, 7.2.1–7.2.3, 1.4.2 |
| Validate | The whole is verified and accepted | 6.1–6.3, 4.3.2, 4.3.3, 5.2.x.4, 7.2.4 |
| Launch | Production cutover | 8.1, 8.2, 4.4, 1.4.3 |
| Sustain | The org is stabilized and handed to its owner | 9.1–9.3, 7.3 |
| Throughout | Governance | 1.3 |

Sprint-based delivery compresses Discover, Design, and Build into repeated passes, one capability or slice at a time. The packages are the same; only their grouping in time changes.

## The WBS at a glance

| ID | Element | Applies to | Indicative share of effort, tier M |
|---|---|---|---|
| 1 | Project management and governance | Any cloud | 10–14% |
| 2 | Discovery and requirements | Any cloud | 6–9% |
| 3 | Platform foundation | Any cloud | 5–8% |
| 4 | Data migration | Any cloud | 7–12% |
| 5 | Integration | Any cloud | 5–15% |
| 6 | Testing | Any cloud | 8–12% |
| 7 | Change, training, and adoption | Any cloud | 6–10% |
| 8 | Deployment and go-live | Any cloud | 2–4% |
| 9 | Hypercare and closeout | Any cloud | 4–7% |
| S | Sales Cloud capabilities | Sales Cloud | 25–35% |

The ranges are orientation, not estimates. Integration and data migration vary most, because they depend on systems outside the project's control. The figure worth noticing is the last one: the capability work that most proposals describe in detail is typically a third of the effort. The remaining two thirds is where under-scoping occurs. The section on calibrating effort describes how to replace these ranges with figures from a practice's own history.

---

# Part 1 — Core WBS

## 1. Project management and governance

### 1.1 Initiation

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 1.1.1 | Delivery handoff pack | Sales-to-delivery notes, assumption list, SOW risks | EL | D | P |
| 1.1.2 | Project charter | Charter with measurable business outcomes | PM, SPON | D | J |
| 1.1.3 | Governance model | RACI, named product owner with decision authority, escalation path | PM | D | J |
| 1.1.4 | Kickoff | Agreed ways of working | PM, EL | D | J |

Where it goes wrong: no single client product owner who can decide; success metrics written as features instead of outcomes.

### 1.2 Plan

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 1.2.1 | Baseline schedule | Milestone plan with gates and client blackout dates | PM | D | P |
| 1.2.2 | Committed resource plan | Named people and hours on both sides | PM, PO | D | J |
| 1.2.3 | RAID log | Live risk, assumption, issue, decision log | PM | D | P |
| 1.2.4 | Communication plan | Cadence, audiences, channels | PM | D | P |

Where it goes wrong: client SME time assumed, never committed.

### 1.3 Control

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 1.3.1 | Status and steering reporting | Weekly status, steerco packs | PM | LOE | P |
| 1.3.2 | Change control | Change request log with impact assessments | PM, SA | LOE | J |
| 1.3.3 | Budget and burn tracking | Burn report against baseline | PM, EL | LOE | P |

Where it goes wrong: small requests absorbed informally until the budget is gone.

### 1.4 Partner quality assurance

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 1.4.1 | Design review | Independent architect review findings, before Gate 2 | SA (not on project) | D | P |
| 1.4.2 | Build quality review | Review against partner standards, mid-build | SA (not on project) | D | P |
| 1.4.3 | Go-live readiness review | Internal readiness findings, before Gate 4 | EL, SA | D | P |

Scaling: at tier S this reduces to a single peer review, by someone not on the project, before design sign-off and again before go-live. It does not reduce to nothing.

---

## 2. Discovery and requirements (cross-cutting)

Capability-specific workshops live in the module (S.n.1). This section holds what spans capabilities.

### 2.1 Current state

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 2.1.1 | As-is process maps | Process by role, including what people actually do | BA | D | J |
| 2.1.2 | System and data landscape | Systems, interfaces, data sources | SA, SME | D | J |
| 2.1.3 | Metric baseline | Starting values for the charter's success metrics | BA | D | J |

Where it goes wrong: only managers interviewed, so the documented process is the official one.

### 2.2 Cross-cutting requirements

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 2.2.1 | KPI catalog | KPIs by audience, defined before any data model decisions | BA, SPON | D | J |
| 2.2.2 | Security and compliance requirements | Visibility rules, regulatory constraints | SA, SME | D | J |
| 2.2.3 | Integration and data requirements | Interface list, migration scope | SA, DATA | D | J |
| 2.2.4 | Non-functional requirements | Volumes, performance, availability, languages, currencies, accessibility | SA | D | J |

Where it goes wrong: reporting gathered last, after the model that must support it is fixed. The KPI catalog is first in this group for that reason.

### 2.3 Backlog baseline

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 2.3.1 | To-be end-to-end process | Future-state flow across all capabilities | BA | D | J |
| 2.3.2 | Prioritized backlog | Consolidated stories from S.n.1, MVP line, explicit out-of-scope list | PO, BA | D | J |
| 2.3.3 | Fit-gap and revalidated estimate | Fit-gap, revised estimate against SOW | SA, PM | D | P |

Where it goes wrong: nothing is ever out of scope; the estimate is never revisited after discovery.

---

## 3. Platform foundation

Everything that must exist before capability work can start.

### 3.1 Org strategy and provisioning

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 3.1.1 | Org strategy decision | Decision record: single vs. multi-org, relationship to existing orgs | SA | D | J |
| 3.1.2 | License and edition validation | Confirmation that purchased licenses support the scoped features | SA, EL | D | J |
| 3.1.3 | Production org readiness | My Domain, email deliverability, company settings, fiscal year, currencies | CON | D | P |
| 3.1.4 | Third-party package evaluation | Build-vs-buy decisions, security review of chosen packages | SA | D | J |

Where it goes wrong: a scoped feature turns out to need a license the client didn't buy, discovered mid-build.

### 3.2 Security and identity

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 3.2.1 | Sharing model design | OWD, role hierarchy, sharing rules, teams | SA | D | P |
| 3.2.2 | Persona-to-permission matrix | Permission sets and groups on minimal profiles | SA | D | P |
| 3.2.3 | Data classification and FLS design | Field sensitivity, encryption decisions | SA | D | J |
| 3.2.4 | Identity configuration | Working SSO, MFA, login policies | DEV, client IT | D | J |
| 3.2.5 | Non-human identity standard | Least-privilege pattern for integration users and agent running users | SA | D | P |
| 3.2.6 | Built security model | Roles, permission sets, and users live in sandboxes | CON | D | P |

Where it goes wrong: role hierarchy copied from the HR org chart; access opened "temporarily" in UAT and never closed; integration and agent users given admin-equivalent access.

### 3.3 Environments and release management

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 3.3.1 | Environment map | Sandbox types, purposes, refresh schedule | SA | D | P |
| 3.3.2 | Source control | Repo and branching convention | DEV, SA | D | P |
| 3.3.3 | Deployment path | Working pipeline or documented manual path | DEV | D | P |
| 3.3.4 | Seed data process | Sandbox seeding with masking | DATA, DEV | D | P |
| 3.3.5 | Release calendar | Dates clear of Salesforce seasonal releases and client blackouts | PM, SA | D | J |
| 3.3.6 | Project access register | Least-privilege project access with offboarding list | PM, CADM | D | J |

Where it goes wrong: configuration done in production on "small" projects.
Scaling: a single-builder, declarative-only tier S project can deploy with change sets from a sandbox. Anything with code, or more than one person building, uses source control. No tier configures directly in production.

### 3.4 Resilience and compliance

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 3.4.1 | Backup and restore | Chosen solution, tested restore | SA, CADM | D | J |
| 3.4.2 | Privacy and compliance review | Consent, retention, residency, and deletion handling | SA, client legal | D | J |
| 3.4.3 | Large data volume assessment | Skew, indexing, and archiving decisions (tier L, or any object over a threshold) | SA | D | P |
| 3.4.4 | Audit and monitoring setup | Field history, setup audit, event monitoring decisions | SA, CADM | D | J |

Scaling: backup (3.4.1) and the privacy review (3.4.2) apply at every tier, sized to the data involved. The large data volume assessment applies at tier L, or whenever any object is expected to reach millions of records.

---

## 4. Data migration

### 4.1 Plan

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 4.1.1 | Migration scope | What migrates, how much history, what is archived | DATA, PO | D | J |
| 4.1.2 | Source profile | Volumes, fill rates, duplicates per source | DATA | D | P |
| 4.1.3 | Mapping workbook | Field mapping and transformation rules | DATA, BA | D | J |
| 4.1.4 | Ownership map | Legacy users to Salesforce users, inactive-owner rule | DATA | D | J |

### 4.2 Prepare

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 4.2.1 | Cleansed source data | Cleansing completed to agreed thresholds, by dated assignments | SME | D | **C** |
| 4.2.2 | Load runbook | Tooling, load order, external IDs, automation bypass | DATA | D | P |

### 4.3 Rehearse

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 4.3.1 | Mock load 1 | Reconciliation report, defect list | DATA | D | P |
| 4.3.2 | Timed dress rehearsal | Full-volume load with timings for the cutover plan | DATA | D | P |
| 4.3.3 | Data acceptance | Client validation of migrated data | SME, PO | D | **C** |

### 4.4 Execute

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 4.4.1 | Production load | Loaded and reconciled production data | DATA | D | P |
| 4.4.2 | Legacy data archive | Unmigrated history preserved and retrievable | DATA, client IT | D | J |

Where it goes wrong: cleansing assigned to the client and never done; first full-volume load is the production one; automation fires on load.

---

## 5. Integration

### 5.1 Integration architecture

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 5.1.1 | Interface catalog | Direction, frequency, pattern, and system of record per field | SA | D | J |
| 5.1.2 | Integration identities | Users and named credentials per 3.2.5 | SA, DEV | D | P |
| 5.1.3 | External team commitments | Named owners, test windows, and dates from every other system's team | PM | D | **C** |

### 5.2 Interface delivery (repeat per interface: 5.2.a, 5.2.b, …)

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 5.2.x.1 | Interface specification | Spec including error handling | SA, DEV | D | J |
| 5.2.x.2 | Built interface | Working in sandbox | DEV | D | P |
| 5.2.x.3 | Monitoring and recovery | Alerts, retry process, named operational owner | DEV, CADM | D | J |
| 5.2.x.4 | Verified interface | Tested at realistic volume | DEV, QA | D | J |

Where it goes wrong: system of record never agreed per field; the other system's team is on nobody's plan.

---

## 6. Testing

Unit testing and demos live with each capability (S.n.4). This section is system-level.

### 6.1 Test foundation

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 6.1.1 | Test plan | Scope, environments, entry and exit criteria, defect-vs-change rule | QA | D | P |
| 6.1.2 | Script library | Scripts traced to acceptance criteria | QA, BA | D | J |
| 6.1.3 | Test data set | Realistic, masked data | QA, DATA | D | P |

### 6.2 System verification

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 6.2.1 | End-to-end test results | Cross-capability scenarios passed | QA | D | P |
| 6.2.2 | Security test results | Verified access per persona, including non-human identities | QA, SA | D | P |
| 6.2.3 | Performance test results | Key transactions at expected volume (tiers M and L) | QA, DEV | D | P |
| 6.2.4 | Regression suite | Repeatable suite, run after every fix release | QA | D | P |

### 6.3 User acceptance

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 6.3.1 | UAT readiness | Environment, data, scripts, briefed testers | QA, OCM | D | J |
| 6.3.2 | UAT staffing | Real end users, released from day jobs for the UAT window | PO | D | **C** |
| 6.3.3 | UAT results | Executed scripts, triaged defects, accepted outcome | QA, PO | D | J |

Where it goes wrong: testers are whoever is available; UAT becomes a second requirements phase.

---

## 7. Change, training, and adoption

### 7.1 Change

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 7.1.1 | Change impact matrix | What changes for whom | OCM | D | J |
| 7.1.2 | Sponsor action plan | Visible sponsor commitments with dates | SPON | D | **C** |
| 7.1.3 | Champion network | Named champions, involved from the first demo | OCM | D | J |
| 7.1.4 | Communication campaign | Message calendar by role | OCM | D | J |

### 7.2 Training

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 7.2.1 | Curriculum | Role-based, scenario-based | OCM | D | J |
| 7.2.2 | Training materials | Guides, videos, in-app guidance | OCM, CON | D | P |
| 7.2.3 | Training environment | Realistic sandbox | CON | D | P |
| 7.2.4 | Delivered training | Attendance and competency records | OCM | D | J |
| 7.2.5 | Admin enablement | Client admin able to own the org | CON, SA | D | J |

### 7.3 Adoption

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 7.3.1 | Adoption dashboard | Logins, data quality, process compliance | OCM, CON | D | P |
| 7.3.2 | Leadership operating rhythm | Pipeline and forecast reviews run from the system, not spreadsheets | SPON | D | **C** |
| 7.3.3 | Reinforcement program | Office hours, refreshers | OCM | LOE | J |

Where it goes wrong: managers keep their spreadsheets, which tells everyone the system is optional.

---

## 8. Deployment and go-live

### 8.1 Readiness

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 8.1.1 | Go/no-go criteria | Written and agreed well before the decision day | PM, SPON | D | J |
| 8.1.2 | Cutover runbook | Hour-by-hour, with owners; sequences 4.4.1 | PM, SA | D | J |
| 8.1.3 | Rehearsed deployment package | Validated against staging, manual steps documented | DEV, CON | D | P |
| 8.1.4 | Rollback plan | Procedure and decision point | SA | D | P |

### 8.2 Cutover

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 8.2.1 | Production release | Deployed, manual steps complete | DEV, CON | D | P |
| 8.2.2 | Activated users | Licenses assigned, users live | CADM | D | **C** |
| 8.2.3 | Smoke test results | Critical paths verified in production | QA, SME | D | J |
| 8.2.4 | Legacy read-only | Old system frozen | client IT | D | **C** |

Where it goes wrong: criteria written on the day; manual steps held in one person's head.

---

## 9. Hypercare and closeout

### 9.1 Hypercare

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 9.1.1 | Support model | Triage process, severities, exit criteria | PM | D | J |
| 9.1.2 | Triage and fix releases | Resolved issues | CON, DEV | LOE | P |
| 9.1.3 | Adoption and data quality monitoring | Weekly report | OCM, CADM | LOE | J |

### 9.2 Transition

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 9.2.1 | As-built documentation | Design document, config workbook, runbooks | SA, CON | D | P |
| 9.2.2 | Operational handover | Admin or managed-services team running the org | SA, CADM | D | J |
| 9.2.3 | Roadmap | Deferred backlog and phase 2 plan | EL, SA | D | J |
| 9.2.4 | Access removal | Partner access deprovisioned | PM, CADM | D | J |
| 9.2.5 | Legacy decommission plan | Dates and owner for shutting the old system down | client IT | D | **C** |

### 9.3 Close

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 9.3.1 | Outcome report | Success metrics measured against the 2.1.3 baseline | EL, SPON | D | J |
| 9.3.2 | Lessons learned | Internal and joint retrospectives | PM | D | J |
| 9.3.3 | Contractual close | Acceptance letter, final invoice | EL, PM | D | J |

Where it goes wrong: hypercare never ends because it has no exit criteria; nobody measures the outcome.

---

# Part 2 — Sales Cloud module

## S. Sales Cloud capabilities

### The capability pattern

Every capability S.n decomposes into the same four work packages:

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| S.n.1 | Discover | Workshop output: user stories with acceptance criteria, fed to 2.3.2 | BA, SME | D | J |
| S.n.2 | Design | Decision records and the capability's section of the solution design | SA, CON | D | P |
| S.n.3 | Build | Configured capability in the dev sandbox (split by scope item if over the sizing rule) | CON, DEV | D | P |
| S.n.4 | Verify | Unit tested, demoed to the product owner, accepted into system test | CON, PO | D | J |

This works for gated delivery (all S.n.1, then all S.n.2, and so on) and for sprint delivery (one capability or slice at a time, through all four).

Automation rule for every S.n.2: Flow only, one entry point per object, a bypass mechanism for migration and integration users, and a decision record for anything that needs code.

### Capabilities

| ID | Capability | Key design decisions (S.n.2) | Build scope (S.n.3) | Where it goes wrong |
|---|---|---|---|---|
| S.1 | Lead management | Use leads at all, or contacts only; qualification criteria; routing and SLA rules; conversion field mapping | Capture (web, import), assignment and queues, duplicate and matching rules, conversion mapping, lead Path | Conversion mapping left to defaults, so qualification data dies at conversion |
| S.2 | Account and contact management | Account hierarchy; person accounts (irreversible); contacts to multiple accounts; ownership and account teams | Record types, layouts, hierarchy, teams, duplicate rules | Person accounts enabled without understanding the consequences |
| S.3 | Opportunity and pipeline | Number of sales processes; stage definitions with exit criteria; record type strategy; teams and splits; stage-gate rules | Sales processes, stages, Path with guidance, contact roles, teams, splits, validation rules, approvals | Stages describe seller activity rather than buyer commitment; record types multiply to fix layout problems |
| S.4 | Products, pricing, and quoting | Standard quotes vs. CPQ or Revenue Cloud (separate scope); price book structure; discount authority | Products, price books, schedules, quotes, templates, discount approvals | Standard quoting stretched to do CPQ's job |
| S.5 | Forecasting | Forecast types; stage-to-category mapping; hierarchy; quota source; adjustment rights | Forecast types, hierarchy, quotas, category mapping | Category mapping debated for weeks because sales leadership was never in the room |
| S.6 | Territory management | Whether territories are needed at all; model and hierarchy; assignment rules; realignment process; territory-based access | Territory model, rules, assignment run, forecast-by-territory if used | Built for the org chart of today with no realignment process |
| S.7 | Productivity and engagement | Email and calendar integration method and its data residency implications; persona app design; mobile scope; campaigns in or out | Lightning apps and record pages per persona, activity capture, templates, mobile layouts and actions, campaigns if scoped | Activity capture chosen without understanding where the data lives and what can be reported on |
| S.8 | Analytics | KPI-to-field traceability from 2.2.1; history and snapshot needs; folder and sharing structure; standard reports vs. CRM Analytics | Custom report types, reports, dashboards by audience, snapshots | Dashboards built for the demo, not for the weekly meeting that would actually use them |
| S.9 | AI and agents | Which features, and whether data volume and quality support them; agent running-user permissions per 3.2.5; guardrails; human-in-the-loop points; monitoring | Feature setup, prompt and agent configuration, permission scoping, guardrail tests | Sold in the SOW with no data readiness check; agents given broad access because scoping was nobody's task |

---

# Part 3 — Using the WBS

## Gates

Gates are milestones, not work, so they do not appear in the WBS. Each is a decision supported by evidence from specific work packages.

| Gate | Decision | Evidence from | Decided by |
|---|---|---|---|
| 1 | Requirements baseline | 2.3.2, 2.3.3 | PO |
| 2 | Design sign-off | All S.n.2, 3.2.1–3.2.3, 5.1.1, 1.4.1 | PO |
| 3 | User acceptance | 6.3.3, 4.3.3 | PO |
| 4 | Go or no-go | 8.1.1–8.1.4, 1.4.3 | SPON, PO |
| 5 | Hypercare exit | Exit criteria in 9.1.1 met | PO |

Under sprint delivery, Gates 1 and 2 become rolling decisions taken per capability or release slice. Gates 3, 4, and 5 do not change.

A design sign-off assembled from nine capability designs is harder to hold than a single document review. A walkthrough using a working prototype, capability by capability, is more reliable than circulating a document for signature, because it produces a decision from someone who has seen what they are approving.

## Brownfield overlay

Implementing into an existing org adds work that a greenfield structure does not contain. These packages are added to the core; nothing is removed.

| ID | Work package | Deliverable | Adds to |
|---|---|---|---|
| B.1 | Org health assessment | Technical debt, automation inventory, limits usage, security posture | 2.1 |
| B.2 | Coexistence design | How new capabilities live alongside existing automation, record types, and sharing | Every S.n.2 |
| B.3 | Remediation backlog | Debt that must be cleared before build, with a decision on who funds it | 2.3 |
| B.4 | Regression baseline | Tests proving that existing functionality still works | 6.1 |
| B.5 | In-place data changes | Transformations to live data, with rollback | 4 |
| B.6 | Existing user impact | Change plan for people already working in the org | 7.1 |

B.3 is the package most often skipped and the one with the largest commercial consequence. Technical debt discovered during build is paid for by whoever did not raise it during discovery.

## The client-side view

Filtering the WBS to packages marked `C` produces the list of work the client must perform for the project to succeed:

| ID | Client-owned package |
|---|---|
| 4.2.1 | Cleansed source data |
| 4.3.3 | Data acceptance |
| 5.1.3 | External team commitments |
| 6.3.2 | UAT staffing with real end users |
| 7.1.2 | Sponsor action plan |
| 7.3.2 | Leadership operating rhythm run from the system |
| 8.2.2 | Activated users |
| 8.2.4 | Legacy system set to read-only |
| 9.2.5 | Legacy decommission plan |

Every item on this list is a dependency, and each one belongs in the assumptions section of the statement of work with an owner and a date. The joint packages deserve the same treatment for their client half, in particular the committed resource plan (1.2.2), which converts "SMEs will be available" into named people and hours.

## Calibrating effort

The indicative shares given earlier are a starting orientation. A delivery practice should replace them with its own figures as quickly as it can, and the WBS is the instrument for doing so.

1. Record actual hours against level-2 groups on every project. Level 3 is too fine to track reliably; level 1 is too coarse to learn from.
2. Record the tier and the principal effort drivers alongside the hours: number of sales processes, lead sources, interfaces, data sources, personas, and dashboards.
3. After three projects at the same tier, replace the indicative ranges with observed ones. After six, estimate capabilities from their drivers rather than from the tier.
4. Treat any project where sections 1–9 fall well below two thirds of total effort as a warning. It usually means core work was done but not recorded, or not done.

| Capability | Principal effort driver |
|---|---|
| S.1 Lead management | Number of lead sources and routing rules |
| S.2 Account and contact management | Hierarchy complexity, state of duplicates |
| S.3 Opportunity and pipeline | Number of sales processes |
| S.4 Products, pricing, and quoting | Catalog size, number of quote templates |
| S.5 Forecasting | Forecast types, hierarchy depth |
| S.6 Territory management | Rule complexity, frequency of realignment |
| S.7 Productivity and engagement | Number of personas, mobile scope |
| S.8 Analytics | Number of dashboards, history requirements |
| S.9 AI and agents | Data readiness, number of agent actions |

Integration is estimated per interface by complexity, not by tier. LOE packages are estimated as a weekly rate multiplied by duration, and re-estimated whenever the schedule moves.

## WBS dictionary template

The tables in this document are the index. For the packages that carry the most risk on a given engagement, a dictionary entry records what the table cannot.

```
ID:
Work package:
Type / Side:
Description:
Deliverable:
Owner and contributors:
Predecessors:
Entry criteria:
Exit criteria:
Effort:
Effort drivers:
Known failure mode:
```

## Extending the structure

The core was written to be independent of Sales Cloud. A module for another cloud follows the same pattern as section S: a list of business capabilities, each decomposed into Discover, Design, Build, and Verify, with its design decisions and build scope stated. The core sections, the gates, the brownfield overlay, and the client-side view apply without change.
