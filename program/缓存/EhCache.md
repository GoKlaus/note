# EhCache

[toc]

## 基本术语（Basic Terms）

### Cache

Wiktionary defines a cache as "a store of things that will be required in the future, and can be retrieved rapidly." A cache is a collection of temporary data that either duplicates data located elsewhere or is the result of a computation. Data that is already in the cache can be repeatedly accessed with minimal costs in terms of time and resources.

### Cache hit

When a data element is requested from cache and the element exists for the given key, it is referred to as a *cache hit* (or simply, "a hit").

### Cache miss

When a data element is requested from cache and the element does not exist for the given key, it is referred to as a *cache miss* (or simply, "a miss").

### System-of-Record

The authoritative source of truth for the data. The cache acts as a local copy of data retrieved from or stored to the system-of-record (SOR). The SOR is often a traditional database, although it might be a specialized file system or some other reliable long-term storage. For the purposes of using Ehcache, the SOR is assumed to be a database.

## Topology Types

拓扑学类型

* Standalone  单机---The data set is held in the application node. Any other application nodes are independent with no communication between them. If a standalone topology is used where there are multiple application nodes running the same application, then there is Weak Consistency between them. They contain consistent values for immutable data or after the time-to-live on an element has completed and the element needs to be reloaded.

* Distributed  分布式----The data is held in a remote server (or array of servers) with a subset of recently used data held in each application node. This topology offers a rich set of consistency options.

  A distributed topology is the recommended approach in a clustered or scaled-out application environment. It provides the highest level of performance, availability, and scalability. *The distributed topology is available only with BigMemory Max.*

* Replicated  ---The cached data set is held in each application node and data is copied or invalidated across the nodes without locking. Replication can be either asynchronous or synchronous, where the writing thread blocks while propagation occurs. The only consistency mode supported in this topology is Weak Consistency.

Many production applications are deployed in clusters of multiple instances for availability and scalability. However, without a distributed or replicated cache, application clusters exhibit a number of undesirable behaviors, such as:

* Cache Drift - If each application instance maintains its own cache, updates made to one cache will not appear in the other instances. This also happens to web session data. A distributed or replicated cache ensures that all of the cache instances are kept in sync with each other.
* Database Bottlenecks - In a single-instance application, a cache effectively shields a database from the overhead of redundant queries. However, in a distributed application environment, each instance must load and keep its own cache fresh. The overhead of loading and refreshing multiple caches leads to database bottlenecks as more application instances are added. A distributed or replicated cache eliminates the per-instance overhead of loading and refreshing multiple caches from a database.

## Storage Tiers

缓存存储的三个级别

|              | 位置 | 速度 |
| ------------ | ---- | ---- |
| MemoryStore  |      | 最快 |
| OffHeapStore |      | 适中 |
| DiskStore    |      | 最慢 |

You can divide a cache or in-memory data set across the following storage areas, referred to as *tiers*:

* MemoryStore – On-heap memory used to hold cache elements. This tier is subject to Java garbage collection.
* OffHeapStore – Provides overflow capacity to the MemoryStore. Limited in size only by available RAM. Not subject to Java garbage collection (GC). Available only with Terracotta BigMemory products.
* DiskStore – Backs up in-memory cache elements and provides overflow capacity to the other tiers

### MemoryStore

The memory store is always enabled and exists in heap memory. It has the following characteristics:

* It accepts all data, whether serializable or not.
* It is the fastest storage option.
* Is thread safe for use by multiple concurrent threads.

If you use OffHeapStore (available with the BigMemory products only), ==MemoryStore holds a copy of the hottest subset of data from the OffHeapStore.==

All caches specify their maximum in-memory size, in terms of the number of elements, at configuration time.

When an element is added to a cache and it goes beyond its maximum memory size, an existing element is either deleted, if overflow is not enabled, or evaluated for spooling to another tier, if overflow is enabled.

If overflow is enabled, a check for expiry is carried out. If it is expired it is deleted; if not it is spooled.

### OffHeapStore

The OffHeapStore extends a cache to memory outside the of the Java heap. This store, which is not subject to Java garbage collection (GC), is limited only by the amount of RAM available. Using OffHeapStore, you can create extremely large local caches. *OffHeapStore is only available with the Terracotta BigMemory products.*

