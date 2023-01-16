This document describes the capabilities and directions of database call search and analysis.

## Prerequisites
Go to the [**Database call analysis**](https://console.cloud.tencent.com/apm/monitor/query) page in the APM console.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/rw97259_1.png)

## SQL monitoring list
The SQL list on the left displays all SQL calls between the application and database in the selected time range, as well as the number of calls, duration, error rate, and DoD change of each SQL statement. You can directly locate the target SQL statement through the search bar above the list.

## SQL analysis

The SQL analysis module on the right displays the change trends of calls and response time of the currently selected SQL statement in the specified time range. The list of exceptions in the current database is displayed below the trend chart, including exception type, caller, number of exceptions, first occurrence time, and last occurrence time. You can click **View details** to view specific database exceptions or click **Trace** to view trace details.

## Exception analysis
You can switch the sub-window menu on the right to enter the exception analysis page. This page displays the list of SQL exceptions, including service exception types, APIs, and the number of exception occurrences.
