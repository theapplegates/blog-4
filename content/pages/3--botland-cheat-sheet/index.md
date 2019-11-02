---
title: Bot Land Cheat Sheet
---

The purpose of this page is to allow quick lookups on specific things about Bot Land game mechanics. I wanted to consolidate this information in one place, since it was scattered all over the internet (some of the docs were available only in-game, some information only in Discord chat, etc.) You can edit this page <a href="https://github.com/baobabKoodaa/blog/blob/master/content/pages/3--botland-cheat-sheet/index.md" target="_blank">here</a>.

<!--<re-img
    src="honeypot.jpg"
    title="Photo by Sonja Langford on Unsplash"
    href="https://unsplash.com/photos/RQHzRELE2Ss"
    >
</re-img>-->

---

## Comparison of weapon types

| Class         | Damage        | Min-range | Max-range | Directionality   | Delay      | Blind-fireable | Reflectable |
| --------------|:-------------:|:---------:|:---------:|:----------------:|:----------:|:--------------:|:-----------:|
| Melee         | 300-550       | 1         |    1-2    | Only cardinal    | 0          |    No          |   No        |
| Lasers        | 100-400       | 1         |    3-5    | Only cardinal    | 0          |    Yes         |   Yes       | 
| Missiles      | 200-300       | 1         |    3-4    | Any direction    | 0          |    No          |   Yes       |
| Artillery     | 250-500       | 5         |    7-7    | Any direction    | 2          |    No          |   No        |
| Zappers       | 100-350       | -         |     -     | -                | 0          |    -           |   -         |
| Landmines     | 600-600       | -         |     -     | -                | 0          |    -           |   -         |

## Melee

- Melee can hit in only cardinal directions (left, right, up, down).
- Melee hits the target immediately.
- Melee can not be blind-fired (you can not hit cloaked enemies).
- Melee has the ability to charge (simultaneously move and attack from 2 tiles distance in a cardinal direction).
- Melee has no cooldown, but charge does.
- `melee()` attempts to melee any enemy (if multiple enemies are within range, target is chosen based on previously set attack priority).
- `melee(entity)` can be used to melee a specific enemy (if you can sense it).
- `melee(direction)` can be used to melee an enemy at a specific direction, if melee in that direction is possible. Note that `direction` must be string `'left'`, `'right'`, `'up'`, or `'down'`.
- `willMeleeHit()`, `willMeleeHit(entity)` and `willMeleeHit(direction)` return true if the corresponding melee is possible. Note that these will return true even if EMP has disabled your melee. You will lose a turn if you attempt to melee when melee is not possible.
- `canCharge()` returns true if charge is not on cooldown (it does not check whether an enemy is within charging range).
- There is no explicit command to charge; `melee()` will charge if possible.

| Weapon        | Damage        | Charge cooldown |
| --------------|:-------------:|:---------------:|
| Melee I       | 300           | 7               |
| Melee II      | 450           | 4               |
| Melee III     | 550           | 4               |

## Lasers

- All lasers only fire in cardinal directions (left, right, up, down).
- All lasers hit the target immediately.
- All lasers can be blind-fired (you can hit cloaked enemies).
- All lasers can be reflected.
- All lasers have no cooldown (can be used again every turn).
- Inferno Lasers ignite the target, causing 100 damage per turn for the duration of the ignition and causing a cloaked unit to become visible for the duration of the ignition (the cloak buff stays on, so the unit may become invisible after the ignition is over). Ignition persists across rounds.
- Stunning Lasers stun the target for 1 turn.
- Stunning Lasers can not stun the same target 2 turns in a row.
- Stunning Lasers' damage can be reflected but the stun can not.
- Vampiric Lasers heal for 30% of damage inflicted (is this correct?)
- `fireLasers()` attempts to fire lasers at any enemy (if multiple enemies are within range, target is chosen based on previously set attack priority).
- `fireLasers(entity)` can be used to fire lasers at a specific enemy (note that if you can not sense the enemy, you should blind-fire lasers by direction instead).
- `fireLasers(direction)` can be used to blind-fire lasers at a specific direction. Note that `direction` must be string `'left'`, `'right'`, `'up'`, or `'down'`.
- `willLasersHit()`, `willLasersHit(entity)` and `willLasersHit(direction)` return true if the corresponding `fireLasers` is possible. Note that `willLasersHit(direction)` does not indicate whether lasers will hit an enemy, only whether fireing lasers is possible. Also note that these will return true even if EMP has disabled your lasers. You will lose a turn if you attempt to fire lasers and it fails to fire (due to EMP, target out of range, target not sensed due to cloaking and lasers not blind-fired, etc.)