Because off-heap data is stored in bytes, only data that is Serializable is suitable for the OffHeapStore. Any non serializable data overflowing to the OffHeapMemoryStore is simply removed, and a WARNING level log message is emitted.

Since serialization and deserialization take place on putting and getting from the off-heap store, it is theoretically slower than the MemoryStore. This difference, however, is mitigated when garbage collection associated with larger heaps is taken into account.

For the best performance, you should allocate to a cache as much heap memory as possible without triggering GC pauses. Then, use the OffHeapStore to hold the data that cannot fit in heap (without causing GC pauses).

### DiskStore

The DiskStore provides a thread-safe disk-spooling facility that can be used for either additional storage or persisting data through system restarts.

```
Note:  
The DiskStore tier is available only for local (standalone) instances of cache. When you use a distributed cache (available only in BigMemory Max), a Terracotta Server Array is used instead of a disk tier.
```

Only data that is Serializable can be placed in the DiskStore. Writes to and from the disk use ObjectInputStream and the Java serialization mechanism. Any non-serializable data overflowing to the disk store is removed and a NotSerializableException is thrown. Be aware that serialization speed is affected by the size of the objects being serialized and their type. For example, it has been shown that:

* The serialization time for a Java object consisting of a large Map of String arrays was 126ms, where the serialized size was 349,225 bytes.
* The serialization time for a byte[] was 7ms, where the serialized size was 310,232 bytes.

Byte arrays are 20 times faster to serialize, making them a better choice for increasing disk-store performance.

Configuring a disk store is optional. If all caches use only memory and off-heap stores, then there is no need to configure a disk store. This simplifies configuration, and uses fewer threads.

## Automatic Resource Control

自动资源控制

Automatic Resource Control (ARC) gives you fine-grained（细粒度的） controls for tuning performance and enabling trade-offs between throughput, latency and data access. Independently adjustable configuration parameters include differentiated tier-based sizing and pinning hot or eternal data in the most effective tier.

ARC offers a wealth of benefits, including:

* Sizing limitations on in-memory caches to avoid OutOfMemory errors（缓存内存设置避免oom错误）
* Pooled sizing – no requirement to size caches individually
* Differentiated tier-based sizing for flexibility（灵活分级的差异化配置内存大小）
* Sizing by bytes, entries, or percentages for more flexibility

### Dynamically Sizing Stores

Tuning often involves sizing stores appropriately. There are a number of ways to size the different Ehcache storage tiers using simple configuration sizing attributes. For information about how to tune tier sizing by configuring dynamic allocation of memory and automatic balancing, see "Sizing Storage Tiers" in the *Configuration Guide* for Ehcache.

### Pinning Data

One of the most important aspects of running a cache involves managing the life of the data in each tier. For more information about managing life of data in a tier using pinning, expiration, and eviction











参考：

[阿姆达法则][]

[Ehcache2][]

[sl4j-log4j12][]





















[Ehcache2]: http://www.ehcache.org/generated/2.10.4/html/ehc-all/#page/Ehcache_Documentation_Set%2Fto-ehcache_online_documentation_library.html%23	"Ehcache2"



[阿姆达法则]: https://colobu.com/2016/04/14/Amdahl-s-Law/#:~:targetText=%E9%98%BF%E5%A7%86%E8%BE%BE%E5%B0%94%E5%AE%9A%E5%BE%8B,%E4%B9%8B%E5%90%8E%E6%95%88%E7%8E%87%E6%8F%90%E5%8D%87%E7%9A%84%E8%83%BD%E5%8A%9B%E3%80%82&amp;targetText=%E8%AD%AC%E5%A6%82%E8%AF%B4%EF%BC%8C%E4%BD%A0%E7%9A%84%E7%A8%8B%E5%BA%8F,%E7%9A%84%E5%8A%A0%E9%80%9F%E6%AF%94%E5%B0%B1%E6%98%AF2%E3%80%82	"阿姆达法则"
[sl4j-log4j12]: http://www.slf4j.org/legacy.html	"sl4j"

