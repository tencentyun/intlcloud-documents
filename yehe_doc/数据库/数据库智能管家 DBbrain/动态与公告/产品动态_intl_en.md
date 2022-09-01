
## July 2022

<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Supported the autonomy service</td>
<td>DBbrain supports automatic throttling and killing for MySQL databases.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/48633">Autonomy Service</a></td></tr>
</tbody></table>

## June 2022

<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Supported event notification</td>
<td>DBbrain can send you the diagnosis results in the exception diagnosis module for MySQL databases.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/39608">Event Notification</a></td></tr>
<tr>
<td>Enhanced multiple features</td>
<td><ul><li>The table analysis feature is added in the optimization window for TencentDB for MySQL and TDSQL-C for SQL.
</li><li>The proxy node aggregate view is added for TencentDB for Redis. </li><li>The latency distribution data is optimized to display value + percentage for TencentDB for Redis. </li><li>The email notification capability is added to the session killing feature for TencentDB for Redis. </li><li>Instances can be searched for in the exception distribution module. </li><li>Key prefix analysis is added to memory analysis for TencentDB for Redis. </li><li>SQL optimization suggestion is supported for `forceindex` and `binary concat` statements. </li><li>Health report subscription and sending are supported for self-built MySQL instances. </li><li>Multiple prompt categories and user experience optimizations are released.</li></ul></td>
<td>-</td></tr>
</tbody></table>

## May 2022

<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Added TencentDB for MongoDB index recommendation</td>
<td>Real-time log information can be collected and analyzed automatically. The optimal index will be recommended and ranked by its impact on performance, which can be operated online.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/48613">Index Recommendation</a></td></tr>
<tr>
<td>Supported SQL throttling for TencentDB for MongoDB</td>
<td>You can control the database requests and SQL concurrency by restrictions on SQL type, maximum concurrency, throttling duration, and SQL keywords to ensure the fast business restoration when excessive CPU is consumed due to high traffic.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/48613">SQL Throttling</a></td></tr>
<tr>
<td>Enhanced basic capabilities for TencentDB for MongoDB</td>
<td><ul><li>SQL template samples and detailed template records are added for the slow SQL analysis feature.</li><li>Slow SQL details can be queried.</li><li>Top table trend and information are added; top database and table retrieval is supported for space analysis.</li></ul></td>
<td><a href="">-</a></td></tr>
</tbody></table>

## April 2022

<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Enhanced multiple features</td>
<td>
<ul><li>Batch health report settings are added for instance management. </li>
<li>Exception-level filtering is supported in the exception push window for various database types covered by DBbrain. </li>
<li>The slow SQL analysis page is optimized to add the **Export** button. </li>
<li>The **Show Sleep Connection** button is added on the real-time session page. </li>
<li>The one-click kill capability is added to the real-time session module. </li>
<li>Multiple quick buttons are added to the SQL optimization module. </li>
<li>Space analysis data (table/database/table without primary key) can be exported. </li>
<li>The real-time session - SQL throttling feature is supported for MySQL 8.0. </li>
<li>Audit analysis results are associated with deadlock diagnosis. </li></ul></td>
<td>-</td></tr>
<tr>
<td>Added APIs</td>
<td>The following APIs are added:
<ul><li>SQL throttling (MySQL): Query the SQL throttling task list of an instance; delete a SQL throttling task for an instance; create a SQL throttling task for an instance; change the SQL throttling task status of an instance. </li>
<li>Big key analysis (TencentDB for Redis): Query the big key list of a TencentDB for Redis instance. </li>
<li>SQL template conversion: Query SQL templates. </li>
<li>Table without primary key: Query tables without primary key in an instance.</li>
<li>Permissions: Verify the database account permissions of a user. </li></ul></td>
<td>-</td></tr>
</tbody></table>

## March 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Supported auditing uncommitted transactions</td>
<td>The exception diagnosis module can diagnose uncommitted transactions and analyze and aggregate their contents. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/48634">Audit Log Analysis</a></td></tr>
</tbody></table>

