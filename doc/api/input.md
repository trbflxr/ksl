# Input manager

Input manager interface used to create re-bindable keybind.

## Bind

There is two variants of this method: for single key and for key combination (4 keys max).

```c#
public int Bind(KeyCode key, Action action, string displayName = null, ActionType actionType = ActionType.Pressed);
public int Bind(KeyCode[] keys, Action action, 	string displayName = null, ActionType actionType = ActionType.Pressed);
```

> [!NOTE]  
> Arguments:
> * KeyCode **key** / KeyCode[] **keys** - default bind key or key combination; it can be changed in the mod settings later
> * Action **action** - an action that will be called
> * string **displayName** - optional name of the keybind that will be displayed in the settings
> * ActionType **actionType** - optional action type when the callback should be called (**Pressed**, **Released** or **Hold**) by default it's **Pressed**

Example usage:

```c#
public override void OnStart() {
  Kino.Input.Bind(KeyCode.Space, Jump, "Jump");

  Kino.Input.Bind(KeyCode.W, MoveForward, "Move forward", ActionType.Hold);
}
```

## SetSuppressInput

> [!WARNING]  
> Be really careful with it because this method will suppress all KSL input if **true** passed.

For example if user has selected the chat window in the game and starts typing, **SetSuppressInput** should be called with **true** to suppress KSL input. After the chat is no longer active (in focus) call **SetSuppressInput** with **false** to unlock the input.

This method mainly designed for use in KSL extensions, but you can access it from the mods as well.

Example usage:

```c#
// Lock input when chat window is focused
private void OnChatActivated() {
  Kino.Input.SetSuppressInput(true);
}

// Unlock input when chat window is unfocused
private void OnChatDeactivated() {
  Kino.Input.SetSuppressInput(false);
}
```
