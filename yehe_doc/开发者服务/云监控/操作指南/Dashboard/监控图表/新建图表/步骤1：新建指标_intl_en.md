This document describes how to add and edit metrics when creating a monitoring chart.

## Adding Metrics

1. Log in to the Cloud Monitor console and click **Dashboard** > **[Default Dashboard](https://console.cloud.tencent.com/monitor/dashboard2/default)** on the left sidebar.
2. Switch to the dashboard that you want to operate to go to the dashboard management page.
3. Click **<img src="https://main.qcloudimg.com/raw/827988040ba03fd73a5a95cc942eb5cd.png"  style="margin:0;" width="3%">** > **Create a Chart** to go to the chart editing page. Configure the metric information as follows:
	- **Select Monitoring Type**: supports basic monitoring and custom monitoring metrics.
	- **Metric**: select the product type and metric.
	- **Filter**: click "Select a variable" and select a filter condition. Data that meets the condition will be displayed in the chart. If you add multiple filter conditions, only data that meets all the conditions (by running the logical AND operation) will be displayed in the chart.
	- **group by**: similar to the Group by feature of SQL, this feature can group data based on specified labels and then aggregate data according to aggregation algorithms. If you do not select a label, you can customize the metric statistical method for the statistical period, which can be avg, max, min, or sum.
	- **Compare**: day-over-day (compare with the same period yesterday), week-over-week (compare with the same period last week), and custom time comparisons are supported. If you select all the comparison options, the chart will display the day-over-day and week-over-week monitoring curves for the selected instance, making it easier for you to compare the data.
	- **Alias**: you can configure the aliases of all instances with one click. To configure different aliases for different instances, you can create multiple metrics and enter an alias under each metric.
	- **Left Y-Axis, Right Y-Axis**: you can adjust the position of the Y-axis, which can be on the left or on the right.
		![](https://main.qcloudimg.com/raw/2a805996896ca227b3d37c50a8ec8377.png)
4. After configuring the preceding settings, click **<img src="https://main.qcloudimg.com/raw/2cf48d6910973ec3dc7074e05bac24db.png"  style="margin:0;" width="3%">** > **OK**.



#### Creating multiple metrics and copying metrics

You can click **Add a Metric** or **<img src="https://main.qcloudimg.com/raw/4498d80ac2e41bb3eda920ce0a672f0c.png"  style="margin:0;" width="2%">** to display multiple metrics in the same chart for cross-instance metric data comparison.

#### Sorting metrics

You can click the **<img src="https://main.qcloudimg.com/raw/6816e91e4d62686ec5ae31be691e703e.png"  style="margin:0;" width="2%">** icon to adjust the sorting of metrics.

## Editing Metrics

1. Log in to the Cloud Monitor console and click **Dashboard** > **[Default Dashboard](https://console.cloud.tencent.com/monitor/dashboard2/default)** on the left sidebar.
2. Switch to the dashboard that you want to operate to go to the dashboard management page.
3. Find the monitoring chart that you want to edit and click **<img src="https://main.qcloudimg.com/raw/50761560b9ec9266d0fca647018f45d7.png"  style="margin:0;" width="3%">**.
4. In the window that appears, click **Edit** to go to the chart editing page.

## Deleting Metrics

1. Log in to the Cloud Monitor console and click **Dashboard** > **[Default Dashboard](https://console.cloud.tencent.com/monitor/dashboard2/default)** on the left sidebar.
2. Switch to the dashboard that you want to operate to go to the dashboard management page.
3. Find the monitoring chart that you want to edit and click **<img src="https://main.qcloudimg.com/raw/50761560b9ec9266d0fca647018f45d7.png"  style="margin:0;" width="3%">**.
4. In the window that appears, click **Edit** to go to the chart editing page. Click **<img src="https://main.qcloudimg.com/raw/05e8bc16c69923223e588465215152cb.png"  style="margin:0;" width="3%">** to delete the metric.
