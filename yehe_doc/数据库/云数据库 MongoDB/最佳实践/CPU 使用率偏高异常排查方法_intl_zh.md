## 问题描述

日常运维，登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)，单击实例 ID 进入**实例详情**页面，选择**系统监控**页签，检查实例的监控指标详情，发现数据库 **CPU监控类** 指标明显持续偏高。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/p6hj771_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16753229907497.png)

## 原因分析及解决方法

1. 确定业务是否存在很高的操作数据库频率。
登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)，单击实例 ID 进入**实例详情**页面，选择**系统监控**页签，查看实例总请求指标 QPS，QPS 反馈的是节点每秒所有请求的次数。
若业务 QPS 明显高，请评估是否需要升级实例配置。具体操作，请参见 <a href="https://intl.cloud.tencent.com/document/product/240/31192">调整实例配置</a>。
2. 查看当前 Mongod 上是否存在慢日志。
登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)，查看实例的慢日志，可选择抽象查询。
![img](https://staticintl.cloudcachetci.com/yehe/backend-news/ctrU959_2-en.png)
请关注 command、COLLSCAN、IXSCAN、keysExamined、docsExamined 等关键字。
  - **command** 指出慢日志中记录的操作请求。
  - **COLLSCAN** 说明该查询进行了全表扫描。
  - **IXSCAN** 代表进行了索引扫描。更多字段描述，请参见 [MongoDB 官网](https://docs.mongodb.com/manual/reference/explain-results/index.html)。
  - **keysExamined** 指明索引扫描条目。
  - **docsExamined** 代表文档扫描条目。keysExamined 和 docsExamined 越大，说明没有建索引或者索引的区分度不高。
更多慢日志说明，请参见 [MongoDB 官网](https://docs.mongodb.com/manual/reference/log-messages/index.html)。根据日志信息，分析具体原因，针对性解决问题。

## 相关参考

更多相关排查方法，请参见 [基于 DBbrain 解决 MongoDB 实例 CPU 使用率高的问题](https://www.tencentcloud.com/document/product/240/52499)。

