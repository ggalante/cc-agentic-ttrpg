# Ruleset Plugin System

This directory contains the mechanical rules used by the Rules Lawyer agent and the Dungeon Master. The active ruleset is declared in `active-ruleset.md`.

Rulesets are self-contained directories. Swapping systems means pointing `active-ruleset.md` at a different directory — nothing else needs to change.

---

## Required Files Per Ruleset

Every ruleset directory must contain these files for the Rules Lawyer to function:

| File | Purpose |
|------|---------|
| `system-notes.md` | What this system is, core design philosophy, tone, key differences from D&D |
| `quickref.md` | Mechanical rules the Rules Lawyer needs: action economy, combat, conditions, spells, key class features |
| `house-rules.md` | DM standing rulings, Rule of Cool policy, and any campaign-specific modifications |
| `rulings-log.md` | Running log of every ruling made — accepted corrections and DM overrides |
| `character-template.md` | How to create a new player character in this system |

---

## Included Rulesets

### `srd-5e-2024/` — DnD 5e 2024 (SRD)
The default. Uses the Creative Commons licensed Systems Reference Document for DnD 5e 2024. All content generated with this ruleset is safe to publish publicly.

---

## Adding a New Ruleset

1. Create a new directory: `rules/<system-name>/`
2. Copy `srd-5e-2024/character-template.md` as a starting point and adapt it
3. Write `quickref.md` covering the system's core mechanics (focus on what comes up in play)
4. Write `system-notes.md` explaining the system's feel and key differences from standard D&D
5. Copy the empty `rulings-log.md` and `house-rules.md` stubs
6. Point `active-ruleset.md` at your new directory

### Notes on Proprietary Systems

If you are using a system you do not have rights to publish (e.g. full DnD 5e beyond the SRD, Daggerheart, Pathfinder), place your ruleset in `rules/private/`. This directory is gitignored and will never be committed or pushed to a public repository.

**Do not publish AI-generated content based on proprietary rules.** The private directory exists precisely so you can play privately without risk.

---

## Switching Systems Mid-Campaign

Switching rulesets mid-campaign requires:

1. Updating `active-ruleset.md` to point at the new directory
2. Rebuilding character sheets using the new system's `character-template.md`
3. Updating `world/current-state.md` to reflect any mechanical changes (HP, conditions, etc.)
4. Noting the switch in the session log

The player journals and narrative files are system-agnostic and carry over unchanged.

---

## Supported System Types

This architecture works with any tabletop RPG system that has:
- Some form of character statistics
- Some form of action resolution (dice, cards, etc.)
- Some form of turn structure

It has been designed with D&D-adjacent systems in mind but can accommodate:
- **D&D-likes**: Pathfinder, OSR games, Level Up: Advanced 5e
- **PbtA systems**: Dungeon World, Masks, Blades in the Dark
- **Narrative systems**: Daggerheart, Ironsworn, Trophy
- **Anything else**: adapt the quickref and character-template to fit the system's actual mechanics
