This document describes how to resolve login failures if the CVM is isolated from the public network.

## Problems
The CVM may have been isolated because it violates current laws and regulations. You can use the following methods to check whether the CVM is isolated.
- When a CVM is isolated from the public network, you will be notified of the isolation via an [internal message in the console](https://console.cloud.tencent.com/message) or a text message.

- The **Monitoring/Status** tab in the [CVM Console](https://console.cloud.tencent.com/cvm/index) displays the status of the CVM: Isolated.

## Causes
When a regulation violation or risk event occurs for a CVM, the offending machine will be partially isolated (except for the private network login port 22, 36000, and 3389, all network access will be isolated. Developers can use a jump server to log in to the server.
For details, see Cloud Security Violation Levels Classification and Penalties Description.

## Solutions

 1. Delete the violating content as instructed by the internal message or text message. Resolve security risks and reinstall the system if necessary.
 2. If the violation is not caused by your own action, your CVM may have encountered malicious intrusion. To resolve this, see [Host Security](https://intl.cloud.tencent.com/document/product/296).
 3. After resolving security risks and deleting violating content, you can [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to contact customer service to remove the isolation.

