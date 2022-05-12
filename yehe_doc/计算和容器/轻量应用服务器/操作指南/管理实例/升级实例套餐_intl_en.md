## Overview
Tencent Cloud Lighthouse Application Server can quickly and easily adjust instance configurations by upgrading existing packages, which shows its flexibility. This article introduces the operation method and precautions for upgrading the package.


## Notes
Lighthouse Application Server instance is only supported in upgrading packages, not in downgrading, which means the selected package's CPU, MEM, SSD system disk, bandwidth/peak bandwidth and monthly traffic should all be larger than the current package.
> - When upgrading your package, you cannot specify the CPU model of the underlying physical server; Instead, Tencent Cloud will randomly assign a physical CPU model that meets the selected package specification.
Upgrading package across availability zones are not supported.
We support fixed bandwidth package (which has been taken offline, configured with 1 core, 1GB MEM, 20GB SSD system disk, 1Mbps bandwidth) to upgrade to traffic package.
Only when the selected package’s CPU, MEM, SSD system disk, bandwidth/peak bandwidth and monthly traffic are all larger than the current package should cross-type upgrade package be available. That is, there is no package type restriction when the instance is upgraded to a package. For example, general package could be upgraded to storage package.
For directions and precautions on instance package upgrade, please refer to [Fees for Instance Package Upgrade](https://intl.cloud.tencent.com/document/product/1103/41407).


## Directions
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. In the instance list, find and enter the details page of the instance for which to upgrade the package.
3. Select **Upgrade Package** in “Fee Information”. As shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/1b647d16dcf19061c1e3ea8dc705ec43.png)
4.In the "Upgrade Package" pop-up window, choose the selected package.
5. Read and tick “Instance Upgrade Descriptions” and click on **Next step: Shutdown tips**. As shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/1523d050542b401dbba584573a2d0601.png" style="width:80%">
6. In the "Shutdown tips" step, tick "Agree to force shutdown" and then click on **Start upgrade**.
<dx-alert infotype="notice" title="">
Operating instance in shutdown status is supported. If you need to operate the instance in the power-on status, you need to confirm a forced shutdown, and it will take effect after restarting.
After upgrading, the current IP address, firewall policy, password/key settings will not be affected.
If the upgrade operation involves the expansion of the system disk of the instance, there is no need to manually expand the partition and file system operation after the package is successfully upgraded, and the original data will not be affected.
The current used traffic of the instance will not change, and the monthly traffic pack limit will be adjusted to the traffic pack limit of the upgraded package.
If the instance is upgraded from a fixed bandwidth to a traffic package, it will obtain a full traffic package limit and start calculating used traffic immediately after successful operation.
</dx-alert>
It usually takes 1-5 minutes for instance to finish upgrade. When it is done successfully, you can check the information about the package in the instance details page.
