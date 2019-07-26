## 规格系列
### Redis 社区版引擎
<table>
<thead>
<tr>
<th align="center">功能</th>
<th colspan="2" >标准版</th>
<th align="center">集群版</th>
</tr>
</thead>
<tbody><tr>
<td align="center">兼容 Redis 版本</td>
<td align="center">2.8</td>
<td align="center">4.0</td>
<td align="center">4.0</td>
</tr>
<tr>
<td align="center">内存规格</td>
<td align="center">1GB - 60GB</td>
<td align="center">1GB - 60GB</td>
<td align="center">12GB - 4TB</td>
</tr>
<tr>
<td align="center">分片数</td>
<td align="center">-</td>
<td align="center">-</td>
<td align="center">3 – 128</td>
</tr>
<tr>
<td align="center">QPS</td>
<td align="center">8万 - 10万</td>
<td align="center">8万 - 10万</td>
<td align="center">千万级</td>
</tr>
<tr>
<td align="center">链接数</td>
<td align="center">10000</td>
<td align="center">10000</td>
<td align="center">10000/分片</td>
</tr>
<tr>
<td align="center">流量限制</td>
<td align="center">10MB/S - 64MB/S</td>
<td align="center">10MB/S - 64MB/S</td>
<td align="center">72MB/S - 5GB/S</td>
</tr>
<tr>
<td align="center">多 DB</td>
<td align="center">支持</td>
<td align="center">支持</td>
<td align="center">不支持</td>
</tr>
<tr>
<td align="center">Mget、Mset</td>
<td align="center">支持</td>
<td align="center">支持</td>
<td align="center">支持</td>
</tr>
<tr>
<td align="center">lua</td>
<td align="center">支持</td>
<td align="center">支持</td>
<td align="center">支持（不支持跨 Slot 访问）</td>
</tr>
<tr>
<td align="center">水平扩容</td>
<td align="center">-</td>
<td align="center">-</td>
<td align="center">支持</td>
</tr>
<tr>
<td align="center">垂直扩容</td>
<td align="center">-</td>
<td align="center">-</td>
<td align="center">支持</td>
</tr>
<tr>
<td align="center">读写分离</td>
<td align="center">不支持</td>
<td align="center">支持</td>
<td align="center">支持</td>
</tr>
<tr>
<td align="center">支持 GEO</td>
<td align="center">不支持</td>
<td align="center">支持</td>
<td align="center">支持</td>
</tr>
<tr>
<td align="center">副本数</td>
<td align="center">0 - 1</td>
<td align="center">1 - 5</td>
<td align="center">1 - 5</td>
</tr>
</tbody></table>






### 实例规格对应连接数和流量
**Redis 社区版引擎**

| 规格（GB） | 最大连接数 | 最大吞吐量（MB/s） |
|  :----------: |  :----------: |  :-------------------: |
| 0.25          | 3000       | 10                  |
| 1          | 10000       | 16                  |
| 2          | 10000       | 24                  | 
| 4          | 10000       | 24                  |
| 8          | 10000       | 24                  |
| 12         | 10000       | 32                  | 
| 16         | 10000       | 32                  | 
| 20         | 10000       | 48                  |
| 24         | 10000       | 48                  | 
| 32         | 10000       | 48                  | 
| 40         | 10000       | 64                  | 
| 48         | 10000       | 64                  | 
| 60         | 10000       | 64                  | 



集群版连接数 = 分片连接数 * 分片数
集群版吞吐量 = 分片吞吐量 * 分片数
>!9000连接数的老实例，经过扩容或降配后连接数会自动变成10000。

