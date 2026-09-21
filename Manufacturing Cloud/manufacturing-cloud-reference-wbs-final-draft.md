# A Reference Work Breakdown Structure for Salesforce Manufacturing Cloud Implementations

*An overlay module on the shared delivery core, sourced to Salesforce documentation*

Final draft · September 2026
Companions: *Reference WBS for Sales Cloud Implementations* v1.0, *Reference WBS for Service Cloud Implementations* v1.0

---

## Why this document is built differently

The Sales Cloud and Service Cloud documents in this series describe products that most practitioners know well, and they draw freely on general delivery experience. Manufacturing Cloud is a different case. It is narrower, it is assembled from separately enabled and sometimes separately priced features, several of its objects are less than a year old, and its central capabilities are calculated from data the project does not own. A reference structure for it has to be exact about what the product does, because a plausible guess about a feature becomes a wrong line in a statement of work.

So this document follows one rule: every statement about the product is traced to a Salesforce source, and anything that is not is labelled. Each row carries a basis code.

| Code | Meaning |
|---|---|
| **D** | Documented in a Salesforce source listed at the end. Numbers in brackets identify the source. |
| **J** | Implementation judgment: work that follows from how projects are delivered, not from a product document. |
| **V** | To be verified. Relevant, but not confirmed from a Salesforce source. The verification register lists each one. |

For the same reason, this document does not give sizing tiers, effort shares, or failure modes. The companion documents could offer those as orientation. Here there is no sourced basis for them, and they should come from delivery history.

**Naming.** Salesforce's own pages currently use both "Manufacturing Cloud" and "Agentforce Manufacturing" for the product [3][9], and product naming has been changing. This document uses "Manufacturing Cloud" and names capabilities by function.

---

## The structural finding: this module is an overlay

The companion documents each pair the shared core with one capability module. Manufacturing Cloud does not fit that shape. Salesforce describes it as a CRM layer for the business outside the shop floor, spanning sales, service, and channel, and sitting over ERP and IoT systems as an engagement layer [3]. Its data model adds objects around the standard ones (accounts, opportunities, orders, assets, work orders) and does not replace them [1].

A Manufacturing Cloud implementation is therefore assembled from four parts:

```
Core (sections 1–9 of the companion documents)
  + selected Sales Cloud capabilities (S)      for example accounts, opportunities, products and pricing
  + selected Service Cloud capabilities (SV)   for example customer and asset model, cases, when service is in scope
  + Manufacturing capabilities (MF)            this document
```

Salesforce groups the product's use cases into three areas: commercial operations, service experience, and channel engagement [3]. Which of the three are in scope is the first scoping question, because it decides which Sales and Service capabilities come with the engagement. **(D** for the three areas, **J** for the consequence.)

---

## How to read it

Structure, the four-package capability pattern, the `Type` and `Side` conventions, role codes, and gates are as defined in the companion documents and are not repeated. IDs in Part 1 continue the core numbering. Work packages are named for what exists when the work is complete.

---

# Part 1 — Changes to the core

The core carries over. These are the additions and adjustments Manufacturing Cloud requires.

