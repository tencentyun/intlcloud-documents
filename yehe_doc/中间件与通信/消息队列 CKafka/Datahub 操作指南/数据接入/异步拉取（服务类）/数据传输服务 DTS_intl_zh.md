## 操作场景

Datahub 支持接入各种数据源产生的不同类型的数据，统一管理，再分发给下游的离线/在线处理平台，构建清晰的数据通道。

本文以 DTS 数据为例介绍如何在 CKafka 控制台创建数据异步拉取任务，并对任务进行修改配置，帮助您更好地了解数据接入功能。

## 操作步骤

### 创建数据接入任务

**前提条件**
- 已创建好目标 CKafka 实例和 Topic。
- 已 [创建 DTS 实例](https://cloud.tencent.com/document/product/571/52412) 和 [消费组](https://intl.cloud.tencent.com/document/product/571/39534)。

**操作步骤**：

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka)。
2. 在左侧导航栏单击**数据流入**，选择好地域后，单击**新建任务**。
3. 在弹窗中数据源类型选择**异步拉取** > **DTS**。
   ![](https://qcloudimg.tencent-cloud.cn/raw/9e673f9ebae8fe05ee15ae2e481c8f35.png)
4. 单击**下一步**，填写任务详情。
   ![](https://qcloudimg.tencent-cloud.cn/raw/c781a56c89f41ae535d69658f8ded1eb.png)
   
   - 任务名称：只能包含字母、数字、下划线、"-"、"."。
   - CKafka 实例：选择 CKafka 实例。
   - 目标 CKafak topic：选择数据投递的目标 CKafak Topic。
   - DTS 实例：选择 DTS 实例，DTS 订阅 Topic 分区数量要与目标转储 Kafka 的 Topic 分区数量一致。
   - DTS 消费组：选择 DTS 消费组。
   - 消费者账号：DTS 消费组的账号。
   - 消费组密码：DTS 消费组的密码。
5. 单击**提交**，完成任务创建。

   

### 更改数据源和数据目标

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka)。
2. 在左侧导航栏单击**数据接入**，单击目标任务的**ID**，进入任务基本信息页面。
3. 单击**数据目标**模块右上角的**更改数据目标**，修改数据目标信息。



### 查看监控

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka)。
2. 在左侧导航栏单击**数据接入**，单击目标任务的**ID**，进入任务基本信息页面。
3. 选择**监控**页签，可查看目标 Topic 监控数据。


### 暂停任务

在 **[数据接入](https://console.intl.cloud.tencent.com/ckafka/datahub-access)** 页面，单击目标任务的操作栏的**暂停**，可暂停任务。
> ?当您发现数据接入任务影响了 CKafka 正常服务时，可以暂停数据接入。

### 恢复任务

在 **[数据接入](https://console.intl.cloud.tencent.com/ckafka/datahub-access)** 页面，单击目标任务的操作栏的**恢复**，可将暂停任务恢复。
>?处于暂停状态的任务可以重新启动，将继续转储数据。

### 删除任务

在  **[数据接入](https://console.intl.cloud.tencent.com/ckafka/datahub-access)** 页面，单击目标任务的操作栏的**删除**，在二次确认弹窗中单击**确认**，可删除任务。
> ?
> - 删除任务表示停止数据接入并删除任务记录，不会影响到已经转储的数据和相关的 CKafka 实例。
> - 任务一旦删除不可恢复，请您谨慎操作。
