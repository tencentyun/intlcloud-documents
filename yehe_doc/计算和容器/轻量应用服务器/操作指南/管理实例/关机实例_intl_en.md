## Overview
The instance can be shut down when you need to stop the service, or modify configurations that can be done only in the shutdown state. Shutting down an instance is like shutting down a local computer.

## Notes

- You can shut down an instance by using system commands (such as the `shutdown` command on Windows and Linux) or in the Lighthouse console. We recommend you view the shutdown process in the console to check whether any problem occurs.
- Once shut down, a Lighthouse instance will no longer provide service. Therefore, before the shutdown, make sure that the instance has stopped receiving service requests.
- During the shutdown, the status of the instance will change from "Shutting down" to "Shutdown". If the shutdown process takes too long, there may be an exception.
- After an instance is shut down, all disk data will be retained, but data in the memory will be lost.
- Shutting down an instance does not change its physical attributes, so the instance public and private IPs will remain unchanged.


## Directions

<dx-alert infotype="notice" title="">
During instance shutdown, soft shutdown will be performed first by default. If the soft shutdown fails, forced (hard) shutdown will be performed automatically.
</dx-alert>


1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Find the target instance in the instance list and select a shutdown method as desired.
 - In the instance card in the instance list, click **More** > **Shut down** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/8dc0a8f7f55e293776286b5f0879685f.png)
 - Enter the instance details page and click **Shut down** in the bottom-right corner on the page as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/d038a525d58b64f0122a0d4879523f6b.png)
 - For an instance created by using an application image, you can enter the instance details page, select **Pre-installed application**, and click **Shut down** in **Application information** or in the top-right corner of the page as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/f09802c5a7af6ebb0bfe586006e86014.png)
3. In the pop-up window, click **OK**.
For instances that cannot be shut down, the specific cause will be displayed on the page.