| ID | Work package | Deliverable | Side | Basis |
|---|---|---|---|---|
| 2.1.4 | Commercial model baseline | How the client sells: run-rate and new business, agreement-based or order-based, direct or through channel, program-based or not | J | J. Salesforce's forecasting description distinguishes run-rate from new business [4]; the baseline itself is delivery practice. |
| 2.2.5 | Planning calendar and units requirements | Fiscal periods, schedule frequency, units of measure, and currencies as used in agreements and forecasts | J | J. Agreement schedules, forecast periods, and period groups are all standard objects [1], so these requirements shape several capabilities at once. |
| 3.1.2 | License and feature validation (widened) | Confirmation of which Manufacturing Cloud features the client's contract includes | J | D/V. The product is available in Enterprise, Unlimited, and Developer editions [1]. Rebate Management has its own pricing, metered by rebate transactions [8]. Packaging of the other features is V. |
| 3.1.5 | Feature enablement plan | Which org settings are turned on, and in what order | P | D. Sales Agreements, Account Forecasts, Advanced Account Forecasting, and Default Analytics Dashboards are separate org settings [6]. Rebate Management is enabled separately in Setup [7]. |
| 3.2.7 | Partner access security | Sharing and object permissions for partner users on an Experience Cloud site | P | D. Partners can view agreements, adjust agreement metrics, and create orders through a site when granted access [10][11]; they upload rebate transactions and view payouts the same way [7]; warranty claims can be submitted through portals or APIs [3]. |
| 3.2.8 | Calculation service access | Read access for the integration user on every object and field used as a data source in forecast and rebate calculations | P | D. Salesforce states the Analytics Cloud Integration User needs read access, with field-level security, on all data source objects and fields in a Data Processing Engine definition [12]. |
| 5.1.5 | System-of-record map for commercial data | Which system owns orders, contracts, prices, products, inventory, and shipments | J | J, following from the engagement-layer positioning [3]. |
| 5.2.x | Order actuals interface | Order data arriving in Salesforce on a dependable schedule, in the form the chosen actuals mode requires | J | D/J. Agreement actuals come from orders, and the actuals calculation mode can be automatic from orders or a manual API upload picked up by a scheduled job [10][13]. The interface work is J. |
| 5.2.x | Forecast publication interface | Consolidated forecast delivered to demand planning or financial planning systems | J | D. Salesforce describes sharing consolidated forecasts with those systems [4]. |
| 4.1.6 | Historical order scope | How much order history is loaded to seed actuals and forecasts | J | J. |
| 6.2.6 | Calculation reconciliation | Agreement actuals and forecast figures reconciled to a trusted source for a sample of accounts and periods | J | J. The figures are produced by scheduled calculation jobs [5][12]; reconciliation is how users come to trust them. |
| 7.3.3 | Planning cadence | The recurring cycle of agreement review, forecast adjustment, and recalculation, with named owners | **C** | J. The product supports adjustment periods and scheduled recalculation [5]; the cadence is organizational. |
| 9.1.6 | Calculation job monitoring | Ownership and alerting for scheduled flows and calculation jobs after go-live | J | J. Forecast and rebate calculations run as scheduled jobs [5][7]; a failed job produces stale numbers, not an error a user sees. |

---

# Part 2 — Manufacturing module

## MF. Manufacturing capabilities

Each capability MF.n decomposes into Discover (MF.n.1), Design (MF.n.2), Build (MF.n.3), and Verify (MF.n.4), as in the companion documents.

### Commercial operations

