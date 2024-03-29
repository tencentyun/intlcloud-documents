## 命名空间

Namespace=QCE/TDMYSQL

## 监控指标
<table style = "table-layout:fixed;">
<thead>
<tr>
<th width="20%">指标英文名</th>
<th width="20%">指标中文名</th>
<th width="20%">指标含义</th>
<th width="8%">单位</th>
<th width="20%">维度</th>
<th width="12%">统计粒度</th>
</tr>
</thead>
<tbody><tr>
<td>ActiveThread<br>CountNode</td>
<td>活跃线程数</td>
<td>DB 节点线程池活跃线程个数</td>
<td>个</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>BinlogDisk<br>AvailableNode</td>
<td>剩余 Binlog 日志磁盘空间</td>
<td>DB 节点剩余 Binlog<br>日志磁盘空间</td>
<td>GB</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>BinlogUsedDiskNode</td>
<td>已用 Binlog 日志磁盘空间</td>
<td>DB 节点已用 Binlog<br>日志磁盘空间</td>
<td>GB</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>ConnUsageRateNode</td>
<td>DB 连接使用率</td>
<td>DB 节点连接使用率，计算方式为 ThreadsConnected/ConnMax</td>
<td>%</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>CpuUsageRateNode</td>
<td>CPU 利用率</td>
<td>DB 节点 CPU 使用率</td>
<td>%</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>DataDisk<br>AvailableNode</td>
<td>可用数据磁盘空间</td>
<td>DB 节点可用数据磁盘空间</td>
<td>GB</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>DataDisk<br>UsedRateNode</td>
<td>数据磁盘空间利用率</td>
<td>DB 节点数据磁盘空间利用率</td>
<td>%</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>DeleteTotalNode</td>
<td>DELETE 请求数</td>
<td>DB 节点 Delete 请求数</td>
<td>次/秒</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>IOUsageRateNode</td>
<td>IO 利用率</td>
<td>IO 利用率</td>
<td>%</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>InnodbBuffer<br>PoolReadsNode</td>
<td>innodb 磁盘读页次数</td>
<td>DB 节点 innodb<br>磁盘读页次数</td>
<td>次</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>InnodbBufferPool<br>ReadAheadNode</td>
<td>innodb 缓冲池预读页次数</td>
<td>DB 节点 innodb<br>缓冲池预读页次数</td>
<td>次</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>InnodbBufferPool<br>ReadRequestsNode</td>
<td>innodb 缓冲池读页次数</td>
<td>DB 节点 innodb<br>缓冲池读页次数</td>
<td>次</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>InnodbRows<br>DeletedNode</td>
<td>innodb 执行 DELETE 行数</td>
<td>DB 节点 innodb<br>执行 DELETE 行数</td>
<td>行</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>InnodbRows<br>InsertedNode</td>
<td>innodb 执行 INSERT行数</td>
<td>DB 节点 innodb<br>执行 INSERT 行数</td>
<td>行</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>InnodbRowsReadNode</td>
<td>innodb 执行 READ 行数</td>
<td>DB 节点 innodb<br>执行 READ 行数</td>
<td>行</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>InnodbRows<br>UpdatedNode</td>
<td>innodb 执行 UPDATE 行数</td>
<td>DB 节点 innodb<br>执行 UPDATE 行数</td>
<td>行</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>InsertTotalNode</td>
<td>INSERT 请求数</td>
<td>DB 节点 INSERT 请求数</td>
<td>次/秒</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>LongQueryCountNode</td>
<td>慢查询数</td>
<td>DB 节点慢查询数</td>
<td>次</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>MemAvailableNode</td>
<td>可用缓存空间</td>
<td>DB 节点可用缓存空间</td>
<td>GB</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>MemHitRateNode</td>
<td>缓存命中率</td>
<td>DB 节点缓存命中率</td>
<td>%</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>ReplaceSelect<br>TotalNode</td>
<td>REPLACE_SELECT 请求数</td>
<td>DB 节点 REPLACE-SELECT<br>请求数</td>
<td>次/秒</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>ReplaceTotalNode</td>
<td>REPLACE 请求数</td>
<td>DB 节点总请求数</td>
<td>次/秒</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>RequestTotalNode</td>
<td>总请求数</td>
<td>DB 节点总请求数</td>
<td>次/秒</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>SelectTotalNode</td>
<td>SELECT 请求数</td>
<td>DB 节点 SELECT 请求数</td>
<td>次/秒</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>SlaveDelayNode</td>
<td>备延迟</td>
<td>DB 节点备延迟</td>
<td>秒</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>UpdateTotalNode</td>
<td>当前打开连接数</td>
<td>DB 节点 UPDATE 请求数</td>
<td>次/秒</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>Threads<br>ConnectedNode</td>
<td>UPDATE 请求数</td>
<td>DB 节点连接数，计算方式为 show processlist 得到的 session 个数</td>
<td>个</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>ConnMaxNode</td>
<td>最大连接数</td>
<td>DB 节点最大连接数</td>
<td>个</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
<tr>
<td>IsMaster</td>
<td>是否为主 DB</td>
<td>表示这个 DB 节点是否为主 DB</td>
<td>-</td>
<td>InstanceId,<br>NodeId</td>
<td>60s</td>
</tr>
<tr>
<td>ThreadsRunningCountNode</td>
<td>运行线程数</td>
<td>DB 节点 Threads_running 数值</td>
<td>个</td>
<td>InstanceId,<br>NodeId</td>
<td>60s、300s、 3600s、86400s</td>
</tr>
</tbody></table>

> ?每个指标的统计粒度（Period）可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度

## 各维度对应参数总览

| 参数名称                       | 维度名称   | 维度解释           | 格式                                                         |
| ------------------------------ | ---------- | ------------------ | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.Name  | InstanceId | 实例 ID 的维度名称 | 输入 String 类型维度名称：InstanceId                         |
| Instances.N.Dimensions.0.Value | InstanceId | 具体实例 ID        | 输入具体实例 ID，例如：tdsqlshard-9kjauqq1                      |
| Instances.N.Dimensions.1.Name  | NodeId     | 节点 ID 的维度名称 | 输入 String 类型维度名称：NodeId                             |
| Instances.N.Dimensions.1.Value | NodeId     | 具体节点 ID        | 输入具体节点 ID，例如：877adc0ada3e |

## 入参说明

分布式数据库 TDSQL MySQL 版-节点监控指标入参说明下：

&Namespace=QCE/TDMYSQL
&Instances.N.Dimensions.0.Name=InstanceId
&Instances.N.Dimensions.0.Value=具体实例 ID
&Instances.N.Dimensions.1.Name=NodeId
&Instances.N.Dimensions.1.Value=具体节点 ID
