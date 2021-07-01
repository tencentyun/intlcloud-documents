## Background
Lucene currently supports two compression algorithms for storing document fields data:
- LZ4 
- Deflate

LZ4 has a higher compression and decompression speed, while Deflate has a higher compression ratio. They have obvious differences in performance and compression ratio. Based on these two existing compression algorithm, you cannot get a good balance between compression ratio and performance. Lucene uses LZ4 by default.

## Optimized Scheme
ES integrates the industry-leading advanced compression algorithm Zstandard (ZSTD) to improve the compression ratio while reducing the performance loss.

### Strengths of Zstandard compression algorithm
The Zstandard compression algorithm **has the strengths of both LZ4 and Deflate**: its performance is equivalent to that of LZ4 (tests with log data show that Zstandard is slightly better than LZ4), while its compression ratio is only slightly lower than that of Deflate.

The following are the comparison results of the three compression algorithms:

| **Compression Algorithm** | **Load Time (1 Shard)** | **Load Time (5 Shards)** | **Fields(\*fdt) File Size** | **Total Index Size** |
| -------------------- | --------------------- | ---------------------- | ------------------------- | -------------- |
| LZ4                  | 1143769 ms             | 420447 ms               | 4.15 GB                   | 6.3 GB         |
| Deflate              | 1270408 ms             | 448738 ms               | 2.56 GB                   | 4.7 GB         |
| Zstandard(16K Chunk) | 1109414 ms             | 415256 ms               | 2.93 GB                   | 5.1 GB         |
| Zstandard(32K Chunk) | 1088959 ms             | 406661 ms               | 2.67 GB                   | 4.8 GB         |

>!
1. Test data: based on a typical log application.
2. Test method: based on Elasticsearch REST High Level Client API.

## Directions
### Based on REST High Level Client API
When creating an index, add the `index.codec` configuration item for `CreateIndexRequest` and set the value to `zstandard`:
```
CreateIndexRequest createRequest = new CreateIndexRequest(indexName);
 createRequest.settings(Settings.builder()
   .put("index.number_of_shards", shards)
   .put("index.number_of_replicas", replicas)
   .put("index.codec", "zstandard")
 );
```

### Based on HTTP request
Similarly, add the `index.codec` configuration item in `settings` and set the value to `zstandard`:
```
PUT /newIndex 
{
   "settings": {
     "**index.codec**": "**zstandard**",
     "index.number_of_shards": 1
   }
} 
```

## Optimization Effect
ZSTD has a 35% higher row storage compression ratio than LZ4 and a performance comparable to that of LZ4.

## Supported Versions
 6.8.2, 7.5.1, and 7.10.1
