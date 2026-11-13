# ADR-0003 — Verify post-reset state on the device, not the portal
Date: 2026-10-31 · Status: Accepted

## Context
The Autopilot Reset confirmation dialog warns that portal sync and compliance state can lag **up to 8 hours** after a reset. In the current Intune admin centre, Autopilot Reset also lives in a non-obvious place: **Remove data ▾** (Retire / Wipe / Fresh start / Autopilot reset) — not under Remote actions ▾, and the classic top-bar button is gone.

## Decision
Post-reset verdicts (device name, join state, provisioning completion) are read **on the device itself** (Settings > About, ESP completion, sign-in identity). Portal rows are corroboration, never the primary verdict, within the lag window. All runbooks in this repo use the current portal path (Remove data ▾) verbatim.

## Alternatives rejected
- Trusting the portal immediately after a reset — the portal's own warning refutes it; this exact lag pattern explained the Oct 7 naming "miss" (DESKTOP-* instead of LAB-*) as assignment-propagation timing, confirmed when the same profile/VM/user produced LAB-25403924589 on the Oct 31 rerun

## Consequences
Proof standard for this lab: a device-side reading with a photo/handle outranks any dashboard screenshot. Applied to the D2 proof: **LAB-25403924589**, photo-verified Oct 31, 2026.
