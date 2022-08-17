在使用腾讯云服务网格（Tencnet Cloud Mesh，TCM）的过程中，涉及到服务网格相关云资源的使用，为了您能正常使用 TCM 的功能，您需要对 TCM 的服务角色 `TCM_QCSRole` 进行授权，授权后，TCM 服务才能使用相关云资源。

需要服务授权的场景主要包含 [首次登录 服务网格控制台](#TCMRole) 以及 [首次使用 TCM 一键体验功能](#TCMRoleInSample) 两个场景，分别对应 ` QcloudAccessForTCMRole ` 和 ` QcloudAccessForTCMRoleInSampleDeployment ` 两个预设策略。



## 首次登录服务网格控制台[](id:TCMRole)

### 授权场景

当您已注册并登录腾讯云账号后，首次登录 [服务网格控制台](https://console.cloud.tencent.com/tke2/mesh) 时，需前往**访问管理**页面对当前账号授予腾讯云服务网格操作容器服务（TKE）、SSL证书（SSL）、日志服务（CLS）等云资源的权限。该权限授予通过关联预设策略 ` QcloudAccessForTCMRole ` 至 TCM 服务角色 `TCM_QCSRole` 完成。如您之前未创建过 TCM 服务角色，该授权流程还会涉及 TCM 服务角色的创建。

### 授权步骤

1. 首次登录 [服务网格控制台](https://console.cloud.tencent.com/tke2/mesh)，自动弹出**服务授权**窗口。
![](https://qcloudimg.tencent-cloud.cn/raw/960f945bce9253063b8f6ff8d5c32e62.png)
2. 单击**前往访问管理**，进入 CAM 控制台服务授权页面。
3. 单击**同意授权**，完成身份验证后即可成功授权。
![](https://qcloudimg.tencent-cloud.cn/raw/c064ec50986682f70eacb39b4cd51097.png)

### 权限内容

**容器服务（TKE）相关**

| 权限 | 描述 | 资源 |
| :-------- | :--------| :------ |
| DescribeClusterSecurity |  查询集群密钥 | 所有资源 `*` |

 **SSL 证书（SSL）相关**

| 权限 | 描述 | 资源 |
| :-------- | :--------| :------ |
| DescribeCertificateDetail | 获取证书详情 | 所有资源 `*` |

 **日志服务（CLS）相关**

| 权限 | 描述 | 资源 |
| :-------- | :--------| :------ |
| getLogset | 获取日志集详情 | 所有资源 ` * ` |
| getTopic | 获取日志主题详情 | 所有资源 ` * ` |
| createLogset | 创建日志集 | 所有资源 ` * ` |
| createTopic | 创建日志主题 | 所有资源 ` * ` |
| modifyIndex | 修改索引 | 所有资源 ` * ` |
| listLogset | 获取日志集列表 | 所有资源 ` * ` |
| listTopic | 获取日志主题列表 | 所有资源 ` * ` |


