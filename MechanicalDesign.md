# Specialties:

## Melee Combat
  - Reduced Stamina Cost when attacking with melee weapons
  - Reduced Damage from attacks with melee weapons
  - Increased chance to hit with melee weapons
  - Increased chance to correctly identify enchanted melee weapons

## Ranged Combat
  - Reduced Stamina Cost when attacking with ranged weapons
  - Increased chance to hit with ranged weapons
  - Increased chance to correctly identify enchanted ranged weapons and ammunition
  - Decreased chance for used ammunition to break once used

## Unarmed Combat
  - Reduced Stamina Cost when attacking unarmed, making barges, and grappling
  - Increased chance to hit when unarmed or with barges
  - Increased chance to successfully grapple, and to break out of being grappled
  - Increased chance to emulate unarmed combat techniques you see

## Sports & Fieldcraft
  - Reduced Stamina Cost when Sprinting, Leaping, Climbing, or other Physical Tasks
  - Increased chance to hit with improvised weapons
  - Increased chance to spot secrets on the map
  - Increased range to spot Items and NPC's

## Potions & Alchemy
  - Reduced Stamina Cost associated with casting spells via drinking, scattering, or otherwise utilizing a Potion
  - Increased chance to correctly identify Potions and Alchemical Compounds
  - Increased chance to correctly brew potions from recipes
  - Increased chance to notice poisioned objects before being affected by the poison

## Scrolls, Sigils, & Arcane Figures
  - Reduced Stamina Cost associated with casting spells from Scrolls, and preparing sigil magics
  - Increased chance to correctly identify Scrolls, arcane figures, and sigils in the overworld
  - Increased chance to correctly cast spells from scrolls, and correctly prepare and trigger sigils
  - Increased chance to duplicate sigils from scrolls, or from instructions in books or verbal descriptions
  
## Spoken, Sung, Danced, And Performed Magic
  - Reduced Stamina Cost to perform both magical and nonmagical spoken word, song, dance, and ritual performances.
  - Increased chance to duplicate a performance spell from seeing the spell performed
  - Increased chance to identify and interrupt a performance spell in progress before it is complete
  - Decreased chance to be affected by a performance magic spell

## Gilding, Imbuing, Enchanting, and Wandcraft
  - Reduced Stamina Cost associated with casting spells using enchanted nonweapon items and wands
  - Reduced Stamina Cost to restore charges to a wand or staff
  - Increased chance of correctly identifying enchanted and cursed nonweapon items
  - Decresed chance of misfiring spells stored in wands, staves, and other nonweapon items

# Stamina System:

## Player has a Stamina stat.  
- It is full after a rest, and doing anything involving a specialty (or being attacked) depletes it.  
- It recovers gradually while the player isn't doing anything.  
- If a player doesn't have enough stamina, the player cannot perform a specialty action without risking injury and falling unconscious.    
- If a player has no stamina, the player falls unconscious.  
- An unconscious player cannot move or perform any actions
- While unconscious, (unless wounded) the player recovers stamina as if they're resting, and once stamina is positive again, the player can move and perform actions again.
- If a player's action takes them below zero Stamina, each point of negative Stamina becomes a chance to Wound the Player.

## Being Attacked depletes Stamina
- Attacks from enemies have an attack value, adjusted by random chance
- Armor, Enchantments, Spells, and Skills in the relevant sort of Combat reduce the attack value
- Remaining Attack Value is depleted from defender's Stamina
- If an Attack drops the defender to zero Stamina, the defender is knocked unconscious
- If an Attack drops the defender below zero Stamina, each point of Attack Value becomes a chance to Wound the defender.

## Wounds
- Each point of negative Stamina is counted as a chance to wound the character when inflicted/incurred.
- The first point has a 1/X chance to Wound.
- - Difficulty determines "X"
- - - Hard X=16, -4 Stamina for 50% chance to Wound, -5 Automatic Wound*
- - - Normal X=128 -7 Stamina for 50% chance to Wound, -8 Automatic Wound*
- - - Easy X=1024 -10 Stamina for 50% chance to Wound, -11 Automatic Wound*
- Each subsequent point of negative Stamina has double the previous chance
- While Wounded, a player doesn't regain Stamina over time.  
- When a player is first Wounded, they regain consciousness at 1 point of Stamina
- If a player who is wounded falls unconscious, they do not recover Stamina while unconscious, and will remain unconscious unless helped.

