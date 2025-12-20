[source](https://www.youtube.com/watch?v=XIHINtB2e1U)

# Main Issue ?

![[BuildContentOfScene.png]]
* Each ref in the scene(pref,texture,mat...) is packed in the build later 
* Load scene = Load all direct refs (including Resources folder )
* control Loading but not unloading assets
* which causes huge loading time at the start of the game when loaded

# Asset Bundles & addressable
* Asset Bundles : to pack assets and load them when needed
* Addressable : configure, pack, build & load said bundles

## Addressable Groups 

![[Groups.png]]
* Functionality of addr. that allows to divide assets into logical units to be packed in asset bundles when building.
![[AssetBundleExample.png]]

> [!faq]- Good To Know
>Unity requires at least one scene in build (entry point)
>Make empty scene (initialization.scene) to be added to the build settings window 
>it's a one-use scene 


## Asset duplication

Even if not marked as addressable in editor an object can be bundled implicitly if it's a dependency of an addressable object (SO for exmple)