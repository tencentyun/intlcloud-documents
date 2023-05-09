

## Type Description
<table>
<thead>
<tr>
<th width=20%>Type</th>
<th align="left">Description</th>
<th align="left">Scope</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Filter in the drop-down list</td>
<td align="left">Filter data in all charts on the dashboard by specifying the field value. If statistics is enabled in the index configuration of the log topic for the filter field, the field value can be automatically obtained as a list item.</td>
<td align="left">All charts on the dashboard</td>
</tr>
<tr>
<td align="left">Filter by search statement</td>
<td align="left">Filter data in all charts on the dashboard by entering a search statement, that is, add a filter in the query statement of the charts.<strong>Filter by search statement includes filter by range, NOT, and full text.</strong></td>
<td align="left">All charts on the dashboard</td>
</tr>
<tr>
<td align="left">Data source variable</td>
<td align="left">A data source variable enables batch switching data sources of the charts on the dashboard. It is applicable to scenarios such as applying a dashboard to multiple log topics and comparing data in blue and green on the dashboard.</td>
<td align="left">Charts that use the variable on the dashboard</td>
</tr>
<tr>
<td align="left">Custom variable</td>
<td align="left">A custom variable can be set to a static input or a value from a dynamic query and applied to search statements, titles, and text charts for quick batch statement modification.</td>
<td align="left">Charts that use the variable on the dashboard</td>
</tr>
</tbody></table>



## Filter

### Configuring the filter in the drop-down list

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Dashboard** to enter the dashboard management page.
3. Click the ID/name of the target dashboard to enter the dashboard details page.
4. Click **Add Filter and Variable** at the top to enter the settings page.

5. In the pop-up window, configure the filter in the drop-down list and click **OK**.

<table>
<thead>
<tr>
<th>Form Element</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Type</td>
<td>Different types correspond to different configuration items and application scenarios. Here, select **Filter in the drop-down list**.</td>
</tr>
<tr>
<td>Filter alias</td>
<td>It is the filter name displayed on the UI, which is optional. If it is left empty, the filter field will be used automatically.</td>
</tr>
<tr>
<td>Log topic</td>
<td>It is the log topic to which the filter field belongs.</td>
</tr>
<tr>
<td>Filter field</td>
<td>It is the object field to be filtered.</td>
</tr>
<tr>
<td>Dynamic option</td>
<td>After it is enabled, the filter field value will be obtained automatically as the filter option.</td>
</tr>
<tr>
<td>Static option</td>
<td>A static option is optional, needs to be added manually, and will be always displayed. You can configure its alias.</td>
</tr>
<tr>
<td>Default filter</td>
<td>It is the default filter of the dashboard and is optional.</td>
</tr>
<tr>
<td>Support for multiple items</td>
<td>After it is enabled, multiple filters can be selected as the filter condition.</td>
</tr>
</tbody></table>
6. Go back to the dashboard details page, click the filter icon, and select the target filter. Then, the dashboard data will be refreshed to the filtered content.




### Configuring filter by search statement
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Dashboard** to enter the dashboard management page.
3. Click the ID/name of the target dashboard to enter the dashboard details page.
4. Click **Add Filter and Variable** at the top to enter the settings page.

5. In the pop-up window, set the information of the filter by search statement and click **Submit**.

<table>
<thead>
<tr>
<th align="left">Form Element</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Type</td>
<td align="left">Different types correspond to different configuration items and application scenarios. Here, select **Filter by search statement**.</td>
</tr>
<tr>
<td align="left">Filter name</td>
<td align="left">It is the unique filter name.</td>
</tr>
<tr>
<td align="left">Filter alias</td>
<td align="left">It is the filter name displayed on the UI, which is optional.</td>
</tr>
<tr>
<td align="left">Log topic</td>
<td align="left">It is the log topic to which the filter field belongs.</td>
</tr>
<tr>
<td align="left">Mode</td>
<td align="left">It is the mode for inputting search statements. Here, interactive and statement modes are supported.</td>
</tr>
<tr>
<td align="left">Default filter</td>
<td align="left">It is the default filter of the dashboard and is optional.</td>
</tr>
</tbody></table>
6. Go back to the dashboard details page, click the filter icon, and select the target filter. Then, the dashboard data will be refreshed to the filtered content.
**Filter by search statement includes filter by range, NOT, and full text.**




## Variable

### Configuring the data source variable

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Dashboard** to enter the dashboard management page.
3. Click the ID/name of the target dashboard to enter the dashboard details page.
4. Click **Add Filter and Variable** at the top to enter the settings page.

5. In the pop-up window, configure the template variable information and click **Submit**.

