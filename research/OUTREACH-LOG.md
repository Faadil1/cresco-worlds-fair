# Discovery Outreach Log

Status: FIRST_WAVE_SENT  
Date: 2026-09-26

| Priority | Lane | Target | Contact surface | Status | Sent | Response | Interview | Evidence |
|---|---|---|---|---|---|---|---|---|
| 1 | Agent | Eric Lovold / Sanction | eric@getsanction.com | SENT | 2026-09-26 · Gmail msg `1a0dcb57aee19742` | — | — | — |
| 2 | Agent / Exception Shape | Session.money / LazorKit builders | dev-support@lazor.sh (route request) · Telegram @sessionmoney_wallet · X @session_money | SENT_EMAIL_ROUTE_REQUEST | 2026-09-26 · Gmail msg `1a0dcb665d774859` | — | — | — |
| 3 | Treasury | Sean Ganser / Squads | sean@sqds.io | SENT | 2026-09-26 · Gmail msg `1a0dcb6fb33edf82` | — | — | — |
| 4 | Trading | Ellipsis Labs / Phoenix | founders@ellipsislabs.xyz | SENT | 2026-09-26 · Gmail msg `1a0dcb705a1c80f3` | — | — | — |
| 5 | Trading | Ergonia Trading | hr@ergonia.io | SENT | 2026-09-26 · Gmail msg `1a0dd9d9840be3ba` | — | — | — |

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

## Status values

- READY
- SENT
- SENT_EMAIL_ROUTE_REQUEST
- RESPONDED
- SCHEDULED
- INTERVIEWED
- NO_RESPONSE
- DECLINED

Do not mark RESPONDED/INTERVIEWED without a real interaction.

## Evidence rule

An outreach being sent is **not** customer validation.

Only concrete workflow evidence from a response/interview may update:
- REAL_PROBLEM;
- EXCEPTION_SHAPE;
- COMPETITIVE_RESIDUAL;
- PULL;
- CONCEPT_LOCK readiness.

| 6 | Trading / Competitor Discovery | Primer Systems / Vault | dev@primer.systems | SENT | 2026-09-26 · Gmail msg `1a0dda01073a93bd` | — | — | — |

### Primer Systems
Purpose:
- test what happens when a legitimate trade exceeds a hard per-trade cap;
- determine whether operators want exact one-trade exception vs policy edit / temporary envelope;
- understand why some Vault rules are hard rejects and others escalate.
