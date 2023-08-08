# KSL Utility methods

### LoadEmbeddedTexture

```c#
public Texture2D LoadEmbeddedTexture(Assembly assembly, string path);
```

This method allows you to load an image from .dll embedded resources.

> Arguments:
> * Assembly **assembly** - current executing assembly
> * string **path** - path to embedded resource including namespace

Example:

```c#
public override Texture2D GetIcon() {
  var assembly = Assembly.GetExecutingAssembly();
  return Kino.Utils.LoadEmbeddedTexture(assembly, "KSL.CarX.Resources.icon.png");
}
	
```

### OpenFilePicker

```c#
public void OpenFilePicker(string title, string pickInFolder, Action<string> onFileSelected, string[] allowedExtensions = null);
```

This method allows you to open file picker context for selected folder. Also you can set file extension filters.

> Arguments:
> * string **title** - title of the file picker context
> * string **pickInFolder** - folder where files should be searched
> * Action<string> **onFileSelected** - this callback will be called on file selection
> * string[] **allowedExtensions** - optional file extension filter
    
Example usage:

```c#
public override void OnUIDraw() {
  if (UI.Button("Select mod")) {
    Kino.Utils.OpenFilePicker("Mods", Paths.Mods, OnFileSelected, new[] { ".dll" });
  }
}

private void OnFileSelected(string filePath) {
  Kino.Log.Info($"Selected file: {filePath}");
}
```