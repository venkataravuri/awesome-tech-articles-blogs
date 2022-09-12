https://redis.io/docs/reference/patterns/distributed-locks/


[Redis SortedSets](https://redis.io/docs/data-types/sorted-sets/)

In Redis, sorted sets having scaling limitations. A sorted set cannot be partitioned. As a result, if the size of a sorted set exceeds the size of the partition, there is nothing you can do (without modifying Redis).
