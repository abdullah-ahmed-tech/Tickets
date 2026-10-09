# Tazakir — Integrated Development Plan

**English final handoff | 9 October 2026**

**Scope authority:** the original `UX Blueprint.md`, represented in English by the Product and UX Specification in this package. The finished product supports **English LTR by default and Arabic RTL as an option**. The delivered prototype is an English visual reference only. No production application or backend has been built yet.

**Planning baseline:** 17 two-week sprints across six stages, assuming one fan-app frontend developer, one admin frontend developer, two backend developers, QA, and part-time design/infrastructure support. Re-estimate after Sprint 1 for the actual team and technical choices. These are sequencing and acceptance gates, not guaranteed dates.

## 1. Rule for synchronized frontend and backend delivery

Every backlog item is a **vertical product slice**. A screen-only task or endpoint-only task cannot be called a completed product story. A slice is accepted only when its fan/admin interface consumes a real API in a shared test environment, the server rules and data migration are complete, and QA has exercised success, error, and permission cases in **both languages**. Mock data may support work in progress but cannot pass sprint review.

Frontend, backend, and QA agree together at the start of each story on request and response contracts, state transitions, validation, authorization, loading/empty/error behavior, and example data. A contract change updates both producer and consumer plus automated contract tests in the same integrated change. Dependent work does not start on an unaccepted slice.

**Suggested two-week cadence:** Days 1–2 agree contract and acceptance tests; Days 3–7 implement frontend and backend in parallel; Day 8 integrate in a shared environment; Day 9 test end-to-end and fix defects; Day 10 demo, accept, and plan. Keep capacity for integration defects rather than carrying a disconnected UI into the next sprint.

### Definition of Done for every story

1. The relevant fan and/or admin screen and its required states use a real API and seeded test data.
2. Database schema/migrations, server rules, authorization, idempotency/concurrency handling where relevant, and error responses are complete.
3. Unit tests cover important rules; contract tests protect the UI/API boundary; at least one success and one failure path run end to end.
4. English LTR and Arabic RTL copy, data, errors, focus order, and accessibility are reviewed. Arabic work is delivered in the same sprint, not in a late translation phase.
5. Logs, metrics, and tracing needed to diagnose the slice exist. No critical or high-severity defect remains open at acceptance.

## 2. Stages and sprints

### Stage 1 — Platform and identity (Sprints 1–2)

| Sprint | Frontend in this sprint | Backend and data in this sprint | Shared acceptance proof |
|---|---|---|---|
| **1 — Foundation and sign-in** | Fan and admin shells, design tokens in both directions, Splash/Onboarding, fan registration/login and admin sign-in (`S-01–S-04`, `A-01`). | Technology and deployment decisions, CI, bilingual-content architecture, users, sessions, initial roles, registration and login APIs. | Fan and admin sign in through real APIs in English and Arabic on the same test environment. Contracts and CI pass. |
| **2 — Account recovery and security** | Password request/OTP/reset, profile and settings, language switch, admin 2FA and role-aware navigation (`S-05`, `S-09`, `S-20`, `S-21`, `A-01`, `A-14`). | OTP expiry and attempt limits, saved language preference, session invalidation, server-enforced roles, account audit events. | Language switch persists and mirrors layout; password reset invalidates required sessions; a restricted role is denied by the API, not just by hidden UI. |

**Stage gate:** one deployable environment, real identity for both products, and an agreed permission matrix. Admin features do not advance without matching server authorization.

### Stage 2 — Catalog, stadiums, and fixtures (Sprints 3–5)

