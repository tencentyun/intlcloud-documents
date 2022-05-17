## 操作场景

Datahub 支持接入各种数据源产生的不同类型的数据，统一管理，再分发给下游的离线/在线处理平台，构建清晰的数据通道。

本文以 HTTP 数据为例介绍如何在 CKafka 控制台创建数据主动上报任务，并对任务进行修改配置，帮助您更好地了解数据接入功能。

## 操作步骤

### 创建数据接入任务

**前提条件**：已创建好目标 CKafka 实例和 Topic。


1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka)。
2. 在左侧导航栏单击**数据接入**，选择好地域后，单击**新建任务**。
3. 在弹窗中数据源类型选择**主动上报**。
   ![](https://qcloudimg.tencent-cloud.cn/raw/c323d26aa295f945b2aeac6a8c08d9b8.png)
4. 单击**下一步**，填写任务名称，选择创建好的目标 CKafka 实例和 Topic。
   ![](https://qcloudimg.tencent-cloud.cn/raw/a44723d55be51388c47616fff20f6ed0.png)
   - 任务名称：填写任务名称，只能包含字母、数字、下划线、"-"、"."。
   - CKafka 实例：选择目标 CKafka 实例。
   - 目标 CKafka Topic：选择数据投递的目标 CKafka Topic，若选择的 Topic 设置了ACL 策略，会影响功能正常使用。
   - Schema：绑定的 Schema 后，将会按该 Schema 对数据进行格式校验。若无合适的 Schema 可以单击 [新建 schema](https://console.intl.cloud.tencent.com/ckafka/datahub-schema?rid=8&createStatus=true) 跳转至新建页面。
   - QPS 限制：填写 QPS 限制。
5. 单击**提交**，任务创建成功后会生成接入点信息。
6. 复制接入点信息到 SDK 中使用，用于写入数据。

>?详细说明请参见 [数据上报 SDK](https://intl.cloud.tencent.com/document/product/597/46808)。


### 修改数据目标

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka)。
2. 在左侧导航栏单击**数据接入**，单击目标任务的 **ID**，进入任务基本信息页面。
3. 单击**数据接入模块**右上角的**更改数据目标**，修改数据接入目标。

> ?
>
> - 仅支持切换目标 CKafka Topic，不支持修改 CKafka 实例。
> - 切换 Topic 会有一定延时，新数据目标会在大约一分钟内生效。
> - 更改数据目标不会重新生成接入点。

4. 单击提交，完成数据目标修改。


### 绑定/解绑 Schema

若用户在新建任务时没有绑定 Schema，后续也可以再进行绑定。同时也支持解绑 Schema。操作路径如下：

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka)。
2. 在左侧导航栏单击**数据接入**，单击目标任务的 **ID**，进入任务基本信息页面，在基本信息模块可以绑定/解绑 Schema。


### 查看监控

1. 登录 [CKafka 控制台](https://console.intl.cloud.tencent.com/ckafka)。
2. 在左侧导航栏单击**数据接入**，单击目标任务的 **ID**，进入任务基本信息页面。
3. 选择**监控**页签，可查看目标 Topic 监控数据。


### 暂停任务

在 **[数据接入](https://console.intl.cloud.tencent.com/ckafka/datahub-access)** 页面，单击目标任务的操作栏的**暂停**，可暂停任务。

> ?当您发现数据接入任务影响了 CKafka 正常服务时，可以暂停数据接入。


### 恢复任务

在 **[数据接入](https://console.intl.cloud.tencent.com/ckafka/datahub-access)** 页面，单击目标任务的操作栏的**恢复**，可将暂停任务恢复。

> ?处于暂停状态的任务可以重新启动，将继续转储数据。


### 删除任务

在  **[数据接入](https://console.intl.cloud.tencent.com/ckafka/datahub-access)** 页面，单击目标任务的操作栏的**删除**，在二次确认弹窗中单击**确认**，可删除任务。

> ?
>
> - 删除任务表示停止数据接入并删除任务记录，不会影响到已经转储的数据和相关的 CKafka 实例。
> - 任务一旦删除不可恢复，请您谨慎操作。
