# A Reference Work Breakdown Structure for Salesforce Service Cloud Implementations

*A cloud-agnostic delivery core with a Service Cloud capability module*

Version 1.0 · September 2026

---

## Why this exists

A sales implementation replaces a tool. A service implementation replaces a running operation. The contact center is answering customers the day before cutover and must be answering them the day after, on every channel, at the same service levels, with the same people. There is no quiet period in which to go live, and when something fails the customer is the first to know.

That difference explains where service implementations go wrong. The case object is rarely the problem. The problems are a phone number that could not be ported by the cutover date because nobody knew the carrier's lead time, a routing design that worked in testing and collapsed at Monday morning volume, a knowledge base that was technically migrated and practically unusable, agents trained in a single session because nobody planned cover for the queues, and a first week of longer handle times that was read as failure because nobody had forecast it.

None of these is a platform failure. Each is work that was not in scope because nobody listed it. A work breakdown structure exists to list it: a hierarchical statement of everything the project must produce, decomposed until each piece can be owned, estimated, and accepted, under two rules. The children of an element add up to the whole of that element, and every piece of work lives in exactly one place.

This document is a reference WBS, a complete starting structure to be cut down to fit an engagement. It has two parts. The **core** (sections 1–9) contains the work common to any Salesforce cloud implementation. The **Service Cloud module** (section SV) contains the capability work specific to service. It shares its core with the companion Sales Cloud WBS, and the section below states exactly what carries over and what does not.

## What carries over from the Sales Cloud WBS

The core was designed to be independent of the cloud being implemented. Applying it to Service Cloud was the first real test of that claim. It largely held: of 103 core work packages, 96 are unchanged, 7 were reworded, and 11 were added. The additions are instructive, because every one of them traces to the same cause. Service is a live, multi-channel operation with external providers in the delivery chain.

| Section | Carries over | Service-specific additions |
|---|---|---|
| 1 Governance | Unchanged | None |
| 2 Discovery | Unchanged, non-functional requirements widened | 2.1.4 Contact demand baseline |
| 3 Platform foundation | Unchanged; license check, org readiness, and privacy review widened for channels, business hours, and recordings | 3.2.7 External access security |
| 4 Data migration | Unchanged, scope widened to case history, emails, and attachments | 4.1.5 Open-case transition plan |
| 5 Integration | Unchanged | 5.1.4 Channel provider dependencies |
| 6 Testing | Unchanged, performance test refocused on routing at peak | 6.2.5 Channel end-to-end results |
| 7 Change and training | Operating rhythm reworded for supervisors | 7.1.5 Training release schedule |
| 8 Go-live | Unchanged | 8.1.5 Rollout strategy, 8.1.6 Channel cutover plan, 8.2.5 Switched channels |
| 9 Hypercare | Unchanged | 9.1.4 Floor support, 9.1.5 Service level recovery report |
| Module | Same four-package pattern | Twelve service capabilities replace nine sales capabilities |

A program implementing both clouds uses one core, not two. The final section describes how the modules combine.

## How to read it

**Structure.** Three levels throughout. Level 1 is a major element of the project, level 2 a named group, level 3 a work package. Each work package is named for the thing that exists when the work is complete.

**A WBS is not a schedule.** Numbering implies no sequence. The lifecycle view below shows how the elements overlap in time.

**Type.** `D` marks a discrete deliverable, estimated as a quantity of work. `LOE` marks level-of-effort work, estimated as a rate sustained over a duration. LOE work grows whenever the schedule slips, and in a service go-live it also grows with the number of shifts to be covered.

**Side.** `P` is partner-owned, `C` is client-owned, `J` is joint. Client-owned packages are shown in bold.

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
| SPON | Executive sponsor, usually the head of service | Client |
| PO | Product owner with decision authority | Client |
| SME | Agents, supervisors, service operations, knowledge owners, and IT | Client |
| CADM | Client Salesforce administrator, the future owner | Client |

Telephony carriers, contact center vendors, and messaging providers are third parties. Their commitments are captured in 5.1.3 and 5.1.4 and owned on the client side, because the client holds those contracts.

**Sizing tiers.**

| Tier | Agents | Channels | Integrations | Operation |
|---|---|---|---|---|
| S | Under 25 | Email and web | None, or one lookup | Single site, business hours |
| M | 25 to 150 | Three or four, including messaging or voice | One to three, including telephony | One or two sites, extended hours |
| L | Over 150 | All, in several languages | Four or more, including order and billing systems | Multiple sites or continuous operation |

