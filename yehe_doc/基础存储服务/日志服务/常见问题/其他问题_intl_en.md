### What is CLS?

Cloud Log Service (CLS) provides a one-stop log data solution. You can quickly and conveniently connect to it in five minutes to enjoy a full range of stable and reliable services from log collection, storage, and processing to search, analysis, consumption, shipping, dashboard generation, and alarming, with no need to care about resource issues such as scaling. It helps you improve the problem locating and metric monitoring efficiency in an all-around manner, making log Ops much easier.

CLS has the following features.

* Log collection: CLS easily collects logs from different regions, channels, platforms, and data sources (e.g., various Tencent Cloud products) in real time.
* Log storage: CLS offers two storage types: real-time storage and IA storage.
* Log search and analysis: You can search for logs by keyword to quickly locate exception logs and use SQL statements to collect and analyze log statistics. This helps you get statistical metrics such as log quantity change trend over time and proportion of error logs.
* Log data processing: CLS can filter, cleanse, mask, enrich, distribute, and structure logs.
* Log shipping and consumption: CLS can ship logs to Tencent Cloud storage and middleware services and consume logs to stream computing services.
* Dashboard: CLS can quickly generate custom dashboards for search and analysis results.
* Alarming: CLS can trigger alarms for exception logs within seconds and notify you through phone, SMS, email, and custom API callback.

### How is a log defined in CLS?

Logs are record data generated during the running of an application system, such as user operation logs, API access logs, and system error logs. Logs are usually stored in text format on the host where the application system resides. A log corresponding to a system running record may contain one line of text (single-line log) or multiple lines of text (multi-line log).

