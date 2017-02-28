```
title: "FlxAction"
apiPath: FlxAction.html
```

```haxe
import flixel.input.actions.FlxAction;
```

FlxActions are blah blah

Temporary FlxActionManager note dump:

/**
 * High level input manager for `FlxAction`s. This lets you manage multiple input
 * devices and action sets, and is the only supported method for natively
 * handling Steam Controllers.
 * 
 * If you are only using Mouse/Keyboard/Gamepad controls for a fairly simple
 * game, this might be overkill, but if you have more complex needs, are
 * supporting the Steam Controller natively, or need robust and flexibile
 * user-customizable inputs, this is the class for you.
 * 
 * OVERVIEW
 * =============
 * 
 * There are four items to consider:
 * 
 * - `FlxAction`
 * - `FlxActionInput`
 * - `FlxActionSet`
 * - `FlxActionManager`
 * 
 * The PLAYER cares about ACTIONS:
 * Mario JUMPS, Samus SHOOTS, Captain Falcon TURNS, BRAKES, and ACCELERATES.
 *
 * The COMPUTER cares about INPUTS:
 * The W key is PRESSED. The Left Mouse button was JUST_RELEASED. Gamepad #2's
 * analog stick is MOVED with values (x=0.4,y=-0.5).
 *
 * The DESIGNER cares about ACTION SETS:
 * Different parts of the game might need different controls. You (usually)
 * can't JUMP or SHOOT in a store menu, but you CAN perform actions like
 * MENU_UP, MENU_DOWN, MENU_LEFT, MENU_RIGHT, BACK, and SELECT.
 * 
 * 1. `FlxAction`s
 * =============
 * 
 * `FlxAction`s come in two varieties: Digital and Analog. You can only create
 * `FlxActionDigital` and `FlxActionAnalog`. Digital is for on/off actions like
 * JUMP and SHOOT. Analog is for things that need a range of values, like
 * jumping with more or less force, or moving a player or camera around.
 * 
 * This lets you just check for: `if(SHOOT.check())` in your update loop 
 * rather than some hand-rolled custom input code.
 * 
 * `FlxAction`s don't do anything until you attach `FlxActionInput`s do them.
 * 
 * 2. `FlxInput`s
 * =============
 * 
 * `FlxActionInput`s are divided into digital and analog types, as well as by
 * the kind of input device they use:
 * 
 * - `FlxActionInputDigitalKeyboard`
 * - `FlxActionInputDigitalMouse`
 * - `FlxActionInputDigitalGamepad`
 * - `FlxActionInputAnalogMouse`
 * - `FlxActionInputAnalogGamepad`
 * 
 * Create a `FlxActionInput` subclass with the input values you want, then call
 * `myAction.addInput(myInput)` to attach it to an action. You can only add
 * digital inputs to digital actions and analog inputs to analog actions.
 * 
 * For digital actions that only have mouse, keyboard, and gamepad input,
 * you're done. You can now call `myAction.check()` in your update loop to 
 * see if it has fired and then act upon it.
 * 
 * It's best to call `update()` on all of your actions in your update loop
 * before checking them, but this is strictly speaking only necessary for:
 *
 * - analog actions (to get proper `JUST_MOVED` / `JUST_STOPPED` values)
 * - if you want the `.fire` property to update every frame
 * - actions (digital or analog) with steam controller input
 *
 * 3. `FlxActionSet`
 * ===============
 * 
 * `FlxActionSet`s are little more than glorified arrays of `FlxAction`s. There's
 * little reason to use them directly unless you are using `FlxActionManager`,
 * but they can still be a convenient way to call update() on all your actions
 * at once.
 * 
 * 4. `FlxActionManager`
 * ===================
 * 
 * `FlxActionManager` lets you manage multiple action sets. When you are using
 * this class, only ONE action set is considered active at a given time for
 * any given device, but multiple devices can be subscribed to the same action
 * set.
 * 
 * For instance, in an asymetrical co-op game where one person drives a tank
 * and the other mans the turret, gamepad #1 could use action set "drive" and
 * gamepad #2 could use action set "gunner". The same could go for the mouse,
 * the keyboard, etc. And in a single-player game you might want to just change
 * the action set of ALL input devices every time you switch to a different
 * screen, such as a menu.
 * 
 * `FlxActionManager` lets you:
 * - ADD action sets
 * - REMOVE action sets
 * - ACTIVATE an action set for a specific device.
 * - UPDATE all your action sets at once
 * - ENFORCE the "only one action set active per device at a time" rule
 * 
 * Once you've set up `FlxActionManager`, you can let flixel handle it globally
 * with: `FlxG.inputs.add(myFlxActionManager)`;
 * 
 * If you don't add it globally, you will have to call `update()` on it yourself.
 * 
 * If you are using the steamwrap library, `FlxActionManager` gains the ability
 * to automatically create action sets from a steamwrap object derived from the
 * master vdf game actions file that Steam makes you set up for native
 * controller support. You must then ACTIVATE one of those action sets for any
 * connected steam controllers, which will automatically attach the proper
 * steam action inputs to the actions in the set. You can also add as many 
 * regular `FlxActionInput`s as you like to any actions in the sets.
 * 
 * NOTE:
 * If you are using a Steam Controller, you MUST use `FlxActionManager` in order
 * to properly process the Steam Controller API via `FlxAction`s. The only other
 * alternative is to call the steamwrap functions directly.
 * 
 */
