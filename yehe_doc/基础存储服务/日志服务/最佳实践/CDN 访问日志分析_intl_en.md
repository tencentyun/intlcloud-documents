## Overview

[Content Delivery Network (CDN)](https://console.cloud.tencent.com/cdn) is a very important internet infrastructure. It allows users to access various images, videos and other resources on the network quickly. During the access process, CDN will generate a large amount of log data. Through the analysis of CDN access logs, users can mine a large amount of useful information for CDN quality and performance analysis, error diagnosis, client distribution analysis, and user behavior analysis.

## Prerequisites

CDN logs have been collected to the Cloud Log Service (CLS). For more information, please see [operation details](https://intl.cloud.tencent.com/document/product/228/35380).


## Scenarios

### Traditional CDN log analysis

At present, CDN service providers usually provide basic monitoring metrics in real time, such as the number of requests, bandwidth, and other information. However, in many specific analysis scenarios, these default real-time metrics may not be sufficient for custom analysis requirements. Usually, users will download raw CDN logs for offline in-depth analysis and mining.

In that case, users need to set up offline analysis clusters themselves, not only requiring a lot of OPS and development costs and manpower but also making it difficult to guarantee the timeliness of offline logs in some analysis scenarios such as CDN log-based alarm reporting and troubleshooting.

### CDN-to-CLS solution

Interconnect Tencent Cloud CDN and CLS so that users can ship CDN data to CLS in real time to further use the search and SQL analysis capabilities of CLS to meet users' personalized real-time log analysis needs in different scenarios:
- Push-button log shipping
- Analyzing tens of billions of log data entries within seconds
- Visualizing real-time logs on dashboards
- Real-time alarm reporting in 1 minute

#### Introduction to CDN logs

CDN log fields are described as follows.

| Log Field      | Raw Log Type | Log Service Type | Description                                                         |
| ------------- | ------------ | ------------ | ------------------------------------------------------------ |
| app_id        | Integer      | long         | Tencent Cloud account `APPID`                                             |
| client_ip     | String       | text         | Client IP                                                    |
| file_size     | Integer      | long         | File size                                                     |
| hit           | String       | text         | Cache hit/miss. Both hits on CDN edge servers and parent nodes are marked as hit |
| host          | String       | text         | Domain name                                                         |
| http_code     | Integer      | long         | HTTP status code                                                  |
| isp           | String       | text         | ISP                                                       |
| method        | String       | text         | HTTP method                                                  |
| param         | String       | text         | Parameter carried in URL                                               |
| proto         | String       | text         | HTTP protocol identifier                                                |
| prov          | String       | text         | ISP province                                                   |
| referer       | String       | text         | Referer information, i.e., HTTP source address                                 |
| request_range | String       | text         | Range parameter, i.e., request range                                         |
| request_time  | Integer      | long         | Response time (in milliseconds), which refers to the time it takes for a node to return all packets to the client after receiving a request.|
| request_port  | String      | long         | A port connecting the client and CDN nodes. This field will be displayed as `-` if the port does not exist. |
| rsp_size      | Integer      | long         | Number of returned bytes                                                   |
| time          | Integer      | long         | Request timestamp in UNIX format (in seconds)                                        |
| ua            | String       | text         | `User-Agent` information                                              |
| url           | String       | text         | Request path                                                     |
| uuid          | String       | text         | Unique request ID                                               |
| version       | Integer      | long         | CDN real-time log version                                                    |

#### CDN quality monitoring

##### Scenario 1: monitor CDN access latency and report an alarm when a specified threshold is exceeded

It is more accurate to use percentiles (such as 99% highest latency) in mathematical statistics as alarm trigger conditions. If average or individual values are used as alarm trigger conditions, the latency of some individual requests will be averaged, failing to reflect the actual situation. For example, you can use the following query analysis statement to calculate the average latency of each minute, the latency of the 50th percentile, and the latency of the 90th percentile in a one-day window (1,440 minutes).
```sql
* | select avg(request_time) as l, approx_percentile(request_time, 0.5) as p50, approx_percentile(request_time, 0.9) as p90, time_series(__TIMESTAMP__, '5m', '%Y-%m-%d %H:%i:%s', '0') as time group by time order by time desc limit 1440
```

If the latency of the 99th percentile is greater than 100 ms, an alarm is reported and the affected domain name, URL, and client IP are included in the alarm information to facilitate fault locating. The alarm setting statement is as follows:
```sql
* | select approx_percentile(request_time, 0.99) as p99
```

By configuring multidimensional analysis, you can include the affected domain name, URL, and client IP in the alarm information to help developers in fault locating.

Once an alarm is triggered, users can obtain key information via WeChat, WeCom, and SMS.



##### Scenario 2: monitor resource access errors and report an alarm when the period-on-period increase exceeds a specified threshold

When the number of page access errors surges, it is possible that the CDN backend server fails or is overloaded with requests. You can set an alarm to monitor the increase in the number of request errors in a certain period of time (e.g., 1 minute). When the period-on-period increase exceeds a certain threshold, an alarm is reported.

**Number of errors in the recent minute**
```sql
* | select * from (select * from (select * from (select date_trunc('minute', __TIMESTAMP__) as time,count(*) as errct where http_code>=400 group by time order by time desc limit 2)) order by time desc limit 1)
```

**Number of errors in the last minute**
```sql
* | select *  from (select * from (select * from (select date_trunc('minute', __TIMESTAMP__) as time,count(*) as errct where http_code>=400 group by time order by time desc limit 2)) order by time asc limit 1)
```

The trigger condition in the alarm policy is configured as follows: Number of errors in the recent minute – Number of errors in the last minute > Specified threshold.
```
$2.errct-$1.errct >100
```




#### CDN quality and performance analysis

CDN logs contain rich content, enabling users to conduct comprehensive statistics and analysis of the overall quality and performance of CDN from multiple dimensions.
- Health
- Cache hit rate
- Average download speed
- ISPs' download count, download traffic, and download speed
- Response latency

##### Health

Calculate the percentage of requests whose `http_code` is less than 500 of all requests.
```sql
* | select round(sum(case when http_code<500 then 1.00 else 0.00 end) / cast(count(*) as double) * 100,1) as "Health"
```


##### Cache hit rate

Calculate the percentage of requests whose `return_code` is less than 400 of requests whose value of `hit` is `hit`.
```sql
http_code<400 | select round(sum(case when hit='hit' then 1.00 else 0.00 end) / cast(count(*) as double) * 100,1) as "Cache hit rate"
```


##### Average download speed

Divide the total downloads over a period of time by the total elapsed time to get the average download speed.
```sql
* | select sum(rsp_size/1024.0) / sum(request_time/1000.0) as "Average download speed (KB/s)"
```



##### ISPs' download count, download traffic, and download speed

Use the `ip_to_provider` function to convert `client_ip` to the corresponding ISP.
```sql
* | select ip_to_provider(client_ip) as isp , sum(rsp_size)* 1.0 /(sum(request_time)+1) as "Download speed (KB/s)" , sum(rsp_size/1024.0/1024.0) as  "Total download amount (MB)",  count(*) as c   group by  isp  order by c desc  limit 10
```


##### Response latency

Collect access latency statistics by window, and appropriate latency time windows can be divided according to the actual situation of the application.
```sql
* | select case when request_time < 5000 then  '~5s'  when request_time < 6000 then '5s~6s'  when request_time < 7000 then '6s~7s' when request_time < 8000 then '7~8s' when request_time < 10000 then '8~10s' when request_time < 15000 then '10~15s' else '15s~' end as  latency , count(*) as count group by latency
```


#### CDN quality and performance analysis

Access errors have always been an important factor that affects service experience. When an access error occurs, you need to quickly locate the following information of the error: QPS and the proportion, domain name and URI that are affected the most, whether the error is region or ISP related, and whether the error is caused by the newly published version.

**Solutions**

Check the distribution of 4xx and 5xx errors.
```
* |  select  http_code , count(*) as c where http_code >= 400 group by http_code order by c  desc 
```

As shown in the figure blow, a 404 error occurs, indicating that the accessed file or content does not exist. In this case, it is necessary to check whether the resource has been deleted or terminated.


For requests whose `http_code` is greater than 400, we conduct multidimensional analysis, for example, sorting requests by domain name and URL separately in descending order, checking error counts by province and ISP, and checking client distribution.
**Sort requests by domain name**
```sql
* |  select  host , count(*) as count where http_code > 400   group by host  order by count desc limit 10 
```

**Sort requests by URL**
```sql
* |  select  url , count(*) as count where http_code > 400   group by url  order by count desc limit 10 
```

**Check error counts by province and ISP**
```sql
* | select client_ip, ip_to_province(client_ip) as "province", ip_to_provider(client_ip) as  "ISP" , count(*) as "Error count"  where http_code >= 400 group by client_ip   order by "Error count" DESC limit 100
```

**Check client distribution**
```sql
* | select ua as "Client version", count(*) as "Error count" where http_code > 400 group by ua order by "Error count" desc limit 10
```



As shown in the figure, all errors occurred on the Safari client. Fault locating finds that the error is caused by a bug in the new version, which causes frequent failure to access resources via the Safari browser window.


#### User behavior analysis

**Requirements**
- Where do most users come from, internally or externally?
- What are the most popular resources for users?
- Are there users who download massive resources frequently, and does the behavior meet expectations?

**Solutions**
- Analyzing access sources
```sql
* | select ip_to_province(client_ip) as province ,  count(*) as c group by province order by c desc limit 50
```

- Analyzing top access URLs
```sql
http_code < 400 | select url ,count(*) as  "Access count", round(sum(rsp_size)/1024.0/1024.0/1024.0, 2) as "Total download amount (GB)" group by url order by "Access count" desc limit 100
```

- Analyzing top domain names in terms of traffic (volume of data downloaded)
```sql
* | select host, sum(rsp_size/1024) as  "Total download amount" group by host order by  "Total download amount"  desc  limit 100
```

- Analyzing top users in terms of download amount
```sql
* | SELECT CASE WHEN ip_to_country(client_ip)='Hong Kong (China)' THEN concat(client_ip, ' ( Hong Kong )') WHEN ip_to_province(client_ip)='' THEN concat(client_ip, ' ( Unknown IP )') WHEN ip_to_provider(client_ip)='Private IP' THEN concat(client_ip, ' (Private IP )') ELSE concat(client_ip, ' ( ', ip_to_country(client_ip), '/', ip_to_province(client_ip), '/', if(ip_to_city(client_ip)='-1', 'Unknown city', ip_to_city(client_ip)), ' ',ip_to_provider(client_ip), ' )') END AS client, pv as "Total access count", error_count as "Error access count" , throughput as "Total download amount (GB)"  from  (select  client_ip , count(*) as pv, round(sum(rsp_size)/1024.0/1024/1024.0, 1) AS throughput , sum(if(http_code  > 400, 1, 0)) AS error_count from log   group by client_ip order by throughput desc limit 100)
```

- Analyzing top users with valid access
```sql
* | SELECT CASE WHEN ip_to_country(client_ip)='Hong Kong (China)' THEN concat(client_ip, ' ( Hong Kong )') WHEN ip_to_province(client_ip)='' THEN concat(client_ip, ' ( Unknown IP )') WHEN ip_to_provider(client_ip)='Private IP' THEN concat(client_ip, ' (Private IP )') ELSE concat(client_ip, ' ( ', ip_to_country(client_ip), '/', ip_to_province(client_ip), '/', if(ip_to_city(client_ip)='-1', 'Unknown city', ip_to_city(client_ip)), ' ',ip_to_provider(client_ip), ' )') END AS client, pv as  "Total access count", (pv - success_count)  as "Error access count" , throughput as "Total download amount (GB)"  from  (select  client_ip , count(*) as pv, round(sum(rsp_size)/1024.0/1024/1024.0, 1) AS throughput , sum(if(http_code  < 400, 1, 0)) AS success_count from log   group by client_ip order by success_count desc limit 100)
```

- Analyzing access PVs and UVs (access count within a certain period of time and independent client IP change trend)
```sql
* | select time_series(__TIMESTAMP__, '1m', '%Y-%m-%dT%H:%i:%s+08:00', '0') as time, count(*) as pv,approx_distinct(client_ip) as uv group by time order by time limit 1000
```


