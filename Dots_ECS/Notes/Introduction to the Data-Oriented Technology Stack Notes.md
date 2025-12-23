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

**Why is my CPU code slow in the first place?**