**Work package size.** At tier M, a work package should represent roughly 40 to 80 hours. Split larger ones, usually Build packages, by scope item. Merge much smaller ones with a sibling.

**Product names.** Salesforce product names have changed more than once in the past year. Capabilities here are named for what they do (messaging, voice, routing) so that the structure survives the next renaming.

## Lifecycle view

| Stage | What is happening | Packages active |
|---|---|---|
| Mobilize | The project is set up to be governable; long-lead items are started | 1.1, 1.2, 3.1.1, 3.1.2, 5.1.4 |
| Discover | Requirements and demand are baselined; change work begins | 2.1–2.3, all SV.n.1, 4.1, 5.1, 7.1 |
| Design | Decisions are made and recorded | All SV.n.2, 3.2.1–3.2.5, 3.2.7, 3.4, 5.2.x.1, 8.1.5, 1.4.1 |
| Build | The solution is configured, migrated, and integrated; content is prepared | 3.2.6, 3.3, all SV.n.3 and SV.n.4, SV.5.5, SV.8.5, SV.10.5, 4.2, 4.3.1, 5.2.x.2–3, 7.2.1–7.2.3, 1.4.2 |
| Validate | The whole is verified and accepted | 6.1–6.3, 4.3.2, 4.3.3, 5.2.x.4, 7.2.4 |
| Launch | Production cutover, channel by channel | 8.1, 8.2, 4.4, 1.4.3 |
| Sustain | Service levels recover; the org is handed to its owner | 9.1–9.3, 7.3 |
| Throughout | Governance | 1.3 |

Channel provider dependencies (5.1.4) sit in Mobilize deliberately. Number porting and messaging sender approvals run on the provider's calendar, and they are the items most likely to fix the go-live date.

## The WBS at a glance

| ID | Element | Applies to | Indicative share of effort, tier M |
|---|---|---|---|
| 1 | Project management and governance | Any cloud | 10–13% |
| 2 | Discovery and requirements | Any cloud | 6–9% |
| 3 | Platform foundation | Any cloud | 5–8% |
| 4 | Data migration | Any cloud | 5–10% |
| 5 | Integration | Any cloud | 8–18% |
| 6 | Testing | Any cloud | 9–13% |
| 7 | Change, training, and adoption | Any cloud | 8–12% |
| 8 | Deployment and go-live | Any cloud | 3–5% |
| 9 | Hypercare and closeout | Any cloud | 5–8% |
| SV | Service Cloud capabilities | Service Cloud | 25–35% |

The ranges are orientation, not estimates. Compared with a sales implementation, integration, change, go-live, and hypercare take a larger share, which follows from telephony, a shift-based workforce, and a cutover with no quiet window. Data migration is often smaller, because many organizations choose to archive closed case history instead of migrating it. The section on calibrating effort describes how to replace these ranges with a practice's own figures.

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

Capability-specific workshops live in the module (SV.n.1). This section holds what spans capabilities.

### 2.1 Current state

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 2.1.1 | As-is process maps | Process by role, including what people actually do | BA | D | J |
| 2.1.2 | System and data landscape | Systems, interfaces, data sources | SA, SME | D | J |
| 2.1.3 | Metric baseline | Starting values for the charter's success metrics | BA | D | J |
| 2.1.4 | Contact demand baseline | Volumes by channel, hour, and contact reason; handle times; backlog | BA, SME | D | J |

Where it goes wrong: only managers interviewed, so the documented process is the official one.

### 2.2 Cross-cutting requirements

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 2.2.1 | KPI catalog | KPIs by audience, defined before any data model decisions | BA, SPON | D | J |
| 2.2.2 | Security and compliance requirements | Visibility rules, regulatory constraints | SA, SME | D | J |
| 2.2.3 | Integration and data requirements | Interface list, migration scope | SA, DATA | D | J |
| 2.2.4 | Non-functional requirements | Peak volumes and concurrency, hours of operation, availability, languages, accessibility, recording and retention obligations | SA | D | J |

Where it goes wrong: reporting gathered last, after the model that must support it is fixed. The KPI catalog is first in this group for that reason.

### 2.3 Backlog baseline

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 2.3.1 | To-be end-to-end process | Future-state flow across all capabilities | BA | D | J |
| 2.3.2 | Prioritized backlog | Consolidated stories from SV.n.1, MVP line, explicit out-of-scope list | PO, BA | D | J |
| 2.3.3 | Fit-gap and revalidated estimate | Fit-gap, revised estimate against SOW | SA, PM | D | P |

