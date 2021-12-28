## 操作场景

该任务指导您通过 TDMQ 控制台创建集群和 Topic 等资源，了解运行一个客户端之前，控制台所需要进行的操作。

## 前提条件

已 [注册腾讯云账号](https://intl.cloud.tencent.com/document/product/378/17985)。

## 操作步骤

### 步骤1：新建集群

1. 登录 [TDMQ 控制台](https://console.cloud.tencent.com/tdmq)，进入**集群管理**页面，选择目标地域。
2. 单击**新建集群**，创建一个集群。
   ![](https://qcloudimg.tencent-cloud.cn/raw/cdb9f5bf094541056fa892d9da76ca96.png)
3. 在集群列表页面，单击创建好的集群操作栏的**接入地址**，得到服务端的连接信息。
   ![](https://qcloudimg.tencent-cloud.cn/raw/77687fcea3acf00e964918980a3b60f3.png)

### 步骤2：创建命名空间

1. 在集群列表页面，单击步骤1创建好的“集群ID”，进入集群基本信息页。
2. 选择顶部的**命名空间**页签，单击**新建**，创建一个命名空间。
   ![](https://qcloudimg.tencent-cloud.cn/raw/5a1fdfd089497eced11a3de69e1ca651.png)

### 步骤3：创建角色并授权

1. 在左侧导航栏选择**角色管理**，单击**新建**，创建一个角色。
2. 在**集群管理**页面，单击刚刚创建好的集群的“ID”，进入**集群**详情页面。
3. 在页面上方选择**命名空间**页签，找到刚刚创建的命名空间，单击操作栏的**配置权限**。
4. 在**配置权限**页面，单击**新建**，为刚刚创建的角色添加生产消费权限。
   ![img](https://qcloudimg.tencent-cloud.cn/raw/aea0918d1f2e54ed0ca5f10ab2a94574.png)

### 步骤4：创建 Topic

1. 在命名空间列表页，选择顶部的**Topic**页签，进入 Topic 列表页。
2. 选择步骤3创建好的命名空间，单击**新建**，创建一个 Topic。
   ![](https://qcloudimg.tencent-cloud.cn/raw/050d76fe792a2e3609d87c15e5862ca7.png)

### 步骤5：创建 Group

1. 在 Topic 列表页，选择顶部的 **Group** 页签，进入 Group 列表页。
2. 选择刚刚创建好的命名空间，单击**新建**，创建一个 Group。
   ![](https://qcloudimg.tencent-cloud.cn/raw/abfb914dfe9819ef247ef84cc84551fd.png)
