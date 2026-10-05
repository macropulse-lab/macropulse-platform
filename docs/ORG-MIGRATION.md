# Organization migration — runbook

> **Update 2026-10-05:** `IRL-engine-AX` is retired (private). The public engine is now
> [macropulse-lab/irl](https://github.com/macropulse-lab/irl) under FSL-1.1-ALv2, published from the
> private `irl-engine` without history. The record below describes the original migration.


Goal: move all MacroPulse + IRL repos from the personal account `GabrielGauss`
into a GitHub **Organization** so the ecosystem lives at `github.com/<org>/*`
with one profile front door.

## Step 1 — Create the org (you, ~2 min · web only)

GitHub does not allow creating an organization via API on personal plans.

1. Go to **https://github.com/account/organizations/new**
2. Choose the **Free** plan.
3. Organization name: **`macropulse`** (recommended). Contact email: your address.
4. Skip adding members for now. Done.

Then tell Claude the exact org name and it will run Step 2–3.

## Step 2 — Transfer repos (Claude runs, once org exists)

Transfers preserve stars, issues, history, and set up redirects from the old
URLs. Order matters — low-risk first, production-linked last.

**Batch A — safe (no external build hooks):**
`macropulse-platform`, `irl-public-docs`, `irl-sdk-python`, `irl-sdk-ts`,
`irl-verify`, `IRL-engine-AX`, `irl-engine` (private), `macropulse-mcp`

**Batch B — production-linked (need reconnect after transfer):**
- `irl-dashboard` → re-link the Vercel project to the new repo path.
- `macropulse` (private) → **caution**: has a GitHub Actions workflow that
  auto-deploys to the VPS on push, and a linked Vercel project for the
  marketing site. Repo-level Actions secrets travel with the repo, but verify
  the Vercel Git connection and the Actions run after transfer.

Transfer API (per repo):
```
POST /repos/GabrielGauss/<repo>/transfer   { "new_owner": "<org>" }
```

## Step 3 — Post-transfer cleanup (Claude runs)

- Create the org profile: a repo named **`.github`** with `profile/README.md`
  = the hub README (already written in `macropulse-platform/README.md`). This
  renders on `github.com/<org>`.
- Update cross-links that hardcode `GabrielGauss/` → `<org>/` in:
  READMEs, `irl-public-docs`, the marketing site footer, welcome email.
  (GitHub redirects keep old links working, but update for cleanliness.)
- Update local git remotes: `git remote set-url origin https://github.com/<org>/<repo>.git`
- Re-pin the important repos on the org profile.

## What NOT to do

- Don't rename `IRL-engine-AX` and transfer in the same step — do one, verify, then the other.
- Don't transfer `macropulse` during active VPS deploys.
- Don't make the private `irl-engine` public — it contains the L1 compliance
  modules (attestation, evidence, chain, webhook) deliberately withheld from
  the public `IRL-engine-AX` edition.