Where it goes wrong: nothing is ever out of scope; the estimate is never revisited after discovery.

---

## 3. Platform foundation

Everything that must exist before capability work can start.

### 3.1 Org strategy and provisioning

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 3.1.1 | Org strategy decision | Decision record: single vs. multi-org, relationship to existing orgs | SA | D | J |
| 3.1.2 | License and edition validation | Confirmation that licenses and channel add-ons support the scoped features and channels | SA, EL | D | J |
| 3.1.3 | Production org readiness | My Domain, email deliverability and org-wide addresses, business hours, holidays, company settings | CON | D | P |
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
| 3.2.7 | External access security | Guest user, portal sharing, and authenticated customer access, when self-service is in scope | SA | D | P |

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
| 3.4.2 | Privacy and compliance review | Consent, retention, residency, and deletion handling, including call recordings, transcripts, and payment data disclosed in conversations | SA, client legal | D | J |
| 3.4.3 | Large data volume assessment | Skew, indexing, and archiving decisions (tier L, or any object over a threshold) | SA | D | P |
| 3.4.4 | Audit and monitoring setup | Field history, setup audit, event monitoring decisions | SA, CADM | D | J |

Scaling: backup (3.4.1) and the privacy review (3.4.2) apply at every tier, sized to the data involved. The large data volume assessment applies at tier L, or whenever any object is expected to reach millions of records.

---

## 4. Data migration

### 4.1 Plan

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 4.1.1 | Migration scope | What migrates, how much case history, which emails and attachments, what is archived | DATA, PO | D | J |
| 4.1.2 | Source profile | Volumes, fill rates, duplicates per source | DATA | D | P |
| 4.1.3 | Mapping workbook | Field mapping and transformation rules | DATA, BA | D | J |
| 4.1.4 | Ownership map | Legacy users to Salesforce users, inactive-owner rule | DATA | D | J |
| 4.1.5 | Open-case transition plan | Rules for cases in flight at cutover: migrate, finish in legacy, or re-create | DATA, PO | D | J |

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
| 5.1.4 | Channel provider dependencies | Carrier and number porting lead times, messaging sender registrations and approvals, with dates | PM, client IT | D | **C** |

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

Unit testing and demos live with each capability (SV.n.4). This section is system-level.

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
| 6.2.3 | Performance test results | Routing and key transactions at peak concurrency (tiers M and L) | QA, DEV | D | P |
| 6.2.4 | Regression suite | Repeatable suite, run after every fix release | QA | D | P |
| 6.2.5 | Channel end-to-end results | Every channel tested from customer entry to case closure, including failure and fallback paths | QA, SME | D | J |

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
| 7.1.5 | Training release schedule | Agents released from queues for training without breaching service levels | SPON, SME | D | **C** |

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
| 7.3.2 | Supervisor operating rhythm | Queues managed and agents coached from the system, not from legacy wallboards and side spreadsheets | SPON | D | **C** |
| 7.3.3 | Reinforcement program | Office hours, refreshers | OCM | LOE | J |

Where it goes wrong: training is squeezed because nobody planned cover for the queues; supervisors keep managing from the old tools, which tells agents the new system is optional.

---

## 8. Deployment and go-live

### 8.1 Readiness

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 8.1.1 | Go/no-go criteria | Written and agreed well before the decision day | PM, SPON | D | J |
| 8.1.2 | Cutover runbook | Hour-by-hour, with owners; sequences 4.4.1 | PM, SA | D | J |
| 8.1.3 | Rehearsed deployment package | Validated against staging, manual steps documented | DEV, CON | D | P |
| 8.1.4 | Rollback plan | Procedure and decision point | SA | D | P |
| 8.1.5 | Rollout strategy | Decision record: single cutover, or phased by channel, team, or site | SA, PO | D | J |
| 8.1.6 | Channel cutover plan | Sequence per channel: email redirection, number porting, chat deployment swap, each with a fallback | SA, client IT | D | J |

### 8.2 Cutover

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 8.2.1 | Production release | Deployed, manual steps complete | DEV, CON | D | P |
| 8.2.2 | Activated users | Licenses assigned, users live | CADM | D | **C** |
| 8.2.3 | Smoke test results | Critical paths verified in production | QA, SME | D | J |
| 8.2.4 | Legacy read-only | Old system frozen | client IT | D | **C** |
| 8.2.5 | Switched channels | Each channel live on the new platform and confirmed with a real contact | SA, client IT | D | J |

