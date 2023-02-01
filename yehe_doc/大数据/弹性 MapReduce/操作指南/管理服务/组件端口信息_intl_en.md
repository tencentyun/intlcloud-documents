This document describes common component ports.

## Common HDFS ports

| Component | Port Number | Description                                                         |
| ---- | ------ | ------------------------------------------------------------ |
| HDFS | 4007   | NameNode RPC port, which is used for:<br>1. The communication between the HDFS client and NameNode.<br>2. The connection between the DataNode and NameNode. |
| HDFS | 4008   | HDFS HTTP port (NameNode), which is used for:<br>1. Point-to-point NameNode checkpoint operations.<br>2. Connecting the remote web client to the NameNode UI. |
| HDFS | 4009   | HDFS HTTPS port (NameNode), which is used for:<br>1. Point-to-point NameNode checkpoint operations.<br>2. Connecting the remote web client to the NameNode UI. |
| HDFS | 4004   | DataNode IPC server port, which is used for connecting the client to the DataNode to perform RPC operations. |
| HDFS | 4001   | DataNode data transfer port, which is used for:<br>1. The data transfer from or to the DataNode to or from the HDFS client.<br>2. Point-to-point DataNode data transfer. |
| HDFS | 4002   | DataNode HTTP port, which is used for connecting the remote web client to the DataNode UI in safe mode. |
| HDFS | 4003   | DataNode HTTPS port, which is used for connecting the remote web client to the DataNode UI in safe mode. |
| HDFS | 4005   | JournalNode RPC port, which is used for client communication to access multiple types of information. |
| HDFS | 4006   | JournalNode HTTP port, which is used for connecting the remote web client to the JournalNode in safe mode. |
| HDFS | 4032   | The listener port of the HttpFS HTTP server, which is used for connecting the remote RESTful API to HttpFS. |

## Common YARN ports

| Component | Port Number | Description                                                         |
| ---- | ------ | ------------------------------------------------------------ |
| YARN | 5024   | The web HTTP port of the JobHistory server, which is used for viewing the webpage of the JobHistory server. |
| YARN | 5022   | JobHistory server port, which is used for: <br>1. Recovering task data on the MapReduce client.<br>2. Getting the task report on the JobHistory client. |
| YARN | 5003   | The web HTTP port of the ResourceManager service.                         |
| YARN | 5002   | The web HTTPS port of the ResourceManager service, which is used for connecting to the ResourceManager web application in safe mode. |
| YARN | 5004   | The web HTTP port of the NodeManager.                                     |
| YARN | 5005   | The web HTTPS port of the NodeManager, which is used for connecting to the NodeManager web application in safe mode. |
| YARN | 5001   | ResourceManager scheduler port.                                   |
| YARN | 5000   | ResourceManager RPC port, which is used for submitting tasks on the client.                  |

## Common Hive ports

| Component | Port Number | Description                                                         |
| ---- | ------ | ------------------------------------------------------------ |
| Hive | 7010   | The port for WebHCat to provide RESTful services, which is used for the communication between the WebHCat client and WebHCat server. |
| Hive | 7001   | The port for HiveServer to provide Thrift services, which is used for the communication between the HiveServer client (Beeline) and HiveServer. |
| Hive | 7004   | The port for MetaStore to provide Thrift services, which is used for the communication between the MetaStore client and MetaStore, i.e., the communication between HiveServer and MetaStore. |
| Hive | 7003   | The web UI port of Hive, which is used for the HTTPS/HTTP communication between web requests and the Hive UI server. |


## Common Spark ports

| Component  | Port Number | Description     |
| ----- | ------ | -------- |
| Spark | 10000  | HTTP port. |

## Common Presto ports

| Component   | Port Number | Description                                       |
| ------ | ------ | ------------------------------------------ |
| Presto | 9000   | The HTTP port for the Presto coordinator or worker to provide external services. |

## Common PrestoSQL ports

| Component   | Port Number | Description                                       |
| --------- | ------ | --------------------------------------------- |
| PrestoSQL | 9000   | The HTTP port for the PrestoSQL coordinator or worker to provide external services. |

## Common Trino ports

| Component   | Port Number | Description                                       |
| ----- | ------ | ----------------------------------------- |
| Trino | 9000   | The HTTP port for the Trino coordinator or worker to provide external services. |

## Common Impala ports

| Component   | Port Number | Description                                       |
| ------ | ------------ | ------------------------------------------------------------ |
| Impala | 27000 and 27009 | The ports for Impala application communication. The former is for Impala 2.x, and the latter is for Impala 3.x. |
| Impala | 27001        | The port for impala-shell communication.                               |
| Impala | 27004        | The web port of the Impala server.                                        |
| Impala | 27007        | The web port of the Impala Catalog.                                       |
| Impala | 27005        | The web port of the Impala StateStore.                                    |

## Common Kudu ports

