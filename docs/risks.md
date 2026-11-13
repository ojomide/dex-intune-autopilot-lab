# Risks — dex-intune-autopilot-lab
| Risk | Impact if it lands | Mitigation in place | Owner | Status |
|---|---|---|---|---|
| Bridge seat renews past Nov 29 by default | Uncapped recurring cost; repeats the pre-lab billing pattern | ADR-0004 dates the decision; weekly status carries it as the Cost line | Olumide | Open — closes at the Nov 29 gate |
| Portal state misread after a reset/wipe | Wrong verdict, wrong next step | ADR-0003: device-side reading is the primary verdict within the 8-hour lag window | Olumide | Mitigated |
| Placement (from Nov 9) starves the lab | Skills decay before the January timed rebuild | Phase B 30–45 min daily rotation, agenda-ranked, not ad hoc | Olumide | Open |
| Knowledge stays portal-only (clicks, no export) | Tenant cannot be rebuilt; interview claims unverifiable | This repo: runbooks + ADRs + status; policy-export habit is the tracked upgrade (Issue #2) | Olumide | Open |
| Lab claims outgrow Business Premium scope | Interview overclaim (Intune Suite, hybrid, Windows 365) | Situating analysis labels them theory-only; never presented as hands-on | Olumide | Mitigated |
