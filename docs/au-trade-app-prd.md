# Product Requirements Document

## Australian Trade Job Management Platform (working name: "PLATFORM")

| Item | Value |
|---|---|
| Version | 1.0 (draft) |
| Date | 29 July 2026 |
| Status | For review |
| Language standard | ASD-STE100 Simplified Technical English |
| Source documents | `au-field-service-app-swot.md`; review analysis of MYOB Acumatica, JACK App and Build Paperless |
| Market | Australia. New Zealand is a later market. |

---

## 1. Purpose of this document

This document states what the product must do. It does not state how to build the product. The engineering team writes the technical design in a separate document.

Each requirement has an identifier, a priority and a release. The team must trace each requirement to a finding in the SWOT analysis.

**Priority definitions:**

| Code | Meaning |
|---|---|
| M | Must have. The release fails without it. |
| S | Should have. The release is weak without it. |
| C | Could have. Include it if time permits. |
| W | Will not have in this release. |

---

## 2. Problem statement

The Australian market has two separate product groups. Neither group serves the target customer well.

**Group 1 — service and maintenance products.** Examples are ServiceM8, Tradify and Fergus. These products manage callouts, quotes and invoices. They do not manage progress claims, variations, retentions or subcontractors. They stop at about 10 staff.

**Group 2 — construction and project products.** Examples are JACK App, Build Paperless, Buildxact and Buildertrend. These products manage estimates, projects and claims. They do not manage recurring maintenance contracts, asset registers or high-volume dispatch.

**The gap.** Many Australian trade businesses do both types of work. An electrical contractor fits new houses and also holds service contracts. A plumbing business does new construction and also does emergency callouts. These businesses must buy two products. They must then enter the same customer, the same price list and the same staff in both products.

**The evidence.** The SWOT analysis found these repeated complaints in the customer reviews:

| Complaint | Source finding |
|---|---|
| The gap between simple and complex products is too wide | SWOT W1 |
| Sales promises do not match the product | SWOT W2 |
| High setup cost and long setup time | SWOT W3 |
| Poor cancellation and contract practice | SWOT W4 |
| Price increases and hidden costs | SWOT W5 |
| Platform restriction (iOS only) | SWOT W6 |
| Weak offline operation | SWOT W7 |
| Weak and inflexible reporting | SWOT W8 |
| Slow response to feature requests | SWOT W9 |
| Poor performance on large jobs | SWOT W10 |

---

## 3. Product vision

**Vision statement:** One platform that runs a trade business from the first enquiry to the last payment. The platform must handle a two-hour service callout and a nine-month construction contract with equal skill.

**Positioning statement:** For Australian trade businesses with 5 to 50 staff that do both service work and construction work, PLATFORM is a job management platform that removes the need for two systems. Unlike ServiceM8 and Tradify, PLATFORM manages projects, claims and subcontractors. Unlike Simpro and AroFlo, PLATFORM has a flat published price, no lock-in contract and a one-day setup.

---

## 4. Target users

### 4.1 Target business

| Attribute | Target |
|---|---|
| Location | Australia, all states and territories |
| Size | 5 to 50 staff |
| Trades | Electrical, plumbing, HVAC and refrigeration, fire protection, solar, carpentry, security, general building |
| Work mix | Both service work and construction work. This is the key attribute. |
| Current systems | One job app, one accounting product, and often one separate safety product |
| Accounting | Xero, MYOB or QuickBooks Online |

### 4.2 Personas

| ID | Persona | Main need | Main risk |
|---|---|---|---|
| P1 | Owner or director | See the profit on each job and the cash position | Will not read a manual |
| P2 | Office administrator | Enter data once. Invoice fast. | Carries the load when the software fails |
| P3 | Service technician | Get the job, do the job, close the job | Works in areas with no data signal |
| P4 | Site supervisor | Manage the programme, the subcontractors and the site records | Uses a phone, not a computer |
| P5 | Subcontractor | Get the work order. Send the invoice. | Will not pay for a licence |
| P6 | Client | See the progress and the cost | Telephones the office when unsure |
| P7 | Estimator | Build an accurate price fast | Loses margin through errors |

---

## 5. Goals and success metrics

