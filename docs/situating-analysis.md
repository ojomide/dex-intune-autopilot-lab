# Worked Example 2 — M365 / Intune Zero-Touch Lab, situated like Harbor Bank
## Your job-interview flagship — for M365 / Modern Workplace roles (MD-102 / MS-102 lane)

**Repo name (proposed):** `dex-intune-autopilot-lab`
**This file is the repo's `docs/situating-analysis.md`. Every status below is tied to a verification handle you already have — keep it that way.**

---

## Part 1 — Canvas

| Line | Intune / Autopilot Lab |
|---|---|
| **Client / user** | A simulated employer: Digitech Explorer Canada tenant, test identity `intunetest@` — standing in for "the next company that hires me to run M365" |
| **Problem** | New-hire device setup done by hand is slow, inconsistent, and unauditable. The modern answer is zero-touch: user powers on, device provisions itself, compliant and named correctly |
| **The old way** | You lived this: imaging bench, MECM/SCCM task sequences, GPOs, manual domain join at BAGCO/Falcon scale |
| **Outcome** | A device Autopilot-resets and re-provisions end-to-end, lands Entra-joined with the correct name — **read on the device itself**, not the (lagging) portal |
| **Constraints** | 1 paid Business Premium seat ($40.41, Oct 31–Nov 29) bought as a bridge; trial (25 seats) set to cancel on expiration, verified on screen; Nov 29 = step-down gate (EMS E3 recon mid-Nov). Cards frozen except a conscious release |
| **Non-goals** | No Security Copilot provisioning (3 gates closed, ~$2,920/mo always-on — nix-at-trigger, evaluated and rejected in writing); no claim of hands-on on Intune Suite / hybrid / co-management (theory-only, labelled) |
| **Proof plan** | Device name as verification handle + tenant screenshots + this repo's lab logs, domain-mapped to MD-102 |

## Part 2 — The 10 areas for this lab

| Area | Decision for THIS project | Tool / status |
|---|---|---|
| 1. Infrastructure | Microsoft 365 tenant "Digitech Explorer Canada" + Hyper-V/lab VM as the test device. Cloud tenant = infrastructure, no server built | **PROVED** — tenant live, 1 paid seat |
| 2. Networking | Cloud-managed endpoint: device reaches Intune/Entra over the internet, no site VPN in the design — state that; it's the point of cloud MDM vs MECM-on-LAN | **PROVED as design** |
| 3. Source control & config | Intune policies are portal config — your differentiator is documenting them as runbooks in Git (click-exact, left-nav vs in-page rows distinguished) so the tenant can be rebuilt from paper | **PARTIAL** — runbooks exist; a policy-export habit is the upgrade |
| 4. CI & Testing | No code pipeline — testing = the **5-touch bar** per skill: guided → closed-book → break-and-remediate → teach-back → timed rebuild (Day 0/2/7/21 spacing) | **PARTIAL** — Autopilot Reset passed end-to-end; D3 break-and-remediate still owed |
| 5. Packages & artifacts | Win32 app deployment is the artifact discipline here (`.intunewin` package, detection rules) | **PLANNED** — ranked #1 in the Nov 2–8 front-load, not yet proved. Say exactly that |
| 6. Containers | **SKIP** — endpoint management has no container story at this scale; containers live in the DevOps lab repos | **SKIP — reason stated** |
| 7. Security | Compliance policies + Conditional Access in report-only first, RBAC, Android MAM. IAM map = Software Entry 002. Security Copilot agents: **evaluated, not provisioned** — governance answer ready | **PARTIAL** — MAM proved; CA report-only verdict still owed |
| 8. Releases | Autopilot deployment profile + ESP + naming template is the "release system" for devices. **Autopilot Reset lives under Remove data ▾** (Retire / Wipe / Fresh start / Autopilot reset) in the current portal — a runbook detail most candidates get wrong | **PROVED** — reset completed Oct 31 |
| 9. Monitoring | Intune reporting + compliance state; portal can lag up to 8 hours after a reset (portal warning, on record) — monitoring rule: **device-side reading outranks portal chrome** | **PARTIAL** — reporting is a named gap in the full-coverage agenda |
| 10. Reliability & Cost | Cost is the story: killed a scheduled yearly conversion (1 licence ≈ $404 with tax, not a per-seat panic), bought exactly 1 bridge seat, step-down decision dated Nov 29. Free Azure sub = the VM bench | **PROVED** — trial kill verified on screen; $40.41 total documented |

**Verification handle (headline proof):** Autopilot Reset D2 completed Oct 31, 2026 — device re-provisioned, re-joined Entra, correctly named **LAB-25403924589**.

**Interview line this example earns you:**
> "I run a paid one-seat M365 tenant as a lab. I set a 25-seat trial to cancel and verified the kill on screen, bought one bridge seat for $40.41, and completed an Autopilot Reset end-to-end — the device came back Entra-joined and correctly named, which I verified on the device because the portal itself warns its compliance state can lag eight hours. My gaps are written down too: Win32 deployment and a report-only Conditional Access verdict are next, in that order."

That last sentence is why this system works in interviews: your **gap list is documented with an order and a reason**, so a gap reads as a plan, not a hole.

## Part 3 — ADRs for this repo

- **ADR-0001:** Buy 1 bridge seat, kill the 25-seat trial conversion. *Rejected:* letting the trial convert; cancelling outright and losing the lab mid-program.
- **ADR-0002:** Do not provision Security Copilot in a 1-seat lab. *Rejected:* ~$2,920/mo always-on SCU capacity for interview optics.
- **ADR-0003:** Verify post-reset state on the device, not the portal. *Reason:* portal's own 8-hour sync warning.
- **ADR-0004:** Step-down at Nov 29 to EMS E3 if the MD-102 lab survives on it (it does); MS-102 workloads are the deciding counterweight.

## Part 4 — Tracking snapshot

- **Milestone:** Nov 29 licence gate
- **Done:** tenant, trial kill verified, bridge seat, Autopilot Reset D2, Android MAM, Redmi selective wipe requested
- **Next (Nov 2–8 front-load, ranked):** Win32 → configuration profiles → D3 break-and-remediate → CA report-only verdict → EMS E3 recon
- **Blocked:** nothing — placement weeks switch this repo to 30–45 min rotation (Phase B of the full-coverage agenda)
- **Cost:** $40.41 committed; $0 next until the Nov 29 decision
