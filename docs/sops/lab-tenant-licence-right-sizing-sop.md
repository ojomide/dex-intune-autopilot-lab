# SOP — Lab Tenant Licence Right-Sizing (Microsoft 365)

**Purpose:** Keep a lab tenant on the cheapest licence that fully covers the workloads the lab actually runs — no more, no less — and prove it with a change record.
**Applies to:** Any Microsoft 365 lab/training tenant (here: Digitech Explorer Canada).
**First executed:** Nov 28, 2026 — Business Premium → EMS E3, CA$40.41/mo → CA$22.10/mo (change record CHG-2026-11-28-001).

## Decision test (run before any change)

1. List the workloads on the lab's critical path for the next 60 days (e.g. Intune configuration/compliance/BitLocker/Autopilot, Entra ID, Conditional Access).
2. Map each workload to the cheapest licence that includes it:
   - Intune + Entra ID P1 only → **EMS E3** (or Intune Plan 1 + Entra ID P1 à la carte).
   - Exchange / SharePoint / Teams / OneDrive / Office apps needed (e.g. MS-102 block) → **Business Premium** (or the relevant M365 plan).
3. Check exam sequencing: an Expert exam (e.g. MS-102) cannot be banked before its Associate prerequisite (e.g. MD-102) — never hold a premium licence for an exam the sequence hasn't reached.
4. If the cheaper licence covers the whole list, step down. If one workload needs the premium licence, rent it for that month only.

## Guardrails

- **Monthly term, pay monthly, always.** Annual terms are cheaper per month and wrong for a lab — they defeat the nix-at-trigger rule.
- Verify the live price in the admin centre Marketplace before deciding; never quote a remembered price. Read the tax-included total on the checkout review screen before "Place order".
- Confirm the tenant name in the header before touching billing. A change in the wrong directory is the classic lab accident.
- Know which user holds the licence (it may be a lab/test user, not the admin) — the replacement licence goes to the same user.
- Check the billing profile's payment method state before ordering (a frozen card will fail the charge at invoicing).
- Never touch disabled/trial subscription rows while working on the active one.

## Procedure

### 1. Read the current state (change nothing)
1. Left nav: Billing
2. Left nav: Your products
3. In-page: note every row — product, licences assigned, status, renewal date
4. In-page: open the active subscription's detail panel — record status, renewal wording, next billing date, recurring-billing state
5. Left nav: Users → Active users
6. In-page: open the licence-holding user → Licenses and apps tab — record exactly what is assigned

### 2. Price the target licence
1. Left nav: Marketplace
2. In-page: All Products tab → search the product name (search the short form, e.g. "Enterprise Mobility", if the full name returns no results)
3. In-page: View details on the product card
4. In-page: record the plans table — monthly term price first; note the annual price but do not take it

### 3. Purchase (stop at the review screen first)
1. In-page (offer details): Subscription length radio "1 month"
2. In-page: Billing frequency radio "Pay monthly"
3. In-page: quantity 1 → Buy
4. In-page (checkout Review): verify product, quantity, subtotal, estimated taxes, total against the figures you recorded — if anything differs, stop and re-decide
5. In-page: Place order (only on the change owner's explicit go)
6. Record the confirmation text shown

### 4. Move the licence
1. Left nav: Users → Active users
2. In-page: open the licence-holding user → Licenses and apps tab
3. In-page: tick the new licence, untick the old licence
4. In-page: Save changes — record the confirmation banner

### 5. Stop the old subscription renewing
1. Left nav: Billing → Your products
2. In-page: select the old subscription's row → Edit recurring billing
3. In-page (dialog): select "Cancel on expiration" (not immediate cancellation — services run to term end)
4. In-page: work through the cancellation dialogs; if a reason is required, pick the honest closest fit (e.g. "Need fewer features")
5. In-page: Confirm cancellation — record the confirmation heading and the effective expiry date **as stated on the cancellation screens** (it can differ by a day from the renewal wording elsewhere; the cancellation screens govern)

### 6. Verify (read back, never assume)
1. Billing → Your products: new subscription Active with the licence assigned and a future renewal date; old subscription showing "Expiring soon" / cancellation wording with 0 licences assigned
2. User → Licenses and apps: only the new licence ticked
3. Note any unverified remainder (e.g. first-invoice settlement) as an open item in the change record

## Rollback

- Before the old subscription's expiry: Your products → old subscription → "Edit renewal" reactivates it.
- After expiry: re-purchase monthly and reassign. Intune/Entra configuration survives a licence swap as long as an Intune-bearing licence remains assigned to the lab user.

## Evidence to capture (every run)

- Timestamped step log: time, page, action, exact confirmation/status text
- Pre- and post-change subscription rows and licence assignments
- Live price read (pre-tax, tax, total) from the Marketplace and the checkout review
- Any date or wording discrepancies between screens, resolved in favour of the screen that governs the action
- The change record filed with the lab's documentation (and committed to the lab repo, sanitized of payment details)