| Weapon                 | Damage        | Range | Special effect | Special duration  |
| -----------------------|:-------------:|:-----:|:--------------:|:-----------------:|
| Lasers I               | 200           | 3     |     -          |    -              |
| Lasers II              | 300           | 4     |     -          |    -              |
| Lasers III             | 400           | 5     |     -          |    -              |
| Inferno Lasers I       | 100           | 3     |     Ignite     |    1              |
| Inferno Lasers II      | 150           | 4     |     Ignite     |    2              |
| Inferno Lasers III     | 200           | 5     |     Ignite     |    3              |
| Stunning Lasers I      | 100           | 3     |      Stun      |    1              |
| Stunning Lasers II     | 150           | 4     |      Stun      |    1              |
| Stunning Lasers III    | 200           | 5     |      Stun      |    1              |
| Vampiric Lasers I      | 150           | 3     |      Heal 30%  |    -              |
| Vampiric Lasers II     | 225           | 4     |      Heal 30%  |    -              |
| Vampiric Lasers III    | 300           | 5     |      Heal 30%  |    -              |

## Missiles

- Any missile can be fired in any direction.
- Any missile hit the target immediately.
- No missile can be blind-fired (you can not hit cloaked enemies).
- Any missile can be reflected.
- Regular Missiles and Multi Missiles have no cooldown.
- Acceleration Missiles have a cooldown which is reduced by consecutive firing and reset by other actions.
- Multi Missiles fire at every enemy in range.
- `fireMissiles()` attempts to fire missiles at any enemy (if multiple enemies are within range, target is chosen based on previously set attack priority).
- `fireMissiles(entity)` can be used to fire missiles at a specific enemy (if you can sense it).
- `willMissilesHit()` and `willMissilesHit(entity)` return true if the corresponding `fireMissiles` is possible. Note that these will return true even if EMP has disabled your missiles. You will lose a turn if you attempt to fire missiles when it's not possible.

| Weapon                    | Damage        | Range | Cooldown         | Acceleration rate |
| --------------------------|:-------------:|:-----:|:----------------:|:-----------------:|
| Missiles I                | 200           | 3     |     -            |    -              |
| Missiles II               | 250           | 3     |     -            |    -              |
| Missiles III              | 300           | 4     |     -            |    -              |
| Multi Missiles I          | 66            | 3     |     -            |    -              |
| Multi Missiles II         | 83            | 3     |     -            |    -              |
| Multi Missiles III        | 100           | 4     |     -            |    -              |
| Acceleration Missiles I   | 200           | 3     |     1.7 → 0.6    |    0.3            |
| Acceleration Missiles I   | 250           | 3     |     1.7 → 0.6    |    0.3            |
| Acceleration Missiles III | 300           | 3     |     1.7 → 0.6    |    0.3            |

## Artillery

- Artillery is the only weapon in the game which does not hit immediately (it takes 2 turns to land a shot).
- Artillery is the only weapon in the game with a _minimum_ range (5 tiles).
- Although artillery has maximum range 7, sensors must be activated to fire further than 5 tiles. Activating sensors costs an action and the duration of sensors enables only 2 consecutive artillery shots.
- Artillery can be fired in any direction.
- Due to the inability to blind-fire and the delay in landing shots, artillery shots can be easily dodged.
- Artillery shots cause splash damage to adjacent squares (including diagonally adjacent?)
- Artillery can not be reflected.
- `fireArtillery()` attempts to fire artillery at any enemy (if multiple enemies are within range, target is chosen based on previously set attack priority).
- `fireArtillery(entity)` can be used to fire artillery at a specific enemy (if you can sense it).
- `willArtilleryHit()` and `willArtilleryHit(entity)` return true if the corresponding `fireArtillery` is possible. Note that these will return true even if EMP has disabled your artillery. You will lose a turn if you attempt to fire artillery when it's not possible.


