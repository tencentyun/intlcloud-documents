[Cloud Load Balancer (CLB)](https://console.cloud.tencent.com/clb/overview) is a product of hundreds of billions of QPS and relies heavily on refined operation. Access logs provided by Cloud Log Service (CLS) are key to refined operation. You can go to [CLB > Access Logs](https://console.cloud.tencent.com/clb/log) to mine the value of massive amounts of access log data. By analyzing access logs, you can monitor client requests, troubleshoot issues, and analyze user behaviors to provide data support for refined operation. This document introduces how to use CLS to analyze CLB access logs.

## Example: OPS Monitoring Scenario

Jack is in charge of the OPS of the advertising platform of an internet business. He received feedback from an advertising partner complaining that, when users click on an advertisement on the platform, the advertisement opens very slowly. The advertising partner has high requirements for timeliness and stability and proposed that if the service experiences an exception, an alarm should be generated within 1 minute and solved within 5 minutes. To meet this requirement, CLB logs can be used to implement the following capabilities:
- Monitor client access latency and exceptional requests, and report alarms when the specified threshold is exceeded.
- When there are alarms, the following additional information is provided to help you determine fault causes:
  - Websites, LB instances, and real server (RS) instances that the requests whose latency exceeds the specified threshold access
  - Access latency statistics of the LB and RS instances

## OPS Monitoring Solution

Based on the 1-minute real-time alarms and multidimensional analysis capabilities of CLS, you can quickly monitor CLB access logs to locate and rectify faults.

### Step 1. Enable the feature of shipping CLB access logs to CLS

1. Log in to the [CLB console](https://console.cloud.tencent.com/clb/overview).
2. On the left sidebar, choose **Instance Management** to go to the instance management page.
3. Click a CLB ID/name to go to the CLB management page.
4. Locate and enable **Cloud Log Service (CLS)**, as shown in the following figure.
For more information, please see [Configuring Access Logs](https://intl.cloud.tencent.com/document/product/214/35063).



### Step 2. Configure the client access latency statistics and alarm policy

- Client access latency statistics
```
* | select time_series(__TIMESTAMP__, '1m', '%Y-%m-%d %H:%i:%s', '0')  as time, round(avg(request_time)*1000,2) as "Average access latency" group by time order by time limit 1000
```
- Error request statistics
```
status:>200 | select time_series(__TIMESTAMP__, '1m', '%Y-%m-%d %H:%i:%s', '0')  as time, status, count(1) group by time,status order by time limit 1000
```



- Configure an alarm policy to detect alarms whose average latency per minute is higher than a specified threshold

- Configure multidimensional analysis in the alarm policy to obtain additional information when an alarm occurs
  - Access latency statistics of the LB and RS instances
  - Websites, LB instances, and real server (RS) instances that the requests whose latency exceeds the specified threshold access



- Configure notification channels. The following channels are supported:
 - Email
 - SMS
 - WeChat
 - WeCom
 - Phone
 - Custom API callback


### Step 3. Receive alarms and perform quick fault locating

Once an alarm is triggered, you can receive alarm information and details through channels such as WeChat, WeCom, SMS, and phone.

Alarm details include information such as affected RS and LB instances.


It can be seen that the average latency of LB instances is relatively high and the LB instance most affected is `9.*****.1`. In this way, Jack can quickly locate the exceptional LB instance and restore it. The entire process takes only 1 minute.

## Example: Operations Statistics Scenario

Jane, responsible for operating a technology content app, needs to plan an offline salon next month to increase the stickiness of existing users and take the opportunity to promote products and attract new users. Due to the short preparation time and limited funds, in order to achieve the KPI target, Jane lists the following information that needs to be obtained:
- Where to hold the offline salon: it is necessary to understand the geographical sources of visiting customers and the geographical locations of key customer groups.
- What is the theme of salon: collect statistics on the top ranking of hot websites to understand which content users pay more attention to
- Which clients are currently used by users to access CLS: design the landing page according to the current client distribution.
- Which channels should the landing page be placed: collect statistics on the request sources of the current website to find out the diversion entries with high traffic and use them as the key areas for advertising.

## Operations Statistics Solution

Analyzing CLB access logs helps Jane solve operations statistics problems with ease.

### Step 1. Find out the geographical sources of visiting customers

Use the IP function provided by CLS to convert client IPs to the corresponding provinces or countries.
- Collect statistics on customer distribution by province in China
```
* | select count(1) as c, ip_to_province(remote_addr) as address group by address limit 100
```
- Collect statistics on customer distribution by country
```
* | select count(1) as c, ip_to_country(remote_addr) as address group by address limit 100
```



### Step 2. Sort hot websites

The `http_host` field records request domain names. By calculating the PV and UV of request domain names, you can sort out top hosts.
```
* | select http_host, count(*) as pv, approx_distinct(remote_addr) as uv group by http_host order by pv desc limit 100
```


### Step 3. Collect statistics on client distribution

```
* | select http_user_agent, count(*) group by http_user_agent
```


### Step 4. Collect statistics on the request sources of the current website

The `http_referer` records the request sources of the website.
```
* | select http_referer, count(*) as count group by http_referer order by count desc limit 100
```



## Summary

By analyzing CLB access logs, you can obtain various valuable results, such as PV and UV trends, client packet traffic statistics, status code distribution, and p99 and p95 access latency statistics. To help you quickly analyze CLB access logs, CLS and CLB have jointly created a visual analysis scheme out of the box. You can enjoy it immediately by enabling the feature of shipping CLB access logs to CLS.









