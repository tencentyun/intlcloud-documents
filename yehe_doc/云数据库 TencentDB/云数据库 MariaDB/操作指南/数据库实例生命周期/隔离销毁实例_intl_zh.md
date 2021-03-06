## 隔离实例
隔离实例即让实例无法使用（但并非销毁或删除）。实例隔离后将不可被访问，您可以在控制台恢复实例，隔离后资源空间不会被释放且保留最基本的数据副本。隔离到期后，实例彻底销毁。
- 按量计费实例：可在 [控制台](https://console.cloud.tencent.com/mariadb/instance/index) 手动退还。实例退还后，状态变为“已隔离”，保留24小时，期间实例无法访问。如您想恢复该实例，可在实例列表进行恢复。

退还后，实例的状态一旦变为“已隔离”时，就不再产生与该实例相关的费用。

>!
>- 隔离后，实例 IP 被释放，再次恢复可能无法获得原有 IP。
>- 隔离后，实例无法进行升级、修改参数、创建修改帐号、回档、修改实例名等修改操作。
>

### 操作步骤
1. 登录 [MariaDB 控制台](https://console.cloud.tencent.com/mariadb)，在实例列表选择实例，在上方选择【更多操作】>【销毁/退货】。
2. 在弹出的对话框，勾选同意，单击【确定】。
![](https://main.qcloudimg.com/raw/6fdd575dba4ca3989f946089327d1f7d.png)
返回实例列表，实例状态变为“已隔离”，隔离期间可选择【恢复/开机】实例。

## 恢复实例
恢复实例是在实例被隔离后恢复实例至正常运行的操作。恢复可能需要几分钟时间，另外，恢复实例可能会重新分配 IP，而非隔离前的 IP。

## 销毁实例
当您不需要某个实例时，可以对实例进行退还，实例退还后，状态变为“已隔离”。隔离中的实例到期后会彻底销毁。

### 注意事项
- 实例彻底销毁后数据将无法找回，请提前备份实例数据。
- 实例彻底销毁后 IP 资源将同时释放，如果该实例有相关的灾备实例，灾备实例将会断开同步连接，自动升级为主实例。
- 实例彻底销毁后，退款处理：
  - 5天无理由自助退还的金额将退还至腾讯云账户。
  - 普通自助退还的金额将按购买支付使用的现金和赠送金支付比例退还至您的腾讯云账户。
  - 推广奖励渠道订单退款将收取订单实际现金支付金额的25%作为退款手续费。 推广奖励渠道订单暂不支持自助退款，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 发起退款申请。

 
