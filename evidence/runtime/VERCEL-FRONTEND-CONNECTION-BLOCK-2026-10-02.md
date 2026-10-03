# CRESCO World’s Fair — Vercel Frontend Connection Block

Date: 2026-10-02 local / 2026-10-03 UTC  
Status: **BLOCKED_EXTERNAL_CONNECTION_VISIBILITY**  
Truth state: **OBSERVED**

## Expected frontend project

The product repository documents the frontend as:

- Vercel project name: `cresco`
- production URL: `https://cresco-lac.vercel.app`
- root directory: `apps/web`
- repository: `Faadil1/cresco`

Source:
- `apps/web/README.md` on product main.

## Connector visibility check

Two Vercel connections are currently available in ChatGPT:

1. team `team_twDc66jGM0sPvNM4I5Huc0x7` (`faadil1's projects`)
2. team `team_b8hypzENtczjR7lfxn2y8L6Q` (`faadil's projects`)

Observed:
- direct lookup of project slug `cresco` in team 1 → `404 Project not found`;
- direct lookup of project slug `cresco` in team 2 → `404 Project not found`;
- direct lookup/fetch of `https://cresco-lac.vercel.app/worlds-fair` through both Vercel connections → deployment not found / connector may not have access;
- the currently visible `faadil1's projects` list contains other active projects but not `cresco`;
- the currently visible `faadil's projects` team exposes no projects.

## Interpretation

The frontend code is not the current blocker.

The blocker is that the ChatGPT Vercel connector does not currently expose the Vercel project/team that owns `cresco-lac.vercel.app`.

No replacement project was silently created because doing so could:
- lose the existing production hostname;
- create a parallel deployment with a different origin;
- require a new CORS change/redeploy on the proven Cloudflare Worker;
- weaken runtime/commit binding.

## Required next action

Extend/reconnect Vercel access so the connection includes the project/team that owns:
- project `cresco`;
- domain `cresco-lac.vercel.app`.

Once visible, the intended publication is:
- repository: `Faadil1/cresco`;
- branch: `main`;
- frontend root: `apps/web`;
- publish current World’s Fair route;
- verify `/worlds-fair`;
- execute browser UI→public API→Solana proof.

## Truth boundary

Hosted API→Solana is already proven live.

Judge self-serve remains blocked only by the public browser deployment edge and subsequent clean-room proof.
