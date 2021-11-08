This document describes how to create and edit a metric when creating a monitoring chart.

## Creating Metric

1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/dashboard2/default).
2. Switch to the target dashboard to enter the dashboard management page.
3. Click <img src="https://main.qcloudimg.com/raw/827988040ba03fd73a5a95cc942eb5cd.png"  style="margin:0;" width="3%"> > **Create Chart** to enter the chart editing page. Configure the metric information as follows:
   - **Select Monitoring Type**: select basic monitoring or custom monitoring metrics.
   - **Metric**: select the product type and metric.
   - **Filter**: select a filter to extract the data that meets the criteria for display on the chart.
    - Instance: the chart will display the monitoring data of the selected instances.
    - Tag: the chart will display the instances to which the tag is bound. For more information on how to set and use tags, please see [Using Tag and TopN Features to Automatically Monitor Cloud Resources in Batches](https://intl.cloud.tencent.com/zh/document/product/248/39349).
   <dx-alert infotype="explain" title="">
   The dashboard tag feature currently is only available for CVM’s basic monitoring and will be supported for more Tencent Cloud services in the future.
   </dx-alert>
    - Template Variable: the chart will display the instances filtered by the template variable. For more information on how to configure template variables, please see [Template Variables](https://intl.cloud.tencent.com/document/product/248/38473).
   - **Group by** (this feature is not available for the tag filter): similar to the Group By feature of SQL, this feature can group data based on specified tags and then aggregate data according to aggregation algorithms. If you don't select a tag, you can customize the metric statistical mode for the statistical period, which can be avg, max, min, or sum.
   - **Comparison**: day-over-day (compare with the same period yesterday), week-over-week (compare with the same period last week), and custom time comparisons are supported. If you select all the comparison options, the chart will display the day-over-day and week-over-week monitoring curves for the selected instance, making it easier for you to compare the data.
   - **Left Y-axis/Right Y-axis**: you can choose to place the Y-axis on the left or on the right.
 - Additional configuration items.
    - **Alias**: you can configure an alias for all instances quickly. To configure different aliases for different instances, you can create multiple metrics and enter an alias under each metric.
    - **Enable Sorting**: the instances bound to the chart will be sorted according to the configured sorting rule and displayed quantity, making it easier for you to monitor the loads of machines in batches.
    - **Sorting Rule**: you can sort metrics in a variety of ways and filter instances according to the sorting result.
    - **Displayed Quantity**: it denotes the number of instances to be displayed.
     For example, if you set the sorting rule to "MAX; DESC" and the displayed quantity to 10, the chart will display the top 10 instances by the maximum value in descending order.
	  ![](https://main.qcloudimg.com/raw/2b5754a7878cb2f918759aa5289d1a2a.png)
4. After configuring the settings, click <img src="https://main.qcloudimg.com/raw/2cf48d6910973ec3dc7074e05bac24db.png"  style="margin:0;" width="3%">.



#### Creating multiple metrics and copying metrics

You can click **Create Metric** or <img src="https://main.qcloudimg.com/raw/4498d80ac2e41bb3eda920ce0a672f0c.png"  style="margin:0;" width="2.2%"> to display multiple metrics on the same chart for cross-instance metric data comparison.

#### Sorting metrics

You can click the <img src="https://main.qcloudimg.com/raw/6816e91e4d62686ec5ae31be691e703e.png"  style="margin:0;" width="2.2%"> icon to adjust the sorting of metrics.


## Editing Metric

1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/dashboard2/default).
2. Switch to the target dashboard to enter the dashboard management page.
3. Find the monitoring chart to be edited and click <img src="https://main.qcloudimg.com/raw/50761560b9ec9266d0fca647018f45d7.png"  style="margin:0;" width="3%">.
4. Click **Edit** in the pop-up window to enter the chart editing page.



## Deleting Metric

1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/dashboard2/default).
2. Switch to the target dashboard to enter the dashboard management page.
3. Find the monitoring chart to be edited and click <img src="https://main.qcloudimg.com/raw/50761560b9ec9266d0fca647018f45d7.png"  style="margin:0;" width="3%">.
4. Click **Edit** in the pop-up window to enter the chart editing page, and click <img src="https://main.qcloudimg.com/raw/05e8bc16c69923223e588465215152cb.png"  style="margin:0;" width="3%"> next to the corresponding metric.
