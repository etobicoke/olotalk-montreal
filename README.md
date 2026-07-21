# Olotalk × City of Montréal — AI Challenge submission

The submission mini-site for the **ALL IN 2026 AI Challenge — Reinventing the Citizen
Experience** (City of Montréal). Everything here is computed from the City's own open
data and is independently reproducible.

**▶ Start at the hub — [index.html](index.html)** (the Pages landing page).

- **Live demo** (interactive, EN + FR): [demo.html](demo.html) · [demo.fr.html](demo.fr.html)
- **Technical proposal**: [proposal.html](proposal.html)
- **Field notes & dead ends**: [findings.html](findings.html)
- **Canonical figures + find-and-replace**: [SUBMISSION_NUMBERS.html](SUBMISSION_NUMBERS.html)
- **Submission runbook**: [RUNBOOK.html](RUNBOOK.html)

The **live routing scorecard** and the **reproduce scripts** (`shadow-run.mjs`,
`montreal-challenge-verify.mjs`) live in the companion shadow-run repo — its public
commit history is the tamper-evident ledger.

The claim in one line: routing a citizen report is ~97% reproducible with a
deterministic, citable resolver — so the AI does perception, and routing stays
auditable and never hallucinates a department.

---

Data: Requêtes 311 and the voirie / géobase / RAAV / RTSS datasets
(`donnees.montreal.ca`, CC-BY 4.0 · © Ville de Montréal). Code: MIT (see `LICENSE`).
To publish or update this site, see [PUBLISH.md](PUBLISH.md).