| Weapon                    | Damage        | Splash damage |
| --------------------------|:-------------:|:-------------:|
| Artillery I               | 250           | 10            |
| Artillery II              | 400           | 20            |
| Artillery III             | 500           | 30            |

## Zappers

- When activated, zapper creates an electric field around your bot, dealing damage to adjacent enemies.
- Diagonally adjacent enemies receive only 50% damage.
- Inferno Zapper ignites the target, causing 100 damage per turn for the duration of the ignition and causing a cloaked unit to become visible for the duration of the ignition (the cloak buff stays on, so the unit may become invisible after the ignition is over). Ignition persists across rounds.

| Weapon                 | Damage        | Duration | Cooldown | Special effect | Special duration  |
| -----------------------|:-------------:|:--------:|:--------:|:--------------:|:-----------------:|
| Zapper I               | 250           | 4        |     9    |    -           | -                 |
| Zapper II              | 300           | 5        |     9    |    -           | -                 |
| Zapper III             | 350           | 6        |     9    |    -           | -                 |
| Inferno Zapper I       | 100           | 3        |     8    |    Ignite      | 2                 |
| Inferno Zapper II      | 150           | 4        |     8    |    Ignite      | 2                 |
| Inferno Zapper III     | 150           | 5        |     8    |    Ignite      | 3                 |

## Landmines

- A bot can lay landmines under itself.
- A mine will explode when enemy steps on it or if its duration expires.
- There is some limit to the amount of mines a bot can lay before their earlier mines begin to disappear.
- There is some limit to the total amount of mines which can be on the battlefield at any time.
- Mines can not be directly detected by the enemy.
- You can not stack mines on the same tile.
- Landmines persist across rounds.

| Weapon                    | Damage        | Duration      |
| --------------------------|:-------------:|:-------------:|
| Landmines I               | 600           | 11            |
| Landmines II              | 600           | 14            |
| Landmines III             | 600           | 17            |

<!-- Line below is a hack to fix a whitespace issue. Do not remove. -->
##

---

## Cloaking

- When activated, makes the bot invisible (a bot can only cloak itself).
- Moving and attacking are possible while cloaked. Other actions will decloak you.
- While you are cloaked, your damage is reduced by 80%.
- Your enemy might decloak you by attempting to move or teleport into your tile.
- If a friendly unit attempts to teleport onto your tile, it will simply teleport into an adjacent free tile.
- Ignition makes you visible for the duration, but does not decloak you. This means you may become invisible again if the ignition wears off but the cloak remains. Inferno Zapper and Inferno Lasers can ignite bots.
- `canCloak()` returns true when the bot has cloaking hardware that is not on cooldown. Does not check if the bot is already cloaked. Does not check if EMP has disabled cloaking hardware.
- `isCloaked()` returns true when the bot is cloaked.
- `cloak()` activates cloak. If EMP has disabled cloaking, trying to activate cloak causes a turn to be lost.

| Support                    | Duration      | Damage reduction |
| ---------------------------|:-------------:|:----------------:|
| Cloaking I                 | 3             | 80%              |
| Cloaking II                | 4             | 80%              |
| Cloaking III               | 5             | 80%              |

## Regen

- Passively regenerates life each turn.

| Support                    | Heal          | 
| ---------------------------|:-------------:|
| Regen I                    | 10            |
| Regen II                   | 25            |
| Regen III                  | 50            |

## Teleport

- When activated, teleports you to the target location.
- Teleporting on top of a cloaked enemy unit will decloak it.
- `teleport(xTo, yTo)` attempts to teleport you to the target location, but if it is occupied, it attempts to teleport you to an adjacent tile (presumably only adjacent tiles within teleport range are considered).
- `canTeleport()` can be used to check if the teleport hardware is available and is not on cooldown. Note that although `canTeleport(xTo, yTo)` exists, it works a little bit unintuitively. It will return true when the corresponding teleport command will succeed in teleporting you somewhere. For example, if the target location is occupied, but teleporting to an adjacent location is possible, then the `teleport` command will succeed, so `canTeleport` will return true even though you can not teleport to the target location (only to an adjacent location). You can use `exists(getEntityAt(xTo, yTo))` to check if the target location is occupied (although it does not reveal cloaked units for you).
- Teleport can be disabled by EMP. You can not check if your teleport has been disabled. Using the teleport when it has been disabled causes you to lose a turn.

