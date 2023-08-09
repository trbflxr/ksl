# KSL mod development guide

> [!IMPORTANT]  
> At this point you already should have KSL [SDK](https://github.com/trbflxr/ksl_sdk) downloaded and configured [project](https://github.com/trbflxr/ksl/blob/master/doc/guide/dev/setup_project.md).
>
> Also your mod must be **registered** and you should already **generated a key** for the maykr. Learn more about it [here](https://github.com/trbflxr/ksl/blob/master/doc/guide/dev/control_panel.md).

Here is list of steps to start mod development:

1. Create an [entrypoint](#entry-point-creation)
2. Setup mod [metadata](#metadata-setup)
3. Setup mod [UI](#setup-ui)
4. Set custom [icon](#set-mod-icon)

## Entry point creation

Create an entrypoint class and extend it from [BaseMod](https://github.com/trbflxr/ksl/blob/master/doc/api/base_mod.md).

```c#
public class ExampleMod : BaseMod {
  ...
}
```

> [!NOTE]  
> Keep in mind that [BaseMod](https://github.com/trbflxr/ksl/blob/master/doc/api/base_mod.md) class inherited from MonoBehaviour and you can use all Unity event functions in it.

## Metadata setup

Add to the entrypoint class a [KSLMeta](https://github.com/trbflxr/ksl/blob/master/doc/api/ksl_meta.md) attribute.

```c#
[KSLMeta("ExampleMod", "1.0.0", "trbflxr")]
public class ExampleMod : BaseMod {
  ...
}
```

At this point your mod can be loaded by KSL.

## Setup UI

To create the UI for the mod you can use [KSL.UI](https://github.com/trbflxr/ksl/blob/master/doc/api/ui.md) or default UnityEngine.IMGUIModule.

```c#
[KSLMeta("ExampleMod", "1.0.0", "trbflxr")]
public class ExampleMod : BaseMod {
  public override void OnUIDraw() {
    Kino.UI.Label("Wellcome to ExampleMod!");
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

## Set mod icon

To make the mod unique it's recommended to set custom icon for it.

You can ship the icon with the mod and load it directly from the disc but it's recommended to embed it into the mod itself.

```c#
[KSLMeta("ExampleMod", "1.0.0", "trbflxr")]
public class ExampleMod : BaseMod {
  public override Texture2D GetIcon() {
    var assembly = Assembly.GetExecutingAssembly();
    return Kino.Utils.LoadEmbeddedTexture(assembly, "Example.Resources.icon.png");
  }
}
```

In this example **icon.png** is added as an **embedded resource** to the ExampleMod project.

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
