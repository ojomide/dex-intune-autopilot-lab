# Lab Log — 2026-10-31 — Autopilot Reset (D2 rerun)
- **Mission:** Re-run Autopilot Reset end-to-end and settle the Oct 7 naming miss (device came back DESKTOP-* instead of the LAB-%SERIAL% template)
- **Map:** Golden-image rebuild + RIS/WDS deployment (2010s) → Autopilot Reset from the cloud console, device self-provisions through ESP
- **Work:** Remove data ▾ → Autopilot reset (current portal path — not Remote actions; see ADR-0003). ESP completed; signed in as intunetest@
- **Wall:** Same profile, same VM, same user as Oct 7 — so configuration could not explain the difference between the two runs
- **Proof:** Device name **LAB-25403924589** read on the device itself (Settings > About, photo). Verdict: the Oct 7 miss was assignment-propagation timing, not configuration — the profile had not yet propagated when the first reset ran
- **Ledger:** Propagation is a real step in cloud management: assign, wait, verify on the device — the portal will not warn you, and its state can lag up to 8 hours