| ID | Capability | What the product provides | Design decisions | Documented cautions |
|---|---|---|---|---|
| MF.1 | Sales agreements | A long-term agreement on price and volume between buyer and seller, with agreement products, per-period product schedules, schedule adjustments, product attributes, and contract lines [1]. Planned versus actual tracking [3]. Standard actions to refresh actuals and mass-update agreement values [2]. An approval setting that either requires a predefined approval process or also allows self-approval [10]. Renewal of active agreements [11]. Custom metrics [14]. **Basis: D** | Agreement term and schedule frequency; product-level or category-level lines; actuals calculation mode; approval policy; renewal handling; which metrics users may adjust; partner visibility. **Basis: D**, each is a documented setting or behavior. | Actuals are accurate only when ordered products are already on the agreement, and orders count once activated [11]. Agreements in Draft, Approved, or Canceled status cannot be renewed [11]. The actuals mode has three options; two are automatic from direct orders and manual API upload, and the third should be read from Help before design (**V**) [10][13]. |
| MF.2 | Account forecasting | A rolling forecast per account built from agreements, orders, and opportunities, with product and period breakdowns and manual adjustments. Only the adjusted quantity and revenue fields are user-editable at the product-period level [1]. Calculation settings, including whether opportunity product schedules contribute, and a recalculate-all function [14]. Quantity-based or revenue-based custom metrics [14]. Standard actions to recalculate and mass-update [2]. Enabled by its own org setting [6]. **Basis: D** | This capability, MF.3, or both; rolling period; which agreement statuses and opportunity data contribute; who may adjust; recalculation schedule. **Basis: D** except schedule (**J**). | Draft and approved agreements contribute to planned figures unless filtered, which Salesforce notes can distort forecasts [14]. Opportunity product schedules require Product Schedules to be enabled in the org [14]. |
| MF.3 | Advanced account forecasting | Forecast sets that hold dimensions, measures, adjustment periods, calculation methods, and frequencies, and can differ by business unit, location, or product line [5]. Up to six dimensions per set [5]. Calculations run on the Data Processing Engine: four templates ship with the product (generation, rollover, recalculation, regeneration), which are cloned, customized, activated, and run by scheduled flow [12][15]. Results are written to a forecast fact object that can be extended or replaced with a custom object [12]. A forecast-set-to-account junction holds what the account manager sees [12]. Another record, such as a manufacturing program, can serve as forecast context [1]. **Basis: D** | Number of forecast sets; dimensions (six at most); measures and formulas; period groups; standard or custom fact object; extent of DPE customization; flow schedule; participating accounts; partner participation. **Basis: D** | Only active DPE definitions with the Advanced Account Forecast process type can be selected in a forecast set [5]. Requires the access in core 3.2.8 [12]. Build needs Data Processing Engine and Flow skills, which is a staffing consideration (**J**). |
| MF.4 | Account manager targets | Targets holding fiscal year, measure, value, dates, and assignment; distributions by account, product, and price book; twelve-period distributions; a target measure list [1]. A standard action cascades value changes from a parent target by percentage [2]. **Basis: D** | Target measures; distribution hierarchy; period spread; relationship to Sales Cloud quotas where S.5 is also in scope. **Basis: D** except the quota relationship (**J**). | None found. |
| MF.5 | Program based business | Manufacturing programs with templates and transformation types; forecast facts at program, component, and product-variant level; product component relationships; a link from component forecasts to opportunity line item schedules [1]. Suppliers import customer forecasts and generate program, variant, and component forecasts [16]. Salesforce describes deriving component demand from third-party industry signals [3]. A standard action imports records from CSV [2]. **Basis: D** | Whether the client's business is program-based at all; program and variant structure; component relationships; source, licensing, and load method of third-party demand data; how program forecasts use MF.3. **Basis: D** except client fit and data licensing (**J**). | Depends on MF.3 [1]. |
| MF.6 | Samples and requirement specifications | Sample requests with items, specifications, quantity, and price; product requirement specifications with items and numbered versions (all API 65.0 and later) [1]. Salesforce lists sample management as a key feature covering intake, tracking, and approval [3]. **Basis: D** | Intake channels; approval rules; relationship to opportunities. **Basis: J** | Recent objects: confirm availability in the client's org (**V**). Grouping these two under one capability is this document's choice (**J**). |
| MF.7 | Product catalog | Salesforce lists product catalog management as a key feature: hierarchy, attributes, product rules, bundles, and attributes on sales agreements [3]. A sales agreement product attribute object exists [1]. **Basis: D** | Boundary with Sales Cloud products and pricing (S.4) and with Revenue Cloud. | Which product delivers this, and how it is licensed, is **V**. Resolve before scoping. |

### Channel engagement

