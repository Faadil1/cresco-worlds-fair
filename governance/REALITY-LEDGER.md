# CRESCO Reality Ledger

Date: 2026-10-02  
Status: ACTIVE

## Purpose

Keep product claims weaker than or equal to actual evidence.

Allowed evidence labels:
- LIVE
- LOCAL
- LOCAL_STUB
- PRESEEDED
- SIMULATED
- PARTIAL
- NOT_IMPLEMENTED

Truth labels:
- OBSERVED
- INFERRED
- UNKNOWN

## Current World’s Fair reality

| Claim / capability | Truth | Evidence state | Current note |
|---|---|---|---|
| Stocklana baseline Solana Devnet capital-path proof exists | OBSERVED | LIVE/BASELINE | Proven in original CRESCO repo/runtime; not equivalent to World’s Fair live product |
| Standing vs exceptional authority semantics exist in baseline | OBSERVED | LOCAL/LIVE-BASELINE | Exact one-time allowance path exists for current specialized action model |
| World’s Fair final wedge selected | OBSERVED | LOCAL | Locked 2026-10-01 as delegated trading / execution-bound delegated capital authority under explicit validation gap |
| Delegated Capital Authority is validated by users | UNKNOWN | PARTIAL | Still not validated by target operators; Concept Lock proceeded under explicit human validation-gap override |
| World’s Fair Live Core Loop exists | OBSERVED | LIVE | Proven on Solana Devnet and strengthened in bound workflow run `37037374212`; receipt: `evidence/runtime/FIRST-LIVE-VERTICAL-SLICE-2026-10-02.md` |
| Load-bearing World’s Fair trading integration exists | OBSERVED | LIVE | CRESCO program `7pgPuPZ…` executes through Orca Whirlpools Devnet pool `63cMwv…`; Pyth evidence is load-bearing where claimed |
| Real execution consequence exists | OBSERVED | LIVE | Standing swaps change Devnet state; exact exception executes once; failed Orca swap rolls back without consuming authority/counters |
| Organic adoption exists | UNKNOWN | NOT_IMPLEMENTED | Outreach/interviews do not equal adoption |
| x402 is part of CRESCO | UNKNOWN | N/A | Not currently in scope |
| LIVE_GATEWAY settlement exists | UNKNOWN | N/A | No load-bearing external payment gateway in current scope |
| Technical Reality Check for locked World’s Fair vertical | OBSERVED | LOCAL | PASS_WITH_BOUNDED_DELTA; no venue integration built yet |
| New World’s Fair on-chain runtime exists | OBSERVED | LIVE | Solana Devnet program `7pgPuPZSUUtFcvFtVGmS3piCE1bHY35kjb14vct9v45Z`; not yet a judge-facing public product surface |
| Shared World’s Fair product core exists | OBSERVED | LIVE | Reusable server-side provider executed 7/7 canonical consequences live in run `37083019145`; receipt: `evidence/runtime/WORLDS-FAIR-OPERATOR-LAB-LIVE-2026-10-02.md` |
| Public World’s Fair v0.3 runtime GET exists | OBSERVED | LIVE | Cloudflare Worker deployment from merge `fa26ff0…` returned HTTP 200 with exact Program ID and program SHA; evidence: `HOSTED-PUBLIC-RUNTIME-FIRST-ATTEMPT-2026-10-02.md` |
| Public World’s Fair v0.3 live POST is reliable | OBSERVED | PARTIAL / INTERMITTENT | Deployed PR #16 runtime remains intermittently affected by public Devnet RPC throttling. PR #18 exact head `494818b…` now passes a full 7/7 live Devnet sequence under substantial 429 throttling, but that repair is not yet merged/deployed. Public hosted reliability therefore remains PARTIAL until post-deploy verification. Evidence: `HOSTED-PREFLIGHT-STATE-READ-BACKOFF-LIVE-VALIDATION-PASS-2026-10-03.md`. |
| World’s Fair web/operator surface is publicly hosted | OBSERVED | LIVE | Full CRESCO frontend is live at `https://cresco.faadil-casecraft.workers.dev`; hosted Chromium proof reached `/worlds-fair` and observed runtime state `Ready`; evidence: `CRESCO-CLOUDFLARE-CORS-AUTH-HOSTED-PASS-2026-10-03.md` |
| Judge self-serve World’s Fair technical flow exists | OBSERVED | PARTIAL / INTERMITTENT | A fresh Chromium run proved the complete path once, but a later manual browser run ended UNKNOWN. Treat self-serve as technically possible but not yet repeatably reliable. |
| Runtime/commit binding for World’s Fair build exists | OBSERVED | LIVE/PROVEN | Local rebuild and on-chain program dump are bit-identical: SHA-256 `084a3f7aad8a5772d773816579f5d2b98542c4b966dbb0dd7c60cb397db21f61`, run `37037374212` |
| System Control Plane v1 reconciled into this active project | OBSERVED | LOCAL | Adopted prospectively on 2026-10-01; not backdated |
| Lifecycle coverage manifest exists | OBSERVED | LOCAL | `governance/LIFECYCLE-COVERAGE.yaml` |
| Claim→Runtime→Evidence Graph exists | OBSERVED | LIVE/PROVEN_WITH_VALIDATION_GAP | Live core, runtime binding, hosted API→Solana, hosted browser, exact CORS, login and browser-triggered 7/7 execution are bound to receipts. Independent external-human validation remains a separate non-runtime evidence gap. |
| Product Exploitation Loop is active now | OBSERVED | LIVE/PROCESS | ACTIVE after the proven first live vertical slice; depth review at `product/POST-VERTICAL-SLICE-DEPTH-GAP-REVIEW-2026-10-02.md` |
| Adevar pre-audit reference is adopted product scope | OBSERVED | N/A | False; currently CLASSIFIED / REFERENCE_ONLY in central Reference Intelligence inbox |

