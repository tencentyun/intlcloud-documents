本文将为您介绍资产概览页的功能和操作。

## 概述
资产概览是从资产维度对主机及15项关键资产指纹数据进行统计盘点、可视化呈现，便于用户了解主机资产情况。

## 限制说明
所有腾讯云用户均可查看资产概览。但由于资产指纹的采集受版本限制，资产概览可统计的数据存在差异，见下表。

| 防护版本 | 采集的资产指纹 |
|---------|---------|
| 基础版（免费） | 不支持 |
| 专业版 | 10项：资源监控、账号、端口、进程、软件应用、数据库、Web 应用、Web 服务、Web 框架、Web 站点 |
| 旗舰版 | 15项：资源监控、账号、端口、进程、软件应用、数据库、Web 应用、Web 服务、Web 框架、Web 站点、Jar 包、启动服务、计划任务、环境变量、内核模块 |

<dx-alert infotype="explain" title="">
资产指纹数据每隔8小时自动采集一次，支持手动采集。
</dx-alert>

## 操作指南
1. 登录 [主机安全控制台](https://console.intl.cloud.tencent.com/cwp) 。
2. 单击左侧导航中的**资产概览**，各功能说明如下。

### 资产概况
在**资产概况**区域中，可查看全部资产及资产指纹的统计情况。
![](https://qcloudimg.tencent-cloud.cn/raw/de78acd734a489e31338db2bf3e6580d.png)
### 主机概况趋势
在**主机概况趋势**中，将以折线图的形式呈现总台数、在线台数、离线台数、风险台数的变化情况。
![](https://qcloudimg.tencent-cloud.cn/raw/d3bd77ea1d4fdd5d38097862bfe4aa19.png)
支持近7天、近14天、近30天或自定义时间段（最长不超过近3个月）查询。
单击**下载**，将导出所选时间范围内主机每天的数据情况。

### 主机标签Top5
在**主机标签TOP5**区域中，可查看所有主机中使用最多的前5个主机安全标签。
![](https://qcloudimg.tencent-cloud.cn/raw/1fa1753eb971f93cb767125af70dbf53.png)

### 资源监控概览
在资源监控概览区域中，可查看系统负载、内存使用率、硬盘使用率的分布情况及相应TOP 5。
![](https://qcloudimg.tencent-cloud.cn/raw/ef7262f38eada7c9f44247dca224cae3.png)

<dx-alert infotype="explain" title="">
仅Linux服务器支持统计系统负载，Windows服务器暂无法支持。
</dx-alert>

### 资产指纹TOP5
在**资产指纹TOP5**中，统计展示了账号、端口、进程、软件应用、数据库、Web 应用、Web服务、Web 框、Web 站点的TOP5数据。
![](https://qcloudimg.tencent-cloud.cn/raw/4c41fc0e0012274de985770e06c250ee.png)



