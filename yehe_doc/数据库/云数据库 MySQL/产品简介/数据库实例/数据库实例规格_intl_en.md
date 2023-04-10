This document describes the latest specifications of TencentDB for MySQL.

## Two-node/Three-node (local SSD disk)
The following table lists the specifications of source instances (two-node/three-node), read-only instances, and disaster recovery instances.
<table class="table-striped">
<tbody>
<tr><th>Isolation Policy</th><th>CPU and Memory</th><th>Maximum IOPS</th><th>Storage Space</th></tr>
<tr>
<td rowspan="14">General</td>
<td>1-core 1000 MB</td><td>1200</td><td rowspan="4">25–3000 GB</td></tr>        
<tr>
<td>1-core 2000 MB</td><td>2000</td></tr>
<tr>
<td>2-core 4000 MB</td><td>4000</td></tr>
<tr>
<td>4-core 8000 MB</td><td>8000</td></tr>
<tr>
<td>4-core 16000 MB</td><td>14000</td><td rowspan="6">25–4000 GB</td></tr>
<tr>
<td>8-core 16000 MB</td><td>20000</td></tr>
<tr>
<td>8-core 32000 MB</td><td>28000</td></tr>
<tr>
<td>16-core 32000 MB</td><td>32000</td></tr>
<tr>
<td>16-core 64000 MB</td><td>40000</td></tr>
<tr>
<td>16-core 96000 MB</td><td>40000</td></tr>
<tr>
<td>16-core 128000 MB</td><td>40000</td><td rowspan="3">25–8000 GB</td></tr>
<tr>
<td>24-core 244000 MB</td><td>60000</td></tr>
<tr>
<td>32-core 256000 MB</td><td>80000</td></tr>
<tr>
<td>48-core 488000 MB</td><td>120000</td><td rowspan="1">25–12000 GB</td></tr>
<tr>
<td rowspan="26">Dedicated</td>
<td>2-core 16000 MB</td><td>8000</td><td rowspan="7">25–3000 GB</td></tr>        
<tr>
<td>4-core 16000 MB</td><td>10000</td></tr>
<tr>
<td>4-core 24000 MB</td><td>13000</td></tr>
<tr>
<td>4-core 32000 MB</td><td>16000</td></tr>
<tr>
<td>8-core 32000 MB</td><td>32000</td></tr>
<tr>
<td>8-core 48000 MB</td><td>36000</td></tr>
<tr>
<td>8-core 64000 MB</td><td>40000</td></tr>
<tr>
<td>12-core 48000 MB</td><td>36000</td><td rowspan="15">25–6000 GB</td></tr>
<tr>
<td>16-core 64000 MB</td><td>60000</td></tr>
<tr>
<td>12-core 72000 MB</td><td>40000</td></tr>
<tr>
<td>12-core 96000 MB</td><td>48000</td></tr>
<tr>
<td>16-core 96000 MB</td><td>60000</td></tr>
<tr>
<td>24-core 96000 MB</td><td>72000</td></tr>
<tr>
<td>16-core 128000 MB</td><td>60000</td></tr>
<tr>
<td>32-core 128000 MB</td><td>80000</td></tr>
<tr>
<td>24-core 144000 MB</td><td>76000</td></tr>
<tr>
<td>24-core 192000 MB</td><td>80000</td></tr>
<tr>
<td>32-core 192000 MB</td><td>90000</td></tr>
<tr>
<td>48-core 192000 MB</td><td>120000</td></tr>
<tr>
<td>32-core 256000 MB</td><td>100000</td></tr>
<tr>
<td>48-core 288000 MB</td><td>140000</td></tr>
<tr>
<td>48-core 384000 MB</td><td>140000</td></tr>
<tr>
<td>64-core 256000 MB</td><td>150000</td><td rowspan="2">25–9000 GB</td></tr>
<tr>
<td>64-core 384000 MB</td><td>150000</td></tr>
<tr>
<td>64-core 512000 MB</td><td>150000</td><td rowspan="2">25–12000 GB</td></tr>
<tr>
<td>90-core 720000 MB</td><td>150000</td></tr>
</tbody></table>        

>?The storage space cap of an instance specification may vary by region as displayed on the purchase page.

## Single-node (SSD cloud disk)
<table class="table-striped">
<thead><tr><th>Isolation Policy</th><th>CPU and Memory</th><th>Maximum IOPS</th><th>Maximum Throughput</th><th>Storage Space</th></tr></thead>
<tbody>
<tr>
<td rowspan="8">Basic</td>
<td>1-core 1000 MB</td><td rowspan="8">Random IOPS formula: Random IOPS = min{1800 + 30 * capacity (GB), 26000}<br>Maximum IOPS: 26000</td><td rowspan="8">Throughput formula (MB/s): Throughput = min{120 + 0.2 * capacity (GB), 260}<br>Maximum throughput (MB/s): 260 MB/s</td><td rowspan="8">20–32000 GB</td></tr>
<tr>
<td>1-core 2000 MB</td></tr>
<tr>
<td>2-core 4000 MB</td></tr>
<tr>
<td>2-core 8000 MB</td></tr>
<tr>
<td>4-core 8000 MB</td></tr>
<tr>
<td>4-core 16000 MB</td></tr>
<tr>
<td>8-core 16000 MB</td></tr>
<tr>
<td>8-core 32000 MB</td></tr>
</tbody></table>

## Single-node (Enhanced SSD cloud disk)
<table class="table-striped">
<thead><tr><th>Isolation Policy</th><th>CPU and Memory</th><th>Maximum IOPS</th><th>Maximum Throughput</th><th>Storage Space</th></tr></thead>
<tbody>
<tr>
<td rowspan="8">Basic</td>
<td>1-core 1000 MB</td><td rowspan="8">Random IOPS formula: Random IOPS = min{1800 + 50 * capacity (GB), 50000}<br>Maximum IOPS: 50000</td><td rowspan="8">Throughput formula (MB/s): Throughput = min{120 + 0.5 * capacity (GB), 350}<br>Maximum throughput (MB/s): 350 MB/s</td><td rowspan="8">20–32000 GB</td></tr>
<tr>
<td>1-core 2000 MB</td></tr>
<tr>
<td>2-core 4000 MB</td></tr>
<tr>
<td>2-core 8000 MB</td></tr>
<tr>
<td>4-core 8000 MB</td></tr>
<tr>
<td>4-core 16000 MB</td></tr>
<tr>
<td>8-core 16000 MB</td></tr>
<tr>
<td>8-core 32000 MB</td></tr>
</tbody></table>
