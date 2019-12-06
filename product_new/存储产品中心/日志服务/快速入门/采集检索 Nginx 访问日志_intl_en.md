
## Overview
NGINX is a common reverse proxy server that handles a high volume of service requests in actual businesses. A high number of access logs are generated when the service is running, causing such problems as scattered logs and massive data within clusters. Therefore, effective log data collection and management is highly important for business OPS. Using NGINX access logs as an example, this document describes how to access NGINX logs through CLS.

#### NGINX log format

You can run the log_format command to define the format of NGINX logs (access.log). The definition of each field and how to configure the index in default format are as follows.

```shell
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
| http_x_forwarded_for | Tracking and recording of actual client IP address when the frontend has a proxy server |

## Directions

#### 1. Creating a logset and a log topic

(1) Log in to the [CLS Console](https://console.cloud.tencent.com/cls). Click **Logset Management** in the left sidebar to enter the logset management page.
(2) On the top of the page, select a region, then click **Create Logset** to create a logset. For example, create a logset named nginx_project.
(3) Click **Logset Name** to enter the log topic management page.
(4) Click **Add Log Topic** and create a log topic. For example, create a log topic named nginx_access. The created log topic is displayed in the log topic list.


#### 2. Creating a server group

>We recommend using the CLS collector to collect logs from the NGINX cluster. For more information about how to download and install the collector, see [Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).

(1) In the left sidebar in the console, click **Server Group Management** to enter the server group management page.
(2) On the top of the page, select a region, then click **Create Server Group** to create a server group named nginx_group. You can enter multiple server IP addresses for one server group, one IP address per row. For Cloud Virtual Machine (CVM), you can enter private IP addresses. For more information, see [Server Group Management](https://intl.cloud.tencent.com/document/product/614/17412).


#### 3. Configuring a collection rule

(1) In the left sidebar in the console, click **Logset Management**, then enter the management page for the created logset and log topic respectively.
(2) On the log topic management page, click **Collection Configuration**, specify a collection path and parsing mode for the log topic, and bind the log topic to a server group.
- Set the log path and bind the log topic to a server group
  For example, set the target collection path to the local log path `/usr/local/webserver/nginx/logs/access.log`, and bind the log topic to the server group nginx_group. The settings are shown in the following figure.
  ![](https://main.qcloudimg.com/raw/f01e1cfa443ca8ca87da51199ed27982.png)
- Extract the key-value
  Set the key-value extraction mode to [Full RegEx](https://intl.cloud.tencent.com/document/product/614/32283), enter a log sample, and verify the regular expression for extraction rule.
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
	![](https://main.qcloudimg.com/raw/0b35a353fb98c1024ff9836e1b5ec78a.png)

#### 4. Configuring an index rule

(1) In the left sidebar in the console, click **Logset Management**, then enter the management page for the created logset and log topic respectively.
(2) On the log topic management page, click **Index Configuration**. Configure the index field on the index configuration management page based on the definition of the NGINX log format field.
![](https://main.qcloudimg.com/raw/776e9a193ec84adeabea01b229d6162d.png)

#### 5. Querying a NGINX log

(1) In the left sidebar in the console, click **Log Search** to enter the log search page. Select the corresponding logset and log topic.
(2) Click **Search** to query the NGINX log.
![](https://main.qcloudimg.com/raw/a62470cb3a3e52e8400c0d212fb2f783.png)
