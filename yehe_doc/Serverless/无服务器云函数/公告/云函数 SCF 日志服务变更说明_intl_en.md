# Log Service Change for SCF

>Note:
>
>SCF plans to upgrade the log service on January 25, 2021 to connect to Cloud Log Service (CLS). After the upgrade, a destination log topic should be specified for new functions, and the SCF backend will no longer store function invocation logs. For more information, please see [Connecting SCF Logs to CLS](https://intl.cloud.tencent.com/document/product/583/34876).
>
>This change will not affect existing functions. The migration of their logs to CLS will start in mid to late February 2021, and we will notify you at that time.
>

## Background

[CLS](https://intl.cloud.tencent.com/document/product/614) provides a one-stop log data solution. You can quickly and conveniently connect to it in five minutes to enjoy a full range of stable and reliable log services from log collection and storage to content search and statistical analysis, without having to care about resource issues such as scaling. CLS helps you easily solve log problems like business issue locating, metric monitoring, and security audit, making log OPS much easier.

After SCF is connected to CLS, function logs can support:

- **Real-time index**: you can index collected log data in real time to enable data search;
- **Flexible search**: you can use various features such as full-text search, multi-keyword search, range search, and fuzzy search;
- **Flexible shipping**: you can customize the log shipping destination and log retention period and ship specified logs to other Tencent Cloud services to meet storage or other computing needs. For example, you can ship logs to a specified COS bucket to manage their lifecycle and meet the need for log audit.

## SCF log service upgrade details

1. Starting January 25, 2021, a destination log topic should be specified for functions created through the SCF console and APIs, and the SCF backend will no longer store the function invocation logs, which will be shipped to the specified topic according to the function log configuration.

2. SCF provides the capability of default log shipping. After you create a function in the console, function invocation logs will be shipped to the log topic `SCF\_logtopic` under the SCF-specific logset `SCF\_logset`, which will be created if it doesn't exist. When you create a function through APIs, you should specify the destination topic for function logs or select default shipping. For more information, please see [CreateFunction](https://intl.cloud.tencent.com/document/product/583/18586). In default shipping mode, function invocation logs will be retained for 7 days by default, and you can view and manage them in the [CLS console](https://console.cloud.tencent.com/cls/logset).

3. After the CLS service is commercialized, Tencent Cloud still provides a certain free tier for all users in each region. The SCF-specific topic will occupy the free tier. For more information on CLS billing, please see [Free Tier](https://intl.cloud.tencent.com/document/product/614/37889).

4. During the upgrade window (January 18, 2021–January 25, 2021), the format of the SCF logs shipped to CLS will be gradually adjusted by region. For the updated log format, please see [Connecting SCF Logs to CLS](https://intl.cloud.tencent.com/document/product/583/34876). Compared to the current format of function logs shipped to CLS, the `SCF_LogTime`, `SCF_Duration`, `SCF_MemUsage`, `SCF_StatusCode`, and `SCF_RetryNum` fields will be added, and the `SCF_Index` field will be removed.

5. After SCF logs are connected to CLS, return data will be retained for asynchronously invoked functions, which will be written to `SCF_Message` in the format of `Response RequestId:xxx RetMsg:xxx`.

>! 
>The value of `SCF_Message` is limited to 8 KB in length, and excessive parts will be truncated.



