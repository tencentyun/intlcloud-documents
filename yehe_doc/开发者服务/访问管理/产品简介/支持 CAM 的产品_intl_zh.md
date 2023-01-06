## 简介 

访问管理已经支持对多数腾讯云产品服务进行权限管理。本文主要介绍支持访问管理 CAM 的产品服务的相关信息。具体维度包括授权粒度、控制台、根据标签进行授权、参考文档等。
以下列表分别罗列了腾讯云平台各大产品类别下已支持 CAM 的服务。
对表中信息进行如下定义：

- 服务：支持 CAM 的云服务的名称，单击链接至对应产品服务文档，方便您快速获取相关信息。  
- 授权粒度：当前服务提供的最小授权粒度。

> ? 其中授权粒度按照粒度粗细分为服务级、操作级和资源级三个级别。  
>
> - 服务级：定义对服务的整体是否拥有访问权限，分为允许对服务拥有全部操作权限或者拒绝对服务拥有全部操作权限。
> - 操作级：定义对服务的特定接口（API）是否拥有访问权限，例如：授权某账号对云服务器服务进行只读操作。  
> - 资源级：定义对特定资源是否有访问权限，这是最细的授权粒度，例如：授权某账号仅读写操作某台云服务器。

- 控制台：是否支持子账号通过控制台访问当前服务，“&#10003;”表示支持，“-”表示暂不支持。  
- 根据标签进行授权：当前服务是否支持通过标签进行权限管理，“&#10003;”表示支持，“-”表示暂不支持。   
- [服务角色](https://intl.cloud.tencent.com/document/product/598/19420)：当前服务是否支持作为角色载体进行跨服务授权访问其他服务，“&#10003;”表示支持，“-”表示暂不支持。  
- 参考文档：当前服务与 CAM 相关的文档链接，“-”表示暂无。

## 计算 

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [云服务器](https://intl.cloud.tencent.com/document/product/213) <sup>1</sup> | cvm |资源级   | &#10003; | &#10003;         | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/213/10311) |
| [弹性伸缩](https://intl.cloud.tencent.com/document/product/377)   | as |资源级   | &#10003; | &#10003;         | &#10003; | -                                                            |
| [批量计算](https://intl.cloud.tencent.com/document/product/599)   | batch | 资源级   | &#10003; | &#10003;         | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/599/33471) |
| [边缘计算机器](https://intl.cloud.tencent.com/document/product/1119) | ecm | 资源级   | &#10003; | &#10003;         | -        | -                                                            |
| [轻量应用服务器](https://intl.cloud.tencent.com/document/product/1103) | lighthouse | 资源级   | &#10003; | &#10003;         | -        | -                                                            |
| [自动化助手](https://intl.cloud.tencent.com/document/product/1147) | tat |资源级   | &#10003; | -                | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1147/46037) |

> ?<sup>1</sup> 云服务器中 [GPU 云服务器](https://intl.cloud.tencent.com/document/product/560)、[专用宿主机](https://intl.cloud.tencent.com/document/product/416)  、[云硬盘](https://intl.cloud.tencent.com/document/product/362) 均已支持使用 CAM。



## 容器

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [容器服务](https://intl.cloud.tencent.com/document/product/457)   | tke | 资源级   | &#10003; | &#10003;         | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/457/37361) |
| [容器镜像服务](https://intl.cloud.tencent.com/document/product/1051) | tcr | 资源级   | &#10003; | -                | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/1051/37246) |
| 服务网格                                                     | tcm |资源级   | &#10003; | -                | &#10003; | -                                                            |



## 存储 

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                              |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [对象存储](https://intl.cloud.tencent.com/document/product/436) <sup>1</sup>  | cos | 资源级   | &#10003; | &#10003;  | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/436/12473) |
| [文件存储](https://intl.cloud.tencent.com/document/product/582)   | cfs | 资源级   | &#10003; | &#10003;              | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/582/14679) |
| [云 HDFS](https://intl.cloud.tencent.com/document/product/1106)   | chdfs | 资源级   | &#10003; | &#10003;              | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1106/41966) |
| [日志服务](https://intl.cloud.tencent.com/document/product/614)   | cls | 资源级   | &#10003; | &#10003;                   | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/614/32853) |

> ?<sup>1</sup> 对象存储中 GetService 和 PutBucket 暂未支持标签授权，需要单独进行自定义策略授权。



## 网络 

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [负载均衡](https://intl.cloud.tencent.com/document/product/214)   | clb | 资源级   | &#10003; | &#10003;         | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/214/9776) |
| [私有网络](https://intl.cloud.tencent.com/document/product/215) <sup>1</sup> | vpc | 资源级   | &#10003; | &#10003;         | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/215/31859) |
| [专线接入](https://intl.cloud.tencent.com/document/product/216)   | dc | 资源级   | &#10003; | &#10003;         | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/216/39512) |

> ?<sup>1</sup> 私有网络中 [弹性网卡](https://intl.cloud.tencent.com/document/product/576)、[NAT 网关](https://intl.cloud.tencent.com/document/product/1015)、[对等连接](https://intl.cloud.tencent.com/document/product/553)、[VPN 连接](https://intl.cloud.tencent.com/document/product/1037)、[网络流日志](https://intl.cloud.tencent.com/document/product/682) 、[Anycast 公网加速](https://intl.cloud.tencent.com/document/product/644)、[云联网](https://intl.cloud.tencent.com/document/product/1003)、[共享带宽包](https://intl.cloud.tencent.com/document/product/684) 均已支持使用 CAM。

## CDN 与加速  

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [全球应用加速](https://intl.cloud.tencent.com/document/product/608) | gaap | 资源级   | &#10003; | &#10003;         | -        | -                                                            |
| [全站加速网络](https://intl.cloud.tencent.com/document/product/570) | ecdn | 资源级   | &#10003; | &#10003;         | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/570/35819) |
| [内容分发网络](https://intl.cloud.tencent.com/document/product/228) <sup>1</sup> | cdn | 资源级   | &#10003; | &#10003;         | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/228/35229) |

> ?<sup>1</sup> 内容分发网络中 [安全加速](https://intl.cloud.tencent.com/products/scdn) 已支持使用 CAM。

## 数据库  

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [云数据库 MySQL](https://intl.cloud.tencent.com/document/product/236) | cdb | 资源级   | &#10003; | &#10003;         | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/236/14465) |
| [云原生数据库 TDSQL-C](https://intl.cloud.tencent.com/document/product/1098) | cynosdb | 资源级   | &#10003; | &#10003;         | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1098/40639) |
| [云数据库 MariaDB](https://intl.cloud.tencent.com/document/product/237) | mariadb | 资源级   | &#10003; | &#10003;         | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/237/35439) |
| [云数据库 SQL Server](https://intl.cloud.tencent.com/document/product/238) | sqlserver | 资源级   | &#10003; | &#10003;         | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/238/34582) |
| [云数据库 PostgreSQL](https://intl.cloud.tencent.com/document/product/409) | postgres | 资源级   | &#10003; | &#10003;         | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/409/38834) |
| [TDSQL MySQL 版](https://intl.cloud.tencent.com/document/product/1042) | tdmysql | 资源级   | &#10003; | &#10003;         | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1042/33342) |
| [云数据库 Redis](https://intl.cloud.tencent.com/document/product/239) | redis | 资源级   | &#10003; | &#10003;               | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/239/32844) |
| [云数据库 MongoDB](https://intl.cloud.tencent.com/document/product/240) | mongodb | 资源级   | &#10003; | &#10003;         | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/240/32838) |
| [时序数据库 CTSDB](https://intl.cloud.tencent.com/document/product/1100) | ctsdb | 资源级   | &#10003; | &#10003;         | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1100/40913) |
| [游戏数据库 TcaplusDB](https://intl.cloud.tencent.com/document/product/1016) | tcaplusdb | 资源级   | &#10003; | &#10003;         | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1016/35749) |
| [数据库智能管家 DBbrain](https://intl.cloud.tencent.com/document/product/1035) | dbbrain | 资源级   | &#10003; | -                | -        | - |
| [数据传输服务](https://intl.cloud.tencent.com/document/product/236) | dts | 资源级   | &#10003; | &#10003;         | &#10003; | - |


## Serverless 

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [云函数](https://intl.cloud.tencent.com/document/product/583)     | scf | 资源级   | &#10003; | &#10003;         | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/583/9203) |
| [Serverless 应用中心](https://intl.cloud.tencent.com/document/product/1040) | sls | 资源级   | &#10003; | -                | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/1040/36859) |
| [事件总线](https://intl.cloud.tencent.com/document/product/1108)  | eb | 资源级   | &#10003; | -                | &#10003; | -                                                            |




## 中间件  

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [消息队列 CMQ - 队列模型](https://intl.cloud.tencent.com/zh/document/product/406) | cmqqueue | 资源级   | &#10003; | &#10003;         | -        | [访问管理指南](https://intl.cloud.tencent.com/zh/document/product/406/34253) |
| [消息队列 CMQ - 主题模型](https://intl.cloud.tencent.com/zh/document/product/406) | cmqtopic | 资源级   | &#10003; | &#10003;         | -        | [访问管理指南](https://intl.cloud.tencent.com/zh/document/product/406/34253) |
| [消息队列 CKafka](https://intl.cloud.tencent.com/document/product/597) | ckafka | 资源级   | &#10003; |-        | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/597/39084) |
| [API 网关](https://intl.cloud.tencent.com/document/product/628)   | apigw | 资源级   | &#10003; | &#10003;         | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/628/34064) |
| [消息队列 TDMQ](https://intl.cloud.tencent.com/document/product/1110) | tdmq | 资源级   | &#10003; | &#10003;            | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1110/42935) |


## 微服务 

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [弹性微服务](https://intl.cloud.tencent.com/document/product/1094) | tem | 操作级   | &#10003; | -                | &#10003; | -                                                            |




## 数据处理 

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [数据万象](https://intl.cloud.tencent.com/zh/document/product/1045) | ci | 资源级   | &#10003; | -                | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/zh/document/product/1045/33448) |

## 域名与网站  

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [SSL 证书](https://intl.cloud.tencent.com/document/product/1007)    | ssl |资源级   | &#10003; |  &#10003;                | &#10003; | - |
| [移动解析 HTTPDNS](https://intl.cloud.tencent.com/document/product/1130) | httpdns | 操作级   | &#10003; | -                | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1130/44478) |
| [私有域解析](https://intl.cloud.tencent.com/document/product/1097) | privatedns | 资源级   | &#10003; | -                | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1097/40575) |




## 终端安全

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [主机安全](https://intl.cloud.tencent.com/document/product/296) | cwp | 操作级   | &#10003; | -                | &#10003; | -        |



## 数据安全


| 产品                                                         | CAM 中简称 | 授权粒度 | 控制台 | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [数据安全中心](https://intl.cloud.tencent.com/document/product/1126) | dsgc       | 操作级   | ✓      | -                | ✓        | -                                                            |
| [密钥管理系统](https://intl.cloud.tencent.com/document/product/1030) | kms        | 资源级   | ✓      | ✓                | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1030/31977) |
| [凭据管理系统](https://intl.cloud.tencent.com/document/product/1078) | ssm        | 资源级   | ✓      | ✓                | ✓        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1078/38610) |


## 安全管理

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [安全运营中心](https://intl.cloud.tencent.com/zh/document/product/1008) | ssa | 操作级   | &#10003; | -                | &#10003; | -        |

## 应用安全

| 产品                                                         | CAM 中简称 | 授权粒度 | 控制台 | 根据标签进行授权 | 服务角色 | 参考文档 |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | -------- |
| [Web 应用防火墙](https://intl.cloud.tencent.com/document/product/627) | waf       | 操作级   | ✓      | ✓                | -        | -        |
| [漏洞扫描服务](https://intl.cloud.tencent.com/document/product/1142) | cws        | 操作级   | ✓      | -                | ✓        | -        |


## 视频服务

| 产品                                                         | CAM 中简称  | 授权粒度 | 控制台 | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------------------------------ | ----------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [实时音视频](https://intl.cloud.tencent.com/document/product/647) | trtc        | 资源级   | ✓      | ✓                | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/647/38319) |
| [云点播](https://intl.cloud.tencent.com/document/product/266)     | consolevod  | 资源级   | ✓      | ✓                | ✓        | [访问管理指南](https://intl.cloud.tencent.com/document/product/266/33970) |
| [视频处理](https://intl.cloud.tencent.com/document/product/1041)   | mps         | 服务级   | ✓      | -                | ✓        | -                                                            |



## 数据分析

| 产品                                                         | CAM 中简称 | 授权粒度 | 控制台 | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [弹性   MapReduce](https://intl.cloud.tencent.com/document/product/1026) | emr        | 资源级   | ✓      | ✓                | ✓        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1026/31100) |
| [Elasticsearch   Service](https://intl.cloud.tencent.com/document/product/845) | es         | 资源级   | ✓      | ✓                | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/845/19550) |
| [云数据仓库   ClickHouse](https://intl.cloud.tencent.com/document/product/1129) | cdwch      | 资源级   | ✓      | ✓                | -        | -                                                            |



## 文字识别

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [文字识别](https://intl.cloud.tencent.com/document/product/1005) | ocr | 服务级   | &#10003; | -                | -        | -        |



## 人脸识别

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [人脸识别](https://intl.cloud.tencent.com/document/product/1059)  | iai | 资源级   | &#10003; | -                | &#10003; | - |
| [人脸核身](https://intl.cloud.tencent.com/document/product/1061) | faceid | 服务级   | &#10003; | -                | &#10003; | -                                                            |


## 语音技术 

| 产品     | CAM 中简称 | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------- -------- | ------------- | -------- | -------- | ---------------- | -------- | ------------------------------------------------------------ |
| [语音识别](https://intl.cloud.tencent.com/document/product/1118) | asr | 资源级   | &#10003; | &#10003;         | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1118/43349) |


## 游戏服务

| 产品                                                         | CAM 中简称 | 授权粒度 | 控制台 | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [游戏多媒体引擎](https://intl.cloud.tencent.com/document/product/607) | gme        | 资源级   | ✓      | ✓                | -        | -                                                            |


## 移动服务 

| 产品                                                         | CAM 中简称 | 授权粒度 | 控制台 | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [移动推送 TPNS](https://intl.cloud.tencent.com/document/product/1024) | tpns       | 资源级   | ✓      | ✓                | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1024/35288) |


## 云通信  

| 产品                                                         | CAM 中简称 | 授权粒度 | 控制台 | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [即时通信   IM](https://intl.cloud.tencent.com/document/product/1047) | im         | 资源级   | ✓      | ✓                | -        | - |
| [短信](https://intl.cloud.tencent.com/document/product/382)       | consolesms | 资源级   | ✓      | ✓                | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/382/38453) |
| [邮件推送](https://intl.cloud.tencent.com/document/product/1084)  | ses        | 服务级   | ✓      | -                | -        | -                                                            |



## 物联网  

| 产品                                                         | CAM 中简称       | 授权粒度 | 控制台 | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------------------------------ | ---------------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [物联网通信](https://intl.cloud.tencent.com/document/product/1105) | iotcloud         | 资源级   | ✓      | ✓                | ✓        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1105/41473) |




## 云资源管理

| 产品                                                         | CAM 中简称 | 授权粒度 | 控制台 | 根据标签进行授权 | 服务角色 | 参考文档 |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | -------- |
| [标签](https://intl.cloud.tencent.com/document/product/651)       | tag        | 操作级   | ✓      | -                | -        | -        |
| [资源编排   TIC](https://intl.cloud.tencent.com/document/product/1043) | tic        | 服务级   | ✓      | -                | ✓        | -        |
| [云顾问](https://intl.cloud.tencent.com/document/product/1079)    | advisor    | 服务级   | ✓      | -                | ✓        | -        |


## 管理与审计

| 产品                                                         | CAM 中简称   | 授权粒度 | 控制台 | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------------------------------ | ------------ | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [访问管理](https://intl.cloud.tencent.com/document/product/598)   | cam          | 操作级   | ✓      | -                | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/598/10590) |
| [云审计](https://intl.cloud.tencent.com/document/product/1021)     | cloudaudit   | 操作级   | ✓      | -                | ✓        | -                                                            |

## 监控与运维  

| 产品                                                         | CAM 中简称 | 授权粒度 | 控制台 | 根据标签进行授权 | 服务角色 | 参考文档                                                     |
| ------------------------------------------------------------ | ---------- | -------- | ------ | ---------------- | -------- | ------------------------------------------------------------ |
| [云监控](https://intl.cloud.tencent.com/document/product/1116)     | monitor    | 资源级   | ✓      | ✓                | ✓        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1116/43206) |
| [迁移服务平台](https://intl.cloud.tencent.com/document/product/1036) | msp        | 服务级   | ✓      | -                | ✓        | -                                                            |
| [前端性能监控](https://intl.cloud.tencent.com/document/product/1131) | rum        | 资源级   | ✓      | ✓                | -        | [访问管理指南](https://intl.cloud.tencent.com/document/product/1131/44510) |


