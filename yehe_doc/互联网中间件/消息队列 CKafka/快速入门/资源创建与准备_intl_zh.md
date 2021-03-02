## 操作场景


该任务指导您通过 CKafka 控制台创建实例和 Topic，快速了解 CKafka 控制台操作流程。

## 前提条件

- 已 [注册腾讯云账号](https://intl.cloud.tencent.com/document/product/378/17985)。
- 已 [购买云服务器](https://buy.cloud.tencent.com/cvm)。

## 操作步骤

### 步骤1：创建实例并添加公网路由

1. 登录 [CKafka 控制台](https://console.cloud.tencent.com/ckafka) 。
2. 在左侧导航栏单击【实例列表】，单击【新建】进入实例购买页，根据自身业务需求选择购买信息。
   ![](https://main.qcloudimg.com/raw/ec7c52c012f1cf71940f9993921b0748.png)

   >?
   >- 选择私有网络时建议选择一个和已有 CVM 一致的私有网络，这样不需要额外添加路由即可连接到 Kafka 服务。
   >- 如果私有网络与您所持有的 CVM 或者其他资源不在同一网络中，可以单击接入方式的 [添加路由策略](https://intl.cloud.tencent.com/document/product/597/32555) 添加路由。
   >- 如果您需要使用公网访问，可以单击接入方式的 [添加路由策略](https://intl.cloud.tencent.com/document/product/597/32555) 开通一条公网路由，公网访问必须对 Topic 进行 ACL 策略的设置（本文以公网访问为例）。

3. 单击【购买】，大约等待3～5分钟即可在实例列表页看到创建好的实例。
   ![](https://main.qcloudimg.com/raw/b8540b7589f70a40b8ad3ab7fac91f86.png)

4. 单击实例的“ID/名称”，进入实例详情页，选择【接入方式】模块中的【添加路由策略】，新增一条公网路由。
   ![](https://main.qcloudimg.com/raw/39733cf43129ef52cb707e4e564eed6c.png)

添加后可获得公网访问的域名与端口。
![](https://main.qcloudimg.com/raw/afc2a197f4e0646f40aa6280c5f6414d.png)


### 步骤2：创建 Topic 并配置 ACL 策略

1. 在实例详情页，选择【Topic 管理】，单击【新建】，填写名称等信息，选择分区数和副本数，创建一个topic。
	 ![](https://main.qcloudimg.com/raw/8451c29a64cc1eed19bebb6ba2d6f939.png)

2. 在实例详情页，选择【用户管理】，单击【新建】，添加一个用户，设置好用户名和密码。
	 ![](https://main.qcloudimg.com/raw/bf56ee0f3f53dda9ce9c0619a5c05cbc.png)

3. 在【ACL策略管理】页面，选择刚刚创建好的topic，单击操作列的【编辑ACL策略】，新增 ACL 策略。
   ![](https://main.qcloudimg.com/raw/88b8f12af12c42640bc4e02a485e167f.png)