| ID | Goal | Metric | Target |
|---|---|---|---|
| G1 | Fast setup | Time from sign-up to the first sent invoice | Less than 1 business day for 80% of new customers |
| G2 | Field adoption | Active field users against licensed field users each week | More than 85% |
| G3 | Offline reliability | Field records that sync without loss | More than 99.9% |
| G4 | Cash flow effect | Median days from job completion to invoice sent | Less than 1 day |
| G5 | Customer retention | Gross revenue churn each month | Less than 1.5% |
| G6 | Support quality | Median first response by telephone or chat in business hours | Less than 15 minutes |
| G7 | Dual-mode use | Customers that use both service jobs and project jobs | More than 50% after 12 months |
| G8 | Trust | Verified public reviews in the first 12 months | More than 100 |

---

## 6. Out of scope

The product will not do these things. This list protects the schedule.

| ID | Item | Reason |
|---|---|---|
| OS1 | A general ledger | Xero, MYOB and QuickBooks Online do this. Do not compete with the integration partner. |
| OS2 | Payroll processing | This needs Single Touch Payroll certification and award interpretation. Export to a payroll product instead. |
| OS3 | Civil, mining and large commercial construction | These segments need different products. |
| OS4 | Building Information Modelling (BIM) and 3D models | The target customer does not use these. |
| OS5 | Markets outside Australia in release 1 | Local depth beats geographic width. |
| OS6 | A public marketplace for third-party apps | Later. Build a good API first. |

---

## 7. Design principles

The team must apply these principles to every decision.

1. **The field comes first.** Design the mobile screen before the web screen.
2. **Enter data one time.** The system must never ask for the same data twice.
3. **Offline is normal.** Treat a data signal as a bonus, not as a requirement.
4. **One job, two modes.** A service job and a project job share the same core record.
5. **Show the money.** Show the margin while the job is open, not after it closes.
6. **No surprises.** Publish the price. Do not use a lock-in contract.
7. **Simple by default.** Hide the advanced functions until the user turns them on.
8. **The truth on site.** A photo, a form and a signature protect the business in a dispute.

---

## 8. Functional requirements

### 8.1 Module A — Core platform and data model

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-A-01 | The system must hold one customer record that both service jobs and project jobs use. | M | MVP |
| FR-A-02 | The system must support two job modes: **Service job** and **Project job**. The user selects the mode when the user creates the job. | M | MVP |
| FR-A-03 | Both job modes must share the same customer, site, price list, staff, timesheet, material, form and document records. | M | MVP |
| FR-A-04 | The system must let a user convert a service job into a project job. It must keep all history. | S | R2 |
| FR-A-05 | The system must support multiple sites for one customer. | M | MVP |
| FR-A-06 | The system must give each job a unique number. The user can set the number format. | M | MVP |
| FR-A-07 | The system must keep a full audit trail. The trail must show who changed each record, and when. | M | MVP |
| FR-A-08 | The user must be able to define custom job statuses and the order of the statuses. | S | MVP |
| FR-A-09 | The system must support multiple companies or divisions under one login. | C | R3 |
| FR-A-10 | The system must remain responsive on a job with more than 500 line items. This answers SWOT W10. | M | MVP |

### 8.2 Module B — Customers, leads and sites

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-B-01 | The system must store customers, contacts, sites and the full communication history. | M | MVP |
| FR-B-02 | The system must verify an Australian Business Number (ABN) against the Australian Business Register. It must then fill the company details. | M | MVP |
| FR-B-03 | The system must record a lead and track it through a sales pipeline. | S | MVP |
| FR-B-04 | The system must capture leads from a web form on the customer website. | S | R2 |
| FR-B-05 | The system must send and receive Short Message Service (SMS) messages against the job. | M | MVP |
| FR-B-06 | The system must record e-mail against the job automatically. | S | R2 |

### 8.3 Module C — Quoting and estimating

