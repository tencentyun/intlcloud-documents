By using an event rule, you can deliver collected events to the specified delivery target for processing and consumption. Currently, EventBridge allows you to set [CKafka](https://www.tencentcloud.com/products/ckafka) as a delivery target to enable direct event consumption in downstream systems.

## Configuration Methods
1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb) and select a specified event bus.
2. On the event bus details page, click **Manage Event Rules** and configure a new rule as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/f05a63feb28020050c800c14fb964e3d.png)
3. Go to the **Event Rule** page and click **Create Event Rule**.
4. Enter information as instructed. When binding a delivery target, select **CMQ (Kafka)** and bind a CKafka instance and topic as instructed.
![](https://qcloudimg.tencent-cloud.cn/raw/549c9b3c745f6aadda2e43e1767819a1.png)
5. Click **Complete**. Then you can view the created event rule on the event rule list page.
>! If the upstream event source of the event bus is also CKafka, make sure that the target bound CKafka topic is different from the event source topic. Otherwise infinite recursion may occur and cause significant expense.

### Delivering events
EventBridge automatically parses the CloudEvent field and delivers the whole event content to specified CKafka topics.
