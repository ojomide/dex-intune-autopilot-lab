# dex-intune-autopilot-lab
> Zero-touch Windows device provisioning, proved end-to-end on a live, paid Microsoft 365 tenant — one seat, run like an enterprise.

## The problem
New-hire device setup done by hand is slow, inconsistent, and unauditable.
The old way — which I ran at scale — was an imaging bench, MECM/SCCM task sequences, GPOs, and a manual domain join for every machine.
The modern answer is zero-touch: the user powers on, the device provisions itself, and it lands compliant, named correctly, with no IT hands on it.

## What this proves
- **Autopilot Reset completed end-to-end** (Oct 31, 2026) — device re-provisioned, re-joined Entra ID, correctly named **LAB-25403924589**, verified **on the device itself** (Settings > About, photo-verified), because the portal warns its compliance/sync state can lag up to 8 hours
- **Licence discipline under a billing guardrail** — a 25-seat Business Premium trial set to cancel on expiration (verified on screen) instead of converting; exactly **1 bridge seat bought: $40.41 CAD, Oct 31 – Nov 29, 2026**, assigned to the test identity, admin unlicensed by design
- **Evaluation, not adoption, of Security Copilot** — assessed against its three gates and deliberately *not* provisioned (~$2,920/mo always-on at 1 seat); reasoning in `docs/decisions/0002`
- **Android MAM** — app protection on a personal device (Redmi, `intunetest@`), selective wipe requested
- **Documentation & organisation** — scope as Issues, decisions as ADRs, weekly 5-line status reporting, every claim tied to a verification handle. Start with `docs/situating-analysis.md`

## Architecture
See [`docs/architecture.md`](docs/architecture.md) and the full 10-area analysis in [`docs/situating-analysis.md`](docs/situating-analysis.md).
Labels used, no inflation: **PROVED / PARTIAL / PLANNED / SKIP** (with reason).

## Tool choices — every tool, one job
| Tool | Area | Job in THIS project | Status |
|---|---|---|---|
| Microsoft Intune | Releases / Config | Provisions and manages the device — Autopilot profile, ESP, naming template `LAB-%SERIAL%` | PROVED |
| Microsoft Entra ID | Security | Identity and join state for the device and test user | PROVED |
| M365 Business Premium (1 seat) | Infrastructure | The licence that makes the tenant a real, paid environment — held by `intunetest@` only | PROVED |
| Git + GitHub | Source & Config | Holds the runbooks, decisions and status for this lab, so the tenant can be rebuilt from paper | PARTIAL — repo built Nov 2, 2026; policy-export habit is the upgrade |
| HashiCorp Vault / Argo CD | — | Not applicable to endpoint tenant state | SKIP — reason in the situating analysis |

**Deliberately skipped:** Security Copilot provisioning (ADR-0002); Intune Suite / Windows 365 / hybrid co-management labs — not in Business Premium, covered as theory only and labelled as such.

## How work is organised here
- **Issues** = scope (one per deliverable, labelled by area) — starter set in `docs/issues-starter-set.md`
- **Board** = Backlog → Ready → In Progress → In Review → Done
- **Milestones** = `2026-11-29 licence gate` (step-down decision), `2027-01 timed rebuild`
- **Decisions** = [`docs/decisions/`](docs/decisions/) — ADRs, never edited after acceptance
- **Reporting** = [`docs/status/`](docs/status/) — weekly, 5 lines, always with a verification handle
- **Changes** = [`CHANGELOG.md`](CHANGELOG.md)

## Status — latest (2026-11-02)
Done: Autopilot Reset D2 complete — device LAB-25403924589, verified device-side
Next: Win32 app deployment → configuration profiles → D3 break-and-remediate → CA report-only verdict (ranked, Nov 2–8 front-load)
Blocked: Nothing — placement weeks (from Nov 9) switch this lab to a 30–45 min daily rotation
Cost: $40.41 committed (1 seat to Nov 29); $0 next spend until the Nov 29 step-down decision
Proof: Device name LAB-25403924589 (photo, Oct 31) · trial-cancel verified on screen (Oct 31)

## Run / reproduce it
The tenant is live and private; this repo is the rebuild record. A timed, closed-book rebuild of the tenant core is scheduled for January 2027 (Phase D of the lab agenda) — its runbook will land in `docs/lab-log/` when executed.