| Support                    | Range         | Cooldown |
| ---------------------------|:-------------:|:--------:|
| Teleport II                | 5             | 10       |

## Thrusters

- Passively increases haste-after-movement. Note that the haste bonus is applied only after movement, not after other actions.

| Support                    | Next turn haste bonus         |
| ---------------------------|:-----------------------------:|
| Thrusters I                | 17%                           |
| Thrusters II               | 34%                           |
| Thrusters III              | 50%                           |

## Reflect

- When activated, grants a chance to reflect missiles and lasers.
- A reflected missile or laser can be reflected onto any nearby enemy bot (not only to the bot which fired it).
- A missile or laser can not be reflected more than once (projectiles can not bounce between targets).

| Support                    | Reflect chance | Duration  | Cooldown |
| ---------------------------|:--------------:|:---------:|:--------:|
| Reflect I                  | 50%            | 4         | 9        |
| Reflect II                 | 65%            | 5         | 9        |
| Reflect III                | 75%            | 6         | 9        |

## Shield

- When activated, casts a shield on yourself or a nearby bot, chip or CPU (you can target the desired entity).
- A shield will absorb all damage up to a certain limit.
- Shields can be stacked infinitely.
- `shield()` shields yourself.
- `shield(entity)` can be used to shield another bot, chip or CPU.
- `canShield()` and `canShield(entity)` can be used to check if the above actions will be possible. However, they will return true even if EMP has disabled your shield hardware. Attempting to use a shield spends a turn even if shielding is not possible.

| Support                    | Damage absorbed | Duration  | Cooldown | Range |
| ---------------------------|:---------------:|:---------:|:--------:|:-----:|
| Shield I                   | 150             | 9         | 8        | 3     |
| Shield II                  | 300             | 12        | 8        | 4     |
| Shield III                 | 400             | 12        | 8        | 5     |

## Armor

- Passively decreases all incoming damage.

| Support                    | Damage reduction |
| ---------------------------|:----------------:|
| Armor I                    | 5%               |
| Armor II                   | 10%              |
| Armor III                  | 15%              |

## EMP

- When activated, disables the specified hardware for all enemies around you within range.
- If an enemy attempts to use the disabled hardware, they will lose their turn.
- The following hardware can be disabled: LASERS, MISSILES, MELEE, ARTILLERY, ZAPPER, REPAIR, CLOAKING, SHIELD, REFLECT, TELEPORT, LANDMINES, and EMP.
- Does not disable an effect which has been previously activated, only prevents the enemy from activating new effects. For example, if the enemy has already activated zapper, you can not disable it with your EMP.

| Support                    | Duration  | Cooldown | Range |
| ---------------------------|:---------:|:--------:|:-----:|
| EMP III                    | 2         | 8        | 5     |


## Repair

- When activated, heals yourself or a nearby bot, chip or CPU (you can target the desired entity).

| Support                    | Heal amount  | Range |
| ---------------------------|:------------:|:-----:|
| Repair I                   | 50           | 1     |
| Repair II                  | 100          | 1     |
| Repair III                 | 150          | 1     |

## Area Repair

- When activated, heals all allies within a certain range (is this targeted or does it repair everything aroudn you?)

| Support                    | Heal amount  | Range | Cooldown |
| ---------------------------|:------------:|:-----:|:--------:|
| Area Repair I              | 50           | 3     | 8        |
| Area Repair II             | 100          | 3     | 8        |
| Area Repair III            | 150          | 3     | 8        |

<!-- Line below is a hack to fix a whitespace issue. Do not remove. -->
##

---

## General information

- Although the game looks like bots are acting real-time, they are actually acting in turns.
- The order that you place your bots on the map defines the order in which they begin to act.
- Acting order is affected by haste (thrusters, haste chips, etc.) TODO explain better.
- Friendly fire is not possible.
- Matchmaking is restricted to players who have logged in during the past 3 days.
- Matchmaking prioritizes defenders who have not had a match in 5 hours (after a new version of the game is deployed, all players are prioritized).

