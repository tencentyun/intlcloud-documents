>?日志服务 CLS 为 TKE Serverless 集群产生的所有审计、事件数据提供**免费服务**至2022年9月5日。请选择自动创建日志集，或在已有日志集中选择自动创建日志主题。活动详情请参见 [TKE 容器服务审计与事件中心日志免费说明](https://intl.cloud.tencent.com/document/product/614/37889)。

## 操作场景

Kubernetes Events 包括 Kuberntes 集群的运行和各类资源调度情况，有助于维护人员日常观察资源的变更以及定位问题。TKE Serverless 集群支持为您的所有集群配置事件持久化功能，还支持使用腾讯云提供的 PAAS 服务和开源软件对事件流水进行检索。开启集群事件持久化后，TKE Serverless集群会将您的集群事件实时导出至配置的存储端。本文档指导您如何开启集群事件持久化存储，您可参考本文开始使用事件存储功能。


## 操作步骤


### 开启事件存储
1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)。
2. 在左侧导航栏中，选择**运维功能管理**，进入“功能管理”页面。
3. 在“功能管理”页面上方选择地域和集群类型“Serverless 集群”，单击需要开启事件存储的集群右侧的**设置**。如下图所示：
![](https://main.qcloudimg.com/raw/0451b3804d21152c49f9f2ada9e31356.png)
4. 在“设置功能”页面，单击事件存储**编辑**。
5. 在“事件存储”编辑页面，勾选**开启事件存储**，并配置日志集和日志主题。如下图所示：
![](https://main.qcloudimg.com/raw/9033f279626e24fed6ad1b26ad17d6b4.png)
6. 单击**确定**，即可开启事件存储。


### 更新日志集或日志主题
1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)。
2. 在左侧导航栏中，选择**运维功能管理**，进入“功能管理”页面。
3. 在“功能管理”页面上方选择地域和集群类型“Serverless 集群”，单击需要开启事件存储的集群右侧的**设置**。如下图所示
![](https://main.qcloudimg.com/raw/ee7c560a062c1849ee5cdec1800bed95.png)
4. 在“设置功能”页面，单击事件存储**编辑**。
5. 在“事件存储”编辑页面，重新选择日志集和日志主题。单击**确定**即可更新日志集和日志主题。


### 关闭事件存储
1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)。
2. 在左侧导航栏中，选择**运维功能管理**，进入“功能管理”页面。
3. 在“功能管理”页面上方选择地域和集群类型“Serverless 集群”，单击需要开启事件存储的集群右侧的**设置**。如下图所示
![](https://main.qcloudimg.com/raw/be47de0f415cfd0c4a7301194178b99f.png)
4. 在“设置功能”页面，单击事件存储**编辑**。
5. 在“事件存储”编辑页面，取消勾选**开启事件存储**。如下图所示，
![](https://main.qcloudimg.com/raw/2502c09e93dc2d150c22eb1a696a7cdb.png)
6. 单击**确定**，即可关闭事件存储。

### 在 CLS 控制台查看事件
1. 登录 [日志服务控制台](https://console.cloud.tencent.com/cls)。
2. 在左侧导航栏中，选择**检索分析**，进入“检索分析”页面。如下图所示：
![](https://main.qcloudimg.com/raw/d22f7efddfc73c53e254f5dccd39ed1a.png)
3. 选择在 [事件存储](#open) 中配置的日志集和日志主题，按需自行配置显示字段并进行检索分析，详情请参见 [日志检索分析](https://intl.cloud.tencent.com/document/product/614/37803)。
>! 当您开启事件存储时，将默认为您的 Topic 开启索引。
