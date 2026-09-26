# Discovery Target Shortlist

Date: 2026-09-26
Status: outreach candidates — no contact claimed

## Selection rule

Prioritize people who can answer from recent operating behavior, not generic Web3 opinions.

## Agent Builders

### Eric Lovold — Sanction

Why:
Sanction is the closest public semantic overlap found so far: exact retry, one-use grant, human escalation, immutable policy revisions and evidence replay.

Public references:
- https://github.com/ericlovold/sanction
- https://getsanction.com/
- public contact listed in Sanction privacy policy: eric@getsanction.com

Questions:
- Which user requests drove one-use grants instead of temporary sessions?
- How often do escalations occur?
- Do users care about the relationship between the violated rule and the grant, or only the final approval?
- Do policy changes invalidate already approved grants?
- Which fields have caused real GRANT_MISMATCH events?
- What do customers ask for that Sanction intentionally does not solve?

Priority: VERY HIGH — both competitor teardown and expert discovery.

### Session.money / LazorKit ecosystem

Public handles surfaced:
- @session_money
- @0xYann_
- @chaukhac_
- @kay_x64

Why:
They made the opposite product bet: agent requests a bounded session (duration + cap + scope), human approves once, then many actions can execute.

Question:
Why a session instead of exact transaction tickets? What behavior led to that design?

Priority: VERY HIGH — direct Exception Shape Test.

### AgentWallet SDK maintainers / users

Public project:
https://github.com/up2itnow0822/agent-wallet-sdk

Why:
Another explicit model of autonomous spending under caps with escalation above thresholds.

Questions:
- What happens after an above-threshold request is approved?
- Is the approval exact, threshold-based, or a temporary policy change?
- What integration complaints appear most often?

Priority: HIGH.

## Treasury / Crypto Ops

### Squads operators / DAO finance contributors

Why:
Squads is the baseline standing-authority system CRESCO must beat.

Start with:
- teams using Spending Limits for recurring operations;
- DAO finance / operations leads;
- MetaDAO launch teams with public monthly spending-limit configurations.

Public evidence source:
https://github.com/metaDAOproject/programs

Questions:
- last legitimate transaction above the spending limit;
- proposal vs config-change workflow;
- how often temporary increases happen;
- whether an already-approved proposal survives config changes;
- which evidence is required for audit.

Priority: VERY HIGH.

### RaYYeR220 — squads-treasury-skill

Public repo:
https://github.com/RaYYeR220/squads-treasury-skill

Why:
Built explicit tooling around Squads treasury configuration risk and proposal lifecycle. Useful as a technical/operator expert even if not a buyer.

Priority: HIGH.

## Delegated Trading

### Ergonia / Flint Labs

Public evidence:
https://jobs.solana.com/companies/flint-labs/
https://jobs.solana.com/companies/ergonia/

Why:
Crypto-native Solana market-making and exchange teams with explicit risk-system work.

Questions:
- last legitimate order blocked by risk controls;
- exact trade vs temporary risk envelope;
- acceptable approval latency;
- whether overrides happen in humans, code or both;
- stale-policy semantics;
- whether onchain enforcement improves the workflow.

Priority: VERY HIGH.

### Ellipsis Labs / Phoenix ecosystem

Public figures / references:
- Eugene Chen
- Rahul Jain
- https://www.ellipsis.xyz/ / Phoenix ecosystem

Why:
Long-running Solana order-book / market-making experience; strong source for whether delegated-capital exception semantics matter in low-latency environments.

Priority: HIGH.

## Organizational Spend — analogue lane

### Ramp community user pattern

Public thread:
https://community.ramp.com/t/set-a-date-on-temporary-limit-increases/1228

Use as behavioral evidence, not as a person to cold-contact outside the forum without context.

Key signal:
Operators may prefer a temporary envelope with explicit expiry over exact-action authorization.

## Outreach sequencing

1. Sanction / Session.money — fastest way to attack the Agent lane.
2. Squads/MetaDAO treasury operators — validates real boundary workflow.
3. Ergonia/Flint/Ellipsis — validates trading override shape and latency.
4. Corporate-spend analogues — informs exception taxonomy, not necessarily World’s Fair wedge.

## Interview evidence standard

A useful interview must capture:
- one recent concrete event;
- standing policy;
- boundary crossed;
- current workaround;
- exact authority object issued;
- duration/use count;
- approver;
- latency;
- audit evidence;
- policy-change interaction;
- measurable cost/risk;
- whether they would trial a different mechanism.

Do not count:
- “sounds cool”;
- generic security concern;
- TAM commentary;
- willingness-to-pay hypotheticals without workflow evidence.
