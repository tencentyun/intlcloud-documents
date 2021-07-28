## 功能介绍
 弹性 MapReduce 支持在控制台对各组件参数最近的一次配置回滚，本文为您介绍如何通过控制台回滚各组件参数配置。

## 操作步骤
1. 登录 [EMR 控制台](https://console.cloud.tencent.com/emr)，在【集群列表】中选择对应的集群单击【详情】进入集群详情页。
2. 在集群详情页中选择【集群服务】单击对应的组件卡页右上角【操作】>【配置管理】，以 HDFS 为例。
![](https://main.qcloudimg.com/raw/f6fa95eb30aa3b929bd1ea4dd86462d1.png)
3. 选择【配置历史】可以看到所有组件的配置历史，支持对最近一次参数配置变更回滚。单击【详情】可以看到回滚前后的参数值对比，选择【回滚】>【确认回滚】，回滚成功重启组件，稍作等待回滚即可生效。
![](https://main.qcloudimg.com/raw/bf67f3da357c8b6592318167dce0cda1.png)
![](https://main.qcloudimg.com/raw/b9fa163d09e3a2668d6c2ca2c4c1ad21.png)
