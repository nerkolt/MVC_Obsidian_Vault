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
SIMD optimization : combines multiple data components that are similar into one single cpu instrction 