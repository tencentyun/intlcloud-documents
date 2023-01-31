TencentDB for MySQL fully upgraded the API service to v3.0 on January 1, 2018. Due to the fact that API 2.0 has a higher access latency and is more complicated to use, technical support has been discontinued for API 2.0, which will be deactivated on March 31, 2023.

We recommend you upgrade to TencentDB for MySQL API 3.0 as soon as possible to avoid affecting your business.

You can refer to the API 2.0 and 3.0 comparison table below, where you can find the new APIs you need to upgrade and complete the upgrade accordingly.

## List of APIs switched from v2.0 to v3.0
<table>
<thead><tr><th>API 2.0</td><th>API 3.0</td><th>API 3.0 Documentation</td><th>Input Parameter Change</td></tr></thead>
<tbody>
<tr>
<td>DescribeCdbInstances</td>
 <td>DescribeDBInstances</td>
 <td>Queries the list of instances. For more information, see <a href="https://www.tencentcloud.com/zh/document/api/236/15872">DescribeDBInstances</a>.</td>
 <td>In order to make the API easier to use, some parameters have been changed as described in <a href="https://www.tencentcloud.com/zh/document/api/236/15872">DescribeDBInstances</a>.</td>
 </tr>
 <tr>
<td>QueryCdbStatisticsInfo</td>
 <td>GetAppStat</td>
 <td>This API has been disused. To get the instance monitoring information, call `GetMonitorData`. For more information, see <a href="https://intl.cloud.tencent.com/document/product/248/33881">GetMonitorData</a>.</td>
 <td>No changes.</td>
 </tr>
 <tr>
<td>DescribeDBInstancesV3</td>
 <td>DescribeDBInstances</td>
 <td>Queries the list of instances. For more information, see <a href="https://www.tencentcloud.com/zh/document/api/236/15872">DescribeDBInstances</a>.</td>
  <td>No changes.</td>
 </tr>
 <tr>
<td>GetCdbExportLogUrl</td>
 <td>GetDownloadUrl</td>
 <td><br><li>type = slowlog_day: Queries slow logs. For more information, see <a href="https://intl.cloud.tencent.com/document/product/236/15845">DescribeSlowLogs</a>. <br><li>type = errlog_day: Queries the error logs of an instance. For more information, see <a href="https://intl.cloud.tencent.com/document/product/236/35669">DescribeErrorLogData</a>. <br><li>type = coldbackup: Queries the list of data backups. For more information, see <a href="https://intl.cloud.tencent.com/document/product/236/15842"> DescribeBackups</a>. <br><li>type = binlog: Queries the list of log backups. For more information, see <a href="https://intl.cloud.tencent.com/document/product/236/15843">DescribeBinlogs</a>.</td>
   <td>In order to make the API easier to use, some parameters have been changed as described in: <li><a href="https://intl.cloud.tencent.com/document/product/236/15845">DescribeSlowLogs</a>.<li><a href="https://intl.cloud.tencent.com/document/product/236/35669">DescribeErrorLogData</a>.<li><a href="https://intl.cloud.tencent.com/document/product/236/15842">DescribeBackups</a>.<li><a href="https://intl.cloud.tencent.com/document/product/236/15843">DescribeBinlogs</a>.</td>
 </tr>
 <tr>
<td>RenewCdb</td>
 <td>RenewDBInstance</td>
 <td>Renews a TencentDB instance. For more information, see <a href="https://www.tencentcloud.com/zh/document/api/236/34477">ModifyNameOrDescByDpId</a>.</td>
 <td>In order to make the API easier to use, some parameters have been changed as described in <a href="https://www.tencentcloud.com/zh/document/api/236/34477">ModifyNameOrDescByDpId</a>.</td>
 </tr>
</tbody></table>
