## Background
On a single ES node, the FST structure in the inverted index resides permanently in the heap memory, which uses a relatively high proportion of the memory (up to over 50% especially on cold nodes with large disks). This restricts the capability of a single node to manage disks, limits the heap memory, and thus affects the node availability. As there are very few query requests on cold nodes, storing FST in the memory is of little significance. Therefore, we need to move this part of data structure out of the heap for management, so that it is not loaded by default but loaded from the disk off heap for direct use when needed, reducing the heap memory usage and improving the single-node disk management capabilities.

## Optimized Scheme
ES implements a precisely controlled off-heap cache based on the WLFU elimination strategy and implements a second-level in-heap cache based on zero copy and weak reference. In this way, the performance is comparable to that of in-heap access.

## Directions
### Enabling/Disabling off-heap feature (disabled by default)
```
curl -H "Content-Type:application/json" -XPUT http://localhost:9200/_cluster/settings -d '{
   "persistent" : {
     "indices.segment_memory.off_heap.enable" : true
    }
}'
```

### Adjusting the size of off-heap cache (500 MB by default)
```
curl -H "Content-Type:application/json" -XPUT http://localhost:9210/_cluster/settings -d '{
  "persistent" : {
     "indices.segment_memory.off_heap.size" : "5gb"
   }
}'
```
 It can be set to 1/3 of the off-heap memory of a single node and should not exceed 32 GB. Below are specific examples:
- If the total memory of s single node (including JVM and off-heap memory) is 64 GB, it can be set to (64 – 32)/3. You can set it to 10 GB.
- If the total memory of s single node (including JVM and off-heap memory) is 96 GB, it can be set to (96 – 32)/3. You can set it to 20 GB.

## Optimization Effect
The optimized scheme works much better in terms of memory overheads, data management, and GC and has a slightly better performance.

| Scheme | FST **Storage Location** | FST Memory Usage | **Single-FST Heap Memory Usage** | **Single-Node Maximum Disk Data Volume** |
| -------- | ---------------- | ---------------------------------- | ------------------------------- | ------------------------ |
| Native scheme | Heap memory | Full storage in memory with high memory usage | MB-level (native FST data structure) | 10 TB (tuning required) |
| Optimized scheme | Off-heap memory | Cold data elimination based on cache LRU with low memory usage | Around 100 bytes (cache key size) | 50 TB |

| Write Performance | Memory Usage (MB) | GC Time (s) | TPS | 90th Percentile Latency (ms) | 99th Percentile latency (ms) |
| ------------ | ---------------- | ----------- | ------- | ------------- | ------------- |
| Native scheme     | 402.59           | 20.453      | 198051  | 463.201       | 617.701       |
| Optimized scheme     | 102.217          | 18.969      | 201188  | 455.124       | 618.379       |
| Difference         | 74.6% better          | 7.26% better     | 1.58% better | 1.74% better       | 0.11% worse       |

| Query Performance | **Memory Usage (MB)** | **GC Time (s)** | **QPS** | 90th Percentile Latency (ms) | 99th Percentile Latency (ms) |
| ------------ | -------------------- | --------------- | ------- | ------------- | ------------- |
| Native scheme     | 401.806              | 20.107          | 200.057 | 3.96062       | 11.1894       |
| Optimized scheme     | 101.004              | 19.228          | 200.087 | 3.87805       | 11.2316       |
| Difference         | 74.9% better              | 4.37% better        | -       | 2.00% better      | 0.38% worse      |

## Supported Versions
6.8.2, 7.5.1, and 7.10.1
