CVM may be blocked and isolated due to security violations (content or behavior violations) or DDoS attacks. This document describes how to solve the problem of login failure due to CVM isolation caused by security violations.

## Problems
The CVM isolation may be brought by violations of applicable laws and regulations. You can check whether the CVM is isolated in the following ways.
- When a CVM is isolated from the public network, you will be notified of the isolation via an [internal message in the console](https://console.cloud.tencent.com/message) or a text message.
 - The **Monitoring/Status** tab in the [CVM Console](https://console.intl.cloud.tencent.com/cvm/instance/index) displays the status of the CVM: Isolated.


## Causes
When a CVM is involved in a violation event or risk event, it will be partially isolated (except for the private network login interfaces 22, 36000, and 3389, all other network access is isolated, and the developers can log in to the CVM through a jump server).

## Solutions

 1. Delete the violating content as instructed by the internal message or text message. Resolve security risks and reinstall the system if necessary.
 2. If the violation is not caused by your own action, your CVM may have encountered malicious intrusion. To resolve this, see [Host Security](https://intl.cloud.tencent.com/zh/document/product/296).
 3. After eliminating potential safety hazards or stopping violations, please [submit a ticket](https://console.intl.cloud.Tencent.com/workorder) 
to contact customer service for removing the isolation.



