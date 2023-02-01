## 操作场景
您可以通过 [云监控](https://console.cloud.tencent.com/monitor/myalarm) 对云函数配置告警策略，对函数运行状态进行监控。
目前云函数可以配置告警的监控指标有运行时间、调用次数、错误次数等。全部支持列表请参考 [监控指标说明](https://intl.cloud.tencent.com/document/product/583/32739)。同时，告警支持选择接收告警的用户组，选择接收邮件、短信、微信等方式的告警渠道。

## 操作步骤

1. 登录 [Serverless 控制台](https://console.cloud.tencent.com/scf)，选择左侧导航栏中的**函数服务**。
2. 在“函数服务”列表页，单击函数名称，进入函数详情页。
3. 选择左侧“监控信息”，在监控信息详情页单击**设置告警**。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/mNL2280_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219161556.png)
4. 在“新建告警策略”页面，配置告警策略，配置说明如下：
	- **策略名称**：自定义。
	- **监控类型**：选择 “云产品监控”。
	- **策略类型**：支持选择“云函数/版本”或“云函数/别名”。
	- **告警对象**：根据实际需求进行设置。若选择 “实例 ID”，其默认地域设置为广州。在不同的地域下，可以查看到相应的函数，请选择需要适用告警策略的函数。
	更加详细的告警策略配置，请参考 [云监控 > 新建告警策略](https://intl.cloud.tencent.com/document/product/248/38916)。
5. 单击**完成**。在**告警管理 > [策略管理](https://console.cloud.tencent.com/monitor/alarm2/policy)** 中，查看到已配置好的策略。并可根据实际需求，随时选择启停。

