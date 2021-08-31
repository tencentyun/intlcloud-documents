

This document describes how to view a monitoring chart.

## Preparations


1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor).
2. On the left sidebar, click **Dashboard List** to enter the dashboard list page.
3. In the dashboard list, find the dashboard that you want to view, and click the dashboard name to enter the dashboard management page.

## Viewing Charts by Using Metric Sorting Feature
Click **<img src="https://main.qcloudimg.com/raw/bc2e0e986ee5ad450e8a090582ca0697.png" width="2.4%">** in the chart to enable the TopN feature, and then adjust the sorting rule and display quantity. This makes it easier for you to view the loads of machines in batches.
![](https://main.qcloudimg.com/raw/06e8a0f40b9717da9daaae11298b111a.png)

If you enable the sorting feature when [creating a metric](https://intl.cloud.tencent.com/document/product/248/38477), you can also click the TopN button in the chart to adjust the sorting rule and display quantity and disable the sorting feature. This makes it easier for you to view the loads of machines in batches.
![](https://main.qcloudimg.com/raw/3e7cd162733479cd853a11f225ea8f8d.png)

## Viewing Charts in Full Screen Mode

Click **<img src="https://main.qcloudimg.com/raw/7aa3947e6678d2e035766c2cc912aab3.png"  style="margin:0;" width="3%">** > **Full-Screen Chart** in the top-right corner of the chart to view it in the full-screen mode.
![](https://main.qcloudimg.com/raw/35b85b5a1d17ac67277ac1fbbfb255af.png)
You can press **ESC** or click the **<img src="https://main.qcloudimg.com/raw/0be3daafc00fb030f84ed2123e05e083.png"  style="margin:0;" width="3%">** icon in the top-right corner to exit the full screen mode.

## Viewing Instance Details

Click the **<img src="https://main.qcloudimg.com/raw/497169f09047d1435cf8fedb6fb12b39.png" style="margin:0;" width="3%">** icon (red circle 1 in the figure below) in the top-right corner of the chart to display the instance details. You can also click the **<img src="https://main.qcloudimg.com/raw/9f49988ef96508fb071de4a6950c4a12.png" style="margin:0;" width="3%">** icon (circle 2 in the figure below) in the top-right corner of the instance details to select the fields and values to be displayed.
![](https://main.qcloudimg.com/raw/f0b3ab4361e60fcf462d3815e8948908.png)



## Scaling and Moving Chart

- Chart scaling: you can scale a chart by hovering over the bottom-right corner of the chart until a straight-angle icon appears as shown below:
![](https://main.qcloudimg.com/raw/c72680059f222810059717ebea194993.png)
- Chart moving: you can move a chart by hovering over the name of the chart until a movement icon appears as shown below:
![](https://main.qcloudimg.com/raw/3eacae042692b3a686eb6ab9f21f0fa3.png)

## Viewing Monitoring Data in Specific Period

You can view the monitoring data in a specific period by hovering over the monitoring chart as shown below:
![](https://main.qcloudimg.com/raw/5fc295ca3a8578bc6dec8d6e6a28eb16.png)

## Viewing Data by Using Variable Selector

If you have many instances, you can define a template variable to dynamically switch tags, so that you can view the monitoring data of different instances in the same monitoring chart.
![](https://main.qcloudimg.com/raw/e1dbd073718dbf503f32bf686f4faf57.png)

>?To create a template variable, please see [Basic Configuration](https://intl.cloud.tencent.com/document/product/248/38472).

## Adjusting the Time Span of Charts to View Monitoring Data

By default, dashboards display the data of the last 12 hours.

You can adjust the time span and granularity for all charts in the current dashboard by using the time selector in the top-right corner of the dashboard. In this way, you can review historical monitoring data and perform troubleshooting.
![](https://main.qcloudimg.com/raw/8684005a0e3b9f07759d2660a593cb03.png)

**Time periods and corresponding chart granularities**

| Time Period | Default Statistical Period |
| ----------- | ------------ |
| <=1 hour | 1 min |
| (1 hour, 12 hours] | 1 min |
| (12 hours, 3 days] | 5 min |
| (3 days, 30 days] | 1 hour |
| (30d,186d] | 1d |
