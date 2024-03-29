本文介绍常用组件端口信息。

## HDFS 常用端口

| 组件 | 端口号 | 说明                                                         |
| ---- | ------ | ------------------------------------------------------------ |
| HDFS | 4007   | NameNode RPC 端口。该端口用于：<br>1. HDFS 客户端与 NameNode 间的通信。<br>2. DataNode 与 NameNode 之间的连接。 |
| HDFS | 4008   | HDFS HTTP 端口（NameNode）。该端口用于：<br>1. 点对点的 NameNode 检查点操作。<br>2. 远程 Web 客户端连接 NameNode UI。 |
| HDFS | 4009   | HDFS HTTPS 端口（NameNode）。该端口用于：<br>1. 点对点的 NameNode 检查点操作。<br>2. 远程 Web 客户端连接 NameNode UI。 |
| HDFS | 4004   | DataNode IPC 服务器端口。该端口用于：客户端连接 DataNode 用来执行 RPC 操作。 |
| HDFS | 4001   | DataNode 数据传输端口。该端口用于：<br>1. HDFS 客户端从 DataNode 传输数据或传输数据到 DataNode。<br>2. 点对点的DataNode传输数据。 |
| HDFS | 4002   | Datanode HTTP 端口。  该端口用于：  安全模式下，远程 Web 客户端连接 DataNode UI。 |
| HDFS | 4003   | Datanode HTTPS 端口。  该端口用于：  安全模式下，远程 Web 客户端连接 DataNode UI。 |
| HDFS | 4005   | JournalNode RPC 端口。  该端口用于：  客户端通信用于访问多种信息。 |
| HDFS | 4006   | JournalNode HTTP 端口。  该端口用于：  安全模式下，远程Web客户端链接 JournalNode。 |
| HDFS | 4032   | HTTPFS HTTP 服务器侦听的端口。  该端口用于：远程 REST 接口连接 HTTPFS。 |

## YARN 常用端口

| 组件 | 端口号 | 说明                                                         |
| ---- | ------ | ------------------------------------------------------------ |
| YARN | 5024   | Job history 服务器 Web HTTP 端口。  该端口用于：查看 Job History 服务器的 Web 页面。 |
| YARN | 5022   | Job history 服务器端口。  该端口用于：  <br>1. 用于 MapReduce 客户端恢复任务的数据。  <br>2. 用于 Job 客户端获取任务报告。 |
| YARN | 5003   | ResourceManager 服务的 Web HTTP 端口。                         |
| YARN | 5002   | ResourceManager 服务的 Web HTTPs 端口。该端口用于：安全模式下，接入 ResourceManager Web 应用。 |
| YARN | 5004   | NodeManager Web HTTP 端口。                                     |
| YARN | 5005   | NodeManager Web HTTPs 端口。  该端口用于：  安全模式下，接入 NodeManager web 应用。 |
| YARN | 5001   | ResourceManager 调度器端口。                                   |
| YARN | 5000   | ResourceManager rpc 接口，用于客户端提交任务。                  |

## Hive 常用端口

| 组件 | 端口号 | 说明                                                         |
| ---- | ------ | ------------------------------------------------------------ |
| Hive | 7010   | WebHCat 提供 REST 服务的端口。  该端口用于：  WebHCat 客户端与 WebHCat 服务端之间的通信。 |
| Hive | 7001   | HiveServer 提供 Thrift 服务的端口。该端口用于：HiveServer 客户端（beeline）与 HiveServer 之间的通信。 |
| Hive | 7004   | MetaStore 提供 Thrift 服务的端口。  该端口用于：  MetaStore 客户端与 MetaStore 之间的通信，即 HiveServer 与 MetaStore 之间通信。 |
| Hive | 7003   | Hive的Web UI 端口。  该端口用 Web 请求与 Hive UI 服务器进行 HTTPS/HTTP 通信。 |


## Spark 常用端口

| 组件  | 端口号 | 说明     |
| ----- | ------ | -------- |
| Spark | 10000  | HTTP 端口 |

## Presto 常用端口

