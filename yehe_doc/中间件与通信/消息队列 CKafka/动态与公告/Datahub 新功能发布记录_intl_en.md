## May 2022

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>EMR ClickHouse is supported</td>
<td>When data is distributed to ClickHouse, EMR ClickHouse can be selected as the data warehouse type.</td>
<td>2022-05-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46828">Data Distribution to ClickHouse</a></td>
</tr><tr>
<td>Tasks can be restarted</td>
<td><b>Abnormal</b> tasks can be restarted. The previously processed data and CKafka instance involved will not be affected.</td>
<td>2022-05-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46802">DataHub Overview</a></td>
  </tr><tr>
<td>Tasks can be replicated and recreated</td>
<td><li>When you have a large number of tasks with similar configurations, after creating the first task successfully, you can create more tasks quickly with the task replication feature. </li><li>Task creation failures may be caused by incorrect configurations. In this case, you can manually recreate tasks.</li></td>
<td>2022-05-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46802">DataHub Overview</a></td>
   </tr><tr> 
  <td>The consumption progress can be displayed during data processing and data distribution</td>
<td>-</td>
<td>2022-05-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46802">DataHub Overview</a></td>
   </tr><tr>
  <td>The latest message can be viewed</td>
<td>-</td>
<td>2022-05-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46802">DataHub Overview</a></td>
</tr></table>











## April 2022

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>The schema management feature is supported</td>
<td>With this feature, you can associate a created schema to a specific data access task to verify the format of the accessed data according to the schema.</td>
<td>2022-04-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46803">Schema Management</a></td>
</tr><tr>
<td>Schema is supported for reporting data over HTTP</td>
<td>You can use the specified schema to verify the format of the data reported over HTTP.</td>
<td>2022-04-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46807">Reporting over HTTP</a></td>
  </tr><tr>
<td>You can specify the start offset for a data sync task</td>
<td>-</td>
<td>2022-04-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/32556">Data Sync</a></td>
   </tr><tr> 
  <td>Data can be distributed to COS</td>
<td>You can use DataHub to distribute CKafka data to COS for data analysis and download.</td>
<td>2022-04-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46830">Data Distribution to COS</a></td>
   </tr><tr>
  <td>COS becomes a supported data source</td>
<td>DataHub supports pulling data from COS for unified management and distribution to downstream offline/online processing systems, forming a clear data flow channel.</td>
<td>2022-04-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46812">COS</a></td>
</tr></table>




## March 2022

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Messages with parsing failures can be discarded in a data distribution task with ES or ClickHouse being the data target</td>
<td>If the data target is ES or ClickHouse, messages that failed to be parsed can be discarded. If you don't discard them, exceptions may occur and data dumping will be stopped.</td>
<td>2022-03-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46826">Data Distribution to ES</a></td>
</tr><tr>
<td>JSONPATH is a supported data processing type</td>
<td>JSONPATH is used to parse nested JSON data. It starts with the `$` symbol and uses the `.` symbol to locate specific fields in nested JSON data.</td>
<td>2022-03-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46822">Simple Data Processing</a></td>
</tr><tr>
<td>Data can be distributed to CLS</td>
<td>You can use DataHub to distribute CKafka data to CLS for troubleshooting, metric monitoring, and security audit.</td>
<td>2022-04-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46829">Data Distribution to CLS</a></td>
</tr></table>




## January 2022

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
  <td>DTS becomes a supported data source</td>
<td>DataHub supports pulling data from DTS for unified management and distribution to downstream offline/online processing systems, forming a clear data flow channel.</td>
<td>2022-01-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46811">DTS</a></td>
  </tr><tr>
<td>Data can be distributed to TDW</td>
<td>You can use DataHub to distribute CKafka data to TDW for data storage, query, and analysis.</td>
<td>2022-01-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46827">Data Distribution to TDW</a></td>
</tr><tr>
<td>Data can be distributed to CLS</td>
<td>You can use DataHub to distribute CKafka data to CLS for troubleshooting, metric monitoring, and security audit.</td>
<td>2022-01-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46829">Data Distribution to CLS</a></td>
 </tr><tr>
<td>Data can be distributed to ClickHouse</td>
<td>You can use DataHub to distribute CKafka data to ClickHouse for data storage, query, and analysis.</td>
<td>2022-01-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46828">Data Distribution to ClickHouse</a></td>
</tr></table>




## December 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>DataHub is officially launched</td>
<td>DataHub is a data access and processing platform in Tencent Cloud for one-stop data access, processing, and distribution. It can continuously receive and collect data from applications, web, cloud product logs, and other sources, and process the data in real time. This helps build a data flow linkage at low costs to connect data sources and data processing systems.</td>
<td>2021-12-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46802">DataHub Overview</a></td>
</tr></table>
