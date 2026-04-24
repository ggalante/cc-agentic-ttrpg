# cc-dnd — Multi-Agent DnD with Claude

A fully AI-driven tabletop RPG campaign using Claude subagents. The main Claude agent acts as Dungeon Master. Four player character subagents make autonomous decisions based on their characters' personalities. A Rules Lawyer subagent reviews mechanical correctness after each combat round. All game state lives in markdown files, versioned in git.

This repository contains an active campaign set in **Aldenmere** — a post-adventure fantasy world where the danger is slowly returning after 50 years of peace. Fork it to run your own game.

---

## How It Works

```
Dungeon Master (main agent)
    │
    ├─── spawns ──► Player: Reginald (Paladin)
    ├─── spawns ──► Player: Zyx (Wizard)
    ├─── spawns ──► Player: Midge (Rogue)
    ├─── spawns ──► Player: Grunka (Barbarian)
    │
    └─── spawns ──► Rules Lawyer (advisory, combat rounds only)
```

- **Player agents** are stateless — all memory lives in markdown files injected into each call
- **Inter-player dialogue** is relayed by the DM; players build opinions of each other through their journals
- **Rules Lawyer** reviews the full combat round as a batch after all players declare; DM accepts or overrules
- **Everything is committed to git** — every session, every ruling, every character memory update

Full architecture details: [`dnd/meta/architecture.md`](dnd/meta/architecture.md)

---

## Fork and Run Your Own Game

### 1. Fork This Repository

Fork on GitHub. Clone your fork locally. The campaign files in `dnd/` are the starting point — you can keep Aldenmere and the existing characters, or replace them entirely.

### 2. Create Your Characters

Copy [`dnd/rules/srd-5e-2024/character-template.md`](dnd/rules/srd-5e-2024/character-template.md) for each player character. Fill in every section — the personality and speech pattern sections are the most important. They drive how the player agent behaves.

Save each character to `dnd/characters/<name>.md` and create a matching starter journal at `dnd/memory/<name>-journal.md`.

Aim for **four characters with contrasting personalities** — the friction between them is where the fun comes from.

### 3. Build Your World

Edit or replace:
- [`dnd/world/lore.md`](dnd/world/lore.md) — history, factions, the Big Threat
- [`dnd/world/current-state.md`](dnd/world/current-state.md) — where the party is and what's happening right now
- [`dnd/world/story-so-far.md`](dnd/world/story-so-far.md) — running narrative summary (starts empty)

### 4. Choose Your Ruleset

The default ruleset is **DnD 5e 2024 (SRD)** — the Creative Commons-licensed subset of the rules. Content generated using it is safe to publish.

To use a different system:

1. Edit [`dnd/rules/active-ruleset.md`](dnd/rules/active-ruleset.md) to point at your ruleset directory
2. Create the ruleset directory with the required files (see [`dnd/rules/README.md`](dnd/rules/README.md))
3. Update character sheets to match the new system

**Proprietary systems** (full DnD 5e beyond SRD, Daggerheart, Pathfinder, etc.): place your ruleset in `dnd/rules/private/`. This directory is gitignored and will never be committed. Do not publish AI-generated content based on proprietary rules.

### 5. Start the Game

Open a Claude Code session in your forked repository and say:

> "Start Session 1."

The DM agent will read the world state, spawn player agents with their character context, and begin narrating. No further input needed — watch the party make their own decisions.

---

## Ruleset Options

| System | Status | Notes |
|--------|--------|-------|
| DnD 5e 2024 (SRD) | ✓ Included, default | CC BY 4.0 — safe to publish |
| DnD 5e 2024 (full) | Private only | Place in `rules/private/` |
| DnD 5e 2014 | Private only | Largely compatible with 2024 SRD mechanics |
| Daggerheart | Private only | Requires new quickref and character template |
| Dungeon World | Private only | PbtA — requires new quickref and character template |
| Pathfinder 2e | Private only | Requires new quickref and character template |
| Other | Private only | See `rules/README.md` for what a ruleset needs |

Adding a new system means writing five files in a new directory. See [`dnd/rules/README.md`](dnd/rules/README.md) for the spec.

---

## File Structure

```
dnd/
  meta/
    architecture.md        ← Full system design and agent flow
    rules-lawyer.md        ← Rules Lawyer agent profile
  world/
    lore.md                ← World history, factions, the Big Threat
    current-state.md       ← Live game state (location, HP, active quests)
    story-so-far.md        ← Cumulative narrative summary
  characters/
    <name>.md              ← One file per PC: stats, personality, backstory
  memory/
    <name>-journal.md      ← One journal per PC: memories, opinions, goals
  rules/
    README.md              ← Ruleset plugin spec
    active-ruleset.md      ← Which ruleset is active
    srd-5e-2024/           ← Default ruleset (DnD 5e 2024 SRD)
    private/               ← Gitignored — proprietary rulesets go here
  sessions/
    session-NN.md          ← Full log of each session
```

---

## Legal Notes

**Default ruleset (SRD)**: The `dnd/rules/srd-5e-2024/` ruleset is based on the [Systems Reference Document 5.2](https://www.dndbeyond.com/srd) licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Session logs and content generated using this ruleset may be published freely.

**Proprietary rulesets**: If you use a proprietary system via `rules/private/`, do not publish AI-generated content based on it. The gitignore on that directory is a safeguard, not a license.

**This repository's campaign content** (Aldenmere, the four characters, the story): original creative work, not derived from any proprietary source.

---

## Contributing

Issues and PRs welcome for improvements to the architecture, agent prompting strategies, or the ruleset plugin system. Campaign-specific content (characters, world lore) is specific to this playthrough and not expected to generalize.
