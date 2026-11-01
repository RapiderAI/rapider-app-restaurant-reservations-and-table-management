<!-- Rapider Official App SOW & Specification | App #171: Restaurant Reservations & Table Management (restaurant-reservations-and-table-management) | Domain: HSP -->

# #171 Restaurant Reservations & Table Management (`restaurant-reservations-and-table-management`) — Scope of Work (SOW)

- **App Number & Name:** `#171` — Restaurant Reservations & Table Management
- **Proposed App Key:** `restaurant-reservations-and-table-management`
- **Suite / Domain Key & Model Prefix:** `HSP` (`Hsp*`)
- **Function Category:** 18. Hospitality, Restaurants & Travel
- **Representative Product (`P1`):** OpenTable
- **Combined Feature Catalog:** [../combined-features/171-restaurant-reservations-and-table-management-features.md](../combined-features/171-restaurant-reservations-and-table-management-features.md)
- **Target Release Posture:** Commission-Free Online Cover Booking, Multi-Zone Floor Plans, Shift Pacing, Digital SMS Waitlist, Prepaid Experiences & Diner 360 CRM Microapplication

---

## 1. Executive Outcome & Target Audience

### 1.1 Business Problem Solved
Full-service restaurants, fine-dining tasting rooms, hotel signature dining venues, and beach/rooftop clubs lose up to 20% of prime-time Friday/Saturday seat capacity to unpenalized no-shows, unpaced `19:00` arrival waves that overwhelm the kitchen, manual clipboard waitlists, uneven server section seating, and third-party marketplace per-cover fees that withhold direct diner data. **Rapider Restaurant Reservations & Table Management (`restaurant-reservations-and-table-management`)** provides an operator-owned reservation engine, multi-zone combinable floor plans, 15-minute cover-pacing matrices, prepaid ticketed tasting experiences, two-way SMS walk-in & cancellation-notify waitlists, fair server cover rotation, and a unified Diner 360 CRM synchronized in real time with `#170 Restaurant Management & Kitchen Operations` and `#169 Hotel PMS`.

### 1.2 Target Personas & Progressive Disclosure
- **SME Fast-Path Defaults (Neighborhood Bistros, Casual Dining, Wine Bars):** Launch in 10 minutes with a single dining room + patio map, standard Lunch/Dinner shift hours, commission-free `ComSite` booking link, SMS walk-in waitlist (`<rapider-phone-input>`), and live `<rapider-kanban>` host stand board.
- **Enterprise Progressive Disclosure (Fine-Dining Groups, Michelin Tasting Rooms, Multi-Outlet Resorts, Beach Clubs):** Unlock multi-zone floor combinations, 15-minute cover-pacing caps, prepaid tasting-menu tickets & minimum-spend cabanas (`HspDiningExperience`), card-on-file no-show protection (`FinPaymentIntent`), *Priority Notify* cancellation backfilling, cross-venue `HspDinerProfile` spend/VIP auto-tagging, `#169` in-house hotel guest recognition, and Revenue Per Available Seat Hour (`RevPASH`) yield analytics.

### 1.3 Measurable Business Outcomes
- **<= 2.5% Prime-Time No-Show Rate:** Automated 24h SMS confirmation links combined with peak-slot card holds/prepaid deposits (`FinPaymentIntent`) and *Priority Notify* slot backfilling cut empty prime tables by over 75%.
- **+15% Peak-Shift `RevPASH` & Smoother Kitchen Pacing:** 15-minute arrival caps and AI table-tetris slot optimization increase second/third table turns without slamming `#170` KDS stations.
- **100% Operator-Owned Diner Relationship:** Every visit, allergy, celebration date, and `#170` check spend enriches canonical `CrmContact` + `HspDinerProfile` with zero third-party per-cover ransom.

### 1.4 Benchmark Summary (`P1`–`P6`)
Combines the floor-plan combinations, 15-minute pacing, and SMS waitlist of **`P1` OpenTable**, operator-owned Diner 360 CRM, 70+ auto-tags, and server rotation of **`P2` SevenRooms**, *Priority Notify* cancellation backfill and POS course-color telemetry of **`P3` Resy (ResyOS)**, prepaid tasting-menu ticketing of **`P4` Tock**, hotel in-house VIP guest recognition of **`P5` Oracle Simphony Table Management**, and native ERP/website deposit & CRM unification of **`P6` Odoo Enterprise**.

---

## 2. In-Scope, Out-of-Scope & Suite Ownership Boundaries

