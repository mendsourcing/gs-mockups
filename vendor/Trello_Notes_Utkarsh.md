# Trello Cards — Vendor System v1 (for Utkarsh)

Interactive mockups (everything below is clickable in these):
- Vendors page: https://mendsourcing.github.io/gs-mockups/vendor/Vendor_Page.html
- RFQ page: https://mendsourcing.github.io/gs-mockups/vendor/RFQ_Page.html
- Settings: https://mendsourcing.github.io/gs-mockups/vendor/Settings_Page.html
- Award page: https://mendsourcing.github.io/gs-mockups/vendor/Award_Page.html

Each section below = one Trello card. Title on first line, description underneath (Trello descriptions accept this markdown as-is).

---

## CARD 1 — Sidebar: new VENDORS section

**What:** New sidebar section "VENDORS" placed between MAIN and INTELLIGENCE.
- Items: "My Vendors" (with NEW badge at launch), "+ Add Vendor" (opens Add Vendor modal directly)
- Mockup: Vendor_Page.html (left rail)

**Done when:** section appears for all member tiers, active state matches existing sidebar styling (blue left border + accent background).

---

## CARD 2 — My Vendors: main page + stat strip

**What:** Vendors landing page with three tabs (My Vendors / GovScraper Member Directory / Vendor Pool) and a stat strip.

Stats (30-day window) — numbers MUST reconcile: RFQs Sent = Quotes Received + Awaiting Response + No Bid/Declined.
- Total Vendors
- RFQs Sent → click opens RFQ Activity view, filter "All Sent"
- Quotes Received → same view, "Quoted" filter
- Awaiting Response → same view, "Awaiting" filter
- No Bid / Declined → same view, "No Bid" filter

**RFQ Activity view:** filter pills with counts, columns: Date Sent, Vendor, Solicitation # (links to RFQ), NSN, Item, Qty, Status, Their Quote, Lead Time. Awaiting rows show "Awaiting · Nd" + Nudge button (see Card 9).

**Done when:** all four stats click through to the filtered list and the math always adds up.

---

## CARD 3 — My Vendors: vendor list table

**Columns:** Vendor (name + "CAGE XXXXX · Type" subtitle), Primary Contact, Email, Phone, Location, RFQs Sent, Quotes Back, FSCs Provided (chips). No "last activity", no lead-time column.

**Toolbar:** text search (name/email/CAGE/part), FSC filter = bubble input (type → suggest → Enter = bubble, multiple allowed), Type filter (MFG / Distributor / Packaging House), sort.

**Vendor types everywhere:** MFG, Distributor, Packaging House — these three only.

**Done when:** row click opens vendor detail; FSC bubbles filter the list.

---

## CARD 4 — Vendor detail page

**Header card:** avatar, name, "Type · CAGE", primary contact, email, phone, address, payment terms, notes. "Edit Vendor" button only (NO Send RFQ button here).

**Stat strip:** RFQs Sent, Quotes Received, Response Rate, Avg Response Time, Avg Lead Time, Awards Won.

**Three sections, in order:**
1. **Request For Quotes Sent** — logged automatically when member sends from an RFQ page. Columns: date, solicitation # (links to RFQ page), NSN, item, qty, status (Quoted/Awaiting·Nd/No Response), their quote. Awaiting rows get Nudge button.
2. **Awards** — created when an RFQ sourced from this vendor moves to Award Won. Columns: award date, **AWARD #** (links to Award page — not solicitation #), NSN, item, qty, vendor cost, award price, margin (% + $), status (PO Sent/Delivered).
3. **Parts & Pricing History** — every price this vendor returned: part #, NSN, item, unit price, qty break, lead time, date quoted, valid until (expired shown red).

**New/pool-added vendors:** header shows only pool data; stats zeroed; all three tables show empty states ("No RFQs sent to this vendor yet — send one from any RFQ page and it logs here automatically." etc.). Mockup: add Sikorsky from Vendor Pool, then open it.

---

## CARD 5 — Add / Edit Vendor modal

**Fields:** Company Name* (powers RFQ autocomplete), Primary Contact*, Title, Email* (auto-fills on RFQ sends), Phone, CAGE (optional, links to CAGE page), Vendor Type (MFG/Distributor/Packaging House), **FSCs They Provide** (bubble input: type FSC or name → dropdown with FSC descriptions → Enter/click = bubble, × removes, Backspace removes last), City, State, Payment Terms, Website, Notes.

**Dedupe:** typing a company name or CAGE that already exists in My Vendors or Vendor Pool shows amber warning with "Open existing profile" / "merge" links. Block silent duplicates.

**Edit mode:** Edit Vendor on the detail page opens the same modal pre-filled; Save Changes updates the detail page AND the list row live.

---

## CARD 6 — Member Directory tab (opt-in)

**Opt-in banner:** only members who enabled "Show me in the Member Directory" in Settings appear. Link → Settings.

**Member card contents:** avatar, company name, city/state, **CAGE badge** (top-right), **blurb** (member-written, HARD CAP 100 characters, italic quote box), email, phone, set-aside pills (SB/SDVOSB/HUBZone/WOSB/8(a)), **ALL FSC chips — no "+N" truncation**.

**Toolbar:** search, set-aside filter, FSC filter.

---

## CARD 7 — Settings: Member Directory card

