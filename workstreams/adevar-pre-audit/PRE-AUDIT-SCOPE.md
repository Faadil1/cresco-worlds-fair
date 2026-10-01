# CRESCO — Adevar Labs Pre-Audit Scope

Status: ACTIVE WORKSTREAM DRAFT
Date: 2026-10-01
Workstream: ADEVAR_PRE_AUDIT
Authority: NONE
Product-scope effect: NONE

## 1. Workstream boundary

Adevar is a separate security workstream for the same CRESCO product core.

It may inspect, challenge, and later help remediate the real implementation, but it MUST NOT:
- redefine the locked World’s Fair concept;
- widen the Colosseum build scope;
- introduce arbitrary CPI or extra venues;
- convert missing operator validation into PASS;
- upgrade Devnet evidence into production evidence;
- silently change product semantics when a security finding is actually a product-policy ambiguity.

Material semantic changes must return to the primary CRESCO canonical project first.

## 2. Current canonical product state

Primary project:
- repo: `Faadil1/cresco-worlds-fair`
- branch: `main`
- state: `CONCEPT_LOCKED_WITH_VALIDATION_GAP`
- current phase: `BUILD`
- build authorized: `true`
- current gate: `BUILD__FIRST_LIVE_VERTICAL_SLICE`

Locked product:
> CRESCO is an execution-bound delegated capital authority layer for Solana.

Locked first vertical:
- delegated trading / capital mandates;
- `SWAP_EXACT_IN`;
- one constrained venue: Orca Whirlpools on Solana Devnet;
- one-use exact exceptional authority;
- soft boundary: per-action/per-trade notional;
- hard boundary: unsupported program, pool, or unparseable action semantics;
- no arbitrary CPI.

Selected venue:
- Orca Whirlpools program: `whirLbMiicVdio4qvUfM5KAg6Ct8VwpYzGff3uctyCc`
- initial pool candidate: `63cMwvN8eoaD39os9bKP8brmA7Xtov9VxahnPufWCSdg`
- initial pair: devUSDC / devUSDT
- fallback pool: `3KBZiL2g8C7tiJ32hTv5v3KM7aK9htpqTw4cTXz1HvPt`
- fallback pair: SOL / devUSDC

## 3. Existing security baseline

Existing implementation:
- repo: `Faadil1/cresco`
- preparation baseline commit: `0eb10dd8352bba69b9717d0d62d89794c9e384cc`
- network: Solana Devnet
- CRESCO program: `ABjE6V5q9VbD3CAHDXxvztY5kXQmDXHRcEP1kZ4KSSfk`

This baseline already contains:
- versioned Mandate + nonce;
- guardian/principal vs beneficiary/delegate signer separation;
- AssetRule limits;
- program-controlled SPL-token vault;
- standing-authority capital execution;
- one-time exceptional authority;
- stale/replay refusal;
- Pyth Lazer verification and bounded parsing;
- amount/notional accounting;
- fail-closed behavior.

Evidence class:
**HISTORICAL TECHNICAL / DEVNET PROOF**.

It is not the final World’s Fair audit target.

## 4. Final audit target

The final Adevar audit target MUST be the exact CRESCO shared-core commit that implements the locked World’s Fair delta.

Final target fields:
- repository: expected `Faadil1/cresco`
- commit SHA: **BLOCKED until implementation freeze**
- network: Solana Devnet for the hackathon proof unless canon changes
- CRESCO program ID: **REVERIFY at freeze**
- Orca program ID: must equal the locked supported value
- exact pool(s): must equal the explicitly supported configuration
- CI run(s): **BLOCKED until final commit**
- runtime/deployment identity: **BLOCKED until final live slice**

## 5. Primary audit scope

### A. Existing CRESCO authority core

Primary source:
- `programs/keys/src/lib.rs`

Audit:
- Charter / Mandate / AssetRule state;
- signer constraints;
- PDA derivation;
- status / stage / version / nonce / expiry;
- standing authority;
- one-time exceptional authority;
- allowance creation, binding, expiry, consumption and replay refusal;
- vault authority;
- amount and notional arithmetic;
- period counters;
- Pyth verification CPI;
- verified-message parsing;
- failure atomicity.

### B. World’s Fair trading delta

Audit the implementation of `TradeActionV0`.

Locked semantic fields:
- `action_kind`;
- `venue_program`;
- `whirlpool`;
- `input_mint`;
- `output_mint`;
- `input_amount`;
- `min_output_amount`;
- `max_notional_micro_usd`;
- `deadline`;
- `mandate_nonce`.

Review requirements:
- deterministic canonical encoding;
- semantic hash reconstruction;
- all material fields bound;
- no caller-controlled opaque semantics;
- exact pool/mint relationship;
- deadline enforcement;
- slippage/min-output enforcement;
- stale nonce refusal;
- mutation refusal.

### C. Constrained Orca adapter

Audit:
- exact Orca program ID check;
- exact supported pool check;
- input/output mint checks;
- required Orca account validation;
- writable/signer account minimization;
- tick-array/oracle/account substitution resistance where applicable;
- instruction discriminator and parameter correctness;
- no arbitrary target program;
- no arbitrary instruction bytes;
- no arbitrary account metas;
- no generic CPI passthrough;
- CPI failure rollback.