<table>
<thead>
<tr>
<th align="left">Form Element</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Variable type</td>
<td align="left">It is the variable type. Different types correspond to different configuration items and application scenarios. Here, select **Data source variable**.</td>
</tr>
<tr>
<td align="left">Variable name</td>
<td align="left">It is the name of the variable in the search statement and can contain only letters and digits.</td>
</tr>
<tr>
<td align="left">Displayed name</td>
<td align="left">It is the variable name displayed on the dashboard, which is optional. If it is empty, the variable name will be used automatically.</td>
</tr>
<tr>
<td align="left">Data source scope</td>
<td align="left">It is the optional scope of the variable value and defaults to **All Log Topics**. You can select **Custom Filter** and set a filter to view only log topics that meet the condition.</td>
</tr>
<tr>
<td align="left">Default log topic</td>
<td align="left">It is the default log topic.</td>
</tr>
</tbody></table>
5. Go back to the dashboard details page and click **More** > **Edit Chart**.
>?If there are no charts on your dashboard, [add charts](https://intl.cloud.tencent.com/document/product/614/43560).
6. On the **Search Statement** tab of **Edit Chart**, click **Log Topic**, select **Use Data Source Variable**, and select the created template variable.

7. Click **Save**.
8. On the dashboard details page, click the **Data Source** drop-down list and select another log topic. Then the system changes automatically changes the data source of the chart using the variable accordingly.


### Configuring the custom variable
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Dashboard** to enter the dashboard management page.
3. Click the ID/name of the target dashboard to enter the dashboard details page.
4. Click **Add Filter and Variable** at the top to enter the settings page.

5. In the pop-up window, set the information of the custom variable and click **Submit**.

	
	 <table>
<thead>
<tr>
<th align="left">Form Element</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Type</td>
<td align="left">It is the variable type. Different types correspond to different configuration items and application scenarios. Here, select **Data source variable**.</td>
</tr>
<tr>
<td align="left">Variable name</td>
<td align="left">It is the name of the variable in the search statement and can contain only letters and digits. A variable is referenced in the format of <b>${Variable name}</b>.</td>
</tr>
<tr>
<td align="left">Variable alias</td>
<td align="left">It is the variable name displayed on the dashboard, which is optional. If it is empty, the variable name will be used automatically.</td>
</tr>
<tr>
<td align="left">Static variable value</td>
<td align="left">A static variable value needs to be added manually and will be always displayed. You can configure its alias.</td>
</tr>
<tr>
<td align="left">Dynamic variable value</td>
<td align="left">After it is enabled, you can select a log topic, enter a search and analysis statement, and use the search and analysis result as the optional variable value.</td>
</tr>
<tr>
<td align="left">Default value</td>
<td align="left">The default value is the variable value and is required.</td>
</tr>
</tbody></table>


6. Go back to the dashboard details page and click **More** > **Edit Chart**.
   
>? If there are no charts on your dashboard, [add charts](https://intl.cloud.tencent.com/document/product/614/43560).

7. On the **Search Statement** tab of **Edit Chart**, insert the created custom variable **${interval}** to replace the original text.

8. Click **Apply to Dashboard**.
9. Go back to the dashboard details page, click the **Time Granularity** drop-down list at the top, and change the time granularity. Then, you can see that the charts inserted with the variable change accordingly.

### FAQs

**Why does a configured data source variable not take effect or take effect only on some charts?**
A data source variable does not apply directly to all charts on the dashboard. It applies only to those charts that use it on the chart editing page.

## Examples

### Analyzing the performance metrics of different application APIs on the dashboard (filter in the drop-down list)

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
3. Add a filter in the drop-down list.
   - Type: Filter in the drop-down list
   - Display Name: API name
   - Log Topic: Log topic A
   - Select field: interface
4. Go back to the dashboard details page, and you can see this variable on the top of the page.
   - If **API Name** is not specified, data is not filtered, and the charts on the dashboard display all data, that is, the overall performance metrics of the application.

   - If **API Name** is specified, all charts on the dashboard use the specified API as the filter condition to filter data and display the performance metrics of the API.


### Viewing the production and test environment performance metrics on the dashboard separately (data source variable)

#### Requirement

An application has a production environment and a test environment, and logs are collected to **Log topic A (production environment)** and **Log topic B (test environment)**. Therefore, during application development, testing, and Ops, you need to pay attention to the performance metrics of the two environments.

#### Solution
1. Create a dashboard.
2. Add variables.
   - Variable Type: Data Source
   - Variable Name: env
   - Display Name: Application Environment
   - Data Source Scope: All log topics
   - Default Log Topic: Log topic A (production environment)
3. Add charts.
   In the **Log Topic** drop-down list, select **Use Data Source Variable** and select the `${env}` variable created in the previous step. Then, charts will use the value of the variable as the data source, that is, **Log topic A (production environment)**.

4. Repeat **Step 3** to add other charts.
5. Go back to the dashboard details page, click the data source variable **Application Environment** at the top of the page, and switch the log topic in the drop-down list of the variable. Then, the charts that use the variable will switch the log topic accordingly.

