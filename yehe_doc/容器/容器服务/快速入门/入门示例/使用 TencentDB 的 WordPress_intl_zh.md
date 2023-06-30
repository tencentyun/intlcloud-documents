## 操作场景
[单实例版 WordPress](https://www.tencentcloud.com/document/product/457/7205) 示例中展示了如何快速创建 WordPress 服务。通过此方式创建的 WordPress 服务特点如下：
- 数据是写到同一个容器运行的 MySQL 数据库中。
- 服务可快速启动。
- 容器因某种原因停止，数据库和存储类的文件将会丢失。

而使用 MySQL 数据库可实现数据永久存储，数据库会在实例/容器重新启动后继续存在。本文档旨在介绍如何通过云数据库 TencentD设置 MySQL 数据库，以及如何创建使用 TencentDB 的 WordPress 服务。

## 前提条件
- 已 [注册腾讯云账户](https://intl.cloud.tencent.com/account/register)。
- 已创建 TKE 标准集群。操作详情请参见 [创建集群](https://intl.cloud.tencent.com/document/product/457/30637)。
>?本文使用数据库为 [云数据库 MySQL](https://intl.cloud.tencent.com/document/product/236/5147)。
>

## 操作步骤

### 创建 WordPress 服务
#### 创建云数据库 TencentDB
1. 登录 [云数据库 MySQL 控制台](https://console.cloud.tencent.com/cdb)，单击数据库实例列表上方的**新建**。如下图所示：
![](https://main.qcloudimg.com/raw/78b43441e5d296e83e2db9246aaddff7.png)
2. 选择购买配置，详情请见 [云数据库 MySQL](https://intl.cloud.tencent.com/document/product/236/5147)。
>!云数据库所在地域与集群相同，否则无法连接该数据库。
>
3. 数据库创建成功后，可在 [MySQL-实例列表](https://console.cloud.tencent.com/cdb) 中查看。
4. 对数据库进行初始化操作，详情请参见 [初始化 MySQL 数据库](https://intl.cloud.tencent.com/document/product/236/37785)。

#### 创建使用 TencentDB 的 WordPress 服务
1. 登录容器服务控制台，选择左侧导航栏中的 **[集群](https://console.cloud.tencent.com/tke2/cluster)** 。
2. 在“集群管理”页面，选择需创建服务的集群 ID，进入集群的基本信息页面。
3. 在**工作负载 > Deployment** 页面，单击**新建**。参数详情见 [创建 Deployment](https://intl.cloud.tencent.com/document/product/457/30662)。
4. 在“新建Deployment” 页面，根据以下信息，设置工作负载基本信息。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9uSg439_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223182910.png)
 - **工作负载名**：输入要创建的工作负载的名称，本文以 wordpress 为例。
 - **描述**：填写工作负载的相关信息。
 - **标签**：本例中标签默认值为 `k8s-app = wordpress`。
 - **命名空间**：根据实际需求进行选择。
 - **数据卷**：根据实需求设置工作负载的挂载卷，详情请参见 [Volume 管理](https://intl.cloud.tencent.com/document/product/457/30678)。
5. 参考以下信息设置“实例内容器”。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/npAd465_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223183029.png)
主要参数信息如下：
  - **名称**：输入实例内容器名称，本文以 test 为例。
  - **镜像**：单击**选择镜像**，在弹框中选择**Docker Hub镜像** > **wordpress** ，并单击**确定**。
  - **镜像版本（Tag）**：使用默认值 `latest`。
  - **镜像拉取策略**：提供 Always、IfNotPresent、Never 三种策略，请按需选择，本文以**不进行设置使用默认策略**为例。
  - **环境变量**：依次输入以下配置信息：
WORDPRESS_DB_HOST = 云数据库 MySQL 的内网 IP
WORDPRESS_DB_PASSWORD = 初始化时填写的密码
6. 在“实例数量”中，根据以下信息设置服务的实例数量。本文以**手动调节**为例，实例数量设置为1。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/xJde374_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223183140.png)
7. 根据以下提示，进行工作负载的访问设置。如下图所示：   
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QStR744_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223183336.png)
 - **Service**：勾选“启用”。
 - **服务访问方式**：选择“公网LB访问”。
 - **负载均衡器**：根据实际需求进行选择。
 - **端口映射**：选择 TCP 协议，将容器端口和服务端口都设置为80 。
>!服务所在集群的安全组需要放通节点网络及容器网络，同时需要放通30000 - 32768端口，否则可能会出现容器服务无法使用问题，详情请参见 [容器服务安全组设置](https://intl.cloud.tencent.com/document/product/457/9084)。
8. 单击**创建Deployment**，完成 wordpress 服务的创建。



### 访问 WordPress 服务
可通过以下两种方式访问 WordPress 服务。

#### 通过负载均衡 IP 访问 WordPress 服务
1. 单击左侧导航栏中 **[集群](https://console.cloud.tencent.com/tke2/cluster)** ，进入“集群管理”页面。
2. 单击 WordPress 服务所在的集群 ID，选择**服务与路由** > **Service**。
3. 在 Service 列表页面，复制 WordPress 服务的负载均衡 IP，如下图所示：
![](https://main.qcloudimg.com/raw/f5f9964eacb4752e528ce32d467662a8.png)
4. 在浏览器地址栏输入负载均衡 IP，按 “**Enter**” 即可访问服务。

#### 通过服务名称访问服务
集群内的其他服务或容器可以直接通过服务名称访问。

### 验证 WordPress 服务
服务创建成功，访问服务时直接进入 WordPress 服务器的配置页。如下图所示：
![](https://main.qcloudimg.com/raw/903f45d57c58541433b555d487bd2980.png)

### 更多 WordPress 设置
若容器创建失败，可查看 [事件常见问题](https://intl.cloud.tencent.com/document/product/457/8187)。
