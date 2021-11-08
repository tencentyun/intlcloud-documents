[腾讯云监控](https://intl.cloud.tencent.com/zh/product/cm) 为用户提供云服务器、云数据库等多个云产品的负载和性能监控指标，用户可以使用云监控控制台、云监控 API 等方式获取相关监控数据。腾讯云监控应用插件 Tencent Cloud Monitor App，是一款适配开源软件 Grafana 的应用插件，通过调用 腾讯云监控 API 3.0 的方式获取监控数据，并对数据进行自定义 Dashboard 展示。

>?该插件提供了云服务器、云数据库 MySQL、负载均衡 等具有代表性的 [Dashboard 预设模板](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/tree/master/src/dashboards)。

支持的云产品监控及文档如下表所示，更多云产品的监控指标数据源在陆续完善中。

产品名称 | 命名空间 | 指标文档 | 实例列表接口文档 
------ | ------- | ------- | ------------- 
CVM 云服务器 | QCE/CVM |[云服务器监控指标](https://intl.cloud.tencent.com/zh/document/api/248/6843) | [查询示例列表](https://intl.cloud.tencent.com/document/product/213/33258)
CDB 云数据库 MySQL | QCE/CDB | 云数据库 MySQL 监控指标 | [查询实例列表](https://intl.cloud.tencent.com/document/api/236/15872) 
云数据库 PostgreSql | QCE/POSTGRES | [云数据库 PostgreSQL 监控指标](https://intl.cloud.tencent.com/document/product/248/17945)  | [查询实例列表](https://intl.cloud.tencent.com/document/api/409/16773) 
云数据库 MongoDB | QCE/CMONGO | [云数据库 MongoDB 监控指标](https://intl.cloud.tencent.com/document/product/248/35671)  | [查询云数据库实例列表](https://intl.cloud.tencent.com/document/product/240/34702) 
云数据库 Redis | QCE/REDIS_MEM | 内存版监控指标（5秒）  | [查询 Redis 实例列表](https://intl.cloud.tencent.com/document/product/239/32065) 
云数据库 TDSQL-C (原CynosDB) | QCE/CYNOSDB_MYSQL | [云数据库 CYNOSDB_MYSQL 监控指标](https://intl.cloud.tencent.com/document/product/248/37383)  | [查询实例列表](https://intl.cloud.tencent.com/document/product/1098/40747)
云数据库 TcaplusDB | QCE/TCAPLUS | [云数据库 TcaplusDB 监控指标](https://intl.cloud.tencent.com/document/product/248/34592)  | [查询实例列表](https://intl.cloud.tencent.com/document/product/1098/40747) 
云数据库 SQL Server | QCE/SQLSERVER | [云数据库 SQL Server 监控指标](https://intl.cloud.tencent.com/document/product/248/11008)  | [查询实例列表](https://intl.cloud.tencent.com/document/product/238/32115) 
分布式数据库 TDSQL MySQL(TDMYSQL) | QCE/TDMYSQL | 实例 | [查询实例列表](https://intl.cloud.tencent.com/document/product/1042/34442) 
CDN 内容分发式网络 | QCE/CDN | 国内域名  | 查询域名基本信息
CDN 省份域名 | QCE/CDN_LOG_DATA | 省份  | 查询域名基本信息
BWP 带宽包 | QCE/BWP | [带宽包监控指标](https://intl.cloud.tencent.com/document/product/248/34645) | [查询带宽包资源](https://intl.cloud.tencent.com/document/product/215/36919) 
CKafka 消息队列 | QCE/CKAFKA | [实例监控指标](https://intl.cloud.tencent.com/document/product/248/17297)  | [获取实例列表](https://intl.cloud.tencent.com/document/product/597/35357) 
CLB 公网负载均衡 | QCE/LB_PUBLIC | 公网负载均衡监控指标  | [查询负载均衡实例列表](https://intl.cloud.tencent.com/document/product/214/33830) 
CLB 内网负载均衡四层协议 | QCE/LB_PRIVATE | 内网负载均衡四层协议监控指标| [查询负载均衡实例列表](https://intl.cloud.tencent.com/document/product/214/33830) 
CLB 负载均衡七层协议 | QCE/LOADBALANCE | 七层协议监控指标 | [查询负载均衡实例列表](https://intl.cloud.tencent.com/document/product/214/33830) 
LB 弹性公网IP | QCE/LB | [弹性公网 IP 监控指标](https://intl.cloud.tencent.com/document/product/248/34646) | [查询弹性公网 IP 列表](https://intl.cloud.tencent.com/document/api/215/16702) 
CFS 文件存储 | QCE/CFS | [文件存储监控指标](https://intl.cloud.tencent.com/document/product/248/34644) | [查询文件系统](https://intl.cloud.tencent.com/document/product/582/34514) 
SCF 云函数 | QCE/SCF_V2 | 云函数监控指标 | [获取函数列表](https://intl.cloud.tencent.com/document/api/583/18582) 
专线接入 专用通道 | QCE/DCX | [专用通道监控指标](https://intl.cloud.tencent.com/document/product/248/10995) | [查询专用通道列表](https://intl.cloud.tencent.com/document/api/216/19819) 
专线接入 物理专线 | QCE/DC | [物理专线监控指标](https://intl.cloud.tencent.com/document/product/248/10994) | [查询物理专线列表](https://intl.cloud.tencent.com/document/product/216/35330) 
私有网络 VPN 网关 | QCE/VPNGW | [VPN 网关监控指标](https://intl.cloud.tencent.com/document/product/248/10988) | [查询 VPN 网关](https://intl.cloud.tencent.com/document/api/215/17514) 
私有网络 专线网关 | QCE/DCG | [专线网关监控指标](https://intl.cloud.tencent.com/document/product/248/10990) | [查询专线网关](https://intl.cloud.tencent.com/document/product/215/36913) 
私有网络 NAT 网关 | QCE/NAT_GATEWAY | [NAT 网关监控指标](https://intl.cloud.tencent.com/document/product/248/10991) | [查询 NAT 网关](https://intl.cloud.tencent.com/document/product/215/34752) 
私有网络 对等连接 | QCE/PCX | [对等连接监控指标](https://intl.cloud.tencent.com/document/product/248/10986) | [查询对等连接](https://intl.cloud.tencent.com/document/product/215/15754) 
私有网络 VPN 通道 | QCE/VPNX | [VPN 通道监控指标](https://intl.cloud.tencent.com/document/product/248/10989) | [查询VPN通道列表](https://intl.cloud.tencent.com/document/api/215/17515) 
私有网络 Anycast弹性公网IP | QCE/CEIP_SUMMARY | Anycast 弹性公网 IP 监控指标 | [查询弹性公网IP列表](https://intl.cloud.tencent.com/document/api/215/16702) 
私有网络 网络探测 | QCE/VPC_NET_DETECT | 网络探测监控指标 | [查询网络探测列表](https://intl.cloud.tencent.com/document/product/215/34742) 
私有网络 云联网 | QCE/VBC | [云联网监控指标](https://intl.cloud.tencent.com/document/product/248/10987) | [查询CCN列表](https://intl.cloud.tencent.com/document/product/215/34787) 
API 网关 | QCE/APIGATEWAY | [API 网关监控指标](https://intl.cloud.tencent.com/document/product/248/19130) | [查询服务环境列表](https://intl.cloud.tencent.com/document/product/628/36627) 
CBS 云硬盘 | QCE/BLOCK_STORAGE | [云硬盘监控指标](https://intl.cloud.tencent.com/document/product/248/37085) | [查询云硬盘列表](https://intl.cloud.tencent.com/document/api/362/16315) 
Elasticsearch | QCE/CES | [Elasticsearch 监控指标](https://intl.cloud.tencent.com/document/product/248/34642) | [查询 ES 集群实例](https://intl.cloud.tencent.com/document/product/845/32214) 
CMQ 消息队列服务 | QCE/CMQ | [队列服务监控指标](https://intl.cloud.tencent.com/document/product/248/34643) | [枚举队列](https://intl.cloud.tencent.com/document/product/406/35944) 
CMQ 消息队列主题订阅 | QCE/CMQTOPIC | [主题订阅监控指标](https://intl.cloud.tencent.com/document/product/248/11013) | [查询主题详情](https://intl.cloud.tencent.com/document/product/406/35931) 
消息队列 TDMQ | QCE/TDMQ | 消息队列 TDMQ 监控指标 | 获取集群列表 
黑石物理服务器1.0 | QCE/CPM | [黑石物理服务器1.0监控指标](https://intl.cloud.tencent.com/document/product/248/37080) | 查询物理机信息 
黑石物理服务器 黑石对等连接 | QCE/BM_PCX | [黑石对等连接监控指标](https://intl.cloud.tencent.com/document/product/248/37082) | 获取对等连接列表
黑石物理服务器 黑石外网负载均衡 | QCE/BM_LB | [黑石外网负载均衡监控指标](https://intl.cloud.tencent.com/document/product/248/37084) | 获取黑石负载均衡实例列表 
黑石物理服务器 黑石内网负载均衡 | QCE/BM_INTRA_LB | [黑石内网负载均衡监控指标](https://intl.cloud.tencent.com/document/product/248/37083) | 获取黑石负载均衡实例列表
弹性 MapReduce（HDFS） | QCE/TXMR_HDFS | [弹性 MapReduce（HDFS）](https://intl.cloud.tencent.com/document/product/248/36845) | [查询EMR实例](https://intl.cloud.tencent.com/document/product/1026/31052) 
弹性 MapReduce（HBASE） | QCE/TXMR_HBASE | [弹性 MapReduce（HBASE）](https://intl.cloud.tencent.com/document/product/248/36846) | [查询EMR实例](https://intl.cloud.tencent.com/document/product/1026/31052) 
弹性 MapReduce（HIVE） | QCE/TXMR_HIVE | [弹性 MapReduce（HIVE）](https://intl.cloud.tencent.com/document/product/248/36847) | [查询EMR实例](https://intl.cloud.tencent.com/document/product/1026/31052) 
弹性 MapReduce（NODE） | QCE/TXMR_NODE | [弹性 MapReduce（NODE）](https://intl.cloud.tencent.com/document/product/248/36848) | [查询EMR实例](https://intl.cloud.tencent.com/document/product/1026/31052) 
弹性 MapReduce（PRESTO） | QCE/TXMR_PRESTO | [弹性 MapReduce（PRESTO）](https://intl.cloud.tencent.com/document/product/248/36849) | [查询EMR实例](https://intl.cloud.tencent.com/document/product/1026/31052) 
弹性 MapReduce（SPARK） | QCE/TXMR_SPARK | [弹性 MapReduce（SPARK）](https://intl.cloud.tencent.com/document/product/248/36850) | [查询EMR实例](https://intl.cloud.tencent.com/document/product/1026/31052) 
弹性 MapReduce（YARN） | QCE/TXMR_YARN | [弹性 MapReduce（YARN）](https://intl.cloud.tencent.com/document/product/248/36851) | [查询EMR实例](https://intl.cloud.tencent.com/document/product/1026/31052) 
弹性 MapReduce（ZOOKEEPER） | QCE/TXMR_ZOOKEEPER | [弹性 MapReduce（ZOOKEEPER）](https://intl.cloud.tencent.com/document/product/248/36852) | [查询EMR实例](https://cloud.tencent.com/document/api/589/34266) 
边缘计算机器 计算和网络 | QCE/ECM | 计算和网络监控指标 | 获取实例相关信息 
边缘计算机器 存储 | QCE/ECM_BLOCK_STORAGE | 存储监控指标 | 获取实例相关信息 
边缘计算机器 负载均衡四层协议 | QCE/ECM_LB | 负载均衡四层协议监控指标 | 查询负载均衡实例列表
对象存储 | QCE/COS | [对象存储监控指标](https://intl.cloud.tencent.com/document/product/248/37269) | [GET Service（List Buckets）](https://intl.cloud.tencent.com/document/api/436/8291) 
全球应用加速 | QCE/QAAP | [全球应用加速通道负载监控指标](https://intl.cloud.tencent.com/document/product/248/13527) | [查询通道实例列表](https://intl.cloud.tencent.com/document/product/608/33101) 
游戏服务器伸缩 | QCE/GSE | 实例 | [API 概览](https://intl.cloud.tencent.com/document/product/1055/37120) 