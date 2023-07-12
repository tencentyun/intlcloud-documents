## Overview

NGINX is a high-performance HTTP and reverse proxy server. By analyzing NGINX logs, you can obtain various valuable results, such as data support for website diagnosis and tuning, website stability monitoring, and operations statistics. This document introduces how to use CLS to comprehensively mine NGINX log data.


## Prerequisites

- NGINX logs have been collected to CLS. For more information, please see [Collecting and Searching NGINX Access Logs](https://intl.cloud.tencent.com/document/product/614/32939).
- This document uses standard NGINX log configuration:
```
log_format  main  '$server_name $remote_addr - $remote_user [$time_local] "$request" '
                        '$status $uptream_status $body_bytes_sent "$http_referer" '
                        '"$http_user_agent" "$http_x_forwarded_for" ';
```

## Scenarios

### Diagnosis and tuning

#### Requirement description

Tune pages with high access latency to improve user experience.

#### Solution

- Calculate the average latency and highest latency of requests every 5 minutes to understand the overall latency situation.
```
* | select time_series(__TIMESTAMP__, '5m', '%Y-%m-%d %H:%i:%s', '0')  as time, avg(request_time) as avg_latency ,max(request_time) as max_latency group by time order by time limit 1000
```

- Find out the request page corresponding to the highest request latency and further optimize the response speed of the page.
```
* | select time_series(__TIMESTAMP__, '5m', '%Y-%m-%d %H:%i:%s', '0')  as time, max_by(request_uri,request_time) group by time order by time limit 1000
```

- Tune the page with the highest access latency.
For example, the **/4nm8c.html** page has the highest access latency and needs to be tuned. To tune the page, you need to calculate the page access PV, UV, request method statistics, request status statistics, browser statistics, average access latency, and highest access latency.
```
request_uri:"/4nm8c.html*" | select count(1) as pv,
        approx_distinct(remote_addr) as uv,
        histogram(method) as method_pv,
        histogram(status) as status_pv,
        histogram(user_agent) as user_agent_pv,
        avg(request_time) as avg_latency,
        max(request_time) as max_latency
```


### Monitoring website stability

#### Requirement description

In terms of performance problems, website errors, and traffic slump or surge, you can detect problems before users based on threshold-based log monitoring.

#### Solution

It is more accurate to use percentiles (such as highest latency of the 99% percentile) in mathematical statistics as alarm trigger conditions. If average or individual values are used as alarm trigger conditions, the latency of some individual requests will be averaged, failing to reflect the actual situation. For example, you can use the following query analysis statement to calculate the average latency of each minute, the latency of the 50th percentile, and the latency of the 90th percentile in a one-day window (1,440 minutes).
```
* | select avg(request_time) as l, approx_percentile(request_time, 0.5) as p50, approx_percentile(request_time, 0.9) as p90, time_series(__TIMESTAMP__, '5m', '%Y-%m-%d %H:%i:%s', '0') as time group by time order by time desc limit 1440
```

The system will report alarms when the latency of the 99th percentile is greater than 100 ms and display the affected URLs and users affected in the alarm information. In this way, you can quickly understand the error situation.
```
* | select approx_percentile(request_time, 0.99) as p99
```

When receiving the alarm information, you can find out the top affected URLs and users and make targeted alarm recovery measures accordingly.


### Analyzing website access information

With CLS, you can build an operations data dashboard to quickly analyze website access information such as access PV/UV statistics, access geographic information statistics, top 10 access sources, and top 10 access addresses.

- Collect statistics on the access IP sources of the recent day
```
* | select count(1) as c, ip_to_province(remote_addr) as address group by address limit 100
```

- Display the top 10 access source pages with the highest PV value of the recent day to get the hot pages
```
* | select count(1) as pv , http_referer  group by http_referer order by pv desc limit 10
```
![image-20210823212306355](https://main.qcloudimg.com/raw/4a73e9cda0bedfa8c8454f10827326b3.png)
- Display the PV and UV statistics of the recent day
```
*| select approx_distinct(remote_addr) as uv ,count(1) as pv , time_series(__TIMESTAMP__, '5m', '%Y-%m-%d %H:%i:%s', '0')  as time group by time order by time limit 1000
```




