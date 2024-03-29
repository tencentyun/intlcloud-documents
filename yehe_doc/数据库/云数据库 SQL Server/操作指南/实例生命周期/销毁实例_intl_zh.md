## 操作场景
根据业务需求，您可以在控制台自助退还按量计费实例。
- 按量计费实例退还后，实例被移入云数据库回收站保留24小时，期间实例无法访问。如您想恢复该实例，可在回收站进行续费恢复。

自助退还后，实例的状态一旦变为**已隔离**时，就不再产生与该实例相关的费用。
>!
>- 实例销毁后数据将无法找回，备份文件会同步销毁，无法在云上进行数据恢复，请提前做好备份文件的转存。
>- 实例销毁后 IP 资源同时释放，如果该实例有相关的只读与发布订阅配置：
>  - 只读实例将同时被销毁。
>  - 实例销毁后会删除该实例上已存在的发布订阅配置。


## 操作步骤
1. 登录 [SQL Server 控制台](https://console.cloud.tencent.com/sqlserver)，在实例列表选择所需实例，在**操作**列中，选择**更多**>**销毁/退货**。
![](https://main.qcloudimg.com/raw/be837273695eb17b86447852317fb45f.png)
2. 在弹出的对话框，勾选同意，单击**销毁**。

![](https://main.qcloudimg.com/raw/eed621d2fb6827d94ab5b2875a42fc84.png)

