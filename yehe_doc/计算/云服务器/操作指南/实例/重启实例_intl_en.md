## Operation Scenario

Restarting the CVM instance is a common method to maintain it. It is equivalent to restarting the operating system of the local computer. This document describes how to restart instances.

## Notes
 - **Preparing to restart instances:** The instance cannot provide services during restart. Make sure before restarting the CVM that it has stopped receiving service requests.
 - **How to restart instances:** We recommended you to restart an instance using the restart operations provided by Tencent Cloud instead of running the restart command in the instance (such as the relaunch command under Windows and the reboot command under Linux).
 - **Restart time:** Generally, it takes only a few minutes to restart an instance.
 - **Physical features of instances:** Restarting an instance does not change its physical features. Its public and private IP addresses as well as stored data will not be changed.
 - **Billing:** Restarting an instance will not start a new instance billing period.

## Directions

You can restart instances via the following methods:
- [Use the console to restart instances](#consoleRestart)
- [Use API to restart instances](#apiRestart)

<span id="consoleRestart"></span>
### Use the console to restart instances

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
2. On the instance management page, select the instance restart method based on the actual number of instances to be restarted.
 - Restarting a single instance: On the row of the instance you want to restart, click **More** > **Instance Status** > **Restart**, as shown below:
 ![Restarting a single instance](https://main.qcloudimg.com/raw/56eb6421097130f3f424f582ff3d9f14.png)
 - Restarting multiple instances: Check all instances you want to restart and click **Restart** at the top of the list to batch restart the instances. If they cannot be restarted, the reason will be displayed, as shown below:
![Restarting multiple instances](https://main.qcloudimg.com/raw/c6eb646bd8d19e5484d43be3b9cac9bf.png)
> A single instance can also be restarted using this method.

<span id="apiRestart"></span>
### Use API to restart instances
Please see [RebootInstances API](https://intl.cloud.tencent.com/document/product/213/33243).
