This document introduces the solution for the problem where the CVM is disconnected with the internet and cannot be logged in.

## Fault symptoms
The CVM may have been isolated because it violated the requirements of current laws and regulations. You can use the following methods to check whether the CVM is isolated.
- When a CVM is isolated from the public network, you will be notified of isolation due to violation or regulations through an [internal message in the console](https://console.cloud.tencent.com/message) or a text message.

<!--
 - Internal message:
![](//mc.qcloudimg.com/static/img/3c8ecd4ac301180e3632a25343be0697/image.png)
Or
![](//mc.qcloudimg.com/static/img/cd3fbf748d3ff61adf3d2198853d18de/image.png)
 - SMS:
![](//mc.qcloudimg.com/static/img/afaff154fa12695844055422f4f103e6/image.png)
- The **Monitor/Status** bar in the [CVM Console](https://console.cloud.tencent.com/cvm/index) displays the status of the CVM: Isolated.
-->

## Cause of the Problem
When a regulation violation or risk event occurs for a CVM, the offending machine will be partially isolated (except for the private network login port 22, 36000, and 3389, other network access is isolated. Developers can use a jump server to log in to the server.
For details, see Cloud Security Violation Levels Classification and Penalties Description.

## Solution

 1. Delete the violating content as instructed by internal message or the text message. Resolve security risks and reinstall the system if necessary.
 2. If it is not your own action that leads to the violation, then your CVM may have been subject to malicious intrusion. To resolve this, see [Host Security](https://intl.cloud.tencent.com/document/product/296).
 3. After resolving security risks and deleting violating content, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=7&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM) to contact customer service to remove the isolation.

