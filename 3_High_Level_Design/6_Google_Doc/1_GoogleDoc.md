# High-level design requirements of Google Docs:

1. Storing, retrieving, and editing documents
2. Sharing permissions: READ, EDIT, LINK-SHARING
3. Notifications on email
4. Version History
5. Spell Checking\*
6. Comments Support
7. Offline and Collaborative Editing

# Document Schema

Document Database Schema

1. What would be the database schema of a stored document?
2. How would we store the metadata of the document?
3. What technology solution should we use to store documents? File Storage, RDBMS or NoSQL?

# Storing Documents

1. How large can a document be?
2. How do we store a document of any size?
3. Where should we store this document? What type of database is suitable for this?

# Version History

Maintaining version history in a document that is updated often is a challenge.

- With what frequency should we store versions of this document?
- Where do we store these versions?
- How do we store changes?

# Avoiding Thundering Herds in Crons

**Problem** : How do you take a single job of size _X_ , to be done in _Y_ time, and have a constant flow of X/Y operations in your system?

**Challenge** : This is a cron job, so the operation is called from time to time.

**Solution** : Hash the job candidates into Y pieces, and run cron jobs at much smaller intervals.

# Compression and Caching

We use two ideas here to save on costs, while speeding up queries:

1. Compression
2. Caching the most recent version

# Concurrent Writes with Locks

Can we wing it?

Are concurrent writes with multiple users in different regions possible with locking (optimistic or pessimistic)?

# Operational Transform Overview

What is the heart of the concurrent document update algorithm?

We need a method by which multiple users can make changes (possibly offline), on the same document, without completely overriding each other's work.

This calls for some reconciliation algorithm. We talk about two major classes (Centralised and Decentralised). Since Google Docs would prefer a centralized algorithm with a single source of truth and low compute requirements on client devices, we choose the operational transform.

# Permission Management

How do you manage permissions to update, view or share a document?

We use a permission manager service to keep track off all permissions in a document, stored in a NoSQL store.
