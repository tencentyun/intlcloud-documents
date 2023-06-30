## 问题描述
使用子账号身份登录登录腾讯云控制台操作服务网格，提示无集群权限：

![](https://qcloudimg.tencent-cloud.cn/raw/15d059a2f1c8b72642b772c685a66e35.png)



## 解决方案
当前登录的子账号无该集群 admin 权限，可参考以下集群授权方法。


### 管理员云账号自授权
如果您的主账号具备管理员权限，可直接在 [TKE 控制台](https://console.cloud.tencent.com/tke2/cluster)，使用**获取集群admin角色**功能，快速为自己的子账号授予该集群的 admin 权限，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/41702de5b18d8c74f80eb848c8df1849.png)

### 为其他子账号授权
1. 登录集群创建者的腾讯云账号（用该账号为子账号授权）。
2. 在 [TKE 控制台](https://console.cloud.tencent.com/tke2/cluster) 中选择集群。
3. 在集群详情页，单击**授权管理** > **RBAC策略生成器**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/ce0c5d4953023a33acfc357701d93d3f.png)
4. 在弹窗中勾选要授权的子账号。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/e79c0b85f0e0633df93306d67e57f40e.png)
5. 单击**完成**，授权管理员权限。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/e4e18be7944537eb7fae74c30a20e0b9.png)
