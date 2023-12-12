# Movement & Actions

Movement and actions in The Cartographer are semi-turn based.  Each entity has a speed, which determines on which game tick that entity can act.  Lower speed means faster, and that entity can act on each game tick which is divisible by its speed.
> Emit signal: GameTick(CurrentGameTick)
> if Object has function "ActionCounter":
>   Object.ActionCounter(CurrentGameTick)

> func ActionCounter(CurrentGameTick)
>  export var Speed
>  var ActionGoNogo
>  ActionGoNogo = CurrentGameTick MODULO(Speed)
>  if ActionGoNogo = 0:
>    ObjectMainActionFunction()
>  else:
>    Pass

If the player's speed lands on the same tick as another entity, the player always goes first.  If multiple enemies land on the same tick, generate a random initiative table for all entities currently loaded.  (Arbitrary max: 256) Store this table in a singleton for the local area (LocalState.gd) And be sure to remove the entry when the entitiy is freed

> var InitiativeCount
> func _onready()
>   LocalState.AssignInitiativeEntry(node-unique-name)
>   InitiativeCount = LocalState.GetInitiativeEntry(node-unique-name)
>
> Func _onfree()
>   LocalState.UnloadInitiativeEntry(node-unique-name)
