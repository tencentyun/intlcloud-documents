## Feature Overview
You can quickly get started with SQL query execution in the Cloud Data Warehouse console, stay on top of slow queries, and optimize or terminate running queries to reduce the usage of cluster resources. You can also manipulate original query log tables on the interactive UI in a simplified and efficient manner.

## Running Queries
1. Log in to the [Cloud Data Warehouse console](https://console.cloud.tencent.com/cdwch), click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page, and switch to the **Query Management** tab.
2. Click the **Running Queries** tab, which displays the details of all running SQL queries by default. You can filter the queries by type, terminate selected queries as needed, or terminate all queries to release resources temporarily.

![](https://qcloudimg.tencent-cloud.cn/raw/7c54d62fffeac9f41257f200d3769114.png)

## Slow Queries
1. Log in to the [Cloud Data Warehouse console](https://console.cloud.tencent.com/cdwch), click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page, and switch to the **Query Management** tab.
2. Click the **Slow Queries** tab, which displays queries taking more than 500 ms to run. You can adjust the threshold of slow query execution duration, timeout period, and set the filter time (including last 15 minutes, last 30 minutes, last hour, and custom time period) as needed and then click the refresh icon.
>?
>- 500 ms is the minimum value of slow query execution duration.
>- You can filter slow queries by date or time (accurate to the minute).

![](https://qcloudimg.tencent-cloud.cn/raw/6302a176725a04fb5549a8989a7885a7.png)