| Sprint | Frontend in this sprint | Backend and data in this sprint | Shared acceptance proof |
|---|---|---|---|
| **3 — Clubs and competitions** | Admin create/edit clubs and competitions (`A-07`, `A-15`); fan follow clubs and no-favorite state (`S-17`, `S-06`) in both languages. | Club, competition, season, crest and localized-name models; authorized CRUD and fan read/follow APIs. | A club/competition created in admin appears correctly in both fan languages under publication rules; empty state comes from the API. |
| **4 — Stadium templates** | Admin stadium/section/capacity builder (`A-06`); fan 2D stadium-map read view (`S-11`). | Stadium/section/deck/row/seat schema, season and VIP flags, capacity validation, map-read API. | Editing a stadium template changes the fan map; invalid capacity is rejected by server and shown clearly in UI. |
| **5 — Fixture publication** | Admin dashboard, matches, editor, pricing and section availability (`A-02–A-05`); fan Home, Fixtures, calendar, search, details, priority/sold-out states (`S-06`, `S-07`, `S-10`, `S-27`). | Draft/published match, pricing, priority windows, search/filter/detail APIs, eligibility rules. | Publishing a valid match makes it visible to eligible fans with matching price and time; draft is hidden; priority and sold-out states are server-driven. |

**Stage gate:** admin publishes a valid match and the fan app consumes the same data. No static duplicate fixture catalog lives in frontend code.

### Stage 3 — Core booking, payment, ticket (Sprints 6–8)

| Sprint | Frontend in this sprint | Backend and data in this sprint | Shared acceptance proof |
|---|---|---|---|
| **6 — Seats and quotes** | Stand/row/seat selection, seat-lost recovery, summary and promo outcomes; admin promo and section controls (`S-11`, `S-12`, `A-05`, `A-11`). | Concurrent seat inventory and temporary hold, central quote and fees, promo eligibility/expiry, double-sale prevention. | Two fans race for one seat: only one hold wins; the other sees seat-lost before payment. Both languages show the same server total. |
| **7 — Immediate payment** | Saved/new method, wallet, success/failure/retry, admin order list/details (`S-13`, `S-14`, `A-09`). | Payment-provider adapter in sandbox, payment intent/order states, authenticated webhook, idempotency keys and amount reconciliation. | Replayed webhook cannot duplicate an order or charge; failure is recoverable. No production-payment claim before provider approval. |
| **8 — Issue, verify, refund** | Confirmation, ticket wallet, offline QR display, admin order review/refund (`S-08`, `S-15`, `S-16`, `A-09`). | Unique ticket issuance, current-state gate validation, cancellation/refund with reason, audit and inventory updates. | Valid ticket passes the gate according to policy; cancelled/refunded ticket does not. Both UI products show the updated state. |

**Stage gate:** one complete published-match-to-valid-ticket path, including failed payment, concurrency, and refund tests. Later commerce paths build on this accepted core.

### Stage 4 — Special commerce paths (Sprints 9–11)

| Sprint | Frontend in this sprint | Backend and data in this sprint | Shared acceptance proof |
|---|---|---|---|
| **9 — Pay later** | 24-hour option, pending order, countdown and expiry in fan and admin (`S-08`, `S-13`, `S-26`, `A-09`). | Server-timed hold for exactly 24 hours, reliable expiry job, later payment, cancellation and seat release. | Payment succeeds once before deadline; after deadline it is rejected and seats return to inventory. Both interfaces use server time. |
| **10 — Season passes** | Packages, fixed-seat selection, pass card and activation, priority view; admin packages (`S-23`, `S-10`, `A-16`, `A-04`). | Package inventory, one fixed seat per pass, included-match eligibility/activation, exceptional-match priority rules. | Included-match activation uses the assigned seat without new selection; priority still respects eligibility and price. |
| **11 — VIP** | Fan submitted/approved/rejected and pending-payment states; admin review, quote and deadline (`S-24`, `S-26`, `A-08`). | VIP type/capacity, request state machine, authorized final price, configurable payment deadline and ticket issuance after payment. | No ticket or collected-revenue status before payment; approval, rejection, and expiry agree across fan/admin. |

**Stage gate:** each path has an explicit server-owned state machine with expiry/failure tests. Frontend counters and eligibility never override server truth.

### Stage 5 — Group, transfer, loyalty (Sprints 12–14)

