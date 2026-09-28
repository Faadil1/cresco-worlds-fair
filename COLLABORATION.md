# Collaboration Guide

## Source of truth

New collaborator? Start with `docs/COLLABORATOR-ONBOARDING.md`.

Read these before changing product direction:

1. `product/PRD.md`
2. `state/CURRENT.yaml`
3. `governance/GATEWAY-REGISTRY.yaml`
4. `governance/PRODUCT-DEPTH-LIVE-REALITY-v1.2.1.md`
5. `governance/REALITY-LEDGER.md`
6. `docs/BASELINE-DELTA.md`
7. `docs/SEMANTIC-TEARDOWN.md`
8. `docs/REALITY-GATE.md`

## Current phase

Pre-Concept-Lock.

Do not build new product features yet.

Allowed work:
- user research;
- competitor teardown;
- evidence collection;
- prototype/mockup solely when needed to test a hypothesis;
- technical feasibility spikes that do not silently establish product scope;
- PRD updates supported by evidence.

## Decision hygiene

For every material decision, record:
- decision;
- evidence;
- alternatives considered;
- why rejected;
- what would falsify the decision;
- date.

## Git / chronology

The Stocklana repository remains historical baseline:
https://github.com/Faadil1/cresco

This repository contains World’s Fair delta work.

Do not squash/rewrite chronology merely to make the story look cleaner.

## Public/private hygiene

Public submission materials should include:
- product truth;
- runtime evidence;
- relevant architecture;
- verified negative events;
- useful research;
- clear limitations.

Do not expose:
- private collaborator handoffs;
- unnecessary internal strategy;
- speculative claims presented as facts;
- credentials/secrets;
- exploratory material that creates judge confusion without adding evidence.

## Canonical rule

**Real failure > fake success.**


## Registry discipline

Every material change must re-evaluate `governance/GATEWAY-REGISTRY.yaml`.

No gate may disappear because it is inconvenient or not yet applicable.

Use only:
- `ACTIVE`
- `N/A`
- `BLOCKED`
- `PROVEN`

A dependent-but-unproven gate is `BLOCKED`, not implied PASS.
