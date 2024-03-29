

## 使用场景
假设您的组织内，因为人员的离职或变动，已经注销了腾讯云账号。腾讯云容器服务向您提供**一键清理**及**自动化清理**已注销腾讯云账号的能力。本文向您介绍如何在容器服务控制台中清除已注销腾讯云账号的 RBAC 资源对象。



## 操作原理

腾讯云用户对集群的访问由 RBAC 控制，您可以参考 [TKE Kuberentes 对象级权限控制](https://intl.cloud.tencent.com/document/product/457/37366) 获取更多信息。

## 操作步骤


### 查看已注销的腾讯云账号
若您的集群中存在已注销的腾讯云账户，您可通过如下步骤查看：
1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2/cluster)，在左侧导航栏中选择**集群**。
2. 在集群管理中，选择集群所在地域。
3. 在集群列表中，单击集群 ID，进入集群详情页。
4. 选择**授权管理 > ClusterRoleBinding** 或**授权管理 > RoleBinding**，在列表中的“账号用户名”下，已注销的腾讯云账户为红色，鼠标悬浮会提示清理相关资源对象。





### 清理失效账户
您可以通过如下步骤，快速实现**手动清理**或**自动清理**集群中已注销腾讯云账号的相关 RBAC 资源对象。


1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2/cluster)，在左侧导航栏中选择**集群**。
2. 在集群管理中，选择集群所在地域。
3. 在集群列表中，单击集群 ID，进入集群详情页。
4. 选择**授权管理 > ClusterRoleBinding** 或**授权管理 > RoleBinding**，在 “ClusterRoleBinding” 或 “RoleBinding” 管理页面中，单击右上角**清理失效账户**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/e76cfa89e3692bbd9da428a1db20478c.png)
5. 若存在未清理的已注销账号，在“清理已注销的腾讯云账号”弹窗中，单击**立即清理**。
    您也可以开启**自动化清理**，定时清理已注销账号。
	![](https://qcloudimg.tencent-cloud.cn/raw/5bfec424ce0f445de5422ab566d1907b.png)
