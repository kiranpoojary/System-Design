# The Problem of Distributed Consensus

In this video by Gaurav Sen, he introduces the concept of Paxos, a distributed consensus protocol. Paxos is an algorithm designed to achieve consensus in distributed systems where individual components can fail, and messages may be dropped during communication.

Key points covered in the video:

1. **Consensus** : Paxos aims to achieve consensus in a distributed system, specifically a majority consensus. This means that more than half of the nodes in the system must agree on a particular value.
2. **Distributed Nature** : Paxos operates in a distributed environment where components can fail, and messages may not always be delivered.
3. **Use Cases** : Paxos is used in various popular systems, including Apache Zookeeper and Google Chubby, mainly for distributed locking and maintaining order in distributed logs.
4. **Importance** : Distributed consensus, especially in the presence of failures and timeouts, is a challenging problem. Paxos offers a solution where consensus is achieved with the agreement of more than half of the nodes.
5. **Prerequisites** : Gaurav suggests reviewing topics like data consistency, isolation levels, two-phase commits, and quorum to better understand the challenges of distributed consensus.

The video sets the stage for a deeper exploration of the Paxos algorithm, its practical use cases, and its applications in systems like distributed locking and log management. Paxos is highlighted as a valuable tool for maintaining consistency and order in distributed systems, even in the face of failures and unpredictable message delivery.

# Basic Algorithm

In this video by InterviewReady, the concept of distributed consensus in a scenario involving three application servers (S1, S2, S3) and three database servers (D1, D2, D3) is explained. The key points covered are:

1. **Consensus Requirement** : Consensus in this context means that for a written request to be considered complete and durable, at least two out of the three databases must accept it.
2. **Broadcasting Write Requests** : When a write request is received by an application server, it is broadcast to all three databases.
3. **Agreeing on a Log Line** : Before writing the data, the servers must agree on which log line (position) the data should be written to. This prevents potential overwrites.
4. **Log Line Synchronization** : Servers ask the databases for their current log line. If more than half of the databases agree on a particular log line, it is selected for writing. This process ensures that the writes are consistent.
5. **Locking the Log Line** : To prevent concurrent writes and overwrites, a server locks the chosen log line by becoming its owner. This is necessary to maintain consistency and avoid conflicts.
6. **Write Operation** : Once a server owns the log line, it can proceed with the write operation. The write is accepted or rejected based on the owner of the log line.
7. **Two-Phase Protocol** : The process involves a two-phase protocol. In the first phase, servers request the logline and lock it, while the second phase involves executing the actual write operation.

The video explains how this two-phase protocol ensures that only one server can write to a particular log line at a time, preventing inconsistencies and conflicts. It also emphasizes that the write operation and log line ownership must be accepted by a majority of nodes to maintain consensus.

This approach helps achieve distributed consensus in a distributed database configuration, ensuring that data remains consistent even in the presence of failures and concurrent write requests.

# Improving the algorithm

To improve the algorithm, servers send timestamps instead of server identities when requesting locks. Timestamps indicate the recency of the request, allowing the system to prioritize the most recent operation rather than solely relying on server proximity.

Servers store both the value of the log line and the timestamp. To ensure uniqueness, they assign timestamps with remainders when divided by three, making it easier to compare and identify the most recent requests. This approach separates the concerns of writing and acquiring locks.

Servers can write to the database even without initially claiming the lock, and they can make multiple requests with different timestamps during a fresh election.