| ID | Capability | What the product provides | Design decisions | Documented cautions |
|---|---|---|---|---|
| MF.8 | Visits | Visits scheduled by a manager for a field rep, typically at distributor, supplier, and partner locations; reusable visit tasks with contexts; KPIs comparing expected and actual values [1]. Salesforce describes action plans, priorities, visit history, and mobile execution [3]. **Basis: D** | Visit types and task templates; KPIs captured; mobile scope. **Basis: J** | Mobile configuration detail is **V**. |
| MF.9 | Dealer and partner sales model | Preferred-seller links from leads and opportunities to dealer accounts; seller products with availability and sales-or-service role; a searchable dealer object for location-based dealer search (all API 65.0 and later) [1]. **Basis: D** | Dealer data ownership; routing of leads and opportunities to dealers; dealer locator exposure. **Basis: J** | Recent objects: confirm availability (**V**). A full partner site is an Experience Cloud module (**J**). |
| MF.10 | Rebates and channel revenue | Rebate Management: rebate programs with payout calculation on growth, unit, amount, or custom measures [17]; enabled in Setup; calculated using Flow, the Data Processing Engine, and Batch Management, each with predefined templates; prebuilt apps with permission sets and templates; partners upload transactions and view payouts through a site [7][18]. Ship-and-debit process support [19]. Stock rotation rebate records (API 65.0 and later) and a published channel partner inventory tracking model [1][20]. **Basis: D** | Rebate types and measures; payout frequency; transaction sources (orders, invoices, claims) and how they arrive; partner self-service; ship-and-debit in or out; dispute handling. **Basis: D** for types and sources, **J** for disputes. | Separately priced, by rebate transactions: one per inbound transaction and one hundred per payout, which makes transaction volume a commercial input to design [8]. The rebate data model was not retrieved, so this capability is probably under-decomposed (**V**). |

### Service experience

| ID | Capability | What the product provides | Design decisions | Documented cautions |
|---|---|---|---|---|
| MF.11 | Warranty terms and claims | Warranty terms covering labor, parts, expenses, and exchange options; coverage by product or code set; product-to-term links; asset warranties with exclusions and extensions. Claims submitted by a partner to the manufacturer, or by the manufacturer to a supplier for recovery, with claim items, causal-part coverage, payment detail, and participants. Code sets with relationships; fault and labor codes by product or family; supplier and supplier product records [1]. Rule-based claim approval and submission through portals or APIs [3]. **Basis: D** | Term structure by product or family; coverage by duration and usage; code sets and their owners; adjudication rules; supplier recovery in or out; partner submission channel. **Basis: D** | Partner claims and supplier recovery share the claim object [1], so they cannot be designed separately. The rules mechanism used for adjudication is **V**. |
| MF.12 | Inventory and depot repair | Product items by location with transactions; product requests, transfers, and shipments; return orders for repair, return, or recall; serialized products; inventory count plans and assessments; replenishment policies; products required and consumed on work orders; work order diagnosis for depot repair; production batches; purchase orders and goods received notes (latest objects API 65.0) [1]. Work orders created from return orders [3]. **Basis: D** | Which locations hold stock in Salesforce; system of record for stock (core 5.1.5); serialized or not; return and repair flow; count and replenishment policy. **Basis: J** | Several objects are shared with Field Service; the boundary with a Field Service module needs an explicit decision (**J**). |
| MF.13 | Asset lifecycle and fleets | Asset milestones such as manufacture, registration, and resale; account and contact participants on assets; fleets, fleet assets, and fleet participants [1]. Salesforce lists asset service management and remote action orchestration based on telemetry [3]. **Basis: D** | Participant roles; milestones tracked; fleet grouping; telemetry in or out. **Basis: J** | Remote action orchestration is confirmed only at feature-list level: setup, prerequisites, and licensing are **V**. Telemetry implies an IoT interface under core section 5 (**J**). |
| MF.14 | Product service campaigns | Campaigns such as safety recalls or compliance upgrades, with campaign items that are assets or serialized products. API 65.0 adds campaign and group definitions, causal items, coordinating partners, partner-held inventory, preferred partners by geography, and eligible work types [1]. **Basis: D** | Campaign types; how affected units are identified; partner execution; work type mapping. **Basis: J** | Depends on MF.12 and MF.13 [1]. |

### Cross-cutting

