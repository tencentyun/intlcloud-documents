
CFS offers two types of file systems: standard and high-performance. Below are their features, benefits, and use cases.

<table>
<tr>
    <th>File System Type</th>
    <th>Features</th>
    <th>Benefits</th>
    <th>Use Cases</th>
  </tr>
<tr>
    <td>Standard</td>
    <td nowrap="nowrap">   
    <li>Elastic scaling of storage capacity </br> based on the number of writes, up to 160 TB</li>
    <li>Linear scaling of throughput based </br> on file system capacity, up to 1.2 GB/s</li>
    <li>Up to 4K IOPS (4 KB random read/write), </br> with a latency at the 10-millisecond level</li>
    </td>
    <td nowrap="nowrap"><li>Low costs<br><li>High capacity</td>
    <td>Cost-sensitive and high-volume businesses, such as data backup, file sharing, and log storage</td>
</tr>
<tr>
    <td>High-performance</td>
    <td>   
    <li>Elastic scaling of storage capacity based on the number of writes, up to 2 PB</li>
    <li>Linear scaling of throughput based on file system capacity, up to 40 GB/s</li>
    <li>Up to 60K IOPS (4 KB random read/write), with a millisecond-level latency</li>
    </td>
    <td nowrap="nowrap"><li>High throughput<br><li>High IOPS</td>
    <td>IO-intensive workloads, such as high-performance computing, media asset rendering, machine learning, DevOps, and OA.</td>
 </tr>
</table>



## Performance Formula

The relationship between the throughput of a single standard or high-performance file system and the amount of write storage is as follows:

<table>
   <tr>
      <th>File System Type</th>
      <th>Performance Formula</th>
   </tr>
   <tr>
      <td>Standard</td>
      <td>Throughput (MB/s) = storage capacity (GB) * 0.1 + 100</td>
   </tr>
   <tr>
      <td>High-performance</td>
      <td>Throughput (MB/s) = storage capacity (GB) * 0.2 + 200</td>
   </tr>
</table>

>The above formulas show the capabilities a file system can provide. To reach the upper performance limit, you usually need to perform multi-threaded reads/writes by using multiple computing nodes.
