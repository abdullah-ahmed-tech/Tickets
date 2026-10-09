# Tazakir — Final English Design Handoff

**Prepared:** 9 October 2026  
**Project:** Football match ticketing fan app + admin panel  
**Delivery state:** Design and implementation planning complete; production software has **not** been developed.

## What to open first

1. [Product and UX Specification](<../02 Product Specification/Tazakir Product Specification.md>) — the English product scope, user journeys, screen requirements, business states, design rules, roles, and open decisions.
2. [Unified Prototype](<../03 Design/Tazakir Prototype.html>) — browse the final **108 unique visual boards** in two pages: 76 fan app and 32 admin. The presentation shell in this package is English.
3. [Complete Editable Artifact](<../03 Design/Tazakir App and Admin Screens.html>) — the full embedded design source and canvas. It has the same 108 displayed boards and two product pages.
4. [Integrated Development Plan](<../06 Delivery Plan/Integrated Development Plan.md>) — 17 synchronized sprints across six stages, with frontend, backend, QA, and both languages delivered in each slice.

The [Design Board Inventory](<../02 Product Specification/Design Board Inventory.csv>) lists each board's display order, product, title, internal ID, and canvas dimensions. The [Initial Screen Analysis](<../02 Product Specification/Initial Screen Analysis - Historical.md>) records the earlier 22-screen baseline; later Blueprint decisions supersede its old assumptions.

## Folder map

| Folder | Contents |
|---|---|
| `01 Overview` | This guide and delivery status. |
| `02 Product Specification` | English consolidated specification, historical initial analysis, and all-board inventory. |
| `03 Design` | English-presentation prototype and the complete design Artifact. |
| `04 Design System` | The supplied Athletics style reference, CSS, and JSON tokens (already in English). |
| `05 Brand Assets` | Supplied Tazakir logos, app icon, and team/competition crests. |
| `06 Delivery Plan` | English, vertically integrated development plan. |
| `07 Original Sources` | Unchanged Arabic source documents, archived to preserve the full project record. |

## Scope and precedence

The unchanged [original UX Blueprint](<../07 Original Sources/UX Blueprint.md>) in this package is the detailed design authority. The English specification consolidates its approved scope for handoff. The final product requires **English LTR as default and Arabic RTL as an option**, with a language switch and bilingual implementation. The visual prototype currently demonstrates English screens only; three earlier Arabic demonstration boards were removed by request. Their removal does **not** cancel Arabic development.

The prototype and Artifact are review tools, not operational apps. They contain representative sample names, prices, dates, orders, and legal copy. The HTML boards are embedded in the two design files; individual `.dc.html` files are not part of this delivery.

## Achieved work

- Defined the full fan app (`S-01–S-30`) and admin panel (`A-01–A-16`) with user journeys, branch states, and acceptance rules.
- Created and consolidated the visual design into 108 unique boards across two product canvases. `PhoneHomeScreen` is first in the fan page; the exact duplicate `PhoneHomeScreenAccount` was removed.
- Applied the Athletics monochrome system, supplied brand assets, 2D stadium structure, and matching fan/admin interface patterns.
- Specified fixed-seat season passes, 24-hour pay-later holds, VIP review, group payment, ticket transfer, loyalty, notifications, legal content, and admin operations.
- Planned synchronized frontend/backend delivery with contracts, shared acceptance tests, bilingual checks, and stage gates.

## Remaining approvals before production or launch

The payment and wallet provider, pay-later implementation model, refund and group-share policy, loyalty earning/redemption policy, company/legal details and review, and logo use rights need decisions before their related sprints or launch. The legal wording inside screens is a draft. Visual sign-off and functional, security, payment, load, and operational testing are still required. No screenshot set or production code is claimed in this handoff.
