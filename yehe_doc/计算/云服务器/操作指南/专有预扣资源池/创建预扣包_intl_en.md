## Overview
This document describes how to create a dedicated reservation in the CVM console. A dedicated reservation allows you to reserve resources to guarantee a sufficient supply of resources.

<dx-alert infotype="explain" title="">
Upon the creation of a dedicated reservation, the requested instances are reserved for you. Note that idle resources in the dedicated reservation will incur an idle fee. For details, see [Dedicated Reservation Billing](https://intl.cloud.tencent.com/document/product/213/43857).
</dx-alert>



## Directions
1. Log in to the CVM console, and click **[Dedicated Reservation](https://console.cloud.tencent.com/cvm/preparedinstances)** in the left sidebar.
2. Click **Create Dedicated Reservation** on the **Dedicated Reservation** list page.
3. Complete the configuration as shown below:![](https://qcloudimg.tencent-cloud.cn/raw/6298a6e5100aaebcfb27502e29a0c544.png)
<table>
<tr>
<th>Item</th><th>Required</th><th>Notes</th>
</tr>
<tr>
<td width="14%"><a href="https://intl.cloud.tencent.com/document/product/213/43850">Reservation type</a></td>
<td>Yes</td>
<td>
<ul class="params">
<li>For repeated reservations, you can create <a href="https://intl.cloud.tencent.com/document/product/213/2180"> pay-as-you-go</a> CVM instances repeatedly within the quota.</li>
</ul>
</td>
</tr>
<tr>
<td width="12%">Region</td>
<td>Yes</td>
<td>Select the region closest to your users to minimize the access latency and improve the access speed</td>
</tr>
<tr>
<td>Availability Zone</td>
<td>Yes</td>
<td>If you need to reserve multiple CVM instances, it’s recommended to create multiple reservations in different AZs for disaster recovery. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/6091">Regions and AZs</a>.
</td>
</tr>
<tr>
<td>Placement Group</td>
<td>No</td>
<td>Add the instances to placement groups to improve your business availability. Configure as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/15486">Placement Group</a>. <br><b>Rules:</b>
<ul style="margin:0;">
<li>If **Placement Group** is enabled for the reservation, the same placement group need to be specified to create an instance.</li>
<li>If **Placement Group** is not enabled, the reservation can take effect when the new instance has the same AZ, instance type and specification as the reservation.</li>
</ul>
</td>
</tr>
<tr>
<td>Period</td>
<td>Yes</td>
<td>The validity period of a reservation. Options include 1 month, 2 months and 3 months. The idle resources will be released directly upon expiration of the reservation.</td>
</tr>
<tr>
<td>Quantity</td>
<td>Yes</td>
<td>The quantity of CVMs to be reserved.</td>
</tr>
</table>

4. Click **Enable now**.
After the creation, you can [check the created reservations](https://intl.cloud.tencent.com/document/product/213/43853).
