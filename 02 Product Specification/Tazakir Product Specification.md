# Tazakir — Product and UX Specification

**Final English handoff | 9 October 2026**

This document is the English delivery specification derived from the project's [original UX Blueprint](<../07 Original Sources/UX Blueprint.md>), initial screen analysis, and the final design files. The Arabic Blueprint remains unchanged in this package's original-sources archive. Where an early analysis and the later Blueprint disagree, the later Blueprint decisions described here take precedence.

## 1. Product, scope, and current status

Tazakir is a football match ticketing platform with a **fan mobile application** and a **separate desktop administration panel**. The fan app covers discovery, seat selection, payment, ticket use, season passes, VIP requests, loyalty, group payment, and ticket transfer. Admin users maintain the catalog, stadiums, matches, pricing, orders, users, notifications, legal content, and reports.

The project is at the **design and development handoff stage**. The HTML files are reviewable design artifacts, not working booking software. No production backend, payment gateway, inventory service, gate validation service, or operational deployment is included in this delivery.

The final design contains **108 unique boards on two product pages**: 76 fan app boards and 32 admin boards. A duplicate device home board and three Arabic demonstration boards were removed from the visual files. The final product still requires **English as the default LTR language and Arabic as an optional RTL language**, including a language switch in S-20. The current prototype is an English visual reference; its lack of Arabic demonstration boards does not narrow the bilingual implementation scope.

The governing product rule is **full-scope delivery**: the features listed below are part of the planned product, not placeholders to be discarded after an MVP. The staged development plan organizes implementation without reducing the feature set.

## 2. Fan app screen inventory

| ID | Screen | Required behavior and important states |
|---|---|---|
| S-01 | Splash | Show Tazakir identity and loading state; resolve onboarding or authentication destination. |
| S-02 | Onboarding | Three slides, Skip/Next/Get Started, concise explanations of booking, seat maps, and following clubs. |
| S-03 | Login | Phone or email and password; route to password recovery and registration. |
| S-04 | Sign Up | Name, Egyptian mobile number, password, and favorite club selected from the managed club catalog; inline validation. |
| S-05 | Forgot Password | Request a code, verify the six-digit OTP, set and confirm a new password; expiry, resend timer, and field errors. |
| S-06 | Home | Upcoming match for the favorite club, recommendations, other fixtures, search and notifications entry points; no-favorite-club state. |
| S-07 | Fixtures | Week/month calendar, competition and round filters, match cards, and no-fixtures state. |
| S-08 | My Tickets | Upcoming, pending, past, and cancelled tabs; VIP/season labels; ticket details and compact QR; empty state. |
| S-09 | Profile | Account summary, loyalty balance, favorite clubs, notifications, help, settings, profile editing, and season-pass discovery. |
| S-10 | Match Details | Teams, competition, venue, kickoff, pricing and demand; season-seat information, priority-window countdown, sold-out and rescheduled states; separate Seat and VIP actions. |
| S-11 | Stadium Map | Interactive 2D stadium map, stand/deck/row/seat selection, availability labels, sold hatching, closed sections, VIP identification, and seat-lost recovery. |
| S-12 | Booking Summary | Selected seats, fee and discount breakdown, valid/invalid promo states, total from the server; preserve seat selection through guest authentication. |
| S-13 | Payment Methods | Saved/new card, wallet, pay-now and 24-hour pay-later choice; explain a temporary hold before confirmation. |
| S-14 | Payment Result | Clear success and failure branches, retry and change-method actions without duplicate charge. |
| S-15 | Confirmation | Order number, seats, entry guidance, VIP/season label when applicable, and link to ticket. |
| S-16 | Full-screen QR Ticket | Large scannable code and match details; offline display, brightness behavior, and authoritative gate validation. |
| S-17 | Manage Clubs | Follow and unfollow clubs in the managed catalog, with official crests where supplied. |
| S-18 | Notifications | Chronological grouping, read/unread state, and deep links to the originating match, ticket, or order. |
| S-19 | Help Center | Search and expand FAQs; submit a support request linked to a relevant order if available. |
| S-20 | Settings | English/Arabic language switch, privacy, push preferences, legal pages, and sign-out. |
| S-21 | Edit Profile | Photo, name, mobile number, and password change with field validation and session handling. |
| S-22 | Legal | Versioned Privacy Policy and Terms & Conditions supplied from admin-managed content. |
| S-23 | Season Tickets | Browse packages and savings, select one eligible fixed seat for the season, pay, display a season card, and activate included matches without reselecting the seat. |
| S-24 | VIP Request | Choose serviced VIP box or VIP seat, guest count, notes, approximate range, and submit for admin review; submitted, approved, and rejected outcomes. |
| S-25 | Loyalty | Balance, progress, transaction history, reward catalog, disabled insufficient-balance actions, and redemption result. |
| S-26 | Pending Order | Shared pattern for 24-hour pay-later and approved VIP awaiting payment: server-based countdown, details, pay now, cancel, expiry. |
| S-27 | Search | Search team, stadium, or competition; recent searches, results, and no-results action. |
| S-28 | System States | Reusable no-connection, required-update, empty, loading, error, disabled, and success patterns. |
| S-29 | Ticket Transfer | Send to phone/email; recipient accepts or declines; ownership and QR validity change on acceptance. |
| S-30 | Group Booking | Split payment by seat, send secure invitations, show each participant's share and group progress, and handle expiry. |

