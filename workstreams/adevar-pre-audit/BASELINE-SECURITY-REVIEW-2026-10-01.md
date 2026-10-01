# CRESCO — Baseline Security Review for Adevar

Date: 2026-10-01
Status: COMPLETED_FOR_BASELINE / NOT_FINAL_WORLD_FAIR_AUDIT
Reviewed repository: `Faadil1/cresco`
Reviewed commit: `0eb10dd8352bba69b9717d0d62d89794c9e384cc`
Primary source: `programs/keys/src/lib.rs`

## Purpose

This review tests the existing CRESCO Solana authority core against the Adevar pre-audit hypotheses H-01 through H-06.

It does **not** audit the future World’s Fair `TradeActionV0 + Orca` delta, because that implementation is not yet present in `Faadil1/cresco/main` or another active code branch as of this review.

Findings below are therefore classified against the existing baseline only.

## Result summary

| Hypothesis | Baseline result | Security interpretation |
|---|---|---|
| H-01 Charter `max_bounded_notional` | CONFIRMED UNUSED DOWNSTREAM | Semantic/configuration gap; not enough alone to claim exploitable loss |
| H-02 Allow-once vs period caps | CONFIRMED BASELINE ENFORCEMENT GAP | Exceptional path updates period counters but does not enforce the same period caps before transfer |
| H-03 Exact-action request binding | CONFIRMED UNDER-BINDING IN BASELINE | `request_hash` is caller-supplied and equality-checked, but not reconstructed from runtime action fields on-chain |
| H-04 Lifecycle paused/revoked/expired transitions | PARTIAL SEMANTIC GAP | Capital execution/grant paths fail closed, but review/stage-transition paths do not uniformly check status/expiry |
| H-05 Token-2022 extension semantics | CONFIRMED UNRESTRICTED EXTENSION SURFACE | Interface permits Token/Token-2022; no explicit extension-policy checks found |
| H-06 Pyth verified-bytes/parser equivalence | NO DIRECT MISMATCH FOUND / REVIEW REMAINS | Same `pyth_message` slice is passed to verification CPI and then parsed; custom-parser assumptions still require audit |

## H-01 — Charter bounded-cap semantics

### Observation

`initialize_charter` receives and stores:
- `max_proposal_notional`
- `max_bounded_notional`

`max_proposal_notional` is subsequently enforced in `commit_proposal`.

A full-source search at the reviewed commit found `max_bounded_notional` only:
1. as an initializer argument;
2. in its non-zero validation;
3. when stored in `Charter`;
4. in the account struct.

No downstream enforcement use was found.

### Classification

**SEMANTIC_AMBIGUITY / CONFIGURATION_GAP — CONFIRMED**

This is not automatically an exploit because the intended authority of the field is unclear. However, a field named `max_bounded_notional` can create a false security assumption if product, UI or operators believe it is enforced.

### Required World’s Fair disposition

Before final audit freeze:
- enforce it if it remains an authoritative cap;
- or remove/deprecate it and document that it is non-authoritative.

Do not leave a security-looking field with undefined enforcement semantics.

---

## H-02 — Allow-once interaction with period caps

### Standing path

`execute_within_mandate` checks:
- per-action amount through `validate_execution_common`;
- then calculates `next_spent`;
- then enforces `next_spent <= asset_rule.max_period_amount`.

`execute_within_mandate_with_pyth` additionally checks:
- period amount;
- period notional against `mandate.max_period_notional`.

### Exceptional path

`execute_once_with_pyth`:
- validates status, stage, expiry and nonce;
- validates allowance;
- verifies Pyth;
- computes exact allowance notional;
- computes `next_spent_amount`;
- computes `next_spent_notional`;
- transfers capital;
- writes both period counters;
- consumes the allowance.

But in the reviewed baseline, the exceptional path does **not** apply the equivalent pre-transfer checks against:
- `asset_rule.max_period_amount`;
- `mandate.max_period_notional`.

### Classification

**CONFIRMED BASELINE ENFORCEMENT GAP**

Whether the old product intended an Allow-once to override period limits was not encoded explicitly in the contract.

For the locked World’s Fair v1, the Concept Lock now says:
- the soft boundary is **per-action/per-trade notional**;
- exceptional execution still updates relevant period counters;
- the exception does not mutate the standing limit.

Therefore the new implementation should make explicit that the exception overrides only the locked soft boundary and does not silently waive unrelated period policy.

### Required test

Create a test where:
- remaining period capacity is below the exceptional trade;
- per-action soft-boundary exception is otherwise valid;
- expected result is REFUSE unless primary canon explicitly authorizes period-limit override.

---

## H-03 — Exact-action request binding

### Observation

`grant_allowance_once` accepts a caller-supplied `request_hash` and stores it in `AllowanceReceipt`.

The allowance PDA is also derived partly from that supplied hash.

`execute_once_with_pyth` accepts a caller-supplied `request_hash` and checks equality with the stored receipt.

However, the program does not reconstruct `request_hash` from the runtime action parameters.

Independent constraints bind:
- Mandate;
- beneficiary;
- mint;
- nonce;
- allowance notional;
- expiry;
- one-use state.

But the hash itself is not on-chain evidence that those runtime fields correspond to the exact action originally represented off-chain.

### Consequence

A compromised or adversarial client can reuse the same approved hash with different runtime semantics that still satisfy the independent on-chain checks.

In the baseline, “exact action” is therefore materially closer to:
> exact allowance lineage + mint + beneficiary + near-exact Pyth-derived notional

than to a universal canonical action binding.

### Classification

