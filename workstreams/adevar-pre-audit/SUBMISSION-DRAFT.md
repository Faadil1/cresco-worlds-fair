# CRESCO — Adevar Labs Pre-Audit Submission Draft

Status: PRE-SUBMISSION DRAFT
Date: 2026-10-01

Do not submit until the Colosseum submission prerequisite is actually satisfied and every BLOCKED placeholder is replaced with verified information.

## Project description

CRESCO is an execution-bound delegated capital authority layer for Solana.

For the Crypto World’s Fair vertical, a principal gives a strategy/operator a versioned standing Mandate. The delegate may execute a constrained Orca Whirlpools swap autonomously when it stays inside standing risk limits. If an otherwise valid trade crosses the locked soft per-trade notional boundary, the principal can authorize that exact trade once without permanently widening the Mandate.

Unsupported execution programs, unsupported pools and unparseable action semantics are hard boundaries with no exception path.

The first vertical is intentionally bounded:
- Solana Devnet;
- Orca Whirlpools;
- `SWAP_EXACT_IN`;
- exact one-use exceptional authority;
- Pyth market evidence where required;
- no arbitrary CPI;
- no mainnet or institutional-capital claim.

## Why we want Adevar to review it

CRESCO’s value depends on the authorization boundary being enforced in the same Solana path that can move capital.

The security-critical surface includes:
- principal/delegate signer separation;
- versioned Mandates and nonce invalidation;
- one-use exceptional authority;
- canonical TradeAction semantic binding;
- constrained Orca CPI;
- pool/mint/account validation;
- per-action and period accounting;
- Pyth verification and parsing;
- slippage/min-output and deadline binding;
- replay resistance;
- transaction rollback;
- retry/unknown-outcome handling.

We want an independent pre-audit to challenge the authority model at the execution boundary, not only run generic static analysis.

## Technical complexity and architecture

The existing CRESCO Anchor/Rust core already implements:
- Charter, Mandate and AssetRule state;
- PDA-bound authority;
- a program-controlled demo-token vault;
- standing capital execution;
- one-use exceptions;
- stale nonce and replay refusal;
- Pyth Lazer verification;
- bounded signed-message parsing;
- amount/notional limits and period counters.

The World’s Fair delta adds one explicit canonical trade action:

`TradeActionV0`
- action kind;
- Orca program;
- exact Whirlpool;
- input mint;
- output mint;
- input amount;
- minimum output/slippage floor;
- max notional;
- deadline;
- Mandate nonce.

The program must reconstruct/bind the material action semantics and CPI only into the explicitly supported Orca path. Caller-supplied arbitrary target programs, instruction bytes and account metas are forbidden.

## Security readiness

We have prepared a dedicated security package with:
- bounded pre-audit scope;
- explicit security invariants;
- trust boundaries;
- a 65-case attack/failure matrix;
- high-priority review hypotheses;
- a final audit-readiness checklist.

We intentionally preserve unresolved questions rather than presenting them as already safe.

Current review hypotheses include:
1. baseline Charter-level bounded-notional semantics;
2. exceptional execution vs non-soft-boundary period policy;
3. canonical TradeAction hash completeness;
4. lifecycle consistency under paused/revoked/expired Mandates;
5. Token-2022 extension assumptions;
6. Pyth verified-message/parser equivalence;
7. Orca constrained-CPI account substitution;
8. slippage/min-output mutation;
9. regression into arbitrary CPI through helper layers;
10. atomic exception consumption and retry truth.

These are review targets, not confirmed vulnerabilities.

## Ecosystem impact

CRESCO is testing a reusable Solana pattern: delegated capital authority that sits between two extremes.

It avoids requiring:
- full unrestricted control by the delegate; or
- synchronous principal approval for every action.

The principal can define standing authority, let the delegate operate independently inside it, and approve one exceptional action without automatically creating broader future authority.

