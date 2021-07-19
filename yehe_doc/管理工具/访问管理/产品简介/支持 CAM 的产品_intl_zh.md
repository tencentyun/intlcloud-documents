<style>
table th:nth-of-type(1) {
width: 27%;        
}
table th:nth-of-type(2) {
width: 15%;        
}
table th:nth-of-type(3) {
width:12%;        
}
table th:nth-of-type(4) {
width: 13%;        
}
table th:nth-of-type(5) {
width: 15%;        
}
table th:nth-of-type(6) {
width: 18%;        
}
</style>

## 简介	

访问管理已经支持对多数腾讯云产品服务进行权限管理。本文主要介绍支持访问管理 CAM 的产品服务的相关信息。具体维度包括授权粒度、控制台、根据标签进行授权、参考文档等。
以下列表分别罗列了腾讯云平台各大产品类别下已支持 CAM 的服务。
对表中信息进行如下定义：

- 服务：支持 CAM 的云服务的名称，单击链接至对应产品服务文档，方便您快速获取相关信息。	
- 授权粒度：当前服务提供的最小授权粒度。

>? 其中授权粒度按照粒度粗细分为服务级、操作级和资源级三个级别。	
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
| [云服务器](https://intl.cloud.tencent.com/document/product/213) <sup>1</sup> | 资源级  | &#10003;      |&#10003;    |  &#10003;  |	 [访问管理指南](https://intl.cloud.tencent.com/document/product/213/10315)   |
| [弹性伸缩](https://intl.cloud.tencent.com/document/product/377) | 资源级   | &#10003;      | &#10003;  | &#10003;    |	-    |	
| [批量计算](https://intl.cloud.tencent.com/document/product/599)  | 资源级 | &#10003;         |  &#10003;  | -    |[访问管理指南](https://intl.cloud.tencent.com/document/product/599/33471)   |		

>?<sup>1</sup> 云服务器中 [GPU 云服务器](https://intl.cloud.tencent.com/document/product/560)、[专用宿主机](https://intl.cloud.tencent.com/document/product/416)  均已支持使用 CAM。


## 容器
| 服务                                                          | 授权粒度 | 控制台  | 根据标签进行授权 |  服务角色 |	参考文档 |	
| ------------------------------------------------------------ | ------ | --------  | ------- | ---- |	---- |	
| [容器服务](https://intl.cloud.tencent.com/document/product/457) | 资源级  | &#10003;       | &#10003; | &#10003;    |	[访问管理指南](https://intl.cloud.tencent.com/document/product/457/11542)  |	
| [容器镜像服务](https://intl.cloud.tencent.com/document/product/1051) | 资源级  | 资源级 | &#10003; | - | &#10003; |	[访问管理指南](https://intl.cloud.tencent.com/document/product/1051/37246)  |	

## 存储	

 | 服务                                                          | 授权粒度 | 控制台  | 根据标签进行授权 |  服务角色 |	参考文档 |	
| ------------------------------------------------------------ | ------ | --------  | ------- | ---- |	---- |	
| [对象存储](https://intl.cloud.tencent.com/document/product/436) | 资源级 | &#10003;       | &#10003; <sup>1</sup> | &#10003;   |	[访问管理指南](https://intl.cloud.tencent.com/document/product/436/12470)   |
| [文件存储](https://intl.cloud.tencent.com/document/product/582) | 资源级 | &#10003;        | &#10003;  |  &#10003;    |[访问管理指南](https://intl.cloud.tencent.com/document/product/582/14679)   |			
| [云硬盘](https://intl.cloud.tencent.com/document/product/362) | 资源级  | &#10003;       | &#10003;  |  -    |-    |	
| [云数据迁移](https://intl.cloud.tencent.com/document/product/623)  | 服务级 | &#10003;        | -  |  - | - |	
| [日志服务](https://intl.cloud.tencent.com/document/product/614)  | 资源级 | &#10003;        | -  | &#10003; |[访问管理指南](https://intl.cloud.tencent.com/document/product/614/32854)    |	

> ?<sup>1</sup> 对象存储中 GetService 和 PutBucket 暂未支持标签授权，需要单独进行自定义策略授权。

## 网络	

| 服务                                                       | 授权粒度 | 控制台 | 根据标签进行授权  |  服务角色 |	参考文档 |	
| ------------------------------------------------------------ | ------ | -------- | ------- | ---- |	 ---- |
| [负载均衡](https://intl.cloud.tencent.com/document/product/214)   | 资源级  | &#10003;      | &#10003;    |    &#10003;  |	[访问管理指南](https://intl.cloud.tencent.com/document/product/214/9777) |	
| [私有网络 VPC ](https://intl.cloud.tencent.com/document/product/215)<sup>1</sup>  | 资源级 | &#10003;        | &#10003;     | - |	 - |	
| [专线接入](https://intl.cloud.tencent.com/document/product/216) | 资源级   | &#10003;       | &#10003;       | -  |	 - |	

>?<sup>1</sup> 私有网络中 [弹性网卡](https://intl.cloud.tencent.com/document/product/576)、[NAT 网关](https://intl.cloud.tencent.com/document/product/1015)、[对等连接](https://intl.cloud.tencent.com/document/product/553)、[VPN 连接](https://intl.cloud.tencent.com/document/product/1037)、[网络流日志](https://intl.cloud.tencent.com/document/product/682) 、[Anycast 公网加速](https://intl.cloud.tencent.com/document/product/644)、[云联网](https://intl.cloud.tencent.com/document/product/1003)、[共享带宽包](https://intl.cloud.tencent.com/document/product/684) 均已支持使用 CAM。

## CDN 与加速	

| 服务                                                      | 授权粒度 | 控制台  | 根据标签进行授权 | 服务角色 |	参考文档 |	
| ------------------------------------------------------------| ------ | -------- | -------- |  ---- |	---- |	
| [全球应用加速](https://intl.cloud.tencent.com/document/product/608)  | 资源级 | &#10003;  |  &#10003;   |  -  |-  |
| [全站加速网络](https://intl.cloud.tencent.com/document/product/570)  | 资源级 | &#10003;  |  &#10003; | -  | -  |
| [内容分发网络](https://intl.cloud.tencent.com/document/product/228)<sup>1</sup>| 资源级 | &#10003;   |  &#10003;   | &#10003; |[访问管理指南](https://intl.cloud.tencent.com/document/product/228/35229)  |


## 数据库	

 | 服务                                                         | 授权粒度 | 控制台   | 根据标签进行授权 | 服务角色 |	参考文档 |	
| ------------------------------------------------------------ | ------ | --------| --------- | ---- |	---- |
| [云数据库 MySQL](https://intl.cloud.tencent.com/document/product/236)  | 资源级 | &#10003; | &#10003;  |  &#10003; |	[访问管理指南](https://intl.cloud.tencent.com/document/product/236/14469) |		
| [云数据库 MariaDB](https://intl.cloud.tencent.com/document/product/237)  |资源级 | &#10003;  | &#10003;    | &#10003;    |[访问管理指南](https://intl.cloud.tencent.com/document/product/237/35441) |	
| [ 云数据库 SQL Server](https://intl.cloud.tencent.com/document/product/238)  |资源级 | &#10003;  | &#10003;    | -     |[访问管理指南](https://intl.cloud.tencent.com/document/product/238/34583) |	
| [云数据库 PostgreSQL](https://intl.cloud.tencent.com/document/product/409)  |资源级 | &#10003;  | &#10003;   | -     | - |
| [TDSQL MySQL版](https://intl.cloud.tencent.com/document/product/1042)  |资源级 | &#10003;  |  &#10003;    | -    |[访问管理指南](https://intl.cloud.tencent.com/document/product/1042/33343) |	
| [云数据库 Redis](https://intl.cloud.tencent.com/document/product/239)   | 资源级| &#10003; | -  | - |[访问管理指南](https://intl.cloud.tencent.com/document/product/239/32845) |	
| [云数据库 MongoDB](https://intl.cloud.tencent.com/document/product/240) |资源级 | &#10003; | &#10003;   |&#10003;|[访问管理指南](https://intl.cloud.tencent.com/document/product/240/32839) |			
| [数据传输服务](https://intl.cloud.tencent.com/document/product/571)  | 资源级 |  &#10003;  | &#10003;    | &#10003;    | - |
| [游戏数据库 TcaplusDB](https://intl.cloud.tencent.com/document/product/1016)  | 资源级 |  &#10003;  | &#10003;   | -    | - |		
| [数据库智能管家 DBbrain](https://intl.cloud.tencent.com/document/product/1035) |资源级 | &#10003;  | -    | -    |[访问管理指南](https://intl.cloud.tencent.com/document/product/1035/36050)|	
| [TDSQL-A PostgreSQL 版](https://intl.cloud.tencent.com/document/product/1099) | 资源级 | &#10003; | &#10003; | &#10003; | [访问管理指南](https://intl.cloud.tencent.com/document/product/1099/40845) |


## Serverless	

| 服务                                                      | 授权粒度 | 控制台  | 根据标签进行授权 | 服务角色 |	参考文档 |	
| ------------------------------------------------------------| ------ | -------- | -------- |  ---- |	---- |	
| [云函数](https://intl.cloud.tencent.com/document/product/583)  | 资源级 | &#10003;        |  &#10003;  | &#10003;   |[访问管理指南](https://intl.cloud.tencent.com/document/product/583/18014)  |	
| [Serverless 应用中心](https://intl.cloud.tencent.com/document/product/1040)  | 资源级 | - |  -   |  &#10003;   | -   |
| Serverless Framework | -    | -    | -    | &#10003; | -    |



## 中间件	

 | 服务                                                       | 授权粒度 | 控制台  | 根据标签进行授权 |  服务角色 |	参考文档 |
| ------------------------------------------------------------| ------ | -------- | -------- |  ---- |	 ---- |
| [消息队列 CMQ](https://intl.cloud.tencent.com/document/product/406) | 资源级   | &#10003;  | &#10003; |  - |	[访问管理指南](https://intl.cloud.tencent.com/document/product/406/34257) |
| [消息队列 CKafka](https://intl.cloud.tencent.com/document/product/597) | 资源级 | &#10003; |  &#10003;  | &#10003;   | - |
| [API 网关](https://intl.cloud.tencent.com/document/product/628)     | 资源级  | &#10003;  | &#10003;  | &#10003; |[访问管理指南](https://intl.cloud.tencent.com/document/product/628/34064)|

## 数据处理	

 | 服务                                                         | 授权粒度| 控制台 | 根据标签进行授权  |  服务角色 |	参考文档 |
| ------------------------------------------------------------ | ------ | --------| ----- | ---- |	 ---- |	
| [数据万象](https://intl.cloud.tencent.com/document/product/1045)   | 资源级    | &#10003;   | -   | &#10003; |	[访问管理指南](https://intl.cloud.tencent.com/document/product/1045/33449) |

## 域名与网站	

 | 服务                                                         | 授权粒度| 控制台 | 根据标签进行授权  | 服务角色 |	参考文档 |
| ------------------------------------------------------------ | ------ | --------| ----- | ---- |	---- |	
| [网站备案](https://intl.cloud.tencent.com/document/product/1022)   | 服务级    | &#10003;   | -   |  - |	- |	
| [SSL证书](https://intl.cloud.tencent.com/document/product/1007)   | 资源级    | &#10003;   | -   |  - |	- |	



## 数据安全

| 服务                                                         | 授权粒度  | 控制台  | 根据标签进行授权 | 服务角色 | 参考文档 |
| ------------------------------------------------------------ | ------ | -------- | ------- | ---- |  ---- |
| [密钥管理系统](https://intl.cloud.tencent.com/document/product/1030) | 资源级   | &#10003;  | &#10003;  |  -     |[访问管理指南](https://intl.cloud.tencent.com/document/product/1030/31978) |


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
| [实时音视频](https://intl.cloud.tencent.com/document/product/647)   | 资源级| &#10003; | &#10003;  |  - |	-|	
| [云直播](https://intl.cloud.tencent.com/document/product/267)   | 资源级| &#10003; | &#10003; |  &#10003;  |	[访问管理指南](https://intl.cloud.tencent.com/document/product/267/32468) |	
| [云点播](https://intl.cloud.tencent.com/document/product/266)    | 资源级   | &#10003;  | &#10003;   |  &#10003; |	[访问管理指南](https://intl.cloud.tencent.com/document/product/266/33970)  |	
| [视频处理](https://intl.cloud.tencent.com/document/product/1041)    | 服务级   | &#10003;  | -    |   &#10003;   |	-  |		
| [媒体直播](https://intl.cloud.tencent.com/document/product/1048)    | 操作级   | &#10003;  | -    |   -   |	-  |	
| [媒体包装](https://intl.cloud.tencent.com/document/product/1063)    | 操作级   | &#10003;  | -    |   -   |	-  |	

## 云智大数据平台

 | 服务                                                       | 授权粒度   | 控制台  | 根据标签进行授权 |  服务角色 |	参考文档 |
| ----------------------------------------------------------- | ------ | --------| ----- |  ---- |	 ---- |
| [弹性 MapReduce](https://intl.cloud.tencent.com/document/product/1026)   | 资源级 | &#10003;  | &#10003;   |  &#10003;  |	 [访问管理指南](https://intl.cloud.tencent.com/document/product/1026/31100) |
| [Elasticsearch Service](https://intl.cloud.tencent.com/document/product/845)  | 资源级   | &#10003; | &#10003;   |  -  |	 [访问管理指南](https://intl.cloud.tencent.com/document/product/845/19550) |

## 图像识别

 | 服务                                                         | 授权粒度 | 控制台  | 根据标签进行授权 | 服务角色 |	参考文档 |
| ------------------------------------------------------------ | ------ | -------- | -------- | ---- |	 ---- |		
| [文字识别](https://intl.cloud.tencent.com/document/product/1005) | 服务级| &#10003;| -  | - |	 - |	

## 游戏服务

| 服务                                                        | 授权粒度 | 控制台 | 根据标签进行授权 |  服务角色 |	参考文档 |
| ----------------------------------------------------------- | ------ | -------- | ----- |  ---- |	 ---- |		
| [游戏多媒体引擎](https://intl.cloud.tencent.com/document/product/607)  | 资源级 | &#10003;| &#10003;   |  -    |	 -   |
| [游戏服务器伸缩](https://intl.cloud.tencent.com/document/product/1055)  | 资源级 | &#10003;| &#10003;   |  &#10003;    |  [访问管理指南](https://intl.cloud.tencent.com/zh/document/product/1055/37776)   |
| [游戏玩家匹配](https://intl.cloud.tencent.com/document/product/1072) | 资源级   | &#10003; | &#10003;         | &#10003; | - |


## 移动服务	

 | 服务                                                        | 授权粒度  | 控制台 | 根据标签进行授权 |  服务角色 |	参考文档 |
| ------------------------------------------------------------  | ------ | -------- | ------- | ---- |	---- |	
| [ 腾讯移动推送](https://intl.cloud.tencent.com/document/product/1024)   |资源级  | &#10003; | -   |  -   |	[访问管理指南](https://intl.cloud.tencent.com/document/product/1024/35288)   |

## 云通信	

 | 服务                                                         | 授权粒度 | 控制台 | 根据标签进行授权 | 服务角色 |	参考文档 |
| ------------------------------------------------------------ | ------ | -------- | ----- | ---- |	---- |
| [即时通信 IM](https://intl.cloud.tencent.com/document/product/1047)   | 资源级 | &#10003;   | -  |  - | - |
| [短信](https://intl.cloud.tencent.com/document/product/382) | 资源级 | &#10003; | &#10003;   | -  |	-  |	

## 云资源管理

 | 服务                                                         | 授权粒度  | 控制台 | 根据标签进行授权 |  服务角色 |	参考文档 |
| ----------------------------------------------------------- | ------ | -------- | ----- | ---- |	 ---- |	
| [标签](https://intl.cloud.tencent.com/document/product/651) | 操作级 | &#10003;  | - |  - |	 - |	
| [资源编排 TIC](https://intl.cloud.tencent.com/document/product/1043) | 服务级 | -  | - | &#10003; |	 - |	

## 管理与审计

 | 服务                                                         | 授权粒度 | 控制台  | 根据标签进行授权 |  服务角色 |	参考文档 |
| ------------------------------------------------------------| ------ | --------| ----- |  ---- |		 ---- |
| [访问管理](https://intl.cloud.tencent.com/document/product/598)  | 操作级  | &#10003; | -   | -    | [访问管理指南](https://intl.cloud.tencent.com/document/product/598/17848)   |
| [云审计](https://intl.cloud.tencent.com/document/product/1021)  | 操作级  | &#10003; | -   | &#10003;    | -   |
| [企业组织](https://intl.cloud.tencent.com/document/product/1031) | 操作级 | &#10003; | -  |- | -   |

## 监控与运维	

 | 服务                                                         | 授权粒度 | 控制台  | 根据标签进行授权 | 服务角色 |	参考文档 |
| ------------------------------------------------------------  | ------ | -------- | ----- | ---- |	---- |
| [云监控](https://intl.cloud.tencent.com/document/product/248) | 资源级 | &#10003;  | &#10003;  |  &#10003; |	- |		
| [迁移服务平台](https://intl.cloud.tencent.com/document/product/1036)  | 服务级   | &#10003; | -   |&#10003;    |	- |	