| Entity        | Life          |
| --------------|:-------------:|
| Bot           | 2000          |
| Chip          | 4000          |
| CPU           | 12000         |

## Defense levels

- The defender can upgrade their defense after gaining experience. Upgrading is optional and downgrading is not possible.
- Arena size can be checked with `arenaWidth` and `arenaHeight`.

| Defense                    | Arena size | Defenders  | Attackers total (max per round) | Chips    |
| ---------------------------|:----------:|:----------:|:-------------------------------:|:--------:|
| Level 0                    | 11x7       |   3        |  6 (2)                          |  0       |
| Level 1                    | 13x9       |   6        |  7 (3)                          |  1       |
| Level 2                    | 15x11      |   9        |  8 (3)                          |  1       |
| Level 3                    | 15x13      |  10        | 10 (4)                          |  2       |
| Level 4                    | 17x13      |  11        | 11 (4)                          |  2       |
| Level 5                    | 19x13      |  12        | 12 (5)                          |  3       |
| Level 6                    | 19x13      |  13        | 13 (5)                          |  3       |
| Level 7                    | 19x13      |  14        | 14 (5)                          |  3       |
| Level 8                    | 19x13      |  15        | 16 (6)                          |  4       |
| Level 9                    | 19x13      |  16        | 17 (7)                          |  4       |
| Level 10                   | 19x13      |  18        | 19 (7)                          |  5       |

## Limitations

- Maximum script length is 16500 characters for Botlandscript and 99000 characters for Blockly.
- Action limit per round: 3000 opportunities-to-act in total from all bots on the map (currently there is no way to accurately gauge how close to the limit you are).
- There are two limits to computation time that can be expended by your bots. First, if an individual bot takes too long to act, it will miss a turn. Second, the total amount of computation time expended by your bots within a match can be roughly 1000ms; once that limit is reached your bots will simply do nothing for the remainder of the match.
- When you use arrays, you have to name them `array1` and `array2`. You can not use more than 2 arrays per bot. Arrays can have at most 100 elements.
- You can share information between bots by utilizing shared variables `sharedA` to `sharedE`.

---

## Top-level APIs

- `init()` is called once for each bot, at the beginning of a round.
- `update()` is called whenever your bot can act. Note that a turn may be skipped due to stun lasers and haste also affects acting order.

## Sharing information between bots

- The following variables are shared: `sharedA`, `sharedB`, `sharedC`, `sharedD`, `sharedE`.
- It's possible to share an array, but only `array1` and `array2` can be shared.
- Sharing information between bots is extremely brittle (due to the turn based nature of the game with haste effects, special shared variables, special array variables, variable scoping, and other limitations). Be very careful!

## Moving 

- `move()` attempts to move at random.
- `move(direction)` attempts to move your bot one tile in a given direction (string `'left'`, `'right'`, `'up'`, or `'down'`).
- `moveTo(xTo, yTo)` will calculate a path towards the target coordinates and attempt to move you one tile further down that path.
- `moveTo(entity)` will calculate a path towards the given entity and move your bot one tile towards the entity. If entity can not be sensed, this command fails (either wasting turn or causing a random movement).
- Calculating a path will fail if the entire path is not visible to the bot.
- `canMove()`, `canMove(direction)`, `canMoveTo(xTo, yTo)`, and `canMoveTo(entity)` check if the corresponding action should be possible. EMP can not be used to disable movement. However, a move action will fail if you attempt to move on a tile which is occupied by a cloaked enemy (the enemy will be decloaked and you will have spent your action).
- If you are attempting to move towards an entity or towards coordinates further than one tile away, and the shortest path is blocked, these commands may cause your bot to move _away_ from the given entity (following whichever shortest path it has calculated).
- If you want to minimize weird behavior, it's a good idea to avoid higher level APIs when moving. Instead, always move by explicitly declaring the tile where you want to move, e.g. `moveTo(x+1, y)`.
- `moveToMiddle` is an undocumented API. Assuming it does something related to its name, you will not need it.
- In addition to normal movement actions, a unit may move by teleporting or charging.

## Other useful APIs

