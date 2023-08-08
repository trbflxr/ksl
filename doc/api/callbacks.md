# KSL Callbacks

### OnMessage

Subscribe to this callback to get KSL info messages.

```c#
public event Action<string> OnMessage;
```

Example for CarX:

```c#
// MyExtension
public override void OnStart() {
  Kino.Callbacks.OnMessage += OnMessage;
}

public override void OnDestroy() {
  Kino.Callbacks.OnMessage -= OnMessage;
}

// Display all KSL messages in CarX message popup
private void OnMessage(string message) {
  GUICommonGodVoice.ShowText($"KSL: {message}");
}
```