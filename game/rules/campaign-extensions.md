# Campaign Rules Extensions

_Campaign-specific rules annotations for this game. Injected into the Rules Lawyer alongside the base ruleset. Does not override base rules — adds specificity on top of them._

_Update this file when characters level up, acquire significant abilities, or when the GM establishes a campaign-specific ruling that doesn't belong in the base ruleset._

---

## Active Optional Rules

- **Flanking**: Not active. Two allies on opposite sides of an enemy do not grant advantage in this campaign.

---

## Party Character Sheets (Mechanical Summary)

### Reginald — Paladin (Oath of Devotion) 3

| Stat | Value |
|------|-------|
| STR | 16 (+3) |
| DEX | 8 (-1) |
| CON | 14 (+2) |
| INT | 12 (+1) |
| WIS | 14 (+2) |
| CHA | 16 (+3) |
| HP | 28 |
| AC | 18 (plate + shield) |
| Spell Save DC | 13 |
| Spell Attack | +5 |
| Spell Slots | 3 × 1st level |
| Proficiency | +2 |

**Key abilities**:
- **Divine Smite** (reaction on hit): 1st slot = 2d8 radiant; +1d8 per slot level above 1st; max 5d8; +1d8 vs undead/fiends
- **Lay on Hands** (action): 15 HP pool/long rest; 5 HP to cure one disease or poison
- **Channel Divinity** (1/short or long rest): Sacred Weapon (+3 attack, bright light 20 ft, 1 min) or Turn the Unholy (WIS DC 13, 30 ft)
- **Prepared spells** (6): Cure Wounds, Bless, Detect Evil and Good, Command, Protection from Evil and Good, Sanctuary

---

### Zyx — Wizard (School of Divination) 3

| Stat | Value |
|------|-------|
| STR | 8 (-1) |
| DEX | 14 (+2) |
| CON | 12 (+1) |
| INT | 18 (+4) |
| WIS | 16 (+3) |
| CHA | 10 (0) |
| HP | 18 |
| AC | 12 (15 with Mage Armor) |
| Spell Save DC | 14 |
| Spell Attack | +6 |
| Spell Slots | 4 × 1st, 2 × 2nd |
| Proficiency | +2 |

**Key abilities**:
- **Portent** (2 dice/dawn): Before any visible creature rolls a d20, Zyx may replace the result with one Portent die. Cannot be rerolled, modified by advantage/disadvantage, or affected by Halfling Lucky. Record current dice in session log.
- **Arcane Recovery** (1/day, short rest): Recover spell slots totaling up to 2 levels combined.
- **Prepared spells** (7): Magic Missile, Shield, Sleep, Misty Step, Scorching Ray, Detect Magic, Identify

---

### Midge — Rogue (Arcane Trickster) 3

| Stat | Value |
|------|-------|
| STR | 8 (-1) |
| DEX | 18 (+4) |
| CON | 12 (+1) |
| INT | 14 (+2) |
| WIS | 8 (-1) |
| CHA | 16 (+3) |
| HP | 22 |
| AC | 15 (leather + DEX) |
| Spell Save DC | 12 |
| Spell Attack | +4 |
| Spell Slots | 2 × 1st level |
| Proficiency | +2 |

**Key abilities**:
- **Sneak Attack** (2d6, once per turn): Requires finesse or ranged weapon + (advantage OR ally within 5 ft of target with no disadvantage on the attack)
- **Cunning Action** (bonus action): Dash, Disengage, or Hide
- **Mage Hand Legerdemain**: Invisible Mage Hand; can pick locks, disarm traps, steal/plant objects from 30 ft; opposed by Perception vs. Midge's Sleight of Hand (+8)
- **Halfling Lucky**: On a natural 1, reroll and use the new result (does not apply to Portent replacements)
- **Cantrips**: Mage Hand (invisible), Minor Illusion, Prestidigitation
- **Prepared spells**: Silent Image, Color Spray, Disguise Self

---

### Grunka — Barbarian (Path of the Berserker) 3

| Stat | Value |
|------|-------|
| STR | 18 (+4) |
| DEX | 14 (+2) |
| CON | 16 (+3) |
| INT | 10 (0) |
| WIS | 14 (+2) |
| CHA | 12 (+1) |
| HP | 34 |
| AC | 15 (Unarmored Defense: 10 + DEX + CON) |
| Proficiency | +2 |

**Key abilities**:
- **Rage** (3/day, bonus action): +2 melee damage, advantage on STR checks/saves, resistance to B/P/S damage; ends if no attack or damage since last turn or unconscious; cannot cast/concentrate spells
- **Reckless Attack**: Advantage on STR melee attacks this turn; enemies have advantage on attacks vs. Grunka until next turn
- **Danger Sense**: Advantage on DEX saves vs. visible effects; not while blinded/deafened/incapacitated
- **Frenzy** (while raging): One additional melee weapon attack as bonus action each turn. **No exhaustion cost (2024 rule).**
- **Relentless Endurance** (1/long rest): Drop to 1 HP instead of 0 (not triggered if outright killed)
- **Savage Attacks**: On critical hit with melee weapon, roll one extra damage die
- **Greataxe**: 1d12 + 4 (STR). Critical hit: 3d12 + 4 (base 2d12 + Savage Attacks die)
- **Unarmored Defense**: AC = 10 + 2 (DEX) + 3 (CON) = **15**

---

## Notes for Rules Lawyer

- All four characters are SRD-compatible at level 3
- Characters will level up during the campaign — update this file when they do
- Zyx's Portent dice should be recorded in `world/current-state.md` at session start and consumed from there
- Midge's Halfling Lucky and Zyx's Portent interact as follows: Lucky applies before Portent replacement is possible; if Portent replaces the roll, Lucky cannot then trigger on the Portent die