| Component   | Port Number | Description                                       |
| ---- | ------ | -------------------- |
| Kudu | 7051   | The PRC port of the Kudu master. |
| Kudu | 7050   | The RPC port of the Kudu server.   |
| Kudu | 8051   | The HTTP port of the Kudu master. |
| Kudu | 8050   | The HTTP port of the Kudu server. |

## Common ClickHouse ports

| Component   | Port Number | Description                                       |
| ---------- | ------ | ------------------------- |
| ClickHouse | 9000   | The TCP port for accessing the business client.   |
| ClickHouse | 8123   | The HTTP port for accessing the business client.  |
| ClickHouse | 9009   | The HTTPS port for accessing the business client. |

## Common Kylin ports

| Component   | Port Number | Description                                       |
| ----- | ------ | -------------- |
| Kylin | 16500  | Kylin HTTP port. |

## Common Doris ports

| Component   | Port Number | Description                                       |
| ----- | ------ | --------------------------------------------------- |
| Doris | 8000   | The Thrift server port on the broker.                      |
| Doris | 9060   | The Thrift server port on the backend, which is used for receiving frontend requests.  |
| Doris | 8060   | The BRPC port on the backend, which is used for the communication between backend instances.                 |
| Doris | 9050   | The heartbeat service port (Thrift) on the backend, which is used for receiving frontend heartbeats. |
| Doris | 8040   | The Thrift server port on the broker, which is used for receiving requests.             |
| Doris | 9010   | The port on the frontend for the communication between metadata management modules (BDBJE).    |
| Doris | 8030   | The HTTP server port on the frontend.                            |
| Doris | 9020   | The Thrift server port on the frontend.                          |
| Doris | 9030   | The port on the frontend for receiving MySQL client access requests.                      |

## Common StarRocks ports

| Component   | Port Number | Description                                       |
| --------- | ------ | --------------------------------------------------- |
| StarRocks | 8000   | The Thrift server port on the broker.                       |
| StarRocks | 9060   | The Thrift server port on the backend, which is used for receiving frontend requests.  |
| StarRocks | 8060   | The BRPC port on the backend for the communication between backend instances.                 |
| StarRocks | 9050   | The heartbeat service port (Thrift) on the backend, which is used for receiving frontend heartbeats. |
| StarRocks | 8040   | The Thrift server port on the broker, which is used for receiving requests.             |
| StarRocks | 9010   | The port on the frontend for the communication between metadata management modules (BDBJE).    |
| StarRocks | 8030   | The HTTP server port on the frontend.                            |
| StarRocks | 9020   | The Thrift server port on the frontend.                          |
| StarRocks | 9030   | The port on the frontend for receiving MySQL client access requests.                      |

## Common Druid ports

| Component   | Port Number | Description                                       |
| ----- | ------ | ------------------------------------------------------------ |
| Druid | 8082   | The listener port of the broker server (`broker-runtime.properties`), which is used for receiving client queries. |
| Druid | 8081   | The listener port of the coordinator server (`coordinator -runtime.properties`) for the communication with other components. |
| Druid | 8083   | The listener port of the historical server (`historical-runtime.properties`) for the communication with other components. |
| Druid | 8091   | The listener port of the middleManager server (`middleManager-runtime.properties`) for the communication with other components. |
| Druid | 8090   | The listener port of the Overlord server (`overlord-runtime.properties`) for the communication with other components. |
| Druid | 18888  | The listener port of the router server (`router-runtime.properties`), which is used for routing client queries to the broker. |

## Common HBase ports

| Component   | Port Number | Description                                       |
| ----- | ------ | ------------------------------------------------------------ |
| HBase | 6000   | HMaster RPC port, which is used for connecting the HBase client to HMaster.        |
| HBase | 6001   | HMaster HTTPS port, which is used for connecting the remote web client to the HMaster UI. |
| HBase | 6002   | The RPC port of the RegionServer (RS), which is used for connecting the HBase client to the RegionServer. |
| HBase | 6003   | RegionServer HTTPS port, which is used for connecting the remote web client to the RegionServer UI. |
| HBase | 6005   | The Info Server listener port of the HBase Thrift server. |
| HBase | 6004   | The HBase Thrift server listener port. |

## Common Flink ports

| Component   | Port Number | Description                                       |
| ----- | ------ | ------------------------------------------------------------ |
| Flink | 16001  | Flink web UI port, which is used for the HTTP/HTTPS communication between client web requests and the Flink server. |

## Common Storm ports

| Component   | Port Number | Description                                       |
| ----- | ------ | ------------------ |
| Storm | 15002  | Logviewer service port. |
| Storm | 15000  | Nimbus service port.     |
| Storm | 15001  | Storm web UI port.     |

## Common Hue ports

| Component | Port Number | Description                                                         |
| ---- | ------ | ------------------------------------------------------------ |
| Hue  | 13000  | The port for Hue to provide HTTPS web services, which can be modified. |

## Common Oozie ports

| Component   | Port Number | Description                                       |
| ----- | ------ | ------------------------ |
| Oozie | 12000  | HTTP port, which is used for client access. |

