* Sharing same memory space => easier to exchange data
* memory overhead (same memo space for most threads) which makes switching between threads faster than between processes with shared resources
* Problems like race conditions could occur (due to snchronization complx)
* Deadlocks/GIL