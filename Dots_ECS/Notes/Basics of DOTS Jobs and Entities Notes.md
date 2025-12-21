[Unit-basics-dots-jobs-entities](https://learn.unity.com/course/basics-dots-jobs-entities?version=2022.3)
## 1. Overview
* The **Burst compiler** is an optimizing C# compiler that often generates much faster code than Mono or even ILCPP.
*Some other packages are built on top of Entities and the rest of the DOTS core:

- The **Unity.Physics** package provides a deterministic rigid body dynamics system and spatial query system.
- The **Unity.Netcode** package (also known as **Netcode for Entities**) provides networked multiplayer with an authoritative server and client-side prediction.

> [!faq]- Things to keep in mind?
> Unity has no entity-based solution for animation, audio, or UI, so an entities-based project must fall back on GameObjects or other alternatives for these features. For example, if you make an entities-based game with animated monsters, you can represent the monsters as entities in the simulation logic but render them as GameObjects. This necessitates syncing state between each monster entity and its GameObject representation, but this overhead may be totally acceptable at small to medium scales

## 2. Key concepts of DOTS
###### The C# Job system

![[NativeArray.png]]
No use of C# managed arrays (System.Array) since it's better not to use managed objects in jobs (managed objects ARE not allowed in burst comp)

![[Pasted image 20251221145348.png]]

Complete() :
* waits for job to finish executing before returning
* used to sync jobs with the main thread
* Removes all record of the job from the job queue

> [!faq]- Things to keep in mind?
> Jobs can only be completed/scheduled by the main thread
> main thread can't access data in use by curr scheduled jobs 
> 