
## Overview
Machine-to-Machine (M2M) communication among different devices can be achieved by forwarding the desired message fields to another topic. You can enter the following topic information:
- **Enter a topic name**
For example, `${productId}/house_monitor/thermometer` can forward messages satisfying the rule to this topic.
- **Enter a topic name with variables**
For example, `${productId}/${house}/device`, where `house` in `${}` represents a variable name, which is the content of the field selected in the SELECT statement.

## Samples
The following sample shows how a forwarding topic with variables works. Assume that the following rule is defined:
```
SELECT temperature as t, house 
FROM house_monitor/thermometer/get 
WHERE house="tencent" AND temperature > 40
```

This rule extracts the values of the `t` and `house` fields from the message. Assume that the content of the `house` field is `tencent`.
If you define forwarding to the `house_monitor/${house}/app` topic, the rule engine will replace the `${house}` variable in this topic with `tencent` and send the values of the `t` and `house` fields to the `house_monitor/tencent/app` topic.

The entire forwarding process is as shown below:
![image](https://main.qcloudimg.com/raw/d4914e4b87c30f9240bbfcd62411be8a.png)

## Configuration
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud), select **Rule Engine** on the left sidebar, and click the rule to be configured.
2. On the rule details page, click **Add Action**.
3. In the pop-up **Add Action** window, enter relevant information and click **Save**.
 - Select "republish" as the action type.
 - Enter the name of the topic to forward to.
![](https://main.qcloudimg.com/raw/ecec657128df4e50498213fda2aaa23f.jpg)

IoT Hub will forward the reported data to this topic.

## QoS Levels of Forwarded Messages

The quality of service (QoS) level of a message will not change when it is forwarded from the source topic to another topic.
- If a message published by a device is at QoS 0, the rule engine will forward it according to QoS 0; if it is at QoS 1, the rule engine will forward it according to QoS 1.
- At QoS 0, if message forwarding fails, the system will discard the message. At QoS 1, if message forwarding fails, the system will retry forwarding the message at intervals of 3s, 6s, and 9s in sequence, and if all three retries fail, the system will store the message in the offline message queue.

