
本文档将为您介绍，当入侵防御误报，导致大量异常拦截，或因策略变更有误，导致流量出现异常下跌情况时，需要如何处理。
## 现象描述
IP 地址出现入侵防御误报导致的大量异常拦截，或因策略变更有误，导致流量出现异常下跌。
## 解决思路
当确认拦截的来源是云防火墙后，可以先止损（如关闭拦截功能）、再排查、最后交由产品安全团队人工处理。
## 处理步骤
### [步骤1：关闭拦截功能](id:step1)

1. 登录 [云防火墙控制台](https://console.cloud.tencent.com/cfw/ips)，在左侧导航中，单击**入侵防御**。
2. 在入侵防御页面，将防护模式切换为**观察模式**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/8aefe20482d102a10ce06bfffe899f3c.png" style="zoom:67%;" />
3. 在拦截列表上方，关闭”启用拦截列表“的功能开关。
![](https://qcloudimg.tencent-cloud.cn/raw/01276741e02f666c36e8cd4c17817c3a.png)

### 步骤2：手动处置
1. 登录 [云防火墙控制台](https://console.cloud.tencent.com/cfw/warncenter)，在左侧导航栏中，单击**告警中心**，进入告警中心页面。
2. 在告警中心页面，选择**阻断拦截统计** > **入站方向**。
3. 在入站方向页签内容，选择**按拦截统计排序**，找到误拦截的 IP。
![](https://qcloudimg.tencent-cloud.cn/raw/adbaf7841559056429298135b27b3150.png)
4. 将误拦截 IP 加入白名单。
	- **方式1**：在误拦截 IP 右侧，单击**放通**，可将 IP 地址加入到白名单（忽略列表），放行该 IP 的后续访问。
	- **方式2**：在 [入侵防御](https://console.cloud.tencent.com/cfw/ips) 页面，选择**忽略列表** > **添加地址**，将误报的 IP 地址批量加入到白名单。
	![](https://qcloudimg.tencent-cloud.cn/raw/ab8be2bcc5dc6bfb54401c616fdfc29e.png)
5. 处理完成后，恢复 [步骤1](#id:step1) 的配置，观察流量是否正常。

### 步骤3：提交工单反馈误报

1. 若手动处置完毕，仍存在流量异常，可进入 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=1290&source=0&data_title=T-Sec-%E4%BA%91%E9%98%B2%E7%81%AB%E5%A2%99&level3_id=1323&queue=3233&scene_code=36970&step=2) 页面，提供 AppID 与误报的 IP 地址给安全团队确认。
2. 安全团队收到反馈后，会在规定时间内快速响应，调整检测规则。