The product needs two levels. A service quote must take two minutes. A construction estimate needs more depth.

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-C-01 | The user must be able to build a quote from a price list on a mobile device. | M | MVP |
| FR-C-02 | The system must support a customer price list, a supplier price list and a labour rate table. | M | MVP |
| FR-C-03 | The system must support quote templates for repeated work. | M | MVP |
| FR-C-04 | The system must send a quote by e-mail with a link. The customer accepts the quote online. | M | MVP |
| FR-C-05 | The system must record the date and time when the customer opens the quote. | S | MVP |
| FR-C-06 | The system must support a multi-section estimate with cost stages for a project job. | M | MVP |
| FR-C-07 | The system must support digital take-off from an uploaded plan in PDF format. The take-off must feed the estimate. | S | R2 |
| FR-C-08 | The system must show the margin on the quote before the user sends it. | M | MVP |
| FR-C-09 | The system must let the user request prices from suppliers and subcontractors, and then compare the answers. | S | R2 |
| FR-C-10 | The system must convert an accepted quote into a job with one action. | M | MVP |
| FR-C-11 | The system must not put vendor branding on a customer quote or invoice. This answers a Tradify complaint. | M | MVP |

### 8.4 Module D — Scheduling and dispatch

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-D-01 | The system must show a drag-and-drop schedule by day, by week and by month. | M | MVP |
| FR-D-02 | The system must show the schedule by staff member, by team and by site. | M | MVP |
| FR-D-03 | The system must show technician locations on a map, with the consent of the staff member. | S | MVP |
| FR-D-04 | The system must support recurring appointments for maintenance contracts. | M | MVP |
| FR-D-05 | The system must support a project programme view with dependencies (a Gantt view). | M | R2 |
| FR-D-06 | The system must notify staff and subcontractors when the schedule changes. | M | MVP |
| FR-D-07 | The system must suggest the best technician by skill, by licence, by location and by availability. | C | R3 |
| FR-D-08 | The system must warn the user when a scheduled staff member has an expired licence or ticket. | S | R2 |
| FR-D-09 | The system must send the customer an "on the way" message with an estimated arrival time. | M | MVP |

### 8.5 Module E — Mobile field app

This module is the highest risk and the highest value. It answers SWOT W6 and W7.

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-E-01 | The app must give identical functions on Android and on iOS. No function may be exclusive to one platform. | M | MVP |
| FR-E-02 | The app must work with no data connection. The user must be able to view jobs, add time, add materials, take photos, complete forms and capture signatures offline. | M | MVP |
| FR-E-03 | The app must queue all offline records. It must sync them automatically when the connection returns. | M | MVP |
| FR-E-04 | The app must show the sync state clearly. The user must always know if a record is safe. | M | MVP |
| FR-E-05 | The app must never lose an offline record, even after the user closes the app or the device restarts. | M | MVP |
| FR-E-06 | The app must resolve sync conflicts without data loss. It must ask the user when it cannot decide. | M | MVP |
| FR-E-07 | The user must be able to start a job in three taps or fewer from the app home screen. | M | MVP |
| FR-E-08 | The app must let the user dictate job notes by voice. | S | R2 |
| FR-E-09 | The app must compress photos before upload. It must keep the original for the record. | M | MVP |
| FR-E-10 | The app must give turn-by-turn navigation to the site through the device map application. | M | MVP |
| FR-E-11 | The app must let a user scan a supplier docket and attach it to the job. | S | MVP |

### 8.6 Module F — Time and labour

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-F-01 | The user must be able to start and stop a timer against a job on the mobile app. | M | MVP |
| FR-F-02 | The user must be able to enter time manually for a past day. | M | MVP |
| FR-F-03 | The system must support cost rates and charge rates for each staff member. | M | MVP |
| FR-F-04 | The system must support day rates as well as hourly rates. | S | MVP |
| FR-F-05 | The manager must be able to approve timesheets in bulk. | M | MVP |
| FR-F-06 | The system must export approved time to Xero, MYOB and QuickBooks Online, and to a CSV file. | M | MVP |
| FR-F-07 | The system must record the location of a clock-in event, with staff consent. | S | R2 |
| FR-F-08 | The system must support allowances such as travel and meals. | S | R2 |

### 8.7 Module G — Materials, stock and purchasing

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-G-01 | The user must be able to add materials to a job from a price list on the mobile app. | M | MVP |
| FR-G-02 | The system must create purchase orders and send them to suppliers. | M | MVP |
| FR-G-03 | The system must match a supplier invoice to a purchase order and to a job. | M | MVP |
| FR-G-04 | The system must read a supplier invoice automatically and create the cost lines. This uses machine reading. | M | R2 |
| FR-G-05 | The system must connect to Australian wholesaler catalogues for live prices. Release 1 must include the largest suppliers for electrical and plumbing. | M | R2 |
| FR-G-06 | The system must track stock in a store and on a vehicle. | S | R2 |
| FR-G-07 | The system must warn the user when a job uses more material than the estimate allowed. | S | R2 |