| ID | Capability | What the product provides | Design decisions | Documented cautions |
|---|---|---|---|---|
| MF.15 | Analytics | A default analytics dashboards setting ships with sales agreements [6]. Salesforce describes prebuilt dashboards for rebate program performance [17] and Actionable Relationship Center templates for payout analysis [18]. **Basis: D** | Packaged dashboards or standard reports; KPI traceability per core 2.2.1. | The analytics product behind the dashboards, its licensing, and its data sync are **V**. |
| MF.16 | AI and agents | Salesforce positions the product around AI agents for rule-based automation, employee assistance, and personalization, and names account summarization for channel sales and AI for demand forecasting [3]. **Basis: D** at positioning level only. | Agent use cases; grounding data; running-user permissions per core 3.2.5; guardrails and monitoring. **Basis: J**, unchanged from the companion documents. | Manufacturing-specific agent templates, actions, and prerequisites are **V**. |

---

# Part 3 — Using the module

## Dependencies stated by the product

Read from object and setup documentation, so all **D**:

- MF.2 and MF.3 consume MF.1: forecasts are built from agreements, orders, and opportunities [1].
- MF.5 runs on MF.3: a manufacturing program can be the context for a forecast set [1].
- MF.14 consumes MF.12 and MF.13: campaign items are assets or serialized products [1].
- MF.3 and MF.10 share a technical foundation: both calculate through the Data Processing Engine and scheduled flows [7][12], so one build skill set and one monitoring approach (core 9.1.6) serve both.
- MF.1, MF.10, and MF.11 all expose work to partners through Experience Cloud [7][10][3], so partner access security (core 3.2.7) is designed once for all three.
- MF.1 actuals and both forecasting capabilities require order data, which makes the order actuals interface a prerequisite for the central capabilities [10][11].

From these, a minimum coherent scope is MF.1, one of MF.2 or MF.3, and the order actuals interface. Every other capability is separable. **(J)**

## The client-side view

Client-owned work added by this module, for the assumptions section of a statement of work:

| ID | Client-owned package | Basis |
|---|---|---|
| 5.2.x | ERP-side delivery of order data for the chosen actuals mode | J |
| 7.3.3 | Planning cadence with named owners | J |
| MF.5 | Licensing and supply of third-party demand data, where used | J |
| MF.10 | Rebate transaction volumes for commercial sizing, and supply of inbound transactions | D [8] |
| MF.11 | Ownership and upkeep of fault and labor code sets | J |
| 3.1.2 | Confirmation from the client's contract of which features are licensed | J |

## Verification register

Open items, in the order I would close them.

| # | Item | Affects | Where to check |
|---|---|---|---|
| 1 | Packaging and licensing of each feature other than rebates | 3.1.2, all scoping | Client order form, Salesforce account team |
| 2 | Permission sets and permission set licenses by capability | Core 3.2.2 | Help |
| 3 | Third actuals calculation mode, and when to use each | MF.1 | Help: actuals calculation mode |
| 4 | Rebate Management data model and object list | MF.10 decomposition | Channel revenue management developer guide |
| 5 | Product catalog management: product and license | MF.7 | Help, account team |
| 6 | Claim adjudication rules mechanism | MF.11 | Help: warranty lifecycle |
| 7 | Remote action orchestration prerequisites | MF.13 | Help, release notes |
| 8 | Analytics product, license, and data sync | MF.15 | Help |
| 9 | Manufacturing-specific agent templates and actions | MF.16 | Help, Agentforce documentation |
| 10 | Availability of API 65.0 objects in the client's org | MF.6, MF.9, MF.12, MF.14 | The client's org |
| 11 | Field Service boundary for inventory objects | MF.12 | Architecture decision |

Items resolved since the exploration draft: the forecasting calculation engine (Data Processing Engine, confirmed [5][12][15]), sales agreement approval and renewal behavior (confirmed [10][11]), and whether rebates are separately priced (confirmed [8]).

## What remains for the author

Sizing tiers, effort shares, effort drivers, and failure modes are absent by design. They should come from Manufacturing Cloud delivery history. The **J** entries are the places where that experience should confirm, replace, or sharpen what is written here.

---

