## 功能介绍
通过 Kudu 数据表监控及 Teblet 分析功能帮助排查表内数据热点倾斜、Tablet 部署层数据热点及倾斜等常见场景。
1. Kudu 数据表分析提供表级、表内 Tablet、TabletServer 读写 QPS、存储等相关负载维度信息
2. 提供 Tablet 分析，结合实际场景支持对所属表或所属 TabletServer 分析读取 QPS、写入 QPS 信息级历史变化趋势。

## 操作步骤
1. 登录 [EMR 控制台](https://console.cloud.tencent.com/emr)，在集群列表中单击对应的**集群 ID/名称**进入集群详情页。
2. 在集群详情页中单击**集群服务**，然后选择 **Kudu组件右上角操作 >数据表分析**，即可进行相关 Kudu 数据表负载查询。

## 数据表列表		
Kudu 数据表列表可查看表级请求 QPS、写入 QPS、OnDiskDataSize 存储量信息，通过列 title 的排序按钮可定位集群 Top 数据表。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/RnfI826_%E5%9B%BD%E9%99%8514.png)
### 查看表详情
单击对应表名，即可弹出表详情。详情页可按整个表、节点维度展示所选择表的请求量（包括读和写）、store 大小（包括 OnDiskDataSize）两个指标数据，选择右上角的节点筛选器可切换节点查看。
### Tablets 操作
单击 **Tablets 操作**，即可查看表所包含的各个 Tablet 的读写请求量，定位表内 Tablet 热点情况。
### Tablet 详情
单击对应 Tablet 名，即可弹出 Tablet 详情，查看指标趋势。详情页可按不同时间粒度展示所选择表的请求量和扫描量等指标数据，选择右上角的时间粒度可切换粒度查看。
### TabletServers 操作
单击 **TabletServers 操作**，即可查看表所分布的各个 TabletServer 的请求延迟及存储数据等信息。
## Tablet 分析
Tablet 分析可检索所属表或筛选所属 TabletServer，通过平均请求 QPS、平均读写 QPS 信息定位集群热点请求分布。
单击列 title 平均读取 QPS、平均写入 QPS 的视图按钮，可查看当前页 Tablet 记录指标的历史趋势，观测突变请求信息，支持时间区间选择。
