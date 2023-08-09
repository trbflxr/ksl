# KSL extension development guide

> [!IMPORTANT]  
> At this point you already should have KSL [SDK](https://github.com/trbflxr/ksl_sdk) downloaded and configured [project](setup_project.md).
>
> Also your extension must be **registered** and you should have already **generated a key** for the maykr. Additional information [here](https://github.com/trbflxr/ksl/blob/master/doc/guide/dev/control_panel.md).

Here is a list of steps to start extension development:

1. Create an [entrypoint](#entry-point-creation)
2. Setup extension [metadata](#metadata-setup)
3. Setup extension [UI](#setup-ui)
4. Set custom [icon](#set-extension-icon)

## Entry point creation

Create an entrypoint class and extend it from [BaseExtension](https://github.com/trbflxr/ksl/blob/master/doc/api/base_extension.md).

```c#
public class ExampleExtension : BaseExtension {
  ...
}
```

> [!NOTE]  
> Keep in mind that [BaseExtension](https://github.com/trbflxr/ksl/blob/master/doc/api/base_extension.md) class are **not** inherited from MonoBehaviour. You can override methods from BaseExtension which represents event methods from MonoBehaviour.
>
> In case if you need for an example need MonoBehaviour to run a coroutine you can use [Behaviour](https://github.com/trbflxr/ksl/blob/master/doc/api/base_extension.md#behaviour) property of BaseExtension.

## Metadata setup

Add to the entrypoint class attribute [KSLMeta](https://github.com/trbflxr/ksl/blob/master/doc/api/ksl_meta.md).

```c#
[KSLMeta("ExampleExt", "1.0.0", "trbflxr")]
public class ExampleExtension : BaseExtension {
  ...
}
```

At this point your extension can be loaded by KSL.

## Setup UI

To create UI for the extension you can use [KSL.UI](https://github.com/trbflxr/ksl/blob/master/doc/api/ui.md) or default UnityEngine.IMGUIModule.

```c#
[KSLMeta("ExampleExt", "1.0.0", "trbflxr")]
public class ExampleExtension : BaseExtension {
  public override void OnUIDraw() {
    Kino.UI.Label("Wellcome to ExampleExtension!");
    if (Kino.UI.Button("Press me")) {
      Kino.Log.Info("Pressed");
    }
  }

  public override void OnAdditionalAboutUIDraw() {
    Kino.UI.Label("Additional about info...");
    Kino.UI.HyperlinkLabel("Visit our<link>", "discord", "https://discord.gg/kinomod");
  }
}
```

## Set extension icon

To make the extension unique it's recommended to set a custom icon for it.

You can ship the icon with the extension and load it directly from the disc but it's recommended to embed it into the extension itself.

```c#
[KSLMeta("ExampleExt", "1.0.0", "trbflxr")]
public class ExampleExtension : BaseExtension {
  public override Texture2D GetIcon() {
    var assembly = Assembly.GetExecutingAssembly();
    return Kino.Utils.LoadEmbeddedTexture(assembly, "Example.Resources.icon.png");
  }
}
```

In this example **icon.png** is added as an **embedded resource** to the ExampleExtension project.

```xml

<Project>
	...
	<ItemGroup>
		<Compile.../>
	</ItemGroup>
	<ItemGroup>
		<EmbeddedResource Include="Resources\icon.png"/>
	</ItemGroup>
</Project>
```

## Example project

You can check an example project in the KSL [SDK](https://github.com/trbflxr/ksl_sdk) repository for more info.
