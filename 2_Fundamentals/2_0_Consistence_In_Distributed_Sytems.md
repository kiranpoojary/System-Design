# What is Data Consistency?

Consistency in a distributed system refers to mesure of  how up-to-date a piece of data is.

A highly consistent system reflects all updates to data, while an inconsistent system provides stale data. Consistency is important because highly consistent systems are easier to reason about and provide a better user experience.

# Why Consistency Important

1. Easier to Understand
2. User Experience

# **Data Consistency Levels** 

## **Linearizable**

At this consistency level, we want to show all changes in the database until the current read request. It means all changes which have happened in the database before the read operation will be reflected in the read query.

For example, suppose initially we had x = 10.

update x to 13

update x to 17

read x --> Returns 17

 update x to 1

read x --> Returns 1

To achieve this we use a **single-threaded** single server. So every read-and-write request will always be ordered. Using the above example, the first read x will be executed after updating the value to 17. This is useful when systems need perfect consistency.

## Eventual Consistent

At this level of consistency, we can send stale data for a read request.

Eventually, our systems catch up with all updates and return fresh data.

To achieve this we can process read and write requests parallelly (using multiple servers) or concurrently (using multiple threads).

Example:

x = 10

update x to 13

update x to 17

read x --> Could return 10 or 13 or 17

update x to 1

read x --> Could return 10 or 13 or 17 or 1

....

...

Eventually, when all update operations have run through...

read x --> returns 1.

In the example above, the write request is made before the read request but the read request is processed first.

So the client may get any possible value for X. But after a given time, the write request will be processed. Then all read requests will show the correct data i.e., X = 10.

Note that eventual consistency is a very loose guarantee, and is often coupled with stronger guarantees like "read your writes".

1. "Read Your Writes" consistency: This type of consistency ensures that a client that makes a write request will immediately see the updated value when it makes a read request, even if the update has not yet propagated to all servers. This type of consistency is often used in systems where low latency is more important than consistency.
2. "Monotonic Read" consistency: This type of consistency ensures that a client will only see values that are as up-to-date or more up-to-date than the values it has previously seen. In other words, once a client has seen a value, it will never see an older value again.
3. "Monotonic Write" consistency: This type of consistency ensures that a client will only see values that are as up-to-date or older than the values it has previously written. In other words, once a client has written a value, it will never see a newer value from another client.

## **Causal Consistency**

At this consistency level, if a previous operation is related to the current operation, then the previous operation must be executed before the current operation.

Causal consistency is stronger and slower than eventual consistency because operations for the same key are processed sequentially.

It is looser and faster than the serializable consistency level because it does not wait for all previous operations to complete.

Causal Consistency fails when performing aggregation operations.

## **Quorum**

Quorum is a mechanism by which we can get consistency guarantees based on our requirements.

It defines how many readers must acknowledge a read operation = R.

It also defines how many writers must acknowledge a read operation = W.

For example, let's say we have three replicas: x = 20 , x = 20 , x = 20.

Update second replica x = 40.
The second node crashes.

Read x => ?? (Depends on the following scenarios)

### Eventual consistency:

W = 1 and R = 1.

In this case, when there is a read operation after the second node crashing, we will get a result of X = 20 from the remaining nodes.

This is stale data. It will eventually be consistent because the second replica is expected to come back up.

When it is back online, we will get the correct result of X = 40.

### Serializable consistency:

W = 2 and R = 2.

The write operation must go to two replicas before an acknowledgment is sent to the client. This means, apart from the second replica, either the first or third replica must set X = 40 before a client gets a write acknowledgment.

Let us assume one replicates the data. Now we have X = 40, X = 40, and X = 20.

On the write operation, we need 2 nodes to reply successfully. Notice that it is impossible to miss the latest data now, because at least one of the nodes we hit will have the last operation reflected in it.

The logic is based on the pigeon hole principle: [https://en.wikipedia.org/wiki/Pigeonhole_principle](https://en.wikipedia.org/wiki/Pigeonhole_principle)

### The mathematical formula for quorum consistency:

Consistency depends on the values R, W, and N.
N here is the total number of nodes in the system.

We can either have an eventually consistent system (R + W<=N) or a strongly consistent system (R+W > N)

**Disadvantages of using quorum **

We need multiple replicas chatting with each other, so costs and latency could be high.


# Data Consistency Levels Tradeoffs

```
╔═════════════╦══════════════╦══════════╦═════════╦══════════════╗
║             ║ Serializable ║ Eventual ║ Causal  ║ Quorum       ║
╠═════════════╬══════════════╬══════════╬═════════╬══════════════╣
║ Consistency ║ Highest      ║ Lowest   ║ Mid-way ║ Configurable ║
╠═════════════╬══════════════╬══════════╬═════════╬══════════════╣
║ Efficiency  ║ Lowest       ║ Highest  ║ Mid-way ║ Configurable ║
╚═════════════╩══════════════╩══════════╩═════════╩══════════════╝
```


# **Transaction Isolation Levels - Read Uncommitted Data**

Transactions are a collection of queries that perform one unit of work. They are atomic which means either all queries in a transaction are executed or none of it is executed.

## **BEGIN**

Marks the start of the transaction.

## **COMMIT**

Marks the end of the transaction, which results in the changes persisting to the database.

## **ROLLBACK**

Marks the end of the transaction and undoes all the changes to the database.

# Isolation:

If two transactions are running concurrently and queries in one transaction do not affect the other transaction then the two transactions are said to be isolated from each other.

## **1. Read Uncommitted**

At this isolation level, even uncommitted data can be read by concurrent transactions. Although it is very fast, it leads to dirty reads.

## **2. Read committed**

At this isolation level, one transaction can only read committed data from other transactions.


## **3. Repeatable Reads**

At this isolation level, we ensure that when a query reads a row, that row will remain unchanged for the entire transaction.

Each transaction has its data copy that is updated. Once the transactions are committed, updates are persisted in the database.

This is known as **Snapshot Isolation** since a transaction is isolated from another by taking different data snapshots.

If two transactions concurrently change the same key to different values, we must roll back one transaction.

This is called **Optimistic Concurrency Control** since we are optimistic about our changes until they are proven incompatible.


## **4. Serializable Isolation Level**

This is the highest isolation level. At this level, all transactions are executed serially. All of the operations are executed serially or every operation is ensured to not meddle with the operations of other transactions. We use this isolation level when we want to avoid Phantom Reads.

A Phantom Read occurs when two identical read queries are executed and the collection of rows returned by the second query is different from the first. It is different from non-repeatable reads because in phantom reads the change in the value can be due to the insertion of a new row.


# Transaction Level Implementations

How are transaction levels implemented in the real world?

* We only need a single entry in the database and it is overwritten whenever there is an update operation
* If we are making an update to a key then the older value of the key stays in the database and the newer value is kept in the local copy till the commit finally goes through.
* We take the values that we care about but we are not changing and keep a version of them. For every key, we will store all the values that it has ever had in different transaction commits
* We use causal ordering here. If two transactions use queries for the same key then they must be ordered. Transactions that do not have any conflict can run concurrently.


# **Conclusion - Transaction Isolation**

## **For Efficiency**

 Read Uncommitted > Read Committed > Repeatable Read > Serializable

## For Isolation

Read Uncommitted < Read Committed < Repeatable Read < Serializable
