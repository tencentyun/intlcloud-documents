本文档将指导您如何为镜像安全事件和运行时安全事件配置告警策略。

## 前提条件
请确认消息订阅中“安全消息-安全事件通知”已打开，单击 [进入设置](https://console.cloud.tencent.com/message/subscription)。

## 事件类型
告警设置中事件类型、默认告警时间和告警如列表所示： 

| 事件类型 | 默认告警时间 | 默认告警项             |
| -------- | ------------ | ---------------------- |
| 安全漏洞 | 全天         | 严重                   |
| 木马病毒 | 全天         | 严重、高危、中危、低危 |
| 敏感信息 | 全天         | 严重、高危、中危、低危 |
| 容器逃逸 | 全天         | -                      |
| 异常进程 | 全天         | 拦截失败、告警         |
| 文件篡改 | 全天         | 拦截失败、告警         |
| 反弹 Shell | 全天         | -         |
| 文件查杀| 全天         | -         |

## 操作步骤
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**告警设置**。
2. 在告警设置页面，单击开启“告警状态”，开启告警设置模式。
![](https://qcloudimg.tencent-cloud.cn/raw/c0217985d748ca8aaeaa1dc08258fde4.png)
3. 开启告警设置模式后，告警时间可以单击![](https://main.qcloudimg.com/raw/f03c476d56766d47f8a37addc74c7d6b.png)图标选择全体或自定义时间。
 - 单击全天左侧![](https://main.qcloudimg.com/raw/f03c476d56766d47f8a37addc74c7d6b.png)图标，即可完成全天告警通知设置。
![](https://qcloudimg.tencent-cloud.cn/raw/3a3547a30818061f1bfa8001901ca776.png) 
 - 单击自定义时间框左侧![](https://main.qcloudimg.com/raw/f03c476d56766d47f8a37addc74c7d6b.png)图标，按需选择开始时间和结束时间后，单击**确定**，即可完成自定义时间通知设置。
![](https://qcloudimg.tencent-cloud.cn/raw/088b19e7691915ae7eb4af20543cda59.png)
