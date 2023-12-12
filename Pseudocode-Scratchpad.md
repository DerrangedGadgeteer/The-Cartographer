# Movement & Actions

Movement and actions in The Cartographer are semi-turn based.  Each entity has a speed, which determines on which game tick that entity can act.  Lower speed means faster, and that entity can act on each game tick which is divisible by its speed.
```
 Emit signal: GameTick(CurrentGameTick)      # DEPRECATED
 if Object has function "ActionCounter":     # DEPRECATED
   Object.ActionCounter(CurrentGameTick)     # DEPRECATED
```
```
 func ActionCounter(CurrentGameTick)
  export var Speed
  var ActionGoNogo
  ActionGoNogo = CurrentGameTick MODULO(Speed)
  if ActionGoNogo = 0:
    ObjectMainActionFunction()
  else:
    Pass
```
If the player's speed lands on the same tick as another entity, the player always goes first.  If multiple enemies land on the same tick, generate a random initiative table for all entities currently loaded.  (Arbitrary max: 256) Store this table in a singleton for the local area (LocalState.gd) And be sure to remove the entry when the entitiy is freed
```
 var InitiativeCount
 func _onready()
   LocalState.AssignInitiativeEntry(node-unique-name)
   InitiativeCount = LocalState.GetInitiativeEntry(node-unique-name)

 Func _onfree()
   LocalState.UnloadInitiativeEntry(node-unique-name)
```
Note: Nonplayer Entities need a way to hold the LocalState at a particular Initiative Entry
```

```
# Animations

Animations use the built-in "Delta" processes

# Collision Detection

Objects with collision have circular collision shapes, 

Entities with movement have eight raycast2d children in the eight directions to the midpoint of each adjacent square.  these detect colliders for movement, detect objects and entities for interaction, and detect valid targets for direct attack.  Depending on which commands are issued by the controller, the relevant ray is checked for collision, then its collider is checked for any functions that trigger on interaction, then whichever relevant action is carried out.  
```
func MovementCommandFromController(direction-for-ray)
 var MoveGoNogo = get_child(direction-for-ray).is_colliding()
 if MoveGoNogo = true
  var BumpedObject = get_shild(direction-for-ray).get_collider()
  if BumpedObject has function "OnBumped":
   BumpedObject.OnBumped(self)
  else:
   BumpAnimation.Play()
 else:
  MoveSelf(direction-for-ray)
```

# Ranged Attack Collision Detection

Ranged Attacks are made against squares selected independantly of collision, however there is a chance for objects with collision to be hit inadvertently if they're in the path of the projectile. (Including a chance of overshooting on a miss)  
- We construct a raycast from the center of the attacker to the center of the target.
 - (On a miss, we duplicate, then normalize it, and relocate the start of it to the center of the target for calculating overshoot)
- We then get all other colliders on that ray,
- order them by ascending distance from the player,
- weight them by their evasion stat,
- and calculate a chance to accidentally hit them on the way to the target.
- If an intervening collider is hit, the attack is made against that object instead.
- If not, the attack is made against the target's evasion like a direct attack.
- If the target is missed as well, we use the unit ray calculated earlier 

# Animation (Movement)
```
var velocity = Vector2.ZERO
var movecountdown = 0           # clamps movement into chunks

func _process(delta)
 if movecountdown = 0:          # Snap position to nearest grid square once movement is done
  var xsnap = position.x / 32
  position.x = xsnap.round() * 32
  var ysnap = position.y / 32
  position.y = ysnap.round() * 32
  velocity = ZERO
 else:                          # Move the entity along the direction, and decrement the countdown
  position += velocity * delta
  movecountdown = movecountdown - 1
  sound.play(footstep)

func MoveSelf(direction)        # When a controller commands an entity to move, set the velocity per the
 velocity = direction           # direction raycast, and set the movement end countdown so it doesn't go on forever
 var distance = 32 * direction.length()
 movecountdown = distance.round()
```

# Controller

I'm thinking of using a separate node to translate between either player controls, multiplayer remote controls, and AI's, and actually moving entities in the game world.  That way I divorce the game entities from the means of controling them.

First: Game Ticks need a singleton, and when the player's game tick comes up, the player controller needs to hold the game until an input is selected.  (copied from above)

```
 func ActionCounter(CurrentGameTick)
  export var Speed
  var ActionGoNogo
  ActionGoNogo = CurrentGameTick MODULO(Speed)
  if ActionGoNogo = 0:
    ObjectMainActionFunction()
  else:
    Pass
```
```
func _on-Gametick-signal-recieved(Gametick)
 ActionCounter(Gametick)
```
```
func ObjectMainActionFunction()
 LocalState.Holdup()
 input.parser # Parse Input &Translate to game object command
 ControlledObject.Action(RequestedAction,Arguments)

 LocalState.Release()  # Upon resolution of the Controlled object action
```
Back in the LocalState Singleton:
```
export var gametick = 0
export var Initiative = 0
func _process(delta)
 if HOLD = false,
  for Entry in InitiativeTable:
   Initiative = Entry
   Signal Initiative.emit(Initiative)
   await InitiativeRelease() # Note: Coroutine here, need to actually play with it a bit.
  gametick = gametick +1
  Signal Gametick.emit(gametick)
 
func Holdup()
 HOLD = true

func Release()
 HOLD = false  
```
In the case of a Nonplayer Controller:
```
var Initiative
var CurrentGametick
var Speed

func _onready()
 Initiative = Localstate.AssignInitiative(self)
 Instantiate.sprites& # WhateverOtherStuff

func _on-Initiative-signal-recieved(CurrentInitiativeCount)
 if CurrentInitiativeCount = Initiative:
  LocalState.InitiativeHold()
  ActionCounter(CurrentGametick)
  Localstate.InitiativeRelease()
 else:
  pass

func _on-Gametick-signal-recieved(Gametick)
 CurrentGametick = Gametick

 func ActionCounter(CurrentGameTick)
  var ActionGoNogo
  ActionGoNogo = CurrentGameTick MODULO(Speed)
  if ActionGoNogo = 0 
    ObjectMainActionFunction()
  else:
    Pass
```
