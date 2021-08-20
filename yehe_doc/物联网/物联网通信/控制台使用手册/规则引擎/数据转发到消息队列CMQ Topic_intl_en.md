
## Overview
The rule engine allows you to configure rules to forward eligible data reported by devices to a CMQ topic. After you subscribe to the topic through TencentCloud API, you can receive messages pushed from the topic. The message push mechanism of the CMQ topic provides the capability to receive messages asynchronously with high reliability.

The figure below shows the entire process of forwarding data to a CMQ topic by the rule engine:
![](https://main.qcloudimg.com/raw/17177d50749d2f18c4b2f740f9f92229.png)


## Configuration
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and click **Rule Engine** on the left sidebar.
2. Go to the rule engine page and click the rule to be configured.
3. On the rule details page, click **Add Action**.
>?You will be prompted to authorize access to the CMQ topic upon the first use. You need to click **Authorize Now** before you can proceed.

4. In the **Add Action** pop-up window, select **Forward data to CMQ topic**, region, and topic and click **Save**.


## Resending Mechanism

The resending mechanism is used to send the message again in case of a failure in the message forwarding process, which makes sure that the message is received. The details are as follows:
- If message forwarding fails, the system will retry forwarding at intervals of 1s, 3s, and 10s in sequence. If all three retries fail, the message will be discarded.
- If you have configured the "action for forwarding failure", then after three unsuccessful retries, the message will be forwarded again according to the configured action. If forwarding still fails, the message will be discarded.


## Example
For more information on how to create a CMQ topic subscription through TencentCloud API, please see [Examples](https://intl.cloud.tencent.com/document/product/406/5853).

