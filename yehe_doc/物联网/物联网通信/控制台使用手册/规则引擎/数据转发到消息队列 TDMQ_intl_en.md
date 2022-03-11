## Overview

The rule engine allows you to configure rules to forward eligible data reported by devices to the message queue TDMQ topic. After subscribing to a TDMQ topic through TencentCloud API, you can receive messages pushed from the topic. The message push mechanism of the TDMQ topic provides the capability to receive messages asynchronously with high reliability.

The following graph shows the entire process of forwarding data to a TDMQ topic by the rule engine:
2. ![]()

## Configuration

1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and click **Rule Engine** on the left sidebar.
2. Click the rule to be configured.
3. On the rule details page, click **Add Action**.
> ? You will be prompted to authorize access to the TDMQ topic if this is your first time using the rule engine. Click **Authorize Now** and continue to create.
> ![]()
4. In the **Add Action** pop-up window, select **Forward data to TDMQ**, region, and topic and click **Save**.
![]()

## Resending Mechanism

The resending mechanism is used to send the message again in case of a failure in the message forwarding process, which makes sure that the message is received. The details are as follows:

- If message forwarding fails, the system will retry forwarding at intervals of 1s, 3s, and 10s in sequence. If all three retries fail, the message will be discarded.
- If you have configured the "action for forwarding failure", then after three unsuccessful retries, the message will be forwarded again according to the configured action. If forwarding still fails, the message will be discarded.



