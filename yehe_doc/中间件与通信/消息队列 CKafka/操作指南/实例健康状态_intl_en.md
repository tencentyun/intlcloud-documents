CKafka runs an inspection program for each instance, which checks for metrics such as the number of connections to the instance, disk usage percentage, peak production bandwidth, and peak consumption bandwidth. The instance status varies based on these metric values. When one of the metric values exceeds a certain threshold, the instance status will change.

### Viewing Instance Statuses
Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka/index), and on the instance list page, view the health status of each instance.

![](https://main.qcloudimg.com/raw/92c0112ed4e863185fa5dd2aeb7c5a65.png)

### Status Description
The instance status is determined by any one of the following 4 metrics: the number of connections, disk usage percentage, peak production bandwidth (excluding replica bandwidth), and peak consumption bandwidth. For more information, see the following table:

<table>
<tr><th>Metric</th><th>Threshold (N)</th><th>Status Description</th></tr>
<tr><td rowspan="3">Number of connections (default maximum value: 5000)</td><td>N ≤ 80%</td><td>Healthy</td></tr>
<tr><td>80% < N ≤ 95%</td><td>Warning</td></tr>
<tr><td>N > 95%</td><td>Exception</td></tr>
<tr><td rowspan="3">Disk usage percentage</td><td>N ≤ 80%</td><td>Healthy</td></tr>
<tr><td>80% < N ≤ 95%</td><td>Warning</td></tr>
<tr><td>N > 95%</td><td>Exception</td></tr>
<tr><td rowspan="3">Peak production bandwidth (excluding replica bandwidth)</td><td>N ≤ 80%</td><td>Healthy</td></tr>
<tr><td>80% < N ≤ 100%</td><td>Warning</td></tr>
<tr><td>N > 100%</td><td>Exception</td></tr>
<tr><td rowspan="3">Peak consumption bandwidth</td><td>N ≤ 80%</td><td>Healthy</td></tr>
<tr><td>80% < N ≤ 100%</td><td>Warning</td></tr>
<tr><td>N > 100%</td><td>Exception</td></tr>
</table>

>!The maximum number of allowed connections to an instance is 5000 by default. The system determines thresholds based on this number. If the number of connections has reached the maximum value, clients cannot build new connections with the instance. If this default maximum number does not meet your business requirements, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=%E6%B6%88%E6%81%AF%E6%9C%8D%E5%8A%A1%20CKafKa&level3_id=955&radio_title=%E9%85%8D%E9%A2%9D%E6%8F%90%E5%8D%87%E7%94%B3%E8%AF%B7&queue=81&scene_code=18356&step=2) to set it to a larger number.