## February 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Supported visual deadlock analysis</td>
<td>The topology of transactions with deadlocks and their lock relationships can be visually displayed. This feature can display the lock scope and details of locked data. It can also infer about executions based on execution plans, table structures, and SQL parsing to help you avoid deadlocks. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/48632">Deadlock Visualization</a></td></tr>
</tbody></table>

## January 2022
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Supported TencentDB for MongoDB</td>
<td>Features supported for replica set and sharded instances include the overview, management, inspection, exception alarm, monitoring dashboard, real-time session, performance trends (distribution of request types with 10–100 ms latency), MongoStatus and MongoTop tools, collection space management, and 3D exception diagram (for replica set instances only). </td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/48620">Performance Optimization for MongoDB</a></td></tr>
<tr>
<td>Released the API for killing sessions during a period</td>
<td>The API for killing sessions during a period is released for TencentDB for MySQL, TDSQL-C for MySQL, and TencentDB for Redis. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/44869">CreateProxySessionKillTask</a></td></tr>
<tr>
<td>Optimized the user experience</td>
<td>27 experience optimizations are added, such as the capabilities to customize dashboards for full instance monitoring, batch search for and add instances, single/multi-column switch in the monitoring view, drag the monitoring view in a larger area, adjust the size of the analysis result window on the right, and globally zoom in the view.</td>
<td>-</td></tr>
</tbody></table>

## December 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Upgraded ad hoc analysis of big key for TencentDB for Redis</td>
<td>The ad hoc analysis of big key feature for TencentDB for Redis (single-shard/multi-shard) supports custom analysis. </td>
<td>-</td></tr>
<tr>
<td>Supported exception push</td>
<td>Exceptions in individual MySQL database instances can be pushed. </td>
<td>-</td></tr>
<tr>
<td>Supported slow SQL details</td>
<td>The slow SQL details feature is released for TencentDB for MySQL and TDSQL-C for MySQL (SQL details and analysis result details). </td>
<td>-</td></tr>
<tr>
<td>Upgraded audit logs</td>
<td>Real-time audit log analysis and detailed records are added. Log audit should be enabled first.</td>
<td>-</td></tr>
<tr>
<td>Supported uncommitted transaction audit</td>
<td>Exception diagnosis, uncommitted transaction SQL details, context, SQL statement performance analysis results, and other capabilities are added. </td>
<td>-</td></tr>
</tbody></table>

## November 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Supported alarming in CM</td>
<td>You can configure CM smart alarm policies for TencentDB for MySQL in DBbrain. </td>
<td>-</td></tr>
<tr>
<td>Optimized metrics</td>
<td>The memory analysis metrics for TencentDB for Redis are optimized to be more accurate. </td>
<td>-</td></tr>
<tr>
<td>Optimized visual analysis</td>
<td>The visual execution plan analysis capabilities are optimized to support the visual analysis of subqueries for TencentDB for MySQL and TDSQL-C for MySQL. </td>
<td>-</td></tr>
<tr>
<td>Added more exception diagnosis scenarios</td>
<td>More metric interactions are added to trigger exception diagnosis for TencentDB for MySQL and TDSQL-C for MySQL. </td>
<td>-</td></tr>
<tr>
<td>Optimized the exception analysis and verification algorithms</td>
<td>DBbrain's exception analysis and verification algorithms are optimized to increase the accuracy and log and analyze some exceptions such as immediate resolution after triggering and crash.</td>
<td>-</td></tr>
</tbody></table>

## October 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Released the visual execution plan feature</td>
<td>Execution plan visualization is supported for TencentDB for MySQL, TDSQL-C for MySQL, and self-built MySQL. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/48635">SQL Optimization</a></td></tr>
<tr>
<td>Supported InnoDB deadlock parsing</td>
<td>InnoDB deadlock parsing is improved to parse more types of data such as decimal and timestamp. </td>
<td>-</td></tr>
</tbody></table>

