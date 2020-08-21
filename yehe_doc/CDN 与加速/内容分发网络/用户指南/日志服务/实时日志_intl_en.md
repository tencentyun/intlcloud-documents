## Feature Overview

CDN can collect and publish access logs in real time, enabling fast retrieval and analysis of log data. You can quickly access comprehensive, stable, and reliable one-stop logging services such as log collection, log storage, and log search in the CDN Console.

>? Currently, the real-time logging service of CDN is in beta. To try it out, first [activate Cloud Log Service (CLS)](https://console.cloud.tencent.com/cls), then [submit an application](https://intl.cloud.tencent.com/apply/p/f4gs2k0au1i). Applications will be reviewed within seven business days.
## Use Cases
This feature can be used to view and analyze user access in real time.

## Basic Concepts
### Logset
A logset is a project management unit in the log service. It is used to distinguish between logs of different projects and corresponds to an item or application. The CDN logset has the following basic attributes:
+ Logset name: cdn_logset
+ Region: the [region](https://intl.cloud.tencent.com/document/product/614/18940) to which a logset belongs.
+ Retention period: the retention period of data in the current logset
+ Creation time: logset creation time

### Log topic
A log topic is the basic management unit in the log service. One logset can contain multiple log topics, and one log topic corresponds to one type of application or service. We recommend you collect similar logs on different machines into the same log topic. For example, if a business project has three types of logs: operation log, application log, and access log, you can create a log topic for each type of log.

The log service system manages different log data based on different log topics. Each log topic can be configured with different data sources, index rules, and shipping rules. Therefore, a log topic is the basic unit for configuring and managing log data in the log service. You need to configure corresponding rules first after creating a log topic before you can perform log collection, search, analysis, and shipping.

Log topic features include:
- Collect logs to log topics.
- Store and manage logs based on log topics.
- Search for and analyze logs by log topics.
- Ship logs to other platforms based on log topics.
- Download and consume logs from log topics.

## Operation Guide
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), click **Log Service** on the left sidebar, and select **Real-Time Log** to access the real-time log page and create real-time log shipping.
![](https://main.qcloudimg.com/raw/d6f22b7194f2e3433f9bbee4f4e4a1dc.png)

### Creating log topic
Click **Create** to create a log topic.
>!Up to 10 log topics can be created under one logset.

![](https://main.qcloudimg.com/raw/94136aa047219848f82948e19cd8dc06.png)

### Configuring log topic
Enter the name of the new log topic and select the domain names to be bound to this topic.
>!
>- The name of the new log topic cannot be the same as the name of any existing log topic.
>- A domain name can be bound to only one log topic.
>- After the configuration information is saved, it takes about 15 minutes for the configuration to take effect.

![](https://main.qcloudimg.com/raw/6e820577732ecc679aae25386683c57e.png)

### Managing log topic
After successfully configuring a log topic, you can perform log topic management. Specifically, you can stop/start shipping logs to the log topic, search for logs in the log topic, manage the log topic, and delete the log topic.
![](https://main.qcloudimg.com/raw/46d8293f0819b693b4b17fa6a79ca78c.png)

#### Stopping/Starting log shipping
You can manually stop/start shipping logs to a log topic.
>!
>- After a log topic is stopped, all logs of the domain names bound to the log topic will no longer be shipped to it. Logs that have already been shipped to it will be retained. This operation will take effect in about 5–15 minutes.
>- After a log topic is started, all logs of the domain names bound to the log topic will be shipped to it. This operation will take effect in about 5–15 minutes.

#### Search
You can search for logs by log topic. Select a desired log topic and click **Search** to access the log search page.
+ Time Range: you can search for log data recorded today, during a 24-hour interval (one of the last 7 days), and during the last 7 days.
+ Sort: you can sort logs in descending or ascending order by log time.
+ Search: you can conduct full-text search, key-value search, and fuzzy keyword search. For more information, please see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439).

![](https://main.qcloudimg.com/raw/dbc8e4aa6ae93062c22cadf4b9373e64.png)

**Log data description**

| Log Field | Raw Log Type | Log Service Type | Description |
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
| prov          | String       | text         | ISP district                                                   |
| referer       | String       | text         | Referer information, i.e., HTTP source address                                 |
| request_range | String       | text         | Range parameter, i.e., request range                                         |
| request_time  | Integer      | long         | Response time (in milliseconds), which refers to the time it takes for a node to respond to a client with all return packets after receiving a request |
| rsp_size      | Integer      | long         | Number of returned bytes                                                   |
| time          | Integer      | long         | Request timestamp in UNIX format                                        |
| ua            | String       | text         | `User-Agent` information                                              |
| url           | String       | text         | Request path                                                     |
| uuid          | String       | text         | Unique request ID                                               |
| version       | Integer      | long         | CDN real-time log version                                                    |

#### Management
You can manage a created log topic and update the list of domain names bound to it.
>? The new configuration will take effect in 5–15 minutes.

![](https://main.qcloudimg.com/raw/ce1f6df0d8bde8ce66f7ebfb4a233e6e.png)

#### Deletion
You can delete log topics manually.
>! After a log topic is deleted, all logs of the domain names bound to the log topic will no longer be shipped to it, and the logs that have already been shipped to the log topic will be completely cleared. This operation will take effect in about 5–15 minutes.