### 2.1 In-Scope Capabilities
1. Multi-zone dining spaces (`HspDiningZone`), physical & combinable tables (`HspDiningFloorTable`), weather-contingent patio holds, and VIP house-hold inventory.
2. Shift pacing templates (`HspDiningShift`) defining party-size turn times, 15-minute arrival cover caps, booking lead windows, and deposit/no-show policies.
3. Individual/group reservations (`HspDiningReservation`), prepaid ticketed experiences & add-ons (`HspDiningExperience`), two-way SMS confirmation/late-grace updates, and no-show fee waiver governance.
4. Digital walk-in & remote waitlists (`HspWaitlistEntry`) with live wait quotes, one-tap SMS paging, grace-window countdowns, and *Priority Notify* cancellation slot backfilling.
5. Host-stand shift timeline & `<rapider-kanban>` seating board, fair `HrEmployee` server section rotation, two-way `#170` course/check progression sync, `#169` hotel guest lookup, pre-shift lineup ("chit"), and `HspDinerProfile` analytics (`RevPASH`).

### 2.2 Out-of-Scope Capabilities (Delegated to Adjacent Rapider Apps)
- **Order entry, nested modifiers, KDS station firing, split-check calculations, and tip-pool distributions:** Owned by `#170 Restaurant Management & Kitchen Operations` (`restaurant-management-and-kitchen-operations`).
- **Recipe yields, ingredient par levels, and food-cost variance:** Owned by `#175 Restaurant Food Cost & Recipe Management`.
- **Full-venue banquet/wedding BEO contracting and sales pipeline:** Promoted from group inquiries (`12+ pax`) into core `crm` (`CrmOpportunity`) and `#169` `HspGroupBlock`.
- **Payment gateway tokenization, SMS carrier delivery, and post-visit survey authoring:** Owned by built `payments`, `sms`, `email`, and `surveys`.

### 2.3 Cross-Suite Ownership & Integration Contract

| Domain / App | Owns (Canonical Models) | Integration Contract with `restaurant-reservations-and-table-management` |
| :--- | :--- | :--- |
| **`restaurant-reservations-and-table-management` (`#171` — This App)** | `HspDiningZone`, `HspDiningFloorTable`, `HspDiningShift`, `HspDiningExperience`, `HspDinerProfile`, `HspDiningReservation`, `HspWaitlistEntry` | Authoritative source of truth for table inventory, cover pacing, reservations, waitlists, seating state, and diner hospitality preferences. |
| **`restaurant-management-and-kitchen-operations` (`#170` — HSP)** | `HspRestaurantOutlet`, `HspDiningCheck`, `HspKitchenTicket` | `#171` emits `hsp.table.party_seated` (table, party size, allergies, VIP tags, deposit credit) to open `HspDiningCheck`; `#171` consumes `hsp.restaurant.course_fired` & `hsp.restaurant.check_settled` to update live table turn state and `HspDinerProfile.lifetimeSpend`. |
| **`hotel-property-management-system-pms` (`#169` — HSP)** | `HspGuestProfile`, `HspHotelReservation` | Cross-references checked-in hotel guests by `CrmContact` / room number to badge in-house VIPs and meal-plan inclusions on `#171` host screens. |
| **`crm` (`CRM` Suite)** | `CrmContact`, `CrmAccount`, `CrmOpportunity` | `HspDinerProfile.contactId` links 1:1 to `CrmContact`; large-party PDR/buyout inquiries (`12+ covers`) promote to `CrmOpportunity`. |
| **`payments` & `billing` (`FIN` Suite)** | `FinPaymentIntent`, `FinInvoice` | Card-on-file holds, upfront per-cover deposits, prepaid tasting tickets, and no-show fee captures run via `FinPaymentIntent` / `FinInvoice`. |
| **`sms`, `email`, `surveys` (`MKT`) & `support` (`SUP`)** | `MktSmsMessage`, `MktEmailMessage`, `MktSurvey`, `SupTicket` | Delivers 24h confirmations, SMS "Table Ready" pages, *Priority Notify* alerts, and post-dining `MktSurvey` links; low ratings link `SupTicket` recovery alerts. |
| **`employees` (`HR` Suite) & Platform** | `HrEmployee`, Home `WorkItem`, `projectChannelMessage` | Maps server sections to `HrEmployee`; routes disputed no-show fee waivers via Home `WorkItem`s; posts AI pre-shift VIP chits in `projectChannelMessage`. |

---

## 3. Primary Web Pages & Sidebar Navigation Architecture

To comply strictly with the **Rapider Minimum 3 Items Sidebar Rule**, all visible pages are organized into **3 sidebar sections (`Host Stand`, `Guest & Experiences`, `Governance`) containing 3 visible items each (9 visible menu items total)**. Detail views and creation/edit drawers set `displayOnMenu: false`.