If secure, the same pattern can apply beyond the demo to operators, automated strategies and agents that need bounded capital execution.

## Current stage and truth boundary

The product direction is concept-locked and the first World’s Fair live vertical slice is now in build.

The existing CRESCO implementation has Devnet technical proof, but the new TradeActionV0 + Orca path is not yet being represented as complete until it is actually implemented and proven.

We do not claim:
- mainnet deployment;
- institutional adoption;
- production custody;
- brokerage;
- real customer capital;
- validated willingness to pay;
- audited production security.

The remaining operator-validation gap is explicitly preserved.

## Repository / audit target

Current public core:
https://github.com/Faadil1/cresco

Historical preparation baseline:
`0eb10dd8352bba69b9717d0d62d89794c9e384cc`

Final audit commit:
**[BLOCKED — replace with exact frozen TradeActionV0 + Orca implementation commit]**

CRESCO program/network:
**[REVERIFY AT FREEZE]**

Orca program:
`whirLbMiicVdio4qvUfM5KAg6Ct8VwpYzGff3uctyCc`

Final supported pool:
**[REVERIFY AFTER DEVNET RUNTIME VIABILITY CHECK]**

Colosseum submission:
**[BLOCKED — insert official submission URL]**

## Suggested short-form answers

### What are you building?

CRESCO is an execution-bound delegated capital authority layer for Solana. A strategy can execute a constrained Orca swap autonomously inside a versioned standing Mandate. A trade that exceeds the soft per-trade notional boundary can receive exact one-use exceptional authority without widening future standing authority. Unsupported execution semantics hard-refuse.

### Why does it need a security review?

The same program that evaluates authority can cause capital movement, so the security boundary is load-bearing. We want review of signer/account constraints, nonce invalidation, exact-action binding, replay resistance, period/notional accounting, constrained Orca CPI, Pyth verification/parsing, arithmetic, rollback and retry behavior.

### What is technically complex?

The Anchor/Rust system combines PDA-bound authority state, versioned Mandates, a program-controlled vault, standing and one-use exceptional authority, Pyth Lazer verification, notional/freshness/confidence checks, canonical trade semantics and a tightly constrained Orca CPI path. Arbitrary CPI is intentionally forbidden.

### What stage are you at?

The World’s Fair product is concept-locked with an explicit operator-validation gap preserved. The existing CRESCO Devnet authority core is proven, and the first live TradeActionV0 + Orca vertical slice is in build. We will bind the Adevar review to the exact frozen implementation commit.

### What should Adevar focus on?

Authority escalation, stale/replayed authorization, canonical TradeAction binding, exact exception semantics, Orca program/pool/account substitution, slippage/output mutation, Pyth verified-message parsing, integer/rounding edge cases, Token-2022 assumptions, transaction rollback and unknown-outcome retries.

## Required X post draft

Just submitted CRESCO to the @AdevarLabs Security Sidetrack on @superteamearn for @Colosseum’s Crypto World’s Fair Hackathon.

CRESCO is building execution-bound delegated capital authority on Solana: autonomous action inside a standing Mandate, with exact one-use exceptions that do not silently widen future authority.

Our World’s Fair vertical uses a constrained Orca Devnet swap path — no arbitrary CPI — with replay, stale-authority, semantic-mutation and failure boundaries designed to fail closed.

Excited for the chance to have the authority and capital path challenged in a full Pre-Audit.

[FINAL COLOSSEUM / PROJECT LINK]

## Before submission

- confirm the Colosseum submission is complete;
- replace all BLOCKED placeholders;
- bind to exact final commit;
- rerun security/CI proof on that commit;
- verify Orca Devnet pool viability;
- verify CRESCO program/network identity;
- include known limitations and unresolved findings;
- make README/application/runtime claims consistent;
- follow @AdevarLabs;
- publish the required X post;
- submit Superteam manually.

Adevar remains a security workstream and does not redefine the locked Colosseum product.
