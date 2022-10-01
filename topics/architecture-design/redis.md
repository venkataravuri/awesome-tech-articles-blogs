### Redis Clustering

Redis Clustering provides a consistent and resilient data service where data is automatically sharded (Partitions data) across multiple Redis nodes (Automatically split your dataset among multiple nodes). 

And it provides a master/slave setup for enhance availability in case of a failure.

Minimal cluster that works as expected requires to contain at least 3 master nodes in the cluster and Redis recommendation is to have at least one slave for each master.
- Minimum 3 Redis master nodes on separate 3 machines for each
- Minimum 3 Redis slaves (One replica for each master node), 1 slave per master (to allow minimal fail-over mechanism)

### How Redis Cluster does data sharding?

Redis Cluster does not use consistent hashing, but a different sharding, where every key is conceptually part of a hash slot.

There are 16384 hash slots in Redis Cluster (distributea 16384 slots among Cluster nodes).
Computes hash slot of a given key, we simply takes CRC16 of the key modulo 16384.

Every node in a Redis Cluster is responsible for a subset of the hash slots, so for example you may have a cluster with 3 nodes, where:
    Node A contains hash slots from 0 to 5500.
    Node B contains hash slots from 5501 to 11000.
    Node C contains hash slots from 11001 to 16383.
    

### How inter node communication in a Redis Cluster?

All nodes continuously PING other nodes in the cluster. A node recognizes and marks another node as possibly failing when there is a timeout longer than N seconds.

Every PING and PONG packet contain a GOSSIP section which contains the information about other nodes idle times, from the point of view of the sending node.


### How Gossip Protocol Works?

Gossip protocol is a peer-to-peer communication mechanism where nodes exchange state information periodically about themselves & other nodes they know about.

Every node begins a gossip round for every second to exchange the state information about itself & other nodes with one other accidental node. So that any new occurrence propagates eventually throughout the system & all nodes rapidly learn about all other nodes within a cluster.

Soure: https://www.elprocus.com/gossip-protocol/

https://redis.io/docs/reference/patterns/distributed-locks/


[Redis SortedSets](https://redis.io/docs/data-types/sorted-sets/)

In Redis, sorted sets having scaling limitations. A sorted set cannot be partitioned. As a result, if the size of a sorted set exceeds the size of the partition, there is nothing you can do (without modifying Redis).