### 8.8 Module H — Compliance and safety

This module removes the need for a separate safety product. It answers SWOT O3.

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-H-01 | The system must include pre-built Safe Work Method Statement (SWMS) templates for common trade tasks. | M | MVP |
| FR-H-02 | The system must include Job Safety Analysis (JSA) forms and a hazard register. | M | MVP |
| FR-H-03 | The system must prevent a technician from starting a job timer until the technician completes the required safety form. | M | MVP |
| FR-H-04 | The system must include a digital forms builder. The user must be able to build a form without help from the vendor. | M | MVP |
| FR-H-05 | The system must include state-specific templates for electrical and gas compliance certificates. | M | R2 |
| FR-H-06 | The system must store staff licences, tickets and insurance certificates. It must warn the user before each expiry date. | M | MVP |
| FR-H-07 | The system must store subcontractor insurance and licence documents. It must block a work order when a document expires. | M | R2 |
| FR-H-08 | The system must record site inductions, toolbox meetings and site attendance. | S | R2 |
| FR-H-09 | The system must record an incident and the follow-up actions. | S | R2 |
| FR-H-10 | The system must check a trade licence against the state register where the register gives access. | C | R3 |

### 8.9 Module I — Assets and maintenance contracts

This module serves the maintenance side of the business.

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-I-01 | The system must hold an asset register against a customer site. | M | MVP |
| FR-I-02 | The system must record the full service history of each asset. | M | MVP |
| FR-I-03 | The technician must be able to find an asset by a QR code or a barcode. | S | R2 |
| FR-I-04 | The system must create planned maintenance jobs automatically from a schedule. | M | MVP |
| FR-I-05 | The system must hold a maintenance contract with a value, a period and included work. | M | R2 |
| FR-I-06 | The system must invoice a contract automatically on a cycle. | M | R2 |
| FR-I-07 | The system must report the profit on each maintenance contract. | S | R2 |
| FR-I-08 | The system must let a technician raise a follow-up job or a quote from a defect found on site. | M | MVP |

### 8.10 Module J — Project delivery

This module serves the construction side of the business.

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-J-01 | The system must support a project with stages, tasks and milestones. | M | MVP |
| FR-J-02 | The system must create progress claims against contract stages or against percentage complete. | M | MVP |
| FR-J-03 | The system must manage variations. A variation must have a price, a customer approval and an audit trail. | M | MVP |
| FR-J-04 | The system must track retention amounts and the release dates. | M | R2 |
| FR-J-05 | The system must record a daily site diary with weather, staff on site, subcontractors on site and delays. | M | MVP |
| FR-J-06 | The system must issue work orders to subcontractors and record their claims. | M | MVP |
| FR-J-07 | The system must support a client selections list with prices and digital sign-off. | S | R2 |
| FR-J-08 | The system must support the payment claim rules of the Security of Payment legislation in each state. It must warn the user before a response date. | S | R3 |
| FR-J-09 | The system must store plans and revisions. It must mark the current revision clearly. | M | R2 |

### 8.11 Module K — Invoicing and payments

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-K-01 | The user must be able to create and send an invoice from the mobile app on site. | M | MVP |
| FR-K-02 | The system must create an invoice from time and materials, from a fixed price, or from a progress claim. | M | MVP |
| FR-K-03 | The invoice must meet Australian tax invoice rules and must show GST correctly. | M | MVP |
| FR-K-04 | The customer must be able to pay by card or by bank transfer from a link on the invoice. | M | MVP |
| FR-K-05 | The system must send payment reminders automatically on a schedule that the user sets. | M | MVP |
| FR-K-06 | The system must show an aged debtor list. | M | MVP |
| FR-K-07 | The system must support deposits, part payments and credit notes. | M | MVP |
| FR-K-08 | The system must produce **one** service report for each job. The report must combine the work of all technicians across all days. This answers a specific Simpro complaint. | M | MVP |

