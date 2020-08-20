While maintaining full compatibility with the open-source Elasticsearch kernel, Tencent Cloud ES team has been continuously and thoroughly exploring and optimizing the kernel based on its rich experience in large-scale applications in various use cases so as to enhance cluster performance, improve stability, and reduce costs. In addition, it has also been maintaining close communications with the open-source community. This document describes the kernel optimizations.

The following table summarizes the key kernel optimizations that the ES team has made **by July 2020** since the start of its kernel research:
<table class="tg">
  <tbody><tr>
    <th class="tg-llyw">Optimization Dimension</th>
    <th class="tg-llyw">Optimization Category</th>
    <th class="tg-llyw">Optimization Policy</th>
    <th class="tg-llyw">	Supported Versions</th>
  </tr>
<tr>
    <td class="tg-0pky"  rowspan="2">Performance</td>
    <td class="tg-0pky">Write performance</td>
    <td class="tg-0pky">The translog lock mechanism is optimized, increasing the overall write performance by 20%. Write deduplication and segment file cropping are optimized, increasing the performance of writes with primary keys by over 50%.</td>
    <td class="tg-0pky">7.5.1</td>
  </tr>
	<tr>
    <td class="tg-0pky">Query performance</td>
    <td class="tg-0pky"><li>The aggregation performance is optimized, making query pruning more efficient and improving the composite aggregation performance by 3–7 times in sorting scenarios.
<li>The query cache is optimized by canceling data caches with high overloads and low hit rates, reducing query glitches from 750 ms to 50 ms in actual use cases.
<li>The merge policies are optimized by developing proprietary tiered merge policies based on time series and size similarity and auto cold shard merge policy, improving the query performance by over 40% in search scenarios.
<li>Sequence capture in the query fetch phase is optimized, increasing the cache hit rate and improving the performance by over 10% in scenarios where the result set is large.</td>
    <td class="tg-0pky">6.4.3, 6.8.2, 7.5.1</td>
  </tr>
<tr>
    <td class="tg-0pky"  rowspan="4">Stability</td>
    <td class="tg-0pky">Availability</td>
    <td class="tg-0pky"><li>Traffic can be limited through a smooth line curve at the access layer.<li>The coordinator node performs memory bloat estimation after receiving results returned by the data node to check whether the estimated memory will exceed the limit.<li>Result sets of large aggregated queries are checked in a streaming manner, and requests will be canceled if the used memory reaches the threshold.<li>The proprietary single request circuit breaker can prevent large queries from occupying excessive resources and thus affecting other queries.<li>Node crashes and cluster avalanches caused by high-concurrence writes and large queries are significantly reduced, and the overall availability is increased to 99.99%.
</td>
    <td class="tg-0pky">6.4.3, 6.8.2, 7.5.1</td>
  </tr>
<tr>
    <td class="tg-0pky">Balancing policy</td>
    <td class="tg-0pky"><li>Balancing policies based on index and node distribution are introduced, alleviating the serious uneven allocation of shards caused by new nodes added to the cluster.<li>The uneven allocation of shards among multiple disks (multiple data directories) is alleviated.<li>The balance of shards of newly created indices in cluster scale-out scenarios and multiple-disk scenarios is improved, reducing OPS costs.
</td>
    <td class="tg-0pky">5.6.4, 6.4.3, 6.8.2, 7.5.1</td>
  </tr>
	<tr>
    <td class="tg-0pky">Rolling restart speed</td>
    <td class="tg-0pky"><li>The logic of reusing local data for shards in case of node restart is optimized.<li>The restoration of shard copies within a scheduled delay time period can be precisely controlled.
The time to restart one single node in a large cluster is reduced from over 10 minutes to 1 minute.
</td>
    <td class="tg-0pky">6.4.3, 6.8.2, 7.5.1</td>
  </tr>
<tr>
    <td class="tg-0pky">Online master switch</td>
    <td class="tg-0pky">The proprietary online master switch feature allows you to switch the master online in seconds by specifying the preferred master through APIs. Typical use cases include:
<li>You can switch online from the current heavily loaded master to a node with a higher specification and a lower load during manual OPS.
<li>During rolling restart, you can restart the master node last and quickly switch the master role to another node before the restart, which helps reduce the service interruption from minutes to seconds.
</td>
    <td class="tg-0pky">6.4.3, 6.8.2, 7.5.1</td>
  </tr>
	<tr>
	 <td class="tg-0pky"  rowspan="2">Cost</td>
    <td class="tg-0pky">Memory</td>
    <td class="tg-0pky"><li>The proprietary off-heap cache helps achieve FST off-heap optimization.<li>The off-heap cache ensures that the FST reclaim policy is controllable.<li>The precise eviction policy improves the cache hit rate.<li>Zero-copy and multi-level caches guarantee high access performance.<li>The heap memory overheads are significantly reduced, the GC time is decreased by over 10%, and the disk capacity of a single node can reach 50 TB, with read/write performance generally unaffected.
</td>
    <td class="tg-0pky">6.8.2, 7.5.1</td>
  </tr>
	<tr>
    <td class="tg-0pky">Storage</td>
    <td class="tg-0pky"><li>The proprietary ID field-based row storage cropping algorithm reduces storage costs by over 20% in time series scenarios.<li>A new compression algorithm is introduced, increasing the compression ratio by 30%–50% and the compression performance by 30%.
</td>
    <td class="tg-0pky">5.6.4, 6.4.3, 6.8.2, 7.5.1</td>
  </tr>
</tbody></table>

