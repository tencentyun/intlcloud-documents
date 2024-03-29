
TDSQL-C MySQL 版计费方式支持按量计费转 Serverless。TDSQL-C MySQL 版通过后台转换集群类型来实现按量计费转 Serverless，转换后 [账单和明细](https://console.cloud.tencent.com/expense/bill/summary) 会发生变化，计费模式仍然为后付费。

>!
>- 按量计费转换 Serverless 过程中，数据库可提供访问，转换的时间点会发生闪断，建议您的应用程序配置自动重连功能。
>- 按量计费转换 Serverless 后，Serverless 实例无法转换回按量计费实例。

## 操作步骤
1. 登录 [控制台](https://console.cloud.tencent.com/cynosdb)，在实例列表选择所需实例，在**操作**列选择**更多**>**按量转Serverless**。
![](https://main.qcloudimg.com/raw/328ba1383f238d0256fc87b9f80c3a13.png)
2. 在弹出的对话框，选择所要转换 [Serverless](https://intl.cloud.tencent.com/document/product/1098/40618) 数据库的最小最大 CCU 和自动暂停时间，勾选同意规则，单击**确定**。
![](https://main.qcloudimg.com/raw/b6c11314bbe95117aa6ee79f01707069.png)
