
| Variable Type | Description                                                         | Effective Scope                 |
| -------- | ------------------------------------------------------------ | ------------------------ |
| Data source   | A data source variable allows you to batch switch data sources of charts in the dashboard. It is suitable for scenarios where a dashboard is applied to multiple log topics, data on the dashboard is compared in blue and green, and more. | Charts that use the variable on the dashboard |
| Quick filtering | A quick filtering variable allows you to filter data of all charts on the dashboard by specified fields, which is equivalent to adding filter criteria in chart query statements. | All charts on the dashboard         |


## Configuring a Data Source Variable

### Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Dashboard** to enter the dashboard management page.
3. Click the ID/name of the target dashboard to enter the dashboard details page.
4. Click ![](https://qcloudimg.tencent-cloud.cn/raw/db1173f042aa2fcc3bd65cfa2a682639.png) at the top to enter the configuration page.
![](https://qcloudimg.tencent-cloud.cn/raw/101678bae6703791c195955f9a17c273.png)
5. Click **Template Variable** and click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/4afdfcc855ed171d9bcad02b54e78177.png)
6. In the pop-up window, configure the template variable information and click **Submit**.
![](https://qcloudimg.tencent-cloud.cn/raw/10a34ab965cc3d050f73b336073619fc.png)
<table>
	<tr><th>Parameter</th><th>Description</th></tr>
	<tr><td>Variable Type</td><td>Variable category. Different categories correspond to different configuration items and application scenarios. Here, select **Data Source**.</td></tr>
	<tr><td>Variable Name</td><td>Name of the variable in the query/search statement. The value can contain only letters and digits.</td></tr>
	<tr><td>Display Name</td><td>Name of the variable displayed on the dashboard. This parameter is optional. If it is empty, the system automatically uses the variable name as the display name.</td></tr>
	<tr><td>Data Source Scope</td><td>Value range of the variable. Currently, only option **All Log Topics** is supported, that is, there is no limit on the data source range.</td></tr>
	<tr><td>Default Log Topic</td><td>Log topic used by default.</td></tr>
</table>
7. On the dashboard details page, click **More** > **Edit** to edit charts.
>? If there are no charts on your dashboard, please [add charts](https://intl.cloud.tencent.com/document/product/614/43560).
>
8. At the top of the edited chart, click **Log Topic**, select **Use Data Source Variable**, and select the template variable created just now.
![](https://qcloudimg.tencent-cloud.cn/raw/0f3390d4b75f694718bb30ef4c7731c8.png)
9. Click **Save**.
10. On the dashboard details page, click the **Data Source** drop-down list and select another log topic. Then the system changes automatically changes the data source of the chart using the variable accordingly.
![](https://qcloudimg.tencent-cloud.cn/raw/7965ccbc7def0e3ff7d3cbe9491773b9.png)



### FAQs

#### Why does a configured data source variable not take effect or take effect only on some charts?

A data source variable does not apply directly to all charts on the dashboard. It applies only to those charts that use it on the chart editing page.


## Configuring a Quick Filtering Variable

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Dashboard** to enter the dashboard management page.
3. Click the ID/name of the target dashboard to enter the dashboard details page.
4. Click ![](https://qcloudimg.tencent-cloud.cn/raw/db1173f042aa2fcc3bd65cfa2a682639.png) at the top to enter the configuration page.
![](https://qcloudimg.tencent-cloud.cn/raw/0124612359c336be0c6fedf717a1e06d.png)
5. Click **Template Variable** and click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/b94b9a91d97290aab7b5b1268a4c1e4d.png)
6. In the pop-up window, configure the template variable information and click **Submit**.
![](https://qcloudimg.tencent-cloud.cn/raw/fb06fb025edf90a46c6e181175091a99.png)
<table>
	<tr><th>Parameter</th><th>Description</th></tr>
	<tr><td>Variable Type</td><td>Variable category. Different categories correspond to different configuration items and application scenarios. Here, select **Quick Filtering**.</td></tr>
	<tr><td>Display Name</td><td>Name of the variable control on the UI. This parameter is optional. If it is empty, the system automatically uses the variable name as the display name.</td></tr>
	<tr><td>Log Topic</td><td>Source log topic of the variable field.</td></tr>
	<tr><td>Select Field</td><td>Filter field.</td></tr>
	<tr><td>Support Multiple-Selection</td><td>If this parameter is toggled on, you can select multiple variable values as filter conditions.</td></tr>
</table>
7. On the dashboard details page, click the variable console and select the filter field. Then the data on the dashboard is refreshed to the filtered content.
![](https://qcloudimg.tencent-cloud.cn/raw/c94d5e052a18665e27f06fbcd7d11d10.png)



## Examples

### Analyzing performance metrics of different APIs on the dashboard (quick variable filtering)

#### Requirement

Log topic A stores NGINX access logs of an application, and you are to use the dashboard to view the throughput, number of error requests, and response time of the **entire application** and **a specified API**. The following is the sample log information:
```
body_bytes_sent:1344
client_ip:127.0.0.1
host:www.example.com
http_method:POST
http_referer:www.example.com
http_user_agent:Mozilla/5.0
proxy_upstream_name:proxy_upstream_name_4
remote_user:example
req_id:5EC4EE87A478DA3436A79550
request_length:13506
request_time:1
http_status:201
time:27/Oct/2021:03:25:24
upstream_addr:219.147.70.216
upstream_response_length:406
upstream_response_time:18
upstream_status:200
interface:proxy/upstream/example/1
```

#### Solution

1. Create a dashboard.
2. Create three charts (sequence diagrams) based on the application performance metrics. The corresponding query statements are as follows:
 - Throughput
```
* | select histogram( cast(__TIMESTAMP__ as timestamp),interval 1 minute) as analytic_time, count(*) as pv group by analytic_time order by analytic_time limit 1000
```
 - Number of error requests
```
http_status:>=400 | select histogram( cast(__TIMESTAMP__ as timestamp),interval 1 minute) as analytic_time, count(*) as pv_lost group by analytic_time order by analytic_time limit 1000
```
 - Average response time
```
* | select histogram( cast(__TIMESTAMP__ as timestamp),interval 1 minute) as analytic_time, avg(request_time) as response_time group by analytic_time order by analytic_time limit 1000
```
3. Add template variables.
 - Variable Type: Quick Filtering
 - Display Name: API name
 - Log Topic: Log topic A
 - Select field: interface
4. Go back to the dashboard details page, and you can see this variable on the top of the page.
 - If **API Name** is not specified, data is not filtered, and the charts on the dashboard display all data, that is, the overall performance metrics of the application.

 - If **API Name** is specified, all charts on the dashboard use the specified API as the filter condition to filter data and display the performance metrics of the API.



### Viewing the production and test environment performance metrics on the dashboard separately (variable Data Source)

#### Requirement

An application has a production environment and a test environment, and logs are collected to **Log topic A (production environment)** and **Log topic B (test environment)**. Therefore, during application development, testing, and Ops, you need to pay attention to the performance metrics of the two environments.

#### Solution

1. Create a dashboard.
2. Add template variables.
 - Variable Type: Data Source
 - Variable Name: env
 - Display Name: Application Environment
 - Data Source Scope: All log topics
 - Default Log Topic: Log topic A (production environment)
3. Add charts.
In the **Log Topic** drop-down list, select **Use Data Source Variable** and select the `${env}` variable created in the previous step. Then, charts will use the value of the variable as the data source, that is, **Log topic A (production environment)**.

4. Repeat **Step 3** to add other charts.
5. Go back to the dashboard details page, click the data source variable **Application Environment** at the top of the page, and switch the log topic in the drop-down list of the variable. Then, the charts that use the variable will switch the log topic accordingly.








