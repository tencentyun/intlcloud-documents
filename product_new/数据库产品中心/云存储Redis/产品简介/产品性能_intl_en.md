## Specifications
### Redis Community Engine
<table>
<thead>
<tr>
<th align="center">Feature</th>
<th colspan="2" >Standard Edition</th>
<th align="center">Cluster Edition</th>
</tr>
</thead>
<tbody><tr>
<td align="center">Redis-Compatible Versions</td>
<td align="center">2.8</td>
<td align="center">4.0</td>
<td align="center">4.0</td>
</tr>
<tr>
<td align="center">Memory</td>
<td align="center">256 MB - 60 GB</td>
<td align="center">1-60 GB</td>
<td align="center">12 GB - 4 TB</td>
</tr>
<tr>
<td align="center">Shard Count</td>
<td align="center">-</td>
<td align="center">-</td>
<td align="center">3-128</td>
</tr>
<tr>
<td align="center">QPS</td>
<td align="center">80,000-100,000</td>
<td align="center">80,000-100,000</td>
<td align="center">Tens of millions</td>
</tr>
<tr>
<td align="center">Max Connections</td>
<td align="center">10,000</td>
<td align="center">10,000</td>
<td align="center">10,000/shard</td>
</tr>
<tr>
<td align="center">Traffic Limit</td>
<td align="center">10-64 MB/s</td>
<td align="center">10-64 MB/s</td>
<td align="center">72 MB/s - 5 GB/s</td>
</tr>
<tr>
<td align="center">Multi-DB</td>
<td align="center">Yes</td>
<td align="center">Yes</td>
<td align="center">No</td>
</tr>
<tr>
<td align="center">Mget, Mset</td>
<td align="center">Yes</td>
<td align="center">Yes</td>
<td align="center">Yes</td>
</tr>
<tr>
<td align="center">Lua</td>
<td align="center">Yes</td>
<td align="center">Yes</td>
<td align="center">Yes (cross-slot access not supported)</td>
</tr>
<tr>
<td align="center">Horizontal Scaling</td>
<td align="center">-</td>
<td align="center">-</td>
<td align="center">Yes</td>
</tr>
<tr>
<td align="center">Vertical Scaling</td>
<td align="center">-</td>
<td align="center">-</td>
<td align="center">Yes</td>
</tr>
<tr>
<td align="center">Read-write Separation</td>
<td align="center">No</td>
<td align="center">Yes</td>
<td align="center">Yes</td>
</tr>
<tr>
<td align="center">GEO</td>
<td align="center">No</td>
<td align="center">Yes</td>
<td align="center">Yes</td>
</tr>
<tr>
<td align="center">Replica Count</td>
<td align="center">0-1</td>
<td align="center">1-5</td>
<td align="center">1-5</td>
</tr>
</tbody></table>

>The 256 MB specification is an entry-level trial version. It is only suitable for functionality verification in test environments but not recommended for production environments. Therefore, other specifications currently cannot be scaled down to the 256 MB specification.

### CKV Engine

| Feature | Standard Edition | Cluster Edition |
| :-------------: | :---------: | :-----------: |
| Redis-Compatible Versions | 3.2       | 3.2         |
| Memory        | 4 GB - 384 GB | 12 GB - 48 TB |
| Shard Count         | -         | 3-128     |
| QPS           |  80,000-120,000    | Tens of millions      |
| Max Connections     |  12,000-24,000    | 12,000-24,000/shard      |
| Traffic Limit           |  16-256 MB/s    | 72 MB/s - 32 GB/s      |
| Multi-DB       |      Yes        |       Yes        |
| Mget, Mset |     Yes     |      Yes      |
| Lua          |      Yes     |     Partially supported     |
| Horizontal Scaling |    -      |       Yes       |
| Vertical Scaling |    -       |    No      |
| Read-write Separation |    No      |    No      |
| GEO |      Yes      |     Yes     |



### Number of Connections and Traffic of Different Instance Specifications
**Redis Community Engine**

| Specification (GB) | Max Connections | Max Throughput (MB/s) |
|  :----------: |  :----------: |  :-------------------: |
| 0.25          | 3,000       | 10                  |
| 1          | 10,000       | 16                  |
| 2          | 10,000       | 24                  |
| 4          | 10,000       | 24                  |
| 8          | 10,000       | 24                  |
| 12         | 10,000       | 32                  |
| 16         | 10,000       | 32                  |
| 20         | 10,000       | 48                  |
| 24         | 10,000       | 48                  |
| 32         | 10,000       | 48                  |
| 40         | 10,000       | 64                  |
| 48         | 10,000       | 64                  |
| 60         | 10,000       | 64                  |

**CKV Engine**

| Specification (GB) | Max Connections | Max Throughput (MB/s) |
|  :----------: |  :----------: |  :-------------------: |
| 4          | 10,000       | 24                  |
| 8          | 10,000       | 24                  |
| 16         | 10,000       | 32                  |
| 24         | 10,000       | 32                  |
| 32         | 10,000       | 32                  |
| 48         | 18,000      | 64                  |
| 64         | 18,000      | 64                  |
| 80         | 18,000      | 64                  |
| 96         | 18,000      | 64                  |
| 128        | 24,000      | 128                 |
| 160        | 24,000      | 128                 |
| 192        | 24,000      | 128                 |
| 256        | 24,000      | 256                 |
| 320        | 24,000      | 256                 |
| 384        | 24,000      | 256                 |

Cluster edition connections = number of connections per shard * shard count;  
Cluster edition throughput = shard throughput * shard count
>After scaling, legacy instances capable of up to 9,000 connections will be capable of 10,000 ones.

## Performance Data
### Performance Reference Values
The performance may vary by Redis command and its execution time in a production environment. The test values in this document are obtained based on specific parameters and for reference only. To get the actual performance values, perform a test on your actual business.

 - Single-node Test Performance

| Redis Instance Specification | Connections | QPS |
|:---------:|:---------:|:--------:|
| Standard Edition, 8 GB | 10,000 | 80,000-100,000 |
| Cluster Edition, 8 GB (single shard) | 10,000 | 80,000-100,000 |
| CKV Standard Edition, 8 GB|  12,000    |   80,000-120,000  |


 - Cluster Edition Test Performance
   Cluster edition performance = standard edition performance * shard count;  
   Cluster edition (CKV) performance = standard edition (CKV) performance * shard count


### Test Method

 - Test Environment

| Number of CVM Instances for Stress Test Client | CVM Cores | CVM Memory | Region | Redis Instance Specification |
|:---------:|:---------:|:---------:|:---------:|:---------:|
| 3 | 2 | 8 GB | Guangzhou Zone 2 | Redis Standard Edition, 8 GB |
| 3 | 2 |8 GB | Guangzhou Zone 2 | CKV Standard Edition, 8 GB |


 - Test Parameters
 ```
redis-benchmark -h 10.66.187.x -p 6379 -a crs-1znib6aw:chen2016 -t set -c 3500 -d 128 -n 25000000 -r 5000000
redis-benchmark -h 10.66.187.x -p 6379 -a crs-1z5536aw:chen2016 -t set -c 3500 -d 128 -n 25000000 -r 5000000
redis-benchmark -h 10.66.187.x -p 6379 -a crs-090rjlih:1234567 -t set -c 3500 -d 128 -n 25000000 -r 5000000
 ```
 - QPS Calculation
Sum of the QPS values of 3 stress test clients (redis-benchmark).


