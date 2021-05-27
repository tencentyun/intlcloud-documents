## Scenario
The instance can be shut down when you need to stop the service, or modify configurations that can be done only in the shutdown state. Shutting down an instance is like shutting down a local computer.

## Notes

- You can shut down an instance using system commands (such as the shutdown command under Windows system and Linux system) or through the Tencent Cloud console. We recommend you view the shutdown process on the console to check whether any problem occurs.
- The instance will no longer provide services after the shutdown. Before the shutdown, make sure the CVM has stopped receiving service requests.
- During the shutdown, the status of the instance will change from "shutting down" to "shutdown". If the shutdown process takes too long, there may be an exception. For more information, please see [Close an CVM](https://intl.cloud.tencent.com/document/product/213/2917) to avoid forced shutdown.
- After an instance is shut down, all storage is still connected to the instance, and all disk data are retained. Data in the memory will be lost.
- Shutting down an instance does not change its physical attributes. The public and private IPs of the instance remain unchanged. [Elastic Public IP](https://intl.cloud.tencent.com/document/product/213/5733) is still bound to the instance. Due to service interruption, however, you will receive an error response when accessing these IPs. [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807) relationship remains unchanged.
- If the instance belongs to the [real server cluster](https://intl.cloud.tencent.com/document/product/214/32388) of the CLB instance, it can no longer provide services after the shutdown.
If the health check policy has been configured, the instance that has been shut down will be automatically blocked and requests will no longer be forwarded to it. Otherwise, the client may receive a 502 error code. For more information, please see [Health Check](https://intl.cloud.tencent.com/document/product/214/38451).
- If the instance that has been shut down is in an [auto scaling group](https://intl.cloud.tencent.com/document/product/377/3590), the auto scaling service will mark the instance as having poor performance, and may replace and move it out of the auto scaling group. For more information, please see [Auto Scaling](https://intl.cloud.tencent.com/document/product/377).

## Directions
### Shutdown an instance via the console
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. Select different methods based on actual needs.
  - Shut down an instance: select the instance to be shut down, and click **More**>**Instance Status**> **Shutdown**in the operation column on the right side.
  - Shut down multiple instances: select all instances to be shut down, and click **Shutdown** at the top of the list to shut down instances in batches.
  Reasons are given for instances that cannot be shut down.

### Shutdown an instance via API
For more information, see the [StopInstances](https://intl.cloud.tencent.com/document/product/213/33235) API.

## Subsequent Operations
You can modify the following attributes only if the instance has been shut down.
- **Instance configuration (CPU, memory):** To change the instance type, see [Change Instance Configuration](https://intl.cloud.tencent.com/document/product/213/2178).
- **Change password:** see [Login Password](https://intl.cloud.tencent.com/document/product/213/6093).
- **Load SSH key:** see [SSH Key](https://intl.cloud.tencent.com/document/product/213/6092).