**CONFIRMED BASELINE UNDER-BINDING**

This directly validates why the World’s Fair spec requires a canonical `TradeActionV0` encoding/hash reconstructed or checked on-chain.

### Required World’s Fair disposition

The final implementation must bind at least:
- action kind;
- exact Orca program;
- exact Whirlpool;
- input mint;
- output mint;
- input amount;
- min output/slippage floor;
- deadline;
- source Mandate nonce.

No opaque client-supplied “semantic hash” may be trusted without reconstruction/checking.

---

## H-04 — Mandate lifecycle consistency

### Good baseline behavior

`grant_allowance_once` requires:
- current nonce;
- `MANDATE_ACTIVE`;
- non-expired Mandate.

Execution authority requires:
- current nonce;
- `MANDATE_ACTIVE`;
- bounded-or-higher stage;
- non-expired Mandate;
- enabled rule;
- supported action mask.

`set_mandate_status` refuses modification after the Mandate is already revoked.

This means capital movement remains strongly fail-closed for paused/revoked/expired Mandates.

### Gap

`record_review` does not check Mandate status or expiry.

`transition_mandate` checks:
- receipt eligibility;
- nonce match;
- receipt nonce;
- forward-only stage transition.

It does not explicitly check:
- `MANDATE_ACTIVE`;
- non-expired state;
- non-revoked state.

A guardian can therefore record review evidence and advance stage while the Mandate is paused. A revoked Mandate can also receive review/stage activity, although it cannot later be reactivated through `set_mandate_status`.

### Classification

**PARTIAL SEMANTIC / DEFENSE-IN-DEPTH GAP**

No direct capital escape was found because execution still checks status/expiry and revocation remains terminal.

However, authority-state history can evolve while operationally disabled, which may be surprising and should be deliberate.

### Required decision

For World’s Fair:
- either explicitly permit administrative stage evolution while paused and document it;
- or require active/non-expired lifecycle state for stage-authority transitions.

---

## H-05 — Token / Token-2022 extension semantics

### Observation

The Rust program uses Anchor SPL `TokenInterface` and enables both:
- `token`
- `token_2022`

The transfer path uses `transfer_checked`.

No explicit source checks were found that restrict supported mint extensions or reject extension configurations whose economics/side effects differ from the simple transfer model.

Potentially material extension classes include:
- transfer fees;
- transfer hooks;
- default account state / freeze-related behavior;
- confidential-transfer-related semantics;
- other extensions affecting amount received or execution behavior.

### Classification

**CONFIRMED UNRESTRICTED EXTENSION SURFACE**

This does not mean the current demo token is unsafe. It means the program’s accepted interface is broader than the documented/simple accounting assumptions unless mint configuration is constrained elsewhere.

### Required World’s Fair disposition

For the initial Orca Devnet pair:
- identify the actual token program and mint extensions for both assets;
- explicitly allow only configurations whose semantics CRESCO models;
- fail closed on unsupported extension combinations.

---

## H-06 — Pyth verification / parser equivalence

### Positive evidence

In both Pyth-backed execution paths:
1. the exact `pyth_message: Vec<u8>` supplied to the CRESCO instruction is passed into `verify_pyth_message_via_lazer`;
2. the same slice is then passed to `parse_verified_market_evidence`.

The verification helper:
- checks the expected Pyth program ID;
- checks expected storage;
- checks the instructions sysvar;
- constructs the Pyth Lazer `verify_message` CPI using those message bytes.

The parser then verifies:
- format magic;
- payload magic;
- accepted channel;
- exactly one feed;
- expected feed ID;
- known property IDs only;
- positive price;
- confidence;
- timestamp/freshness;
- safe exponent conversion.

### No direct mismatch found

No code path was found where one byte array is verified and a different byte array is parsed.

### Remaining audit surface

The implementation uses a custom parser for a deliberately small subset of the public Pyth payload schema.

Adevar should still review:
- duplicate property semantics;
- ordering assumptions;
- exact Pyth Lazer serialization compatibility;
- instruction-index assumptions used by the verification CPI;
- unsupported future schema evolution;
- confidence/exponent arithmetic boundaries.

### Classification

**NO DIRECT VULNERABILITY FOUND IN BASELINE / EXTERNAL REVIEW STILL WARRANTED**

---

## Baseline severity triage

### Must be addressed before reusing unchanged in World’s Fair execution

1. **H-02 — exceptional path period-cap enforcement**
2. **H-03 — canonical exact-action binding**

These conflict most directly with the newly locked World’s Fair security semantics if the baseline path were copied unchanged.

### Must be resolved explicitly before audit freeze

3. H-01 — bounded-cap semantics
4. H-04 — lifecycle transition semantics
5. H-05 — Token-2022 supported-extension policy

### Continue specialist review

6. H-06 — Pyth parser/CPI correctness

## H-07 through H-10

Status: **BLOCKED_NOT_IMPLEMENTED**

The current `Faadil1/cresco` main branch does not yet contain:
- `TradeActionV0`;
- Orca program integration;
- Whirlpool constraints;
- min-output/slippage binding;
- constrained venue CPI.

Therefore the following cannot yet be honestly tested:
- H-07 Orca constrained-CPI escape;
- H-08 slippage/output mutation;
- H-09 arbitrary-CPI regression;
- H-10 atomic Orca exception consumption/retry behavior.

They remain mandatory once the implementation lands.

## Promotion rule

This review must not be described as:
- an external audit;
- an Adevar audit;
- production security certification;
- final World’s Fair security approval.

It is an internal baseline security review used to improve audit readiness and preserve known gaps before the real implementation/freeze.
