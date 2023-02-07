This document describes the latest and historical specifications of TDSQL-C for MySQL.
>?
>- The current specification list may contain some deactivated specifications. Available specifications are listed on the purchase page.
>- The read-write instance and read-only instances in a TDSQL-C for MySQL cluster have the same specification configuration.
>- If you need a higher specification to meet your storage needs, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## Compute node specification[](id:CYNOSJSJDGE)
**Specifications of monthly subscribed and pay-as-you-go compute nodes**:
<table>
<thead><tr>
<th rowspan=2 >Compute Node Specification<br>(CPU and Memory)</th>
<th colspan = "2" style="text-align:center" width="50%">Supported Max Storage Space (GB)</th>
<th rowspan=2 >Max IOPS</th>
<th rowspan=2 >I/O Bandwidth</th></tr>
<tr>
<th>MySQL 5.7 kernel minor version &lt; 2.0.15<br>MySQL 8.0 kernel minor version &lt; 3.1.2</th><th>MySQL 5.7 kernel minor version ≥ 2.0.15<br>MySQL 8.0 kernel minor version ≥ 3.1.2</th></tr>
</thead><tbody>
<tr>
<td>1-core 1 GB MEM</td>
<td>1000</td><td>3000</td><td>8000</td><td>1 Gbps</td></tr>
<tr>
<td>1-core 2 GB MEM</td>
<td>1000</td><td>3000</td><td>8000</td><td>1 Gbps</td></tr>
<tr>
<td>2-core 4 GB MEM</td>
<td>5000</td><td>10000</td><td>48000</td><td>6 Gbps</td></tr>
<tr>
<td>2-core 8 GB MEM</td>
<td>5000</td><td>10000</td><td>48000</td><td>6 Gbps</td></tr>
<tr>
<td>2-core 16 GB MEM</td>
<td>5000</td><td>10000</td><td>48000</td><td>6 Gbps</td></tr>
<tr>
<td>4-core 8 GB MEM</td>
<td>10000</td><td>30000</td><td>96000</td><td>12 Gbps</td></tr>
<tr>
<td>4-core 16 GB MEM</td>
<td>10000</td><td>30000</td><td>96000</td><td>12 Gbps</td></tr>
<tr>
<td>4-core 24 GB MEM</td>
<td>10000</td><td>30000</td><td>96000</td><td>12 Gbps</td></tr>
<tr>
<td>4-core 32 GB MEM</td>
<td>10000</td><td>30000</td><td>96000</td><td>12 Gbps</td></tr>
<tr>
<td>8-core 16 GB MEM</td>
<td>10000</td><td>50000</td><td>216000</td><td>27 Gbps</td></tr>
<tr>
<td>8-core 32 GB MEM</td>
<td>10000</td><td>50000</td><td>216000</td><td>27 Gbps</td></tr>
<tr>
<td>8-core 48 GB MEM</td>
<td>10000</td><td>50000</td><td>216000</td><td>27 Gbps</td></tr>
<tr>
<td>8-core 64 GB MEM</td>
<td>10000</td><td>50000</td><td>216000</td><td>27 Gbps</td></tr>
<tr>
<td>12-core 48 GB MEM</td>
<td>10000</td><td>80000</td><td>288000</td><td>36 Gbps</td></tr>
<tr>
<td>12-core 72 GB MEM</td>
<td>10000</td><td>80000</td><td>288000</td><td>36 Gbps</td></tr>
<tr>
<td>12-core 96 GB MEM</td>
<td>10000</td><td>80000</td><td>288000</td><td>36 Gbps</td></tr>
<tr>
<td>16-core 64 GB MEM</td>
<td>20000</td><td>100000</td><td>384000</td><td>48 Gbps</td></tr>
<tr>
<td>16-core 96 GB MEM</td>
<td>20000</td><td>100000</td><td>384000</td><td>48 Gbps</td></tr>
<tr>
<td>16-core 128 GB MEM</td>
<td>20000</td><td>100000</td><td>384000</td><td>48 Gbps</td></tr>
<tr>
<td>24-core 96 GB MEM</td>
<td>20000</td><td>150000</td><td>480000</td><td>60 Gbps</td></tr>
<tr>
<td>24-core 144 GB MEM</td>
<td>20000</td><td>150000</td><td>480000</td><td>60 Gbps</td></tr>
<tr>
<td>24-core 192 GB MEM</td>
<td>20000</td><td>150000</td><td>480000</td><td>60 Gbps</td></tr>
<tr>
<td>32-core 128 GB MEM</td>
<td>50000</td><td>200000</td><td>576000</td><td>72 Gbps</td></tr>
<tr>
<td>32-core 192 GB MEM</td>
<td>50000</td><td>200000</td><td>576000</td><td>72 Gbps</td></tr>
<tr>
<td>32-core 256 GB MEM</td>
<td>50000</td><td>200000</td><td>576000</td><td>72 Gbps</td></tr>
<tr>
<td>48-core 192 GB MEM</td>
<td>50000</td><td>300000</td><td>648000</td><td>81 Gbps</td></tr>
<tr>
<td>48-core 288 GB MEM</td>
<td>50000</td><td>300000</td><td>648000</td><td>81 Gbps</td></tr>
<tr>
<td>48-core 384 GB MEM</td>
<td>50000</td><td>300000</td><td>648000</td><td>81 Gbps</td></tr>
<tr>
<td>48-core 488 GB MEM</td>
<td>50000</td><td>300000</td><td>648000</td><td>81 Gbps</td></tr>
<tr>
<td>64-core 256 GB MEM</td>
<td>50000</td><td>400000</td><td>720000</td><td>90 Gbps</td></tr>
<tr>
<td>64-core 384 GB MEM</td>
<td>50000</td><td>400000</td><td>720000</td><td>90 Gbps</td></tr>
<tr>
<td>64-core 512 GB MEM</td>
<td>50000</td><td>400000</td><td>720000</td><td>90 Gbps</td></tr>
<tr>
<td>88-core 710 GB MEM</td>
<td>50000</td><td>400000</td><td>780000</td><td>98 Gbps</td></tr>
</tbody></table>	
