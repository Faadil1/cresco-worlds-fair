# CRESCO World’s Fair — Material Reality Reconciliation (2026-10-11)

**Status: SOURCE-ONLY AUDIT / NO PUBLIC OR MAINNET PROMOTION**

## Source binding and authority

- Central canon: `Faadil1/faadil-agent-system@cdb55dbfe41fdfcb2f5e9232517fbb058c8b4c9b`, version `0.1.59-adaptive-best-of-system-execution-v1-promoted`.
- World Fair governance baseline before this PR: `Faadil1/cresco-worlds-fair@ffcc8ea64604990a4014cfb1c8a7a01809fdbe67`.
- Product baseline: `Faadil1/cresco@4c7b82ff22ae7d4fb2756e68c640548bf1f7965d` (PR #30 already merged).
- World Fair living requirements: `product/PRD.md` in this governance repository; product repo's `product/PRD.md` is historical family/Key baseline, **not** the sole World Fair PRD.
- Protected actions retain human authority. GitHub branch/CI evidence does not prove deployment.

## Macro-lifecycle

`QUALIFY → DECIDE → DESIGN → DELIVER → AUDIT → EXPAND` remains active.

Judged-project sequence:
`RUBRIC → PAIN → PROBLEM → NEGATIVE EVENT → DIFFERENTIATOR → EXECUTION → LIVE DEPTH → EVIDENCE → STORY → DEMO → Q&A`.

Product exploitation remains primary. Neither competition timing, technical proof, seeded runs nor narrative work makes a vertical slice the Definition of Done.

## Truthful capability ledger

| Capability | Truth | Evidence class | Notes |
|---|---|---|---|
| Solana delegated capital authority | OBSERVED | LIVE | Solana Devnet, constrained program binary/hash evidence |
| Orca Whirlpools capital movement | OBSERVED | LIVE | One full 7/7 exact-head run `37214175230`; signatures in receipt |
| Pyth Lazer restriction / market evidence | OBSERVED | LIVE | Evidence may refuse/restrict but never grant |
| Autonomous standing execution | OBSERVED | LIVE | Two confirmed standing swaps in 7/7 |
| Exact exception + mutation/replay refusal | OBSERVED | LIVE | Exception grant and execution; standing policy unchanged |
| Hard boundary, invalid evidence, rollback, stale nonce | OBSERVED | LIVE | Scenario-specific proofs in 7/7 |
| Historical browser-triggered Devnet operator lab | OBSERVED | LIVE (historical build) | Does not prove current Worker deployment identity |
| Current `main` bound to public Worker `keys-api-stocklana` | UNKNOWN | MISSING deployment binding | The authorized workflow `37233079206` stopped before deployment due empty Cloudflare GitHub secrets |
| Current post-merge live repeatability | UNKNOWN | NOT_PROVEN | One live PASS does not prove reliability |
| Public operator-specific trade composition and execution | NOT_IMPLEMENTED | NOT_IMPLEMENTED | Existing `POST /api/v0.3/worlds-fair/run` accepts only `CANONICAL_LIVE` |
| Independent principal/allocator decision surface | NOT_IMPLEMENTED | NOT_IMPLEMENTED | Script's grant is not a real externally authenticated risk-owner decision |
| Verified principal/operator identity and permissions | NOT_IMPLEMENTED | NOT_IMPLEMENTED | Existing Devnet actor keys are held server-side |
| Persistent operator intent, exception request and receipt recovery | NOT_IMPLEMENTED as full workflow | NOT_IMPLEMENTED | Output receipt is not a durable actor-linked history |
| Uncertain hosted run quarantine | PROPOSED / LOCAL-VERIFIED only | LOCAL | Product draft PR #32: `a914b4736554982f6f8c042fa873c58d86f40a08`; do not claim LIVE |
| External representative operator validation / WTP | UNKNOWN | MISSING | Sanction founder interview is competitor/expert evidence, not customer demand |
| Time-to-first-value and operational economics | UNKNOWN | MISSING | No representative operator baseline, failure-rate or run-cost product telemetry |

## P0 blockers and consequences

### P0-01 — Public deployment identity and operational credentials

**OBSERVED:** PR #29 was merged, and CI passed. The authorized public deployment workflow run `37233079206` stopped before checkout/deploy because `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID` were absent. No public POST was executed. No later deployment binding is observed by this audit.

**Consequence:** current public API cannot be advertised as serving `4c7b82ff22ae7d4fb2756e68c640548bf1f7965d`.

**Next:** separately authorized credential provisioning/Cloudflare deployment/identity verification; preserve no-rerun limit and source identity.

### P0-02 — Protected workflows automatically triggered

**OBSERVED IN BASE MAIN:** `.github/workflows/worlds-fair-operator-lab-live.yml` triggers from `pull_request` for certain runtime files. Some other Devnet write workflows have automatic triggers. Product PR #31 proposes manual-only triggers and a regression guard.

**Consequence:** an ordinary source PR can unintentionally cause externally consequential Devnet writes.

**Next:** review PR #31, preserve a serialized manual workflow group with `cancel-in-progress: false`, pass CI, request explicit merge authorization. Its removal of the operator-lab concurrency block is an unresolved review finding as of this audit.

### P0-03 — Hosted unknown outcome / replay containment

**OBSERVED IN BASE MAIN:** public Worker unlocks its durable lease on completion even when run result is UNKNOWN; lease duration was five minutes. Expired lease did not itself prove no on-chain effects. This is a potential duplicate-action failure if retried.

**Response:** product draft PR #32 introduces server-side quarantine, read-only run-status, and negative tests. Historical partial-effect failures remain part of regression evidence.

**Remaining:** PR #32 is not merged/deployed, the human-authenticated reconciliation/release workflow is not implemented, and a browser-lost PASS response still needs durable intent idempotency to prevent double execution.

### P0-04 — Product depth is materially thinner than the selected wedge

**OBSERVED IN CODE:** only a fixed `CANONICAL_LIVE` 7/7 live sequence is exposed through the World Fair API. It is a powerful engineering verification view, not a configurable daily-use operator/allocator workflow.

**Missing load-bearing journey:** operator constructs an exact trade intent → current on-chain policy evaluation & Policy Diff → explicit principal/risk-owner decision → exact one-use authorization or refusal → bound real Devnet execution → durable status/consequence/recovery. This must be separately designed with genuine identity/authority; a seeded UX is not a replacement.

**Next:** continue product exploitation under World Fair concept lock, with real actions and negative/recovery paths before considering terminal readiness.

### P0-05 — Independent product and market validation

**OBSERVED:** Eric/Sanction yielded real expert/competitor input. Target-operator pull, exception preferences, buyer, payment intent and external clean-room operation remain unverified. Additional outreach was sent on October 7; no relevant reply was found at the October 11 Gmail check. No delivery receipt guarantees external comprehension or adoption.

**Next:** obtain two credible independent operator trials; observe a real recent exception event, workaround, frequency, operational cost, and whether exact one-use or time-bound envelope is preferred. Record negative responses without weakening the truth boundary.

### P0-06 — Canonical drift and dual-PRD authority confusion

**OBSERVED:** this World Fair repository remains pinned to central 0.1.48 while the central merged-main canon is 0.1.59, and the implementation state before PR #31 was pinned to 0.1.56. Product repo PRD is the family/Key baseline; World Fair living PRD and Concept Lock are in this governance repo.

**Next:** apply material-delta-aware pinning; keep Product Reality v1.5, Eval-Driven Reliability conditional (deterministic core; activate on material agent/stochastic or significant failure), Adaptive Best-of-System Execution without new authority; preserve all historical evidence and conditional gates.

## Gateway / product readiness disposition

- `LIVE_CORE_LOOP`: **PROVEN on Devnet** for fixed 7/7, not a full multi-role product.
- `RUNTIME_COMMIT_BINDING`: **PROVEN** for historical on-chain program; **BLOCKED/UNKNOWN** for latest public Worker.
- `PUBLIC_RUNTIME`: **BLOCKED** for latest merged repair identity.
- `NEGATIVE_PATH` / `EVIDENCE_INTEGRITY`: **PROVEN** for historical 7/7; active for new journeys.
- `EVAL_DRIVEN_RELIABILITY`: **conditional**; deterministic tests do not establish repeated stochastic reliability. Production failures are regression inputs.
- `PRE_LAUNCH_SHIP`, `JUDGE_PERFORMANCE_ASSURANCE`, `SUBMISSION_INTEGRITY`, `OUTSIDER_BREAK`, `RULES_ELIGIBILITY`: **ACTIVE** for future submission/ship assessment, not terminally PROVEN.
- `x402`, payments, mainnet, tokenized equities, other unrelated domains: **N/A with explicit reason** under current Devnet scope; re-activate when scope changes.
- Current terminal verdict: **NOT READY** for claims of complete operator product or current-public deployed reliability.

## Source-only execution this audit

- Product PR #31: canonical v0.1.59 reconciliation + manual-only workflow changes; CI observed green; **not merged**.
- Product PR #32: uncertain-run quarantine + read-only status + negative regression tests + recovery runbook; CI observed green before the runbook-only follow-up commit; **draft and not merged**.
- Review comment on PR #31 asks to restore manual-live serialization to avoid partial on-chain writes after cancellation.
- No new public deploy, no newly authorized Devnet live, no repeatability, no mainnet.

## Next high-value product exploitation milestone

1. Stabilize protected write workflows and quarantine; obtain verified CI and bounded merge authorization separately.
2. Resolve latest Worker public identity / credentials when separately authorized.
3. Productize the operator intent → risk/Policy Diff → principal decision → live bounded action → recovery contract, using one shared source of truth and actual authority.
4. Independent operator trial + clean-room break test; measure time to first value and operational costs.
5. Apply Final Canonical Assurance/Project Finisher for judged or terminal readiness only after material depth gaps are closed or explicitly blocked, not merely because a demo looks polished.

**Do not change existing Concept Lock or claim value/WTP by inference.**
