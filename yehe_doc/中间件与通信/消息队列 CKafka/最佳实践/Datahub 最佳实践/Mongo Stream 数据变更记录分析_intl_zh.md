## 操作场景

MongoDB 内有 Change Stream 作为其追踪变更的解决方案，但为了更好地对变更记录进行搜索，往往需要将变更记录同步到 Elasticsearch、日志服务(CLS) 等。

![](https://qcloudimg.tencent-cloud.cn/raw/a808d4924bf5f10c029caa5f1bc7f81a.png)

本文以 MongoDB 接入 CKafka 并从 CKafka 流出到 CLS 为例，讲解如何使用 DataHub 数据转储服务实现 Mongo Stream 数据变更记录分析。

## 运行原理

MongoDB 的数据流入配置项可参见官方 [MongoDB Kafka source connector](https://docs.mongodb.com/kafka-connector/current/source-connector/)，通过设置不同的配置项，能够对接入的变更记录做相应的数据处理后再写入到 CKafka 实例的 Topic。

## 前提条件

- 需开启云数据库 MongoDB 服务或使用负载均衡 CLB 监听自建 MongoDB。
并且设置的安全组需要开放 TCP:27017 端口。
- 需开启 CKafka 服务。
- 需开启 CLS 服务。

## 操作步骤

### 步骤1：创建数据接入任务

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka)。
2. 在左侧导航栏单击**数据流入**，选择好地域后，单击**新建任务**。
3. 在弹窗中数据源类型选择 **异步拉取** > **MongoDB**。
4. 单击**下一步**，填写任务详情。
5. 单击**提交**，等待任务显示健康，即表示创建成功。
6. 当 MongoDB 数据发生变更时，可以看到选中的 CKafka 实例的 Topic 有新增的消息。

### 步骤2：创建数据流出任务

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka)。
2. 在左侧导航栏单击**数据流出**，选择好地域后，单击**新建任务**。
3. 目标类型选择**日志服务（CLS）**，单击**下一步**。
4. 填写任务详情，选取与数据接入任务相同的 CKafka 实例和 Topic，保证在消息生产后能直接进行消费。
5. 单击**提交**，等待任务显示健康，即表示创建成功。
<dx-alert infotype="explain" title="">
当任务在健康的状态时， Topic 有新增的消息写入，会直接被消费到指定的 CLS 日志主题中。
</dx-alert>



### 步骤3：查看流出数据

1. 登录 [日志服务](https://console.intl.cloud.tencent.com/cls/overview?region=ap-guangzhou) 控制台。
2. 在左侧导航栏选择**检索分析**，选择流出时填写的日志集与日志主题的“ID”，即可看到 MongoDB 的变更记录。
3. 通过关键字检索等操作，能直观得到所需要的记录。

