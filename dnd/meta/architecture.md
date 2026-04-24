# Multi-Agent DnD: Architecture

## Overview

This is a Dungeons & Dragons campaign run entirely by AI agents. The main Claude agent acts as the **Dungeon Master**. Four **Player Character (PC) subagents** are spawned each turn using the Claude Agent SDK, one per character. A fifth subagent, the **Rules Lawyer**, reviews mechanical correctness in an advisory capacity. Each subagent fully embodies its role and makes autonomous decisions — the human observer does not direct the players.

---

## Agent Roles

### Dungeon Master (Main Agent)
- Maintains world state
- Describes scenes, NPCs, and outcomes
- Resolves actions using DnD 5e 2024 rules (rolls simulated)
- Spawns player agents each round/scene
- Calls the Rules Lawyer at appropriate points (see Turn Structure)
- Has **final authority** on all rulings — may accept or overrule the Rules Lawyer at any time
- Writes session logs and updates all memory files

### Player Agents (Subagents)
- Spawned fresh each turn via the Agent tool
- Receive injected context (see below) — they are stateless between calls
- Make in-character decisions based solely on their character personality and available context
- Cannot communicate directly with each other — the DM relays inter-party dialogue

### Rules Lawyer (Subagent)
- Spawned after all player actions are declared in a combat round (or when flagged by DM)
- Reviews mechanical correctness against DnD 5e 2024 rules
- Returns a structured advisory — never blocks play
- Flags Rule of Cool opportunities as well as errors
- DM reads the advisory and explicitly accepts, modifies, or overrules each item
- All rulings (including overrides) logged in `rules/rulings-log.md` for future consistency
- See full profile in `meta/rules-lawyer.md`

---

## Context Injection Per Player Agent

Each subagent prompt contains:

1. **Character file** (`characters/{name}.md`) — who they are, stats, personality, speech patterns
2. **Personal journal** (`memory/{name}-journal.md`) — accumulated memories, opinions of other PCs, current goals and feelings
3. **Story so far** (`world/story-so-far.md`) — cumulative narrative summary
4. **Current state** (`world/current-state.md`) — exact location, active scene, NPCs present, recent events
5. **Current scene prompt** — the DM's specific situation requiring a response

## Context Injection Per Rules Lawyer Call

1. **Active ruleset config** (`rules/active-ruleset.md`) — declares which system is in play and its directory
2. **Quick reference** (`rules/<active-directory>/quickref.md`) — mechanical rules for the active system
3. **House rules** (`rules/<active-directory>/house-rules.md`) — standing DM rulings and Rule of Cool policy
4. **Rulings log** (`rules/<active-directory>/rulings-log.md`) — past rulings to avoid re-litigating settled decisions
5. **Actions to review** — the specific declarations, rolls, and situations for this call (provided by DM)

---

## Turn Structure

### Exploration / Roleplay Scenes

```
1. DM sets the scene
2. Player agents called SEQUENTIALLY (each sees what prior players said)
   └─ Order rotates each scene to avoid one character always leading
3. DM narrates outcomes
4. Rules Lawyer: NOT called unless DM flags a specific edge case
5. DM updates current-state.md if significant
```

### Combat

```
ROUND START
│
├─ Initiative set (d20 + DEX, highest first)
│
└─ For each round:
   │
   ├─ PLAYER TURNS (sequential, in initiative order)
   │   └─ Each player agent sees: scene state + all prior player actions this round
   │
   ├─ RULES LAWYER REVIEW [ONE call, batch review of full round]
   │   ├─ Receives: all player declarations + current combat state
   │   └─ Returns: structured advisory (✓ LEGAL / ⚠ CORRECTION / ❌ ERROR / ★ RULE OF COOL)
   │
   ├─ DM RULING
   │   ├─ Reads advisory
   │   ├─ Accepts, modifies, or overrules each item
   │   └─ Logs decisions in rulings-log.md
   │
   └─ DM narrates outcomes + resolves enemy turn
```

**The Rules Lawyer is called once per combat round** — after all players have declared but before outcomes are narrated. This keeps the review tight and non-blocking while catching consequential mechanical errors.