## Common Superset ports

| Component   | Port Number | Description                                       |
| -------- | ------ | -------------------------------- |
| Superset | 18088  | Superset service port, which is used for client connection. |

## Common Zeppelin ports

| Component   | Port Number | Description                                       |
| -------- | ------ | -------------------------------- |
| Zeppelin | 18000  | Zeppelin service port, which is used for client connection. |

## Common Kafka ports

| Component   | Port Number | Description                                       |
| ----- | ------ | ------------------------------ |
| Kafka | 9092   | The port for the broker to provide data reception and acquisition services. |

## Common Kafka Manager ports

| Component   | Port Number | Description                                       |
| ------------ | ------ | ------------------------------------------ |
| Kafka Manager | 9000   | The listener port of the Kafka Manager server, which is used for client connection. |

## Common Ranger ports

| Component   | Port Number | Description                                       |
| ------ | ------ | --------------------------- |
| Ranger | 6080   | Ranger admin web UI port.         |
| Ranger | 5151   | The port of Ranger UserSync for authentication services. |

## Common COSRanger ports

| Component   | Port Number | Description                                       |
| --------- | ------ | --------------------------------------------- |
| COSRanger | 9999   | The listener port of the COSRangerServer server, which is used for client connection. |

## Common KRB5 ports

| Component   | Port Number | Description                                       |
| --------- | ------ | ------------------------------------------------------------ |
| KRB5      | 749    | Kadmin service port.                                               |
| KRB5      | 754    | Kprop service port.                                                |
| KRB5      | 88     | Kerberos server port for component authentication in the Kerberos service, which may be used in configuring mutual trust of clusters. |

## Common Knox ports

| Component   | Port Number | Description                                       |
| ------------ | ------ | ------------------------------------------ |
| Knox      | 30002  | HTTP port, which is usually used for browser connection.                                 |
| Knox      | 33389  | The LDAP port of Knox, which is used for Knox authentication.                       |

## Common ZooKeeper ports

| Component   | Port Number | Description                                       |
| ------------ | ------ | ------------------------------------------ |
| ZooKeeper | 2181   | ZooKeeper client port, which is used for connecting the ZooKeeper client to the ZooKeeper server. |

## Common OpenLDAP ports

| Component   | Port Number | Description                                       |
| ------------ | ------ | ------------------------------------------ |
| OpenLDAP  | 389    | The port for client access. |



## Common Tez ports

| Component   | Port Number | Description                                       |
| ------------ | ------ | ------------------------------------------ |
| Tez       | 2000   | The web UI port of Tez.                                            |

## Common Livy ports

| Component   | Port Number | Description                                       |
| ------------ | ------ | ------------------------------------------ |
| Livy      | 8998   | The listener port of the Livy server, which is used for client connection.                     |

## Common Kyuubi ports

| Component   | Port Number | Description                                       |
| ------------ | ------ | ------------------------------------------ |
| Kyuubi    | 10009  | The listener port of the Kyuubi server, which is used for client connection.                   |

## Common Alluxio ports

| Component   | Port Number | Description                                       |
| ------------ | ------ | ------------------------------------------ |
| Alluxio   | 20001  | The RPC port of the Alluxio Job Master, which is used by the Alluxio Master to assign tasks to the Alluxio Job Master. |
| Alluxio   | 30001  | The RPC port of the Alluxio Job Worker, which is used by the Alluxio Job Master to assign tasks to the Alluxio Job Worker. |
| Alluxio   | 19998  | The RPC port of the Alluxio Master, which is used for connecting the client to the Alluxio Master.  |
| Alluxio   | 29998  | The RPC port of the Alluxio Worker, which is used by the Alluxio Master to assign read-write tasks to the Alluxio Worker. |


## Common GooseFS ports

| Component   | Port Number | Description                                       |
| ------------ | ------ | ------------------------------------------ |
| GooseFS   | 9206   | The RPC port of the Alluxio Job Master, which is used by the Alluxio Master to assign tasks to the Alluxio Job Master. |
| GooseFS   | 9210   | The RPC port of the Alluxio Job Worker, which is used by the Alluxio Job Master to assign tasks to the Alluxio Job Worker. |
| GooseFS   | 9201   | The RPC port of the Alluxio Master, which is used for connecting the client to the Alluxio Master.  |
| GooseFS   | 9211   | The listener port of the GooseFSProxy server, which is used for client proxy.                   |
| GooseFS   | 9204   | The RPC port of the Alluxio Worker, which is used by the Alluxio Master to assign read-write tasks to the Alluxio Worker. |

## Common Ganglia ports

| Component   | Port Number | Description                                       |
| ------------ | ------ | ------------------------------------------ |
| Ganglia   | 1602   | Gmetad server port.                                             |
| Ganglia   | 1603   | Gmetad server port, which is used for receiving HTTPd data queries.                    |
| Ganglia   | 1601   | The port for gmond process communication and gmetad access.                        |
