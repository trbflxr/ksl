# Mods / extensions installation guide

## Mods

> [!NOTE]  
> Install your mods to ```kino/mods``` folder.

KSL supports loading of encrypted **.ksm** mods made for KSL. Also it can load legacy mods for Kino loader (**.dll** and **.kn**) and **.dll** mods made for **BepInEx** in backward compatibility mode.

More info about making mods can be found [here](dev/mods.md).

## Extensions

> [!NOTE]  
> Install your extensions to ```kino/extensions``` folder.

KSL can load **.kse** extensions made for it. Extensions are primarily designed to extend KSL functionality for different games. You can lock input where needed, make sure that KSL UI isn't click-through and more depending on a game.

Learn more about KSL extensions [here](dev/extensions.md).

---

> [!IMPORTANT]  
> Keep in mind that KSL will search mods and extensions in the root folder and one level deep folders.

Example:

```c#
mods:
  kino.dll            - OK

  test.ksm            - OK

  my-mod-folder:
    mod_data.txt
    MyMod.ksm         - OK

  another-mod-folder:
    mod-subfolder:
      the_mod.ksm     - Not OK  
```