Where it goes wrong: criteria written on the day; manual steps held in one person's head; a cutover planned as if the contact center had a quiet window, when it does not.

---

## 9. Hypercare and closeout

### 9.1 Hypercare

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| 9.1.1 | Support model | Triage process, severities, exit criteria | PM | D | J |
| 9.1.2 | Triage and fix releases | Resolved issues | CON, DEV | LOE | P |
| 9.1.3 | Adoption and data quality monitoring | Weekly report | OCM, CADM | LOE | J |
| 9.1.4 | Floor support | On-site or on-call support present for every live shift, not only business hours | CON, OCM | LOE | P |
| 9.1.5 | Service level recovery report | Handle time, backlog, and service levels tracked against the 2.1.4 baseline until recovered | PM, SME | LOE | J |

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

Where it goes wrong: hypercare never ends because it has no exit criteria; the expected productivity dip was never forecast, so a normal first fortnight is read as failure.

---

# Part 2 — Service Cloud module

## SV. Service Cloud capabilities

Field service is a separate module with its own scheduling, mobile, and inventory capabilities, and is not covered here. A self-service site is covered as a capability (SV.10) to the extent of case deflection and case submission; a full customer community is an Experience Cloud module.

### The capability pattern

Every capability SV.n decomposes into the same four work packages:

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| SV.n.1 | Discover | Workshop output: user stories with acceptance criteria, fed to 2.3.2 | BA, SME | D | J |
| SV.n.2 | Design | Decision records and the capability's section of the solution design | SA, CON | D | P |
| SV.n.3 | Build | Configured capability in the dev sandbox, split by scope item if over the sizing rule | CON, DEV | D | P |
| SV.n.4 | Verify | Unit tested, demoed to the product owner, accepted into system test | CON, PO | D | J |

This works for gated delivery (all SV.n.1, then all SV.n.2, and so on) and for sprint delivery (one capability or slice at a time, through all four).

Automation rule for every SV.n.2: Flow only, one entry point per object, a bypass mechanism for migration and integration users, and a decision record for anything that needs code.

Three capabilities carry a fifth package, because they depend on work that is not configuration:

| ID | Work package | Deliverable | Owner | Type | Side |
|---|---|---|---|---|---|
| SV.5.5 | Telephony provisioning | Contact center instance, numbers, call flows, and carrier arrangements ready for integration | client IT, SA | D | J |
| SV.8.5 | Knowledge content | Articles reviewed, rewritten where needed, migrated, categorized, and approved by their owners | SME | D | **C** |
| SV.10.5 | Self-service content and branding | Site content, forms, and brand assets approved for publication | SME, OCM | D | J |

### Capabilities