New card on Settings & Account (reachable via top-right avatar icon):
- Toggle: "Show me in the Member Directory" — off hides everything below and removes member from directory.
- "What gets shared" chips: company, city/state, email & phone, CAGE, set-asides, FSCs, blurb.
- Blurb textarea: maxlength=100, live counter (amber ≥86, red at 100).
- **Live preview** of their directory card updating as they type.
- Save button.

Mockup: Settings_Page.html.

---

## CARD 8 — Vendor Pool tab

Shared, agent-built directory of manufacturers/distributors (seeded from approved-source lists + award-history CAGEs already in our data; enriched via SAM.gov + web discovery; emails verified).

**Columns:** Company (name + role subtitle), CAGE, Location, FSCs (chips), Found Via ("Approved source · 41 RFQs" / "Won 6 awards" / "Web discovery"), Contact (email + ✓ when verified; "Agent searching…" when pending), **Profile** (Verified / Unverified / GovScraper Member), "+ My Vendors" button.

**Filters:** search, FSC, Profile (Verified/Unverified/GovScraper Member/In My Vendors). No "Found Via" filter. No agent banner.

**Add flow:** "+ My Vendors" → confirm dialog (company card, CAGE, contact, FSC chips) with two notes: (1) once added they appear in My Vendors + RFQ autocomplete and are editable; (2) **"Your copy is yours alone"** — edits never write back to the pool, pool updates never overwrite member edits. Okay → row inserted at top of My Vendors tagged "from Vendor Pool", button flips to "✓ In My Vendors", counts increment.

**Data model rule:** pool record = shared + agent-maintained; My Vendors record = member's private fork created at add time. One-way copy.

---

## CARD 9 — RFQ page: Vendor Reference Table (rebuild)

Replaces current VRT. Columns: Vendor, Type, Email, Part Number, Qty & Unit, **Status**, Date Sent, Price/Unit, Lead Time, **Last Update** (not "valid until"), actions (🔔 nudge + ➤ send). No FILE column. Footer: "+ Add Row" only, plus "Best quote so far: $X / EA · Vendor → sets your suggested bid".

**Status values:** Not Sent / Sent / Quoted / No Quote / Declined — color-coded pill dropdown. These statuses roll up to the Vendors page stats and the vendor's detail tables.

**Autocomplete:** Vendor field suggests from My Vendors + Vendor Pool in a styled dropdown (white card, bold name, email+type subtitle, hover highlight — match the house status-dropdown style, NOT native datalist). Picking one auto-fills Email + Type.

**Approved Source List:** keep exactly as current production (Name, CAGE ⓘ, Part #, City, State, Reference Role, RNCC, RNVC) + ONE new column: "+ Add to table" → inserts that source as a VRT row with email from pool when known.

**Send (➤):** opens Compose Email (Card 10). On send: status → Sent, Date Sent + Last Update stamped.

---

## CARD 10 — Compose Email modal (send + nudge)

**Triggered by ➤ (first send):** "Compose Email" modal — From (member's integrated email), To (auto-filled from row), Subject "RFQ - Part {part} *{rfq_id}", Template 1 body with part number + quantity merged in, member's signature, rich-text toolbar, "Attach the RFQ PDF" checkbox, Cancel/Send. Template picker shows Template 1 (only one for v1).

**Triggered by 🔔 (nudge, row already Sent):** same modal, "Follow-Up Template": Subject "Re: {original subject}", body references original send date + part + qty, re-lists quote requirements (lead time, stock, certs, country of origin, cert charge), quotes the original email at the bottom. On send: nudge button → "✓ Reminder sent" (complete state), status stays Sent.

Nudge buttons appear wherever an Awaiting row shows: RFQ page rows, vendor detail RFQs-sent table, RFQ Activity view.

---

## CARD 11 — RFQ stage auto-sync

RFQ status stages auto-set from the Vendor Reference Table (green AUTO badge on the active stage + hint line):
- any row Quoted → **Ready to Bid**
- else any row Sent → **Currently Sourcing**
- else all active rows No Quote/Declined → **Will Source** (hint: "all vendors declined — source more vendors")
- no activity → New Opportunity

Member clicking a stage manually disables auto-sync for that RFQ (hint says so).

---

## CARD 12 — Award page ↔ vendor integration

- Vendor detail Awards table links by **award number** to the Awarded Contract page.
- Award page "Vendor Used" field links back to that vendor in My Vendors.
- Award page Pricing & Cost Analysis: **Vendor Cost auto-fills from the vendor's quote** on the linked RFQ (show source note: "from {vendor}'s quote on {RFQ} ({date})"). Profit/margin computed from it — must match the margin shown on the vendor detail Awards row.
- Vendor quote PDF uploaded on the award is also visible from the vendor's record.

---

## CARD 13 — Sourcing agent (backend, can ship after UI)

Pipeline per company: seed CAGEs from approved-source lists + procurement-history winners (grouped by FSC) → SAM.gov Entity API for legal name/address/NAICS/set-asides (free) → web enrichment for website + quotes email + phone → email verification (ZeroBounce-class) → mark Verified.
- "GovScraper Member" = claimed on Supplier Portal (profile self-maintained).
- Budget: ~$0.10–0.30 per enriched profile all-in. Pilot = 10 MFGs per FSC on our 17 target FSCs before scaling.
- Growth hook (later): when a member adds a pool company, invite that company to claim its free profile.
