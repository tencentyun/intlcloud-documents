## Overview
The rule engine allows you to configure forwarding rules to forward eligible data reported by devices to Tencent CloudBase (TCB). You can create an environment in the [TCB console](https://console.cloud.tencent.com/tcb/env/index).

The figure shows the entire process of forwarding data to TCB by the rule engine:
![](https://qcloudimg.tencent-cloud.cn/raw/2ddc40cfa1cb52084547d270ee53cad3.jpg)

## Configuration
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and click **Rule Engine** on the left sidebar.
2. Click the rule to be configured.
3. On the rule details page, click **Add Action**.
>?You will be prompted to authorize access to TCB upon the first use. You need to click **Authorize Now** before you can proceed.
![]()
4. In the **Add Action** pop-up window, select **Forward data to Tencent CloudBase**, environment, and function and click **Save**.
![]()

>!Currently, data can be forwarded only to functions in TCB. You need to create a development environment and function in TCB before you can select them here.

## Resending Mechanism

The resending mechanism is used to send the message again in case of a failure in the message forwarding process, which makes sure that the message is received. The details are as follows:
- If message forwarding fails, the system will retry forwarding at intervals of 1s, 3s, and 10s in sequence. If all three retries fail, the message will be discarded.
- If you have configured the **Forward Error Action** item, then after three unsuccessful retries, the message will be forwarded again according to the configured action. If forwarding still fails, the message will be discarded.
