This is an example mod for ValksGodotTools/Template.

## Creating the mod.json
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
You will need to know the exact path to the asset in the game. In order to find this out the game developer will either need to tell you this or you will need to figure out how to get this information yourself.

In ValksGodotTools/Template, the path to a concept art jpg is `res://Template/Sprites/Concept Art/elk-skull-lodge.jpg`. If you would like to replace this you will need to recreate this exact path with the same file name.

This means you can replace scenes, shaders, models, textures, sound effects, and music. You can import pretty much any kind of asset except for csharp scripts.

## How to Add Your Own Scripts
Due to the way how assemblies are loaded in ValksGodotTools/Template, all scripts will be need to be in unique locations for each mod. If two scripts are in the same location from two different mods, both mods will fail to load.

Put your scripts in `res://<author>/<id>` where `<author>` and `<id>` are what you set in `mod.json`. Making sure these are the same is very important otherwise your mod will fail to load.

So for example for the example mod I have created I would put my scripts in `res://valkyrienyanko/example_mod`.

You must have a scene in `res://valkyrienyanko/example_mod` named `mod.tscn` and the first node in the scene must have the following script attached.
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

I have yet to figure out how to modify existing scripts but I'd imagine it would be something like `GetTree().Root.GetNode<Player>("PathToPlayer").SetPosition(50, 0);`. I would have to provide a dummy Player class to the mod so you could type out `Player` and `SetPosition(x, y)` with no errors.
