# ADR-0002 — Do not provision Security Copilot in this lab
Date: 2026-11-02 · Status: Accepted

## Context
The Intune Agents page was reviewed on a live screenshot (Nov 2, 2026). Access is denied behind three closed gates: (1) no Security Copilot capacity units — standalone provisioning runs ~$4 USD per provisioned SCU/hr, ≈ $2,920/mo always-on, Azure-billed; the E5/E7 allowance (400 SCU/mo per 1,000 licences) is meaningless at 1 seat, and Business Premium includes neither path; (2) no Defender Vulnerability Management; (3) Copilot roles are separate across Intune, Defender, and Security Copilot portals.

## Decision
Do not provision Security Copilot in this lab (nix-at-trigger). The four agents (Policy Configuration, Change Review, Device Offboarding, Vulnerability Remediation) are covered as **evaluation and governance knowledge** for interviews — never claimed as hands-on experience.

## Alternatives rejected
- Provision 1 SCU for "hands-on optics" — ~$2,920/mo to decorate a 1-seat lab; fails the free-first and one-tool-per-job tests

## Consequences
Interview framing stays honest and is arguably stronger: an architecture/governance evaluation with priced gates beats an unexamined "I clicked it once." Revisit only if an employer's tenant already carries the capacity.
