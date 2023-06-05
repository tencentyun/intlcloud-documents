## 功能介绍
数据表分析提供 Hbase 表级、表内 Regions、Regionservers 的读写请求量和存储情况等维度信息；同时提供 Region 分析，结合实际场景支持对所属表或所属 RegionServer 分析读取 QPS、写入 QPS 信息及历史变化趋势。

## 操作步骤
1. 登录 [EMR 控制台](https://console.cloud.tencent.com/emr)，在集群列表中单击对应的**集群ID/名称**进入集群详情页。
2. 在集群详情页中单击**集群服务**，然后选择 HBase 组件右上角**操作 >数据表分析**，即可进行相关 HBase 数据表负载查询。

## 数据表列表
Hbase 数据表列表可查看表级请求 QPS、写入 QPS、MetaStore 存储量、StoreFile 大小等信息，通过列 title 的排序按钮可定位集群 Top 数据表。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/8eaP605_%E5%9B%BD%E9%99%851.png)

### 查看表详情
单击对应表名，即可弹出表详情。详情页可按整个表、节点维度展示所选择表的请求量（包括读和写）、store 大小（包括 memstore 和 storeFile）两个指标数据，选择右上角的节点筛选器可切换节点查看。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/DvIx551_%E5%9B%BD%E9%99%852.png)

### Regions 操作
单击 **Regions 操作**，即可查看表所包含的各个 Region 的读写请求量，定位表内 region 热点情况。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/IRTT895_%E5%9B%BD%E9%99%853.png)

### Region 详情
单击对应 Region 名，即可弹出 Region 详情，查看指标趋势。详情页可按不同时间粒度展示所选择表的请求量（包括读和写）指标数据，选择右上角的时间粒度可切换粒度查看。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/WiUR800_%E5%9B%BD%E9%99%854.png)

### RegionServers 操作
单击 **RegionServers 操作**，即可查看表所分布的各个 RegionServer 的请求延迟。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/mv8U638_%E5%9B%BD%E9%99%85%E7%AB%995.png)
## Region 分析
Region 分析可检索所属表或筛选所属 RegionServer，通过平均请求 QPS、平均读写 QPS 信息定位集群热点请求分布。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5dI2042_%E5%9B%BD%E9%99%856.png)
点击列 title 平均读取 QPS、平均写入 QPS 的视图按钮，可查看当前页 Region 记录指标的历史趋势，观测突变请求信息，支持时间区间选择。
