# CRESCO — Orca Dependency Verification for Adevar

Date: 2026-10-01
Status: VERIFIED_FOR_PREAUDIT_PREPARATION
Purpose: External dependency verification for the locked World’s Fair v1 adapter

## Sources checked

Official Orca repositories/documentation:
- https://github.com/orca-so/whirlpools
- https://github.com/orca-so/whirlpools-sdk-tutorial-kit
- https://github.com/orca-so/whirlpools-cpi-examples

## Program identity

Official Orca Whirlpools program:
`whirLbMiicVdio4qvUfM5KAg6Ct8VwpYzGff3uctyCc`

The current official Orca repository states that this program is deployed on:
- Solana Mainnet
- Solana Devnet

The repository also states that the deployment is verifiable-build backed.

### CRESCO implication

World’s Fair v1 must hard-bind the expected Orca program ID. No arbitrary caller-selected CPI target is allowed.

## Selected Devnet pool

Primary locked candidate:
- pair: devUSDC / devUSDT
- tick spacing: 1
- Whirlpool: `63cMwvN8eoaD39os9bKP8brmA7Xtov9VxahnPufWCSdg`

The official Orca tutorial kit currently lists this exact Devnet pool.

### Tokens

devUSDC:
- mint: `BRjpCHtyQLNCo8gqRUr8jtdAj5AjPYQaoqbvcZiHok1k`
- decimals: 6
- token program: legacy Token
- listed extensions: none

devUSDT:
- mint: `H8UekPGwePSmQ3ttuYGPU1szyFfjZR4N53rymSFwpLPm`
- decimals: 6
- token program: legacy Token
- listed extensions: none

### Security implication

For the initial locked pair, Token-2022 extension behavior does not need to be load-bearing.

The safest v1 rule is therefore:
- exact input mint = devUSDC;
- exact output mint = devUSDT for the canonical direction under test;
- exact legacy SPL Token program;
- reject unexpected Token-2022 mints/programs/extensions in the v1 path.

This narrows H-05 from a generic interface risk into a concrete enforcement requirement.

## Compatibility

Current CRESCO baseline:
- Anchor: 0.32.1
- Solana: 2.3.0

Current Orca main repository:
- Anchor: 0.32.1
- Solana requirement documented around 2.1.0

This is favorable at the Anchor interface level, but runtime/build compatibility still requires actual integration tests.

## CPI example caveat

The current Orca CPI examples repository exposes examples for:
- Anchor 0.29.0
- Anchor 0.30.1
- Anchor 0.31.1

It does not currently advertise a dedicated 0.32.1 example in the README checked for this review.

### Security implication

Do not blindly copy an older CPI example and assume account/instruction parity.

The World’s Fair build should:
1. derive the actual instruction/accounts from the current official Orca program/client definitions;
2. pin dependency versions;
3. test against the real Devnet program;
4. verify exact account ownership, PDA and mint relationships;
5. preserve no-arbitrary-CPI constraints.

## Runtime viability still required

Static/source verification does not prove:
- current pool liquidity;
- current tick-array availability for the desired swap;
- sufficient dev token funding;
- deterministic transaction success at demo time;
- current RPC reliability.

Therefore:
`POOL_IDENTITY = VERIFIED`
but
`LIVE_SWAP_VIABILITY = BLOCKED_UNTIL_RUNTIME_TEST`.

## Adevar relevance

This dependency verification should be included in the pre-audit package because it:
- narrows supported token semantics;
- gives the auditor exact external program/pool/mints;
- prevents an overly broad Token-2022 threat model from obscuring the actual v1 path;
- exposes the remaining runtime/CPI-version integration risks honestly.
