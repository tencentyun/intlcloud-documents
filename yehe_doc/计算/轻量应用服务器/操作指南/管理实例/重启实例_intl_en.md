## Overview

Instance restart is a common maintenance method for Lighthouse and is similar to restarting the OS on a local computer.

## Notes
 - **Preparing to restart instances:** The Lighthouse instance cannot provide services during restart. Make sure before restarting the instance that it has stopped receiving service requests.
 - **How to restart instances:** We recommended you restart an instance by using the restart operations provided by Tencent Cloud instead of running the restart command in the instance (such as the relaunch command under Windows and the `Reboot` command under Linux).
 - **Restart time:** Generally, it takes just a few minutes from when the instance starts to execute the restart operation to when the operating system is completely started.
 - **Physical features of instances:** Restarting an instance does not change its physical features. Its public and private IP addresses as well as stored data will not be changed.

## Directions

<dx-alert infotype="notice" title="">
During instance restart, soft restart will be performed first by default. If soft restart fails, forced (hard) restart will be performed automatically.
</dx-alert>



1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Find the target instance in the instance list and select a restart method as desired.
 - In the instance card in the instance list, click **More** > **Restart** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/9e4307f9e2fd3e87450d2944b53c744a.png)
 - Enter the instance details page and click **Restart** in the top-right corner on the page as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/d066f4da7c37d59bb5c9867fd5c91442.png)
 - For an instance created by using an application image, you can enter the instance details page, select **Pre-installed application**, and click **Restart** in **Application information** or in the top-right corner of the page as shown below:
 ![](https://qcloudimg.tencent-cloud.cn/raw/4db038ed29dcad52baf4f8c67c4ad78b.png)
3. In the pop-up window, click **OK**.
