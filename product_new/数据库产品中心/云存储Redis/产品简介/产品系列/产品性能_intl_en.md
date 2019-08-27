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
<td align="center">Compatible Redis versions</td>
<td align="center">2.8</td>
<td align="center">4.0</td>
<td align="center">4.0</td>
</tr>
<tr>
<td align="center">Memory specification</td>
<td align="center">1-60 GB</td>
<td align="center">1-60 GB</td>
<td align="center">12 GB - 4 TB</td>
</tr>
<tr>
<td align="center">Number of shards</td>
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
<td align="center">Number of connections</td>
<td align="center">10,000</td>
<td align="center">10,000</td>
<td align="center">10,000/shard</td>
</tr>
<tr>
<td align="center">Traffic limit</td>
<td align="center">10-64 MB/s</td>
<td align="center">10-64 MB/s</td>
<td align="center">72 MB/s - 5 GB/s</td>
</tr>
<tr>
<td align="center">Multi-DB</td>
<td align="center">Supported</td>
<td align="center">Supported</td>
<td align="center">Not supported</td>
</tr>
<tr>
<td align="center">Mget, Mset</td>
<td align="center">Supported</td>
<td align="center">Supported</td>
<td align="center">Supported</td>
</tr>
<tr>
<td align="center">Lua</td>
<td align="center">Supported</td>
<td align="center">Supported</td>
<td align="center">Supported (cross-slot access not supported)</td>
</tr>
<tr>
<td align="center">Horizontal scaling</td>
<td align="center">-</td>
<td align="center">-</td>
<td align="center">Supported</td>
</tr>
<tr>
<td align="center">Vertical scaling</td>
<td align="center">-</td>
<td align="center">-</td>
<td align="center">Supported</td>
</tr>
<tr>
<td align="center">Read-write separation</td>
<td align="center">Not supported</td>
<td align="center">Supported</td>
<td align="center">Supported</td>
</tr>
<tr>
<td align="center">GEO</td>
<td align="center">Not supported</td>
<td align="center">Supported</td>
<td align="center">Supported</td>
</tr>
<tr>
<td align="center">Number of replicas</td>
<td align="center">0-1</td>
<td align="center">1-5</td>
<td align="center">1-5</td>
</tr>
</tbody></table>






### Number of Connections and Traffic of Different Instance Specifications
**Redis Community Engine**

| Specification (GB) | Maximum Connections | Maximum Throughput (MB/s) |
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



Cluster Edition connections = Number of connections per shard * number of shards
Cluster Edition throughput = Shard throughput * number of shards
> After scaling, legacy instances capable of up to 9,000 connections will be capable of 10,000 ones.

