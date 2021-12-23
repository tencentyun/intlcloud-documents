## 操作场景

该任务指导您通过 TDMQ 控制台创建集群、Vhost、Exchange 和 Queue 等资源，了解运行一个客户端之前，控制台所需要进行的操作。

## 前提条件

已 [注册腾讯云账号](https://intl.cloud.tencent.com/document/product/378/17985)。

## 操作步骤

### 步骤1：新建集群

1. 登录 [TDMQ 控制台](https://console.cloud.tencent.com/tdmq)，进入**集群管理**页面，选择目标地域。
2. 单击**新建集群**，填写集群名称和说明。
3. 单击**提交**，完成集群创建。
   ![](https://qcloudimg.tencent-cloud.cn/raw/6f32ba4d48604459759c3e234cafb7e0.png)
4. 在集群列表页面，单击刚刚创建好的集群作栏的**接入地址**，得到服务端的连接信息。
![](https://qcloudimg.tencent-cloud.cn/raw/27d49fe8aef1e4f9401ff17e35d6a56f.png)

### 步骤2：创建 Vhost

1. 在集群列表页面，单击刚刚创建好的集群 ID，进入集群基本信息页。
2. 选择顶部的 **Vhost** 页签，单击**新建**，填写 Vhost 相关信息。
   - Vhost 名称：设置 Vhost 的名称（创建后不可修改），3-64个字符，只能包含字母、数字、“-”及“_”
   - 消息 TTL：设置未消费消息的保留时间，过期未 ACK（确认消息） 则自动删除，范围：60秒-15天
   - 说明：Vhost 的备注说明
3. 单击**提交**，完成 Vhost 创建。
   ![](https://qcloudimg.tencent-cloud.cn/raw/e6dd389c40c696a4e81f571d38b41655.png)

### 步骤3：创建角色并授权

1. 在 [TDMQ 控制台](https://console.cloud.tencent.com/tdmq) 左侧导航栏选择**角色管理**，单击**新建**，创建一个角色。
2. 在**集群管理**页面，单击刚刚创建好的集群的“ID”，进入**集群**详情页面。
3.在页面上方选择 **Vhost** 页签，找到刚刚创建的 Vhost，单击操作栏的**配置权限**。
4. 在**配置权限**页面，单击**新建**，为刚刚创建的角色添加生产消费权限。
<img src="https://qcloudimg.tencent-cloud.cn/raw/27f5ba2394ed0306e82310fb344321a7.png" width="535">


### 步骤4：创建 Exchange

1. 在 Vhost 列表页，选择顶部的 **Exchange** 页签，进入 Exchange 列表页。
2. 选择刚刚创建好的 Vhost，单击**新建**，填写 Exchange 名称和说明，选择路由类型。
   - Direct：该类型 Exchange 会把消息路由到 RoutingKey 和 BindingKey 完全匹配的 Queue 中。
   - Fanout：该类型 Exchange 会将消息路由到所有与其绑定的 Queue 中。
   - Topic：该类型 Exchange 支持多条件匹配和模糊匹配，即使用 Routing Key 模式匹配和字符串比较的方式将消息路由至与其绑定的 Queue 中。
3. 单击**提交**，完成 Exchage 创建。
   ![](https://qcloudimg.tencent-cloud.cn/raw/f1c98dd23bceef637c707c846f359d14.png)

### 步骤5：创建 Queue

1. 在 Exchange 列表页，选择顶部的 **Queue** 页签，进入 Queue 列表页。
2. 选择刚刚创建好的 Vhost，单击**新建**，填写 Queue 名称和说明。
3. 单击**提交**，完成 Queue 创建。
   ![](https://qcloudimg.tencent-cloud.cn/raw/fb820128e02ce7f7a79fb0ab2285fee8.png)

### 步骤6：创建路由关系

1. 在 Queue 列表页，选择顶部的**路由关系**页签，进入路由关系列表页。
2. 选择刚刚创建好的 Vhost，单击**新建**。
   源 Exchange 选择刚刚创建的 Exchange，绑定类型选择 Queue，绑定目标选择刚刚创建好的 Queue。
3. 单击**提交**，完成路由关系绑定。
   ![](https://qcloudimg.tencent-cloud.cn/raw/e5614e3c31c35f170e3f59f36c3c6a86.png)
