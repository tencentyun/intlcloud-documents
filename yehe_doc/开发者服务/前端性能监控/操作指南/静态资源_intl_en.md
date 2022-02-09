This document describes how to monitor static resources. Static resources in a frontend HTML page include JavaScript, CSS, and image files. If the loading of such files takes too long or fails, it will directly affect or even paralyze the page. Static resource monitoring helps you analyze the frontend static resource conditions.

## Prerequisites
You have [connected your application](https://intl.cloud.tencent.com/document/product/1131/44496).

## Directions 
1. Log in to the [RUM console](https://console.cloud.tencent.com/rum).
2. On the left sidebar, click **Static Resource**.
3. On the static resource page, you can view the static resource metrics.

### Aggregated analysis
It displays the change trends of key static resource performance metrics, including static resource request duration and success rate.
- You can click a legend above the chart to hide or show the corresponding data.
- You can display the trend for the specified time period or the past 14 days.
- You can drag the curve to display the static resource duration at a specific time point.
- You can drag the round buttons left and right to adjust the time span of the chart.
![](https://main.qcloudimg.com/raw/27ee49677d3ebf5dc20e5a763efa7c0d.png)

### Page analysis
It displays the average loading duration of all static resources on all pages.
![](https://main.qcloudimg.com/raw/ba9066f501d2f70362ee0eb7ca842ab4.png)

### Top view
- 资源请求 TOP 视图，按接口耗时排序展示静态资源请求情况，最多可展示1000个静态资源。
- Top resources view: it displays the top static resources with the highest number of requests. Up to 1,000 static resources can be displayed.
- Top resource failures view: it displays the top static resources with the highest number of failed requests. Up to 1,000 static resources can be displayed.
![](https://main.qcloudimg.com/raw/02d13e0331d1d4da74e3253bbd21745d.png)

### Other views

| View Name | Description |
|---------|---------|
| Network/Platform view | It uses a pie chart to display the number, percentage, average duration, success rate, TCP connection time, and DNS query time of static resources from each network type/platform, such as 3G, 4G, and Wi-Fi networks as well as macOS, Windows, and iOS platforms. |
| ISP view | It uses a pie chart to display the number, percentage, average duration, success rate, TCP connection time, and DNS query time of static resources from each ISP such as China Mobile, China Telecom, and China Unicom. | 
| Region view | It uses a pie chart to display the number, percentage, average duration, success rate, TCP connection time, and DNS query time of static resources from each region. | 
| Brand/Model view | It uses a pie chart to display the number, percentage, average duration, success rate, TCP connection time, and DNS query time of static resources from each mobile phone brand/model. |
| Browser view | It uses a pie chart to display the number, percentage, average duration, success rate, TCP connection time, and DNS query time of static resources from each browser. |
| Version view | It uses a pie chart to display the number, percentage, average duration, success rate, TCP connection time, and DNS query time of static resources from each application version. You can use `new Aegis` to pass in `version` during application connection to customize the version information related to development. The SDK version is used by default. |
| ext1/ext2/ext3 views | They are custom views. You can customize their parameters passed in during reporting. |