### 8.12 Module L — Financial visibility

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-L-01 | The system must show the live margin on a job while the job is open. It must compare the estimate against the actual cost. | M | MVP |
| FR-L-02 | The system must alert the owner when a job passes a margin threshold. | S | MVP |
| FR-L-03 | The system must produce a work-in-progress (WIP) report. | M | R2 |
| FR-L-04 | The system must produce a cash flow forecast from the job pipeline, the schedule and the debtor list. | M | R2 |
| FR-L-05 | The system must report profit by trade, by staff member, by customer and by job type. | M | R2 |

### 8.13 Module M — Portals

Free portal users create a network effect. They also remove a cost barrier.

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-M-01 | The system must give each client a portal. The portal shows quotes, progress, photos, variations, claims and invoices. | M | R2 |
| FR-M-02 | The system must give each subcontractor a portal. The portal shows work orders, the schedule, safety documents and claims. | M | R2 |
| FR-M-03 | The system must give each supplier a portal for purchase orders and invoices. | C | R3 |
| FR-M-04 | Portal users must never need a paid licence. | M | R2 |
| FR-M-05 | The account owner must control what each portal user can see. | M | R2 |

### 8.14 Module N — Reporting

This module answers SWOT W8.

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-N-01 | The system must include standard reports for revenue, margin, job volume, debtors and staff use. | M | MVP |
| FR-N-02 | The user must be able to build a custom report without help from the vendor. | M | R2 |
| FR-N-03 | The user must be able to schedule a report by e-mail. | S | R2 |
| FR-N-04 | The user must be able to export any report to CSV and to PDF. | M | MVP |
| FR-N-05 | The system must give a dashboard that each user role can arrange. | S | R2 |

### 8.15 Module O — Automation and machine assistance

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-O-01 | The user must be able to build simple rules. Example: when a job status changes, send an SMS message. | S | R2 |
| FR-O-02 | The system must read supplier invoices and create cost lines. See FR-G-04. | M | R2 |
| FR-O-03 | The system must draft a customer-facing job summary from the technician notes. The user must approve the text before the system sends it. | S | R2 |
| FR-O-04 | The system must tag site photos automatically by job and by stage. | C | R3 |
| FR-O-05 | The system must never send machine-written text to a customer without human approval. | M | R2 |

### 8.16 Module P — Administration and access

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-P-01 | The system must support roles with different permissions. | M | MVP |
| FR-P-02 | The system must hide costs and margins from staff who do not have permission. | M | MVP |
| FR-P-03 | The system must support single sign-on. | C | R3 |
| FR-P-04 | The system must let the owner cancel the subscription from the web application without contact with the vendor. This answers SWOT W4. | M | MVP |

### 8.17 Module Q — Data import, export and migration

| ID | Requirement | Priority | Release |
|---|---|---|---|
| FR-Q-01 | The system must import customers, sites, price lists and open jobs from CSV files. | M | MVP |
| FR-Q-02 | The vendor must supply a free guided migration from ServiceM8, Tradify, Fergus, AroFlo and Simpro. | M | MVP |
| FR-Q-03 | The user must be able to export all data at any time in an open format, with no fee. | M | MVP |
| FR-Q-04 | The vendor must keep customer data for 90 days after a cancellation. | M | MVP |

---

## 9. Integration requirements

| ID | Requirement | Priority | Release |
|---|---|---|---|
| IR-01 | The system must sync in two directions with Xero for invoices, bills, payments and contacts. | M | MVP |
| IR-02 | The system must sync in two directions with MYOB Business. | M | MVP |
| IR-03 | The system must sync in two directions with QuickBooks Online. | S | R2 |
| IR-04 | The supplier invoice sync must work correctly. This is the most common failure in the market. The team must test it against real supplier files before release. | M | MVP |
| IR-05 | The system must connect to Stripe for card payments and to a bank transfer service. | M | MVP |
| IR-06 | The system must connect to the Australian Business Register for ABN checks. | M | MVP |
| IR-07 | The system must connect to the Bureau of Meteorology for site weather and delay records. | S | R2 |
| IR-08 | The system must connect to Australian wholesaler catalogues. See FR-G-05. | M | R2 |
| IR-09 | The system must export to common payroll products. | S | R2 |
| IR-10 | The system must give a public REST API with OAuth 2.0, webhooks and clear documents. | M | R2 |
| IR-11 | The API rate limit must be at least 20,000 calls each day. This is ten times the AroFlo limit. | M | R2 |

