>! All Ops events such as alarms and auditing events generated by Tencent Cloud services will be delivered to the Tencent Cloud service event bus, which is the default event bus and cannot be modified or deleted. You can go to the EventBridge console to bind rules and targets to the Tencent Cloud service event bus to distribute Tencent Cloud service events.

If you want to use the **Cloud Monitor events** (such as CVM kernel faults and OOM exceptions) and **CloudAudit events** (available soon) that are generated by Tencent Cloud services as event sources, you only need to activate the corresponding Tencent Cloud services, and then the Tencent Cloud services will be automatically connected to EventBridge. The events generated by Tencent Cloud services will be delivered to the **Tencent Cloud service event bus** by default. For more information, see [Tencent Cloud Service Event](https://intl.cloud.tencent.com/document/product/1108/46256).

## Directions
The following is the procedure for viewing all Tencent Cloud services (Cloud Monitor) data sources currently supported:

1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb) and choose **Tencent Cloud service event bus** > **default** to view the Tencent Cloud service events that are currently connected to the Tencent Cloud service event bus.
![](https://qcloudimg.tencent-cloud.cn/raw/f3390702fc368a8c2af977508cb3e369.png)
2. In the **Event Connector** area, you can view all Tencent Cloud services that support alarm event push.
![](https://qcloudimg.tencent-cloud.cn/raw/0a30362ed9089fd82a08b760fc3cf2c4.png)
3. You can click **Details** to view all alarm event types that are currently supported.
![](https://qcloudimg.tencent-cloud.cn/raw/21ecfd42593c59c07548b20ce96eba86.png)

## Supported Event Sources
- [Cloud Monitor Event](https://intl.cloud.tencent.com/document/product/1108/46252)
- [CloudAudit Event](https://intl.cloud.tencent.com/document/product/1021/37598)
