## 操作背景

由于弹性微服务需要访问其他云产品的 API，所以需要授权弹性微服务创建服务角色。

## 前提条件

[注册腾讯云账号](https://intl.cloud.tencent.com/document/product/378/17985)

>?当您注册腾讯云账号后，系统默认为您创建了一个主账号，用于快捷访问腾讯云资源。

## 操作步骤

初次使用弹性微服务，需要按照以下步骤分别为您创建 TEM_QCSLinkedRoleInAccessCluster 服务角色、TEM_QCSLinkedRoleInTEMLog 服务角色，授予您访问其他云产品资源的权限。

1. 使用**主账号**登录 [弹性微服务控制台](https://console.cloud.tencent.com/tem)。
   ![](https://qcloudimg.tencent-cloud.cn/raw/9d3dc63147c10a39be367806c0871d3f.png)
2. 单击**前往授权**， 进入 [CAM 控制台](https://console.cloud.tencent.com/cam/overview) 授权，单击**同意授权**，则为您创建 TEM_QCSLinkedRoleInAccessCluster 服务角色，授予您访问除了 CLS 外其他云产品资源的权限。
   ![](https://qcloudimg.tencent-cloud.cn/raw/bfc5e42cacfd469b62aa4e7199ff163a.png)
3. 返回 [弹性微服务控制台](https://console.cloud.tencent.com/tem)，单击**已完成授权**。
4. 在左侧导航栏单击**应用管理**，在弹出的授权窗口中单击**前往授权**， 进入 [CAM 控制台](https://console.cloud.tencent.com/cam/overview) 授权，单击**同意授权**，则为您创建 TEM_QCSLinkedRoleInTEMLog 服务角色，授予您访问 CLS 云产品资源的权限。