## Sources

All are Salesforce-published.

1. *Manufacturing Cloud Developer Guide: Standard Objects*, Spring '26, API 66.0. https://developer.salesforce.com/docs/atlas.en-us.260.0.mfg_api_devguide.meta/mfg_api_devguide/mfg_api_overview.htm
2. *Manufacturing Cloud Developer Guide: Standard Invocable Actions*. https://developer.salesforce.com/docs/atlas.en-us.mfg_api_devguide.meta/mfg_api_devguide/mfg_actions_parent.htm
3. *Guide to Manufacturing Cloud*, modified 2026-08-28. https://www.salesforce.com/manufacturing/cloud/guide/
4. *Manufacturing Cloud – Sales* product page. https://www.salesforce.com/manufacturing/cloud/sales/
5. Salesforce Help, *Create and Configure Forecast Sets for Advanced Account Forecasting*. https://help.salesforce.com/s/articleView?id=ind.aaf_admin_forecast_set_task.htm&language=en_US&type=5
6. *IndustriesManufacturingSettings* metadata type. https://developer.salesforce.com/docs/atlas.en-us.260.0.automotive_cloud.meta/automotive_cloud/auto_metadata_api_industriesmanufacturingsettings.htm
7. Trailhead, *Rebate Management Basics: Get Started with Rebate Management*. https://trailhead.salesforce.com/content/learn/modules/rebate-management-basics/get-started-with-rebate-management
8. *Rebate Management Pricing*. https://www.salesforce.com/manufacturing/channel-revenue-management/pricing/
9. Trailhead, *Manufacturing Cloud Admin Essentials: Get Started*. https://trailhead.salesforce.com/content/learn/modules/manufacturing-cloud-admin-essentials/get-started-manufacturing-cloud
10. Trailhead, *Manufacturing Cloud Admin Essentials: Configure Sales Agreements*. https://trailhead.salesforce.com/content/learn/modules/manufacturing-cloud-admin-essentials/configure-sales-agreements-to-negotiate-better
11. Trailhead, *Sales Agreements Foundations: Manage and Renew Active Sales Agreements*. https://trailhead.salesforce.com/content/learn/modules/sales-agreements-foundations/manage-and-renew-active-sales-agreements
12. Trailhead, *Data Processing Engine Essentials in Advanced Account Forecasting* (units on forecast data creation, templates, and customization strategy). https://trailhead.salesforce.com/content/learn/modules/data-processing-engine-essentials-in-advanced-account-forecasting
13. Trailhead, *Manufacturing Cloud Admin Essentials: Permissions, Flow Actions, and APIs*. https://trailhead.salesforce.com/content/learn/modules/manufacturing-cloud-admin-essentials/set-up-targets-for-account-managers
14. Trailhead, *Manufacturing Cloud Admin Essentials: Forecast Metrics and Formulas*. https://trailhead.salesforce.com/content/learn/modules/manufacturing-cloud-admin-essentials/configure-forecast-metrics-and-formulas
15. Trailhead, *Advanced Account Forecasting with Manufacturing Cloud: Configure Forecast Sets*. https://trailhead.salesforce.com/content/learn/modules/advanced-account-forecasting-with-manufacturing-cloud/configure-forecast-sets
16. Trailhead, *Manufacturing Cloud Basics: Track Sales with Agreement Terms*. https://trailhead.salesforce.com/content/learn/modules/manufacturing-cloud-basics/track-sales-with-agreement-terms
17. *Rebate Management* product page. https://www.salesforce.com/manufacturing/channel-revenue-management/rebate-management/
18. Salesforce Help, *Rebate Management*. https://help.salesforce.com/s/articleView?id=rebates_admin_parent.htm&language=en_US&type=5
19. *Rebate Management Software* product page. https://www.salesforce.com/ca/manufacturing/rebate-management-software/
20. *Data Model Gallery: Manufacturing*. https://developer.salesforce.com/docs/platform/data-models/guide/manufacturing-cloud-category.html
