# CRESCO — World’s Fair Security Acceptance Test Plan

Date: 2026-10-01
Status: READY_TO_APPLY_WHEN_IMPLEMENTATION_LANDS
Workstream: ADEVAR_PRE_AUDIT

## Rule

These tests are mandatory security acceptance checks for the locked `TradeActionV0 + Orca` vertical.

They must run against the exact implementation commit that will be bound to the Adevar audit scope.

Passing baseline transfer tests does not satisfy these tests.

## A. Canonical TradeAction binding

### SEC-A01 — canonical serialization determinism
Construct the same TradeAction through two code paths.
Expected:
- identical canonical bytes;
- identical action hash.

### SEC-A02 — action-kind mutation
Authorize `SWAP_EXACT_IN`, mutate action kind.
Expected: REFUSE.

### SEC-A03 — venue mutation
Authorize Orca program, substitute another program ID.
Expected: HARD REFUSE, no exception path.

### SEC-A04 — pool mutation
Authorize selected Whirlpool, substitute another valid Orca pool.
Expected: HARD REFUSE or exact-action mismatch.

### SEC-A05 — input mint mutation
Change devUSDC input mint.
Expected: REFUSE.

### SEC-A06 — output mint mutation
Change devUSDT output mint.
Expected: REFUSE.

### SEC-A07 — amount increase
Increase input amount after approval.
Expected: REFUSE.

### SEC-A08 — amount decrease
Decrease input amount materially after exact approval.
Expected: REFUSE unless the locked semantics explicitly permit a bounded range.

### SEC-A09 — min-output weakening
Lower `min_output_amount` after approval.
Expected: REFUSE.

### SEC-A10 — min-output strengthening
Raise `min_output_amount`.
Expected:
- either REFUSE under exact-action semantics;
- or explicitly documented safe narrowing if primary canon chooses that rule.
No silent behavior.

### SEC-A11 — deadline extension
Move deadline later.
Expected: REFUSE.

### SEC-A12 — deadline expired
Execute after deadline.
Expected: REFUSE.

### SEC-A13 — nonce mutation
Issue exception, then advance Mandate nonce.
Expected: REFUSE stale exception.

## B. Standing vs exceptional policy

### SEC-B01 — in-bound standing trade
Trade under per-action and period limits.
Expected: ALLOW without principal approval.

### SEC-B02 — soft per-action boundary
Trade exceeds only per-action notional.
Expected:
- standing path REFUSE;
- exception route available.

### SEC-B03 — valid exact exception
Grant one-use exception for SEC-B02 exact trade.
Expected:
- execution succeeds;
- exception consumed;
- standing policy unchanged.

### SEC-B04 — replay
Replay SEC-B03.
Expected: REFUSE.

### SEC-B05 — period cap remains hard under exception
Set remaining period capacity below exceptional trade while per-action exception is valid.
Expected: REFUSE unless primary canon explicitly changes period semantics.

This is the regression test for baseline H-02.

### SEC-B06 — unsupported program remains hard
Unsupported program + otherwise acceptable notional.
Expected: HARD REFUSE, no exception route.

### SEC-B07 — unsupported pool remains hard
Unsupported pool + otherwise acceptable semantics.
Expected: HARD REFUSE, no exception route.

## C. Orca constrained-CPI integrity

### SEC-C01 — exact program ID
Pass wrong executable program account.
Expected: REFUSE before CPI.

### SEC-C02 — exact Whirlpool
Pass another valid Orca Whirlpool.
Expected: REFUSE.

### SEC-C03 — pool/mint mismatch
Use selected pool but substituted token mint/account.
Expected: REFUSE.

### SEC-C04 — token vault substitution
Replace Orca/CRESCO token vault account with attacker-controlled or wrong vault.
Expected: REFUSE or CPI incapable of unintended transfer.

### SEC-C05 — tick-array substitution
Supply tick arrays unrelated to the selected Whirlpool/current swap.
Expected: REFUSE or Orca validation + CRESCO constraints prevent semantic escape.

### SEC-C06 — arbitrary writable account injection
Attempt to add/swap caller-controlled writable accounts that alter execution effect.
Expected: impossible or REFUSE.

