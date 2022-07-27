## 操作场景
腾讯云会根据您的云服务器实例前三天的负载情况，给出对应的调整实例配置建议。该建议是基于云监控采集的 CPU、内存等监控数据，进行分析后得出，您可结合实际情况决定是否调整实例配置。


## 说明事项
- 调整实例配置建议基于实例前三天的平均负载数据（每5分钟统计一次数据）得出，适用于工作负载在一段时间内比较稳定的实例，不适用于具有极短 CPU 或内存峰值的实例。
- 本功能不适用于 GPU、FPGA 等异构机型及裸金属云服务器，您可通过 [创建告警](https://intl.cloud.tencent.com/document/product/213/5179) 来主动监控实例的使用情况。
- 该建议仅供参考，如果您对监控实例使用情况有较高要求，建议使用 [云监控](https://intl.cloud.tencent.com/document/product/248/32799) 进行主动监控。

## 操作步骤
1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/instance/index?rid=1)，进入实例列表页面。
2. 在实例列表页面中，可查看实例的监控栏出现 <img src="https://main.qcloudimg.com/raw/b966dd0b540ed2caa752be60c0f99230.png" style="margin:-6px 0px" width="20px"> 警示图标，则对应实例已具有调整配置的建议。
3. 单击 <img src="https://main.qcloudimg.com/raw/b966dd0b540ed2caa752be60c0f99230.png" style="margin:-6px 0px" width="20px"> 警示图标，弹出“调整配置建议”窗口。
4. 在“调整配置建议”窗口中，可查看根据该实例使用情况所推荐的目标机型，您可勾选“显示更多推荐机型”查看其他推荐机型。
5. 若您需按照建议调整实例配置，则勾选“已阅读并同意实例调整配置费用说明”后，单击**开始调整**即可。