| ID | Capability | Key design decisions (SV.n.2) | Build scope (SV.n.3) | Where it goes wrong |
|---|---|---|---|---|
| SV.1 | Customer and asset model | Business accounts, person accounts (irreversible), or both; how an unknown contact is matched or created; whether assets and products are tracked; ownership and visibility of customer records | Account and contact configuration, matching and duplicate rules, assets and products where scoped | Inbound contacts create duplicate customers on every channel because matching was designed per channel, or not at all |
| SV.2 | Case management | Case lifecycle and statuses with definitions; record types and support processes; categorization scheme sized for reporting, not for completeness; parent and child cases; case teams; closure rules | Record types, statuses, page layouts, assignment rules, escalation rules, auto-response, case merge, validation and closure rules | A categorization tree so deep that agents pick the first option, leaving contact-reason reporting worthless |
| SV.3 | Email and web channels | Routing addresses and their mapping to queues; threading behavior; auto-response and loop prevention; attachment handling; spam handling; web form fields and required data | Email-to-case routing addresses, threading, templates, web-to-case forms, auto-response rules | Auto-responders on both sides create mail loops; forwarded and shared mailboxes break threading |
| SV.4 | Messaging | Which channels (web and in-app chat, SMS, WhatsApp, others); synchronous or asynchronous service model; pre-conversation data capture; business-hours behavior; hand-off between automated and human service | Messaging channels and deployments, pre-chat, routing configuration, auto-responses, session and inactivity rules | Asynchronous messaging staffed and measured as if it were live chat; sender registration started too late |
| SV.5 | Voice and telephony | Native voice or partner telephony through CTI; recording, transcription, and consent; screen-pop and caller matching; call wrap-up and dispositions; what happens when telephony or the platform is down | Telephony integration, softphone, caller matching, voice call records, wrap-up codes, recording controls | Telephony treated as a configuration item when it is an integration with a vendor, a carrier, and a porting lead time attached |
| SV.6 | Routing and workload | Queue-based or skills-based routing; capacity model per channel and across channels; presence statuses and what each means for reporting; priority and overflow rules; supervisor controls | Omni-channel routing configurations, queues, skills, presence statuses, capacity settings, supervisor views | Capacity rules tuned on test volumes fail at real peak; too many presence statuses make utilization unreadable |
| SV.7 | Agent workspace | Console layout per role; what an agent must see without clicking; guided processes for the highest-volume contact reasons; macros and quick text ownership | Service console app, record pages, utility items, macros, quick text, screen flows for guided handling, email templates | A workspace designed by the project team and never timed against real contacts, adding seconds to every interaction |
| SV.8 | Knowledge | Article types and lifecycle; data category structure; authoring, review, and approval responsibilities; visibility by channel (internal, customer, partner); how agents find and attach articles; how content is kept current | Knowledge configuration, record types, data categories, approval process, channel visibility, article-to-case behavior | Legacy articles migrated unread; the knowledge base launches complete and untrusted, and agents stop searching it within a month |
| SV.9 | Entitlements and service levels | Whether formal entitlements are needed or business-hours rules suffice; milestones and their clocks; business hours and holidays by region; what pauses the clock; violation and warning actions | Entitlement processes, milestones, business hours, holidays, service contracts where scoped, milestone actions | Contractual service levels modeled before the business agreed what stops the clock, so every breach report is disputed |
| SV.10 | Self-service | What customers can do without an agent; authenticated or public access; case submission and status; knowledge exposure; deflection measurement; boundary with a full community | Help center site, case forms, knowledge surfacing, guest and authenticated access per 3.2.7, deflection tracking | Guest user access configured for convenience and exposing records; deflection claimed but never measured |
| SV.11 | Service analytics and customer feedback | KPI definitions from 2.2.1 (first contact resolution, handle time, backlog, service level attainment, satisfaction); how each is calculated from captured data; survey timing and channel; supervisor and executive views | Custom report types, reports, dashboards by audience, routing and workload reporting, surveys and response capture | Handle time and resolution reported from fields agents fill in by hand, so the figures measure compliance with data entry |
| SV.12 | AI and agents | Which contact reasons are suitable for automated resolution; grounding sources and their quality; agent running-user permissions per 3.2.5; hand-off to a human with context preserved; guardrails and topics out of bounds; monitoring and review of conversations | AI agent configuration, topics and actions, grounding on knowledge, classification and recommendation features, escalation paths, guardrail tests, conversation monitoring | An AI agent grounded on the unreviewed knowledge base from SV.8; hand-off that drops the conversation history, so the customer starts again with a human |

SV.12 depends on SV.8 more than on any technical factor. An AI agent answers from the content it is given, and the state of the knowledge base sets the ceiling on what it can safely resolve.

---

# Part 3 — Using the WBS

## Gates

Gates are milestones, not work, so they do not appear in the WBS. Each is a decision supported by evidence from specific work packages.

| Gate | Decision | Evidence from | Decided by |
|---|---|---|---|
| 1 | Requirements baseline | 2.1.4, 2.3.2, 2.3.3 | PO |
| 2 | Design sign-off | All SV.n.2, 3.2.1–3.2.3, 3.2.7, 5.1.1, 8.1.5, 1.4.1 | PO |
| 3 | User acceptance | 6.3.3, 6.2.5, 4.3.3 | PO |
| 4 | Go or no-go, per channel where rollout is phased | 8.1.1–8.1.6, 5.1.4, SV.8.5, 1.4.3 | SPON, PO |
| 5 | Hypercare exit | Exit criteria in 9.1.1 met, service levels recovered per 9.1.5 | PO |

Two features are specific to service. The rollout strategy (8.1.5) is part of design sign-off, because a phased rollout means agents, and sometimes customers, live in two systems at once, and that has design consequences. And Gate 4 includes knowledge content (SV.8.5): a contact center that goes live with a knowledge base its agents do not trust has gone live with a slower operation than the one it replaced.

## Brownfield overlay

Implementing into an existing org adds work that a greenfield structure does not contain.

