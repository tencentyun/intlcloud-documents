## Background

In CLS use cases, it is very common to migrate the data source from other log tools to CLS. If you use ES as the data source and Grafana as the visual monitoring tool, after you migrate the data source to CLS, various dashboard resources and Ops tools and platforms created based on Grafana will become useless. To avoid building this system again, CLS needs to be connected to Grafana to replace the ES data source.

<img src="https://qcloudimg.tencent-cloud.cn/raw/b26bfe6312c74eaf48a361f93a34515d.png" style="width: 35%"/>

## Installing Tencent Cloud Monitor

The Tencent Cloud Monitor plugin (CLS data source) is maintained by the CLS team and has been [officially signed by Grafana](https://grafana.com/grafana/plugins/tencentcloud-monitor-app/). You can quickly install it on the Grafana settings page.

For detailed directions, see [CLS Connection to Grafana](https://intl.cloud.tencent.com/document/product/614/39592).


## Replacing ES with CLS as Data Source

### Comparing data source configuration sections

- **ES data source plugin:** The query statement UI consists of the **query input box** at the top and **auxiliary input features** in other places. You can enter Lucene statements in the **Query** input box to filter logs. In the auxiliary input section, you can click buttons and enter values to generate DSL content for data aggregation, which is similar to SQL statements in CLS.
![](https://qcloudimg.tencent-cloud.cn/raw/295b6c3570d00f111b399203ddfca312.png)
- **CLS data source plugin:** The query statement UI consists of the **region and log topic selection** section and **search and analysis statement** section. They are used to quickly switch the log topic and enter CLS query statements respectively.
A CLS query statement consists of a Lucene statement and a SQL statement, which are separated by a pipe symbol "|". Here, the Lucene statement is the same as the content in the **Query** input box for ES. The entered SQL statement supports not only standard SQL syntax but also diversified SQL functions to offer the same features as in the auxiliary input section for ES. For more information, see [Overview and Syntax Rules](https://intl.cloud.tencent.com/document/product/614/37803).
![](https://qcloudimg.tencent-cloud.cn/raw/2cf2779d2fb88f1d59959a0bcdfa2918.png)


### Directions

#### Counting logs

To draw a histogram of the number of logs changing over time, in the ES data source, select **Count** for **Metric** and **Data Histogram** for **Group By**; in the CLS source data, you can combine the histogram and the aggregate function `Count` to write a search statement. You can also use other [general aggregate functions](https://intl.cloud.tencent.com/document/product/614/41995) such as `Max`, `Min`, and `Distinct` in the same way by directly replacing the `Count` function.
![](https://qcloudimg.tencent-cloud.cn/raw/e9dc944ac3161448f50d9c4209929bab.png)

#### Viewing raw logs

To directly view logs meeting the search criteria, select **Logs** for **Metric** in the ES data source, or enter the corresponding Lucene statement in the CLS data source. The statements entered are as compared below:
![](https://qcloudimg.tencent-cloud.cn/raw/44ead3e30bad90c36a5e185e23ab0260.png)
Display effect: 
![](https://qcloudimg.tencent-cloud.cn/raw/7febf23b94596d5fae9ac705a272e7fa.png)


#### Aggregate statistics - error code proportion

You can aggregate error codes and display the numbers of logs with each error code. As can be seen here, the statement contains the `$path` variable. The CLS data source plugin adapts to the variable capabilities of Grafana for direct use.
>! To draw a pie chart, select **ValueOptions-AllValues** in the chart options on the right.
>
![](https://qcloudimg.tencent-cloud.cn/raw/54db97edaf414ca3ab8f2a2a1312ab5c.png)
Display effect: 
![](https://qcloudimg.tencent-cloud.cn/raw/e1734c6f79ca8d041352457590fe2b37.png)

#### Aggregate statistics - changes in numbers of top five requests

In the ES data source plugin, you can enter a `Size` value for the **Group By** aggregate option to select the top N most frequent values and aggregate them.
In the CLS data source, you can write a `having` SQL statement nesting subqueries to achieve the same purpose.

```
*|select histogram( cast(__TIMESTAMP__ astimestamp),interval1hour)as analytic_time,"action",count(*)as countgroupby analytic_time,"action"having"action"in(selectactiongroupbyactionorderbycount(*)desclimit5)orderby analytic_time limit1000
```
![](https://qcloudimg.tencent-cloud.cn/raw/9f2db8ff443a629b76469079228aa71b.png)
The chart of query results displays five curves as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/417919ff2d5e84a8ca6c3e77bf8057e4.png)
By combining the above statements, you can meet the needs in most search and analysis scenarios.

#### Ranged statistics of API call time

In the dashboard of the ES data source, there is an example with complicated configuration items but a wide applicability, that is, to draw a chart of numbers of requests distributed in different time ranges.
In this example, the numbers of requests with an API call time of 0–500 ms, 500 ms–2s, 2–5s, and above 5s are presented respectively. 
![](https://qcloudimg.tencent-cloud.cn/raw/7392ca4ebc44c8e12275b42ac5c7ffb9.png)

Accordingly, after migrating the data source to CLS, you can also use multiple statements to draw a similar chart. However, CLS has more powerful SQL capabilities, so you can merge relevant statistics collection statements into one SQL statement:
![](https://qcloudimg.tencent-cloud.cn/raw/e017c6908fcd844a8d352a03672cd69a.png)
```
urlPath:$path AND region:$region AND action:$action AND returnCode:$returnCode | select histogram( cast(__TIMESTAMP__ as timestamp),interval 1 minute) as analytic_time ,count_if(timeCost<=200) as "0~500ms" ,count_if(500<timeCost and timeCost <=2000) as "500ms~2s" ,count_if(2000<timeCost and timeCost <=5000) as "2s~5s" ,count_if(5000<timeCost) as "Above 5s" group by analytic_time order by analytic_time limit 1000
```

In similar scenarios, you can write a statement by using the estimation function `approx_percentile` to analyze the consumed time.
![](https://qcloudimg.tencent-cloud.cn/raw/ab99a40e1e378d6848dd499b42abd256.png)

```
urlPath:$path AND region:$region AND action:$action AND returnCode:$returnCode  | select time_series(__TIMESTAMP__, '$__interval', '%Y-%m-%dT%H:%i:%s+08:00', '0') as time ,avg(timeCost) as avg ,approx_percentile(timeCost, 0.50) as P50 ,approx_percentile(timeCost, 0.90) as P90 ,approx_percentile(timeCost, 0.95) as P95 group by time order by time limit 10000
```

#### Template variable capabilities

The Grafana variable feature is used in all of the above examples to different degrees. Grafana has diverse variable types. For constant and textbox types, they are completely the same for different data sources and don't require additional configuration for migration. This section describes how to migrate variables of query type.

**`$action` variable for ES**: It indicates the API category and is described in DSL in the ES data source. The following syntax is to find the content matching the query condition `urlPath:$path AND region:$region`, select the `action` field, and sort API categories by the number of occurrences. 
![](https://qcloudimg.tencent-cloud.cn/raw/3e79f7d523547550e770075f7043c1bd.png)

**`$action` variable for CLS**: For this variable, the CLS data source has the same user experience and input behavior in chart editing as ES. You can select CLS as the service type, select the corresponding log topic, and enter a SQL statement to achieve the same effect.
![](https://qcloudimg.tencent-cloud.cn/raw/007b7a2dc54e8bb23e71c4480d9283a8.png)

In addition to using search statements of CLS to query variables, you can also use the resource query feature of CM to display service resources in Tencent Cloud as a list. For more information, see [Template Variables](https://intl.cloud.tencent.com/document/product/248/40024).
```
Namespace=QCE/CLS&Action=DescribeInstances&Region=$region&display=${TopicName}/${TopicId}
```
Query the log topic list:
![](https://qcloudimg.tencent-cloud.cn/raw/354ea9d40abf924f1fa46511fba1d90a.png)

#### Merging data content of requests from different regions

In the original implementation, if you store all data in the same ES instance, after CLS is used, you may want to merge the content of those log tops into the same chart.
For three statements querying logs from different regions:
![](https://qcloudimg.tencent-cloud.cn/raw/5dcd071c5d9db8d7eb5fadd32ea2327e.png)
You can calculate the total numbers in the **Transform** module and select an appropriate chart to display them. 
![](https://qcloudimg.tencent-cloud.cn/raw/7cf8c5f0ed99441d228e68ac891b3aec.png)

### Summary

You can repeat the above migration steps to completely convert an existing ES data source dashboard into a CLS one.
By migrating the data source from ES to CLS, you can continue to use the accumulated visual resources after migrating your business from self-built ELK to CLS.
A converted dashboard not only has all capabilities of the ES data source, but also supports other capabilities of the CLS data source plugin, such as CM template variables, to better integrate with the Tencent Cloud ecosystem.
