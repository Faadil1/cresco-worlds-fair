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
| World’s Fair web/operator surface exists in source | OBSERVED | LOCAL | `/worlds-fair` plus v0.3 API adapter are implemented and build-tested; public hosted binding is not yet observed |
| Judge self-serve World’s Fair flow exists | UNKNOWN | PARTIAL | Product surface and live shared core exist, but hosted UI→API→Solana execution has not yet been proven |
| Runtime/commit binding for World’s Fair build exists | OBSERVED | LIVE/PROVEN | Local rebuild and on-chain program dump are bit-identical: SHA-256 `084a3f7aad8a5772d773816579f5d2b98542c4b966dbb0dd7c60cb397db21f61`, run `37037374212` |
| System Control Plane v1 reconciled into this active project | OBSERVED | LOCAL | Adopted prospectively on 2026-10-01; not backdated |
| Lifecycle coverage manifest exists | OBSERVED | LOCAL | `governance/LIFECYCLE-COVERAGE.yaml` |
| Claim→Runtime→Evidence Graph exists | OBSERVED | LIVE/PARTIAL | Live core, bit-identical runtime binding and shared product core are bound to receipts; the remaining material causal edge is public hosted UI/API→Solana |
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
