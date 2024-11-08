# Introduction to design tradeoffs

Meeting customer expectations and business considerations drive these requirements. Examining one feature or functional condition at a time is essential to identifying the necessary actions to make it successful.

Trade-offs are common in engineering systems. This chapter will help you decide when and what you should choose!

# Pull vs. Push Architectures

1. Subscribed for post notificatio
2. get post in specific time zone(time)
3. not worry about view post or not

- Push Model : The event creator push to all recepient(for post subscribers)
- Pull Model :n recepient will pull post after it posted( for non prioritized user)

# Memory vs. Latency

The trade-off between memory and latency is discussed, with a focus on the example of a cache.

For popular profiles or highly active users on Instagram, their profiles and follower counts are cached in memory on the server. This allows for faster access and reduces latency to around 10 milliseconds.

By keeping frequently accessed data in memory, latency is minimized but it requires more memory and additional costs. On the other hand, reducing the cache size may lead to increased latency for certain requests.

A medium approach suggests keeping hot entries in the cache using a suitable replacement algorithm and write policy.

# Throughput vs. Latency

latency: time required to get response from server

throughput: how much processing power

# Consistency vs. Availability

consitency: always get latest data

availability: avail always

# Latency vs. Accuracy

Reducing latency involves avoiding blocking or waiting for resources. Sacrificing accuracy for faster responses involves making guesses on past data.

Sacrificing accuracy for latency can be acceptable in certain systems.

# SQL vs. NoSQL databases

NoSQL and SQL databases are compared on factors like consistency and fault tolerance.

NoSQL databases typically have more relaxed consistency, employ a cluster architecture, and distribute read and write requests among nodes.

NoSQL databases are designed for high scalability, allowing fast read and write operations. SQL databases can also have fast read operations, but write operations may be slower due to potential bottlenecks.

NoSQL databases often have built-in sharding, which involves distributing data across nodes based on predefined ranges or shards. Sharding is not inherent in SQL databases.

NoSQL databases typically lack transaction support, meaning they don't provide ACID guarantees.

# Relations Between Tradeoffs

In this video, Gaurav Sen discusses the relationships between different parameters in design trade-offs.

1. Memory: Increasing memory decreases latency because more data can be cached. However, it also increases cost. The impact on consistency and availability depends on the policies used.
2. Throughput: Throughput is inversely proportional to latency. Reducing latency usually means reducing throughput. There is no significant relation between throughput and cost or availability.
3. Cost: Increasing cost may reduce latency because more resources can be allocated. However, there is no direct relation between cost and throughput, availability, or memory.
4. Latency: Increasing cost may reduce latency, but it is not guaranteed. Latency is inversely related to consistency. If the system can tolerate inconsistency, latency can be low.
5. Consistency: Consistency and availability are inversely proportional. Increasing consistency reduces availability. The guarantees of consistency and availability depend more on algorithms than on cost.
6. Availability: Availability is inversely related to consistency. Partition tolerance is an important factor, and a system doesn't need to be perfectly consistent or available, but good enough based on SLAs and user requirements.
