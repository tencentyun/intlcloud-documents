## Overview
Restarting the CVM instance is a common method to maintain it. It is equivalent to restarting the operating system of the local computer. This document describes how to restart instances.

## Notes
 - **Preparing to restart instances:** The instance cannot provide services during restart. Make sure before restarting the CVM that it has stopped receiving service requests.
 - **How to restart instances:** We recommended you restart an instance using the restart operations provided by Tencent Cloud instead of running the restart command in the instance (such as the relaunch command under Windows and the reboot command under Linux).
 - **Restart time:** Generally, it takes only a few minutes to restart an instance.
 - **Physical features of instances:** Restarting an instance does not change its physical features. Its public and private IP addresses as well as stored data will not be changed.
 - **Billing:** Restarting an instance will not start a new instance billing period.

## Directions
You can restart instances via the following methods:
<dx-tabs>
::: Restarting instance in console

#### Restarting a single instance
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. On the instance management page, proceed according to the actually used view mode:
  - **List view**: in the row of the target instance, select **More** > **Instance Status** > **Restart** as shown below:
 ![](https://qcloudimg.tencent-cloud.cn/raw/fa35600ee1e53b77d9f0abafbef162bc.png)
  - **Tab view**: on the page of the target instance, select **Restart** in the top-right corner as shown below:
 ![](https://qcloudimg.tencent-cloud.cn/raw/d5384873a89471914f97df0b22230d7a.png)


#### Restarting multiple instances
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. Select all instances you want to restart and click **Restart** at the top of the list to batch restart the instances. If they cannot be restarted, the reason will be displayed as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/c887966def1c1d83e837ae18b855d45f.png)
<dx-alert infotype="explain" title="">
A single instance can also be restarted in this method.
</dx-alert>


:::
::: Restarting instances via API
For more information, see the [RebootInstances](https://intl.cloud.tencent.com/zh/document/product/213/33243) API.
:::
</dx-tabs>
