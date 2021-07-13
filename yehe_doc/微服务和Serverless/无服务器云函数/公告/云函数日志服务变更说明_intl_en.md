
## Notes:

- SCF plans to upgrade the log service on January 29, 2021 to connect to Cloud Log Service (CLS). After the upgrade, you need to specify the destination log topic or use the default shipping configuration for **new functions**. For more information, please see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/39777).
- Functions created before January 29, 2021 will be gradually migrated by region from April 5, 2021. We will configure the SCF-specific log topic for functions for which you have not configured logging. In the following scenarios, the SCF cannot complete automatic migration or will not perform automatic migration. If you need to view the function invocation logs, please manually associate your functions with a log topic to save the function invocation logs. For details, please see [Log Delivery Configuration](https://intl.cloud.tencent.com/document/product/583/34876).
<table>
<thead>
<tr>
<th>Status</th>
<th>Scenario</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="3">SCF cannot complete the automatic migration.</td>
<td>Your Tencent Cloud account has not completed the identity verification. Please complete the <a href="https://intl.cloud.tencent.com/document/product/378/3629">identity verification</a>, and then associate your functions with a log topic to save the function invocation logs.</td>
</tr>
<tr><td>Your Tencent Cloud account has overdue payment. Please top up your account first, and then associate your functions with a log topic to save the function invocation logs.</td></tr>
<tr><td>The role <code>SCF_QcsRole</code> does not exist. Please complete <a href="https://intl.cloud.tencent.com/document/product/583/38176">SCF service authorization</a>, and then associate your functions with a log topic to save the function invocation logs.</td></tr>
<tr>
<td>SCF will not perform automatic migration.</td>
<td>The functions under your Tencent Cloud account were not invoked during the migration statistical period (March and April 2021). The system determines that you are an inactive user of SCF and will not create log service related resources for you. Before invoking the function again, you need to manually associate your function with a log topic to save the function invocation logs.</td>
</tr>
</tbody></table>





## Background

[Cloud Log Service (CLS)](https://intl.cloud.tencent.com/document/product/614) is a one-stop logging solution. It can be easily integrated in just five minutes, freeing you from resource or scaling issues. CLS offers solutions for collecting, storing, searching, and analyzing logs, helping you identify business issues, monitor metrics, ensure security, and simplify operations.

After SCF is connected to CLS, function logs can support:

- **Real-time index**: index collected log data in real time to enable data search.
- **Flexible search**: you can use various features such as full-text search, multi-keyword search, range search, and fuzzy search.
- **Log shipping**: you can ship specified logs to other cloud products to meet storage or other computing needs. For example, you can ship a log to a specified COS bucket to manage its lifecycle and meet the need for log auditing.



## SCF Log Service Upgrade Details

- Starting from January 29, 2021, the new functions will use the default log topic if no destination log topic is specified, and their invocation logs will be delivered to the specified topic according to the function log configuration.
- Existing functions will be migrated by region from April 5 to June 30, 2021. We will associate the default destination log topic with functions for which you have not configured logging, while the functions for which you have already configured logging will not be affected.
>!
>- If you want to specify the destination log topic for function logs, please configure it before the migration of existing functions starts. For the configuration method, please see [Log Delivery Configuration (Legacy)](https://intl.cloud.tencent.com/document/product/583/34876).
>- We recommend you not change the log configuration during the migration window of existing functions so as to avoid exceptional log query caused by log delivery to different topics.
>- Existing functions will be migrated in stages. For specific migration time, please see the SMS and Message Center notification you receive.

- When the default log shipping feature is enabled, SCF will activate CLS automatically and ship function invocation logs to the log topic (prefixed by "SCF_logtopic") in the SCF-specific logset (prefixed by "SCF_logset"). If the log topic and logset do not exist, new ones will be created automatically. Logs are stored for seven days by default. You can check and manage them on the [CLS console](https://console.cloud.tencent.com/cls/logset).
- The [`GetFunctionLogs`](https://intl.cloud.tencent.com/document/product/583/18583) API will be disused on July 1, 2021. After the function is connected to CLS, we recommend you use the [related CLS API](https://intl.cloud.tencent.com/document/product/614/16875) to get the best log search experience.
>!
>To ensure the compatibility of the [`GetFunctionLogs`](https://intl.cloud.tencent.com/document/product/583/18583) API, the input parameter `FunctionName` is optional, but we recommend you enter it; otherwise, log acquisition may fail.

- After the CLS service is commercialized, Tencent Cloud still provides a certain free tier for all users in each region. The SCF-specific topic will consume the free tier. For more information on CLS billing, please see [Free Tier](https://intl.cloud.tencent.com/document/product/614/37889).
- For more information on the format of logs delivered from SCF to CLS, please see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/39777).
- After SCF logs are connected to CLS, return data will be retained for asynchronously invoked functions, which will be written to `SCF_Message` in the format of `Response RequestId:xxx RetMsg:xxx`.

>!The value of `SCF_Message` is limited to 8 KB in length, and excessive parts will be discarded.



