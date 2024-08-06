## What is this?
This is the example mod for ValksGodotTools/Template. Mods can add and replace assets as well as execute C# scripts.

Every mod needs a `mod.json` file. The `id` should be unique to your mod and only your mod.
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

## How to Add Your Own C# Scripts
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
The `_Ready()` and any other functions you add like `_PhysicsProcess()` will be called. This is the entry point to your mod.

So far this example mod only prints "Hello from Example Mod by valkyrienyanko" when the mod is loaded in.

I have yet to figure out how to modify existing scripts but I'd imagine it would be something like `GetTree().Root.GetNode<Player>("PathToPlayer").SetPosition(50, 0);`. I would have to provide a dummy Player class to the mod so you could type out `Player` and `SetPosition(x, y)` with no errors.