| 组件   | 端口号 | 说明                                       |
| ------ | ------ | ------------------------------------------ |
| Presto | 9000   | Presto Coordinator 或 Worker 对外提供服务的 HTTP 端口。 |

## PrestoSQL 常用端口

| 组件      | 端口号 | 说明                                          |
| --------- | ------ | --------------------------------------------- |
| PrestoSQL | 9000   | PrestoSQL Coordinator 或 Worker 对外提供服务的 HTTP 端口。 |

## Trino 常用端口

| 组件  | 端口号 | 说明                                      |
| ----- | ------ | ----------------------------------------- |
| Trino | 9000   | TRINO Coordinator 或 Worker 对外提供服务的 HTTP 端口。 |

## Impala 常用端口

| 组件   | 端口号       | 说明                                                         |
| ------ | ------------ | ------------------------------------------------------------ |
| Impala | 27000、27009 | 提供给 Impala 应用通信的端口。前者 Impala <br>2.x 使用，后者 Impala3.x 使用。|
| Impala | 27001        | 提供给 Impala-shell 通信的端口。                               |
| Impala | 27004        | ImpalaServer 的 Web 端口。                                        |
| Impala | 27007        | ImpalaCatalog 的 Web 端口。                                       |
| Impala | 27005        | ImpalaStateStore 的 Web 端口。                                    |

## Kudu 常用端口

| 组件 | 端口号 | 说明                 |
| ---- | ------ | -------------------- |
| Kudu | 7051   | KuduMaster PRC 端口。  |
| Kudu | 7050   | KuduServer RPC 端口。  |
| Kudu | 8051   | KuduMaster HTTP 端口。 |
| Kudu | 8050   | KuduServer HTTP 端口。 |

## ClickHouse 常用端口

| 组件       | 端口号 | 说明                      |
| ---------- | ------ | ------------------------- |
| ClickHouse | 9000   | 业务客户端 TCP 接入端口。   |
| ClickHouse | 8123   | 业务客户端 HTTP 接入端口。  |
| ClickHouse | 9009   | 业务客户端 HTTPS 接入端口。 |

## Kylin 常用端口

| 组件  | 端口号 | 说明           |
| ----- | ------ | -------------- |
| Kylin | 16500  | Kylin HTTP 端口。 |

## Doris 常用端口

| 组件  | 端口号 | 说明                                                |
| ----- | ------ | --------------------------------------------------- |
| Doris | 8000   | Broker 上的 Thrift server 端口。                       |
| Doris | 9060   | BE 上 Thrift server 的端口，用于接收来自 FE 的请求。  |
| Doris | 8060   | BE 上的 brpc 端口，用于 BE 之间通讯。                 |
| Doris | 9050   | BE 上心跳服务端口（thrift），用于接收来自 FE 的心跳。 |
| Doris | 8040   | Broker 上的 Thrift server，用于接收请求。             |
| Doris | 9010   | FE 上的 元数据管理模块（bdbje ）之间通信用的端口。    |
| Doris | 8030   | FE 上的 HTTP server 端口。                            |
| Doris | 9020   | FE 上的 Thrift server 端口。                          |
| Doris | 9030   | FE 上接收 Mysql client 访问端口。                      |

## StarRocks 常用端口

| 组件      | 端口号 | 说明                                                |
| --------- | ------ | --------------------------------------------------- |
| StarRocks | 8000   | Broker 上的 Thrift server 端口。                       |
| StarRocks | 9060   | BE 上 Thrift server 的端口，用于接收来自 FE 的请求。  |
| StarRocks | 8060   | BE 上的 brpc 端口，用于 BE 之间通讯。                 |
| StarRocks | 9050   | BE 上心跳服务端口（thrift），用于接收来自 FE 的心跳。 |
| StarRocks | 8040   | Broker 上的 Thrift server，用于接收请求。             |
| StarRocks | 9010   | FE 上的 元数据管理模块（bdbje ）之间通信用的端口。    |
| StarRocks | 8030   | FE 上的 HTTP server 端口。                            |
| StarRocks | 9020   | FE 上的 Thrift server 端口。                          |
| StarRocks | 9030   | FE 上接收 Mysql client 访问端口。                     |