## Rule

Any future claim must add:
- exact evidence location;
- commit/runtime binding where relevant;
- truth label;
- evidence state;
- known limitation.

Missing evidence → **UNKNOWN**, never silent PASS.

## 2026-10-02 live-slice promotion

The World’s Fair vertical is now truthfully promotable to **FIRST_LIVE_VERTICAL_SLICE** on Solana Devnet.

Observed live path:
- standing autonomous Orca swaps;
- soft per-action notional refusal;
- exact one-use exceptional authority;
- semantic mutation refusal;
- replay refusal;
- unsupported-program hard refusal;
- missing Pyth evidence refusal;
- Orca failure rollback with allowance/counter preservation;
- stale-authority refusal after Mandate nonce change.

Preserved limits:
- no mainnet claim;
- no production custody claim;
- no audited-security claim;
- no institutional-trading claim;
- no operator-demand/WTP/adoption claim;
- no judge self-serve product-surface claim yet.

## 2026-10-02 / 2026-10-03 UTC shared-core promotion

Observed at source head `cedfbb400f00f28fbe4268fde46ab68933d42e3c`:
- reusable World’s Fair server-side provider is live on Solana Devnet;
- stable distinct delegate is `4VLFryH36ed8Mc7ByBMLwvtrtYMgo2hKmAicDU2oRfj7`;
- stable Mandate is `CPdat8L1kNUZXAHd6smzeK14nRXD9p1kXU4pF6SSMBXG`;
- seven canonical consequences pass through the shared core;
- overlapping public-run semantics are serialized with a Durable Object lease and return `409 BUSY` in tests;
- Cloudflare Worker dry-run bundle passes;
- the web surface is implemented and build-tested.

Still **not observed**: public hosted Worker + public `/worlds-fair` + UI-triggered live Solana receipt. Therefore judge self-serve remains UNKNOWN/PARTIAL, not PROVEN.


## 2026-10-03 hosted browser 7/7 promotion

Observed in run `37124741369`:
- public frontend: `https://cresco.faadil-casecraft.workers.dev`;
- public API: `https://keys-api-stocklana.faadil-casecraft.workers.dev`;
- fresh Chromium browser opened `/worlds-fair`;
- runtime state: Ready;
- browser clicked the live authority control;
- UI displayed `7/7 live checks proven`;
- five Solana Explorer transaction links were visible;
- browser request failures: 0;
- starting Mandate nonce: 6;
- a second browser context with no cookies/storage also reached the public product, Runtime Ready state and live-run control.

External-human judge/operator use was **not** observed and must not be inferred from this technical clean-room proof.


## 2026-10-03 manual intermittent reliability downgrade

A later manual browser recording reached public `/worlds-fair`, observed Runtime Ready and Mandate nonce 7, then ended with `WORLD_FAIR_LIVE_RUN_UNCONFIRMED` after the user triggered the live sequence.

This is a real negative event. It does not erase the prior 7/7 PASS, but it downgrades repeatable technical self-serve from PROVEN to PARTIAL / INTERMITTENT until the failure is diagnosed and repaired.

See `evidence/runtime/HOSTED-MANUAL-INTERMITTENT-UNKNOWN-2026-10-03.md`.


## 2026-10-03 reliability repair deployment

PR #15 exact head `e868b1522c9fa28486777e3805f52a4c5d27093e` was merged as `0ef9dc9618d9cbdfac1e714b7349993f4292aff9`.

