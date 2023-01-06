This document describes the pricing of TDSQL-C for MySQL Serverless.

## Billing mode
In the Serverless mode, computing and storage are billed separately: computing is billed by the number of CCUs, while storage is billed by the usage in GB. The billing system calculates the usage by second and settles fees by hour.

## Billing formula
**Total Serverless fees = compute node fees + storage space fees = Serverless computing power price * number of CCUs + storage space price * storage space**

## Serverless compute unit pricing
<table>
<thead><tr>
<th rowspan=2 >Billable Unit</th>
<th >Guangzhou, Shanghai, Beijing, and Nanjing</th>
<tr>
<th>CCU Price (USD/Unit/Second)</th></tr></thead>
<tbody><tr>
<td>Serverless instance</td>
<td>0.00001397</td></tr>
</tbody></table>

>?
>- CynosDB Compute Unit (CCU) is the computing and billing unit for the Serverless Edition. A CCU is approximately equal to 1 CPU core and 2 GB memory. The number of CCUs used in each billing cycle is the greater value between the number of CPU cores used by the database and 1/2 of the memory size.
>- You can refer to [Compute Unit](https://www.tencentcloud.com/document/product/1098/51975) to select the corresponding maximum and minimum CCU values. The storage space upper limit is the same as the maximum storage space corresponding to the common compute node specifications as described in [Product Specifications](https://intl.cloud.tencent.com/document/product/1098/46430).

## [Storage space pricing](id:cckjjg)
The Serverless cluster storage space is pay-as-you-go at 0.0000002 USD/GB/second.