### Pre-Action Check (Optional)
Before a player attempts something highly unusual or high-stakes, the DM may call the Rules Lawyer in advance to confirm legality. This is at DM discretion.

### Between Scenes
- DM updates `world/current-state.md`
- Player journals updated if significant personal events occurred

### Between Sessions
- DM updates `world/story-so-far.md` with full session summary
- All four player journals updated with memories, relationship changes, emotional notes
- Session log committed to `sessions/session-NN.md`
- Rulings log reviewed; any standing house rules promoted to `rules/house-rules.md`

---

## File Structure

```
dnd/
  meta/
    architecture.md        ← this file
    rules-lawyer.md        ← Rules Lawyer agent profile and mandate
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
  rules/
    README.md              ← Ruleset plugin system: what a ruleset directory must contain
    active-ruleset.md      ← Config: which ruleset is active and its directory path
    .gitignore             ← Gitignores rules/private/ for proprietary systems
    srd-5e-2024/           ← Default: DnD 5e 2024 SRD (CC BY 4.0, safe to publish)
      system-notes.md      ← What this system is; SRD scope; 2024 vs 2014 differences
      quickref.md          ← Mechanical rules reference
      house-rules.md       ← DM standing rulings; Rule of Cool policy
      rulings-log.md       ← Every ruling made, accepted or overruled, with reason
      character-template.md ← Template for creating new PCs in this system
    private/               ← Gitignored. Place proprietary rulesets here.
  sessions/
    session-01.md          ← (created during play)
```

---

## Design Notes

### Why Subagents Are Stateless
The Agent tool spawns a fresh context each call. All persistent state lives in markdown files, which the DM reads and injects. This is intentional — it keeps state auditable and versionable in git.

### The Memory System
Player journals accumulate genuine character development. An agent playing Grunka in Session 5 will have Grunka's memories of Sessions 1-4 injected, producing continuity of personality and relationship. The rulings log serves the same function for the Rules Lawyer.

### Inter-Party Dialogue
When one character speaks to another, the DM includes that dialogue verbatim in the next character's context prompt. Characters can develop opinions of each other across sessions through their journals.

### Authentic Character Play
Player subagents are explicitly instructed to make decisions their *character* would make, not the "optimal" game decision. A character with a flaw should act on that flaw. This produces drama.

### The Rule of Cool
The DM retains final authority over all rulings. When the Rules Lawyer flags a Rule of Cool opportunity, the DM defaults to yes — possibly with a check, a cost, or a narrative constraint. Fun takes precedence over strict mechanical correctness, provided it doesn't break game integrity or undermine other players.

### Ruleset Plugin System

The rules engine is fully swappable. The active system is declared in `rules/active-ruleset.md`. Changing that config file is all that's required to switch systems — the Rules Lawyer, DM, and player agents all read from the declared ruleset directory.

Each ruleset is a self-contained directory containing five files: `system-notes.md`, `quickref.md`, `house-rules.md`, `rulings-log.md`, and `character-template.md`. See `rules/README.md` for the full spec.

**Proprietary rulesets**: Place non-SRD systems (full DnD 5e, Daggerheart, Pathfinder, etc.) in `rules/private/`. This directory is gitignored and will never be committed to a public repository.

**Default ruleset**: `rules/srd-5e-2024/` — the Creative Commons-licensed SRD subset of DnD 5e 2024. Content generated using this ruleset is safe to publish.

### 2024 Edition Note
This campaign uses DnD 5e 2024 (SRD) as the primary ruleset. Key differences from 2014 that affect this party are documented in `rules/srd-5e-2024/system-notes.md` and `rules/srd-5e-2024/house-rules.md`. The most significant: Frenzy no longer causes exhaustion, and Divine Smite is now a reaction.

---

## Session Log Format

Each session file (`sessions/session-NN.md`) contains:
- **Scene descriptions** (DM narration)
- **Player declarations** (what each character does/says, labeled by character name)
- **Rules Lawyer reviews** (the advisory output, inline at each combat round)
- **DM rulings** (accepted/overruled, dice results, consequences)
- **Combat turns** (structured: initiative order, action, result, HP tracking)
- **End-of-session notes** (what changed, cliffhanger if any)
