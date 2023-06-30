The GN7vw GPU instance model is a rendering model based on NVIDIA Tesla T4 GPU, configured with the vDWS license server, and installed with the GRID driver. It is suitable for graphics and image processing scenarios such as 3D rendering and video encoding/decoding. Its billing mode and prices are different from those of other instance models. This document describes its billing details.

## Billing
Fees of the GN7vw GPU instance model include [instance fees](#instancePrice) and [storage fees](#storagePrice) and are postpaid monthly.

### Instance fees[](id:instancePrice)

#### Billing cycle
The fees are postpaid monthly. If an instance is used for less than one month, the usage duration will be calculated based on the ratio of the actual usage duration in hours to the total number of hours in that month.

#### Calculation formula
Calculation formula for the fees of an instance used for less than one month: **instance fees = usage duration percentage * monthly instance unit price**
>? Usage duration percentage = actual monthly usage duration in hours / (number of days in the month * 24), which is accurate down to the hour.
>
For example, if a user created a 4-core 16 GB memory GN7vw GPU instance at 15:04 on May 8, 2021 and terminated it at 18:39 on May 23, 2021, then the instance fees were:

 - Usage duration percentage = (instance termination time - instance creation time) / (number of days in the month * 24) = 340 / (31 * 24) = 45.7%
 - Instance fees = 45.7% * 1047 = 478.48 CNY

#### Instance prices
<table>
<thead>
<tr>
<th align="left">Model Specification</th>
<th align="left">vCPU (Cores)</th>
<th align="left">Memory (GB)</th>
<th>GPU Graphic Card (Tesla T4)</th>
<th align="left">Price (CNY/Month)</th>
</tr>
</thead>
<tbody><tr>
<td align="left">GN7vw.LARGE16</td>
<td align="left">4</td>
<td align="left">16</td>
<td>1/4</td>
<td align="left">1047</td>
</tr>
<tr>
<td align="left">GN7vw.2XLARGE32</td>
<td align="left">8</td>
<td align="left">32</td>
<td>1/2</td>
<td align="left">1874</td>
</tr>
<tr>
<td align="left">GN7vw.4XLARGE64</td>
<td align="left">16</td>
<td align="left">64</td>
<td>1</td>
<td align="left">3528</td>
</tr>
<tr>
<td align="left">GN7vw.8XLARGE128</td>
<td align="left">32</td>
<td align="left">128</td>
<td>2</td>
<td align="left">7056</td>
</tr>
</tbody></table>

### Storage Fees[](id:storagePrice)

#### Storage type
**Local storage (SSD)** is based on NVMe SSD. It provides low-latency, ultra high-IOPS, and high-throughput storage resources but has data loss risks (in cases such as host failure), so you need to guarantee data reliability at the application layer.

#### Storage price
The unit price is 1 CNY/GB/month. You can modify the storage capacity of the system and data disks as needed when creating a module.


>?
>- Instances with different configurations provide different computing and storage capabilities. You can select the instance configuration and quantity based on your actual business needs.
>- Bills are reported by instance in the Tencent Cloud billing system. You can view the instance information such as instance ID, name, usage start time, usage end time, and edge node name.

