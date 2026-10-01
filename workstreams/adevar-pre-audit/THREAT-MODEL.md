# CRESCO — Threat Model and Attack Matrix

Status: ACTIVE DRAFT
Date: 2026-10-01
Scope: Adevar pre-audit workstream

## Objective

Prevent any actor, stale authorization, semantic mutation, external dependency, malformed account set, retry, arithmetic edge case or CPI escape from causing capital movement beyond the exact authority CRESCO intends to grant.

## Adversaries

- malicious delegate with its legitimate signing key;
- unauthorized signer;
- compromised/off-spec frontend or backend;
- replay/retry actor;
- malicious account supplier;
- malformed/stale/wrong-feed oracle-data supplier;
- adversarial mint/token-extension configuration;
- CPI account-substitution attacker;
- integration failure producing ambiguous transaction state.

## Attack matrix

| ID | Attack / failure hypothesis | Expected safe behavior | Priority |
|---|---|---|---|
| ATK-01 | Delegate invokes guardian-only policy mutation | REFUSE | P0 |
| ATK-02 | Wrong Charter/Mandate lineage | REFUSE seeds/has_one | P0 |
| ATK-03 | Replay old ReviewReceipt after nonce change | REFUSE | P0 |
| ATK-04 | Replay old exceptional authority after nonce change | REFUSE | P0 |
| ATK-05 | Replay already-consumed exception | REFUSE | P0 |
| ATK-06 | Different delegate consumes exception | REFUSE | P0 |
| ATK-07 | Different input mint | REFUSE | P0 |
| ATK-08 | Different output mint | REFUSE | P0 |
| ATK-09 | Increase input amount | REFUSE | P0 |
| ATK-10 | Materially decrease/change exact amount | REFUSE except explicitly accepted rounding semantics | P0 |
| ATK-11 | Weaken min output/slippage after approval | REFUSE semantic mismatch | P0 |
| ATK-12 | Change deadline after approval | REFUSE | P0 |
| ATK-13 | Use expired action/exception | REFUSE | P0 |
| ATK-14 | Change action kind | REFUSE | P0 |
| ATK-15 | Hash collision via non-canonical/ambiguous serialization | One canonical serialization; no ambiguity | P0 |
| ATK-16 | Client submits hash that does not match runtime fields | On-chain reconstruction/check refuses | P0 |
| ATK-17 | Standing action exceeds per-trade notional | REFUSE under standing authority | P0 |
| ATK-18 | Exception used to bypass period cap | REFUSE unless canon explicitly authorizes that dimension | P0 |
| ATK-19 | Period-counter overflow | REFUSE | P0 |
| ATK-20 | Period-boundary time edge resets early/twice | Correct deterministic accounting | P1 |
| ATK-21 | Paused Mandate executes | REFUSE | P0 |
| ATK-22 | Revoked Mandate executes | REFUSE | P0 |
| ATK-23 | Expired Mandate executes | REFUSE | P0 |
| ATK-24 | Grant exception while lifecycle state forbids it | REFUSE | P0 |
| ATK-25 | Transition authority from forbidden lifecycle state | REFUSE | P0 |
| ATK-26 | Wrong venue program | HARD REFUSE, no exception route | P0 |
| ATK-27 | Arbitrary program ID routed through adapter | HARD REFUSE | P0 |
| ATK-28 | Arbitrary instruction bytes | Impossible by construction | P0 |
| ATK-29 | Arbitrary writable account metas | Impossible / constrained | P0 |
| ATK-30 | Unsupported Whirlpool | HARD REFUSE | P0 |
| ATK-31 | Pool address valid but mints substituted | REFUSE | P0 |
| ATK-32 | Orca vault accounts substituted | REFUSE / CPI cannot move unintended funds | P0 |
| ATK-33 | Tick-array/account substitution changes execution semantics | REFUSE or prove safe exact validation | P0 |
| ATK-34 | Orca oracle/account substitution | REFUSE where applicable | P1 |
| ATK-35 | Incorrect Whirlpool instruction discriminator/layout | REFUSE / test against official interface | P0 |
| ATK-36 | Orca CPI fails after CRESCO validation | Entire transaction rolls back | P0 |
| ATK-37 | Orca CPI succeeds but post-state CRESCO mutation fails | Entire transaction rolls back | P0 |
| ATK-38 | Output less than approved min output | Swap refuses / rolls back | P0 |
| ATK-39 | Price movement between approval and execution | Authorized min-output/deadline constraints remain binding | P1 |
| ATK-40 | Wrong Pyth program | REFUSE | P0 |
| ATK-41 | Wrong Pyth storage | REFUSE | P0 |
| ATK-42 | Wrong instructions sysvar | REFUSE | P0 |
| ATK-43 | Signed message for wrong feed | REFUSE | P0 |
| ATK-44 | Stale Pyth message | REFUSE/UNKNOWN | P0 |
| ATK-45 | Far-future Pyth timestamp | REFUSE | P0 |
| ATK-46 | Confidence too wide | REFUSE | P0 |
| ATK-47 | Unsupported/duplicate payload property ambiguity | REFUSE or deterministic safe parse | P0 |
| ATK-48 | Verified bytes differ from parsed bytes | Impossible; prove equivalence | P0 |
| ATK-49 | Exponent overflow/unsafe scaling | REFUSE | P0 |
| ATK-50 | Integer truncation lowers notional under cap | No material bypass | P0 |
| ATK-51 | Mint decimals exploit allowance rounding tolerance | Only bounded rounding dust | P0 |
| ATK-52 | Token-2022 transfer fee changes received economics | Explicitly supported or refused | P1 |
| ATK-53 | Token-2022 transfer hook introduces unexpected behavior | Explicitly supported or refused | P1 |
| ATK-54 | Frozen/default-state/confidential extension breaks assumptions | Explicitly supported or refused | P1 |
| ATK-55 | Malicious token program supplied | Restrict to intended token programs | P0 |
| ATK-56 | Failed token CPI after validations | Full rollback | P0 |
| ATK-57 | Backend retry after unknown tx outcome | No duplicate logical trade | P0 |
| ATK-58 | Backend/UI renders success before confirmation | PENDING/UNKNOWN, never false success | P0 |
| ATK-59 | Same idempotency key reused for changed action | REFUSE / semantic mismatch | P0 |
| ATK-60 | Receipt points to wrong tx/Mandate/action hash | Verification detects mismatch | P1 |
| ATK-61 | Charter `max_bounded_notional` exceeded | Enforce if authoritative or deprecate truthfully | REVIEW |
| ATK-62 | Program upgrade authority compromised | Operational trust assumption documented/mitigated | TRUST |
| ATK-63 | Guardian key compromised | Authority-root trust assumption documented | TRUST |
| ATK-64 | Orca program/config changes after freeze | Scope delta / revalidation | DEP |
| ATK-65 | Pyth program/config changes after freeze | Scope delta / revalidation | DEP |

