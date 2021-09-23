## Overview

With dashboards, you can view the traffic monitoring data of each instance and the total traffic.

[](id:step1)
## Viewing CVM Instance Traffic
>?Bill-by-traffic instances are billed by the public outbound traffic.

1. Go to the [dashboard list in the CM console](https://console.cloud.tencent.com/monitor/dashboard2/dashboards).
2. In the Tencent Cloud service dashboard folder, click the preset **Traffic Monitoring** dashboard.
3. Enter the traffic monitoring dashboard where you can view the overall conditions of CVM instance traffic.
   The use cases of each monitoring dashboard are as follows:
<table>
<tr>
<th  colspan="2">Chart Name</th>
<th>Use Case</th>
</tr>
<tr>
<td  rowspan="4">Public outbound traffic</td>
<td>Total</td>
<td>Bill-by-traffic instances are billed by the public outbound traffic. You can use this chart to view the total traffic of CVM instances in a certain period of time and calculate the corresponding fees. As shown below, 0.41 MB is the total traffic used in the current time period. You can refer to the <a href = "https://intl.cloud.tencent.com/document/product/213/39743">bill-by-traffic rules</a> to calculate the bandwidth fees incurred in the current time period.</td>
</tr>
<tr>
<td>General trend</td>
<td>View the public outbound traffic usage of all instances.</td>
</tr>
<tr>
<td>By instance</td>
<td>View the public outbound traffic usage by instance.</td>
</tr>
<tr>
<td>Top 5 instances</td>
<td>View the data of the top 5 instances that use the most traffic among the instances you filter.</td>
</tr>
<tr>
<td  colspan="2">General trend of public inbound and outbound bandwidth</td>
<td>Observe the difference between public outbound and inbound bandwidth.</td>
</tr>
<tr>
<td  colspan="2">Public outbound bandwidth</td>
<td>View the public outbound bandwidth data and observe user access to CVM.</td>
</tr>
<tr>
<td  colspan="2">Public inbound bandwidth</td>
<td>View the public inbound bandwidth data and observe user resource upload to CVM. To do so, click **Create Dashboard** in the top-left corner of the dashboard list page to enter the dashboard creation page.</td>
</tr>
</table>



[](id:step2)
## Viewing Traffic of Other Tencent Cloud Services

>?Currently, only CVM traffic has a preset monitoring dashboard. To view the traffic trends of other Tencent Cloud services, you need to create dashboards as shown below. Before creation, please check out the [dashboard creation process](https://intl.cloud.tencent.com/document/product/248/35282) first.

The following uses creating a chart for the total private traffic of TencentDB as an example:

### Step 1. Create a traffic monitoring dashboard

1. Go to the [dashboard list in the CM console](https://console.cloud.tencent.com/monitor/dashboard2/dashboards).
2. On the dashboard list page, click **Create Dashboard**.
3. On the dashboard creation page, click **Save**.
4. Enter the dashboard name in the pop-up window, select the folder to which it belongs, and click **Save**.

### Step 2. Create a template variable

1. Click the **![](https://main.qcloudimg.com/raw/8e26fe2eacdd794457a53a745bd48f3c.png)** icon on the page of the created dashboard.
2. Click **Template Variable** in the pop-up window to enter the template variable management page.
3. Click **Create**, enter the variable name, and select the associated tag as "TencentDB - MySQL - server monitoring instance".
4. After completing the configuration, click **OK**.



### Step 3. Create a chart
1. Return to the dashboard management page and click **Create Chart**.
2. Configure on the chart creation page as instructed/shown below:
   - Metric: select "TencentDB - MySQL - server monitoring" and "Core metric - private outbound traffic".
   - Filter: select "Template variable" and select the corresponding variable name.
   - Chart name: enter "Private outbound traffic: total".
   - Chart type: select the "Digit" chart type.

3. After completing the configuration, click **Save** in the top-right corner.
> ?If you need to create charts in other types, please see [Use Cases of Different Chart Types](https://intl.cloud.tencent.com/document/product/248/38479).
