## Overview 
For Tencent Cloud service events collected by the default Tencent Cloud service event bus, EventBridge allows you to configure message push to push Cloud Monitor events to user terminals in real time.
>! Currently, message push **can be bound only to the default Tencent Cloud service event bus**.

![](https://qcloudimg.tencent-cloud.cn/raw/2a3cd10daa2d3976fbf55a0654e0e442.png)

## Directions 
1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb), choose **Event Rule**, select the **default Tencent Cloud service event bus**, and click **Create Event Rule**.
![](https://qcloudimg.tencent-cloud.cn/raw/113a311524e5a04de86c12cda823d64e.png)
2. Set **Trigger** to **Notification message**, and set **Recipients**, **Delivery Method**, and other information as prompted.
![](https://qcloudimg.tencent-cloud.cn/raw/0307108f029b759b73feac750d4c74f3.png)


>! 
>- Use limits: For SMS message delivery, a notification message can contain up to 500 characters. For phone delivery, a notification message can contain up to 350 characters. If fields such as the instance name are too long, notification messages may fail to be sent due to excessive length. You are advised to configure multiple delivery channels at the same time.
>- Cross-MLC-border API callback may fail due to network instability. Exercise caution when selecting API callback.

## Message Push Template

```
Tencent Cloud service${Service name abbreviation}Alarm notification
Dear Tencent Cloud user,

An alarm event occurred for Tencent Cloud service ${4} under your account (ID: ${Account ID}, nickname: ${Account name}). Check and resolve the issue in time.



Alarm event: ${Event details}
Alarm service: ${Service name abbreviation}
Alarm resource: ${Resource ID}
Alarm region: ${Resource region}
Event generation time: ${Alarm time}
Event status: ${Recovered/Not recovered/Stateless}

For more details, log in to the EventBridge console.
```
