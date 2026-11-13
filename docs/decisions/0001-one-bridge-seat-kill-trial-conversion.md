# ADR-0001 — Buy 1 bridge seat, kill the 25-seat trial conversion
Date: 2026-10-31 · Status: Accepted

## Context
The 25-seat M365 Business Premium trial was scheduled to convert. A yearly conversion for the lab identity would have cost ~$404 CAD with tax (1 licence at $357.60/yr) — and a multi-seat conversion was the larger risk the guardrail existed to prevent. The lab still needed a *paid, real* tenant through November: trials behave differently from paid tenants, and the MD-102 lab depends on it.

## Decision
Set the trial to cancel on expiration (kill verified applied on screen, Oct 31), and buy exactly **1 monthly Business Premium seat: $35.76 + $4.65 HST = $40.41 CAD, Oct 31 – Nov 29, 2026**, assigned to `intunetest@` as sole holder. The admin account stays unlicensed by design — Intune licences the enrolled/targeted user, not the portal operator. Neo card unfrozen only until the $40.41 posts, then refrozen.

## Alternatives rejected
- Let the trial convert — uncontrolled recurring cost, the exact failure the nix-at-trigger rule exists to prevent
- Cancel everything on Oct 31 — loses the lab mid-program, weeks before placement

## Consequences
Lab survives on a known, capped cost. **Nov 29, 2026 is now a decision gate:** renew the bridge, or step down to EMS E3 (~$22.10/mo — the MD-102 lab survives on it; MS-102 workloads are the counterweight). Revisit then, not before.