## Druid 常用端口

| 组件  | 端口号 | 说明                                                         |
| ----- | ------ | ------------------------------------------------------------ |
| Druid | 8082   | broker 服务端监听端口（broker-runtime.properites），用于接收客户端查询。 |
| Druid | 8081   | coordinator 服务端监听端口（coordinator -runtime.properites），用于与其它组件进行通信。 |
| Druid | 8083   | historical 服务端监听端口（historical-runtime.properites），用于与其它组件进行通信。 |
| Druid | 8091   | middleManager 服务端监听端口（middleManager-runtime.properites），用于与其它组件进行通信。 |
| Druid | 8090   | overlord 服务端监听端口（overlord-runtime.properites），用于与其它组件进行通信。 |
| Druid | 18888  | router 服务端监听端口（router-runtime.properites），用于路由客户端查询到 broker。 |

## HBase 常用端口

| 组件  | 端口号 | 说明                                                         |
| ----- | ------ | ------------------------------------------------------------ |
| HBase | 6000   | HMaster RPC 端口。该端口用于 HBase 客户端连接到 HMaster。    |
| HBase | 6001   | HMaster HTTPS 端口。该端口用于远程 Web 客户端连接到 HMaster UI。 |
| HBase | 6002   | RS （RegoinServer） RPC 端口。该端口用于 HBase 客户端连接到 RegionServer |
| HBase | 6003   | RegionServer HTTPS 端口。该端口用于远程 Web 客户端连接到 RegionServer UI。 |
| HBase | 6005   | Hbase Thrift Server 的 Info Server 侦听端口。                |
| HBase | 6004   | Hbase Thrift Server 侦听端口。                               |

## Flink 常用端口

| 组件  | 端口号 | 说明                                                         |
| ----- | ------ | ------------------------------------------------------------ |
| Flink | 16001  | Flink的Web UI端口。该端口用于：Client Web请求与Flink server进行HTTP/HTTPS通信。 |

Storm 常用端口

| 组件  | 端口号 | 说明               |
| ----- | ------ | ------------------ |
| Storm | 15002  | Logviewer 服务端口。 |
| Storm | 15000  | Nimbus 服务端口。     |
| Storm | 15001  | Storm Web UI  。     |

## Hue 常用端口

| 组件 | 端口号 | 说明                                                         |
| ---- | ------ | ------------------------------------------------------------ |
| Hue  | 13000  | Hue 提供 HTTPS 服务端口。  该端口用于：HTTPS 方式提供 Web 服务，支持修改。 |

## Oozie 常用端口

| 组件  | 端口号 | 说明                     |
| ----- | ------ | ------------------------ |
| Oozie | 12000  | HTTP 端口，用于客户端访问。 |

## Superset 常用端口

| 组件     | 端口号 | 说明                             |
| -------- | ------ | -------------------------------- |
| Superset | 18088  | Superset 服务端口，用于客户端连接。 |

## Zeppelin 常用端口

| 组件     | 端口号 | 说明                             |
| -------- | ------ | -------------------------------- |
| Zeppelin | 18000  | Zeppelin 服务端口，用于客户端连接。 |

## Kafka 常用端口

| 组件  | 端口号 | 说明                           |
| ----- | ------ | ------------------------------ |
| Kafka | 9092   | Broker 提供数据接收、获取服务。 |

## KafkaManager 常用端口

| 组件         | 端口号 | 说明                                       |
| ------------ | ------ | ------------------------------------------ |
| KafkaManager | 9000   | Kafkamanager 服务端监听端口，用于客户端连接。 |

## Ranger 常用端口

| 组件   | 端口号 | 说明                        |
| ------ | ------ | --------------------------- |
| Ranger | 6080   | Ranger Admin web UI。         |
| Ranger | 5151   | RangerUsersync 认证服务端口。 |

## COSRanger 常用端口

| 组件      | 端口号 | 说明                                          |
| --------- | ------ | --------------------------------------------- |
| COSRanger | 9999   | CosRangerServer 服务端监听端口，用于客户端连接。 |

