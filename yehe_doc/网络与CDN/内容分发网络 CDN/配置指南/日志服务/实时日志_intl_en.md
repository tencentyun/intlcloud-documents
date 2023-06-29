## Real-time Logging

Tencent Cloud CDN provides the real-time log feature. This feature collects and publishes access logs in real time, enabling fast retrieval and analysis of log data. You can quickly access comprehensive, stable, and reliable one-stop logging services such as log collection, log storage, and log search in the CDN console.

## Use Cases

You can access log data to view or analyze business conditions in multiple dimensions in real time.

## Directions

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), click **Log Service** in the left sidebar, and then click the **Real-time Logs** tab.

### Enabling logging

To use this feature, you need to activate [Logging Service (CLS)](https://console.cloud.tencent.com/cls/search?region=ap-shanghai) and grant CDN the permissions to create a logset.

>?
>- We recommend that you use the root account to enable this feature. If you use a sub-account or are a collaborator, enable the real-time log feature as instructed in [Activate Real-time Logging as Sub-account/Collaborator](https://www.tencentcloud.com/document/product/228/43581).
>- When you enable the real-time log feature, CDN creates a logset for each region to host CDN logs.
>- A logset is a billable item as a part of CLS. However, the publish of CDN logs is free. For more information about the billing rules, see [Billing Overview](https://intl.cloud.tencent.com/document/product/614/37509).
>- At present, log shipping is supported in Shanghai, Beijing, Chengdu, Chongqing, Nanjing, Guangzhou, and Singapore. 

### Creating a log topic

Create a log topic in a logset, and ship the access logs of the target accelerated domain name to [CLS](https://console.cloud.tencent.com/cls/overview).

>!
>- A logset can contain up to 500 log topics.
>- The topic name must be unique.
>- You cannot bind both CDN and ECDN domain names to the same log topic.
>- Logs of CDN domain names in the Chinese mainland can be shipped to Shanghai, Beijing, Chengdu, Chongqing, Nanjing, and Guangzhou. The logs of CDN domain names outside the Chinese mainland can be shipped to only the Singapore region.
>- ECDN domain names do not support log publishing to regions outside the Chinese mainland.

### Log search

Log search supports various search and analysis methods and chart types. For more information, see [Search and Analysis](https://www.tencentcloud.com/document/product/614/12503).

You can search for logs by log topic. To do so, select a log topic as needed and click **Search** to access the log search page.

### Managing log topics and logsets

You can manage log topics in the CDN console. The following operations are supported:

- Manage: Update the list of domain names bound to a log topic
- Disable: Stop shipping logs of bound domain names to the log topic. . Received logs are retained.
- Enable: Ship logs of bound domain names to the log topic. 
- Delete: After a log topic is deleted, the log topic no longer accepts new log shipping of the bound domain names, and completely clears all logs it contains. 

For more logset managing operations, such as renaming a logset, you can go to the [CLS](https://console.cloud.tencent.com/cls/overview) console.

## Real-time Log Fields

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
| remote_port  | String      | long         | A port connecting the client and CDN nodes. This field will be displayed as `-` if the port does not exist. |
| rsp_size      | Integer      | long         | Number of returned bytes                                                   |
| time          | Integer      | long         | Request timestamp in UNIX format (in seconds)                                        |
| ua            | String       | text         | `User-Agent` information                                              |
| url           | String       | text         | Request path                                                     |
| uuid          | String       | text         | Unique request ID                                               |
| version       | Integer      | long         | CDN real-time log version                                                    |

## Glossary

### Logset

A logset is a project management unit in the log service. It is used to distinguish between logs of different projects and corresponds to an item or application. The CDN logset has the following basic attributes:

- Region: The [region](https://www.tencentcloud.com/document/product/614/18940) to which a logset belongs.
>? At present, log shipping is supported in Shanghai, Beijing, Chengdu, Chongqing, Nanjing, Guangzhou, and Singapore.
- Logset name: Name of the logset.
- Retention period: Retention period of data in the logset.
- Creation time: Logset creation time.

### Log topic

A log topic is the basic management unit in the log service. One logset can contain multiple log topics, and one log topic corresponds to one type of application or service. We recommend you collect similar logs on different machines into the same log topic. For example, if a business project has three types of logs: operation log, application log, and access log, you can create a log topic for each type of log.

The log service system manages different log data based on different log topics. Each log topic can be configured with different data sources, index rules, and shipping rules. Therefore, a log topic is the basic unit for configuring and managing log data in the log service. You need to configure corresponding rules first after creating a log topic before you can perform log collection, search, analysis, and shipping.

Log topic features include:

- Collect logs to log topics.
- Store and manage logs based on log topics.
- Search and analyze logs by log topics.
- Ship logs to other platforms based on log topics.
- Download and consume logs from log topics.

>? For more information, see CLS documentation.

## FAQs

#### Some of my logsets and log topics in the CLS console are not displayed in the CDN console. Why is that?
The CDN console displays only the logs created by the CDN service role, which are real-time logs exclusive to CDN. Other logsets and log topics are not synchronized to the CDN console.
#### I cannot retrieve the data I want in the real-time logs. Are they lost?
It may be because your log data volume is large, but the corresponding log topic has only a single partition, or automatic splitting is disabled for it. When you create a log topic, the default number of partitions is 1, and automatic splitting is enabled by default.
We recommend you estimate the number of required partitions based on your log volume and configure it in the advanced options in the [CLS](https://console.cloud.tencent.com/cls/search?region=ap-shanghai) console. For more information, see [Topic Partition](https://www.tencentcloud.com/document/product/614/33779).
#### Can I delete CLS logsets?
Yes. To delete a CDN logset, go to the CLS console, delete all log topics in the logset, and then delete the logset. The deletion will be synchronized to the CDN console. You can create new logsets and log topics in the CDN console later.

