
For the SCF quotas that exceed the limit, the corresponding solutions are as follows:

<table>
<thead>
<tr>
<th>Content</th>
<th>Solution</th>
</tr>
</thead>
<tbody><tr>
<td>The number of namespaces per region reaches the upper limit.</td>
<td>Please <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1">submit a ticket</a> to increase the limits.</td>
</tr>
<tr>
<td>The number of functions per namespace reaches the upper limit.</td>
<td><li>There are multiple namespaces in each region. If the functions quota of a namespace reaches the upper limit, the function quotas of other namespaces can be used first.</li><li>If the number of namespaces and functions in the current region reaches the upper limit, you can <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1">submit a ticket</a> to increase the limits.</li></td>
</tr>
<tr>
<td>The number of triggers per function reaches the upper limit.</td>
<td><li>It is recommended to to split a function into multiple functions by separating the function business logic and bind them to different triggers.</li><li>If the function cannot be split to multiple functions and bound to different triggers due to business needs, please <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1">submit a ticket</a> to increase the limits.</li></td>
</tr>
<tr>
<td>The total concurrency quota of functions per region reaches the upper limit.</td>
<td>Please adjust the <b>Total concurrency quota in the current region</b> in the <b>Concurrency Management</b> > <b>Concurrency Quota</b> page.</td>
</tr>
<tr>
<td>The initialization timeout period of the function exceeds the limits.</td>
<td>Please <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1">submit a ticket</a> to increase the limits.</td>
</tr>
</tbody></table>