## KRB5 常用端口

| 组件      | 端口号 | 说明                                                         |
| --------- | ------ | ------------------------------------------------------------ |
| KRB5      | 749    | Kadmin 服务端口。                                               |
| KRB5      | 754    | Kprop 服务端口。                                                |
| KRB5      | 88     | Kerberos 服务端端口。该端口用于：组件向 Kerberos 服务认证。配置集群互信可能会用到。 |

## KNOX 常用端口

| 组件         | 端口号 | 说明                                       |
| ------------ | ------ | ------------------------------------------ |
| KNOX      | 30002  | HTTP 端口，通常用于浏览器连接。                                 |
| KNOX      | 33389  | Knox 自带的 ldap 的端口号，用于 Knox 的认证。                       |

## ZooKeeper 常用端口

| 组件         | 端口号 | 说明                                       |
| ------------ | ------ | ------------------------------------------ |
| ZooKeeper | 2181   | ZooKeeper 客户端端口。  该端口用于：  ZooKeeper 客户端连接 ZooKeeper 服务器。 |

## OpenLDAP 常用端口

| 组件         | 端口号 | 说明                                       |
| ------------ | ------ | ------------------------------------------ |
| OpenLDAP  | 389    | 客户端访问端口。                                               |



## Tez 常用端口

| 组件         | 端口号 | 说明                                       |
| ------------ | ------ | ------------------------------------------ |
| Tez       | 2000   | Tez的WEB UI 端口。                                            |

## Livy 常用端口

| 组件         | 端口号 | 说明                                       |
| ------------ | ------ | ------------------------------------------ |
| Livy      | 8998   | LivyServer 服务端监听端口，用于客户端连接。                     |

## Kyuubi 常用端口

| 组件         | 端口号 | 说明                                       |
| ------------ | ------ | ------------------------------------------ |
| Kyuubi    | 10009  | KyuubiServer 服务端监听端口，用于客户端连接。                   |

## Alluxio 常用端口

| 组件         | 端口号 | 说明                                       |
| ------------ | ------ | ------------------------------------------ |
| Alluxio   | 20001  | AlluxioJobMaster RPC 端口，AlluxioMaster 通过该端口分派任务给 AlluxioJobMaster。 |
| Alluxio   | 30001  | AlluxioJobWorker RPC 端口，AlluxioJobMaster 通过改端口分派任务给 AlluxioJobWorker。 |
| Alluxio   | 19998  | AlluxioMaster RPC 端口，客户端通过该端口来链接 AlluxioMaster。  |
| Alluxio   | 29998  | AlluxioWorker RPC 端口，AlluxioMaster 通过该端口分派读写任务给 AlluxioWorker。 |


## GooseFS 常用端口

| 组件         | 端口号 | 说明                                       |
| ------------ | ------ | ------------------------------------------ |
| GooseFS   | 9206   | AlluxioJobMaster RPC 端口，AlluxioMaster 通过该端口分派任务给 AlluxioJobMaster。 |
| GooseFS   | 9210   | AlluxioJobWorker RPC 端口，AlluxioJobMaster 通过改端口分派任务给 AlluxioJobWorker。 |
| GooseFS   | 9201   | AlluxioMaster RPC 端口，客户端通过该端口来链接 AlluxioMaster。  |
| GooseFS   | 9211   | GooseFSProxy 服务端监听端口，用于代理客户端。                   |
| GooseFS   | 9204   | AlluxioWorker RPC 端口，AlluxioMaster 通过该端口分派读写任务给 AlluxioWorker。 |

## Ganglia 常用端口

| 组件         | 端口号 | 说明                                       |
| ------------ | ------ | ------------------------------------------ |
| Ganglia   | 1602   | Gmetad 服务端端口。                                             |
| Ganglia   | 1603   | Gmetad 服务端端口，用于接收 HTTPd 的数据查询。                    |
| Ganglia   | 1601   | gmond 进程间的通信端口，也供 gmetad 访问。                        |
