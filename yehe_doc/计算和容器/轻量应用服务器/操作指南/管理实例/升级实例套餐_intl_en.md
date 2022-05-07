## Overview
This document guides you through the process of upgrading a Tencent Cloud Lighthouse instance.


## Limits
- Lighthouse instances can only be upgraded, but not downgraded. It means that the new specification (including the CPU, MEM, SSD system disk size, bandwidth/bandwidth cap and monthly traffic plan) must be higher than the current specification.
- The CPU model of the underlying physical server can not be specified for the upgrade. It’s randomly assigned.
- The availability zone can not be changed in the upgrade.
- If the instance is using a fixed bandwidth package (1C1G, 20 GB SSD system disk and 1 Mbps bandwidth), as this package has been discontinued, you can upgrade it to a traffic package.
- To change the instance type, all the specifications, including the CPU, MEM, SSD system disk size, bandwidth/bandwidth cap and monthly traffic plan, must all be higher than the current specifications. 
- For the price of upgrading an instance, please refer to [Fees for Upgrading Instances](https://intl.cloud.tencent.com/document/product/1103/41562).
 

## Directions
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. In the instance list, locate the instance to upgrade and open its details page.
3. Select **Upgrade package** in **Billing information**.
![](https://qcloudimg.tencent-cloud.cn/raw/b3383496bed35cc6c319654ddda13e68.png)
4. In the **Upgrade package** pop-up window, choose the target package.
5. Select **I have read and agree to Fees for Instance Package Upgrade** and click **Next: Shut down the instance**. 
<img src="https://main.qcloudimg.com/raw/f1c38c5480bc9883b6d5f7f9fa3d5c08.png" style="width:80%">
6. In the **Shutdown instance** step, select **Agree to a forced shutdown** and then click **Upgrade now**.
<dx-alert infotype="notice" title="">
- To upgrade an instance, it must be shut down. You can manually shut down the instance first or **Agree to a forced shutdown** to forcibly shut down a running instance for the upgrade and restart it again. 
- After the upgrade, the current IP address, firewall policies, password/key settings will not be affected.
- For a system disk expansion, there is no need to manually expand the partition and file system. The original data is not be affected.
- The current traffic usage of the instance is not changed. Only the traffic quota of the monthly traffic package is upgraded.
- If the instance is upgraded from a fixed bandwidth to a traffic package, the usage of the traffic package starts upon the completion of upgrade.
</dx-alert>
- It usually takes 1-5 minutes for the upgrade to take effect. You can check the instance in the instance details page when the upgrade is completed.