## September 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tbody>
<tr>
<td>Released P99/P95 advanced audit capabilities for TDSQL-C for MySQL</td>
<td>In addition to the all request analysis feature, DBbrain also supports <strong>request time consumed analysis (P99)</strong> and <strong>request time consumed analysis (P95)</strong> for TDSQL-C for MySQL, which are more accurate and in-depth and provide advanced analysis capabilities for SQL access latency.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/48634" target="_blank">Audit Log</a></td></tr>
<tr>
<td>Released the health report configuration center</td>
<td>DBbrain allows you to customize health reports. You can generate and receive health reports regularly as needed. You can also customize the rules of health reports and kill reports and specify recipients and recipient groups for report sending. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36042" target="_blank">Health Report Management</a></td></tr>
<tr>
<td>Supported ad hoc analysis of big key for TencentDB for Redis</td>
<td>DBbrain supports ad hoc analysis of big key for TencentDB for Redis, so you can trigger big key analysis at any time as needed. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/48625" target="_blank">Big Key Analysis</a></td></tr>
</tbody></table>

## August 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tr>
<td>Supported batch killing sessions during a period</td>
<td>The capability of batch killing sessions during a period is added for TencentDB for MySQL and TDSQL-C for MySQL. </td>
<td>-</td></tr>
<tr>
<td>Extended the audit log task execution time</td>
<td>The execution time range of a single audit log task is extended from half an hour to two hours. </td>
<td>-</td></tr>
<tr>
<td>Optimized slow log analysis</td>
<td>Slow SQL analysis supports cross-day time selection. </td>
<td>-</td></tr>
<tr>
<td>Optimized the user experience</td>
<td>Slow query display and time display are optimized for TencentDB for Redis. </td>
<td>-</td></tr>
</tbody></table>

## July 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tr>
<td>Supported TencentDB for Redis</td>
<td>The following features are supported for TencentDB for Redis: instance overview, instance management, database inspection, exception alarm, monitoring dashboard, performance monitoring (including performance trends and real-time performance monitoring), real-time session, memory analysis (including key analysis and big key analysis), access analysis (including hot key analysis, latency analysis, and command line analysis), slow log analysis, real-time log analysis, health report, etc.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/48626" target="_blank">Performance Optimization for Redis</a></td></tr>
<tr>
<td>Optimized the user experience</td>
<td>You can redirect to a specific instance from the full instance monitoring section.</td>
<td>-</td></tr>
</tbody></table>

## May 2021
<table>
<thead><tr><th width=20%>Update</th><th width=50%>Description</th><th width=20%>Documentation</th></tr></thead>
<tr>
<td>Added kill records and details</td>
<td>DBbrain allows you to view the records and details of killed sessions. The "Kill Sessions during a Period" execution mode supports manual stop and scheduled stop. You can also view the details of sessions killed during a period.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/48638" target="_blank">Real-Time Session</a></td></tr>
<tr>
<td>Supported self-built database autonomy</td>
<td>DBbrain supports self-built database access through direct connection or the deployment of DBbrain Agent on users' database hosts. This enables multiple types of self-built databases (including CVM-based self-built databases, self-built databases in local IDCs, and self-built databases on VMs of other cloud vendors) to enjoy database autonomy capabilities provided by DBbrain, such as monitoring and alarming, performance optimization, and database management.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/40594" target="_blank">Self-Built Database Access</a></td></tr>
</table>


## March 2021
<table>
<tr><th width=20%>Update</th><th width=50%>Description</th><th width=10%>Release Date</th><th width=20%>Document</th></tr>
<tr>
<td>Scanning tables without primary key is supported</td>
<td>With this feature, you can detect tables without primary key in the current instance through regular scanning and manual refreshing.</td>
<td>2021-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36039" target="_blank">Space Analysis</a></td></tr>
</table>

## December 2020
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tr>
<td>Sending health report via email is supported</td>
<td>Users can easily know the health status of the database instance through the health reports email without logging in to the console. Users can also customize the health reports and recipients as needed.</td>
<td>2020-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/39371" target="_blank">Sending Health Report Email</a></td>
</tr>
</table>


## October 2020
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tbody><tr>
<td>Connection to TencentDB for MySQL instances in new regions is supported</td>
<td>DBbrain can connect to TencentDB for MySQL instances in the following regions: Taipei (China), Mumbai, Singapore, Bangkok, Frankfurt, Moscow, Toronto, Seoul, and Tokyo.</td>
<td>2020-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/38560" target="_blank">Region List</a></td>
</tr>
<tr>
<td>DBbrain supports TencentDB for CynosDB (compatible with MySQL)</td>
<td>The following DBbrain features are supported for TencentDB for CynosDB (compatible with MySQL): instance overview, instance management, database inspection, exception alarms, monitoring dashboards, full instance monitoring, exception diagnosis, performance trends, real-time sessions, etc.</td>
<td>2020-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/38559" target="_blank">Feature List</a></td>
</tr>
</tbody></table>