### D. Pyth/risk path

Where Pyth remains load-bearing:
- expected program/storage;
- verified bytes = parsed bytes;
- feed binding;
- freshness;
- confidence;
- timestamp;
- exponent;
- notional conversion;
- no authority widening from market evidence.

### E. Off-chain construction / outcome truth

Supporting scope when security-relevant:
- canonical TradeAction construction;
- request/action hash construction;
- transaction retry/idempotency;
- confirmation status;
- PENDING/UNKNOWN vs confirmed success;
- receipt binding to transaction, Mandate, exception and runtime.

## 6. Explicitly out of primary scope

Unless it becomes load-bearing:
- visual design;
- market research;
- outreach;
- submission narrative;
- learning content;
- unrelated frontend surfaces;
- speculative future multi-venue routing;
- leverage;
- lending;
- order books;
- mainnet deployment;
- generalized arbitrary DeFi execution.

## 7. Security assets

Protect:
1. program-controlled capital;
2. principal-only authority mutation;
3. standing Mandate integrity;
4. one-time exceptional authority;
5. TradeAction semantic integrity;
6. stale/replay invalidation;
7. pool/program/mint constraints;
8. period/notional accounting;
9. Pyth evidence integrity;
10. atomic Orca execution + state mutation;
11. truthful execution outcome.

## 8. Highest-priority audit questions

1. Can a delegate or arbitrary signer widen authority?
2. Can old authorization survive a Mandate nonce change?
3. Can a one-use exception authorize a semantically different trade?
4. Is the semantic hash reconstructed from canonical fields rather than trusted from the client?
5. Can the exception bypass any standing dimension other than the locked soft boundary?
6. Are period counters/caps preserved under exceptional execution?
7. Can a caller redirect the CPI to another program, pool, mint, tick array, vault, or destination?
8. Can Orca CPI account substitution change economic meaning while the CRESCO hash still matches?
9. Can slippage, minimum output, deadline, notional, or route semantics mutate after approval?
10. Can failed Orca/Pyth/token CPI consume exception state or counters?
11. Can Token-2022 or mint extensions invalidate CRESCO accounting assumptions?
12. Can rounding/truncation reduce the computed notional enough to bypass authorization?
13. Does `max_bounded_notional` have intended enforcement or is it obsolete metadata?
14. Are paused/revoked/expired Mandates consistently fail-closed across every privileged path?
15. Can an unknown transaction outcome be retried into duplicate capital movement?

## 9. Current review hypotheses

These are not confirmed vulnerabilities.

### H-01 — Charter bounded cap semantics
`max_bounded_notional` exists in the baseline but was not found in downstream enforcement. Determine whether it is intentionally obsolete or a missing invariant.

### H-02 — Exceptional execution vs period policy
The locked v1 exception is for the per-action soft boundary only. The final implementation must demonstrate that an exception does not silently bypass other standing risk dimensions, including period policy, unless canon explicitly says otherwise.

### H-03 — TradeAction semantic hash completeness
The World’s Fair design requires deterministic binding of program, pool, pair, amount, min output/slippage, deadline and nonce. Verify every material field is reconstructed and bound on-chain.

### H-04 — Mandate lifecycle consistency
Test proposal, transition, allowance grant and execution under paused, revoked and expired states.

### H-05 — Token extension behavior
Verify supported Token/Token-2022 mint configurations do not change transfer economics or callback behavior beyond CRESCO’s assumptions.

### H-06 — Pyth verification/parser equivalence
Validate that CRESCO parses the same authenticated bytes Pyth verifies, with no ambiguity or unsupported layout path.

### H-07 — Orca constrained-CPI escape
Attempt wrong program, unsupported pool, swapped mints, arbitrary writable accounts and account substitution.

### H-08 — Slippage/output mutation
Ensure principal-approved `min_output_amount` and related execution constraints cannot be weakened after authorization.

### H-09 — Arbitrary CPI regression
Ensure no helper or adapter layer evolves into caller-controlled arbitrary program/instruction/account passthrough.

### H-10 — Atomic exception consumption
Prove venue/oracle/token failure rolls back counter and allowance state, while successful exception execution consumes exactly once.

## 10. Final evidence package

Before Adevar submission/freeze, provide:
- exact repo + commit SHA;
- final program/network IDs;
- build/test instructions;
- dependency versions and lock state;
- architecture and trust boundaries;
- canonical action serialization spec;
- supported venue/pool configuration;
- security invariants;
- threat/attack matrix;
- current CI runs;
- success/boundary/mutation/replay/stale/hard-boundary/oracle-failure/venue-failure receipts;
- known limitations and unresolved findings;
- commit ↔ runtime/deployment binding where live claims depend on it.

## 11. Scope-delta rule

Any post-freeze change to:
- authority semantics;
- TradeAction fields/serialization;
- signer/accounts/PDAs;
- Orca adapter/account constraints;
- token program behavior;
- Pyth semantics;
- exception consumption;
- counters;
- or retry/outcome logic

requires an explicit audit-scope delta review.

Adevar findings may drive remediation. They do not independently authorize a product-direction change.
