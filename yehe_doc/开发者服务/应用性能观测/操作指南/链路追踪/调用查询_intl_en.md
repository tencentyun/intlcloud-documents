This document describes the capabilities and directions of API call search and analysis. With this feature, you can query the trace information, trace IDs, and trace details of servers and clients. In addition, the method stack information can be displayed for applications that use the proprietary probe to report data.

## Prerequisites
Go to the [**Call query**](https://console.cloud.tencent.com/apm/monitor/span) page in the APM console.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/dtVr029_1.png)


### Basic query

You can query API calls by server name, server IP, client name, client IP, target API, trace ID, or business tag in the basic query module on the **Call query** page.

>?If you don't select the server or client, all traces in the application will be displayed in the list.

#### Business tag

You can customize tags when reporting data based on the business type, such as order and cart tags. If there is an exception in a user's order, you can quickly get the order call conditions, including response time, execution result, and service status.

For example, when reporting the data of a PHP application, you can customize a tag and then search for the business bound to the tag by the tag key and value (key:value).
```php
$span->tag('key', $value);
```
![](https://staticintl.cloudcachetci.com/yehe/backend-news/P2ew986_2.png)

#### Displaying the trace entry only
You can quickly search for the trace entry (span) in an application to locate abnormal traces.
Assume a trace is as shown below. If you select **Display the trace entry only**, the list will only display the call status of the trace entry **Service A**.

![](https://qcloudimg.tencent-cloud.cn/raw/be94c84889e9fb7ecb8d1145487294fe.png)


### Call trace details
Click **Request details** or **TraceID/SpanID** in the **Operation** column of the target API to enter the trace analysis page, where you can view the duration of each stage of the trace and the reported information of the entire trace, including the trace health and duration.
The method stack information can be displayed for applications that use the proprietary Java probe as described in [Reporting via TAPM](https://www.tencentcloud.com/document/product/1166/51713) to report data. You can view the line numbers of method stacks in the trace list to quickly troubleshoot slow calls and abnormal method stacks.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/S9jn353_4.png)