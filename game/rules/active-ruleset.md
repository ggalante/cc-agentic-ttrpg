# Active Ruleset Configuration

_Read by the Rules Lawyer agent and the GM at the start of every session._

> **Configure before your first session. Do not change this file mid-campaign.**
> The agents — GM, players, and Rules Lawyer — all load their mechanical context from this file at the start of each call. Changing the ruleset mid-campaign will cause agents to operate on different rule systems across the same session, producing inconsistent and confusing results. If you want to try a different system, start a new campaign.

---

## Current Ruleset

**Name**: DnD 5e 2024 (SRD — Systems Reference Document)
**Directory**: `rules/srd-5e-2024/`
**Legal status**: Creative Commons CC BY 4.0. Content generated using this ruleset is safe to publish.
**Description**: The open-license subset of DnD 5e 2024. All core mechanics are included. Proprietary subclasses, spells beyond the SRD list, and setting-specific content are excluded. All characters in this campaign use SRD-compatible options.

## Campaign Extensions

**File**: `rules/campaign-extensions.md`
**Purpose**: Campaign-specific rules annotations — exact stats for this party's characters, active optional rules, and any clarifications specific to this game. Injected alongside the ruleset files. Does not override the base ruleset; adds specificity on top of it.

---

## Available Rulesets in This Repository

| Directory | System | Legal Status |
|-----------|--------|--------------|
| `rules/srd-5e-2024/` | DnD 5e 2024 SRD | ✓ CC BY 4.0 — safe to publish |
| `rules/private/` | Your private rulesets | Gitignored — never committed |

To add a new ruleset, create a directory under `rules/` containing the files described in `rules/README.md`.
