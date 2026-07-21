# Submission numbers — the canonical reference

**One source of truth for every figure that appears in the Montréal submission.**
Use these forms in the memo, the form answers, the video script, and anywhere else.
Re-verified against the live City API on **2026-07-21**.

## The rule

> **Cite rates exactly. Round every count.**

The 311 dataset is *"2022 à ce jour"* — it grows every day. Rates (accuracy, shares)
are stable to a fraction of a point; raw counts drift up. A juror who re-runs in
September will get **bigger counts and near-identical rates**. If you quote a raw
count, it will not match theirs and reads as an error. If you round it, and quote
rates exactly, everything they see confirms you. The verifier reports growing counts
as **DRIFT, not FAIL** for exactly this reason — the drift is proof the data is live.

## Use these forms

| Say this (drift-proof) | Exact value today | Notes |
|---|---|---|
| **~97%** of routing reproduced with no ML | **97.27%** held-out | Rule B (geometry + one switch/category). Safe to state exactly — it's a rate. |
| **~90%** from geography alone | **90.99%** held-out | Rule A. A rate — safe exactly. |
| **"3 million+ requests"** | 3,066,063 | Was 3,034,731 on 07-15. **Never quote the raw number** — round it. |
| **~82%** still arrive by phone | 81.98% | Rounds to 82. |
| **~1.5 million** located requests evaluated | 1,547,517 | Was 1,529,458 on 07-15. Round it. |
| **~500** live service categories | 522 in 2026 | 994 all-time incl. 279 retired. "About 500 live" is safe. |
| **~75%** of traffic-signal reports → one borough | 74.71% → Rosemont–La Petite-Patrie | The shared-service trap. Rate — safe. |
| **19 distinct units** handle one pothole category | 19 | Structural, stable. |
| Frozen-policy training set | ~960,000 requests (pre-2025) | 961,599 exactly. Round it. |

## Find & replace for the five submission docs

Search each of the five docs (tech spec, contracts, form blocks, memo, form
answers) for the left column; replace with the right. Skip anything not present.

**A. Standardize on the HELD-OUT rates everywhere.** They match the live scorecard,
so a juror who opens the scorecard URL sees the same numbers as the memo — and
held-out is the stronger claim than in-sample.

| Find | Replace with | Why |
|---|---|---|
| `97.55%` | **`97.27%`** (held-out) | 97.55 is in-sample; lead with held-out |
| `90.33%` | **`90.99%`** (held-out) | same |
| `90.95%` | **`90.99%`** | drift on held-out Rule A |
| `96.46%` | **`90.99%` / `97.27%`** | old pothole-only geometry number — replace with the whole-dataset held-out figures |
| `97.27%` | *keep* ✓ | held-out Rule B — unchanged |

**B. Round every raw count — they grow daily.**

| Find | Replace with |
|---|---|
| `3,034,731` · `3.03M` · "3.0 million" | **3 million+** |
| `1,529,458` | **~1.5 million** |
| `567,859` | **~585,000** (held-out set) |
| `2,489,180` | **~2.5 million** (phone) |
| `62,008` | **~62,000** |
| `47,578` | **~48,000** (Organisme divers) |
| `961,599` · `961,216` | **~960,000** (training set) |
| `993` · `994` | **nearly 1,000** (all-time categories) |
| `513` | **~500** (live in 2026) |
| `252` | **~275** (retired) |
| `311` (ville-liée potholes) | **~300** |
| `82.02%` | **~82%** (or 81.98%) |
| `74.70%` | **~75%** (or 74.71%) |
| `66.90%` | **~67%** (or 66.92%) |

**C. These are STABLE — keep them exact** (frozen 2020 voirie snapshot / structural):
`16,750` voirie assets · `121` / `68` / `60` autoroute→borough attributions · `7`
third-party asset rows · `19` units per pothole category · `0.69%` borough
divergence · `2020-05-30` snapshot date. They do not drift.

**D. Denominator hygiene — a check, not a swap.** Never pair the 97% with the 3M.
The 97% is of the **held-out ~585,000** (and ~1.5M evaluated in-sample). Keep the
three straight: **3M scanned · ~1.5M evaluated · ~585K held-out.**

**E. Language traps** (from `findings.md`) — search and delete:
- any "predict **before** the City decides / acts" → the open data ships each
  request already routed; say "provably not retrofitted + independently
  recomputable" instead.
- any claim that `PROPRIETAIRE_REF` **gives** the owner → it's a territory tag;
  jurisdiction is **reconciled** across sources.

**F. If any doc cites the policy hash**, it must read exactly
`b1f8107035578539f3c3a9f81e2ec1d9365ec038ed409ab8fc1bf96ea915a1f1`.

## The two headline rates — never round these

- **Routing is 97% reproducible with no machine learning** (a lookup table + a
  containment test), held out of sample: policy fit on pre-2025 data, tested on
  requests created 2025-01-01 → 2026-07-21 it was never fit on. **97.27%.**
- **90% from geography alone.** **90.99%.**

These are the load-bearing claims. They are rates, they are stable, and they are the
reason the whole submission is "measured, not asserted." Quote them exactly.

## The frozen-policy hash (for the shadow scorecard / oracle)

```
b1f8107035578539f3c3a9f81e2ec1d9365ec038ed409ab8fc1bf96ea915a1f1
```

Minted 2026-07-21 on requests created before 2025-01-01. Immutable. It is what lets
the jury verify the routing policy was not retrofitted.

## Re-verify before you submit

```bash
node shadow/montreal-challenge-verify.mjs        # every proposal figure, PASS/DRIFT/FAIL
node shadow/shadow-run.mjs       # the live scorecard
```

Run both on submission morning. Expect **0 FAIL** and some **DRIFT** on counts (that
is correct). If a *rate* moves more than ~0.5pp, stop and investigate before quoting.

## What NOT to claim (carried from findings.md)

- Do **not** say the system predicts routing *before the City decides* — the open
  data ships each request already routed. The claim is "provably not retrofitted +
  independently recomputable," not "we beat the City to the answer."
- Do **not** present the 3M as the denominator of the 97% — the headline rests on
  the **1.5M located requests** (and the held-out 585,918). Keep the denominators
  straight: 3M scanned · ~1.5M evaluated · 585,918 held out.
- Do **not** quote `PROPRIETAIRE_REF` as a jurisdiction source — it's a territory
  tag that mislabels autoroutes as borough-owned. Jurisdiction is *reconciled*, not
  looked up.
