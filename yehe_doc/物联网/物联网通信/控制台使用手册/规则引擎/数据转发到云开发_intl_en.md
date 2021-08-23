## Overview
The rule engine allows you to configure forwarding rules to forward eligible data reported by devices to TCB. You can create an environment in the [TCB console](https://console.cloud.tencent.com/tcb/env/index). For detailed directions, please see Creating Environment.

The figure below shows the entire process of forwarding data to TCB by the rule engine:
![](https://main.qcloudimg.com/raw/9d5dbcde287f620b1e3121dc0bdc26a7.png)

## Configuration
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and click **Rule Engine** on the left sidebar.
2. Go to the rule engine page and click the rule to be configured.
3. On the rule details page, click **Add Action**.
>?You will be prompted to authorize access to TCB upon the first use. You need to click **Authorize Now** before you can proceed.
![](https://main.qcloudimg.com/raw/f5c5f9efe32682543843e1242eb42b7e.png)
4. In the **Add Action** pop-up window, select **Forward data to Tencent CloudBase**, environment, and function and click **Save**.


>!Currently, data can be forwarded only to functions in TCB. You need to create a development environment and function in TCB before you can select them here.

## Resending Mechanism

The resending mechanism is used to send the message again in case of a failure in the message forwarding process, which makes sure that the message is received. The details are as follows:
- If message forwarding fails, the system will retry forwarding at intervals of 1s, 3s, and 10s in sequence. If all three retries fail, the message will be discarded.
- If you have configured the "action for forwarding failure", then after three unsuccessful retries, the message will be forwarded again according to the configured action. If forwarding still fails, the message will be discarded.