| ID | Work package | Deliverable | Adds to |
|---|---|---|---|
| B.1 | Org health assessment | Technical debt, automation inventory, limits usage, security posture | 2.1 |
| B.2 | Coexistence design | How new capabilities live alongside existing automation, record types, and sharing | Every SV.n.2 |
| B.3 | Remediation backlog | Debt that must be cleared before build, with a decision on who funds it | 2.3 |
| B.4 | Regression baseline | Tests proving that existing functionality still works | 6.1 |
| B.5 | In-place data changes | Transformations to live data, with rollback | 4 |
| B.6 | Existing user impact | Change plan for people already working in the org | 7.1 |
| B.7 | Legacy channel migration | Retired or superseded channel features replaced, in particular legacy chat, which Salesforce stopped supporting in February 2026 | SV.4 |
| B.8 | Shared-object impact | Effect on sales or other teams already using accounts, contacts, and cases in the same org | SV.1, 3.2.1 |

B.8 matters whenever service is added to an org that sales already uses. The account and contact model, the sharing model, and the duplicate rules are shared property, and changing them for service changes them for everyone.

## The client-side view

Filtering the WBS to packages marked `C` produces the list of work the client must perform for the project to succeed:

| ID | Client-owned package |
|---|---|
| 4.2.1 | Cleansed source data |
| 4.3.3 | Data acceptance |
| 5.1.3 | External team commitments |
| 5.1.4 | Channel provider dependencies |
| 6.3.2 | UAT staffing with real agents |
| 7.1.2 | Sponsor action plan |
| 7.1.5 | Training release schedule |
| 7.3.2 | Supervisor operating rhythm run from the system |
| 8.2.2 | Activated users |
| 8.2.4 | Legacy system set to read-only |
| 9.2.5 | Legacy decommission plan |
| SV.8.5 | Knowledge content |

Each belongs in the assumptions section of the statement of work with an owner and a date. Three deserve particular attention in a service engagement. Channel provider dependencies and knowledge content are the two most common causes of a late go-live, and both are outside the partner's control. The training release schedule is the one most often assumed: agents can only be trained if someone else is answering customers while they are.

## Calibrating effort

The indicative shares given earlier are a starting orientation. A delivery practice should replace them with its own figures.

1. Record actual hours against level-2 groups on every project.
2. Record the tier and the principal effort drivers alongside the hours.
3. After three projects at the same tier, replace the indicative ranges with observed ones. After six, estimate capabilities from their drivers.
4. Estimate LOE packages in 9.1 by shift coverage, not by calendar weeks. Two weeks of floor support for a continuous operation is three times the effort of two weeks for a business-hours one.

| Capability | Principal effort driver |
|---|---|
| SV.1 Customer and asset model | Customer types, state of duplicates, asset tracking in or out |
| SV.2 Case management | Number of support processes and record types |
| SV.3 Email and web channels | Number of routing addresses and forms |
| SV.4 Messaging | Number of channels and sender registrations |
| SV.5 Voice and telephony | Native or partner telephony, number of call flows, recording requirements |
| SV.6 Routing and workload | Queue or skills model, number of skills, cross-channel capacity rules |
| SV.7 Agent workspace | Number of roles, number of guided processes |
| SV.8 Knowledge | Article count and condition, number of languages, channel visibility |
| SV.9 Entitlements and service levels | Number of distinct service level agreements, regions, and calendars |
| SV.10 Self-service | Public or authenticated, number of forms, brand requirements |
| SV.11 Analytics and feedback | Number of dashboards, survey channels |
| SV.12 AI and agents | Number of contact reasons automated, number of actions, state of grounding content |

## Combining with the Sales Cloud module

A program that implements both clouds runs one core, not two. The core packages are performed once, sized for the combined scope. The modules then sit side by side, with three points of contact that need an explicit owner:

| Shared concern | Sales module | Service module | Resolution |
|---|---|---|---|
| Customer model | S.2 Account and contact management | SV.1 Customer and asset model | Design once, as a single capability, with both teams in the workshop. The person-account decision in particular cannot be made twice. |
| Analytics | S.8 Analytics | SV.11 Service analytics and customer feedback | One KPI catalog (2.2.1); separate build packages per audience. |
| AI and agents | S.9 AI and agents | SV.12 AI and agents | One non-human identity standard (3.2.5) and one guardrail approach; separate agents and topics. |

Everything else in the two modules is independent and can be sequenced separately, which is the usual reason for phasing one cloud ahead of the other.

## WBS dictionary template

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