## Mortally Wounded
- If a player who is already wounded gets wounded again, they are then Mortally Wounded.
- When a player is first Mortally Wounded, they remain unconscious at 0 Stamina
- While Mortally wounded, a player doesn't regain stamina over time.
- If an item, spell, or the actions of a Party Member restore a Mortally Wounded Player's Stamina, that restored Stamina ticks back down to 0 at a rate of "Y" points per turn.
- - Difficulty determines "Y"
- - - Hard Y=4*
- - - Normal Y=2*
- - - Easy Y=1*

## Death
- A Mortally Wounded player has a 1/Z chance to Die each turn. 
- - Difficulty determines "Z"
- - - Hard Z=4*
- - - Normal Z=8*
- - - Easy Z=16*
- If a Mortally Wounded player accumulates Negative Stamina, the player dies.

## Massive Damage
- If an attack is made that inflicts more Negative Stamina than the Automatic Wound Threshold, then remaining Negative Stamina is accumulated and figured against the stamina like a separate attack/action would.
- If that accumulated Negative Stamina Mortally Wounds the player and still has Negative Stamina accumulated, that Player Dies outright from Massive Damage.
### Example: 
> - Player has 8 Stamina, and recieves 25 Negative Stamina, (Difficulty: Easy)
> - Player hits 0 Stamina, falls Unconscious, 17 Negative Stamina remains
> - 11 Negative Stamina means Player is Automatically Wounded, 6 Negative Stamina Remains
> - Player Regains Consciousness, Player is now Wounded, Player has 1 Stamina, 6 Negative Stamina Remains
> - Player hits 0 Stamina again, falls Unconscious again, 5 Negative Stamina means 5 chances for wounds.
> - First Chance for Mortal Wounds: 1/1024 chance, Player doesn't get wounded,
> - 2nd Chance: 1/512 chance, 
> - 3rd Chance: 1/256 chance,  
> - 4th Chance: 1/128 chance, Player gets unlucky and gets Mortally Wounded, 0 Stamina,
> - Mortally Wounded Player is at 1 Negative Stamina and dies.


## Restoration, First Aid, and Healing.
- Potions, Scrolls, Spells, and Enchanted Items "...of Vigor" restore Stamina irrespective of whether the Player is Wounded.
- - These are common items to find
- Potions, Scrolls, Spells, and Enchanted Items "...of Healing" return a Wounded Player to Normal, or make a Mortally Wounded player merely Wounded.
- - These are rare items,
- - These do not restore Stamina
- Potions, Scrolls, Spells, and Enchanted Items "...of Restoration" combine the effects of "Vigor" and "Healing" Items.
- - These are exceedingly rare items.
- - "...of Restoration" will return a Wounded Player to Normal or return a Mortally Wounded player to Wounded, and restore half of maximum Stamina.
- - "..of Greater Restoration" will return a player in any condition to Normal with full Stamina.
-


"*" = subject to change for balance

# Porting to Tabletop:

- Since everything so far is based on powers of 2, can I use d4's to bring this math to the tabletop?
  > 1D4 = 1/4
  > 2D4 = 1/16
  > 3D4 = 1/64
  > 4D4 = 1/256
  > 5D4 = 1/1024
- Another possibility is using dice from Ur... D4's with two painted corners (D2's)
  > 1D2 = 1/2
  > 2D2 = 1/4
  > 3D2 = 1/8
  > 4D2 = 1/16
  > 5D2 = 1/32
  > 6D2 = 1/64
  > 7D2 = 1/128
  > 8D2 = 1/256
  > 9D2 = 1/512
  > 10D2 = 1/1024
  - 10 dice isn't too many is it?

# Notes:

- Wound chance: 1, 2, 4, 8, 16, (Hardmode) 32, 64, 128, (Normal Mode) 256, 512, 1024 (Easy Mode) 
- Don't use a simple "Plus to hit" magic weapon.  Make them all interesting in some way. 