- `x` and `y` contain coordinates for your bot.
- `moveTo(xTo, yTo)` 
- `getX(entity)` and `getY(entity)` return x and y coordinates for a given entity, given that your bot can sense it. The following syntax also works: `entity.x`, `entity.y`.
- `life` contains currently remaining hit points for your bot (`lifePercent` is also available).
- `getLife(entity)` and `getLifePercent(entity)` return the corresponding values for an entity if your bot can sense it.
- The following utility functions are available: `abs`, `floor`, `ceil`, `min`, `max`, `round`, `size` (length of array).
- `exists(entity)` will return true if the entity is not null and not undefined. `isDefined(entity)` also does the exact same thing.
- `canSense(entity)` will return true if your bot can sense the target entity. It returns true when the target entity is within vision range (5 or 7 tiles depending if sensors are activated). Blocking vision (line of sight) is not possible, only range matters. Cloaked enemies can only be sensed when they have been ignited. This API may be useful if you are saving entity references in variables (your bot may have previously sensed an entity and saved its reference to a variable, but it may be unable to sense it next turn -- or another bot may have shared an entity reference to a shared variable).

## Not-so-useful APIs

- `setAttackPriority(LITERAL)` can be used to set the priority in which your bots will attack in the narrow scenario _where there are multiple allowed targets of different types and you do not specify an attack target_. The default attack priority is `BOT_CHIP_CPU` and you probably will not want to change this (because your bots will be either "normal" bots which will be fine with this priority, or they will be CPU rushing bots, which will have hardcoded commands to attack the CPU specifically). Nonetheless, other possible permutations can be set, such as `CPU_BOT_CHIP`. Note that the values must be literals, not strings.
- `isAttacker` is true when you are the attacker.

## Undocumented APIs

TODO: document these APIs:

- `closestDistanceToWaypointAchieved`
- `
  "REDUCE_BY_MISSING_LIFE", 
  "ENEMY", 
  "IS_OWNED_BY_ME", 
  "CHIP", 
  "CPU", 
  "BOT", 
  "ANYTHING", 
  "SORT_BY_DISTANCE",
  "SORT_BY_LIFE",  
  "SORT_ASCENDING", 
  "SORT_DESCENDING",
  "canEMP",
  "canEmp",
  "canZap",
  "canReflect",
  "willRepair",
  "canActivateSensors",
  "canLayMine",
  "isCloaked",
  "isOnFire",
  "waypointExists",
  "isZapping",
  "areSensorsActivated",
  "isReflecting",
  "isShielded",
  "distanceTo",
  "getDistanceTo",
  "getEntityAt",
  "isEnemyMineAt",
  "percentChance",
  "randInt",
  "randomInteger",
  "willMoveWork",
  "isAdjacent",
  "filterEntities",
  "reduceEntities",
  "count",
  "findEntity",
  "findEntities",
  "findEntitiesInRange",
  "findClosestEnemyBot",
  "findClosestEnemyCpu",
  "findClosestFriendlyChip",
  "findClosestEnemyChip",
  "findClosestAlliedBot",
  "findMyCpu",
  "findMyClosestBot",
  "getNumMinesLaid",
  "add",
  "canSense",
  "canSenseEntity",
  "clampNumber",
  "checkTime",
  "figureItOut",
  "figureItOutDefense",
  "layMine",
  "emp",
  "EMP",
  "zap",
  "reflect",
  "activateSensors",
  "pursueBot",
  "pursueWaypoint",
  "revealMines",
  "pursue",
  "repair",
  `

<!-- Line below is a hack to fix a whitespace issue. Do not remove. -->
##

---

## Open questions

- Is ignition damage affected by cloak damage reduction?
- Can a bot sense friendly bots if they are cloaked?

## Related links

- [Open-sourced bots by mizzao, one of the top competitors](http://github.com/mizzao/bot.land)
- [Bot Land minifier by Ron](https://github.com/rondlite/botland-minifier)
- [ESLint Bot Land plugin by freaktechnik](https://www.npmjs.com/package/eslint-plugin-botland)
- [Youtube channel Adam13531, the developer of Bot Land](https://www.youtube.com/channel/UCJFxRNHar-c_lKYxFMIPg_g)