## 3. Admin panel screen inventory

| ID | Screen | Required behavior and important states |
|---|---|---|
| A-01 | Admin Login | Role-based sign-in with optional second factor and access controls. |
| A-02 | Dashboard | Today's sales, upcoming matches, pending VIP requests, expiring pay-later holds, recent bookings, and sales summaries. |
| A-03 | Matches | Search and filter by competition and status; show fixture, venue, occupancy, and state. |
| A-04 | Match Editor | Select competition, clubs, stadium, date and kickoff; draft/publish and exceptional-match priority-window dates; review before publishing. |
| A-05 | Pricing and Sections | Price actual stadium tiers and VIP seats, open/close match sections, show occupancy, and publish only after required setup. |
| A-06 | Stadiums | Maintain reusable 2D section-map templates, capacities, deck/side divisions, season-eligible areas, VIP seats/boxes and box capacity. |
| A-07 | Clubs and Teams | Add/edit clubs, crests, and catalog membership; support new continental opponents when needed. |
| A-08 | VIP Requests | Review type, guests and capacity; set final price and payment deadline; approve or reject with notification and audit. |
| A-09 | Orders and Bookings | Search by order/phone/email; inspect seats and payment history, pending BNPL countdown, cancel/refund with reason, resend ticket. |
| A-10 | Users | Fan list, booking history, season-member status, and controlled account freeze. |
| A-11 | Discount Codes | Create and manage value, validity, eligibility, usage limits, and status. |
| A-12 | Notifications | Compose, target, preview, schedule, and review delivered messages; include season holders as an audience. |
| A-13 | Statistics and Reports | Attendance, revenue by ticket category including VIP, trend charts, and authorized CSV/PDF export. |
| A-14 | Settings | Platform/payment settings, maintenance, team roles and invitations, legal-content editor and publication. |
| A-15 | Competitions | Domestic and continental competition catalog, seasons, match counts, and active status. |
| A-16 | Season Packages | Club, stadium, eligible section, price, included match count, and sold/available fixed-seat counts. |

The board inventory CSV in this folder lists every embedded board in display order. The `.dc.html` values there are **internal board IDs inside the Artifact**, not separate files.

## 4. End-to-end journeys

### Standard booking

Browse Home/Fixtures → Match Details → eligibility and priority check → stand/deck/row/seat → server quote and optional discount → guest sign-in if needed without losing selection → payment method → success or failure → confirmation → ticket QR. A season holder activating an included match uses the previously assigned fixed seat and skips new seat selection. An exceptional match may give season holders an earlier **paid** booking window; the priority right does not make that match free.

### Match publication

Authorized admin selects or creates competition, clubs, and stadium → configures draft match and any priority window → sets tier/VIP prices and section availability → reviews → publishes. The published fixture becomes visible to the fan app according to eligibility. A draft is never exposed as a live ticket offer.

### VIP

Fan submits a box or seat request → admin reviews capacity and sets a final price and payment deadline → fan receives approval or rejection → approved request becomes a pending order → ticket is issued only after successful payment. The estimate is never shown as collected revenue.

### Pay later, season, group, and transfer

- **Pay later:** the server holds selected seats for exactly 24 hours from creation. Payment confirms the order; expiry cancels it and releases the seats. Fan and admin see the same server time.
- **Season:** admin defines a package and eligible inventory; fan purchases one fixed seat for the season and activates included matches. Package terms control coverage; exceptional-match priority may be separate.
- **Group:** one invitation and share are attached to each seat. The order is confirmed only after all required shares are paid. On expiry, seats and paid shares follow the approved refund policy.
- **Transfer:** the sender retains ownership until recipient acceptance. Acceptance atomically moves ownership and invalidates the sender's QR. Decline or cancellation leaves sender ownership intact.

## 5. State and data contracts for implementation

The normal seat lifecycle is **published match → available section → selected seat → server quote → temporary hold → payment pending/succeeded/failed → issued ticket**. The final amount is seat prices plus service fees minus an accepted discount. No payment starts after the seat has been lost. Each seat has an identity under a stadium, section, optional deck, row, and seat number. Stadium structures vary; the software must not assume every stadium has three tiers or two decks.

Payment creation and webhooks must be idempotent. Seat holds must prevent double sale under concurrency. The ticket QR must be unique and linked to the ticket's current status; used, cancelled, refunded, or transferred tickets must not authorize fresh entry. The security team chooses signing, offline-display, and gate-verification mechanics. A locally visible offline pass never overrides authoritative gate validation.

