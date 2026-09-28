# Discovery Outreach Log

Status: FIRST_INTERVIEW_SCHEDULING  
Date: 2026-09-27

| Priority | Lane | Target | Contact surface | Status | Sent | Response | Interview | Evidence |
|---|---|---|---|---|---|---|---|---|
| 1 | Agent / Competitor Discovery | Eric Lovold / Sanction | eric@getsanction.com | SCHEDULING | 2026-09-26 · Gmail msg `1a0dcb57aee19742` | 2026-09-27 · Positive response; open to 15-min call | Proposed 2026-09-28 3:00 PM ET or 2026-09-29 11:00 AM ET; reply msg `1a0e8c516fe9a344` | Founder/expert evidence only; Sanction still early |
| 2 | Agent / Exception Shape | Session.money / LazorKit builders | dev-support@lazor.sh (route request) · Telegram @sessionmoney_wallet · X @session_money | SENT_EMAIL_ROUTE_REQUEST | 2026-09-26 · Gmail msg `1a0dcb665d774859` | — | — | — |
| 3 | Treasury | Sean Ganser / Squads | sean@sqds.io | SENT | 2026-09-26 · Gmail msg `1a0dcb6fb33edf82` | — | — | — |
| 4 | Trading | Ellipsis Labs / Phoenix | founders@ellipsislabs.xyz | SENT | 2026-09-26 · Gmail msg `1a0dcb705a1c80f3` | — | — | — |
| 5 | Trading | Ergonia Trading | hr@ergonia.io | SENT | 2026-09-26 · Gmail msg `1a0dd9d9840be3ba` | — | — | — |
| 6 | Trading / Competitor Discovery | Primer Systems / Vault | dev@primer.systems | SENT | 2026-09-26 · Gmail msg `1a0dda01073a93bd` | — | — | — |

## Eric Lovold / Sanction — response note

Eric accepted a 15-minute conversation and explicitly framed what he can provide:
- Sanction is still early;
- he can share design decisions;
- he can share what they are learning through testing;
- he cannot yet claim established user patterns;
- the approval → execution gap is one of the areas they are actively examining.

Interpretation:
- HIGH-VALUE expert/competitor discovery;
- NOT customer validation;
- NOT evidence of willingness to pay;
- NOT evidence that a recurring user workflow is established.

Interview focus:
1. policy change after approval but before grant redemption;
2. one-use grant vs temporary session;
3. attempt vs completion semantics;
4. whether Policy Diff/minimal authority delta matters;
5. whether enforcement should sit at the execution/capital path;
6. what Sanction intentionally does not solve.

## Message purposes

### Sanction
Kill/save the Agent lane by testing:
- one-use grant vs temporary session;
- policy change after approval but before redemption;
- Policy Diff value;
- attempt vs completion semantics;
- missing customer needs.

### Session.money / LazorKit
Run the Exception Shape Test:
- why session instead of exact action;
- common duration/cap/scope;
- policy/security change during active session;
- whether exact-once is ever preferred.

### Squads
Run the Treasury Reconstruction Test:
- last legitimate transaction above Spending Limit;
- Proposal vs Config Transaction;
- whether temporary standing authority is used;
- stale approvals after security/config changes;
- value of explicit exception delta.

### Ellipsis / Phoenix
Run the Trading Reality Gate:
- last legitimate order blocked by risk control;
- exact trade vs temporary risk envelope;
- override latency;
- current OMS/risk-engine adequacy;
- stale-policy semantics;
- value of atomic onchain override + execution.

### Primer Systems
Test:
- what happens when a legitimate trade exceeds a hard per-trade cap;
- exact one-trade exception vs policy edit / temporary envelope;
- why some Vault rules are hard rejects while others escalate.

## Status values

- READY
- SENT
- SENT_EMAIL_ROUTE_REQUEST
- RESPONDED
- TO_SCHEDULE
- SCHEDULED
- INTERVIEWED
- NO_RESPONSE
- DECLINED

## Evidence rule

An outreach being sent or accepted is **not** customer validation.

Only concrete workflow evidence may update:
- REAL_PROBLEM;
- EXCEPTION_SHAPE;
- COMPETITIVE_RESIDUAL;
- PULL;
- CONCEPT_LOCK readiness.