### SEC-C07 — arbitrary instruction payload
Attempt caller-controlled raw Orca instruction bytes.
Expected: impossible; CRESCO constructs the instruction from validated fields.

### SEC-C08 — wrong token program
Supply Token-2022 for the canonical devUSDC/devUSDT path.
Expected: REFUSE.

### SEC-C09 — exact canonical mint program
Use official legacy Token program for both selected mints.
Expected: pass only if all other conditions hold.

## D. Pyth and arithmetic

### SEC-D01 — correct feed
Expected: pass when fresh/confident and policy permits.

### SEC-D02 — wrong feed
Expected: REFUSE.

### SEC-D03 — stale evidence
Expected: REFUSE/UNKNOWN.

### SEC-D04 — future timestamp
Expected: REFUSE.

### SEC-D05 — confidence too wide
Expected: REFUSE.

### SEC-D06 — unsupported exponent
Expected: REFUSE.

### SEC-D07 — notional rounding boundary below limit
Expected: deterministic intended classification.

### SEC-D08 — notional rounding boundary above limit
Expected: REFUSE; no truncation bypass.

### SEC-D09 — max u64 arithmetic edge
Expected: overflow-safe REFUSE.

## E. Failure atomicity

### SEC-E01 — forced Orca failure before swap mutation
Expected:
- no CRESCO counters changed;
- exception unused;
- no success receipt.

### SEC-E02 — forced slippage failure
Expected full transaction rollback.

### SEC-E03 — forced token transfer/CPI failure
Expected full rollback.

### SEC-E04 — forced Pyth verification failure
Expected no swap, no counters, no allowance consumption.

### SEC-E05 — post-CPI CRESCO failure
Intentionally trigger a CRESCO error after CPI if safely testable in local/test harness.
Expected full Solana transaction rollback including Orca state.

This test is especially important to prove the atomicity claim rather than infer it.

## F. Lifecycle

### SEC-F01 — paused Mandate
Expected capital execution REFUSE.

### SEC-F02 — revoked Mandate
Expected execution REFUSE and no reactivation.

### SEC-F03 — expired Mandate
Expected execution REFUSE.

### SEC-F04 — exception grant while paused
Expected product-owner-defined fail-closed semantics; recommended REFUSE for v1.

### SEC-F05 — stage/policy transition while revoked
Expected no security-relevant widening. Semantics must be explicit.

## G. Retry and outcome truth

### SEC-G01 — duplicate request/idempotency
Submit the same logical action twice.
Expected at most one successful one-use execution.

### SEC-G02 — unknown confirmation then retry
Simulate submitted transaction with unknown client confirmation.
Expected:
- query/reconcile chain state before resubmission;
- no blind duplicate execution.

### SEC-G03 — success rendering
UI/API receives no confirmed signature/final state.
Expected: PENDING or UNKNOWN, never confirmed success.

### SEC-G04 — receipt mismatch
Attach a receipt from another action/Mandate/tx.
Expected verifier rejects mismatch.

## H. Baseline regression checks

### SEC-H01 — max_bounded_notional disposition
If field remains authoritative, add direct enforcement test.
If deprecated, ensure no UI/API/security docs represent it as enforced.

### SEC-H02 — request-hash regression
Final TradeAction authorization must not rely on a caller-supplied opaque hash alone.

Expected:
- runtime fields are canonically encoded/reconstructed;
- mutation tests A02–A13 prove binding.

## Evidence packet per test

For every material test record:
- commit SHA;
- program ID/network;
- test ID;
- input action fields;
- Mandate version/nonce;
- exception ID/hash if any;
- expected outcome;
- observed outcome;
- transaction signature or local validator receipt;
- relevant logs/error code;
- before/after balances/counters;
- exception used state;
- dependency identities;
- timestamp.

## Promotion condition

The World’s Fair implementation is not security-ready for Adevar freeze until:
- every P0 test is PASS or explicitly accepted/documented;
- H-02 and H-03 baseline regressions are demonstrably closed;
- H-07 through H-10 have concrete runtime evidence;
- no arbitrary CPI path exists;
- known unresolved material findings remain disclosed.