Validation covers phone/email, password policy, OTP expiry and resend limits, nonnegative admin values, section capacity not falling below sold/allocated inventory, and discount outcomes such as valid, expired, ineligible, and exhausted. Publishing a match, approving VIP, refunding an order, freezing an account, or publishing legal text requires visible confirmation and an audit record. Server authorization is mandatory even when the UI hides an action.

All mock names, prices, order numbers, and kickoff times are illustrative. A displayed “Connected” payment setting in the design does **not** prove a real integration exists.

## 6. Design system and accessibility

The interface follows the supplied Athletics design system: Obsidian `#000000`, Charcoal `#1d1d1d`, Paper White `#ffffff`, and Ash `#d6d5d0`. Functional states are monochrome and always combine **explicit text, a shape/icon or hatch, and surface contrast**. Official club/competition crests may retain their brand colors; state meaning must not depend on chromatic color. Use hairline borders, restrained cards, pill actions, no elevation or gradients, and an 8px spacing base.

The working UI font substitutes are Newsreader for English display type and IBM Plex Sans for English functional type. Arabic uses Noto Serif Arabic and IBM Plex Sans Arabic as defined in the Blueprint. English LTR is the default; selecting Arabic mirrors navigation, arrows, alignment, and relevant layout in RTL. Deliver both languages with each functional development slice even though the delivered visual prototype currently contains English boards only.

The approved first-release stadium map is **interactive 2D**, rendered as an oval stadium around a horizontal pitch, with actual section geometry and club crests where provided. VIP is identified by a double hairline frame and text. Seat availability uses text and hatching as well as opacity, never color alone. Provide an accessible list-based seat alternative for keyboard and screen-reader use.

Design reference canvases are approximately 390×844 for mobile and 1440×900 for admin, **not fixed production viewport constraints**. Review mobile layouts at 320, 390, and 430px and admin at 1024 and 1440px. Keep primary actions reachable above device controls and keyboards; allow structured table overflow on smaller admin widths. Test focus order, touch targets, labels, contrast, and both reading directions.

## 7. Administrative roles

| Role | Intended scope |
|---|---|
| Super Admin | All screens, team and permissions, platform settings. |
| Match Manager | Matches, stadiums, clubs, competitions, packages, pricing, and priority windows. |
| Finance | Orders, payments, refunds, reports, and authorized payment settings. |
| Support | Users, tickets, VIP requests and ticket resend; no match publication or pricing changes. |

Exact read/write permissions need a server-enforced operation matrix during development. Hidden buttons are not a security boundary.

## 8. Assets, content, and approved decisions

The supplied assets include the Tazakir wordmark in light/dark SVG and PNG, a 1024×1024 app icon, and a set of club and competition crests. The approved design uses real supplied crests where available and a neutral placeholder where not supplied. Confirm use rights before production. New club/continental-opponent logos must be uploadable through A-07; opponents cannot be treated as a fixed list.

The product supports multiple stadiums and domestic/continental competitions within one country. Stadium data must model tier, deck, and side per venue rather than forcing a universal A/B/C layout. The source Blueprint records illustrative stadium capacities and a club list from an earlier design review; these are **sample content requiring fresh operational verification**, not a production database.

Key decisions retained from the Blueprint:

1. A season pass assigns a fixed seat for its season and may provide paid priority access to exceptional fixtures.
2. Pay-later temporarily holds seats for 24 hours; the gateway/provider is not yet selected.
3. VIP comprises serviced boxes and VIP seats and requires admin review and final pricing.
4. The stadium map is 2D for the first release and matches the realistic tier/deck/side structure.
5. The design remains monochrome for functional UI states.
6. The default language is English LTR; Arabic RTL is available from Settings in the product implementation.
7. Loyalty includes a full redemption catalog, not only a points balance.
8. Search, system states, transfer, and group payment are in full scope.
9. The final product name is **Tazakir**. Use actual generators for functional artifacts such as QR codes rather than decorative imitations.
10. Official crests supplied later replaced earlier generic crest placeholders where possible.

An in-app official club merchandise store and its discounts are **outside this ticketing product**. Any later store integration needs its own decision. Stadium photography and payment-brand logos are optional future visual assets, subject to rights and licensing.

The legal screens contain draft Privacy Policy and Terms text, including booking-specific subjects such as pay-later, transfer, resale restrictions, and season passes. They require the real company identity, contact details, effective date, and legal review before publication. Neither the design text nor this handoff is legal approval.

## 9. Open decisions and acceptance before production

The team may begin interface, data-model, and API development, but the following must be settled before live transactions or launch: the card/wallet/pay-later provider and whether pay-later is a third-party service or internal temporary hold; loyalty earning and redemption rules; refund/service-fee handling for cancelled and incomplete group orders; changed/cancelled fixture treatment across ordinary, season, and VIP tickets; approved legal identity/text; and logo rights.

Acceptance requires review of at least one complete immediate-payment path, expired pay-later path, season path, VIP approval and rejection, group payment, and transfer in **English and Arabic**. The design review must also check errors, empty and offline states, admin roles, accessibility, and smaller viewports. Implementation then needs separate functional, security, payment, load, and operational tests. No static board alone proves a service works.
