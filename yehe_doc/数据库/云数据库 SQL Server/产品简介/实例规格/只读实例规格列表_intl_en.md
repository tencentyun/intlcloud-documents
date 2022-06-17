In TencentDB for SQL Server, you can create one or more read-only instances and use them to sustain high numbers of database reads, so as to implement auto scaling of read capabilities and alleviate pressure on the database. This document describes the specifications and configurations of read-only instances.

### TencentDB for SQL Server Read-Only Instance

<table>
<thead><tr><th>Version</th><th>Disk Type</th><th>CPU and Memory</th><th>Disk</th></tr></thead>
<tbody>
<td rowspan=13><br>2008 R2 Enterprise<br>2012 Enterprise<br>2014 Enterprise<br>2016 Enterprise<br>2017 Enterprise<br>2019 Enterprise</td>
<td rowspan="13">High-performance local SSD</td>
<td>1-core 2 GB MEM</td><td rowspan="7">10–3,000 GB</td>
<tr><td>1-core 4 GB MEM</td></tr>
<tr><td>1-core 8 GB MEM</td></tr>
<tr><td>2-core 16 GB MEM</td></tr>
<tr><td>4-core 32 GB MEM</td></tr>
<tr><td>8-core 64 GB MEM</td></tr>
<tr><td>12-core 96 GB MEM</td></tr>
<td>16-core 128 GB MEM</td><td rowspan="6">10–6,000 GB</td>
<tr><td>24-core 192 GB MEM</td></tr>
<tr><td>32-core 256 GB MEM</td></tr>
<tr><td>48-core 384 GB MEM</td></tr>
<tr><td>64-core 512 GB MEM</td></tr>
<tr><td>90-core 720 GB MEM</td></tr>
</tbody></table>

