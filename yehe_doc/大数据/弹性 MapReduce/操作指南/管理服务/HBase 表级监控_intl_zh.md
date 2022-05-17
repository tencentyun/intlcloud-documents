## 功能说明
HBase 表级监控提供了 HBase 中各表的读写请求数以及表存储情况的监控。
## HBase表负载列表
1. 登录 [EMR 控制台](https://console.cloud.tencent.com/emr)，在集群列表中单击对应的**集群ID/名称**进入集群详情页。
2. 在集群详情页中单击集群服务，然后选择 HBase 组件右上角**操作 > 表级监控**，即可进行相关 HBase 表负载查询。
![](https://qcloudimg.tencent-cloud.cn/raw/6d062e13f9b62dc8998ae662b09f8704.png)

## 查看表详情
单击对应表名，即可弹出表详情。详情页可按整个表、节点维度展示所选择表的请求量（包括读和写）、store 大小（包括 memstore 和 storeFile）两个指标数据，选择右上角的**节点筛选器**可切换节点查看。
![](https://qcloudimg.tencent-cloud.cn/raw/3f5f82ba954706c21398bce89ee01b85.png)

## Regions 操作
单击 Regions 操作，即可查看表所包含的各个 Region 的读写请求量。
![](https://qcloudimg.tencent-cloud.cn/raw/2d4a3f7e2eb22d5d7e38dd17e312e9c4.png)

## Region 详情
单击对应 Region 名，即可弹出 Region 详情。详情页可按不同时间粒度展示所选择表的请求量（包括读和写）指标数据，选择右上角的**时间粒度**可切换粒度查看。
![](https://qcloudimg.tencent-cloud.cn/raw/7bd425872b04d87c303f228e58906bd1.png)

## RegionServers 操作
单击 RegionServers 操作，即可查看表所分布的各个 RegionServer 的请求延迟。
![](https://qcloudimg.tencent-cloud.cn/raw/c68cfd7ac497c8e3a9d96fd5ebf7f344.png)
