# Multi-Agent DnD: Architecture

## Overview

This is a Dungeons & Dragons campaign run entirely by AI agents. The main Claude agent acts as the **Dungeon Master**. Four **Player Character (PC) subagents** are spawned each turn using the Claude Agent SDK, one per character. Each subagent fully embodies its character and makes autonomous decisions — the human observer does not direct the players.

---

## Agent Roles

### Dungeon Master (Main Agent)
- Maintains world state
- Describes scenes, NPCs, and outcomes
- Resolves actions using DnD 5e rules (rolls simulated)
- Spawns player agents each round/scene
- Writes session logs and updates all memory files

### Player Agents (Subagents)
- Spawned fresh each turn via the Agent tool
- Receive injected context (see below) — they are stateless between calls
- Make in-character decisions based solely on their character personality and available context
- Cannot communicate directly with each other — the DM relays inter-party dialogue

---

## Context Injection Per Player Agent

Each subagent prompt contains:

1. **Character file** (`characters/{name}.md`) — who they are, stats, personality, speech patterns
2. **Personal journal** (`memory/{name}-journal.md`) — accumulated memories, opinions of other PCs, current goals and feelings
3. **Story so far** (`world/story-so-far.md`) — cumulative narrative summary
4. **Current state** (`world/current-state.md`) — exact location, active scene, NPCs present, recent events
5. **Current scene prompt** — the DM's specific situation requiring a response

---

## Turn Structure

### Exploration / Roleplay Scenes
- Players are called **sequentially** — each agent sees what the previous players said
- This allows in-character reactions and conversations to build naturally
- Order rotates to avoid one character always leading

### Combat
- Initiative is rolled at scene start
- Players act in initiative order (sequential calls, each seeing prior actions)
- Enemy actions are resolved by the DM between player turns
- Combat state (HP, conditions, positions) tracked in `world/current-state.md`

### Between Scenes
- DM updates `world/current-state.md`
- Player journals updated if significant personal events occurred

### Between Sessions
- DM updates `world/story-so-far.md` with full session summary
- All four player journals updated with memories, relationship changes, emotional notes
- Session log committed to `sessions/session-NN.md`

---

## File Structure

```
dnd/
  meta/
    architecture.md        ← this file
  world/
    lore.md                ← world history, factions, the Last Great Evil
    current-state.md       ← live game state (location, scene, HP, quests)
    story-so-far.md        ← cumulative narrative summary
  characters/
    reginald.md            ← Sir Reginald Pompsworth III (Paladin)
    zyx.md                 ← Zyx (Wizard)
    midge.md               ← Midge Thistlewick (Rogue)
    grunka.md              ← Grunka (Barbarian)
  memory/
    reginald-journal.md    ← Reginald's personal memories and opinions
    zyx-journal.md         ← Zyx's personal memories and opinions
    midge-journal.md       ← Midge's personal memories and opinions
    grunka-journal.md      ← Grunka's personal memories and opinions
  sessions/
    session-01.md          ← (created during play)
```

---

## Design Notes

### Why Subagents Are Stateless
The Agent tool spawns a fresh context each call. All persistent state lives in markdown files, which the DM reads and injects. This is intentional — it keeps state auditable and versionable in git.

### The Memory System
Player journals accumulate genuine character development. An agent playing Grunka in Session 5 will have Grunka's memories of Sessions 1-4 injected, producing continuity of personality and relationship.

### Inter-Party Dialogue
When one character speaks to another, the DM includes that dialogue verbatim in the next character's context prompt. Characters can develop opinions of each other across sessions through their journals.

### Authentic Character Play
Subagents are explicitly instructed to make decisions their *character* would make, not the "optimal" game decision. A character with a flaw should act on that flaw. This produces drama.

---

## Session Log Format

Each session file (`sessions/session-NN.md`) contains:
- **Scene descriptions** (DM narration)
- **Player declarations** (what each character does/says, labeled by character name)
- **Combat turns** (structured: initiative order, action, result, HP tracking)
- **DM rulings** (dice results, consequences)
- **End-of-session notes** (what changed, cliffhanger if any)
