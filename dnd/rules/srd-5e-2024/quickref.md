# DnD 5e 2024 — Mechanical Quick Reference

_Generic mechanical reference for DnD 5e 2024 (SRD). Campaign-specific character stats and party-specific clarifications live in `rules/campaign-extensions.md`. 2014 differences noted where relevant._

---

## Core Mechanic

All checks: roll d20 + modifier vs. Difficulty Class (DC) or opponent's roll.
- **Advantage**: Roll 2d20, take higher.
- **Disadvantage**: Roll 2d20, take lower.
- Advantage and disadvantage cancel each other regardless of how many sources of each.
- Bonuses/penalties beyond advantage/disadvantage still apply (e.g., Bless adds 1d4 to attack rolls and saving throws regardless of advantage state).

---

## Action Economy

On your turn you have:
- **1 Action**
- **1 Bonus Action** (only if a feature or spell specifically grants one)
- **1 Reaction** (on your turn or others' turns; recharges at start of your next turn)
- **Movement** (up to speed; can split around actions)
- **Free Interactions** (draw/sheathe weapon, open unlocked door — one per turn)

**2024 Action Types**:
| Action | Description |
|--------|-------------|
| Attack | Make one or more weapon/unarmed attacks |
| Cast a Spell | Cast a spell with a casting time of 1 action |
| Dash | Move up to your speed again this turn |
| Disengage | Movement doesn't provoke opportunity attacks this turn |
| Dodge | Attacks against you have disadvantage; you have advantage on DEX saves (requires you can see attacker) |
| Help | Give an ally advantage on next ability check or attack |
| Hide | Make Stealth check to become hidden |
| Influence | Attempt to sway a creature's attitude (Persuasion, Deception, Intimidation, or Animal Handling) |
| Magic | Some class features use this action type (distinct from Cast a Spell) |
| Ready | Prepare an action to trigger on a specified condition |
| Search | Make Perception or Investigation check to find something |
| Study | Make Arcana, History, Medicine, Nature, or Religion check |
| Utilize | Activate a magic item that requires an action |

---

## Attack Rolls

**To hit**: d20 + ability modifier + proficiency bonus (if proficient) vs. target AC.
- **Critical Hit**: Natural 20. Roll all damage dice twice, add modifiers once.
- **Critical Miss**: Natural 1. Attack automatically misses.
- **Damage on hit**: Weapon damage die + ability modifier (STR for melee, DEX for ranged/finesse).

---

## Saving Throws

d20 + ability modifier + proficiency (if proficient) vs. spell DC or effect DC.  
Spell DC = 8 + proficiency + spellcasting modifier.

---

## Conditions (2024)

| Condition | Key Effect |
|-----------|------------|
| Blinded | Auto-fail sight checks; attacks against have advantage; your attacks have disadvantage |
| Charmed | Can't attack charmer; charmer has advantage on social checks vs. you |
| Deafened | Auto-fail hearing checks |
| Exhaustion | **2024**: Each level imposes -2 to all d20 Tests (attack, save, ability check). Max 6 levels; level 6 = death. Removed by long rest (1 level) or lesser restoration (all levels). |
| Frightened | Disadvantage on ability checks/attacks while source is in sight; can't willingly move closer to source |
| Grappled | Speed 0. Ends if grappler is incapacitated or effect ends. Escape: STR or DEX (Athletics or Acrobatics) vs. grappler's Athletics. |
| Incapacitated | Can't take actions or reactions |
| Invisible | Can't be seen without magic; attacks against have disadvantage; your attacks have advantage |
| Paralyzed | Incapacitated; auto-fail STR/DEX saves; attacks have advantage; hits within 5 ft are critical hits |
| Petrified | Transformed to stone; incapacitated; auto-fail STR/DEX saves; resistance to all damage |
| Poisoned | Disadvantage on attack rolls and ability checks |
| Prone | Disadvantage on attack rolls; attacks have advantage within 5 ft, disadvantage from further; stand up costs half movement |
| Restrained | Speed 0; disadvantage on attacks; attacks against have advantage; disadvantage on DEX saves |
| Stunned | Incapacitated; auto-fail STR/DEX saves; attacks against have advantage |
| Unconscious | Incapacitated, prone; auto-fail STR/DEX saves; attacks have advantage; hits within 5 ft are critical hits |

---

## Death & Dying

- At 0 HP: fall unconscious, begin making death saving throws.
- **Death saving throw**: d20 at start of your turn. 10+ = success, 9 or lower = failure. No modifiers.
  - 3 successes: stabilized (unconscious at 1 HP)
  - 3 failures: dead
  - Natural 20: regain 1 HP and consciousness
  - Natural 1: counts as 2 failures
  - Taking damage while at 0 HP: 1 failure; critical hit: 2 failures
- Any healing while at 0 HP restores HP and ends unconscious/dying state.

---

## Concentration

- Only one concentration spell at a time.
- Taking damage while concentrating: CON saving throw, DC = 10 or half damage taken (whichever is higher). Failure = spell ends.
- Incapacitated or dying = concentration ends automatically.

---

## Combat: Key Mechanics

**Initiative**: At combat start, everyone rolls d20 + DEX modifier. Highest goes first.

**Opportunity Attacks**: When a creature you can see moves out of your reach. Costs your reaction. One melee attack.

**Two-Weapon Fighting**: When you take the Attack action with a light melee weapon, you can use a bonus action to attack with a different light melee weapon in your off-hand. No ability modifier to damage on the bonus attack (unless negative).

**Grappling**: Replace one attack with a STR (Athletics) check vs. target's STR (Athletics) or DEX (Acrobatics). Success = target is grappled.

**Shove**: Replace one attack with STR (Athletics) vs. target's STR (Athletics) or DEX (Acrobatics). Success = push 5 ft or knock prone.

**Flanking** *(optional rule)*: Two allies on opposite sides of a creature grant each other advantage. Not active by default — DM must explicitly enable it. Check `rules/campaign-extensions.md` for this campaign's setting.

---

## Spellcasting

**Spell Slots**: Expended when casting a spell of 1st level or higher. Recovered on long rest (or partial on short rest for some classes).

**Cantrips**: No slot required. Unlimited use.

**Upcast**: Cast a lower-level spell using a higher-level slot for enhanced effect (if the spell allows it).

**Verbal (V) / Somatic (S) / Material (M) components**: Required unless a feature removes the need. If silenced, can't cast V spells. If hands restrained, can't cast S spells. M components are handled by a spell focus or component pouch.

**Ritual Casting**: Some spells can be cast as a ritual (10 extra minutes, no slot consumed). Only if the caster has the ritual casting feature and the spell is tagged as a ritual.

---

## Class Feature Reference (Generic)

Key features that commonly produce rules questions. For this campaign's specific characters and exact numbers, see `rules/campaign-extensions.md`.

**Divine Smite (Paladin, 2024)**: Reaction triggered after a melee hit is confirmed. Expend a spell slot: 1st = 2d8 radiant, +1d8 per slot level above 1st, max 5d8; +1d8 additional vs undead or fiends.

**Lay on Hands (Paladin)**: Action. Pool = 5 × paladin level HP/long rest. Touch to heal up to pool amount, or spend 5 HP to cure one disease or poison. Cannot target constructs or undead.

**Channel Divinity (Paladin)**: 1/short or long rest. Options depend on subclass.

**Portent (Divination Wizard)**: Roll 2d20 at dawn. Before any visible creature makes a d20 roll, expend one die to replace the result. Portent dice cannot be rerolled or modified by advantage/disadvantage.

**Arcane Recovery (Wizard)**: Once/day on a short rest. Recover spell slots with total levels ≤ half wizard level (rounded up). Cannot recover slots 6th level or higher.

**Sneak Attack (Rogue)**: Once per turn (not round). Requires finesse or ranged weapon + (advantage OR ally within 5 ft of target, and no disadvantage).

**Cunning Action (Rogue 2+)**: Bonus action to Dash, Disengage, or Hide.

**Rage (Barbarian)**: Bonus action. +2 melee damage, advantage on STR checks/saves, resistance to B/P/S. Ends if no attack or damage since last turn, or unconscious. Cannot cast or concentrate on spells while raging.

**Reckless Attack (Barbarian)**: Advantage on all STR melee attack rolls this turn; enemies have advantage on attacks vs. you until your next turn.

**Frenzy (Berserker Barbarian, 2024)**: While raging, make one additional melee weapon attack as a bonus action each turn. No exhaustion cost (2024 change from 2014).

**Unarmored Defense (Barbarian)**: AC = 10 + DEX modifier + CON modifier (while not wearing armor).

**Halfling Lucky**: On a natural 1, reroll and use the new result. Does not apply when a Portent die or other effect replaces the roll rather than rerolling it.

---

## Common Mistake Reference

| Mistake | Correct Rule |
|---------|-------------|
| Sneak Attack on any attack | Only with finesse/ranged weapon + advantage or ally adjacent |
| Divine Smite declared before rolling | 2024: declared as reaction after hit confirmed |
| Frenzy causes exhaustion | 2024: no exhaustion cost |
| Bonus action attack with Frenzy without being in Rage | Frenzy only activates while raging |
| Two concentration spells at once | Never. Casting a second drops the first. |
| Natural 20 always crits | Only on attack rolls. Not saving throws or ability checks. |
| Advantage stacks | It doesn't. Multiple sources of advantage = still just advantage. |
| Portent dice can be rerolled | No. The rolled number stands. |
| Lay on Hands as a bonus action | It's an action. |
| Cantrip damage scales with character level | Yes — cantrips scale at levels 5, 11, 17. |
