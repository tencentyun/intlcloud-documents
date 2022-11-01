
## Overview
NGNIX is a common reverse proxy server that handles a lot of service requests in actual businesses. It will produce a large number of scattered logs and massive data within clusters. Therefore, it is very important to collect and manage log data effectively, which benefits the business OPS and operations. This document describes how to access NGNIX logs through CLS.

#### NGNIX log format

You can run the log_format command to define the format of NGINX logs (access.log). The definition of each field and how to configure the index in default format are as follows.

```plaintext
log_format  main  '$remote_addr - $remote_user [$time_local] "$request"'
                      '$status $body_bytes_sent "$http_referer"'
                      '"$http_user_agent" "$http_x_forwarded_for"';
```

The fields are defined as follows:

| Field Name               | Description                                                 |
| -------------------- | ---------------------------------------------------- |
| remote_addr          | Client IP address                                         |
| remote_user          | Client name                                           |
| time_local           | Local server time                                       |
| method               |HTTP request method                                        |
| url                  | URL                                             |
| protocol             | Protocol type                                             |
| status               | HTTP request status code                                      |
| body_bytes_sent      | Number of bytes sent to client                                 |
| http_referer         | Access source page URL                               |
| http_user_agent      | Client browser information                                     |
| http_x_forwarded_for | Actual client IP address when the frontend has a proxy server |

## Directions

#### 1. Create a log topic

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls), On the left sidebar, click **Log Topic** to go to the log topic management page.
2. Select a region and click **Create Log Topic**.
3. In the pop-up window, enter information and click **OK**.
For example, create a log topic named **nginx_access**. The created log topic is displayed on the log topic list.


#### 2. Create a machine group

>?We recommend using the CLS collector to collect logs from the NGINX cluster. For more information about how to download and install the collector, see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).
>

1. On the left sidebar, click **Machine Group** to go to the management page.
2. Select the desired region and click **Create Machine Group**
3. In the pop-up window, enter information and click **OK**.
For example, create a machine group named **nginx_group**.
Multiple IPs can be input in a machine group (one IP per line). For CVM instances, please input the private IP addresses directly. For more information, please see [Machine Group Management](https://intl.cloud.tencent.com/document/product/614/17412).


#### 3. Configure LogListener

1. On the left sidebar, click **Log Topic** to go to the log topic management page.
2. Click the desired log topic ID/name to go to the log topic management page.
3. Select the **Collection Configuration** tab to specify the collection path, bound machine group, and parsing mode.
>? The following describes how to collect logs using LogListener. For more information, please see [Collection Methods](https://intl.cloud.tencent.com/document/product/614/12502).
>
 - Set the log path and bind the log topic to a machine group
For example, set the target collection path to the local log path `/usr/local/webserver/nginx/logs/access.log`, and bind the log topic to the machine group nginx_group. The settings are shown in the following figure.

 - Extract the key-value
Set the key-value extraction mode to [Full Regular Expression](https://intl.cloud.tencent.com/document/product/614/31654), enter a log sample, and verify the regular expression for extraction rule.
For example, log_format of the NGINX access log is defined as follows:
```shell
log_format  main  '$remote_addr - $remote_user [$time_local] "$request"'
                      '$status $body_bytes_sent "$http_referer"'
                      '"$http_user_agent" "$http_x_forwarded_for"';
```
A complete sample of the NGINX access log is as follows:
```shell
59.x.x.x - - [06/Aug/2019:12:12:19 +0800] "GET /nginx-logo.png HTTP/1.1" 200 368 "http://119.x.x.x/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/75.0.3770.142 Safari/537.36" "-"
```
The corresponding regular expression for key-value extraction is as follows:
```shell
(\S+)\s\S+\s(\S+)\s\[([^\]]+)\]\s\"([^\"]+)\s(\S+)\s([^\"]+)\"\s(\d+)\s(\d+)\s\"([^\"]+)\"\s\"([^\"]+)\"\s\"([^\"]+)\"$
```
After the regular expression for extraction passes verification, name a key-value for each field:


#### 4. Configure indexes

1. On the left sidebar, click **Log Topic** to go to the log topic management page.
2. Click the desired log topic ID/name to go to the log topic management page.
3. Click the **Index Configuration** tab and configure the corresponding index field based on the definition of the NGINX log format fields.



#### 5. Query NGINX logs

1. On the left sidebar, click **Search and Analysis** to go to the search and analysis page.
2. Click the drop-down lists of **Logset** and **Log Topic** to select the log topic to be searched.

3. Click **Log Time**, select a log time for search, and click **Search and Analysis** to query NGINX access logs.
