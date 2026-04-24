# Multi-Agent Tabletop RPG Engine

Run a tabletop RPG campaign where AI agents play the characters. The Game Master, each player character, and a Rules Lawyer are all separate agents that communicate through a shared set of markdown files. Everything is versioned in git.

Works with Claude Code, the Claude API, or any multi-agent AI system that supports tool use and spawning subagents (Gemini, GPT-4o with function calling, etc.). The markdown files are the universal state layer — any LLM can read them.

This repository contains an active campaign: **Aldenmere**, a post-adventure fantasy world where the danger is returning after 50 years of peace, played with four AI-driven characters using DnD 5e 2024 (SRD).

---

## Quick Start

**Fork this repo, then:**

1. **Delete or replace the campaign files** in `game/characters/`, `game/memory/`, and `game/world/` with your own, using the templates in `game/rules/srd-5e-2024/character-template.md` and the existing world files as a guide.

2. **Choose your ruleset** by editing `game/rules/active-ruleset.md`. The default is DnD 5e 2024 SRD (safe to publish). For other systems, see [Changing the Ruleset](#changing-the-ruleset).

3. **Fill in `game/rules/campaign-extensions.md`** with your party's character stats. This is what the Rules Lawyer uses to check mechanical correctness — keep it updated as characters level up.

4. **Commit everything** to git before starting. The agents read from the files on disk.

5. **Start the game.** Open a Claude Code session and say: `Start Session 1.`

The GM agent reads the world state, spawns player agents with their character context, and begins narrating. No further input needed.

For a full setup walkthrough, see [`game/meta/architecture.md`](game/meta/architecture.md).

---

## How It Works

```
Game Master (orchestrating agent)
    │
    ├── spawns ──► Player agent (reads character file + memory journal)
    ├── spawns ──► Player agent
    ├── spawns ──► Player agent
    ├── spawns ──► Player agent
    │
    └── spawns ──► Rules Lawyer (after each combat round, advisory only)
```

- **Player agents are stateless** — all memory lives in markdown files injected into each call
- **Journals accumulate** — each player's `memory/<name>-journal.md` grows with opinions, memories, and emotional state across sessions, giving agents continuity of character
- **Inter-player dialogue** is relayed by the GM; players build relationships through their journals
- **Rules Lawyer** reviews the full combat round as a batch; GM accepts or overrules — the GM always has final say
- **Everything is committed to git** — sessions, rulings, character memories, world state

---

## File Structure

```
game/
  meta/
    architecture.md        ← Full system design, agent flow, context injection
    rules-lawyer.md        ← Rules Lawyer agent profile
  world/
    lore.md                ← World history, factions, the Big Threat
    current-state.md       ← Live game state (location, HP, active quests)
    story-so-far.md        ← Cumulative narrative summary (updated each session)
  characters/
    <name>.md              ← One file per PC: stats, personality, backstory
  memory/
    <name>-journal.md      ← One journal per PC: memories, opinions, goals
  rules/
    README.md              ← Ruleset plugin spec and campaign-extensions guide
    active-ruleset.md      ← Which ruleset is active (configure before Session 1)
    campaign-extensions.md ← This campaign's character stats and specific annotations
    srd-5e-2024/           ← Default ruleset (DnD 5e 2024 SRD)
    private/               ← Gitignored — proprietary rulesets go here
  sessions/
    session-NN.md          ← Full log of each session
```

---

## Changing the Ruleset

The ruleset is a plugin. To switch systems:

1. Edit `game/rules/active-ruleset.md` to point at a new ruleset directory
2. Create the directory with the required files (see `game/rules/README.md` for the spec)
3. Rebuild character sheets using the new system's `character-template.md`
4. Update `game/rules/campaign-extensions.md` for the new system's mechanics

> **Do this before Session 1.** Changing rulesets mid-campaign causes agents to operate on inconsistent rule systems. If you want a different system, start a new campaign.

**Proprietary systems** (full DnD 5e beyond SRD, Daggerheart, Pathfinder, etc.): place your ruleset in `game/rules/private/`. This directory is gitignored. Do not publish AI-generated content based on proprietary rules.

---

## Using a Different AI System

The engine is not Claude-specific. The markdown files are plain text — any LLM can read them. To adapt for another system:

- **Gemini / GPT-4o / other**: Implement the same orchestration pattern — a main agent that reads the state files and spawns subagents with injected context. The file structure and injection logic is documented in `game/meta/architecture.md`.
- **Custom agent frameworks**: The five context files injected per player call (character, journal, story-so-far, current-state, scene prompt) are the interface. Any framework that can pass these as context to a subagent will work.

---

## Legal Notes

**Default ruleset (SRD)**: `game/rules/srd-5e-2024/` uses content from the [System Reference Document 5.1](https://dnd.wizards.com/resources/systems-reference-document) ("SRD 5.1") by Wizards of the Coast LLC, licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/legalcode). Session logs generated using this ruleset may be published freely. See [`CREDITS.md`](CREDITS.md) for the required attribution notice you must include in any published work.

**Campaign content** (Aldenmere, the four characters, the story): original creative work, not derived from any proprietary source.

**Proprietary rulesets**: Do not publish AI-generated content based on systems you don't have rights to publish. The `rules/private/` gitignore is a safeguard, not a license.

### If You Fork This Repository

> **You must retain SRD attribution in any published work.**

If you fork this repo and publish content generated using the default SRD ruleset — session logs, stories, videos, a game product — you are required by the CC BY 4.0 license to include the attribution notice from [`CREDITS.md`](CREDITS.md) in that published work. The exact text is:
>
> *"This work includes material taken from the System Reference Document 5.1 ("SRD 5.1") by Wizards of the Coast LLC and available at https://dnd.wizards.com/resources/systems-reference-document. The SRD 5.1 is licensed under the Creative Commons Attribution 4.0 International License available at https://creativecommons.org/licenses/by/4.0/legalcode."*

Additional requirements:
- Do **not** use the trademarks "Dungeons & Dragons," "D&D," or "Dungeon Master" on your product — these are registered trademarks of Wizards of the Coast and are not covered by the CC BY 4.0 license.
- You **may** describe your work as "compatible with fifth edition" or "5e compatible."
- If you switch to a **proprietary ruleset** (anything not in the SRD), keep it in `rules/private/` and do not publish AI-generated content derived from it without appropriate rights.
- The CC BY 4.0 license permits commercial use — you may sell products built on this template, provided attribution is included.

---

## Contributing

PRs welcome for improvements to the architecture, agent prompting strategies, or the ruleset plugin system. Campaign-specific content (the Aldenmere characters and story) is specific to this playthrough.
