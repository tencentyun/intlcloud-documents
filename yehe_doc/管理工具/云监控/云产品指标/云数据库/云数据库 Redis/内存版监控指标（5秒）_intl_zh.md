## 命名空间

Namespace=QCE/REDIS_MEM

## 监控指标

### 实例汇总 

| 指标英文名       | 指标中文名                                                   | 单位  | 维度       |
| ---------------- | ------------------------------------------------------------ | ----- | ---------- |
| MemUsed          | 实际使用内存容量，包含数据和缓存部分                         | MB    | instanceid |
| CpuUtil          | 平均 CPU 使用率                                              | %     | instanceid |
| MemUtil          | 实际使用内存和申请总内存之比                                 | %     | instanceid |
| Keys             | 实例存储的总 Key 个数（一级 Key）                            | 个    | instanceid |
| Expired          | 时间窗内被淘汰的 Key 个数，对应 info 命令输出的 expired_keys | 个    | instanceid |
| Evicted          | 时间窗内被驱逐的 Key 个数，对应 info 命令输出的 evicted_keys | 个    | instanceid |
| Connections      | 连接到实例的 TCP 连接数量                                    | 个    | instanceid |
| ConnectionsUtil  | 实际 TCP 连接数量和最大连接数比                              | %     | instanceid |
| InFlow           | 内网入流量                                                   | MB/s  | instanceid |
| InBandwidthUtil  | 内网入流量实际使用和最大流量比                               | %     | instanceid |
| InFlowLimit      | 入流量触发限流的次数                                         | 次    | instanceid |
| OutFlow          | 内网出流量                                                   | MB/S  | instanceid |
| OutBandwidthUtil | 内网出流量实际使用和最大流量比                               | %     | instanceid |
| OutFlowLimit     | 出流量触发限流的次数                                         | 次    | instanceid |
| LatencyMax       | proxy 到 redis  server 的执行时延最大值                      | ms    | instanceid |
| LatencyAvg       | proxy 到 redis  server 的执行时延平均值                      | ms    | instanceid |
| LatencyRead      | proxy 到 redis server 的读命令平均执行时延               | ms    | instanceid |
| LatencyWrite     | proxy 到 redis  server 的写命令平均执行时延              | ms    | instanceid |
| LatencyOther     | proxy 到 redis  server 的读写命令之外的命令平均执行时延   | ms    | instanceid |
| Commands         | QPS，命令执行次数                                            | 次/秒 | instanceid |
| CmdRead          | 读命令执行次数                                               | 次/秒 | instanceid |
| CmdWrite         | 写命令执行次数                                               | 次/秒 | instanceid |
| CmdOther         | 读写命令之外的命令执行次数                                   | 次/秒 | instanceid |
| CmdBigValue      | 请求命令大小超过32KB的执行次数                               | 次/秒 | instanceid |
| CmdKeyCount      | 命令访问的 Key 个数                                          | 个/秒 | instanceid |
| CmdMget          | Mget 命令执行次数                                            | 次/秒 | instanceid |
| CmdSlow          | 执行时延大于 slowlog-log-slower-than 配置的命令次数          | 次    | instanceid |
| CmdHits          | 读请求 Key 存在的个数，对应 info 命令输出的 keyspace_hits 指标 | 个    | instanceid |
| CmdMiss          | 读请求 Key 不存在的个数，对应 info 命令输出的 keyspace_misses 指标 | 个    | instanceid |
| CmdErr           | 命令执行错误的次数，例如命令不存在、参数错误等情况           | 次    | instanceid |
| CmdHitsRatio     | Key 命中/(Key 命中+KeyMiss)，该指标可以反应 Cache  Miss的情况 | %     | instanceid |
| CpuMaxUtil       | 实例中节点（分片或者副本）最大 CPU 使用率                    | %     | instanceid |
| MemMaxUtil       | 实例中节点（分片或者副本）最大内存使用率                     | %     | instanceid |

### Redis 节点 

| 指标英文名          | 指标中文名                                                   | 单位  | 维度                |
| ------------------- | ------------------------------------------------------------ | ----- | ------------------- |
| MemUsedNode         | 实际使用内存容量，包含数据和缓存部分                         | MB    | instanceid、rnodeid |
| ConnectionsNode     | Proxy 连接到节点的连接数                                     | 个    | instanceid、rnodeid |
| ConnectionsUtilNode | 节点连接数使用率                                             | %     | instanceid、rnodeid |
| CpuUtilNode         | 平均 CPU 使用率                                              | %     | instanceid、rnodeid |
| MemUtilNode         | 实际使用内存和申请总内存之比                                 | %     | instanceid、rnodeid |
| KeysNode            | 实例存储的总 Key 个数（一级 Key）                            | 个    | instanceid、rnodeid |
| ExpiredNode         | 时间窗内被淘汰的 Key 个数，对应 info 命令输出的 expired_keys | 个    | instanceid、rnodeid |
| EvictedNode         | 时间窗内被驱逐的 Key 个数，对应 info 命令输出的 evicted_keys | 个    | instanceid、rnodeid |
| ReplDelayNode       | 副本节点的相对主节点命令延迟长度                             | B     | instanceid、rnodeid |
| CommandsNode        | QPS，命令执行次数                                            | 次/秒 | instanceid、rnodeid |
| CmdReadNode         | 读命令执行次数                                               | 次/秒 | instanceid、rnodeid |
| CmdWriteNode        | 写命令执行次数                                               | 次/秒 | instanceid、rnodeid |
| CmdOtherNode        | 读写命令之外的命令执行次数                                   | 次/秒 | instanceid、rnodeid |
| CmdSlowNode         | 执行时延大于 slowlog-log-slower-than 配置的命令次数          | 次    | instanceid、rnodeid |
| CmdHitsNode         | 读请求 Key 存在的个数，对应 info 命令输出的 keyspace_hits 指标 | 个    | instanceid、rnodeid |
| CmdMissNode         | 读请求 Key 不存在的个数，对应 info 命令输出的 keyspace_misses 指标 | 次    | instanceid、rnodeid |
| CmdHitsRatioNode    | Key 命中/(Key 命中+KeyMiss)，该指标可以反应 Cache  Miss 的情况 | %     | instanceid、rnodeid |

