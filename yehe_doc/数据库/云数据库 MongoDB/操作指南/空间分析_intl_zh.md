## 操作场景
云数据库 MongoDB 支持接入数据库智能管家 DBbrain对 mongod 节点的计算存储规格进行分析。 您可以查看实例空间的使用率，包括数据空间和日志空间的大小、空间使用率的日均增长量、预估的可用天数，以及查看实例表空间、库空间所占用的空间详情及变化趋势。 

## 前提条件
- 已 [创建云数据库 MongoDB 实例](https://intl.cloud.tencent.com/document/product/240/3551)。
- 云数据库 MongoDB 副本集实例或分片实例状态为**运行中**。

## 操作步骤
1. 登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)。
2. 在左侧导航栏 **MongoDB** 的下拉列表中，选择**副本集实例**或者**分片实例**。副本集实例与分片实例操作类似。
3. 在右侧实例列表页面上方，选择地域。
4. 在实例列表，查找需进行空间分析的实例。
5. 在目标实例的**实例 ID / 名称**列，单击蓝色字体的实例 ID，进入**实例详情**页面。
6. 在**实例详情**页面的**配置信息**区域，**mongod 节点规格**的后面单击**空间分析**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/413495df598c0f4c6d56154b03526abc.png" style="zoom:80%;" />
7. 在 [DBbrain 控制台](https://console.cloud.tencent.com/dbbrain) 的空间分析页面，分析 mongod 节点的空间使用详情。

