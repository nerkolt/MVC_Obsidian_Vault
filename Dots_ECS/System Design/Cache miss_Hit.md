[source](https://www.youtube.com/watch?v=zF4VMombo7U)
# Caching
![[OOD.png|400]]
Memory management of entities :
![[PVH.png|150]]
## OOD :
![[Ram_OOD.png]]
scattered data => hard to access
## DOD
![[DOD memory.png]]ECS usage to manage indiv components of entities and group them together in memo for ez access.
# Cache Miss/Hit concept for ECS
![[CacheMiss.png]]

system tries to retrieve data from cache => not there? =>fallback to a slower, more expensive source(RAM,Disk,network...)
### Examples in System Design

1. **CPU Cache Miss in a High-Performance Application**:
    - Imagine a processor running a data-intensive app, like a machine learning model processing large arrays.
    - The CPU has multi-level caches: L1 (smallest, fastest, per-core), L2 (larger, shared), and L3 (even larger).
    - If the app requests an array element not in L1 (L1 miss), it checks L2. If not there (L2 miss), then L3. A full miss means fetching from RAM, which is 10-100x slower (e.g., 100ns vs. 1ns for L1).

![[Cache Hit.png]]
=> @ copied from said source as well as the rest of the @ following it (since access is sequencial)
* Thus no more need for expensive access since data is already in cache
* exple : if positions are accessed now the % of it being accessed again next frame is high => cache with no reload
# Examples in Unity 
Unity uses caching internally (e.g., via AssetBundles, shader variants) to optimize for mobile/desktop performance.
#### **Texture Cache Miss During Runtime Loading**:
- In a 3D game, textures are cached in GPU memory for fast rendering.
    - A player enters a new level; Unity tries to access a texture from the cache. On a miss (e.g., first load or evicted due to memory limits), it loads from disk/AssetBundle, decompresses, and uploads to GPU.
    - Example : In a mobile game like an endless runner, this could frustrate players. 
    - Fix: Use Addressables for asynchronous loading, pre-load assets in a loading screen, or mipmapping to improve cache efficiency.

####  **Shader Variant Cache Miss in Dynamic Lighting**:

- Unity's Shader Variant system precompiles shaders for different conditions (e.g., with/without fog).
    - If a scene enables a new feature like dynamic shadows, and the variant isn't cached, Unity compiles it on-the-fly (miss), causing a stutter.
    - **Examples**: player customizations trigger variants. 
    - Fix: Use Shader Variant Collection assets to pre-warm the cache during build, or strip unused variants to reduce build size/memory.
#### **Physics Cache Miss in Collision Detection**:
- Unity's PhysX caches collision data for efficiency.
    - In a racing game, if a car's collision mesh isn't in the cache (e.g., after spawning many objects), a miss fetches/computes it anew.
    - **Example**: Jittery physics or slowdowns in crowded scenes. 
    - Fix: Optimize by pooling objects (reuse instead of instantiate/destroy) and using simpler colliders where possible.
# Key Takeaways

- Cache misses highlight the trade-off between speed and storage: caches are limited, so not everything fits.
- Prevention: Design for predictability (e.g., locality in code, TTLs in apps) and monitor with metrics.
- In games, misses often manifest as "pop-in" or lag; in systems, as scalability issues.