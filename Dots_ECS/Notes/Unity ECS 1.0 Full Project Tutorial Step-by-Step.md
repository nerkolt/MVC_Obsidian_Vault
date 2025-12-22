[source](https://www.youtube.com/watch?v=IO6_6Y_YUdE)

* Archetypes : Unique combo of data components that form an entity
* Player loop in systems :
**Initialization grp**
**simulation grp**
**presentation grp**

## Job system scheduling

###### Run()
* Runs immediately on the main thread ( little to no overhead + good for small jobs without worrying abt dependencies)
###### Schedule()
* Run on worker Thread (only on one )
* != ScheduleParallel() multiple workers //

## Burst Compilers
SIMD (Single instruction, multiple data) optimization : combines multiple data components that are similar into one single CPU instruction

## Aspects

* Provides a way to combine multiple DATA components into a single easy way to interface
* You can add helper functions to them

> [!faq]- IAspect obsolete?
> Unity has no entity-based solution for animation, In Unity's Data-Oriented Technology Stack (DOTS), the obsolete `IAspect` interface has been replaced by directly using **`Component` and `EntityQuery` APIs** within systems.
> The move away from `IAspect` is part of an effort to consolidate APIs, reduce code generation (improving compile times), and improve iteration time.

## Entity Manager
Could be used for spawning entities for example But over using entity managers slows down the spawning.
solution : 
## Entity Command Buffer 
Basically queueing up commands inside the ECB and then play it back later 
Structural changes : Spawn/destroy entities , add/remove component ... any change on an entity that affects where it exists in memory 
They require Sync Points before execution
## Sync Point
Basically all scheduled jobs need to be completed before this is run.

*Go back to minute 58:40*
# unity view
If you aren’t seeing entities in the Scene View but you can still see them in the Game View - open the Preferences window (Edit > Preferences…) then on the Entities section, make sure “Scene View Mode” is set to “Runtime Data” not “Authoring Data”
![[SceneView.png]]
# Main changes between versions (Mine 1.4.3 latest)
Unity split `LocalToWorldTransform` into **two separate components**:

- LocalTransform → position, rotation, scale (what you write to)
- LocalToWorld → the computed world matrix (read-only, auto-calculated)
## UniformScaleTransform
should now be called `LocalTransform`, and should contain all fields from `UniformScaleTransform`
## LocalToWorldTransform
should now be called `LocalToWorld`
> [!faq]- Old VS New way?

Old
```csharp
ecb.SetComponent(newTombstone,new LocalToWorld{Value = newTombstoneTransform});
````
New
```csharp
ecb.SetComponent(newTombstone, newTombstoneTransform);
````

## TransformAspect
Old
```csharp
private readonly TransformAspect _transformAspect;
````
New
```csharp
    private readonly RefRW<LocalTransform> _transformAspect;
```

### key takeaway 

|Old (pre-1.0)|New (1.0+)|
|---|---|
|`LocalToWorldTransform`|`LocalTransform` + `LocalToWorld` (computed)|
|`UniformScaleTransform`|`LocalTransform.FromPositionRotationScale()`|
|`TRSToLocalToWorldTransform`|`LocalTransform.FromMatrix()`|
|Set `LocalToWorld` directly|Usually don’t – let `TransformSystem` do it|
