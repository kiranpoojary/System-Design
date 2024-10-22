# Cache

Avoiding repeated work thorugh storage.

# Benefits of a cache:

1. Saves network calls
2. Avoids repeated computations
3. Reduces DB load

## Drawbacks of a cache:

1. Can be expensive
2. Potential thrashing

# Cache Policies:

## Cache Replacement Policy

policy to remove existing cache entry to add new entry when cache is full.

1. LRU
1. LFU


### **1. LRU Policy (Least Recently Used)**

In this policy, we evict the entry that has not been used for the longest. To implement this policy, we need to add another data point i.e., Last Used.

***Time interval in which Write-Around Policy Replacement Policies LRU Policy (Least Recently Used) an entry was not used = current_timestamp - LastUsed for that entry.***

### **2. LFU Policy (Least Frequently Used)**

In this policy, we evict the entry that is used least frequently(which has less read count).


## Cache Write Policy

How do you maintain the consistency of the cache?

A write policy is triggered when there is a write operation in the cache. Keep in mind that it is different from the replacement policy. A replacement policy is triggered when there is no space for a new key and a key is evicted from the cache.

A write request means some entry is added, updated or deleted in the cache. But because a cache is a source of truth each of the write requests will impact the entire system.

### 1. Write-Back Policy(Cache is truthy)

* **FLOW: write to cache only -> on replacement update it to DB**

If the key-value pair that is to be updated is present in the cache then it is updated. However, the key-value pair is not immediately updated in the database. So as long as the cache is alive, users will get consistent data. However, if the cache is not alive, the data will be stable.

***To avoid this problem we use:***

1. Timeout-Based Persistence
2. Event-Based Write Bac
3. Replacement Write Back

### 2. Write-Through Policy

* **FLOW: clear the cache entry -> on get fill the updated data to cache**

In this policy, when there is a write request, we evict the key that is being updated, while simultaneously updating the database. The next time there is a read request, that is when the cache polls the database for the entry, persists the entry and sends the response to the user.

However, we can run into problems when using this policy.

**For example,**

Initially, we have

X = 10

There is a write request for

X = 20

Then there is a read request for X, but the write request is not updated yet. So the read request returns X = 10 . So it can cause inconsistency.

To avoid such problems, we can lock the data which is to be written and only unlock the data after the update operation is completed. This policy is useful When we need a high level of consistency When we need a high level of persistence However, it is less efficient compared to the write-back policy.


### 3. Write-Around Policy(TTL)

* **FLOW: update the db -> cache has TTL it will update with latest data after cache removed by TTL**

In this policy, when we get a write request, instead of updating the entry in the cache, we update the entry in the database. Now when we get a read request, we will send the stale value from the cache. And we will be getting stale values until the entry is evicted from the cache. This policy is useful When we need a high level of efficiency When we need a high level of persistence However, it makes our system eventually consistent.


# Cache Thrashing

when lot of cache miss happened or lot of cache evicted(frequent replaced)


# Memcachd

cold region: Recently used(maintains count of use)

warm region: second recently used(maintains count of read)

**write**:- move data from cold to warm means less frequentlt to frequently region

**read**:- first check warm if not found then cold region
