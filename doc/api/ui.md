# UI API

## UI

KSL UI interface. Use it to draw the UI with KSL styles.

### Getters

#### IsVisible

```c#
public bool IsVisible { get; }
```
Getter for current KSL UI visible state.

---

#### IsMouseOver

```c#
public bool IsMouseOver { get; }
```
Getter for mouse over state. Return **true** if the mouse is hovering over KSL UI.

---

#### Scale

```c#
public float Scale { get; }
```

Current UI scale.

---

#### DefaultSkin

```c#
public GUISkin DefaultSkin { get; }
```

Default Unity UI skin.

---

### Methods

---

#### PushContext

```c#
public void PushContext(Action contextUI, string contextName = null);
```

Method allows you to push new context to the stack. Call it with UI function and optional (but recommended) context name specified.

> Arguments:
> * Action **contextUI** - a context UI function that should be called
> * string **contextName** - optional name of the context

Example usage:

```c#
public override void OnUIDraw() {
  if (Kino.UI.ContextButton("Settings")) {
    Kino.UI.PushContext(UISettingsContext, "Mod settings");
  }
}

// Context UI function
private void UISettingsContext() {
  Kino.UI.Label("Mod settings");
  Kino.UI.Toggle("Setting0", ref setting0Active_);
}
```

---

#### PopContext

```c#
public void PopContext();
```

Method needed to pop context from the stack. If the stack is empty it will open KSL main menu.

Example:

```c#
public override void OnUIDraw() {
  if (Kino.UI.Button("Go back")) {
    Kino.UI.PopContext();
  }
}
```

---

#### BeginHorizontal, EndHorizontal, BeginVertical, EndVertical

```c#
public void BeginHorizontal();
public void EndHorizontal();
public void BeginVertical();
public void EndVertical();
```

Those methods are used to draw layout groups. Works on the same principals as Unity methods.