## P0 review lanes

### 1. Authority escape
ATK-01 through ATK-25.

### 2. Constrained execution / no arbitrary CPI
ATK-26 through ATK-39.

### 3. Oracle and arithmetic
ATK-40 through ATK-51.

### 4. Token and atomicity
ATK-55 through ATK-59 plus applicable Token-2022 cases.

## Required runtime counter-cases

The final vertical slice should preserve evidence for:
- two in-bound standing swaps;
- soft notional refusal;
- one-use exception grant;
- semantic mutation refusal;
- exact exception success;
- exception replay refusal;
- stale exception refusal after nonce change;
- unsupported program hard-refuse;
- unsupported pool hard-refuse;
- stale/invalid Pyth refusal;
- forced Orca CPI failure and rollback;
- unknown/failed confirmation not rendered as success.

## Review hypotheses

- H-01: baseline Charter bounded cap semantics;
- H-02: exception must not waive non-soft-boundary period policy;
- H-03: TradeAction hash completeness/canonicalization;
- H-04: lifecycle-state consistency;
- H-05: Token-2022 semantics;
- H-06: Pyth verified-bytes/parser equivalence;
- H-07: Orca account-substitution / constrained-CPI escape;
- H-08: slippage/output mutation;
- H-09: arbitrary-CPI regression through helper layers;
- H-10: atomic exception consumption and retry truth.

## Finding taxonomy

Adevar or internal review findings should be classified as:
- CONFIRMED_SECURITY_FINDING
- SEMANTIC_AMBIGUITY_REQUIRING_PRODUCT_OWNER
- DEFENSE_IN_DEPTH
- FALSE_POSITIVE
- OUT_OF_SCOPE
- ACCEPTED_RISK

Security remediation may change implementation. Product-authority semantics require primary-project canonical approval.