| # | Route | Page Title | Sidebar Section | Menu Visible | Key Components & UX |
| :--- | :--- | :--- | :--- | :--- |
| 1 | `dashboard` | Shift & Cover Pulse | `Host Stand` | `true` (Order 1) | Live KPI cards (`countSWR`): Booked Covers vs. Capacity, Walk-Ins Seated, Active Waitlist Count, Current `RevPASH`, No-Show Rate %, 15-min arrival pacing bar chart. |
| 2 | `host-board` | Live Floor & Seating Board | `Host Stand` | `true` (Order 2) | Dual view: `<rapider-kanban>` (`UPCOMING`, `ARRIVED_AT_HOST`, `SEATED_DINING`, `MAINS_ON_TABLE`, `CHECK_DROPPED`, `BUSING_DIRTY`) + visual zone/table grid with server rotation counters. |
| 3 | `waitlist` | Walk-In & Notify Waitlist | `Host Stand` | `true` (Order 3) | Live `HspWaitlistEntry` queue (`findSWR`), `#activeFilterTagsBar` with `Clear all`, `<rapider-phone-input>` quick-add, AI wait-quote badge, one-tap **Page SMS** & **Seat Now** actions. |
| 4 | `reservations` | Reservation Book | `Guest & Experiences` | `true` (Order 4) | Searchable `HspDiningReservation` ledger across dates/shifts/channels/VIP tags, `#activeFilterTagsBar`, deposit status chips, clickable `#RES-...` -> `reservation-detail`. |
| 5 | `diner-directory` | Diner 360 Guestbook | `Guest & Experiences` | `true` (Order 5) | `HspDinerProfile` CRM table with auto-tags (`VIP`, `ALLERGY`, `IN_HOUSE_HOTEL`, `REGULAR`), lifetime visits, avg spend/cover (`Decimal128`), clickable diner name -> `diner-detail`. |
| 6 | `experiences` | Prepaid Tickets & Tasting | `Guest & Experiences` | `true` (Order 6) | `HspDiningExperience` catalog (Chef's Counter, Wine Pairing Dinner, Rooftop Cabana Minimums), ticket inventory sold/remaining, `Decimal128` prepayment totals. |
| 7 | `floor-zones` | Floor Plans & Table Combos | `Governance` | `true` (Order 7) | `HspDiningZone` and `HspDiningFloorTable` configurator, combinable table pairs/trios with priority rank, ADA/patio attributes, weather-pause toggle. |
| 8 | `shifts-pacing` | Shifts, Pacing & Policies | `Governance` | `true` (Order 8) | `HspDiningShift` rules: 15-min cover caps, party-size turn minutes, VIP house holds, peak card-hold / no-show fee rules (`Decimal128`). |
| 9 | `preshift-analytics` | Pre-Shift Chit & RevPASH | `Governance` | `true` (Order 9) | Printable/digital pre-service lineup roster (VIPs, severe allergies, occasions, `#169` room guests) plus `RevPASH`, turn-time variance, and no-show waiver audit metrics. |
| 10 | `reservation-detail` | Reservation & Seating 360 | *(Hidden)* | `false` | Full `HspDiningReservation` cockpit (`?id=...`): table assignment, SMS confirmation log, `FinPaymentIntent` deposit/hold status, linked `#170` `HspDiningCheck` live total, `Back to list`. |
| 11 | `diner-detail` | Diner 360 Profile | *(Hidden)* | `false` | Complete `HspDinerProfile` (`?id=...`): dietary allergies, favorite tables/wines, visit & `#170` item history, `#169` hotel stay badge, `SupTicket` service recovery notes, `Back to Guestbook`. |
| 12 | `reservation-drawer` | Book / Edit Reservation | *(Hidden)* | `false` | Sliding drawer checking real-time 15-min pacing & table combos, `<rapider-phone-input>` guest mobile, allergy/occasion selectors, deposit link, `try/catch/finally` save reset, auto-close. |
| 13 | `waitlist-drawer` | Add Walk-In / Notify Request | *(Hidden)* | `false` | Fast host-stand sliding drawer with `<rapider-phone-input>`, party size, zone preference, grounded AI wait-minute quote, and instant SWR list update on save. |

---

## 4. Canonical Data Models (`Hsp*` — 7 Models)

All models omit `projectId`, use platform UUIDs (`00000000-xxxx-xxxx-xxxx-xxxxxxxxxxxx` in seed data), enforce optimistic `version`, and store all deposits, ticket prices, minimum spends, and diner spend metrics as `Decimal128`.

| Model Name | Key Fields & Types | Relationships & External Refs | Invariants & Lifecycle |
| :--- | :--- | :--- | :--- |
| **`HspDiningZone`** | `code` (String), `name` (String), `zoneType` (`MAIN_DINING`, `BAR_LOUNGE`, `PATIO_OUTDOOR`, `CHEFS_COUNTER`, `PRIVATE_DINING`), `isWeatherContingent` (Boolean), `availabilityState` (`OPEN`, `WEATHER_PAUSED`, `HOUSE_HOLD_ONLY`, `CLOSED`) | `outletId` -> `HspRestaurantOutlet.id` (`#170`) | Setting `WEATHER_PAUSED` halts new online patio bookings and flags existing bookings for indoor relocation. |
| **`HspDiningFloorTable`** | `tableNumber` (String), `minCovers` (Int), `maxCovers` (Int), `shape` (`ROUND`, `SQUARE`, `BOOTH`, `COUNTER_SEAT`), `attributes` (String[]: `WINDOW`, `QUIET`, `ADA_ACCESSIBLE`, `HIGH_TOP`), `combinableWithTableIds` (UUID[]), `comboPriorityRank` (Int), `liveStatus` (`AVAILABLE`, `RESERVED_SOON`, `SEATED_DINING`, `MAINS_ON_TABLE`, `CHECK_DROPPED`, `BUSING_DIRTY`, `BLOCKED`) | `outletId` -> `HspRestaurantOutlet.id`, `zoneId` -> `HspDiningZone.id`, `assignedServerId` -> `HrEmployee.id` (current shift) | `maxCovers >= minCovers >= 1`; cannot seat two active parties on the same `HspDiningFloorTable` simultaneously. |
| **`HspDiningShift`** | `name` (String: `LUNCH`, `BRUNCH`, `DINNER`), `daysOfWeek` (Int[]), `startTime` (String), `lastSeatingTime` (String), `maxCoversPer15Min` (Int), `turnMinutesByPartySize` (JSON map: `{"1-2": 75, "3-4": 90, "5-6": 105, "7+": 120}`), `policyType` (`STANDARD_FREE`, `CARD_HOLD_NO_SHOW`, `UPFRONT_DEPOSIT`), `feePerCover` (`Decimal128`), `cancelCutoffHours` (Int) | `outletId` -> `HspRestaurantOutlet.id` | Online booking requests exceeding `maxCoversPer15Min` in a slot are rejected even if physical tables exist (protecting `#170` kitchen pacing). |
| **`HspDiningExperience`** | `code` (String), `title` (String), `pricingMode` (`PER_PERSON_TICKET`, `TABLE_MINIMUM_SPEND`, `DEPOSIT_CREDIT`), `pricePerUnit` (`Decimal128`), `taxRatePct` (`Decimal128`), `includedAddOns` (String[]), `isTransferable` (Boolean), `status` (`PUBLISHED`, `SOLD_OUT`, `ARCHIVED`) | `outletId` -> `HspRestaurantOutlet.id`, `allowedZoneIds` -> `HspDiningZone.id[]` | Prepaid `PER_PERSON_TICKET` bookings require `FinPaymentIntent` capture prior to status `CONFIRMED`. |
| **`HspDinerProfile`** | `autoTags` (String[]: `VIP`, `REGULAR_10X`, `HIGH_SPENDER`, `WINE_COLLECTOR`, `SERVICE_RECOVERY_DUE`, `CHRONIC_NO_SHOW`), `severeAllergies` (String[]), `dietaryPreferences` (String[]), `seatingPreferences` (String[]), `totalVisits` (Int), `noShowCount` (Int), `lifetimeSpend` (`Decimal128`), `avgSpendPerCover` (`Decimal128`), `specialDates` (JSON: birthday/anniversary) | `contactId` -> `CrmContact.id` (1:1), `hotelGuestProfileId` -> `HspGuestProfile.id` (`#169`, optional) | `avgSpendPerCover` recalculates deterministically from settled `#170` `HspDiningCheck` events; allergy edits propagate to all upcoming `HspDiningReservation`s. |
| **`HspDiningReservation`** | `reservationCode` (String, unique), `sourceChannel` (`DIRECT_WEB`, `HOST_PHONE`, `WALK_IN_SEATED`, `HOTEL_CONCIERGE`, `NOTIFY_BACKFILL`), `reservationDate` (Date), `slotStartAt` (DateTime), `expectedClearAt` (DateTime), `partySize` (Int), `guestPhone` (String E.164), `occasionTag` (`NONE`, `BIRTHDAY`, `ANNIVERSARY`, `BUSINESS_DINNER`, `VIP_HOSTED`), `dietaryNotes` (String), `depositCapturedAmount` (`Decimal128`), `noShowFeeAmount` (`Decimal128`), `status` (`PENDING_PAYMENT`, `BOOKED`, `CONFIRMED_BY_GUEST`, `ARRIVED_AT_HOST`, `SEATED`, `COMPLETED`, `NO_SHOW_CHARGED`, `NO_SHOW_WAIVED`, `CANCELLED`) | `outletId` -> `HspRestaurantOutlet.id`, `shiftId` -> `HspDiningShift.id`, `dinerProfileId` -> `HspDinerProfile.id`, `experienceId` -> `HspDiningExperience.id` (optional), `assignedTableIds` -> `HspDiningFloorTable.id[]`, `activeDiningCheckId` -> `HspDiningCheck.id` (`#170`), `paymentIntentId` -> `FinPaymentIntent.id` | No two overlapping `BOOKED`/`CONFIRMED_BY_GUEST`/`SEATED` reservations may lock the same `assignedTableIds`; transitioning to `NO_SHOW_WAIVED` above host cap requires approved Home `WorkItem`. |
| **`HspWaitlistEntry`** | `entryType` (`WALK_IN_LIVE`, `REMOTE_JOIN`, `PRIORITY_NOTIFY_SLOT`), `partySize` (Int), `guestName` (String), `guestPhone` (String E.164), `preferredZoneType` (String), `quotedWaitMinutes` (Int), `joinedAt` (DateTime), `pagedAt` (DateTime), `holdExpiresAt` (DateTime), `status` (`WAITING`, `PAGED_HOLDING`, `GUEST_CONFIRMED_ON_WAY`, `SEATED_CONVERTED`, `EXPIRED_DROPPED`, `CANCELLED`) | `outletId` -> `HspRestaurantOutlet.id`, `dinerProfileId` -> `HspDinerProfile.id` (optional), `convertedReservationId` -> `HspDiningReservation.id` (optional) | Paging sets `holdExpiresAt = pagedAt + graceMinutes`; converting to `SEATED_CONVERTED` atomically seats the target table and opens `#170` `HspDiningCheck`. |

---

## 5. Core End-to-End User Journeys

### Journey 1: SME Fast-Path — Walk-In Waitlist -> SMS Page -> Host Seating -> `#170` Check Open
1. A walk-in party of 4 arrives at `19:15`; the Host opens `waitlist-drawer`, enters `4 covers`, `PATIO_OUTDOOR` or `FIRST_AVAILABLE`, and `+13125550148` (`<rapider-phone-input>`), seeing an AI-grounded quote of `22 min` based on two tables currently in `CHECK_DROPPED`.
2. When Table `T08` resets from `BUSING_DIRTY` to `AVAILABLE` at `19:34`, the Host taps **Page SMS** on `#/waitlist`, dispatching a `MktSmsMessage` ("Your table for 4 is ready! Reply 1 within 10 mins to confirm").
3. The guest replies `1` (`GUEST_CONFIRMED_ON_WAY`) and steps up to the stand; the Host taps **Seat at T08** (assigned to Server Maya, who has the lowest cover rotation count), flipping `T08` to `SEATED_DINING` and emitting `hsp.table.party_seated` so `#170` automatically opens `HspDiningCheck` `#CHK-5102`.

### Journey 2: Prepaid Chef's Counter Tasting Ticket & Deposit Credit Application
1. A diner books 2 seats for Saturday's **7-Course Chef's Tasting (`\$165.00/person`)** (`HspDiningExperience`) via the `ComSite` widget, noting a `CELIAC_GLUTEN` allergy and `ANNIVERSARY` occasion, and completes a `\$330.00` + tax capture via `payments` (`FinPaymentIntent`).
2. Before service, `#/preshift-analytics` highlights the anniversary + `CELIAC_GLUTEN` requirement on the kitchen/floor pre-shift chit.
3. Upon seating at Counter Seats `C1–C2`, `#171` passes `depositCapturedAmount = \$330.00` and the `CELIAC_GLUTEN` banner to `#170` `HspDiningCheck`, so only incremental wine pairings and gratuity remain due at the end of the meal.

### Journey 3: Cancellation -> *Priority Notify* Automated Slot Backfill
1. At `16:30`, a booked 4-top for `19:45` prime dinner cancels via their 24h SMS link (`status = CANCELLED`), freeing Table `T14` (`BOOTH`).
2. Workflow `wf-hsp-priority-notify-backfill` checks `HspWaitlistEntry` (`PRIORITY_NOTIFY_SLOT` for `19:00–20:15`, `4 pax`), ranks an in-house `#169` Hotel Platinum VIP (`HspDinerProfile` tag `IN_HOUSE_HOTEL`) first, and texts a 15-minute claim link.
3. The VIP claims the `19:45` slot in 3 minutes—saving `\$400+` in prime dinner revenue with zero host phone tag.

### Journey 4: Disputed No-Show Fee Waiver Governance via Rapider Home `WorkItem`
1. A Saturday 6-top (`\$25.00/cover` = `\$150.00` card hold) fails to arrive by `20:30` after two SMS nudges; the Host marks `NO_SHOW` and requests a waiver after the guest calls claiming a flight delay.
2. Because `\$150.00` exceeds the Host's `\$50.00` waiver limit, `#171` creates a Rapider Home `WorkItem` for the General Manager containing the diner's `HspDinerProfile` (`totalVisits = 14`, `noShowCount = 0`, `lifetimeSpend = \$4,820.00`).
3. Seeing a loyal `REGULAR_10X` guest, the GM approves the waiver in Home `WorkItem`s—releasing the `FinPaymentIntent` hold, transitioning status to `NO_SHOW_WAIVED`, and rebooking them for Sunday dinner.

### Journey 5: Two-Way `#170` Course Telemetry & Click-Through Filter State Preservation
1. As `#170` fires courses and settles checks throughout service, `#/host-board` table cards transition automatically (`SEATED_DINING` -> `MAINS_ON_TABLE` -> `CHECK_DROPPED` -> `BUSING_DIRTY`), updating remaining turn-time badges in real time.
2. On `#/reservations`, the Maitre D' searches `Anniversary` and filters `Tag: "VIP"`, clicks `#RES-2026-9914` to open `#/reservation-detail?id=...` (checking the linked `#170` live check balance and wine notes), and clicks **Back to Reservation Book**—restoring `#/reservations` with both filter chips intact in `#activeFilterTagsBar`.

---

## 6. Consolidated Feature Priorities & Work Packages

### `P0` Foundation Work Packages (Mandatory MVP Launch)
- **WP-P0-1: Floor Zones, Combinable Tables & Shift Pacing (`RTM-001`, `RTM-002`, `RTM-003`):** `HspDiningZone`, `HspDiningFloorTable`, `HspDiningShift` (`#/floor-zones`, `#/shifts-pacing`), 15-minute cover pacing caps, and valid table combinations.
- **WP-P0-2: Real-Time Availability, Online Booking & Deposit Holds (`RTM-005`, `RTM-006`):** `HspDiningReservation`, `#/reservations`, `reservation-drawer`, `<rapider-phone-input>`, and `FinPaymentIntent` card holds/deposits credited to `#170`.
- **WP-P0-3: Walk-In Waitlist & Two-Way SMS Paging (`RTM-010`, `RTM-011`):** `HspWaitlistEntry`, `#/waitlist`, `waitlist-drawer`, one-tap `MktSmsMessage` table-ready paging, and grace-window expiry.
- **WP-P0-4: Host Kanban, Server Rotation & Two-Way `#170` Check Sync (`RTM-013`, `RTM-014`, `RTM-015`, `RTM-017`):** `#/host-board` (`<rapider-kanban>` + zone map), `HrEmployee` fair server cover rotation, `hsp.table.party_seated` <-> `#170` course telemetry, and `HspDinerProfile` (`#/diner-directory`).

### `P1` Scale & Enterprise Work Packages
- **WP-P1-1: Prepaid Tasting Experiences, Confirmations & Waiver Governance (`RTM-004`, `RTM-007`, `RTM-008`, `RTM-009`):** `HspDiningExperience` (`#/experiences`), VIP house holds, weather patio pause, 24h two-way SMS confirmations, and Home `WorkItem` no-show fee waivers.
- **WP-P1-2: *Priority Notify* Backfill, Hotel VIP Sync & Pre-Shift Chits (`RTM-012`, `RTM-016`, `RTM-018`, `RTM-019`):** Sold-out slot cancellation backfill, busing reset timers, `#169` in-house hotel guest badges, and `#/preshift-analytics` chits.
- **WP-P1-3: Post-Visit Recovery, PDR `CRM` Handoff & `RevPASH` Analytics (`RTM-020`, `RTM-021`, `RTM-022`):** `MktSurvey` + `SupTicket` service-recovery loop, `12+ pax` group lead promotion to `CrmOpportunity`, and `RevPASH` yield reporting.

### `P2` Adjacent & Grounded AI Work Packages
- **WP-P2-1: Grounded AI Wait-Quote Predictor & Table-Tetris Optimizer (`RTM-023`, `RTM-024`):** Live wait-minute prediction grounded in seated `#170` course stages and human-confirmed shift table reassignment maximizing prime turns.
- **WP-P2-2: No-Show Risk Scorer & Pre-Shift VIP Dossiers (`RTM-025`, `RTM-026`):** Proactive outreach flags for high-risk bookings and grounded pre-meal VIP/allergy summaries in `projectChannelMessage`.

---

## 7. Roles, Permissions & Field-Level Governance

| Role | Permitted Actions | Restricted / Field-Level Boundaries |
| :--- | :--- | :--- |
| **Host / Maitre D'** | View floor board, reservations, waitlist, and diner notes; book/modify/seat parties; page SMS waitlist; waive no-show fees up to host limit (e.g., `\$50`). | Cannot waive no-show fees above threshold without Home `WorkItem`; cannot export bulk `HspDinerProfile` contact CSVs; cannot alter `FinPaymentIntent` payout accounts. |
| **Server / Sommelier** | View `#/host-board` assigned section, `#/preshift-analytics` chit, and `HspDinerProfile` dietary allergies, wine preferences, and celebration tags. | Read-only on shift pacing caps and deposit rules; guest mobile/email masked unless needed for authorized sommelier follow-up. |
| **Floor Manager** | All Host actions + approve no-show waiver Home `WorkItem`s, release VIP house-hold tables, toggle patio `WEATHER_PAUSED`, rebalance server sections. | Cannot hard-delete historical settled reservations or alter `#170` closed `Decimal128` spend history on `HspDinerProfile`. |
| **Restaurant GM / Director** | Configure `HspDiningZone`, `HspDiningFloorTable`, `HspDiningShift` pacing caps, `HspDiningExperience` pricing, and `MktSurvey` triggers. | All deposit-policy, cancellation-fee, and bulk CRM export operations are logged to immutable platform audit trails. |

---

## 8. Technical APIs, Guarded Commands, Events & `requiredWorkflows`

### 8.1 Guarded Domain Commands
Every state-mutating command requires `{ idempotencyKey, correlationId, expectedVersion }`:
- `hsp.tables.bookDiningReservation` — Atomically verifies `HspDiningShift` 15-min cover pacing cap + valid single/combinable `HspDiningFloorTable` interval availability, initiates `FinPaymentIntent` hold/capture when required, and locks slot.
- `hsp.tables.seatPartyAtTable` — Verifies target `HspDiningFloorTable`(s) are `AVAILABLE`, updates table status to `SEATED_DINING`, increments assigned `HrEmployee` server cover rotation counter, and emits `hsp.table.party_seated` (with allergies & deposit credit) to `#170`.
- `hsp.tables.pageWaitlistGuest` — Transitions `HspWaitlistEntry` to `PAGED_HOLDING`, sets `holdExpiresAt`, and dispatches `MktSmsMessage`.
- `hsp.tables.processNoShowPolicy` — Captures `FinPaymentIntent` no-show fee or, if waiver requested above caller's limit, creates a Rapider Home `WorkItem`.
- `hsp.tables.applyAiTableRebalance` — Applies host-confirmed table reassignments across unassigned `UPCOMING` reservations using multi-record optimistic `expectedVersion` checks.

### 8.2 Published & Consumed Kafka Domain Events
- **Published:** `hsp.reservation.dining_booked`, `hsp.reservation.dining_cancelled`, `hsp.table.party_seated`, `hsp.table.status_changed`, `hsp.waitlist.guest_paged`, `hsp.diner.group_inquiry_promoted`.
- **Consumed:** `hsp.restaurant.course_fired` & `hsp.restaurant.check_settled` (from `#170`), `hsp.guest.checked_in` & `hsp.guest.checked_out` (from `#169`), `fin.payment_intent.succeeded` (from `payments`), `mkt.sms.inbound_reply` (from `sms`).

### 8.3 `requiredWorkflows` (Declared in `app.manifest.json`)
1. `wf-hsp-dining-24h-confirmation-sms` — Dispatches 24h SMS/email confirmation requests and processes guest `Confirm` / `Cancel` / `Running Late` replies (`RTM-008`).
2. `wf-hsp-priority-notify-backfill` — Matches newly cancelled prime-time slots against `PRIORITY_NOTIFY_SLOT` `HspWaitlistEntry` subscribers and sends time-boxed claim links (`RTM-012`).
3. `wf-hsp-waitlist-grace-expiry` — Monitors `PAGED_HOLDING` entries past `holdExpiresAt` and alerts the host stand before releasing held tables (`RTM-011`).
4. `wf-hsp-post-visit-survey-and-crm-enrich` — Updates `HspDinerProfile` spend/auto-tags on `hsp.restaurant.check_settled` and triggers post-visit `MktSurvey` (`RTM-017`, `RTM-020`).

### 8.4 Grounded Rapider AI Guardrails
- AI Wait-Time Predictor, Table-Tetris Optimizer, and Pre-Shift VIP Dossier cite specific `HspDiningReservation`, `HspDinerProfile`, `HspDiningFloorTable`, and `#170` `HspDiningCheck` IDs within RBAC permissions.
- AI **never** auto-cancels unconfirmed reservations, charges no-show cards, or reassigns already-`SEATED` tables without explicit human confirmation.

---

## 9. Security, Privacy, Compliance & Non-Functional Requirements

- **TCPA / GDPR SMS & Marketing Consent:** Transactional reservation confirmations and waitlist "Table Ready" pages (`MktSmsMessage`) are strictly separated from promotional marketing opt-ins on canonical `CrmContact`; `STOP` replies immediately suppress SMS delivery.
- **PCI-DSS & Allergy Health Data Protection:** Card holds/deposits exclusively use tokenized `FinPaymentIntent` references; diner allergy/health notes on `HspDinerProfile` are access-restricted to authorized hospitality staff and erasable under GDPR/CCPA subject requests.
- **High-Concurrency Peak Release Resilience:** Popular tasting-menu ticket drops (e.g., 1st-of-month `10:00` releases) enforce atomic slot/table locks with zero double-sold seats.
- **Accessibility & Host-Stand Ergonomics:** WCAG 2.2 AA compliant across `1440px` back-office screens, `768px` host-stand tablets (portrait & landscape), and `390px` manager phones in dim candlelit dining rooms (dark/light theme parity).

---

## 10. Deterministic Acceptance Criteria

1. **Sidebar Minimum-3-Items Compliance:** `app.manifest.json` defines 3 visible sidebar sections (`Host Stand`, `Guest & Experiences`, `Governance`) with 3 visible items each (`displayOnMenu: true`); detail and drawer routes set `displayOnMenu: false`.
2. **15-Minute Pacing Cap & Table Double-Booking Guard:** `bookDiningReservation` rejects a booking if adding `partySize` exceeds `HspDiningShift.maxCoversPer15Min` even when empty tables exist, and rejects concurrent bookings targeting the same table/interval (`409 Conflict`).
3. **Combinable Table Resolution:** A booking for `6 covers` when only `4-top` tables `T10` and `T11` (`combinableWithTableIds` linked) are free automatically locks `T10 + T11` for the party's turn duration.
4. **Two-Way `#170` Seating & Course Sync:** Clicking **Seat Party** on `#/host-board` emits `hsp.table.party_seated` with allergies and `Decimal128` deposit credit, and incoming `hsp.restaurant.course_fired` (`COURSE_2_MAINS`) updates table status to `MAINS_ON_TABLE`.
5. **Prepaid Ticket & Deposit Precision:** Booking a `\$165.00` prepaid tasting experience for `2` covers calculates exact `Decimal128` totals and keeps status `PENDING_PAYMENT` until `FinPaymentIntent` succeeds.
6. **Home `WorkItem` No-Show Waiver Governance:** Requesting a `\$150.00` no-show fee waiver as a Host (cap `\$50.00`) creates a Rapider Home `WorkItem` and withholds waiver completion until Manager approval.
7. **Waitlist SMS Page & Grace Timer:** Tapping **Page SMS** sets `status = PAGED_HOLDING`, populates `holdExpiresAt`, and converts cleanly to `SEATED_CONVERTED` when seated.
8. **Hotel In-House VIP Recognition:** Matching a diner's `contactId` to an active `#169` `CHECKED_IN` `HspHotelReservation` displays the `IN_HOUSE_HOTEL` room badge on `#/host-board` and `#/preshift-analytics`.
9. **Custom Elements Adoption:** Every reservation and waitlist mobile input uses `<rapider-phone-input>`, and `#/host-board` renders live party stages via `<rapider-kanban>`.
10. **SWR Clean Query & Optimistic UI Standard:** Initial reads use `findSWR` / `countSWR` without `isDeleted` API query filters, optimistically update local state + invalidate SWR cache upon drawer save/delete, and reset save buttons inside `finally`.
11. **Table Action & Click-Through Navigation Standard:** No data table displays a `View` button in `Actions`; clicking `#RES-...` or Diner Name navigates to `#/reservation-detail?id=...` or `#/diner-detail?id=...` without `<base href>` 404 hijacking, and `Back` restores filter state.
12. **Search, `#activeFilterTagsBar` & `Clear all`:** Filtering reservations, waitlist entries, or diners renders HTML-escaped chips in `#activeFilterTagsBar` with `✕` dismissal and `Clear all` reset.
13. **Theme & Button Contrast Compliance:** All 13 routes pass `validate_theme` in dark and light modes with `#ffffff !important` contrast on primary/danger buttons and zero native `window.alert`/`confirm`/`prompt`.
