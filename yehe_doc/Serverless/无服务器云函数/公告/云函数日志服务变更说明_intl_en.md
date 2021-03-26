


>?
>- SCF plans to upgrade the log service on January 29, 2021 to connect to CLS. After the upgrade, a destination log topic should be specified for new functions; otherwise, the default delivery feature will be used. For more information, please see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/39777).
>- This change will not affect existing functions. The migration of their logs to CLS will start in mid to late February 2021.






## Background

[CLS](https://intl.cloud.tencent.com/document/product/614) provides a one-stop log data solution. You can quickly and conveniently connect to it in five minutes to enjoy a full range of stable and reliable log services from log collection and storage to content search and statistical analysis, without having to care about resource issues such as scaling. CLS helps you easily solve log problems like business issue locating, metric monitoring, and security audit, making log OPS much easier.

After SCF is connected to CLS, function logs can support:

- **Real-time index**: you can index collected log data in real time to enable data search.
- **Flexible search**: you can use various features such as full-text search, multi-keyword search, range search, and fuzzy search.
- **Flexible delivery**: you can customize the log delivery destination and log retention period and deliver specified logs to other Tencent Cloud services to meet storage or other computing needs. For example, you can deliver logs to a specified COS bucket to manage their lifecycle and meet the need for log audit.

## SCF Log Service Upgrade Details

- Starting January 29, 2021, default delivery will be used for newly created functions for which no destination log topic is specified, and their invocation logs will be delivered to the specified topic according to the function log configuration.
- For default log delivery, SCF will activate the CLS service for you and deliver the function invocation logs to the log topic under the SCF-specific logset, which are prefixed with `SCF_logtopic` and `SCF_logset` respectively and will be created automatically if not existing. Function invocation logs will be retained for 7 days by default, and you can view and manage them in the [CLS console](https://console.cloud.tencent.com/cls/logset).
  
>!  
>- To ensure the compatibility of the [`GetFunctionLogs`](https://intl.cloud.tencent.com/document/product/583/18583) API, the input parameter `FunctionName` is optional, but we recommend you enter it; otherwise, log acquisition may fail.
>- After the function is connected to CLS, we recommend you use the [related CLS API](https://intl.cloud.tencent.com/document/product/614/16875) to get the best log search experience.

- After the CLS service is commercialized, Tencent Cloud still provides a certain free tier for all users in each region. The SCF-specific topic will consume the free tier. For more information on CLS billing, please see [Free Tier](https://intl.cloud.tencent.com/document/product/614/37889).
- During the release window (January 25–29, 2021), the format of the SCF logs delivered to CLS will be gradually adjusted by region. For the updated log format, please see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/39777). Compared to the current format of function logs delivered to CLS, the `SCF_LogTime`, `SCF_Duration`, `SCF_MemUsage`, `SCF_StatusCode`, and `SCF_RetryNum` fields will be added, and the `SCF_Index` field will be removed.
- After SCF logs are connected to CLS, return data will be retained for asynchronously invoked functions, which will be written to `SCF_Message` in the format of `Response RequestId:xxx RetMsg:xxx`.
>! The value of `SCF_Message` is limited to 8 KB in length, and excessive parts will be discarded.



