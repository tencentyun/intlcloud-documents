
>?
>- SCF plans to upgrade the log service on January 29, 2021 to connect to Cloud Log Service (CLS). After the upgrade, you need to specify the destination log topic for new functions. Otherwise the default log shipping configuration will be used. For more information, please see [Connecting SCF Logs to CLS](https://intl.cloud.tencent.com/document/product/583/34876).
>- This update does not affect existing functions. We plan to migrate existing function logs to CLS in mid-to-late February, 2021. 






## Background

[Cloud Log Service (CLS)](https://intl.cloud.tencent.com/document/product/614) is a one-stop logging solution. It can be easily integrated in just five minutes, freeing you from resource or scaling issues. CLS offers solutions for collecting, storing, searching, and analyzing logs, helping you identify business issues, monitor metrics, ensure security, and simplify operations.

After SCF is connected to CLS, function logs can support:

- **Real-time index**: index collected log data in real time to enable data search.
- **Flexible search**: you can use various features such as full-text search, multi-keyword search, range search, and fuzzy search;
- **Log shipping**: you can ship specified logs to other cloud products to meet storage or other computing needs. For example, you can ship a log to a specified COS bucket to manage its lifecycle and meet the need for log auditing.

## SCF log service upgrade details

- Starting from January 29, 2021, you need to specify the destination log topic for new functions. Otherwise the default log shipping configuration will be used. 
- When the default log shipping feature is enabled, SCF will activate CLS automatically and ship function invocation logs to the log topic (prefixed by "SCF_logtopic") in the SCF-specific logset (prefixed by "SCF_logset"). If the log topic and logset do not exist, new ones will be created automatically. Logs are stored for seven days by default. You can check and manage them on the [CLS console](https://console.cloud.tencent.com/cls). 
- After the CLS service is commercialized, Tencent Cloud still provides a certain free tier for all users in each region. The SCF-specific topic will occupy the free tier. For more information on CLS billing, please see [Free Tier](https://intl.cloud.tencent.com/document/product/614/37889).
- During the upgrade window (January 25, 2021 to January 29 2021), the format of the SCF logs shipped to CLS will be gradually adjusted by region. For the updated log format, please see [Connecting SCF Logs to CLS](https://intl.cloud.tencent.com/document/product/583/34876). Compared to the current format of function logs shipped to CLS, the `SCF_LogTime`, `SCF_Duration`, `SCF_MemUsage`, `SCF_StatusCode`, and `SCF_RetryNum` fields will be added, and the `SCF_Index` field will be removed.
- After SCF logs are connected to CLS, return data will be retained for asynchronously invoked functions, which will be written to `SCF_Message` in the format of `Response RequestId:xxx RetMsg:xxx`.
>!The value of `SCF_Message` is limited to 8 KB in length, and excessive parts will be truncated.
