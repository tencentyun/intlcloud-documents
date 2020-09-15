## Overview

NGINX is a common reverse proxy server that handles a lot of service requests in actual businesses. It will produce scattered logs and massive data within clusters. Therefore, it is very important to collect and manage log data effectively. This document describes how to analyze NGINX access logs through CLS.

#### NGINX log format

The format of NGINX access log (access.log) can be defined using the `log_format` field.

```shell
log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                  '$status $body_bytes_sent $request_time "$http_referer" '
                  '"$http_user_agent" "$http_x_forwarded_for"';
```

The fields are defined as follows:

| Field Name               | Description                                                 |
| -------------------- | ------------------------------------------------------ |
| remote_addr          | Client IP address                                         |
| remote_user          | Client name                                           |
| time_local           | Local server time                                       |
| method               | HTTP request method                                        |
| url                  | URL                                             |
| protocol             | Protocol type                                             |
| status               | HTTP request status code                                      |
| body_bytes_sent       | Number of bytes sent to client                                 |
| request              | Request response time, in seconds                               |
| http_referer         | Access source page URL                               |
| http_user_agent      | Client browser information                                     |
| http_x_forwarded_for | Tracking and recording of actual client IP address when the frontend has a proxy server |

#### Prerequisites: key-value index configured

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls/overview?region=ap-guangzhou), and click **Logset** on the left sidebar to enter the **Logset Management** page. Click the ID/Name of the logset that stores NGINX logs to enter its details page.
2. Locate the log topic and click **Manage** in the **Operation** column. Click the **Index Configuration** tab and configure **Key-Value Index** based on the definition of the NGINX log format fields.
3. Enable statistics for specified fields to support SQL analysis.


>!The index configuration takes effect in about 1 minute. The new configuration is only effective for log data written subsequently.



## Sample SQL Analysis

#### Bandwidth curve

```sql
* | select HISTOGRAM(CAST(time_iso8601 AS TIMESTAMP), INTERVAL 1 MINUTE) AS dt, round(SUM(body_bytes_sent)*8/1000.0, 2) AS "Bandwidth( Kb/min)" group by dt order by dt limit 50
```



#### Average download speed

```sql
* | select HISTOGRAM(CAST(time_iso8601 AS TIMESTAMP), INTERVAL 1 MINUTE) AS dt, round(SUM(body_bytes_sent) * 1.0 / SUM(request_time),2) AS "Download speed (KB/sec)" group by dt order by dt limit 50
```



#### uv

```sql
* | select HISTOGRAM(CAST(time_iso8601 AS TIMESTAMP), INTERVAL 1 MINUTE) AS dt, count(distinct(remote_addr)) as uv group by dt order by dt limit 50
```



#### pv

```sql
* | select HISTOGRAM(CAST(time_iso8601 AS TIMESTAMP), INTERVAL 1 MINUTE) AS dt, count(*) as pv group by dt order by dt limit 50
```



#### Request type distribution

```sql
* | select HISTOGRAM(CAST(time_iso8601 AS TIMESTAMP), INTERVAL 1 MINUTE) AS dt, count(*) as pv, method group by dt, method order by dt limit 200
```


Status code ratio

```sql
* | select count(*) as count, status where url like 'http://console.cloud.tencent.com/cls/sql/index1%' group by status
```



#### Top URL

```sql
* | select request_url as "t-url", count(*) as count group by request_url order by count desc limit 10
```