| Sprint | Frontend in this sprint | Backend and data in this sprint | Shared acceptance proof |
|---|---|---|---|
| **12 — Group booking** | Invitations, participant shares, group progress and expiry (`S-30`, `A-09`). | One invitation/share per seat, independent share payments, all-paid confirmation, expiry and approved refund treatment. | Partial payments cannot issue confirmed group tickets; expiry processes seats and money with an auditable record. |
| **13 — Ticket transfer** | Sender/recipient send, accept, decline and wallet states (`S-29`, `S-08`); support history view. | Single-state transfer request, atomic ownership change, old-QR invalidation and audit. | Sender and recipient cannot both use one ticket; decline preserves sender ownership. |
| **14 — Loyalty** | Balance, history, reward catalog and redemption outcome (`S-25`); admin rule view. | Auditable points ledger, atomic earning/redemption, eligibility and promo interaction rules. | Every balance change has a ledger entry; retries do not duplicate points; both products show one balance. |

**Stage gate:** money, ticket ownership, and points remain consistent after each transition, including retries and connection loss.

### Stage 6 — Operations and release (Sprints 15–17)

| Sprint | Frontend in this sprint | Backend and data in this sprint | Shared acceptance proof |
|---|---|---|---|
| **15 — Notifications and support** | Notification center/deep links, help requests, admin composition/scheduling (`S-18`, `S-19`, `A-12`) in both languages. | Localized templates by user preference, audience selection, delivery/retry log, support cases linked to orders/tickets. | Changed-match alert arrives in the preferred language and opens the right record; retries do not double-send; support gives a case number. |
| **16 — Admin operations and content** | Users, reports, settings and legal content (`A-10`, `A-13`, `A-14`, `S-22`), offline/update states (`S-28`). | Real-data reports and export permissions, approved English/Arabic legal versions, operational settings/audit, minimum-app-version policy. | Report reconciles to orders and export is role-restricted; legal and system messages follow language preference. |
| **17 — Stabilize and launch** | UX/accessibility fixes at 320/390/430px mobile and 1024/1440px admin, final English LTR and Arabic RTL copy. | Booking/payment load tests, security/role review, backup and restore, observability, alerts, rollback and deployment plan. | Bilingual UAT for every Blueprint route, order/payment/ticket reconciliation, no critical/high defect, signed product and operations approval. |

**Launch gate:** screen completion alone is insufficient. Concurrency, payment, QR, permission, recovery, and operational test evidence are required, together with approved payment provider, legal text, refund rules, and asset rights.

## 3. Backlog, integration, and language controls

- Maintain **one backlog organized by user journey**. Each story includes frontend, API contract, backend, data, QA, UX and operations checks. Closing a frontend or backend subtask does not close the product story.
- Version API contracts with examples for success, validation, unauthorized, conflict, and expired states. CI fails on consumer-breaking changes until both sides and tests update together.
- Deploy an integrated test environment every day with repeatable seed data. Report end-to-end journey health daily. Reserve sprint capacity for integration defects.
- Track accepted end-to-end journeys, contract/E2E failures, defect age, order/payment inconsistencies, and coverage of Blueprint screens and states. Do not use raw screen or endpoint count as progress.
- Each new screen/state ships **English and Arabic copy, correct direction, localized server-provided names/errors, and bilingual acceptance tests in that sprint**. Stable IDs, order numbers, amounts, and business states remain language-neutral. Missing Arabic sample boards in the prototype never waive this condition; design reviews RTL differences within the sprint.

## 4. Decisions required before dependent work

| Decision | Latest needed | If unresolved |
|---|---|---|
| App/admin/backend frameworks, database and hosting | End of Sprint 1 | Do not fragment production contracts across incompatible choices. |
| Card/wallet provider, pay-later model, sandbox and webhook specification | Before Sprint 7; pay-later detail before Sprint 9 | Build/test adapter boundaries, but do not accept or market production payment readiness. |
| Cancellation/refund/service-fee and incomplete-group-share policy | Before Sprint 8; group detail before Sprint 12 | Do not activate or accept live refunds without approved policy. |
| Loyalty earning, redemption and promo interaction rules | Before Sprint 14 | Do not enable real reward redemption. |
| Final bilingual legal copy, company identity, and crest use rights | Before Sprint 16/launch | Do not publish unapproved legal or branded content. |

The plan sequences the full Blueprint scope while keeping frontend, backend, QA, and both languages aligned. It reduces integration rework; it cannot eliminate the need for testing and final approval.
