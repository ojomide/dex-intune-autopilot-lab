# Change Record — CHG-2026-11-28-001

**Title:** Lab tenant licence right-sizing — Microsoft 365 Business Premium → Enterprise Mobility + Security E3
**Date:** Saturday, November 28, 2026 (America/Toronto)
**Tenant:** Digitech Explorer Canada (Microsoft 365 lab tenant)
**Change owner / approver:** Olumide Ojo
**Executed by:** Muse (Strider), under the owner's per-step approval
**Status:** COMPLETE — verified on screen at 06:13 EST, Nov 28, 2026

## Reason for change (FinOps)

The tenant exists to run an Intune / Entra ID lab (MD-102 track). Every workload on the lab's critical path — device configuration, compliance, BitLocker, update rings, Autopilot, Conditional Access — runs on Intune + Entra ID P1, both of which are included in EMS E3. The Business Premium workloads (Exchange Online, SharePoint, OneDrive, Teams, Office apps) are not in the December lab plan; MS-102, the exam that needs them, is sequenced after MD-102 and cannot be banked before that prerequisite is met. Paying for Premium through December would rent services the lab does not touch.

- Before: Business Premium, CA$35.76/mo + 13% HST = **CA$40.41/mo**
- After: EMS E3, CA$19.56/mo + 13% HST = **CA$22.10/mo** (price read live in the admin centre Marketplace, Nov 28, 2026)
- **Saving: CA$18.31/mo (~CA$219.72/yr)**, with zero loss of lab capability
- Term discipline: monthly term, pay monthly — the change is reversible in either direction at the next monthly boundary (nix-at-trigger rule). Premium can be re-rented for exactly one month when the MS-102 block starts.

## Pre-change state (verified 05:39–05:44 EST, read-only staging run)

- Business Premium: Active, 1 of 1 licences, assigned to the lab user "Intune Test"; list price CA$35.76 user/month; recurring billing On; subscription list renewal date 11/29/2026, detail panel "Renews on November 30, 2026", next billing date November 30, 2026.
- A second Business Premium row (25-licence trial) sat Disabled, 0 of 25 — not touched by this change.
- EMS E3 offer (Marketplace): 1-month term CA$19.56 licence/month; annual CA$17.12 licence/month (declined — annual term conflicts with monthly flexibility).
- Checkout review screen (staged, NOT committed in this run): Subtotal CA$19.56, Estimated taxes CA$2.54, Total CA$22.10; commit button labelled "Place order".

## Execution timeline (all times EST, Nov 28, 2026)

| Time | Run | What happened |
|---|---|---|
| 05:39–05:44 | Staging | Price and state verified; purchase walked to the review screen and stopped before "Place order". No changes made. Owner then held the change ("Hold for now", 05:47). |
| 05:54–05:57 | Execution (interrupted) | Owner approved implementation at 05:53. During this run the EMS E3 order was placed and the licence reassignment completed ("Your changes have been saved" banner seen for Intune Test). The Business Premium cancellation flow was opened and "Cancel on expiration" selected but NOT confirmed. Owner stopped the run at 05:57 ("Hold") to confirm the documentation approach before proceeding. |
| 06:10–06:14 | Completion + verification | Read-only state check established: EMS E3 subscription already existed (Active, 1 of 1 assigned, renewal 12/27/2026) and Intune Test already held EMS E3 only. The one incomplete item — Premium recurring billing still set to Renew — was completed: Edit recurring billing → "Cancel on expiration" → cancellation reason recorded as "Need fewer features" → Confirm cancellation. Confirmation heading: "Microsoft 365 Business Premium subscription cancellation scheduled". |

## Post-change verification (06:13 EST, read back from Billing → Your products and the user licence tab)

- **Enterprise Mobility + Security E3** — NEW, 1 of 1 licences assigned, **Active**, renewal **12/27/2026**
- **Microsoft 365 Business Premium** (1-seat) — 0 of 1 assigned, status changed Active → **"Expiring soon"**; detail panel: "This subscription will be canceled when it expires on November 29, 2026"; "Microsoft 365 Business Premium expires on 11/29/2026"
- **Intune Test → Licenses and apps** — Licenses (1): Enterprise Mobility + Security E3 [checked]; Microsoft 365 Business Premium [unchecked, 1 of 1 available]; location Canada
- Disabled 25-licence Premium row and Microsoft Entra ID Free: unchanged

## Discrepancies and notes

- **Expiry date:** the subscription detail panel and the Renew dialog said November 30, 2026; every cancellation screen (review, confirmation, post-change detail) states **November 29, 2026** as the effective cancellation/expiry date. November 29 governs.
- **Order evidence:** no order-confirmation screen was captured for the EMS E3 purchase (it completed inside the interrupted run). The subscription's Active state, licence assignment, and 12/27/2026 renewal date are the operative proof. The first invoice / charge settlement (CA$22.10 against the billing profile's saved payment method) was not directly observed — verify under Billing → Bills & payments or the invoice email.
- Per the cancellation review screen: access continues until November 29, 2026, and data is retained for 90 days after that date before deletion.
- Cancellation reason recorded with Microsoft: "Need fewer features".

## Rollback

- Before Nov 29, 2026: Billing → Your products → Business Premium → "Edit renewal" reactivates renewal.
- After expiry: re-purchase Business Premium monthly (CA$35.76 + tax) from the Marketplace and reassign to Intune Test. All Intune configuration, policies and device state persist independently of which licence the lab user holds, provided an Intune-bearing licence (EMS E3 or better) remains assigned.