For more information and examples, see [Log and Log Group](https://intl.cloud.tencent.com/document/product/614/38888).

### How long can a log be retained?

CLS provides the log lifecycle management feature. You can set the log validity period to 1–3,600 days or permanent when creating a log topic. Once expired, the data will be cleared and no longer incur storage fees.

### What are the differences between a logset and a log topic?

A log topic is a basic unit for log data collection, storage, search and analysis on the CLS platform. The massive amounts of logs collected are managed by log topic. For example, you can configure log collection rules and storage time, search for and analyze logs, and download, consume, and ship logs by log topic.

A logset is a class of log topics and can contain multiple log topics. A logset itself does not store any log data, but just makes it easier for users to manage log topics.

For more information and examples, see [Log Topic and Logset](https://intl.cloud.tencent.com/document/product/614/32849).

### How many logs can a single log topic collect?

To collect high numbers of logs, a single topic contains multiple partitions, each of which has up to 500 write QPS and 5 MB/s write traffic. If there are many logs to be collected, we recommend you enable the [automatic partition splitting](https://intl.cloud.tencent.com/document/product/614/39587) feature (which is enabled by default). A single log topic can contain up to 50 partitions and thus has up to 50 \* 500 = 25000 write QPS and 50 \* 5 = 250 MB/s write traffic.

Here, the write request quantity and write traffic are not simply equal to the number of logs and log volume respectively. As multiple logs will be packaged and compressed into a [log group](https://intl.cloud.tencent.com/document/product/614/38888) during log upload, the actually supported number of logs and log volume are far greater than the above values. Logs will be automatically packaged and compressed if you use LogListener, so you don't need to care about the specific packaging policy.

### What are an index and a segment?

Index configuration is necessary for log search and analysis in CLS. Only after index is enabled can CLS search for and analyze logs. Index creation is to split a raw log into multiple segments with the specified symbol and add an [inverted index](https://en.wikipedia.org/wiki/Inverted_index) to such segments.

For more information and examples, see [Segment and Index](https://intl.cloud.tencent.com/document/product/614/45409).

### What are the differences between full-text index and key-value index?

- Full-text index: A raw log is split into multiple segments, and indexes are created based on the segments. You can query logs based on keywords (full-text search). For example, entering `error` means to search for logs that contain the keyword `error`.
- Key-Value search: A raw log is split into multiple segments based on a field (key:value), and indexes are created based on the segments. You can query logs based on key-value (key-value search). For example, entering `level:error` means to search for logs with a `level` field whose value contains `error`.

For more information and examples, see [Configuring Indexes](https://intl.cloud.tencent.com/document/product/614/39594).

### What are the differences between search and analysis?

- Search: You can search for matched raw logs by specified criteria. For example, you can enter `status:404` to search for application request logs whose response status code is 404.
- Analysis: You can use SQL statements to collect and analyze the statistics of logs meeting specified search criteria. For example, you can enter `status:404 | select count(*) as logCounts` to get the number of application request logs whose response status code is 404.

For more information and examples, see [Overview and Syntax Rules](https://intl.cloud.tencent.com/document/product/614/37803).

### How high is the performance of log search and analysis?

- Search performance: Results can be returned within seconds for tens of billions of logs.
- Analysis performance: Results can be returned within seconds for hundreds of millions of logs and within one minute for tens of billions of logs. The performance is subject to the complexity of the SQL statement used for analysis. If the statement is very complex, the performance may be lower.

### How long does it take for logs to become searchable after generation?

The delay is within one minute if LogListener is used for log collection. If an API or SDK is used to collect logs, it takes no more than one minute for logs to become searchable after API call.

### Can I use CLS if my business is not in Tencent Cloud?

Yes. CLS has no restrictions on the log source. You can collect logs to CLS as long as the log source can be connected to CLS over the network. For specific regions supported by CLS and corresponding domain names, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).

### How do I configure LogListener after the server IP address is changed?

- If the server is bound to a machine group by server ID, you don't need to modify the LogListener configuration. Therefore, if the server IP needs to be changed frequently, we recommend you configure a machine group by server ID. For more information, see [Machine Group Management](https://intl.cloud.tencent.com/document/product/614/17412).
- If you configure the machine group by IP address, modify the configuration as follows:
 1. Modify the `/etc/loglistener.conf` file under the LogListener installation directory. Here, the `/user/local` installation directory is used as an example:
```go
vi /usr/local/loglistener-2.3.0/etc/loglistener.conf
```
 2. Press **i** to enter the edit mode.
 3. Enter the changed IP address in `group_ip` in the configuration file.
 4. Press **Esc**, enter **:wq**, and press **Enter** to save the configuration and exit the editor.
 5. Run the following command to restart LogListener.
```go
 /etc/init.d/loglistenerd restart
```
 6. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview?region=ap-guangzhou) and select **Machine Group Management** on the left sidebar. Locate the machine group to which the server is bound and click **Edit**. In the pop-up window, replace the old IP address with the new one and click **OK**.

### How do I troubleshoot when the testing alarm notification channel reported an error or failed to receive the testing message?

**Case 1: The page displays "Message sending failed".**

Hover over the "Message sending failed" message to view the error code and detailed failure cause. Common error codes are as listed below:

| Error Code | Description | Troubleshooting Method |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| -1004  | Message sending via this notification channel failed. | This is generally because no mobile numbers or email addresses have been configured or verified for all recipients or recipient groups. You can view and configure them in the [user list](https://console.cloud.tencent.com/cam). |
| -1005  | Some messages failed to be sent via notification channels; for example, messages failed to be sent to some users or via some notification channels. | This is generally because no mobile numbers or email addresses have been configured or verified for some recipients or recipient groups. You can view and configure them in the [user list](https://console.cloud.tencent.com/cam). |
| -1006  | The custom API callback reported an error.                                 | Troubleshoot based on the specific failure cause. Common errors include: <ul  style="margin: 0;"><li>invalid URI for request: The URL is Invalid.</li><li>i/o timeout: API access timed out. Check the API address and whether it can be directly accessed over the public network.</li><li>callback custom error with status:xxx: An API response error occurred. Check whether the API address and backend service are normal.</li><li>ssrf attack: The callback API address must be directly accessible over the public network. This error may occur if the API address is a Tencent Cloud private network address.</li></ul> |

**Case 2: The page displays "Sent", but the testing message is not received.**

Common reasons of different receipt channels are as listed below:

| Receipt Channel | Reason |
| -------------------------------------- | ------------------------------------------------------------ |
| Email, SMS, and phone | To avoid disturbing users with repeated notifications, only one testing message can be sent to the same user via each channel per day. |
| Custom API callback (DingTalk and Lark bot addresses) | The testing message didn't meet DingTalk or Lark's API requirements and was ignored. In this case, the feature of the testing notification channel is meaningless. You can directly configure the appropriate request headers and content in the alarm policy according to DingTalk and Lark's API requirements to send alarm messages. |
| Custom API callback (other addresses)             | CLS determines whether a message was sent successfully based on the HTTP response status code. Check whether the custom API has other business logic limits while the HTTP response status code is normal. |

