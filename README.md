## What is this?
This is the example mod for ValksGodotTools/Template. Mods can add and replace assets as well as execute C# scripts.

> [!CAUTION]
> In order to execute scripts across several mods properly, [this issue](https://github.com/ValksGodotTools/Template/issues/15) needs to get resolved. In the meantime mods adding scripts to mods should be avoided.

> [!WARNING]
> Every mod needs a `mod.json` file. The `id` should be unique to your mod and only your mod.
```json
{
    "name": "Example Mod",
    "id": "example_mod",
    "modVersion": "1.0",
    "gameVersion": "*",
    "description": "Example description.",
    "author": "valkyrienyanko",
    "dependencies": {},
    "incompatibilities": {}
}
```

## How to Replace Game Assets
Game assets include things like sounds, pictures, shaders and models. In order to even start replacing game assets, you will need to know where they are in the game. Only the developer who made the game will be able to tell you this.

In [ValksGodotTools/Template](https://github.com/ValksGodotTools/Template), a path to one of the assets is `res://Template/Sprites/Concept Art/elk-skull-lodge.jpg`. If you would like to replace this you will need to recreate the exact folder structure in this mod. That is create a new folder named `Template` and then create a folder inside that named `Sprites` and then `Concept Art` and finally a image with the same file name and file extension, that is `elk-skull-lodge.jpg`. 

> [!CAUTION]
> C# Scripts are the only kind of assets that cannot be replaced

## How to Add C# Scripts
Due to the way how assemblies are loaded in ValksGodotTools/Template, all scripts will be need to be in unique locations for each mod. If two scripts are in the same location from two different mods, both mods will fail to load.

Put your scripts in `res://<author>/<id>` where `<author>` and `<id>` are what you set in `mod.json`. Making sure these are the same is very important otherwise your mod will fail to load.

You must have a scene in `res://<author>/<id>` named `mod.tscn` and the first node in the scene must have the following script attached.
```cs
using Godot;

public partial class Mod : Node
{
    public override void _Ready()
    {
        
    }
}
```
> [!NOTE]
> The `Mod` node will get added as a child when the mod loads in, so any built-in node functions like `_Ready()` and `_PhysicsProcess()` will act as the entry point to your mod.

## Exporting the Mod
1. Export the mod via `Project > Export...`
2. Create a new folder for your mod. The mod should contain at least 3 files.
    - `mod.json` *(the file you created earlier)*
    - `mod.pck` *(generated from the export)*
    - `Mod.dll` *(generated inside `.godot\mono\temp\bin\Debug`)*
3. Put this folder inside the `Mods/` folder of the game
