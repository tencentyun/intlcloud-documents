## Overview

After the domain name is added to Content Delivery Network (CDN), the CDN node will schedule and respond to all user resource requests. To help you statistically analyze resource access, CDN connects to the Cloud Log Service (CLS) platform, and supports uploading CDN access logs to CLS in real time for multi-dimensional analysis, including quality and performance monitoring, user access analysis using Top command, and download traffic statistics.

>?CDN Real-time Log Analysis is currently in beta. To use it, you can [submit an application](https://intl.cloud.tencent.com/apply/p/f4gs2k0au1i). You application will be reviewed within seven business days.



## Log Collection

1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Log Service** in the left sidebar to enter the log service page. Click the **Real-time Log** tab.
2. Click **Create** to create a log topic.
3. Enter the name of the new log topic and select the domain names to be bound to this topic:
	- The topic name must be unique.
	- A domain name can only be bound to one log topic.
	- The configuration will take effect in about 15 minutes.
4. Log in to the [CLS Console](https://console.cloud.tencent.com/cls/) and click **Search Analysis** in the left sidebar to enter the search analysis page. Complete the following configurations:
 - Select the Shanghai region
 - Select “cdn_logset” for **Logset**
 - Select the log topic created in Step 3 for **Log Topic**
5. Click **Search Analysis** to search CDN access logs in real time.
#### Log data description
The CDN logs uploaded to CLS contain the following fields:
<table>
<thead>
<tr>
<th>Log Field</th>
<th>Raw Log Type</th>
<th>CLS Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>app_id</td>
<td>Integer</td>
<td>long</td>
<td>APPID of your Tencent Cloud account</td>
</tr>
<tr>
<td>client_ip</td>
<td>String</td>
<td>text</td>
<td>Client IP</td>
</tr>
<tr>
<td>file_size</td>
<td>Integer</td>
<td>long</td>
<td>File size</td>
</tr>
<tr>
<td>hit</td>
<td>String</td>
<td>text</td>
<td>Cache HIT/MISS. A hit in a CDN edge server or parent node will be marked as HIT</td>
</tr>
<tr>
<td>host</td>
<td>String</td>
<td>text</td>
<td>Domain name</td>
</tr>
<tr>
<td>http_code</td>
<td>Integer</td>
<td>long</td>
<td>HTTP status code</td>
</tr>
<tr>
<td>isp</td>
<td>String</td>
<td>text</td>
<td>ISP</td>
</tr>
<tr>
<td>method</td>
<td>String</td>
<td>text</td>
<td>HTTP request method</td>
</tr>
<tr>
<td>param</td>
<td>String</td>
<td>text</td>
<td>URL parameters</td>
</tr>
<tr>
<td>proto</td>
<td>String</td>
<td>text</td>
<td>HTTP protocol identifier</td>
</tr>
<tr>
<td>prov</td>
<td>String</td>
<td>text</td>
<td>ISP districts</td>
</tr>
<tr>
<td>referer</td>
<td>String</td>
<td>text</td>
<td>Referer information, i.e., HTTP source address</td>
</tr>
<tr>
<td>request_range</td>
<td>String</td>
<td>text</td>
<td>Range parameter, i.e., request range</td>
</tr>
<tr>
<td>request_time</td>
<td>Integer</td>
<td>long</td>
<td>Response time (in milliseconds), which refers to the time it takes for a node to return all packets to the client after receiving a request</td>
</tr>
<tr>
<td>rsp_size</td>
<td>Integer</td>
<td>long</td>
<td>Number of bytes returned</td>
</tr>
<tr>
<td>time</td>
<td>Integer</td>
<td>long</td>
<td>Request time, which is a UNIX timestamp</td>
</tr>
<tr>
<td>ua</td>
<td>String</td>
<td>text</td>
<td>User-Agent information</td>
</tr>
<tr>
<td>url</td>
<td>String</td>
<td>text</td>
<td>Request path</td>
</tr>
<tr>
<td>uuid</td>
<td>String</td>
<td>text</td>
<td>Unique request identifier</td>
</tr>
<tr>
<td>version</td>
<td>Integer</td>
<td>long</td>
<td>Version protocol</td>
</tr>
</tbody></table>



## Log Analysis Samples

### Overall quality analysis

#### Health log requests
```plaintext
http_code<500 | select count(*)
```


#### Average access latency
```plaintext
select ROUND(avg(request_time),2)
```


### Error diagnosis

#### Error code distribution
```plaintext
select http_code,count(*) as c group by http_code order by c desc
```


#### Querying and analyzing logs of an error code
```plaintext
http_code:403
```


