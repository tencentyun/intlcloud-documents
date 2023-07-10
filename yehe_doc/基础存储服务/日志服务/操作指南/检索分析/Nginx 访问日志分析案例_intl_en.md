## Introduction

Ngnix is a common reverse proxy server that handles a lot of service requests in actual businesses. It will produce a large number of scattered logs and massive data within clusters. Therefore, it is very important to collect and manage log data effectively, which benefits the business OPS and operations. This document describes how to analyze Ngnix logs through CLS.

#### Ngnix log format

The format of Ngnix access log (access.log) can be defined using the `log_format` field in the Ngnix configuration file “/etc/nginx/nginx.conf”, as shown below.

```shell
log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                  '$status $body_bytes_sent $request_time "$http_referer" '
                  '"$http_user_agent" "$http_x_forwarded_for" "$msec"';
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
| body_bytes_sent      | Number of bytes sent to client                                 |
| request              | Request response time, in seconds                               |
| http_referer         | Access source page URL                               |
| http_user_agent      | Client browser information                                     |
| http_x_forwarded_for | Tracking and recording of actual client IP address when the frontend has a proxy server |
| msec                 | Log written time, in seconds. It’s in the format of UNIX timestamp accurate to the millisecond level      |

>!To use the CLS analysis feature, the key-value index of statistical fields must be configured, with statistics enabled.
>
The index configuration takes effect in about 1 minute. The new configuration is only effective for log data written subsequently.



## Sample SQL Analysis

#### Bandwidth curve

```plaintext
* | select HISTOGRAM(CAST(msec*1000 AS TIMESTAMP), INTERVAL 1 MINUTE) AS dt, round(SUM(body_bytes_sent)*8/1000.0, 2) AS "Bandwidth(Kb/min)" group by dt order by dt limit 50
```



#### Average download speed

```plaintext
* | select HISTOGRAM(CAST(msec*1000 AS TIMESTAMP), INTERVAL 1 MINUTE) AS dt, round(SUM(body_bytes_sent) * 1.0 / SUM(request_time),2) AS "Download speed(KB/s)" group by dt order by dt limit 50
```



#### UV

```plaintext
* | select HISTOGRAM(CAST(msec*1000 AS TIMESTAMP), INTERVAL 1 MINUTE) AS dt, count(distinct(remote_addr)) as uv group by dt order by dt limit 50
```



#### PV

```plaintext
* | select HISTOGRAM(CAST(msec*1000 AS TIMESTAMP), INTERVAL 1 MINUTE) AS dt, count(*) as pv group by dt order by dt limit 50
```



#### Request type distribution

```plaintext
* | select HISTOGRAM(CAST(msec*1000 AS TIMESTAMP), INTERVAL 1 MINUTE) AS dt, count(*) as pv, method group by dt, method order by dt limit 200
```

Status code ratio

```plaintext
* | select count(*) as count, status where url like 'http://console.cloud.tencent.com/cls/sql/index1%' group by status
```



#### Top URL

```plaintext
* | select request_url as "t-url", count(*) as count group by request_url order by count desc limit 10
```


