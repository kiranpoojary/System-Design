# Data Replication

Data replication involves copying data from one location to another, while data migration is manually moving data to a new location. Replication is more common in mature companies and those using cloud solutions.

In a replication scenario, clients are connected to a server with a database, but the database could fail due to various reasons. To address this, a replica (or backup) of the original database is created. Data consistency is maintained by sending write requests to the primary database, while read requests are directed to both the primary and the replica. This approach benefits read-intensive applications, as write operations are infrequent.

The benefits of a primary-replica architecture include fault tolerance, improved read speeds, and relative simplicity. If the primary database fails, the replica can take over. Read requests can be distributed among multiple primary and replica nodes. However, there are drawbacks, including potential consistency issues if there are in-flight messages, and slightly slower write speeds due to the added complexity. Fault tolerance comes at the cost of increased latency.

In summary, data replication is an essential practice in maintaining data availability and fault tolerance in software engineering, particularly in mature companies or those using cloud solutions. While it offers benefits, it also introduces challenges related to data consistency and latency.

```
![Alt Text](./Images/5_0_DB_replication.png)
```

## Pros

1. Fault tolerance
2. Read Speed
3. Simple


## Cons

1. Data Consistency
2. Write Slower


# Why Replication


We discuss various challenges and solutions related to data replication. It begins by explaining why having two primary databases can be problematic, leading to inconsistencies and difficulties in reconciliation. This situation is referred to as "split brain." Manual reconciliation and techniques like "last writer wins" are mentioned, but they come with their own risks and complexities.

To avoid split brain scenarios, the speaker suggests having an odd number of primary nodes to ensure a majority consensus in case of network partitions. The use of an even number of nodes can lead to reconciliation issues and require manual intervention.

We also touch on the challenges of replication when dealing with multiple read replicas, such as the issue of "write amplification" and the potential for increased latency.

I recommend using a consensus mechanism like Paxos or Raft to ensure that the entire cluster agrees on a value during data replication. This ensures strong consistency across the system.


# Data Migration

So you found a flashy new database technology. You run some tests, check the performance, and are convinced! Time to speak to your manager! But wait… How do you move millions of records, each entry representing a user's aspirations, into a new database? Without any downtime? AND without any mistakes… After sweating profusely, you come up with a plan:

1. Stop the existing DB.
2. This fails all incoming requests to the DB (You should probably have some email communication setup beforehand to notify users of a planned outage).
3. Take a Data Dump of the current DB into your shiny new DB.
4. When the process completes, point the existing servers to the new DB. This will take a deployment or a server restart


# Migrating the DB

This is going to be more complex engineering, but worth it the savings in downtime.

1. Set up a change data capture solution (Similar to a SQL trigger).
2. Take a database copy of all older records.
3. Setup a view or proxy to serve existing clients through the old database.
4. Set the clients to point to the proxy.
5. Now point the proxy to the new database.
6. Point clients to the new database directly (this requires a deployment or server restart).
7. Delete the proxy.

Yey! Remember, despite our best efforts, there is always a chance of a data miss. It's best to check for correctness after deployment, and keep your clients in the loop

## Cross Region Migration
