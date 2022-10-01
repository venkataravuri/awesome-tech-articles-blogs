

How Gossip Protocol Works?

Gossip protocol is a peer-to-peer communication mechanism where nodes exchange state information periodically about themselves & other nodes they know about.

Every node begins a gossip round for every second to exchange the state information about itself & other nodes with one other accidental node. So that any new occurrence propagates eventually throughout the system & all nodes rapidly learn about all other nodes within a cluster.

Soure: https://www.elprocus.com/gossip-protocol/

https://redis.io/docs/reference/patterns/distributed-locks/


[Redis SortedSets](https://redis.io/docs/data-types/sorted-sets/)

In Redis, sorted sets having scaling limitations. A sorted set cannot be partitioned. As a result, if the size of a sorted set exceeds the size of the partition, there is nothing you can do (without modifying Redis).