## July 2020
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tbody><tr>
<td>Supported monitoring dashboard</td>
<td>The monitoring dashboard feature supports dashboard customization and allows you to link, compare, and view the monitoring data of multiple instances and metrics.</td>
<td>2020-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/37668" target="_blank">Monitoring Dashboard</a></td>
</tr>
<tr>
<td>Supported performance trends</td>
<td>The performance trends feature supports selection of multiple performance metrics and multiple ways to view performance trends, such as fine-grained view of one single performance metric trend, link comparison view of multiple performance metric trends, and time comparison view of multiple performance metric trends.</td>
<td>2020-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/37666" target="_blank">Performance Trends</a></td>
</tr>
<tr>
<td>Supported quick execution for database account authentication and common OPS commands</td>
<td>The SQL optimization feature helps you authorize database accounts, batch execute SQL statements, query history records, and identify transactions. It also provides common OPS commands for quick execution.</td>
<td>2020-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36040" target="_blank">SQL Optimization</a></td>
</tr>
<tr>
<td>Added SQL throttling and hotspot update protection</td>
<td>The SQL throttling feature is now available to help you downgrade business at database level. The hotspot update protection feature is under beta test. It can improve database concurrency performance.</td>
<td>2020-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36037" target="_blank">Real-Time Session</a></td>
</tr>
<tr>
<td>Added physical file size measurement</td>
<td>The space analysis feature calculates the sizes of physical files and provides trend curves of top tables and databases.</td>
<td>2020-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36039" target="_blank">Space Analysis</a></td>
</tr>
</tbody></table>



## June 2020
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tbody>
<tr>
<td>Connection to database instances in new regions is supported</td>
<td>DBbrain now supports connecting to database instances in the Shenzhen, Nanjing, Chongqing, Chengdu, Hong Kong (China), Silicon Valley, and Virginia regions.</td>
<td>2020-06</td>
<td>-</td>
</tr>
</tbody></table>



## May 2020
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tbody><tr>
<td>Supported database inspection</td>
<td>The database inspection feature regularly automates health inspection of full instance. You can also set up custom inspections based on your own needs to help troubleshoot potential instance issues and provide solutions.</td>
<td>2020-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/37178" target="_blank">Database Inspection</a></td>
</tr>
<tr>
<td>Launched the SQL optimization effect prediction and comparison engine</td>
<td>The SQL optimization feature can display execution plan and overheads comparison before and after SQL optimization as well as performance improvement rate.</td>
<td>2020-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36040" target="_blank">SQL Optimization</a></td>
</tr>
<tr>
<td>Added database account security scan</td>
<td>The database account security scan feature is launched to ensure account/password security.</td>
<td>2020-05</td>
<td>-</td>
</tr>
<tr>
<td>Upgraded database health scoring system</td>
<td>The database health scoring system is upgraded to get more accurate running status of user's database by using AI.</td>
<td>2020-05</td>
<td>-</td>
</tr>
<tr>
<td>Added new exception diagnosis items</td>
<td>New exception diagnosis items are added, including availability exception diagnosis (OOM, primary-secondary switch, failover, and delayed elimination) and root cause analysis.</td>
<td>2020-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36036" target="_blank">Exception Diagnosis</a></td>
</tr>
</tbody></table>




## February 2020
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tbody><tr>
<td>Added statistics to slow SQL analysis</td>
<td>Statistics are available in slow SQL analysis, including time consumed distribution and source IP analysis.</td>
<td>2020-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36038" target="_blank">Slow SQL Analysis</a></td>
</tr>
<tr>
<td>Supported instance list management</td>
<td>The instance management feature displays the information of the database instances currently supporting DBbrain. It mainly shows the basic information of database instances (instance name/ID, status, etc.) and their access sources, groups, exception alarms, health scores, and operations.</td>
<td>2020-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36033" target="_blank">Instance Management</a></td>
</tr>
<tr>
<td>Supported exception alarm</td>
<td>The exception alarm feature displays the information overview of exception alarms (exceptions detected by "24/7 Exception Diagnosis") generated by database instances connected to DBbrain, including the basic information of the database instance (instance name/ID, private IP, AZ), risk level, diagnosis items, duration, and operations.</td>
<td>2020-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/37177" target="_blank">Exception Alarm</a></td>
</tr>
</tbody></table>

