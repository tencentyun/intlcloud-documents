## Overview
This document describes how to attach a cloud disk to any Lighthouse instances in the same availability zone in the console.

<dx-alert infotype="notice" title="">
Up to 5 data disks can be attached to one Lighthouse instance.
</dx-alert>





## Directions
You can attach the cloud disks in the following ways:
<dx-tabs>
::: Select an instance to associate
1. Log in to the Lighthouse console and click **[Cloud Disk](https://console.cloud.tencent.com/lighthouse/cbs/index)** on the left sidebar.
**. Select a region at the top of the **Cloud Disk" page, find the target cloud disk, and click **More** > **Attach**.
![](https://qcloudimg.tencent-cloud.cn/raw/7e4c460087d0a181c667a9eadaea206a.png)
3. Open **Attach to the instance** > **Select an instance**.
	Select the target instance, and complete the parameters **Attaching options**.
	 - Unified expiry time with the instance (XXX)
	 - Monthly auto-renewal **(recommended)**
	 - Attach directly
4. Click **Next**, and note the following in **Subsequent operations**:
After attaching the cloud disk, you need to log in to the instance and initialize the disk.
5. Click **Attach now**.
If the status of the cloud disk changes to **Attached**, the attachment is successful.
![](https://qcloudimg.tencent-cloud.cn/raw/bc73e077bf06ba4470d3a3ca11b54474.png)


:::
::: Select a cloud disk to attach
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index) and select the target instance and enter the details page.
2. Select the **Cloud disk** tab, and click **Attach cloud disk**.
![](https://qcloudimg.tencent-cloud.cn/raw/f503112e1027d0eb20c5a116a9291fb2.png)
3. In the pop-up window, "select a cloud disk":
	Select the cloud disk that needs to be attached, and complete the parameters **Attaching options**.
	 - Unified expiry time with the instance (XXX)
	 - Monthly auto-renewal **(recommended)**
	 - Attach directly
4. Click **Next**, 
After attaching the cloud disk, you need to log in to the instance and initialize the disk.
![](https://qcloudimg.tencent-cloud.cn/raw/4dd6904d0daa8ff8490692b9fb035242.png)

:::
</dx-tabs>


## Subsequent Operations
After attaching the cloud disk, you need to log in to the instance and initialize the disk first before using it. For details, see [Initializing a Cloud Disk](https://intl.cloud.tencent.com/document/product/1103/46566).


<style>
.params{margin:0px !important}
</style>
