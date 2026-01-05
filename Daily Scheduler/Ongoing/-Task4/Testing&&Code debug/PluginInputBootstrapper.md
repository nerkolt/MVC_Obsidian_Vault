![[hybridMono bootstrapper.png]]
https://github.com/bxbstudio/hybrid-mono/blob/master/Runtime/Core/MonoBakingSystem.cs

https://docs.unity3d.com/6000.3/Documentation/ScriptReference/RuntimeInitializeOnLoadMethodAttribute.html


The PluginInputBootstrapper class is a crucial component of the input system architecture. It handles the discovery and lifecycle of input plugins so that other systems (like PluginInputReaderSystem ) can access them without hard dependencies.

I've implemented the class with the following features:

1. Automatic Initialization : Uses [RuntimeInitializeOnLoadMethod] to run before the scene loads.
2. Reflection-based Discovery : Scans all assemblies for classes inheriting from PluginInputProvider and instantiates them.
3. Plugin Management : Stores plugins in a dictionary keyed by their hash for quick lookup.
4. Active Plugin Retrieval : Provides a helper to get the currently selected plugin based on VehicleInputSettings .

# PluginInputBootstrapper implementation

### The Main Flow
```

Game Starts
    ↓
RuntimeInitialize() is called automatically
    ↓
InitializeSystem() runs
    ↓
DiscoverPlugins() finds all plugin classes
    ↓
Plugins are stored in a dictionary
    ↓
Ready to provide plugins to other systems!
```