### Proxy 节点 

| 指标英文名            | 指标中文名                                               | 单位  | 维度                |
| --------------------- | -------------------------------------------------------- | ----- | ------------------- |
| CpuUtilProxy          | Proxy CPU 使用率                                         | %     | instanceid、pnodeid |
| CommandsProxy         | Proxy 执行的命令数                                       | 次/秒 | instanceid、pnodeid |
| CmdKeyCountProxy      | 命令访问的 Key 个数                                      | 次/秒 | instanceid、pnodeid |
| CmdMgetProxy          | Mget 命令执行次数                                        | 次/秒 | instanceid、pnodeid |
| CmdErrProxy           | Proxy 命令执行错误的次数，例如命令不存在、参数错误等情况 | 次/秒 | instanceid、pnodeid |
| CmdBigValueProxy      | 请求命令大小超过32KB的执行次数                           | 次/秒 | instanceid、pnodeid |
| ConnectionsProxy      | 连接到实例的 TCP 连接数量                                | 个    | instanceid、pnodeid |
| InFlowProxy           | 内网入流量                                               | MB/S  | instanceid、pnodeid |
| OutFlowProxy          | 内网出流量                                               | MB/S  | instanceid、pnodeid |
| ConnectionsUtilProxy  | 连接数使用率                                             | %     | instanceid、pnodeid |
| InBandwidthUtilProxy  | 内网入流量实际使用和最大流量比                           | %     | instanceid、pnodeid |
| OutBandwidthUtilProxy | 内网出流量实际使用和最大流量比                           | %     | instanceid、pnodeid |
| InFlowLimitProxy      | 入流量触发限流的次数                                     | 次    | instanceid、pnodeid |
| OutFlowLimitProxy     | 出流量触发限流的次数                                     | 次    | instanceid、pnodeid |
| LatencyAvgProxy       | proxy 到 redis  server 的执行时延平均值                  | ms    | instanceid、pnodeid |
| LatencyMaxProxy       | proxy 到 redis  server 的执行时延最大值                  | ms    | instanceid、pnodeid |
| LatencyReadProxy      | proxy 到 redis  server 的读命令平均执行时延              | ms    | instanceid、pnodeid |
| LatencyWriteProxy     | proxy 到 redis  server 的写命令平均执行时延              | ms    | instanceid、pnodeid |
| LatencyOtherProxy     | proxy 到 redis  server 的读写命令之外的命令平均执行时延  | ms    | instanceid、pnodeid |

## 各维度对应参数总览

| 参数名称                       | 维度名称   | 维度解释            | 格式                                                         |
| ------------------------------ | ---------- | ------------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.Name  | instanceid | 实例 ID 维度名称    | 输入 String 类型维度名称：instanceid                         |
| Instances.N.Dimensions.0.Value | instanceid | 实例具体 ID         | 输入实例的具体 Redis 实例 ID，例如：tdsql-123456 也可以是实例串号，例如：crs-ifmymj41，可通过 [查询 Redis 实例列表接口](https://intl.cloud.tencent.com/zh/document/product/239/32065) 查询 |
| Instances.N.Dimensions.1.Name  | rnodeid    | redis 节点 ID 维度名称 | 输入 String 类型维度名称：rnodeid        |
| Instances.N.Dimensions.1.Value | rnodeid    | redis 具体节点 ID     | 输入 Redis 具体节点 ID，可以通过 [查询实例节点信息](https://intl.cloud.tencent.com/zh/document/product/239/38627) 接口获取 |
| Instances.N.Dimensions.1.Name  | pnodeid    | proxy 节点 ID 维度名称 | 输入 String 类型维度名称：pnodeid   |
| Instances.N.Dimensions.1.Value | pnodeid    | proxy 具体节点 ID     | 输入 proxy 具体节点 ID，可以通过 [查询实例节点信息](https://intl.cloud.tencent.com/zh/document/product/239/38627) 接口获取 |

## 入参说明

**查询云数据库 Redis 内存版监控数据，入参取值如下：**
&Namespace=QCE/REDIS_MEM
&Instances.N.Dimensions.0.Name=instanceid
&Instances.N.Dimensions.0.Value=实例的 ID

**查询云数据库 Redis 内存版—redis 节点监控数据，入参取值如下：**
&Namespace=QCE/REDIS_MEM
&Instances.N.Dimensions.0.Name=instanceid
&Instances.N.Dimensions.0.Value=实例的 ID
&Instances.N.Dimensions.1.Name=rnodeid 
&Instances.N.Dimensions.1.Value=Redis 节点ID

**查询云数据库 Redis 内存版— proxy 节点 监控数据，入参取值如下：**
&Namespace=QCE/REDIS_MEM
&Instances.N.Dimensions.0.Name=instanceid
&Instances.N.Dimensions.0.Value=实例的 ID
&Instances.N.Dimensions.1.Name=pnodeid
&Instances.N.Dimensions.1.Value=proxy 节点ID

