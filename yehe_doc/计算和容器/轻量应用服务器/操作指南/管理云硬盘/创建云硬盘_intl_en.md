## Overview
You can create a cloud disk and attach it to any Lighthouse instances in the same availability zone to use as a data disk. This document describes how to create a cloud disk in the Tencent Cloud Lighthouse console.
<dx-alert infotype="explain" title="">
The [CBS cloud disks](https://intl.cloud.tencent.com/document/product/362/2345) used on Lighthouse instances are with the same performance as the ones used on CVM instances. 
</dx-alert>

## Considerations
- Cloud disks can be attached only to the instances in the same availability zone (AZ). Cross-AZ attaching is not supported, and the AZ of cloud disks cannot be changed.
- Each region has a quota of 20 cloud disks.

## Directions
1. Log in to the Lighthouse console and click **[Cloud Disk](https://console.cloud.tencent.com/lighthouse/cbs/index)** on the left sidebar.
2. On the top of the **Cloud Disk** page, select a region, and click **Create**.
3. Configure the following parameters in the pop-up window:
<table>
<tr>
<th>Parameter Name</th><th>Description</th>
</tr>
<tr>
<td>Availability zone</td><td>The availability zone where the cloud disk is located.<br><b>Cross-AZ attaching is not supported, and the AZ of the cloud disk cannot be changed.</b></td>
</tr>
<tr>
<td>Cloud disk type</td><td>Supports premium and SSD cloud disks. For more information, see <a href="https://intl.cloud.tencent.com/document/product/362/31636">Cloud Disk Types</a>.</td>
</tr>
<tr>
<td>Capacity</td>
<td>Cloud disk capacity. The adjustment increment is 10 GB. The specifications are as follows:
<ul class="params">
<li>Premium cloud disks: 10 - 1000 GB</li>
<li>SSD cloud disks: 20 - 1000 GB</li>
</ul>
</td>
</tr>
<tr>
<td>Disk name</td><td>Optional. The name can contain up to 60 characters. When it's left empty, the cloud disk ID is used by default.</td>
</tr>
<tr>
<td>Purchase quantity</td><td>It defaults to *1*. Up to 10 cloud disks can be created in a batch. </td>
</tr>
<tr>
<td>Purchase period</td><td>Valid range: 1 month (default) - 5 years.</td>
</tr>
<tr>
<td>Auto-renewal</td><td>When it's enabled, the cloud disk is automatically renewed on a monthly basis upon its expiration when your account has sufficient balance.</td>
</tr>
</table>
4. Click **OK**.
You can view the created cloud disks on the [Cloud Disk](https://console.cloud.tencent.com/lighthouse/cbs/index) page. New cloud disks are "to be attached".
![](https://qcloudimg.tencent-cloud.cn/raw/b6a526ef9313d10e858764e1246ea0b3.png)


## See Also
[Attaching a Cloud Disk](https://intl.cloud.tencent.com/document/product/1103/46568)
