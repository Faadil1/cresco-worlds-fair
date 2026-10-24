# CRESCO — Security Invariants

Status: ACTIVE DRAFT
Date: 2026-10-01
Workstream: ADEVAR_PRE_AUDIT

These properties are audit targets. They are not claims that every property has already been formally proven.

## A. Authority

**INV-A01 — Guardian-only widening**  
Only the bound principal/guardian may increase standing authority or grant exceptional authority.

**INV-A02 — Delegate cannot self-widen**  
The delegate may consume valid authority but cannot create or enlarge it.

**INV-A03 — Proposal is not authority**  
A request, proposal, Policy Diff, UI state or backend record cannot authorize execution by itself.

**INV-A04 — Evidence is not authority**  
Pyth data, P&L, learning, model scores or review evidence may restrict or inform policy, never widen authority automatically.

**INV-A05 — Unsupported semantics are hard-refuse**  
Unsupported program, pool, action type or unparseable trade semantics expose no exception route.

## B. Mandate lifecycle

**INV-M01 — Nonce freshness**  
Security-sensitive authorization and execution must match the current Mandate nonce.

**INV-M02 — Stale exception invalidation**  
Any v1 Mandate nonce/version change invalidates previously issued exceptional authority.

**INV-M03 — Monotonic lineage**  
Standing policy changes advance lineage; old lineage cannot silently reactivate.

**INV-M04 — Revocation fail-closed**  
Revoked authority cannot execute or be silently reactivated.

**INV-M05 — Pause fail-closed**  
Paused authority cannot execute capital paths.

**INV-M06 — Expiry uses trusted time**  
Expired Mandates or actions refuse using Solana-trusted time semantics.

## C. TradeActionV0 semantic integrity

**INV-T01 — One canonical encoding**  
The same deterministic encoding defines the authorized action everywhere security depends on the action hash.

**INV-T02 — Action kind bound**  
`SWAP_EXACT_IN` cannot mutate into another action type.

**INV-T03 — Venue bound**  
The authorization binds the exact supported Orca program.

**INV-T04 — Pool bound**  
The authorization binds the exact supported Whirlpool.

**INV-T05 — Pair bound**  
Input and output mints are both bound.

**INV-T06 — Input amount bound**  
The approved input quantity cannot increase or materially change.

**INV-T07 — Output/slippage bound**  
The principal-approved `min_output_amount` cannot be weakened after approval.

**INV-T08 — Deadline bound**  
The approved deadline is immutable and enforced.

**INV-T09 — Nonce bound**  
The action binds the source Mandate nonce.

**INV-T10 — No opaque caller semantics**  
Arbitrary bytes, arbitrary account lists or opaque caller labels cannot substitute for on-chain reconstructed semantics.

## D. Standing policy

**INV-S01 — Per-action limit**  
Standing execution cannot exceed the current per-action notional policy.

**INV-S02 — Period limit**  
Standing execution cannot exceed current period policy.

**INV-S03 — Exception is narrow**  
The v1 exception may override only the locked soft boundary for the exact trade; it does not silently waive unrelated policy dimensions.

**INV-S04 — Counters remain authoritative**  
Exceptional execution updates the relevant period counters while leaving standing limits unchanged.

**INV-S05 — Standing Mandate unchanged after one-use exception**  
A successful exception does not permanently widen policy.

**INV-S06 — Disabled/unsupported rule refuses**  
Disabled rule or unsupported action mask cannot execute.

## E. Exceptional authority

**INV-E01 — Principal grant only**  
Only the principal can create the exceptional authorization.

**INV-E02 — Same delegate**  
The exception cannot be consumed by a different delegate.

**INV-E03 — Same semantic trade**  
Any meaningful mutation of the authorized TradeAction refuses.

**INV-E04 — Same lineage**  
The exception is usable only under its source Mandate nonce.

**INV-E05 — Unexpired**  
Expired exceptional authority refuses.

