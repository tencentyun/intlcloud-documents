## Overview
EdgeOne's real-time log feature can collect and publish access logs in real time, enabling fast retrieval and analysis of log data. You can quickly access comprehensive, stable, and reliable one-stop logging services such as log collection, log storage, and log search in the EdgeOne console.

## Use Cases
You can access log data to view or analyze business conditions in multiple dimensions in real time.


## Prerequisites
Currently, real-time logs can be pushed to CLS only. To use CLS in EdgeOne, you need to activate [CLS](https://console.cloud.tencent.com/cls) first and grant EdgeOne access to create free logsets.
>? We recommend you use the root account to enable this feature. If you are a sub-account or collaborator, enable the real-time log feature as instructed in [Activate Real-time Logging as Sub-account/Collaborator](https://intl.cloud.tencent.com/document/product/228/43581).

## Creating push task
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Log analysis** > **Real-time log** on the left sidebar.
2. On the real-time log page, select the target site and click **Create push task** to create a real-time log push task.
>?Currently, real-time logs can be pushed to CLS only.
3. On the push task creation page, enter a task name, select the desired data and target subdomain under the current site, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/60ba6bd464372687072380dd530fd775.png)

**Parameter description:**
 - Task name: You can enter 1–200 letters, digits, underscores, and hyphens.
 - Data: Currently, only site acceleration data can be pushed.
 - Subdomain: Subdomain under the current site to which logs need to be pushed.

>? All subdomains can be added in only one subdomain field.
4. Select the required parameters and click **Push**.
![](https://qcloudimg.tencent-cloud.cn/raw/4d42f3254c7ca7e6c6bdbf44042851a0.png)

**Parameter description:**
 - Target address: CLS is selected by default and cannot be changed.
 - Region: Select the target region to which logs will be pushed.
 - Target logset name: Select a logset in the target region.

>?If there are no options or you need to create a logset, click **Create** to create a logset in the selected region.
 - Log topic name: You can enter 1–200 letters, digits, underscores, and hyphens.
 - Log retention period: Enter a positive integer between 1 and 366.



## Managing Push Task
#### Editing push task
1. On the [real-time log page](https://console.cloud.tencent.com/edgeone/log/realtime), select the target push task and click **Edit** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/608b29ac9e89aad8ec8139419ed20850.png)
2. On the task editing page, you can modify the push task's name, subdomain list, push data, log topic name, and log retention time. Then, click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/af1336ab7d283102f496e0ff4abcf257.png)

#### Disabling push task
You can disable a log push task to stop shipping logs to the specified log topic.
1. On the [Real-time log](https://console.cloud.tencent.com/edgeone/log/realtime) page, select the target push task and click **More** > **Disable** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/7cb01aa688cfd4d2f55aa63525bf0fbc.png)
2. Once the push task is disabled, its subdomain logs will stop being shipped to the specified log topic, but shipped logs will be retained.

#### Enabling push task
You can enable a log push task to ship logs to the specified log topic.
1. On the [Real-time log](https://console.cloud.tencent.com/edgeone/log/realtime) page, select the target push task and click **More** > **Enable** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/e6ba03769fd65eea77742b8f914a9ff2.png)
2. Once the push task is enabled, its subdomain logs will be shipped to the specified log topic.

#### Deleting push task
1. On the [Real-time log](https://console.cloud.tencent.com/edgeone/log/realtime) page, select the target push task and click **More** > **Delete** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/bc3e23770d0165a8c2960390adc55bf9.png)
2. Once the push task is deleted, its subdomain logs will stop being shipped to the specified log topic, its log topic will be deleted, and all shipped logs will be cleared.

## Log search
Log search supports various search and analysis methods and chart types. For more information, see [Cloud Log Service](https://intl.cloud.tencent.com/document/product/614/12503).
EdgeOne logs can be searched for by push task. On the [Real-time log](https://console.cloud.tencent.com/edgeone/log/realtime) page, select the target push task and click **Search** to enter the log search page.
![](https://qcloudimg.tencent-cloud.cn/raw/a4899c8e69269c2689792cf5e07f3f04.png)

You can manage modules such as logsets in [CLS](https://console.cloud.tencent.com/cls/overview); for example, you can rename logsets.

## Glossary
#### Logset
A logset is a project management unit in CLS. It is used to distinguish between logs of different projects and corresponds to a set. An EdgeOne logset has the following basic attributes:
- Region: The [region](https://intl.cloud.tencent.com/document/product/614/18940) to which a logset belongs.
- Logset name: The name of a logset.
- Log retention period: Retention period of data in the current logset.
- Creation time: Logset creation time.

#### Log topic
A log topic is the basic management unit in CLS. One logset can contain multiple log topics, and one log topic corresponds to one type of applications or services. We recommend you collect similar logs on different machines into the same log topic. For example, if a business project has three types of logs: operation, application, and access logs, you can create a log topic for each type of logs.

The log service system manages different log data based on different log topics. Each log topic can be configured with different data sources, index rules, and shipping rules. Therefore, a log topic is the basic unit for configuring and managing log data in the log service. You need to configure corresponding rules first after creating a log topic before you can perform log collection, search, analysis, and shipping.

Log topic features include:
- Collect logs to log topics.
- Store and manage logs based on log topics.
- Search for and analyze logs by log topics.
- Ship logs to other platforms based on log topics.
- Download and consume logs from log topics.

>? 
>- The above information is quoted from the product documentation of [CLS](https://intl.cloud.tencent.com/document/product/614). If there are any differences, the CLS documentation shall prevail.
>- Each real-time log push task that ships logs to CLS pushes the logs of selected subdomains to the specified log topic.

## Real-time log field description

| Log Field      | Raw Log Type | Log Service Type | Description                                                         |
| ------------- | ------------ | ------------ | ------------------------------------------------------------ |
| app_id        | Integer      | long         | Tencent Cloud account `APPID`                                             |
| client_ip     | String       | text         | Client IP                                                    |
| file_size     | Integer      | long         | File size                                                     |
| hit           | String       | text         | Cache hit/miss. Both hits on EdgeOne edge nodes and parent nodes are marked as hit |
| host          | String       | text         | Domain                                                         |
| http_code     | Integer      | long         | HTTP status code                                                  |
| isp           | String       | text         | ISP                                                       |
| method        | String       | text         | HTTP method                                                  |
| param         | String       | text         | Parameter carried in URL                                               |
| proto         | String       | text         | HTTP protocol identifier                                                |
| prov          | String       | text         | ISP province/state                                                  |
| referer       | String       | text         | Referer information, i.e., HTTP source address                                 |
| request_range | String       | text         | Range parameter, i.e., request range                                         |
| request_time  | Integer      | long         | Response time (in milliseconds), which refers to the time it takes for a node to return all packets to the client after receiving a request |
| remote_port   | String       | long         | A port connecting the client and EdgeOne nodes. This field will be displayed as `-` if the port does not exist |
| rsp_size      | Integer      | long         | Number of returned bytes                                                   |
| time          | Integer      | long         | Request timestamp in UNIX format in seconds                          |
| ua            | String       | text         | `User-Agent` information                                              |
| url           | String       | text         | Request path                                                     |
| uuid          | String       | text         | Unique request ID                                               |
| version       | Integer      | long         | EdgeOne real-time log version                                  |



## FAQs
#### Why can't I see certain log topics created in the CLS console in the EdgeOne console?
As EdgeOne console supports and displays the log information created by the EdgeOne role, i.e., real-time log service dedicated to EdgeOne, other logsets and log topics won't be synced to EdgeOne.

#### Why can't I find data by searching for real-time logs? What can I do if data loss occurs?
It may be because your log data volume is large, but the corresponding log topic has only a single partition, or automatic splitting is disabled for it. When you create a log topic, the default number of partitions is 1, and automatic splitting is enabled by default.

We recommend you estimate the number of required partitions based on your log volume and configure it in the advanced options in the [CLS](https://console.cloud.tencent.com/cls/search?region=ap-shanghai) console. For more information, see [Topic Partition](https://intl.cloud.tencent.com/document/product/614/33779).

#### Can I delete CLS logsets?
Yes. You need to log in to the [CLS console](https://console.cloud.tencent.com/cls) to delete a logset. Before deleting it, you need to delete all its log topics. The deletion will be synced to EdgeOne. If you want to use logsets and log topics again, create them again in the EdgeOne console.
