# Ruleset Plugin System

This directory contains the mechanical rules used by the Rules Lawyer agent and the Game Master. The active ruleset is declared in `active-ruleset.md`.

Rulesets are self-contained directories. Swapping systems means pointing `active-ruleset.md` at a different directory.

> **Set your ruleset before Session 1 and leave it alone.** The GM, player agents, and Rules Lawyer all load rules context at the start of every call from `active-ruleset.md`. Changing the ruleset mid-campaign causes agents to operate on inconsistent rule systems within the same session. If you want a different system, start a new campaign.

---

## Two Layers of Rules

### 1. Ruleset (system-level, generic)
The base rules of the game system — action economy, conditions, core class mechanics. These are reusable across any campaign using the same system. Lives in `rules/<system>/`.

### 2. Campaign Extensions (campaign-level, specific)
This campaign's specific annotations on top of the ruleset — exact character stats at current level, active optional rules, and GM clarifications that are specific to this game. Lives in `rules/campaign-extensions.md`.

**Keep them separate.** The ruleset files should be reusable by anyone forking this repo. Campaign-specific details belong only in `campaign-extensions.md`.

---

## Required Files Per Ruleset

Every ruleset directory must contain these files for the Rules Lawyer to function:

| File | Purpose |
|------|---------|
| `system-notes.md` | What this system is, core design philosophy, tone, key mechanical concepts |
| `quickref.md` | Generic mechanical rules: action economy, combat, conditions, core class features |
| `house-rules.md` | GM standing rulings, Rule of Cool policy. Keep generic — campaign-specific rulings go in `campaign-extensions.md` |
| `rulings-log.md` | Running log of every ruling made — accepted corrections and GM overrides |
| `character-template.md` | Template for creating a new PC in this system |

---

## Campaign Extensions File

`rules/campaign-extensions.md` is always injected alongside the ruleset files. It contains:

- **Character sheets (mechanical summary)**: Current stats, HP, spell slots, key ability details with exact numbers — updated when characters level up
- **Active optional rules**: Which optional rules are on or off for this campaign (e.g. flanking, lingering injuries)
- **Party-specific interactions**: Edge cases or ability interactions specific to this party's composition
- **GM clarifications**: Rulings that are specific to this campaign's world or tone

When creating a new campaign from this template, replace `campaign-extensions.md` with one describing your own party.

---

## Included Rulesets

### `srd-5e-2024/` — DnD 5e 2024 (SRD)
The default. Uses the Creative Commons licensed Systems Reference Document for DnD 5e 2024. All content generated with this ruleset is safe to publish publicly.

---

## Adding a New Ruleset

1. Create a new directory: `rules/<system-name>/`
2. Copy `srd-5e-2024/character-template.md` as a starting point and adapt it
3. Write `quickref.md` covering the system's core mechanics — keep it generic, no campaign-specific content
4. Write `system-notes.md` explaining the system's feel and key mechanics
5. Copy the empty `rulings-log.md` and `house-rules.md` stubs
6. Point `active-ruleset.md` at your new directory before starting play

### Notes on Proprietary Systems

If you are using a system you do not have rights to publish (e.g. full DnD 5e beyond the SRD, Daggerheart, Pathfinder), place your ruleset in `rules/private/`. This directory is gitignored and will never be committed or pushed to a public repository.

**Do not publish AI-generated content based on proprietary rules.**

---

## Supported System Types

This architecture works with any tabletop RPG system that has:
- Some form of character statistics
- Some form of action resolution (dice, cards, narrative moves, etc.)
- Some form of turn structure

It has been designed with fifth-edition systems in mind but can accommodate:
- **5e-likes**: Pathfinder, OSR games, Level Up: Advanced 5e
- **PbtA systems**: Dungeon World, Masks, Blades in the Dark
- **Narrative systems**: Daggerheart, Ironsworn, Trophy
- **Anything else**: adapt the quickref and character-template to fit the system's actual mechanics