**INV-E06 — Exactly one success**  
At most one successful capital execution may consume a one-use exception.

**INV-E07 — Replay refuses**  
A consumed exception cannot move capital again.

**INV-E08 — Failed venue/oracle/token execution is not consumption**  
A reverted transaction cannot leave the exception consumed or counters advanced.

## F. Orca adapter

**INV-O01 — Exact supported program**  
CPI target must equal the locked Orca Whirlpools program ID.

**INV-O02 — Supported pool only**  
Only explicitly supported pool configuration may execute.

**INV-O03 — Mint/pool consistency**  
Input/output mint accounts must match the supported pool semantics.

**INV-O04 — No arbitrary CPI**  
Caller cannot supply arbitrary target program, arbitrary instruction bytes or arbitrary account metas.

**INV-O05 — Required Orca accounts constrained**  
All economically meaningful pool/vault/tick-array/oracle accounts are validated as required by the selected Orca instruction.

**INV-O06 — Output protection survives CPI construction**  
The executed swap preserves the exact authorized minimum-output/slippage constraint.

**INV-O07 — CPI failure rolls back**  
Any Orca failure leaves CRESCO authority/counters/exception state unmodified.

## G. Oracle / Pyth

**INV-P01 — Expected verifier**  
Pyth CPI uses the expected trusted program/storage identities.

**INV-P02 — Verified bytes equal parsed bytes**  
The message CRESCO parses is the message whose authenticity was verified.

**INV-P03 — Feed bound**  
Evidence corresponds to the expected feed.

**INV-P04 — Freshness bound**  
Stale evidence refuses.

**INV-P05 — Future timestamp bound**  
Unreasonably future evidence refuses.

**INV-P06 — Confidence bound**  
Confidence wider than allowed refuses.

**INV-P07 — Price validity**  
Missing, zero or negative price refuses.

**INV-P08 — Safe exponent/math**  
Unsupported exponent or arithmetic overflow refuses.

**INV-P09 — Market evidence never grants authority**  
Pyth may restrict/refuse but cannot widen human authority.

## H. Capital/account integrity

**INV-C01 — Program-controlled vault**  
Capital leaves only through the intended CRESCO-authorized path.

**INV-C02 — Destination integrity**  
Assets cannot be redirected to an unauthorized destination.

**INV-C03 — Amount integrity**  
Capital movement matches the amount/notional that passed authorization.

**INV-C04 — Arithmetic fail-closed**  
Overflow/truncation/rounding cannot create an authorization bypass.

**INV-C05 — Token semantics supported explicitly**  
If Token-2022 extensions alter transfer economics or callbacks, they are intentionally supported or rejected.

## I. Outcome truth and retry

**INV-R01 — Transaction atomicity**  
Failed Solana execution leaves no partial authority/accounting state.

**INV-R02 — Retry safety**  
Unknown/retried off-chain submissions cannot create duplicate logical execution.

**INV-R03 — UNKNOWN is not confirmed success**  
UI/API must not display success without sufficient confirmation.

**INV-R04 — Receipt identity**  
Receipts bind to the correct action hash, Mandate, nonce, exception, venue, transaction and runtime.

## J. Unresolved baseline field

**INV-X01 — Charter `max_bounded_notional` semantics**  
The baseline stores this field but existing source review did not identify downstream enforcement. Final code must either:
- define and enforce it;
- remove/deprecate it truthfully;
- or document why it is non-authoritative.

The Adevar workstream may expose this ambiguity but cannot silently decide product semantics.

## Review classification

Each invariant must eventually be labeled:
- PROVEN_BY_TEST
- PROVEN_BY_CODE_REVIEW
- PROVEN_BY_RUNTIME
- PARTIAL
- UNKNOWN
- INTENTIONALLY_NOT_APPLICABLE

A passing demo is not sufficient to upgrade an invariant.