## December 2019
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tbody><tr>
<td>Supported full instance monitoring</td>
<td>The full instance monitoring page gives you an overview of the database monitoring metrics of all instances. The unified monitoring view displays the horizontal view of single monitoring metrics of all instances, allowing you to view and detect database exceptions and providing you with a new macro view on monitoring information.</td>
<td>2019-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/37669" target="_blank">Full Instance Monitoring</a></td>
</tr>
</tbody></table>


## November 2019
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tbody><tr>
<td>Supported health score and health report</td>
<td>The health score is used as a measure of the overall health of a database instance to show its health status. The health report feature can routinely perform health checks on the database instance and output the corresponding health reports for the specified time period.</td>
<td>2019-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36042" target="_blank">Health Report</a></td>
</tr>
<tr>
<td>Supported instance dashboard</td>
<td>The instance dashboard feature displays the summary of your instances. You can view information such as task execution, region distribution, real-time performance, and health assessment of all connected instances, which helps you stay up to date with all your database instances.</td>
<td>2019-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36032" target="_blank">Instance Overview</a></td>
</tr>
<tr>
<td>Supported SQL optimization</td>
<td>The SQL optimization feature allows you to optimize SQL statements in just a few clicks and provides the corresponding execution plan interpretation and optimization advice.</td>
<td>2019-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36040" target="_blank">SQL Optimization</a></td>
</tr>
<tr>
<td>Supported real-time session</td>
<td>The real-time session feature supports viewing real-time session information of the current instance, including performance and connection monitoring, running threads, and online killed sessions.</td>
<td>2019-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36037" target="_blank">Real-Time Session</a></td>
</tr>
<tr>
</tbody></table>


## August 2019
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tbody><tr>
<td>Supported audit log analysis (formerly SQL insight)</td>
<td>The audit log analysis feature can carry out in-depth SQL analysis for a database instance. It can collect the statistics of, sample, and aggregate all SQL statements and their execution information based on the audit logs generated by the database within a specified time period. <br>It analyzes the SQL performance based on the execution plan result, comprehensive resource consumption, sizes of scan set and result set, and index usage rationality of the aggregated SQL statements. Then, it provides optimization advice for poorly performing SQL statements by taking into account the index conditions and database/table design.</td>
<td>2019-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36041" target="_blank">Audit Log Analysis (Formerly SQL Insight)</a></td>
</tr>
<tr>
<td>Supported exception diagnosis</td>
<td>Exception diagnosis provides real-time and historical views. The exception diagnosis feature provides you with real-time performance monitoring, health checks, and failure diagnosis and optimization, so that you can intuitively know the real-time operation status of database instances, locate newly appeared performance exceptions in real time, and optimize the system based on the optimization suggestions.</td>
<td>2019-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36036" target="_blank">Exception Diagnosis</a></td>
</tr>
<tr>
<td>Supported slow SQL analysis</td>
<td>The slow SQL analysis feature calculates, samples, and aggregates records and execution information (source information, number of executions, execution duration, etc.) of slow SQL statements on the instance.<br>Slow SQL analysis analyzes the performance of slow SQL statements based on the execution plan, comprehensive resource consumption, sizes of scan and result sets, and index usage rationality of the aggregated SQL statements and provides optimization suggestions.</td>
<td>2019-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36038" target="_blank">Slow SQL Analysis</a></td>
</tr>
<tr>
<td>Supported disk space analysis</td>
<td>Using the space analysis, you can view the instance capacity utilization, including the sizes of data and log capacities, the daily increase in capacity utilization, the estimated number of available days, and the capacity used by tablespaces under the instance.</td>
<td>2019-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36039" target="_blank">Space Analysis</a></td>
</tr>
</tbody></table>

