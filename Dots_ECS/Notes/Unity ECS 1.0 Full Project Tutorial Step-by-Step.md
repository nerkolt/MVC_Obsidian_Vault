[source](https://www.youtube.com/watch?v=IO6_6Y_YUdE)

* Archetypes : Unique combo of data components that form an entity
* Player loop in systems :
Initialization grp
simulation grp
presentation grp

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