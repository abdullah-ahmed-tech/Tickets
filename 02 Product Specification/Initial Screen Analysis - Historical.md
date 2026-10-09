# Initial Screen Analysis — Historical Baseline

This English rendering records the project's **initial** screen inventory. It is included to show how the work evolved. The later [Product and UX Specification](./Tazakir%20Product%20Specification.md) and original `UX Blueprint.md` supersede any older assumption here, including generic A/B/C pricing, 2D/3D uncertainty, and an early description of season benefits as a discount.

## Initial user routes

- A guest enters Splash → Onboarding → Login/Sign Up. Attempting a booking prompts authentication in a modal.
- A signed-in fan follows Home → Discovery → Checkout → Post-booking.
- A season member follows the standard route with a season-ticket activation action at Match Details or Payment. The later Blueprint refines this into a fixed season seat and included-match activation.

## Original 22 fan screens

| ID | Screen | Initial purpose and controls |
|---|---|---|
| S-01 | Splash | Brand, competition name, loading indicator. |
| S-02 | Onboarding | Three explanatory slides about quick booking, interactive maps, and following clubs; Skip/Next. |
| S-03 | Login | Phone/email, password, forgot-password route. |
| S-04 | Sign Up | Name, mobile, password, favorite-club selector. |
| S-05 | Forgot Password | Mobile, OTP, new password. |
| S-06 | Home | Upcoming preferred-club fixtures, match cards, quick booking, recommendations. |
| S-07 | Fixtures | Week/month calendar, round filters, match list. |
| S-08 | My Tickets | Upcoming/past/cancelled tickets and compact QR. |
| S-09 | Profile | Photo, name, loyalty balance, settings and favorites navigation. |
| S-10 | Match Details | Club crests, venue, classification, prices, Select Seats. |
| S-11 | Stadium Map | Interactive seating map and available/full/closed sections. The later decision is 2D. |
| S-12 | Booking Summary | Seats, quantity, total, promo code, continue to payment. |
| S-13 | Payment Methods | Saved/new card, wallet, pay-later choice. |
| S-14 | Payment Result | Success acknowledgement or failure reason and retry. |
| S-15 | Confirmation | Order number, seats, entry instructions, view ticket. |
| S-16 | Full-screen QR | Scannable code, brightness behavior, fixture details. |
| S-17 | Manage Clubs | Follow/unfollow available league clubs. |
| S-18 | Notifications | Ticket releases, schedule changes, and results in a chronological list. |
| S-19 | Help Center | Searchable and expandable FAQs, contact support. |
| S-20 | Settings | English/Arabic switch, privacy, push preferences, session logout. |
| S-21 | Edit Profile | Photo, name, mobile and password changes. |
| S-22 | Legal | Privacy Policy and Terms display. |

## Original admin functions

The early analysis proposed a separate web admin experience for match management, ticket-tier pricing, opening and closing stadium sections, VIP request review, and attendance/sales statistics. The later Blueprint expanded this to the 16 named A-01–A-16 admin screens and their states. Use the later specification for implementation.
