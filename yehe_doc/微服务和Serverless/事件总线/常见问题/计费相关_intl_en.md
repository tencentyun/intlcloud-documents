### 1. How are cloud service alarm events billed?
Cloud service alarm events are free of charge. Currently, all of them are delivered to the **Tencent Cloud service event bus** in Guangzhou region, and no fees will be charged for events in this event bus in the long run. Alarm services migrated from CM are still **free of charge**.

### 2. How are custom event buses billed?
If you create a **custom event bus**, fees will be charged by the number of events delivered to it. For billing details, see [Product Pricing](https://intl.cloud.tencent.com/document/product/1108/43288).

![](https://qcloudimg.tencent-cloud.cn/raw/739566a990aee6b8a0dd8d33f87d93c7.png)

### 3. Will fees be charged if I only create an event bus without no events delivered to it?
No. EventBridge is pay-as-you-go and only charges fees when events are delivered to event buses.

### 4. What is the logic of fee freezing?
EventBridge pushes the usage data to the billing platform hourly, and the actual bill amount is deducted daily. When a [custom event bus](https://intl.cloud.tencent.com/document/product/1108/42285) is created, 0.64 USD will be frozen and will be unfrozen and refunded after the event bus is deleted. If your account balance is less than 0.64 USD, event bus creation will fail.

### 5. Will fees be charged when a TDMQ trigger is used in SCF?
If you configure a TDMQ trigger in SCF, as the underlying layer uses EventBridge to complete triggering, fees will be charged by EventBridge according to the same billing rule.
