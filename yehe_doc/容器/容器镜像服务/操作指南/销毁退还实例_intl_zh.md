
## 操作场景
本文档介绍如何在腾讯云容器镜像服务 TCR 中销毁、退还企业版实例。

## 前提条件
已成功 [购买企业版实例](https://intl.cloud.tencent.com/document/product/1051/39088)，且当前操作账号具有该实例的删除权限。


## 操作步骤
1. 登录 [容器镜像服务控制台](https://console.cloud.tencent.com/tcr/instance?rid=1)。
2. 单击左侧导航栏中的**实例管理**，进入“实例管理”页面。
3. 选择需要销毁/退还的实例右侧的**更多**>**销毁/退还**。
4. 在弹出的确认窗口中，按需勾选“随实例删除关联的 COS 存储桶”。如下图所示：
![](https://main.qcloudimg.com/raw/d6dbb8b3a6765d8372b51ce55dd5a8f6.png)
<dx-alert infotype="notice" title="">
- 请仔细阅读销毁/退还实例的相关提示。实例删除将彻底清理实例使用过程中存储的用户数据及相关配置，且不可恢复，请谨慎操作。
- 如果确认不再需要使用容器镜像服务企业版过程中存储的容器镜像、Helm Chart 等底层数据，请勾选随实例删除后端存储 COS Bucket，避免产生不必要费用。
- 如果当前账户已处于欠费状态，对象存储服务不允许直接删除关联 COS Bucket，请不要勾选该选项，正常删除实例后前往 [对象存储](https://console.cloud.tencent.com/cos) 控制台管理该 COS Bucket。
- 实例销毁后，按量计费实例将不再继续产生费用。
</dx-alert>
5. 勾选“已阅读并同意退费规则”后单击**确定**即可删除当前所选实例，该实例将不再产生费用。
<dx-alert infotype="explain" title="">
若实例删除花费时间过长，或显示状态为异常，您可 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们。
</dx-alert>



## 相关文档

您还可以使用 DeleteInstance 接口删除实例。详细信息请参见 删除实例 API 文档。
