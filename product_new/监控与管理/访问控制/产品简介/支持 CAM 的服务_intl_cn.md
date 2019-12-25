## 简介	

访问管理已经支持对多数腾讯云产品服务进行权限管理。本文主要介绍支持访问管理 CAM 的产品服务的相关信息。具体维度包括授权粒度、控制台、根据标签进行授权、参考文档等。
以下列表分别罗列了腾讯云平台各大产品类别下已支持 CAM 的服务。
对表中信息进行如下定义：

- 服务：支持 CAM 的云服务的名称，单击链接至对应产品服务文档，方便您快速获取相关信息。	
- 授权粒度：当前服务提供的最小授权粒度。

> 其中授权粒度按照粒度粗细分为服务级、操作级和资源级三个级别。	
>
> - 服务级：定义对服务的整体是否拥有访问权限，分为允许对服务拥有全部操作权限或者拒绝对服务拥有全部操作权限。
> - 操作级：定义对服务的特定接口（API）是否拥有访问权限，例如：授权某账号对云服务器服务进行只读操作。	
> - 资源级：定义对特定资源是否有访问权限，这是最细的授权粒度，例如：授权某账号仅读写操作某台云服务器。

- 控制台：是否支持子账号通过控制台访问当前服务，“&#10003;”表示支持，“-”表示暂不支持。	
- 根据标签进行授权：当前服务是否支持通过标签进行权限管理，“&#10003;”表示支持，“-”表示暂不支持。		
- [服务角色](https://intl.cloud.tencent.com/document/product/598/19420)：当前服务是否支持作为角色载体进行跨服务授权访问其他服务，“&#10003;”表示支持，“-”表示暂不支持。	
- 参考文档：当前服务与 CAM 相关的文档链接，“-”表示暂无。

## 计算	

 | 服务                                                         | 授权粒度 | 控制台 | 根据标签进行授权 |  服务角色 |	参考文档 |	
| ------------------------------------------------------------| ------ | -------- | ------- |  ---- |	---- |	
| [云服务器](https://intl.cloud.tencent.com/document/product/213) <sup>1</sup> | 资源级  | &#10003;      |&#10003;    |  &#10003;  |	 [访问管理指南](https://intl.cloud.tencent.com/document/product/213/10311)   |		
| [容器服务](https://intl.cloud.tencent.com/document/product/457) | 资源级  | &#10003;       | - | &#10003;    |	[访问管理指南](https://intl.cloud.tencent.com/document/product/457/11526)  |	
| [弹性伸缩](https://intl.cloud.tencent.com/document/product/377) | 资源级   | &#10003;      | -  | &#10003;    |	-    |	
| [云函数](https://intl.cloud.tencent.com/document/product/583)  | 资源级 | &#10003;        |  -  | &#10003;   |[访问管理指南](https://intl.cloud.tencent.com/document/product/583/9203)  |	
| [批量计算](https://intl.cloud.tencent.com/document/product/599)  | 资源级 | &#10003;         |  -  | -    |-    |	
><sup>1</sup> 云服务器中 [GPU 服务器](https://intl.cloud.tencent.com/document/product/560)、[专用宿主机](https://intl.cloud.tencent.com/document/product/416)  均已支持使用 CAM。

## 存储	

 | 服务                                                          | 授权粒度 | 控制台  | 根据标签进行授权 |  服务角色 |	参考文档 |	
| ------------------------------------------------------------ | ------ | --------  | ------- | ---- |	---- |	
| [对象存储](https://intl.cloud.tencent.com/document/product/436) | 资源级 | &#10003;       | -  | &#10003;   |	[访问管理指南](https://intl.cloud.tencent.com/document/product/436/12473)   |
| [文件存储](https://intl.cloud.tencent.com/document/product/582) | 资源级 | &#10003;        | -  |  &#10003;    |[访问管理指南](https://intl.cloud.tencent.com/document/product/582/14679)   |		
| [云硬盘](https://intl.cloud.tencent.com/document/product/362) | 资源级  | &#10003;       | &#10003;  |  -    |-    |	
| [日志服务](https://intl.cloud.tencent.com/document/product/614)  | 资源级 | &#10003;        | -  | &#10003; |[访问管理指南](https://intl.cloud.tencent.com/document/product/614/35564)    |	
    
## 网络	

 | 服务                                                       | 授权粒度 | 控制台 | 根据标签进行授权  |  服务角色 |	参考文档 |	
| ------------------------------------------------------------ | ------ | -------- | ------- | ---- |	 ---- |
| [负载均衡](https://intl.cloud.tencent.com/document/product/214)   | 资源级  | &#10003;      | &#10003;    |    &#10003;  |	[访问管理指南](https://intl.cloud.tencent.com/document/product/214/9777) |	
| [私有网络 VPC ](https://intl.cloud.tencent.com/document/product/215)<sup>1</sup>  | 资源级 | &#10003;        | -     | - |	 - |	
| [专线接入](https://intl.cloud.tencent.com/document/product/216) | 资源级   | &#10003;       | -       | -  |	 - |	
><sup>1</sup> 私有网络 VPC 中 [弹性网卡](https://intl.cloud.tencent.com/document/product/576)、[NAT 网关](https://intl.cloud.tencent.com/document/product/1015)、[对等连接](https://intl.cloud.tencent.com/document/product/553)、[VPN 连接](https://intl.cloud.tencent.com/document/product/1037)、[Anycast 公网加速](https://intl.cloud.tencent.com/document/product/644)、[云联网](https://intl.cloud.tencent.com/document/product/1003)均已支持使用 CAM。

## 数据库	

 | 服务                                                         | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 |	参考文档 |	
| ------------------------------------------------------------ | ------ | --------| --------- | ---- |	---- |
| [云数据库 MySQL](https://intl.cloud.tencent.com/document/product/236)  | 资源级 | &#10003; | -  |  &#10003; |	[访问管理指南](https://intl.cloud.tencent.com/document/product/236/14469) |			
| [ 云数据库 SQL Server](https://intl.cloud.tencent.com/document/product/238)  |资源级 | &#10003;  | -    | -     |- |	
| [分布式数据库 TDSQL](https://intl.cloud.tencent.com/document/product/1042)  |资源级 | &#10003;  | -    | -    |[访问管理指南](https://intl.cloud.tencent.com/document/product/1042/33343) |	
| [云数据库 Redis](https://intl.cloud.tencent.com/document/product/239)   | 资源级| &#10003; | -  | - |[访问管理指南](https://intl.cloud.tencent.com/document/product/239/32845) |	
| [云数据库 MongoDB](https://intl.cloud.tencent.com/document/product/240) |资源级 | &#10003; | -   |&#10003;|[访问管理指南](https://intl.cloud.tencent.com/document/product/240/32839) |			
| [数据传输服务](https://intl.cloud.tencent.com/document/product/571)  | 资源级 |  &#10003;  | -    | &#10003;    |-|	

## CDN 与加速	

| 服务                                                      | 授权粒度 | 控制台  | 根据标签进行授权 | 服务角色 |	参考文档 |	
| ------------------------------------------------------------| ------ | -------- | -------- |  ---- |	---- |	
| [全球应用加速](https://intl.cloud.tencent.com/document/product/608)  | 资源级 | &#10003;  |  -   |  -  |-  |
| [全站加速网络](https://intl.cloud.tencent.com/document/product/570/10364)  | 服务级 | &#10003;  |  - | -  |-  |
| [内容分发网络](https://intl.cloud.tencent.com/document/product/228)| 操作级<sup>1</sup> | &#10003;   |  -   | &#10003; |[访问管理指南](https://intl.cloud.tencent.com/document/product/228/12722)  |

><sup>1</sup> 内容分发网络暂不支持通过策略语法进行权限管理，支持使用项目进行权限管理，单击 [权限说明](https://intl.cloud.tencent.com/document/product/228/12722) 了解更多。

## 中间件	

 | 服务                                                       | 授权粒度 | 控制台  | 根据标签进行授权 |  服务角色 |	参考文档 |
| ------------------------------------------------------------| ------ | -------- | -------- |  ---- |	 ---- |
| [消息队列 CMQ](https://intl.cloud.tencent.com/document/product/406) | 资源级   | &#10003;  | - |  - |	- |
| [消息队列 CKafka](https://intl.cloud.tencent.com/document/product/597) | 资源级 | &#10003; | - | &#10003;   | - |
| [API 网关](https://intl.cloud.tencent.com/document/product/628)     | 资源级  | &#10003;  | -  | &#10003; | - |

## 域名与网站	

 | 服务                                                         | 授权粒度| 控制台 | 根据标签进行授权  | 服务角色 |	参考文档 |
| ------------------------------------------------------------ | ------ | --------| ----- | ---- |	---- |	
| [网站备案](https://intl.cloud.tencent.com/document/product/1039)   | 服务级    | &#10003;   | -   |  - |	- |	

## 网络安全	

 | 服务                                                          | 授权粒度 | 控制台 | 根据标签进行授权 |  服务角色 |	参考文档 |
| ----------------------------------------------------------- | ------ | -------- | ----- | ---- | ---- |
| [BGP 高防包](https://intl.cloud.tencent.com/document/product/1029) | 服务级  | &#10003; | -   |  - | - |
| [BGP 高防 IP](https://intl.cloud.tencent.com/document/product/297) | 服务级  | &#10003; | -   |  - | - |

## 安全管理

 | 服务                                                         | 授权粒度  | 控制台  | 根据标签进行授权 | 服务角色 | 参考文档 |
| ------------------------------------------------------------ | ------ | -------- | ------- | ---- |  ---- | 
| [安全运营中心](https://intl.cloud.tencent.com/document/product/1008)    | 操作级  | &#10003; | -   | &#10003; |-  | 

## 应用安全

 | 服务                                                        | 授权粒度   | 控制台 | 根据标签进行授权 |  服务角色 |	参考文档 |
| ------------------------------------------------------------ | ------ | -------- | ------ |---- |	---- |	
| [Web 应用防火墙](https://intl.cloud.tencent.com/document/product/627)  | 操作级 | &#10003;  | -  |  - |- |

## 视频服务

 | 服务                                                         | 授权粒度 | 控制台 | 根据标签进行授权 | 服务角色 |	参考文档 |
| ------------------------------------------------------------ | ------ | -------- | -------- | ---- |	---- |	
| [云直播](https://intl.cloud.tencent.com/document/product/267)   | 资源级| &#10003; | &#10003;  |  &#10003;  |	[访问管理指南](https://intl.cloud.tencent.com/document/product/267/32468) |		

## 云智大数据平台

 | 服务                                                       | 授权粒度   | 控制台  | 根据标签进行授权 |  服务角色 |	参考文档 |
| ----------------------------------------------------------- | ------ | --------| ----- |  ---- |	 ---- |
| [弹性 MapReduce](https://intl.cloud.tencent.com/document/product/1026)   | 操作级 | &#10003;  | -   |  &#10003;  |	 [访问管理指南](https://intl.cloud.tencent.com/document/product/1026/31100) |
| [云数据仓库套件 Sparkling](https://intl.cloud.tencent.com/document/product/1019)  | 资源级  | &#10003; | -  | &#10003;    |	 - |
| [流计算服务](https://intl.cloud.tencent.com/document/product/1000)  | 服务级   | &#10003;     | -  | &#10003;  | - |
| [Elasticsearch Service](https://intl.cloud.tencent.com/document/product/845)  | 操作级   | &#10003; | -   |  -  |	 [访问管理指南](https://intl.cloud.tencent.com/document/product/845/19550) |

## 图像识别

 | 服务                                                         | 授权粒度 | 控制台  | 根据标签进行授权 | 服务角色 |	参考文档 |
| ------------------------------------------------------------ | ------ | -------- | -------- | ---- |	 ---- |		
| [文字识别](https://intl.cloud.tencent.com/document/product/1005) | 服务级| &#10003;| -  | - |	 - |	

## 游戏服务

| 服务                                                        | 授权粒度 | 控制台 | 根据标签进行授权 |  服务角色 |	参考文档 |
| ----------------------------------------------------------- | ------ | -------- | ----- |  ---- |	 ---- |		
| [游戏多媒体引擎](https://intl.cloud.tencent.com/document/product/607)  | 资源级 | &#10003;| -   |  -    |	 -   |

## 移动服务	

 | 服务                                                        | 授权粒度  | 控制台 | 根据标签进行授权 |  服务角色 |	参考文档 |
| ------------------------------------------------------------  | ------ | -------- | ------- | ---- |	---- |	
| [腾讯移动推送](https://intl.cloud.tencent.com/document/product/1024)   |操作级  | &#10003; | -   |  -   |	-   |

## 云通信	

 | 服务                                                         | 授权粒度 | 控制台 | 根据标签进行授权 | 服务角色 |	参考文档 |
| ------------------------------------------------------------ | ------ | -------- | ----- | ---- |	---- |
| [短信](https://intl.cloud.tencent.com/document/product/382) | 接口级 | &#10003; | -   | -  |	-  |	
	
## 云资源管理

 | 服务                                                         | 授权粒度  | 控制台 | 根据标签进行授权 |  服务角色 |	参考文档 |
| ----------------------------------------------------------- | ------ | -------- | ----- | ---- |	 ---- |	
| [标签](https://intl.cloud.tencent.com/document/product/651) | 操作级 | &#10003;  | - |  - |	 - |	

## 管理与审计

 | 服务                                                         | 授权粒度 | 控制台  | 根据标签进行授权 |  服务角色 |	参考文档 |
| ------------------------------------------------------------| ------ | --------| ----- |  ---- |		 ---- |
| [访问管理](https://intl.cloud.tencent.com/document/product/598)  | 操作级  | &#10003; | -   | -    | [访问管理指南](https://intl.cloud.tencent.com/document/product/598/17848)   |
| [云审计](https://intl.cloud.tencent.com/document/product/1021)  | 操作级  | &#10003; | -   | &#10003;    | -   |
| [企业组织](https://intl.cloud.tencent.com/document/product/1031) | 操作级 | &#10003; | -  |- | -   |

## 监控与运维	

 | 服务                                                         | 授权粒度 | 控制台  | 根据标签进行授权 | 服务角色 |	参考文档 |
| ------------------------------------------------------------  | ------ | -------- | ----- | ---- |	---- |
| [云监控](https://intl.cloud.tencent.com/document/product/248) | 操作级 | &#10003;  | -  |  - |	- |	
| [密钥管理服务](https://intl.cloud.tencent.com/document/product/1030/) | 资源级   | &#10003;  | -  |  -     |[访问管理指南](https://intl.cloud.tencent.com/document/product/1030/31978) |	
| [迁移服务平台](https://intl.cloud.tencent.com/document/product/1036/)  | -   | -  | -   |&#10003;    |	- |	