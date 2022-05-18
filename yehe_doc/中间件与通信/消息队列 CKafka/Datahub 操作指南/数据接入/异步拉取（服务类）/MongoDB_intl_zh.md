## 操作场景

Datahub 支持接入各种数据源产生的不同类型的数据，统一管理，再分发给下游的离线/在线处理平台，构建清晰的数据通道。

本文以 MongoDB 为例介绍如何在 CKafka 控制台创建数据异步拉取任务，并对任务进行修改配置，帮助您更好地了解数据接入功能。



## 操作步骤

### 创建数据接入任务

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka) 。
2. 在左侧导航栏单击**数据流入**，选择好地域后，单击**新建任务**。
3. 在弹窗中数据源类型选择 **异步拉取** > **MongoDB**。
   ![](https://qcloudimg.tencent-cloud.cn/raw/54de252cc0d3839df7dedf39d874c91a.png)
4. 单击**下一步**，填写任务详情。
![](https://qcloudimg.tencent-cloud.cn/raw/bc25013acab15fa51237f80ef1353828.png)
 - 任务名称：只能包含字母、数字、下划线、"-"、"."。
 - CKafka 实例：选择 CKafka 实例。
 - 目标 CKafak topic：选择数据流入的目标 CKafka topic。
 - 源数据库类型：
    - 腾讯云 MongoDB：选择数据库实例。
    - 自建 MongoDB：选择用户 CLB 实例并指定端口。
 - 用户名：源 MongoDB 的用户名。
 - 密码：源 MongoDB 的密码。
 - database：源 MongoDB 的数据库名，不支持导入 MongoDB 默认数据库数据。
 - collection：源 MongoDB 的集合，默认是监听所有即可，即”“，也可以指定某个集合。
 - 复制存量数据：是否复试源 MongoDB 的存量数据。
5. 单击**提交**，完成任务创建。

   

### 更改数据源和数据目标

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka) 。
2. 在左侧导航栏单击**数据接入**，单击目标任务的**ID**，进入任务基本信息页面。
3. 单击**数据源**模块右上角的**更改数据源**，修改数据源信息。
4. 单击**数据目标**模块右上角的**更改数据目标**，修改数据目标信息。



### 查看监控

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka) 。
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
