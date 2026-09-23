# Caching

**When?**
High read traffic → DB becomes bottleneck
Postgres ~50ms → Redis ~1ms

**Problems?**
Cache invalidation + failure handling

### 1. External Cache — Default

**Redis, Memcached**

**Pros:**

* Shared across all application servers
* Scales well
* TTL + eviction policies (e.g. LRU)

**Cons:**

* Network call → slower than in-process cache
* Cache can fail / become unavailable

### 2. CDN

**Cloudflare, Fastly, Akamai**

Geographically distributed servers that cache content close to users.

**Best for:** Static media (images, videos, files)

**Pros:**

* Lower latency by serving from nearby edge
* Reduces load on origin servers

**Cons:**

* Mainly useful for cacheable/public content
* Cache invalidation can be harder

### 3. Client-Side Cache

**Browser HTTP cache, localStorage, mobile app memory/storage**

**Pros:**

* No network call → very fast
* Reduces backend requests

**Cons:**

* Backend has limited control
* Data can become stale
* Invalidation is harder

### 4. In-Process Cache

Cache stored directly in the application's memory.

**Good for:** Config, feature flags, hot keys, small reference data

**Pros:**

* Fastest → no network call
* Simple for small, frequently accessed data

**Cons:**

* Each server has its own cache → not shared
* Updates/invalidation don't automatically propagate
* Not a replacement for Redis
