
This document describes how to view a monitoring chart.


## Preparations
1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor).
2. In the left sidebar, click **Dashboard** > **Dashboard List** to go to the dashboard list page.
3. In the dashboard list, find the dashboard that you want to view, and click the dashboard name to go to the dashboard management page.


## Viewing Charts in the Full Screen Mode
Click the "Full-Screen Chart" icon **<img src="https://main.qcloudimg.com/raw/9bd9730e6a3135b097d648f752399fac.png"  style="margin:0;" width="3%">** in the upper-right corner of the chart to view it in the full-screen mode.

You can press **ESC** or click the **<img src="https://main.qcloudimg.com/raw/0be3daafc00fb030f84ed2123e05e083.png"  style="margin:0;" width="3%">** icon in the upper-right corner to exit the full screen mode.

## Chart Scaling and Moving
- Chart scaling: you can scale a chart by hovering over the lower-right corner of the chart until a straight-angle icon appears, as shown in the figure below:
![](https://main.qcloudimg.com/raw/af0c24e97e2d3fbb4fbd19f66ee8de79.png)
- Chart moving: you can move a chart by hovering over the name of the chart until a movement icon appears, as shown in the figure below:
![](https://main.qcloudimg.com/raw/b5b73ac325e0a62ad3f77a947b785f55.png)

## Viewing the Monitoring Data of a Period
You can view the monitoring data of a period by hovering over the monitoring chart, as shown in the figure below:
![](https://main.qcloudimg.com/raw/06ccca4fb26ff980e318809e68b88e7b.png)

## Viewing Data by Using the Variable Selector

If you have many instances, you can define a template variable to dynamically switch labels so that you can view the monitoring data of different instances in the same monitoring chart.
![](https://main.qcloudimg.com/raw/996212d9fed2a69e269606cfa306b08d.png)
>? To create a template variable, see [Configuring a Dashboard](https://intl.cloud.tencent.com/document/product/248/38472).


## Adjusting the Time Span of Charts to View Monitoring Data
By default, dashboards display the data of the last 12 hours.

You can adjust the time span and granularity for all charts in the current dashboard by using the time selector in the upper-right corner of the dashboard. In this way, you can review historical monitoring data and perform troubleshooting.
![](https://main.qcloudimg.com/raw/87d43329f351da1614b312d362ffea44.png)

**Time Periods and Corresponding Chart Granularities**

| Time Range | Default Statistical Period |
| ------------- | ------------ |
| <=1h | 1min |
| (1h,12h] | 1min |
| (12h,3d] | 5min |
| (3d,30d] | 1h |
| (30d,186d] | 1d |


