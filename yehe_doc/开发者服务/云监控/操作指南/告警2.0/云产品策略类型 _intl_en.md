This document lists the policy type names and corresponding parameters of Tencent Cloud services.

| Policy Type Name    | Policy Type Parameter |
| ----------------- | -------------- |
| CVM - basic monitoring | cvm_device     |
| CVM - storage monitoring | BS             |
| TKE - pod                                                      |DOCKER_POD	|
| TencentDB - MySQL - server monitoring                                       |cdb_detail	|
| TencentDB - MariaDB                                                  |tdsql_cluster|
| TencentDB - Redis - CKV Edition                                          |redisUuid|
| TencentDB - SQL_Server                                               |sqlserver_instance|
| TencentDB - MongoDB                                                  |cmongo_instance|
| TencentDB - PostgreSQL                                               |POSTGRESQL|
| TencentDB - TcaplusDB                                                |tcaplusdb|
| TencentDB - TBase                                                    |tbase|
| CLB - public network listener                                          |CLB_LISTENER_PUBLIC|
| CLB - private network listener                                          |CLB_LISTENER_PRIVATE|
| CLB - CLB instance                                       |LB_VIP|
| CLB - layer-7 protocol monitoring                                       |LB-SEVEN-LAYER-MONITOR|
| CLB - Classiclink                              |VPC_CRCCN	|
| Total CVM bandwidth (project)                                         |CVM_TRAFFIC_PRJ	|
| Total CVM bandwidth (region)                                        |CVM_TRAFFIC_REGION|
| Direct Connect - dedicated tunnel                                             |dcchannel|
| Direct Connect - connection                                             |dcline|
| CDN - CDN project in the Chinese mainland                                                   |cdn_project|
| CDN - CDN domain name in the Chinese mainland                                                   |cdn_domain|
| VPC - NAT gateway                                                |nat_tc_stat	|
| VPC - VPN tunnel                                                |vpn_tunnel	|
| CPM - basic monitor                                    |phy_device	|
|  IM (API)                                                 |imopen||
|  IM (application)                                                 |imopen_app|
| BM (MySQL)                                            |BM_CDB|
| VPC - peering connection                                             |vpc_region_conn|
| GAAP - acceleration connection                                       |QAAP_TUNNEL|
| GAAP - acceleration connection listener                              |QAAP_TUNNEL_LISTENER|
| VPC - Direct Connect gateway                                             |DC_GW|
| TKE - node                                                   |	dcgw_server|
| VPC - VPN gateway                                                |VPN_GW|
| TKE - service                                                   |DOCKER_SERVICE|
| TKE - container                                                   |DOCKER_CONTAINER	|
| TKE - cluster                                                   |DOCKER_CLUSTER	|
| COS                                                          |COS|
| BM VPC - peering connection                                       |BMPC|
| Tencent Distributed SQL - TDSQL                                              |DCDB|
| CKafka - topic                                              |CKAFKA_TOPIC|
| CKafka - instance                                             |CKAFKA_INSTANCE|
| CDN - CDN domain name outside the Chinese mainland                                                   |OV_CDN_DOMAIN|
| CDN - CDN project outside the Chinese mainland                                                    |OV_CDN_PROJECT|
| TencentDB - MySQL - secondary monitoring                                       |CDB_SLAVE|
| EMR - cluster alarm                                                      |EMR|
| CSG - volume gateway                                                |CSG	|
| CPM - ENI monitoring                                    |BM_NETCARD|
| VPC - network detection                                             |NET_DETECT|
| VPC - BWP                                          |BANDWIDTHPACKAGE|
| BM VPC - NAT gateway                                          |BM_NATGW|
| Aegis - Anti-DDoS Advanced                                                    |HAIP|
| CKafka - ConsumerGroup - partition                            |CKAFKA_CONSUMERGROUP|
| BM VPC - IPsec VPN gateway                                    |BMIPSECGW|
| BM VPC - IPsec VPN tunnel                                    |BMIPSECCONN|
| GAAP - acceleration connection rule                                 |QAAP_TUNNEL_RULE|
| DTS - data subscription                                       |DTS_DATA_SUBSCRIPTION	|
| TSF - log alarm                                                      |TSF_LOG	|
| CMQ - queue - message request                                   |cmq-queue	|
| TencentDB - CTSDB                                                    |CTSDB|
| CAT task                                                          |cat_task|
| CMQ - topic - message request                                   |CMQ-TOPIC	|
| Snova cluster                                                           |pgdw_cluster|
| SCF                                                 |SCF|
| BM VPC - SSL VPN gateway                                      |BMSSLVPNGW|
| BM CLB - CLB instance                                 |BM_LB_Instance|
| BM CLB - public network listener                                    |BM_LB_ON_LISTENER	|
| VPC - CCN - cross-region                                      |VBC_BETWEEN_REGIONS|
| BM CLB - private network listener                                    |BM_LB_INNER_SERVER_PORT|
| CKafka - ConsumerGroup - topic                                |CKAFKA-CONSUMERGROUP-TOPIC	|
| BM CLB - public network server port                              |BM_LB_OUTER_SERVER_PORT|
| BM CLB - private network server port                              |BM_LB_INNER_SERVER_PORT	|
| TencentDB - Redis - Community Edition                                          |REDIS-CLUSTER	|
| VPC - EIP                                           |EIP	|
| VPC - Anycast EIP                                    |AnycastEIP|
| API Gateway - environment                                                      |APIGW_ENV|
| TSF - service alarm                                                      |TSF|
| API Gateway - API                                                         |APIGW_API
| ECDN - ECDN domain name                                                       |DSA_DOMAIN
| ECDN - ECDN project                                                       |dsa_project|
| Total CPM bandwidth (region)                                |BmTraffic|
| CMQ - queue - message retention                                   |CMQ-HEAP-UP	|
| CFS                                                          |cfs_monitor|
| BM VPC - network detection                                       |BM_NETDETECT|
| VPC - CCN - single-region                                      |VBC_SINGLE_REGION_BM|
| Snova - compute node monitoring                                  |snova_cluster_node|
| Snova - primary node monitoring                                     |SMNM|
| Snova - cluster monitoring                                        |SCM|
| CLB - server port (others) - listener dimension                  |LB_RS_PORT_STATUS|
| TencentDB - CynosDB - MySQL                                            |CYNOSDB_MYSQL|
| Oceanus                                                     |SCS|
| DTS - self-created migration                                       |MIGRATEJOB_INTERRUPTION|
| LVB - LVB domain name                                                |livestat|
| Peer node basic monitoring                                          |peer_altering|
| Anti-DDoS - Anti-DDoS Advanced                                                   |BGPIP|
| CLB - server port (others) - server port dimension            |CLB_PORT_PUBLIC_NEW	|
| TSF - deployment group alarm                                                   |TSF_GROUP|
| Sparkling                                        |SPARKLING|
| EMR - Spark - SparkJobHistoryServer                          |spark_sparkjobhistoryserver|
| EMR - Hive - HiveMetaStore                                   |hive_hivemetastore|
| EMR - Hive - HiveServer2                                     |hive_hiveserver2
| EMR - Hive - HiveWebHcat                                     |hive_hivewebhcat	
| EMR - Presto - Presto_Coordinator                            |presto_presto_coordinator|
| EMR - Presto - Presto_Worker                                 |presto_presto_worker|
| EMR - server monitoring - CPU                                     |node_cpu|
| EMR - HBase - HMaster                                        |hbase_hmaster|
| EMR - HBase - RegionServer                                   |hbase_regionserver	|
| EMR - server monitoring - file handle                            |node_filehandle|
| EMR - server monitoring - network                                  |node_network|
| EMR - server monitoring - memory                                  |node_memory|
| EMR - server monitoring - process                                  |node_process|
| EMR - HDFS - DataNode                                        |hdfs_datanode|
| EMR - HDFS - JournalNode                                     |hdfs_journalnode|
| EMR - HDFS - NameNode                                        |hdfs_namenode|
| EMR - HDFS - ZKFailoverController                            |hdfs_zkfailovercontroller|
| EMR - YARN - JobHistoryServer                                |yarn_jobhistoryserver|
| EMR - ZooKeeper - ZooKeeper                                  |zookeeper_zookeeper|
| EMR - YARN - NodeManager                                     |yarn_nodemanager|
| EMR - YARN - ResourceManager                                 |yarn_resourcemanager	|
| EMR - Presto - overview                                        |presto_overview|
| EMR - Presto - overview                                                     |emr_presto_overview|
| EMR - HDFS - overview                                          |hdfs_overview_aggregation	|
| EMR - YARN - overview                                          |yarn_overview_aggregation|
| EMR - HBase - overview                                         |hbase_overview_aggregation|
| VPC - EIP IPv6                                         |EIPv6|
| SCDN - user in the Chinese mainland                                                     |scdn_appid|
| SCDN - domain name in the Chinese mainland                                                      |scdn_domain	|
| SCDN - project in the Chinese mainland                                                      |scdn_projectid|
| MGOBE - pod monitoring                            |pod|
| TI-ONE - notebook                                        |tione_notebook|
| MGOBE - real-time server monitoring                   |server|
| CSG - file gateway                                             |csgfs|
| GSE - server fleet                                                   |fleet|
| CLS - server group                                                |cls_machine_group|
| TI-EMS                                           |tiems|
| CMQ - topic - message retention                                   |cmq_heap|
| GSE - game server queue                                             |queue|
| TI-ONE - SDK job                                       |tione_sdk_job|
| ES                                                   |	CES|