Observed production deployment:
- backend Worker `keys-api-stocklana`: SUCCESS, build `a3a7d586-8392-417f-a574-744e340ee469`;
- frontend Worker `cresco`: SUCCESS, build `2b755dc6-b38e-4a75-a5d1-d91ce01104fd`;
- post-deploy read-only `/worlds-fair`: HTTP 200;
- post-deploy read-only World’s Fair runtime: HTTP 200 / READY;
- no World’s Fair live authority sequence was executed by the read-only smoke.

An unrelated legacy `devnet-execution-bridge` workflow auto-triggered from the main-branch merge because `src/http-api.mjs` changed. It preserved a real period refusal, emitted no successful new on-chain execution signature in its logs, and failed closed on `PYTH_MARKET_EVIDENCE_UNAVAILABLE`. This side effect was outside the explicit merge/redeploy authorization and is recorded as a CI governance defect to gate before future protected merges.

Stable hosted self-serve remains PARTIAL / INTERMITTENT until separately authorized post-deploy live repeatability checks succeed.


## 2026-10-03 ORCA_CONTEXT read-retry deployment

PR #16 exact head `9eb857bb3c369a0ab412977a976c131afac6899f` was merged as `27300a396d9f3049f19e7aed228acdb2f0bdf9d9`.

Observed production deployment:
- backend Worker `keys-api-stocklana`: SUCCESS, build `35efb0a3-f66e-4e66-9839-57893ee75be4`;
- frontend Worker `cresco`: SUCCESS, build `b70afa8d-707a-4665-9a05-e29db714c98f`;
- post-deploy read-only `/worlds-fair`: HTTP 200;
- post-deploy read-only World’s Fair runtime: HTTP 200 / READY;
- no live authority sequence was executed by the read-only smoke;
- the legacy `devnet-execution-bridge` was not triggered because PR #16 did not touch its monitored paths.

Stable hosted self-serve remains PARTIAL / INTERMITTENT until a fresh bounded post-deploy browser live-repeatability campaign succeeds.


## 2026-10-03 post-PR16 quote-stage reliability finding

A separately authorized bounded repeatability campaign was rerun against the deployed PR #16 runtime.

Observed:
- attempt 1: fresh-browser 7/7 PASS, nonce `10 → 11`, five transaction links, zero browser request failures;
- attempt 2: HTTP 503 / UNKNOWN at `STANDING_1_QUOTE`;
- failure class: `TRANSIENT_RPC`;
- retry policy: `SAFE_RETRY_READ`;
- confirmed effects: `0`;
- attempt 3: not executed.

This proves the ORCA_CONTEXT repair moved the failure frontier forward, but public Devnet RPC throttling can still exhaust the quote-stage read retry budget after one full live run.

A source-only repair now increases the read-heavy Orca retry profile to six attempts with a 2-second linear base delay, for a maximum 30-second wait budget before the sixth attempt. Write paths remain non-replayed. This patch is non-live proven only and awaits a separate live-validation authorization.

See:
- `evidence/runtime/HOSTED-POSTDEPLOY-REPEATABILITY-AFTER-ORCA-RETRY-2026-10-03.md`
- `evidence/runtime/HOSTED-ORCA-QUOTE-READ-BACKOFF-PREMERGE-2026-10-03.md`


## 2026-10-03 PR #18 exact-head live reliability validation

PR #18 source head `494818b67b0e2ab8cdb304c64422e36d89dc67f0` was validated live on Solana Devnet before merge.

Observed:
- root PR test run `37149230534`: PASS;
- Cloudflare Worker CI run `37149230535`: PASS;
- World’s Fair live-provider run `37149230540`: PASS;
- live job `111279373905`;
- runtime state before execution: READY;
- starting Mandate nonce: `11`;
- ending Mandate nonce: `12`;
- all seven canonical scenarios: PASS;
- receipt artifact: `11283376180`;
- artifact digest: `sha256:383773aa09db6d5fe8cd562fc4ef80cb08aac3693181d2b7cdf216f871960f19`.

A substantial burst of public Solana Devnet RPC HTTP 429 responses occurred during the successful run. The bounded read-side retry repair recovered and completed the canonical sequence. This is direct evidence that the new preflight/state + quote read budgets improve resilience under the observed failure mode.

Truth boundary:
- this is LIVE exact-head Devnet evidence;
- it is not evidence that the public Cloudflare runtime contains the repair;
- it is not post-deploy repeatability evidence;
- public hosted self-serve remains PARTIAL / INTERMITTENT until PR #18 is separately authorized, merged, deployed and re-verified;
- PR #17 remains untouched/superseded.

See `evidence/runtime/HOSTED-PREFLIGHT-STATE-READ-BACKOFF-LIVE-VALIDATION-PASS-2026-10-03.md`.
