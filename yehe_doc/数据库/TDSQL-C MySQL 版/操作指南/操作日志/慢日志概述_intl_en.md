## Overview
Slow logs are also called slow SQL queries. They are a type of logs provided by TDSQL-C for MySQL to record SQL statements with a longer response time than the threshold in the database process. Specifically, SQL statements with a longer execution time than the `long_query_time` value are recorded in slow logs.
>?The slow log feature is currently in beta test and only available in Beijing region. It will be made available in more regions.

## Parameters
The `long_query_time` value of TDSQL-C for MySQL defaults to 10, indicating that SQL statements running more than 10 seconds will be recorded in slow logs. You can adjust the value in the range of 0.000000 to 3,600.000000. For more information, see [Setting Instance Parameters](https://intl.cloud.tencent.com/document/product/1098/44602).

## Purpose
After setting this parameter in TDSQL-C for MySQL, you can identify and optimize inefficient SQL statements. Simply put, slow logs are used to troubleshoot SQL statement issues and check the current performance.

## Relevant operations
<table>
<thead><tr><th>Operation</th><th>Use Case</th><th>Method</th></tr></thead>
<tbody>
<tr>
<td>Prevent slow logs from being generated</td><td>Get suggestions from DBbrain for slow SQL statement optimization.</td><td>-</td></tr>
<tr>
<td>Set slow log parameters</td><td>Set the value of `long_query_time` to record slow logs.</td><td><a href="https://intl.cloud.tencent.com/document/product/1098/44602" target="_blank">Setting Instance Parameters</a></td></tr>
<tr>
<td>View slow log monitoring alarms</td><td>View slow instance queries through the instance monitoring metric (Slow Queries) and set alarms to receive notifications.</td><td><a href="https://intl.cloud.tencent.com/document/product/1098/44597" target="_blank">Alarm Policies (Cloud Monitor)</a></td></tr>
<tr>
<td>Query and download slow log details</td><td>On the **Operation Log** page, query the following slow log information: execution time, SQL statement, client address, username, database, execution duration (s), lock duration (s), parsed rows, and returned rows. You can download them in CSV or native formats.</td><td><a href="https://intl.cloud.tencent.com/document/product/1098/48375" target="_blank">Querying and Downloading Slow Log Details</a></td></tr>
<tr>
<td>Analyze and optimize slow logs</td><td>View the complete SQL template, SQL sample, and optimization suggestion and description through DBbrain to analyze and optimize SQL statements.</td><td><a href="https://intl.cloud.tencent.com/document/product/1035/36038" target="_blank">Slow SQL Analysis</a></td></tr>