---

## 10. Non-functional requirements

### 10.1 Performance

| ID | Requirement | Target |
|---|---|---|
| NFR-P-01 | A web page must load within 2 seconds on a standard connection. | 95th percentile |
| NFR-P-02 | The mobile app must open a job within 1 second when the data is local. | 95th percentile |
| NFR-P-03 | Performance must not fall when a job holds more than 500 lines. | Measured |
| NFR-P-04 | The system must sync a queue of 200 offline records within 60 seconds. | 95th percentile |

### 10.2 Availability and reliability

| ID | Requirement | Target |
|---|---|---|
| NFR-A-01 | Service availability in Australian business hours. | 99.9% each month |
| NFR-A-02 | Recovery point objective after a failure. | 15 minutes |
| NFR-A-03 | Recovery time objective after a failure. | 4 hours |
| NFR-A-04 | The vendor must publish a public status page. | Required |

### 10.3 Security and privacy

| ID | Requirement | Priority |
|---|---|---|
| NFR-S-01 | The vendor must host all customer data in Australia. | M |
| NFR-S-02 | The system must encrypt data in transit and at rest. | M |
| NFR-S-03 | The vendor must comply with the Privacy Act 1988 and the Australian Privacy Principles. | M |
| NFR-S-04 | The vendor must support multi-factor authentication. | M |
| NFR-S-05 | The vendor must obtain ISO 27001 certification, or SOC 2 Type II, within 18 months. This answers a known AroFlo gap. | M |
| NFR-S-06 | The vendor must run an external penetration test each year and must publish a summary. | S |

### 10.4 Usability and accessibility

| ID | Requirement | Target |
|---|---|---|
| NFR-U-01 | A new technician must complete a full job without training. | Measured in a usability test |
| NFR-U-02 | The interface must meet WCAG 2.2 level AA. | Required |
| NFR-U-03 | The app must remain readable in direct sunlight. | High contrast mode |
| NFR-U-04 | The app must work with gloves on a phone screen. | Large touch targets |
| NFR-U-05 | The product must use Australian English and Australian terms. | Required |

### 10.5 Support

| ID | Requirement | Target |
|---|---|---|
| NFR-T-01 | The vendor must give telephone support in Australian business hours. This answers SWOT W-support findings. | Required |
| NFR-T-02 | Median first response by telephone or chat. | Less than 15 minutes |
| NFR-T-03 | The vendor must publish a feature request list with a public status. This answers SWOT W9. | Required |

---

## 11. Commercial requirements

The commercial model is a product feature. It answers the largest group of complaints in the SWOT analysis.

| ID | Requirement | Priority |
|---|---|---|
| CR-01 | The vendor must publish all prices on the website. The vendor must not use a quote-only model. | M |
| CR-02 | The price must not depend on the job count. It must depend on the user count. | M |
| CR-03 | Office users must cost less than field users, or must be free. | M |
| CR-04 | Client, subcontractor and supplier portal users must be free. | M |
| CR-05 | The vendor must not charge a setup fee. | M |
| CR-06 | The vendor must offer a monthly term. The vendor must not force an annual lock-in. | M |
| CR-07 | The user must be able to cancel in the application at any time. | M |
| CR-08 | The vendor must give 90 days notice of a price increase. | M |
| CR-09 | The vendor must include all core modules in the base price. The vendor must not hide core functions behind a higher tier. | M |
| CR-10 | The vendor must offer a 14-day free trial with no credit card. | M |
| CR-11 | Migration and onboarding must be free. | M |

**Indicative price:** $49 per field user each month. Office and manager users are free. All modules are included. This price sits between Tradify and Fergus, and far below Simpro and AroFlo. The team must test this price before launch.

---

## 12. Release plan

### 12.1 MVP — target 6 months

**Goal:** A trade business with 5 to 20 staff can run all of its service work and simple project work on the platform.

Includes: Module A, B, C (basic), D (basic), E (full), F, G (basic), H (basic), I (basic), J (basic), K, L (basic), N (basic), P, Q. Xero and MYOB integrations.

**MVP exit criteria:**
1. Ten paying customers run their whole business on the platform for one full month.
2. The offline sync loses zero records in a 30-day test.
3. The Xero supplier invoice sync passes a test with real files from five different wholesalers.
4. A new customer reaches the first sent invoice within one business day.

