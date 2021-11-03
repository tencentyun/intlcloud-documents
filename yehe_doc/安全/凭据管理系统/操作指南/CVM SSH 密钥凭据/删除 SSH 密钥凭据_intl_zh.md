本文档将指导您如何在凭据管理系统控制台中删除 CVM SSH 密钥。

## 前提条件
- 已创建 [CVM SSH 密钥的凭据](https://intl.cloud.tencent.com/document/product/1078/42683)。 
- 对凭据进行删除操作之前，需要对凭据进行禁用操作。
- 待删除的凭据未绑定实例。
>? 如果待删除的凭据已绑定实例，您需要在对应的实例中先解除绑定，然后再进行删除操作。

## 操作步骤
1. 登录 [凭据管理系统](https://console.cloud.tencent.com/ssm) 控制台，在左侧导航栏中，单击 **CVM SSH 密钥管理**，进入 CVM SSH 密钥页面。
   ![](https://qcloudimg.tencent-cloud.cn/raw/6dc101c473746a93db5e8484906f7649.png)
2. 在 CVM SSH 密钥页面中，单击左上角的“区域下拉框”，切换区域。
   ![](https://qcloudimg.tencent-cloud.cn/raw/2cf5ca140fb4b47aae8bbc8fc5f227be.png)
3. 在 CVM SSH 密钥页面中，单击搜索框，可通过“标签和凭据名称”等关键字对凭据进行查找。
![](https://qcloudimg.tencent-cloud.cn/raw/2683c5fec852e996db5f26a2f8bd3f13.png)
4. 在筛选结果列表中，选择需要删除的凭据，在凭据的右侧操作栏中单击【删除】。
![](https://qcloudimg.tencent-cloud.cn/raw/eb5f3828f2ea838dad5a6d949b3e3b21.png)
5. 在删除界面中，可根据实际需求选择 **只删除 SSM 存储的 SSH 密钥** 或**同时删除 SSM 和 CVM 存储的密钥**后，单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/d55efe86b592e95d417ffb1b70ce08fd.png)
