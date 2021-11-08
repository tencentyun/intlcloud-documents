[Tencent Cloud Monitor](https://intl.cloud.tencent.com/zh/product/cm) (CM) provides load and performance monitoring metrics for various Tencent Cloud services such as CVM and TencentDB. You can use the CM console and APIs to get relevant monitoring data. Tencent Cloud Monitor App is an application plugin that adapts to the open-source software Grafana. It calls CM APIs (version 3.0) to get and display monitoring data on custom dashboards.

>?Typical [preset dashboard templates](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/tree/master/src/dashboards) are provided for CVM, TencentDB for MySQL, and CLB.

Supported Tencent Cloud services and corresponding documents are as listed in the following table. Data sources of monitoring metrics for more Tencent Cloud services will be supported in the future.

Service | Namespace | Metric Document | Instance List API Document 
------ | ------- | ------- | ------------- 
CVM | QCE/CVM |[CVM](https://intl.cloud.tencent.com/zh/document/api/248/6843) | [DescribeInstances](https://intl.cloud.tencent.com/document/product/213/33258)
TencentDB for MySQL | QCE/CDB | TencentDB for MySQL | [DescribeDBInstances](https://intl.cloud.tencent.com/document/api/236/15872) 
TencentDB for PostgreSQL | QCE/POSTGRES | [TencentDB for PostgreSQL](https://intl.cloud.tencent.com/document/product/248/17945)  | [DescribeDBInstances](https://intl.cloud.tencent.com/document/api/409/16773) 
TencentDB for MongoDB | QCE/CMONGO | [TencentDB for MongoDB](https://intl.cloud.tencent.com/document/product/248/35671)  | [DescribeDBInstances](https://intl.cloud.tencent.com/document/product/240/34702) 
TencentDB for Redis | QCE/REDIS_MEM | Memory Edition, 5-Second  | [DescribeInstances](https://intl.cloud.tencent.com/document/product/239/32065) 
TDSQL-C | QCE/CYNOSDB_MYSQL | [TDSQL-C](https://intl.cloud.tencent.com/document/product/248/37383)  | [DescribeInstances](https://intl.cloud.tencent.com/document/product/1098/40747)
TencentDB for TcaplusDB | QCE/TCAPLUS | [TencentDB for TcaplusDB](https://intl.cloud.tencent.com/document/product/248/34592)  | [DescribeInstances](https://intl.cloud.tencent.com/document/product/1098/40747) 
TencentDB for SQL Server | QCE/SQLSERVER | [TencentDB for SQL Server](https://intl.cloud.tencent.com/document/product/248/11008)  | [DescribeDBInstances](https://intl.cloud.tencent.com/document/product/238/32115) 
TDSQL for MySQL | QCE/TDMYSQL | Instance | [DescribeDCDBInstances](https://intl.cloud.tencent.com/document/product/1042/34442) 
CDN | QCE/CDN | Chinese Mainland Domain | DescribeDomains
CDN - province domain | QCE/CDN_LOG_DATA | Province  | DescribeDomains
BWP | QCE/BWP | [BWP](https://intl.cloud.tencent.com/document/product/248/34645) | [DescribeBandwidthPackages](https://intl.cloud.tencent.com/document/product/215/36919) 
CKafka | QCE/CKAFKA | [Instance](https://intl.cloud.tencent.com/document/product/248/17297)  | [DescribeInstances](https://intl.cloud.tencent.com/document/product/597/35357) 
CLB - public network CLB | QCE/LB_PUBLIC | Public Network CLB  | [DescribeLoadBalancers](https://intl.cloud.tencent.com/document/product/214/33830) 
CLB - private network CLB layer-4 protocol | QCE/LB_PRIVATE | Private Network CLB Layer-4 Protocol | [DescribeLoadBalancers](https://intl.cloud.tencent.com/document/product/214/33830) 
CLB - Layer-7 Protocol | QCE/LOADBALANCE | Layer-7 Protocol | [DescribeLoadBalancers](https://intl.cloud.tencent.com/document/product/214/33830) 
EIP | QCE/LB | [EIP](https://intl.cloud.tencent.com/document/product/248/34646) | [DescribeAddresses](https://intl.cloud.tencent.com/document/api/215/16702) 
CFS | QCE/CFS | [CFS](https://intl.cloud.tencent.com/document/product/248/34644) | [DescribeCfsFileSystems](https://intl.cloud.tencent.com/document/product/582/34514) 
SCF | QCE/SCF_V2 | SCF | [ListFunctions](https://intl.cloud.tencent.com/document/api/583/18582) 
Direct Connect - dedicated tunnel | QCE/DCX | [Dedicated Tunnel](https://intl.cloud.tencent.com/document/product/248/10995) | [DescribeDirectConnectTunnels](https://intl.cloud.tencent.com/document/api/216/19819) 
Direct Connect - connection | QCE/DC | [Connection](https://intl.cloud.tencent.com/document/product/248/10994) | [DescribeDirectConnects](https://intl.cloud.tencent.com/document/product/216/35330) 
VPC - VPN Gateway | QCE/VPNGW | [VPN Gateway](https://intl.cloud.tencent.com/document/product/248/10988) | [DescribeVpnGateways](https://intl.cloud.tencent.com/document/api/215/17514) 
VPC - Direct Connect Gateway | QCE/DCG | [Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/248/10990) | [DescribeDirectConnectGateways](https://intl.cloud.tencent.com/document/product/215/36913) 
VPC - NAT Gateway | QCE/NAT_GATEWAY | [NAT Gateway](https://intl.cloud.tencent.com/document/product/248/10991) | [DescribeNatGateways](https://intl.cloud.tencent.com/document/product/215/34752) 
VPC - Peering Connection | QCE/PCX | [Peering Connection](https://intl.cloud.tencent.com/document/product/248/10986) | [DescribeVpcPeeringConnections](https://intl.cloud.tencent.com/document/product/215/15754) 
VPC - VPN tunnel | QCE/VPNX | [VPN Tunnel](https://intl.cloud.tencent.com/document/product/248/10989) | [DescribeVpnConnections](https://intl.cloud.tencent.com/document/api/215/17515) 
VPC - Anycast EIP | QCE/CEIP_SUMMARY | Anycast EIP | [DescribeAddresses](https://intl.cloud.tencent.com/document/api/215/16702) 
VPC - network detection | QCE/VPC_NET_DETECT | Network Detection | [DescribeNetDetects](https://intl.cloud.tencent.com/document/product/215/34742) 
VPC - CCN | QCE/VBC | [CCN](https://intl.cloud.tencent.com/document/product/248/10987) | [DescribeCcns](https://intl.cloud.tencent.com/document/product/215/34787) 
API Gateway | QCE/APIGATEWAY | [API Gateway](https://intl.cloud.tencent.com/document/product/248/19130) | [DescribeServiceEnvironmentList](https://intl.cloud.tencent.com/document/product/628/36627) 
CBS | QCE/BLOCK_STORAGE | [CBS](https://intl.cloud.tencent.com/document/product/248/37085) | [DescribeDisks](https://intl.cloud.tencent.com/document/api/362/16315) 
ES | QCE/CES | [Elasticsearch](https://intl.cloud.tencent.com/document/product/248/34642) | [DescribeInstances](https://intl.cloud.tencent.com/document/product/845/32214) 
CMQ | QCE/CMQ | [Queue Service](https://intl.cloud.tencent.com/document/product/248/34643) | [DescribeQueueDetail](https://intl.cloud.tencent.com/document/product/406/35944) 
CMQ - topic model | QCE/CMQTOPIC | [Topic Subscription](https://intl.cloud.tencent.com/document/product/248/11013) | [DescribeTopicDetail](https://intl.cloud.tencent.com/document/product/406/35931) 
TDMQ | QCE/TDMQ | TDMQ | DescribeClusters 
CPM 1.0 | QCE/CPM | [CPM 1.0](https://intl.cloud.tencent.com/document/product/248/37080) | DescribeDevices 
CPM - BM peering connection | QCE/BM_PCX | [BM Peering Connection](https://intl.cloud.tencent.com/document/product/248/37082) | DescribeVpcPeerConnections
CPM - BM public network CLB | QCE/BM_LB | [BM Public Network CLB Instance](https://intl.cloud.tencent.com/document/product/248/37084) | DescribeLoadBalancers 
CPM - BM private network CLB | QCE/BM_INTRA_LB | [Private Network CLB Instance](https://intl.cloud.tencent.com/document/product/248/37083) | DescribeLoadBalancers
EMR (HDFS) | QCE/TXMR_HDFS | [EMR (HDFS)](https://intl.cloud.tencent.com/document/product/248/36845) | [DescribeInstances](https://intl.cloud.tencent.com/document/product/1026/31052) 
EMR (HBase) | QCE/TXMR_HBASE | [EMR (HBase)](https://intl.cloud.tencent.com/document/product/248/36846) | [DescribeInstances](https://intl.cloud.tencent.com/document/product/1026/31052) 
EMR (Hive) | QCE/TXMR_HIVE | [EMR (Hive)](https://intl.cloud.tencent.com/document/product/248/36847) | [DescribeInstances](https://intl.cloud.tencent.com/document/product/1026/31052) 
EMR (node) | QCE/TXMR_NODE | [EMR (Node)](https://intl.cloud.tencent.com/document/product/248/36848) | [DescribeInstances](https://intl.cloud.tencent.com/document/product/1026/31052) 
EMR (Presto) | QCE/TXMR_PRESTO | [EMR (Presto)](https://intl.cloud.tencent.com/document/product/248/36849) | [DescribeInstances](https://intl.cloud.tencent.com/document/product/1026/31052) 
EMR (Spark) | QCE/TXMR_SPARK | [EMR (Spark)](https://intl.cloud.tencent.com/document/product/248/36850) | [DescribeInstances](https://intl.cloud.tencent.com/document/product/1026/31052) 
EMR (YARN) | QCE/TXMR_YARN | [EMR (YARN)](https://intl.cloud.tencent.com/document/product/248/36851) | [DescribeInstances](https://intl.cloud.tencent.com/document/product/1026/31052) 
EMR (ZooKeeper) | QCE/TXMR_ZOOKEEPER | [EMR (ZooKeeper)](https://intl.cloud.tencent.com/document/product/248/36852) | [DescribeInstances](https://cloud.tencent.com/document/api/589/34266) 
ECM - computing and network | QCE/ECM | Computing and Network | DescribeInstances 
ECM- storage | QCE/ECM_BLOCK_STORAGE | Storage | DescribeInstances 
ECM - CLB layer-4 protocol | QCE/ECM_LB | CLB Layer-4 Protocol | DescribeLoadBalancers
COS | QCE/COS | [COS](https://intl.cloud.tencent.com/document/product/248/37269) | [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/api/436/8291) 
GAAP | QCE/QAAP | [GAAP Channel Load](https://intl.cloud.tencent.com/document/product/248/13527) | [DescribeProxies](https://intl.cloud.tencent.com/document/product/608/33101) 
GSE | QCE/GSE | Instance | [API Category](https://intl.cloud.tencent.com/document/product/1055/37120) 