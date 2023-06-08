
# Redis

Redis ~ **Re**mote **Di**ctionary **S**ervice
- Redis is mostly single-threaded, except background IO
- A distributed data structure server
    - Key:String => Value:String
    - Key:String => Value:List
    - Key:String => Value:Set
    - Key:String => Value:Zset
    - [List of Redis Data Structures](https://miro.medium.com/v2/resize:fit:720/format:webp/1*Jo5_Qy3oXe4i0gqLQINi0A.png)
- Operations on any Type

### Redis Sorted Sets

[Try to understand Sorted Sets with a leaderboard example](https://medium.com/analytics-vidhya/redis-sorted-sets-explained-2d8b6302525)
[Redis SortedSets](https://redis.io/docs/data-types/sorted-sets/)

In Redis, sorted sets having scaling limitations. A sorted set cannot be partitioned. As a result, if the size of a sorted set exceeds the size of the partition, there is nothing you can do (without modifying Redis).

[ChatGPT redis-py data leak issue](https://openai.com/blog/march-20-chatgpt-outage)

### Atomicity in Redis

- Series of operations
    - Guaranteed to all run or none run
    - Prevents operations from running partially
- The effects all operations are immedately visible, i.e. another client cannot see partial updates

#### Atomi Operations

INCR key   # GET key, value++, SET key value

#### Pipelining

- Ensures commands are run in order per-connection
- Sends batch of commands seperated by newlines
- Commands are sent in same message

**Pipelining is NOT atomic**. It for,
- Reduce latency
- Send several commands in one message
- Receive several responses in one message

Use MULTI for true atomicity
- Atomic regardless of other clients and connections
- Client sends MULTI; more commands, EXEC

Use LUA script to reduce latency.

Source: https://www.slideshare.net/RedisLabs/atomicity-in-redis-thomas-hunter

### Redis Sentinel Vs. Redis Cluster 

- If you need high availability, even if it is not scalable, and you have less data than RAM on a machine -> Use Redis Sentinel
- You need data sharding, scalability and automatic failover, it doesn’t have to be entirely highly available and you have more data than RAM on a server -> Use Redis Cluster

[Redis Solutions: Standalone vs Sentinel vs Cluster](https://medium.com/hepsiburadatech/redis-solutions-standalone-vs-sentinel-vs-cluster-f46e703307a9)

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
    
###  Redis Cluster TCP ports

Every Redis Cluster node requires two TCP connections open. 
- The normal Redis TCP port used to serve clients, for instance let’s take 7000,
- Cluster Bus port obtained by adding 10000 to the data port, so 17000.

Cluster bus is a node-to-node communication channel using a binary protocol. The Cluster bus is used by nodes for failure detection, configuration update, failover authorization and so forth. 

### How inter node communication in a Redis Cluster?

All nodes continuously PING other nodes in the cluster. A node recognizes and marks another node as possibly failing when there is a timeout longer than N seconds.

Every PING and PONG packet contain a GOSSIP section which contains the information about other nodes idle times, from the point of view of the sending node.

### Redis Cluster Bus

This second high port (In here, 17000) is used for the Cluster bus, that is a node-to-node communication channel using a binary protocol. The Cluster bus is used by nodes for failure detection, configuration update, failover authorization and so forth. If you don’t open both TCP ports, your cluster will not work as expected. So make sure that you open both ports in your firewall.

### How Gossip Protocol Works?

Gossip protocol is a peer-to-peer communication mechanism where nodes exchange state information periodically about themselves & other nodes they know about.

Every node begins a gossip round for every second to exchange the state information about itself & other nodes with one other accidental node. So that any new occurrence propagates eventually throughout the system & all nodes rapidly learn about all other nodes within a cluster.

Soure: https://www.elprocus.com/gossip-protocol/

### How Redis persistence writes data to disk?

Persistence refers to the writing of data to durable storage, such as a solid-state disk (SSD). Redis itself provides a range of persistence options:

- RDB (Redis Database): The RDB persistence performs point-in-time snapshots of your dataset at specified intervals. RDB files are perfect for backups. For instance you may want to archive your RDB files every hour for the latest 24 hours, and to save an RDB snapshot every day for 30 days.
- AOF (Append Only File): The AOF persistence logs every write operation received by the server, that will be played again at server startup, reconstructing the original dataset. Commands are logged using the same format as the Redis protocol itself, in an append-only fashion. Redis is able to rewrite the log in the background when it gets too big. AOF log is an append-only log, so there are no seeks, nor corruption problems if there is a power outage. Even if the log ends with a half-written command for some reason (disk full or other reasons) the redis-check-aof tool is able to fix it easily.
- No persistence: If you wish, you can disable persistence completely, if you want your data to just exist as long as the server is running.
- RDB + AOF: It is possible to combine both AOF and RDB in the same instance. Notice that, in this case, when Redis restarts the AOF file will be used to reconstruct the original dataset since it is guaranteed to be the most complete.

### How can use Redis for Distributed Locks?

Redis uses Redlock algorithm, which implements a DLM (Distributed Lock Manager) which we believe to be safer than the vanilla single instance approach.

Minimum guarantees needed to use distributed locks in an effective way.

- **Safety property**: Mutual exclusion. At any given moment, only one client can hold a lock.
- **Liveness property A**: Deadlock free. Eventually it is always possible to acquire a lock, even if the client that locked a resource crashes or gets partitioned.
- **Liveness property B**: Fault tolerance. As long as the majority of Redis nodes are up, clients are able to acquire and release locks.


https://redis.io/docs/reference/patterns/distributed-locks/