Also you can use [Group](#group-enum) parameter to specify the elements' margins.

Example:

```c#
public override void OnUIDraw() {
  // Horizontal group
  Kino.UI.BeginHorizontal();
  Kino.UI.Button("Left button");
  Kino.UI.Button("Right button");
  Kino.UI.EndHorizontal();

  // Vertical group
  Kino.UI.BeginVertical();
  Kino.UI.Button("Top button");
  Kino.UI.Button("Bottom button");
  Kino.UI.EndVertical();

  // Horizontal group with two vertical groups in it
  Kino.UI.BeginHorizontal();

  // Left vertical group
  Kino.UI.BeginVertical();
  Kino.UI.Label("Left group label");
  Kino.UI.Button("Left button");
  Kino.UI.EndVertical();

  // Right vertical group
  Kino.UI.BeginVertical();
  Kino.UI.Label("Right group label");
  Kino.UI.Button("Left button");
  Kino.UI.EndVertical();

  Kino.UI.EndHorizontal();

  // Horizontal group with margins specefied
  Kino.UI.BeginHorizontal();
  Kino.UI.Button("Left button", Group.HLeft);
  Kino.UI.Button("Middle button", Group.HRight);
  Kino.UI.Button("Right button", Group.HMiddle);
  Kino.UI.EndHorizontal();
}
```

---

#### HorizontalLine

```c#
public void HorizontalLine();
```

Draw a horizontal separator line.

Example:

```c#
public override void OnUIDraw() {
  Kino.UI.HorizontalLine();
}
```

---

#### Spacer

```c#
public void Spacer();
```

Add spacer to UI.

Example:

```c#
public override void OnUIDraw() {
  Kino.UI.Button("Top button");
  Kino.UI.Spacer();
  Kino.UI.Button("Bottom button");
}
```

---

#### Label

```c#
public void Label(string text);
```

This method will draw a label with text aligned to left side.

> Parameters:
> * string **text** - label text

Example usage:

```c#
public override void OnUIDraw() {
  Kino.UI.Label("Hello from KSL!");
}
```

---

#### GroupLabel

```c#
public void GroupLabel(string text);
```

This method will draw a label with text aligned to the left side but slightly shifted and without the bottom margins to mark element groups.

> Parameters:
> * string **text** - label text

Example usage:

```c#
public override void OnUIDraw() {
  Kino.UI.Label("Group name");
  Kino.UI.Button("Button", Group.VFirst);
  Kino.UI.Toggle("Toggle 0", ref toggle0_, Group.VMiddle);
  Kino.UI.Toggle("Toggle 1", ref toggle1_, Group.VLast);
}
```

---

#### Hyperlink

```c#
public void Hyperlink(string text, string url, Tooltip tooltip = null);
public void Hyperlink(string text, Action callback, Tooltip tooltip = null);
```

This method is used to draw hyperlinks with ability to execute a callback or open an URL.

> Parameters for the hyperlink with a URL:
> * string **text** - hyperlink text
> * string **url** - URL to open
> * Tooltip **tooltip** - optional [tooltip](#tooltip-class)

> Parameters for the hyperlink with a callback:
> * string **text** - hyperlink text
> * Action **callback** - the callback that will be called
> * Tooltip **tooltip** - optional [tooltip](#tooltip-class)

Example usage:

```c#
public override void OnUIDraw() {
  Kino.UI.Hyperlink("Google", "https://google.com");

  Kino.UI.Hyperlink("Log something", () => {
    Kino.Log.Info("Logging something");
  });
}
```

---

#### HyperlinkLabel

```c#
public void HyperlinkLabel(string format, string linkText, string url, Tooltip tooltip = null);
public void HyperlinkLabel(string format, string linkText, Action callback, Tooltip tooltip = null);
```

This method allows to create a label with a hyperlink in it. Useful to create text with properly aligned hyperlinks.

> Parameters for hyperlink with URL:
> * string **format** - string format that should include **<![CDATA[<link>]]>** in order to have hyperlink
> * string **linkText** - hyperlink text that will replace **<![CDATA[<link>]]>** in **format**
> * string **url** - URL to open
> * Tooltip **tooltip** - optional [tooltip](#tooltip-class)

> Parameters for hyperlink with callback:
> * string **format** - string format that should include **<![CDATA[<link>]]>** in order to have hyperlink
> * string **linkText** - hyperlink text that will replace **<![CDATA[<link>]]>** in **format**
> * Action **callback** - the callback that will be called
> * Tooltip **tooltip** - optional [tooltip](#tooltip-class)

Example usage:

```c#
public override void OnUIDraw() {
  Kino.UI.HyperlinkLabel("Check out <link> project!", "KSL example", "https://github.com/trbflxr/ksl_sdk");

  Kino.UI.HyperlinkLabel("Log <link>", "something", () => {
    Kino.Log.Info("Logging something");
  });
}
```

---

#### Button

```c#
public bool Button(string text, Group group = Group.Single, bool active = false, Tooltip tooltip = null);
```

This method is used to draw text buttons with text aligned to middle.

> Parameters:
> * string **text** - button text
> * Group **group** - optional [group](#group-enum)
> * bool **active** - optional flag to set the button look pressed down
> * Tooltip **tooltip** - optional [tooltip](#tooltip-class)
>
> Return: **true** if the button is pressed

Example usage:

```c#
public override void OnUIDraw() {
  if (Kino.UI.Button("Press me!")) {
    Kino.Log.Info("You just pressed the button");
  }
}
```

---

#### ContextButton

```c#
public bool ContextButton(string text, Group group = Group.Single, Tooltip tooltip = null);
```

This method is used to draw text buttons with text aligned to left side and with an arrow at the right. Useful to create navigation buttons to make end-user know that this button will open a different context.

> Parameters:
> * string **text** - button text
> * Group **group** - optional [group](#group-enum)
> * Tooltip **tooltip** - optional [tooltip](#tooltip-class)
>
> Return: **true** if the button is pressed

Example usage:

```c#
public override void OnUIDraw() {
  if (Kino.UI.ContextButton("Settings")) {
    Kino.UI.PushContext(UISettingsContext, "Mod settings");
  }
}

private void UISettingsContext() { ... }
```

---

#### Toggle

```c#
public bool Toggle(string text, ref bool active, Group group = Group.Single, Tooltip tooltip = null);
```

Toggle switch with a label and a small toggle button.

> Parameters:
> * string **text** - toggle label text
> * **ref** bool **active** - ref to a bool flag that represent the toggle activity
> * Group **group** - optional [group](#group-enum)
> * Tooltip **tooltip** - optional [tooltip](#tooltip-class)
>
> Return: **true** if the element was toggled

Example usage:

```c#
public override void OnUIDraw() {
  if (Kino.UI.Toggle("Toggle 0", ref toggle0_)) {
    Kino.Log.Info("Toggle 0 was toggled -_-");
  }

  Kino.UI.Toggle("Toggle 1", ref toggle1_);
}
```

---

#### Slider

```c#
public bool Slider(ref float value, float min, float max, string text, Group group = Group.Single, Tooltip tooltip = null);
```

This method used to draw a slider with a label.

> Parameters:
> * **ref** float **value** - ref to slider value
> * float **min** - min. value
> * float **max** - max. value
> * string **text** - display text
> * Group **group** - optional [group](#group-enum)
> * Tooltip **tooltip** - optional [tooltip](#tooltip-class)
>
> Return: **true** if the value has changed

Example usage:

```c#
public override void OnUIDraw() {
  if (Kino.UI.Slider(ref volume_, 0.0f, 1.0f, $"Volume: {volume_:F1}")) {
    Kino.Log.Info($"Volume changed to: {volume_}");
  }
}
```

---

#### SliderWithButtons

```c#
public bool SliderWithButtons(ref float value, float min, float max, float step, string text, Group group = Group.Single, Tooltip tooltip = null);
```

This method is used to draw more advanced sliders with **+** and **-** buttons. And with a fixed value step that will be added or subtracted by dragging the slider or clicking the buttons.

> Parameters:
> * **ref** float **value** - ref to slider value
> * float **min** - min. value
> * float **max** - max. value
> * float **step** - step that will be added or subtracted by clicking the buttons and dragging the slider
> * string **text** - display text
> * Group **group** - optional [group](#group-enum)
> * Tooltip **tooltip** - optional [tooltip](#tooltip-class)
>
> Return: **true** if the value has changed

Example usage:

```c#
public override void OnUIDraw() {
  if (Kino.UI.SliderWithButtons(ref volume_, 0.0f, 1.0f, 0.1f,$"Volume: {volume_:F1}")) {
    Kino.Log.Info($"Volume changed to: {volume_}");
  }
}
```

---

#### Input

```c#
public bool Input(ref string value, int maxLength = -1, string regex = null, Group group = Group.Single, Tooltip tooltip = null);
```

This method is used to draw a text input field with optional max. length and regex.

> Parameters:
> * **ref** string **value** - ref to a string value
> * int **maxLength** - optional max. text length
> * string **regex** - optional regex to validate **value**
> * Group **group** - optional [group](#group-enum)
> * Tooltip **tooltip** - optional [tooltip](#tooltip-class)
>
> Return: **true** if the value has changed

Example usage:

```c#
public override void OnUIDraw() {
  if (Kino.UI.Input(ref textValue_)) {
    Kino.Log.Info($"Text value changed to: {textValue_}");
  }
}
```

---

#### ListView

```c#
public void ListView<T>(ref Vector2 scrollPos, float visibleHeight, IEnumerable<T> items, Action<int, T> itemIterator);
```

This method allows to draw a List view component from a list of items. This method will call a draw callback for each item in the list so you can control how it should be drawn.

> Parameters:
> * **ref** Vector2 **scrollPos** - ref to Vector2 scroll position
> * float **visibleHeight** - visible list height. It will be scaled depending on KSL [UI.Scale](#scale)
> * List<T> **items** - the list of items to display
> * Action<int, T> **drawCallback** - item draw callback it will be called for each item; here you can specify how to draw the item

Example usage:

```c#
public override void OnUIDraw() {
  // Draw a list of strings (List<string> list_)
  Kino.UI.ListView(ref scrollPos_, 100.0f, list_, (index, str) => {
    if (Kino.UI.Button(str)) {
      Kino.Log.Info($"Selected {str} with index {index}");
    }
  });
}
```

---

## Tooltip class

Tooltip class. Can be created implicitly from a string.

Fields:

* **Text** - Tooltip text
* **SingleLine** - Should tooltip be single lined
* **CustomWidth** - Allows you to explicitly specify tool tip width. It will be scaled depending on KSL UI.Scale

Example usage:

```c#
// Implicit tooltip creation from a string
if (Kino.UI.Button("Log message", tooltip: "Log the message using KSL logger")) {
  Kino.Log.Info("Message");
}

// Single lined tooltip
if (Kino.UI.Button("Log message", tooltip: new Tooltip { Text = "Log the message using KSL logger", SingleLine = true })) {
  Kino.Log.Info("Message");
}

// Tooltip with width of 150 (scaled) pixels
if (Kino.UI.Button("Log message", tooltip: new Tooltip { Text = "Log the message using KSL logger", CustomWidth = 150.0f })) {
  Kino.Log.Info("Message");
}
```

## Group enum

This enum is used to specify element group. It basically controls the margins around the element.
Have a closer look in the KSL [example project](https://github.com/trbflxr/ksl_sdk).

* **Single** - _Single_ element, with equal margins on each side
* **VFirst** - _First_ element in _VERTICAL_ group
* **VMiddle** - _Middle_ element in _VERTICAL_ group
* **VLast** - _Last_ element in _VERTICAL_ group
* **HLeft** - _First_ element in _HORIZONTAL_ group
* **HMiddle** - _Middle_ element in _HORIZONTAL_ group
* **HRight** - _Last_ element in _HORIZONTAL_ group
