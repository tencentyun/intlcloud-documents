## 功能介绍
支持 Impala 查询多种维度指标的分位分布视图，Impala 列表可快速查看查询语句、查询状态、用户、数据库、扫描行数、峰值内存使用、总读取/发送 Bytes 量、HDFS 扫描行数等多项明细指标。

## 操作步骤

1. 登录 [EMR 控制台](https://console.cloud.tencent.com/emr)，在集群列表中单击对应的集群 **ID/名称**进入集群详情页。  
2. 在集群详情页中单击**集群服务**，然后选择 IMPALA 组件右上角**操作 > 查询管理**，即可进行相关视图查看。
示例：以持续时长为例当前筛选时间范围内，TP90分位时长为6.86k(ms)表示90%的查询时长在6.86s以内。
![](https://qcloudimg.tencent-cloud.cn/raw/7e97423c7ce5d9d5cc1c5c521d813db3.png)
3. 提供 Impala 查询列表信息，部分列头字段支持筛选或排序功能，支持多种维度的复合筛选操作。
![](https://qcloudimg.tencent-cloud.cn/raw/14700f34a1d04e23b7e3cbbacc8935e0.png)
4.	**操作列 > 总览**可查看 Impala 查询的全生命周期的时间分布信息、重点指标信息及运行时的部分节点信息。
![](https://qcloudimg.tencent-cloud.cn/raw/4d2462fd2946facd890d9a833fb29114.png)
**操作列 > 详情**中可查看查询语句、查询计划、执行总览、Profile、内存信息。
![](https://qcloudimg.tencent-cloud.cn/raw/5dc48316831aecd786494088a5af0f36.png)
>! 执行时长超过3s的 Impala 查询提供查看**总览**和**详情**中的 Profile 功能。
