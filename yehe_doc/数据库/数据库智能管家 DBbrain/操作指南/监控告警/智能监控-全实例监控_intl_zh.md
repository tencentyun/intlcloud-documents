全实例监控页为用户提供全实例维度（用户整体视角）的数据库监控指标展示。统一监控视图里展示所有实例单个监控指标的横向视图，便于用户查看和发现数据库异常问题，也为用户提供全新的宏观监控查看视角。

>?全实例监控功能目前支持云数据库 MySQL（不含单节点 - 基础型）、云原生数据库 TDSQL-C（TDSQL-C for MySQL）、自建数据库 MySQL、云数据库 Redis、云数据库 MongoDB。

![](https://qcloudimg.tencent-cloud.cn/raw/1d7f3d7b55aac41fc641410c24e2ea8f.png)

## 切换地域
1. 登录 [DBbrain 控制台](https://console.cloud.tencent.com/dbbrain/analysis)，在左侧导航选择**监控告警** > **智能监控**，在上方选择对应数据库，然后选择**全实例监控**页。
2. 在全实例监控页，默认展示全地域的数据库实例，可通过上方的下拉菜单按地域进行筛选。

## 切换监控指标
1. 登录 [DBbrain 控制台](https://console.cloud.tencent.com/dbbrain/analysis)，在左侧导航选择**监控告警** > **智能监控**，在上方选择对应数据库，然后选择**全实例监控**页。
2. 通过上方的下拉菜单搜索控件，选择需要查看的监控指标，支持腾讯云 MySQL/TDSQL-C 云监控提供的所有监控指标及用户自建数据库的监控指标，全实例监控视图根据所选指标排序展示。
![](https://qcloudimg.tencent-cloud.cn/raw/1edc65e72bf1ae84f4d6bf207ea42435.png)

## 查看实时/历史监控
1. 登录 [DBbrain 控制台](https://console.cloud.tencent.com/dbbrain/analysis)，在左侧导航选择**监控告警** > **智能监控**，在上方选择对应数据库，然后选择**全实例监控**页。
2. 在全实例监控页，可查看实时监控和历史监控，历史监控中会显示所选时间段内该指标的 MAX 值和出现的时间点。

## 搜索实例
1. 登录 [DBbrain 控制台](https://console.cloud.tencent.com/dbbrain/analysis)，在左侧导航选择**监控告警** > **智能监控**，在上方选择对应数据库，然后选择**全实例监控**页。
2. 在全实例监控页，选择腾讯云 MySQL 数据库时，可按实例 ID、实例名和内网 IP 进行模糊搜索；选择腾讯云 TDSQL-C 数据库时，可按集群 ID、集群名、实例 ID、实例名和接入点地址进行模糊搜索；选择自建 MySQL 数据库时，可按实例 ID、实例名和 IP 地址进行模糊搜索。
>?单击搜索栏右方的“标识符”，可查看实例搜索帮助文档。
>
![](https://qcloudimg.tencent-cloud.cn/raw/6054b1a4719e3e2b6df0c41876ff8ee7.png)

## 切换宫格
1. 登录 [DBbrain 控制台](https://console.cloud.tencent.com/dbbrain/analysis)，在左侧导航选择**监控告警** > **智能监控**，在上方选择对应数据库，然后选择**全实例监控**页。
2. 在全实例监控页，可切换9宫格和36宫格的视图，用户实例较多的情况下建议使用**36宫格**视图，全局视角更明显，用户也可以更清晰地查看监控指标的波动状态。
单击实例右上角的展开按钮，可以查看清晰的实例信息和指标趋势详情。