### 12.2 Release 2 — target 12 months

Adds: digital take-off, project programme view, retentions, client and subcontractor portals, supplier catalogues, machine reading of invoices, cash flow forecast, custom reports, the public API, QuickBooks Online.

### 12.3 Release 3 — target 18 months

Adds: automatic technician selection, Security of Payment tracking, licence register checks, supplier portal, single sign-on, multi-company support. New Zealand market entry.

---

## 13. Risks

| ID | Risk | Effect | Control |
|---|---|---|---|
| R1 | The dual-mode data model becomes too complex. | The product serves both segments badly. | Build the service mode first. Add the project mode on the same core. Do not fork the data model. |
| R2 | The offline sync fails and a customer loses data. | The brand fails. Trade users do not forgive data loss. | Treat sync as the highest engineering priority. Test it before all other work. |
| R3 | The supplier invoice sync does not work. | The product repeats the largest market failure. | Test against real supplier files during the MVP, not after it. |
| R4 | The incumbents reduce their prices. | The price advantage disappears. | Compete on the contract terms and the support, not on the price alone. |
| R5 | Customers will not move their data. | Growth stops. | Free migration. Free export. Prove that the exit is easy. |
| R6 | Support costs exceed the plan. | The margin falls. | Reduce the need for support through a simple design. Measure the contacts for each customer. |
| R7 | The wholesaler catalogue work is larger than expected. | Release 2 slips. | Start with the three largest suppliers. Add more later. |
| R8 | Construction insolvencies reduce the market. | Growth slows. | Serve both service work and construction work. Service revenue is more stable. |

---

## 14. Open questions

| ID | Question | Owner | Needed by |
|---|---|---|---|
| Q1 | What is the correct price point? | Commercial | Before the MVP launch |
| Q2 | Which wholesaler catalogues do the target trades use most? | Product research | Before Release 2 |
| Q3 | Do we build the take-off engine or license one? | Engineering | Before Release 2 |
| Q4 | Which state compliance certificates do we support first? | Product research | Before Release 2 |
| Q5 | Do we support MYOB Business, MYOB Acumatica, or both? | Product | Before the MVP launch |
| Q6 | Which trade associations will partner with us? | Commercial | Before the MVP launch |

---

## 15. Traceability

| SWOT finding | Requirements that answer it |
|---|---|
| W1 — the gap in the middle of the market | FR-A-02, FR-A-03, Modules I and J |
| W2 — sales promises do not match the product | CR-01, CR-10, MVP exit criteria |
| W3 — high setup cost and time | CR-05, CR-11, G1, FR-Q-02 |
| W4 — poor cancellation practice | CR-06, CR-07, FR-P-04 |
| W5 — price increases and hidden costs | CR-01, CR-08, CR-09 |
| W6 — platform restriction | FR-E-01 |
| W7 — weak offline operation | FR-E-02 to FR-E-06 |
| W8 — weak reporting | FR-N-02, FR-N-03 |
| W9 — slow response to feature requests | NFR-T-03 |
| W10 — poor performance on large jobs | FR-A-10, NFR-P-03 |
| O3 — compliance is a selling point | Module H |
| O4 — cash flow is the true problem | FR-K-01, FR-K-05, FR-L-01, FR-L-04 |
| O5 — platform-neutral and offline-first | FR-E-01, FR-E-02 |
| O6 — simple and honest pricing | All CR requirements |
| O7 — automation and open APIs | Module O, IR-10, IR-11 |
| O8 — association partnerships | Q6 |

---

## 16. Abbreviations

| Abbreviation | Meaning |
|---|---|
| ABN | Australian Business Number |
| API | Application Programming Interface |
| CSV | Comma Separated Values |
| ERP | Enterprise Resource Planning |
| FSM | Field Service Management |
| GST | Goods and Services Tax |
| JSA | Job Safety Analysis |
| MVP | Minimum Viable Product |
| PDF | Portable Document Format |
| PRD | Product Requirements Document |
| SMS | Short Message Service |
| SWMS | Safe Work Method Statement |
| SWOT | Strengths, Weaknesses, Opportunities, Threats |
| WCAG | Web Content Accessibility Guidelines |
| WIP | Work In Progress |
