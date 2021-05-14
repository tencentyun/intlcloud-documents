### 云服务器无监控数据。
云服务器无监控数据主要有五大原因：
- 未安装监控 Agent 或未启动 Agent。
- 无法解析数据上报域名。
- Agent 获取 uuid 错误。
- 云服务器重启或关机。
- 云服务器高负载。

如需排查具体原因请参见 [云服务器无监控数据排查文档](https://intl.cloud.tencent.com/document/product/248/36208)。

### 如何创建云监控告警策略？
1. 登录 [云监控控制台](https://console.cloud.tencent.com/monitor)。
2. 单击【告警配置】>【告警策略】，进入告警策略配置页面。
3. 单击【新增】，即可配置告警策略。

具体配置说明参见 [创建告警策略](https://intl.cloud.tencent.com/document/product/248/38916)。

### 云监控如何拉取监控数据？
云监控支持通过 [GetMonitorData 接口](https://intl.cloud.tencent.com/document/product/248/39306) 获取云产品监控数据。
具体步骤可参见最佳实践- [使用 API 拉取云产品监控数据](https://intl.cloud.tencent.com/document/product/248/39917)。

### 云监控快速创建Dashboard
请参见 [快速创建Dashboard](https://intl.cloud.tencent.com/document/product/248/35282)。



### 云监控未收到告警
未收到告警主要有五大原因：
- 告警策略未启用。
- 短信配额不足。
- 未配置或未验证报告通知渠道。
- 接收组未配置用户。
- 未达到告警触发条件。

如需排查具体原因，请参见 [未收到告警排查文档](https://intl.cloud.tencent.com/document/product/248/38297)。

### 云监控如何新建接收人/组

告警接收人/组决定了哪些用户能够接收到告警信息。您也可以把关心相同告警的人聚合到一个组，触发告警时，组内的人员都会收到相应的告警。详情请参见 [告警接收人/组](https://intl.cloud.tencent.com/document/product/248/38921)。

### 云服务器Ping不可达
如收到云服务器 “ping 不可达” 事件告警通知，您可以点击参见 [排查步骤](https://intl.cloud.tencent.com/document/product/248/36205)  恢复告警，如告警通知打扰到您可以点击参见 [关闭告警功能](https://intl.cloud.tencent.com/document/product/248/36205)。

详情可点击查看 [云服务器Ping不可达排查文档](https://intl.cloud.tencent.com/document/product/248/36205)。
