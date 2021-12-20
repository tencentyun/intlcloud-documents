During log search and analysis, you may encounter inconsistencies between query results and business logs, or between chart analysis results and the number of log entries. This is usually caused by changes in index configuration. The typical cases are as follows:

### When I search for logs, the number of logs in a certain period is 0, but there are actually logs in that period. What should I do?

When searching for logs via `demokey:value`, if you find that the number of logs in a certain period is 0 in the log quantity bar chart, but there should be logs in that period, you can troubleshoot the problem as follows:
1. Use a blank search statement to search for logs and observe whether logs in the time period are found:
 - If no, it may be that the logs were not collected successfully. Troubleshoot the problem by referring to [Log Search Failure](https://intl.cloud.tencent.com/document/product/614/38446).
 - If yes, proceed with the next step.
2. Go to [Search and Analysis](https://console.cloud.tencent.com/cls/search), click **Index Configuration**, and check the last modification time of the index configuration at the bottom of the left sidebar.

 - If the last modification time is within the time period searched, go to the next step.
 - If the last modification time is beyond the time period searched, check that the search statement syntax is correct by referring to [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439). If the problem persists, please contact [smart customer service](https://intl.cloud.tencent.com/contact-sales).
3. If the index configuration is modified within the time range for log search, the new index configuration takes effect only for the logs that are collected later. If you add a field to the index configuration and use the field to query logs, the logs before the index configuration modification cannot be queried, and for the fields that do not change, logs before and after the index configuration modification can still be queried.


### The number of logs obtained by using the count(\*) function in the analysis statement is inconsistent with the actual number of logs. What should I do?

If you use an analysis statement to obtain the number of logs, even if the analysis statement does not contain filters such as `where`, for example, `* | select count(*) as log_counts`, the number of logs obtained is inconsistent with the actual number of logs. You can troubleshoot the problem as follows:
1. Go to [Search and Analysis](https://console.cloud.tencent.com/cls/search), click **Index Configuration**, and check the last modification time of the index configuration at the bottom of the left sidebar.

- If the last modification time is within the time period searched, go to the next step.
- If the last modification time is beyond the time period searched, check that the analysis statement syntax is correct by referring to [Analysis Overview](https://intl.cloud.tencent.com/document/product/614/37803). If the problem persists, please contact [smart customer service](https://intl.cloud.tencent.com/contact-sales).
2. If the index configuration is modified within the time range for log search, the new index configuration takes effect only for the logs that are collected after the query time range. All fields in the analysis statement also take effect only for the logs that are collected after the query time range. Therefore, the actual time range of the statistics is smaller than the time range you select.


### The execution result of the analysis statement is inconsistent with the actual business situation. What should I do?

If the statistical result of an analysis statement is obviously inconsistent with the actual business situation, for example, when collecting PV statistics, the actual PV should be about 1 million, but the statistical result is only tens of thousands, you can troubleshoot the problem as follows:

1. Go to [Search and Analysis](https://console.cloud.tencent.com/cls/search), click **Index Configuration**, and check the last modification time of the index configuration at the bottom of the left sidebar.

 - If the last modification time is within the time period searched, go to the next step.
 - If the last modification time is beyond the time period searched, check that the analysis statement syntax is correct by referring to [Analysis Overview](https://intl.cloud.tencent.com/document/product/614/37803). If the problem persists, please contact [smart customer service](https://intl.cloud.tencent.com/contact-sales).
2. If the index configuration is modified within the time range for log search, the new index configuration takes effect only for the logs that are collected after the query time range. All fields in the analysis statement also take effect only for the logs that are collected after the query time range. Therefore, the actual time range of the statistics is smaller than the time range you select.
