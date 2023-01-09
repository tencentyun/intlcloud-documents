## Overview
EdgeOne provides the real-time logging feature to collect and ship access logs in real time, allowing for fast retrieval and analysis of log data. 

## Use Cases
You can access log data to view or analyze business conditions in multiple dimensions in real time.


## Prerequisites
Activate [CLS](https://console.cloud.tencent.com/cls) and grant EdgeOne access to create logsets.
>? It’s recommended to enable real-time logging by using a root account. If you are a sub-account or collaborator, you need to obtain the required permission. 

## Creating a Push Task
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Log Service** > **Real-time Logs** on the left sidebar.
2. On the **Real-time Logs** page, select the target site and click **Create push task**.
>?Real-time logs can only be shipped to CLS for now.
3. On the **Create push task** page, enter the task name, select the data to ship and the target subdomain under the current site, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/60ba6bd464372687072380dd530fd775.png)
**Parameter description:**
 - **Task name**: 1 to 200 characters, including `a-z, A-Z, 0-9, _, -`.
 - **Data**: For now, only site acceleration data can be shipped.
 - **Subdomain**: Subdomain of which you want to ship the logs. It must be under the current site.
>? You need to add all subdomain names in to one push task.
4. Configure the parameters below and click **Push**.
![](https://qcloudimg.tencent-cloud.cn/raw/4d42f3254c7ca7e6c6bdbf44042851a0.png)
**Parameter description:**
 - **Target address**: Only **CLS** is supported.
 - **Region**: Select the destination region.
 - **Target logset name**: Select a logset in the destination region.
>?Click **Create** to create a logset in the selected region if necessary.
 - **Log topic name**: 1 to 200 characters, including `a-z, A-Z, 0-9, _, -`.
 - **Log retention period**: Enter a positive integer between 1 and 366.



## Managing Push Tasks
#### Editing push task
1. On the [Real-time Logs](https://console.cloud.tencent.com/edgeone/log/realtime) page, select the push task and click **Edit** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/608b29ac9e89aad8ec8139419ed20850.png)
2. On the **Edit task** page, modify the task name, subdomains, push data, log topic name, and log retention time. Then, click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/af1336ab7d283102f496e0ff4abcf257.png)

#### Disabling push task
You can suspend a log push task to stop shipping logs to the specified log topic.
1. On the [Real-time Logs](https://console.cloud.tencent.com/edgeone/log/realtime) page, select the push task and click **More** > **Disable** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/7cb01aa688cfd4d2f55aa63525bf0fbc.png)
2. Once the push task is disabled, its subdomain logs will stop being shipped to the specified log topic, but shipped logs will be retained.

#### Enabling a push task
You can enable a log push task to ship logs to the specified log topic.
1. On the [Real-time Logs](https://console.cloud.tencent.com/edgeone/log/realtime) page, select the target push task and click **More** > **Enable** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/e6ba03769fd65eea77742b8f914a9ff2.png)
2. Once the push task is enabled, its subdomain logs will be shipped to the specified log topic.

#### Deleting a push task
1. On the [Real-time log](https://console.cloud.tencent.com/edgeone/log/realtime) page, select the target push task and click **More** > **Delete** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/bc3e23770d0165a8c2960390adc55bf9.png)
2. Once the push task is deleted, its subdomain logs will stop being shipped to the specified log topic, its log topic will be deleted, and all shipped logs will be cleared.

## Log Search
Log search supports various search and analysis methods and chart types. For more information, see [Cloud Log Service](https://intl.cloud.tencent.com/document/product/614/12503).
EdgeOne logs can be searched for by push task. On the [Real-time logs](https://console.cloud.tencent.com/edgeone/log/realtime) page, select the target push task and click **Search** to enter the log search page.
![](https://qcloudimg.tencent-cloud.cn/raw/a4899c8e69269c2689792cf5e07f3f04.png)

For more logset managing operations, such as renaming a logset, you can go to the [CLS](https://console.cloud.tencent.com/cls/overview) console.

## Glossary
#### Logset
A logset is a project management unit in CLS. It is used to distinguish between logs of different projects and corresponds to a set. An EdgeOne logset has the following basic attributes:
- Region: The [region](https://intl.cloud.tencent.com/document/product/614/18940) to which a logset belongs.
- Logset name: The name of a logset.
- Retention period: The retention period of data in the current logset.
- Creation time: Logset creation time.

#### Log topics
A log topic is the basic management unit in the Tencent Cloud log service (CLS). One logset can contain multiple log topics, and one log topic corresponds to one type of application or service. We recommend you collect similar logs on different machines into the same log topic. For example, if a business project has three types of logs: operation log, application log, and access log, you can create a log topic for each type of log.

The log service system manages different log data based on different log topics. Each log topic can be configured with different data sources, index rules, and shipping rules. Therefore, a log topic is the basic unit for configuring and managing log data in the log service. You need to configure corresponding rules first after creating a log topic before you can perform log collection, search, analysis, and shipping.

Log topic features include:
- Collect logs to log topics.
- Store and manage logs based on log topics.
- Search and analyze logs by log topics.
- Ship logs to other platforms based on log topics.
- Download and consume logs from log topics.
> ? 
>- For more information, see [CLS documentation](https://intl.cloud.tencent.com/document/product/614). 
>- Each real-time log push task ships logs of the selected subdomains to the corresponding log topic in CLS.

## Real-time Log Fields

| Field               | Type | Description                                                         |
| ---------------------- | ------------ | ------------------------------------------------------------ |
| RequestID              | String   | Unique ID of the client request                                    |
| ClientIP               | String   | Client IP                                                  |
| ClientCountry          | string       | The two-digit country code (ISO 3166-2) of the client location. |
| RequestTime            | int          | Client request time (a UNIX timestamp in seconds)|
| RequestHost            | string   | Client request host                                          |
| RequestBytes           | int      | Client request size, which includes the size of the file itself and request headers |
| RequestMethod          | string   | HTTP client request method                                   |
| RequestUrl             | string   | Client request URL                                           |
| RequestUrlQueryString  | string   | A query string that is carried in the client request URL                            |
| RequestUA              | string   | Client request User-Agent                                 |
| RequestRange           | string   | Client request Range                                  |
| RequestReferer         | string   | Client request Referer                                   |
| RequestProtocol        | string   | Client request HTTP protocol: HTTP, HTTPS, and HTTP/3                |
| RemotePort             | int      | Port connecting the client and nodes under the TCP protocol. This field will be "-" if the port does not exist.           |
| EdgeCacheStatus        | string   | Whether the client request hits the node cache: HIT, MISS, and Dynamic             |
| EdgeResponseStatusCode | int      | Response status code returned to the client by the nodes                               |
| EdgeResponseBytes      | int      | Response size returned to the client by the nodes                                 |
| EdgeResponseTime       | int          | The period from the point when the request is initiated from the client and the point when the client receives response from the server|


## FAQs
#### Some of the CLS log topics are not visible in the EdgeOne console. 
In the EdgeOne console, you can only see log topics created by using the EdgeOne role.

#### I cannot retrieve the data I want in the real-time logs. Are they lost?
It may be because your log data volume is large, but the corresponding log topic has only a single partition, or automatic splitting is disabled for it. When you create a log topic, the default number of partitions is 1, and automatic splitting is enabled by default.

We recommend you estimate the number of required partitions based on your log volume and configure it in the advanced options in the [CLS](https://console.cloud.tencent.com/cls/search?region=ap-shanghai) console. For more information, see [Topic Partition](https://intl.cloud.tencent.com/document/product/614/33779).

#### Can I delete CLS logsets?
Yes. You can delete the logsets in the [CLS console](https://console.cloud.tencent.com/cls). Note that to delete a logset, you need to delete all its log topics first. The deletion will be synced to EdgeOne. 
