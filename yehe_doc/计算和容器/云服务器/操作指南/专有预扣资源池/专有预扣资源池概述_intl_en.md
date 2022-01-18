## Overview
Dedicated Reservation guarantees the supply for resources to meet users’ large-scale and long-term resource requirements. Upon the creation of a dedicated reservation, the specified CVM resources are reserved for the user. When the user creates CVM instances with the same configuration as of the reservation, the reserved resources are applied. 


## Reservation Type[](id:type)
There are one option of Dedicated Reservations, namely  **repeated reservation**.
<table>
<tr>
<th>Features</th>
<td>Repeated Reservation</td>
</tr>
<tr>
<th>Application Scenarios</th>
<td>Applicable for long-term businesses with periodic workloads</td>
</tr>
<tr>
<th>Repeated deduction<sup>*</sup></th>
<td>Supported</td>
</tr>
<tr>
<th>Supported billing mode</th>
<td>Pay-as-you-go</td>
</tr>
<tr>
<th>Validity options</th>
<td colspan=2>1 month, 2 months and 3 months</td>
</tr>
<tr>
<th>Reservation renewal</th>
<td colspan=2>Supported</td>
</tr>
<tr>
<th>Idle fee</th>
<td colspan=2>The same for both reservation types. For details, see <a href="https://intl.cloud.tencent.com/document/product/213/43857">Dedicated Reservation Billing</a></td>
</tr>
</table>

#### Repeated Deduction[](id:repeatDeduction)

 Suppose you have created a repeated reservation with 1 instance and valid for one month. After successfully creating one instance with this reservation, the reservation has no available instance for deduction. Return this instance after using it for a period of time. If the reservation has not expired, the instance is returned to the reservation and can be used for deduction next time. If the reservation expires, the instance will be released.

## Usage Limits
 - Dedicated reservations can be used to create pay-as-you-go CVMs. See [Billing Plans](https://intl.cloud.tencent.com/document/product/213/2180).
- One reservation can include up to 100 instances.
- The reservation cannot be returned once created.
- The actual inventory determines the quota when creating a reservation.
  For example, if one user needs to create a reservation containing 100 instances, but the inventory actually contains 50 instances, then the user can only create a reservation with 50 instances.



## References
<table>
<tr>
<th>Content</th>
<th>Documentation</th>
</tr>
<tr>
<td>Billing rules of dedicated reservation</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/213/43857">Dedicated Reservation Billing</a>
</td>
</tr>
<tr>
<td>Reserve CVM instances to a dedicated reservation</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/213/43851">Creating Reservations</a>
</td>
</tr>
<tr>
<td>Checking available reservations</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/213/43852">Aggregated List of Available Reservations</a>
</td>
</tr>
<tr>
<td>Checking existing reservations</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/213/43853">Checking Created Reservations</a>
</td>
</tr>
<tr>
<td>Reservation renewal</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/213/43854">Renewing Reservations</a>
</td>
</tr>
<tr>
<td>Create reservations with the same configurations</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/213/43855">Creating Reservations with the Same Configurations</a>
</td>
</tr>
<tr>
<td>Create instances using reserved resources</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/213/43856">Creating Similar Instances</a>
</td>
</tr>
</table>
