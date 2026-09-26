# PRE-BUILD REALITY GATE

Status: ACTIVE  
Date: 2026-09-26

## Rule

No candidate direction may become Concept Lock because it sounds technically elegant, maps well to CRESCO’s current code, or is fashionable in the market.

It must pass every required gate with evidence.

## Candidate lanes

### Treasury / Crypto Ops

Working hypothesis:
Teams need a way to handle legitimate actions outside standing treasury authority without silently turning the exception into future standing authority.

Current status:
- Real Problem: PARTIAL
- Real User: PASS category-level
- 5-Year Durability: PASS
- WTP for CRESCO semantics: UNPROVEN
- Killer Demo: STRONG
- Native Advantage: STRONG/PARTIAL
- Negative Event: STRONG category-level
- Competitive Residual: BLOCKED

Must prove:
- recurring legitimate boundary events;
- current workaround;
- exact vs temporary-envelope preference;
- stale-approval semantics;
- why Squads/Safe/Turnkey are insufficient;
- at least 2 users willing to trial.

### Agent Builders

Working hypothesis:
Agents need more than spending caps; they need explicit authority semantics when a legitimate action falls outside normal policy.

Current status:
- Real Problem: PASS category-level
- Real User: PASS
- 5-Year Durability: PASS
- WTP for CRESCO semantics: UNPROVEN
- Killer Demo: STRONG
- Native Advantage: STRONG
- Negative Event: STRONG category-level
- Competitive Residual: BLOCKED by Turnkey/SDP/Session/etc.

Must prove:
- real boundary events;
- actions that are “under cap but wrong”;
- escalation latency tolerance;
- exact vs scoped-session preference;
- existing workaround pain;
- at least 2 builders willing to integrate/test.

### Delegated Trading

Working hypothesis:
Trading systems need bounded delegated capital plus explicit, policy-aware override semantics for exceptional trades.

Current status:
- Real Problem: PASS category-level
- Real User: PASS
- 5-Year Durability: PASS
- WTP: SUPPORTED category-level
- Killer Demo: VERY STRONG
- Native Advantage: VERY STRONG
- Negative Event: SUPPORTED
- Competitive Residual: UNPROVEN

Must prove:
- recurring legitimate trades blocked by risk limits;
- current override behavior;
- latency tolerance;
- exact trade vs temporary risk envelope;
- current OMS/risk-engine sufficiency;
- at least 2 operators willing to test.

### Family Progressive Agency

Working hypothesis:
Families prefer durable standing autonomy plus rare explicit exceptions over either per-action approval or broad child control.

Current status:
- Real Problem: PLAUSIBLE
- Real User: PASS
- 5-Year Durability: PASS
- WTP for CRESCO semantics: UNPROVEN
- Killer Demo: EXCELLENT
- Native Advantage: WEAK/PARTIAL
- Negative Event: PARTIAL category-level
- Competitive Residual: PARTIAL

Must prove:
- parents experience approval fatigue / precedent creep;
- exact exception is preferable to temporary limit change;
- decision lattice does not collapse to yes/no;
- child-controlled signer is acceptable;
- product can avoid securities/custody traps.

## Universal interview rule

Ask about **past behavior first**.

Do not lead with CRESCO.

Primary prompt:

> Tell me about the last time a legitimate action hit a spending, risk, permission, or approval boundary. What happened next?

Then reconstruct:
- standing rule;
- requested action;
- why it was legitimate;
- who decided;
- what new authority was issued;
- whether that authority remained afterward;
- whether it was reverted;
- whether the action changed between approval and execution;
- how long approval took;
- what failure would have cost.

Only after understanding the workflow should CRESCO concepts be shown.

## Exception Shape Classification

Classify every observed real exception:

A. DECLINE — no new authority.  
B. EXACT ACTION — one specific action.  
C. PARAMETRIC TEMPORARY — bounded envelope for a short context.  
D. SCOPED SESSION — repeated actions inside temporary scope.  
E. PERMANENT EVOLUTION — standing policy changes.  
F. FULL CO-SIGN — principal jointly authorizes the action.

The distribution of real events across these classes determines the product.

## Decision-Lattice Test

Test whether users really need:

```
DECLINE
EXCEPTION
EVOLVE
```

or whether actual behavior collapses to:
- approve / deny;
- session / deny;
- widen / deny.

## Stale-Policy Test

Ask:

> An exception was approved under policy v7. Before execution, the standing policy changed to v8. Should the old exception still execute?

Record why.

Possible semantics:
- always stale;
- survives only if v8 is broader;
- survives if unrelated fields changed;
- must be re-evaluated against v8;
- principal explicitly chooses at issuance.

Do not pick one before user/domain evidence.

## Promotion threshold

A lane can be proposed for Concept Lock only when:
- multiple users independently report the boundary problem;
- workaround pain is measurable;
- exception shape is understood;
- stale-policy semantics are understood;
- incumbent residual is explicit;
- native advantage is tangible;
- at least two credible users want to test;
- one concrete negative event maps causally to the product;
- the killer demo is honest and provable.

Until then:

**BUILD_AUTHORIZED = FALSE**
