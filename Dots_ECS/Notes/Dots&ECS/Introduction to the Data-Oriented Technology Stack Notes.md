[[Introduction_to_the_Data-Oriented_Technology_Stack_for_advanced_Unity_developers_Unity_2022_LTS.pdf#page=1&selection=0,0,4,10|Introduction_to_the_Data-Oriented_Technology_Stack_for_advanced_Unity_developers_Unity_2022_LTS, page 1]]

# Overview
* is a guide from Unity aimed at experienced developers but with concepts that can be adapted for beginners like you. 
* It focuses on Unity's Data-Oriented Technology Stack (DOTS), which is a set of tools and packages designed to make games run faster and more efficiently, especially on devices with multiple CPU cores (like modern phones or PCs).
* The core idea is shifting from traditional "object-oriented" programming (using things like GameObjects and MonoBehaviours, which can be slow for big games) to a "data-oriented" approach. This means organizing your game's data (like positions, health, or velocities) in a way that's super friendly to the computer's hardware, reducing lag, hitches, and crashes.
# Notes
Are loading times annoyingly long, and does the game freeze for full seconds every time the player walks through a door? Reasons could be :
* rendering: textures are too large, meshes too complex, shaders too expensive
* there’s ineffective use of batching, culling, and LOD
* excessive use of complex mesh colliders, which greatly increase the cost of the physics simulation

> [!faq]- Moore's Law?
> **[Moore's law](https://en.wikipedia.org/wiki/Moore%27s_law)** is the observation that the [number of transistors](https://en.wikipedia.org/wiki/Transistor_count "Transistor count") in an [integrated circuit](https://en.wikipedia.org/wiki/Integrated_circuit "Integrated circuit") (IC) doubles about every two years.

### **Why is my CPU code slow in the first place?**

- **Garbage Collection (GC) Pauses**: In C#, when you create objects (like new enemies), memory gets "garbage-collected" automatically. This pauses your game briefly, causing stutters. Analogy: Imagine your game is a party—GC is like the cleanup crew stopping the music to tidy up.
- **Slow Code Compilation**: Unity's default compilers (Mono or IL2CPP) don't optimize code well, making it run slower.
- **Single-Threaded Code**: Most games run everything on one CPU "lane" (the main thread), ignoring extra cores. It's like having a multi-lane highway but only using one.
- **Cache-Unfriendly Data**: Data scattered in memory makes the CPU wait (cache misses). Tight-packed data (like in arrays) is faster.
- **Too Much Abstraction**: Fancy OOP code (inheritance, etc.) hides costs but slows everything down without clear fixes.

A GameObject and its components are all separately allocated, so they often end up in different parts of memory.

>[!faq]- for more info
>check [[Introduction_to_the_Data-Oriented_Technology_Stack_for_advanced_Unity_developers_Unity_2022_LTS.pdf#page=8&selection=6,0,7,35|Introduction_to_the_Data-Oriented_Technology_Stack_for_advanced_Unity_developers_Unity_2022_LTS, page 8]]


# C# Job systems
For an easier alternative, Unity provides the C# job system:
*  The job system maintains a pool of worker threads, one for each additional core of the target platform. For example, when Unity runs on eight cores, it creates one main thread and seven worker threads. 
* The worker threads execute units of work called jobs. When a worker thread is idle, it pulls the next available job from the job queue to execute. 
* Once a job starts execution on a worker thread, it runs to completion (in other words, jobs are not preempted).
## Job safety checks and dependencies

*  Jobs that share the same data should not execute concurrently because this creates race conditions. So the job system “safety checks” throw errors when you schedule jobs that might conflict with others.
* Note that jobs are intended only for processing data in memory, not performing I/O (input and output) operations, such as reading and writing files or sending and receiving data over a network connection.
* Because some I/O operations may block the calling thread, performing them in a job would defeat the goal of trying to maximize utilization of the CPU cores. If you want to do multithreaded I/O work, you should call asynchronous APIs from the main thread or use conventional C# multithreading.
# Burst Compiler
* Burst-compiled code can’t access [[managed vs Unmanaged objects]]
* the performance gains of Burst come from the use of [[SIMD]] and better awareness of [[aliasing]]

# Collections

Because these collections are unmanaged, they don’t create garbage collection pressure, and can be safely used in jobs and Burst-compiled code
The collection types fall into a few categories: 
* The types whose names start with Native will perform safety checks. These safety checks will throw an error: — If the collection is not properly disposed of. 
* If the collection is used with jobs in a way that isn’t thread-safe.
* The types whose names start with Unsafe perform no safety checks.
* The remaining types which are neither Native or Unsafe are small struct types with no pointers, so they are not allocated at all. Consequently, they need no disposal and have no potential thread-safety issues.

# Mathematics
* a C# math library that, similar to Collections, is created for Burst and the job system to be able to compile C#/IL code into highly efficient native code.
[Cheat sheet jic](https://github.com/Unity-Technologies/EntityComponentSystemSamples/blob/master/EntitiesSamples/Docs/cheatsheet/mathematics.md)

# ECS
## Archetypes
* all entities with the same set of component types are stored together in the same “archetype”.
##### Example
For example, say you have three component types: A, B, and C. Each unique combination of component types is a separate archetype, e.g.: 
* All entities with component types A, B, and C, are stored together in one archetype. 
* All entities with component types A and B are stored together in a second archetype. 
* All entities with component types A and C are stored in a third archetype. 
Adding a component to an entity or removing a component from an entity moves the entity to a different archetype.
![[ArchetypeChunks.png]]

>[!faq]- Conclusion
> In Unity’s ECS, all entities with the same set of component types are stored together in the same “archetype”

# Chunks


A chunk’s arrays are always kept tightly packed: 
* When a new entity is added to the chunk, it’s stored in the first free index of the arrays. 
* When an entity is removed from the chunk, the last entity in the chunk is moved to fill in the gap (an entity is removed from a chunk when it’s being destroyed or moved to another archetype.)

# Queries
![[QueryWorkflow.png]]
# Subscenes and baking
* A monobehavior referencing a scene asset to be baked(a scene nested in another scene)
* Baking(feature) processes each subscene to produce a set of serialized entities.
* baking: conversion of GO in a subscene into s.e .
* when a subscene is loaded at runtime it's the subscene s.e that get loaded =/= the GO
![[Pasted image 20251224112615.png]]
* opening a subscene loads its GOs into the editor and triggers the baking conversion process
* Closing a subscene unloads GOs from editors but entities produced 
![[Pasted image 20251224124056.png]]
* what we see is the entity baked from the GO 
* any changes applied in play mode on the subscene entities will persist even after exiting






### key things to remember
- Entities are created with components.
- Archetypes group them by component types.
- Chunks store the data in fast arrays.
- Queries find the right chunks to work on.
- Jobs run the updates across CPU cores.

 #### Why This Is Powerful
- **Speed**: Chunks and archetypes make data access fast. Jobs use all CPU cores.
- **Scale**: Handles thousands of entities (like the city’s drones and buildings) without lag.
- **Organization**: Queries ensure you only update what needs it.