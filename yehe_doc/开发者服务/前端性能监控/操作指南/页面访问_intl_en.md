This document describes how to use the page view feature. It displays page view metrics (UV and PV) and supports multidimensional page view analysis.

## Directions
1. Log in to the [RUM console](https://console.cloud.tencent.com/rum).
2. On the left sidebar, click **Page View**.
3. On the page view page, view the page view metrics.

### Advanced filters
You can filter data by business system, page address, time, ISP, network type, and platform.
### Data analysis
It displays the data analysis menu by default where only the PV change trend chart is displayed.
- You can click **Data Export** in the top-right corner to export the PV data for the specified time period.
- You can drag the two round buttons below the trend chart left and right to adjust the time span.
![](https://main.qcloudimg.com/raw/4ff943b4bbd21158e8db2f0c7e072537.png)

### PV and UV
It displays the PV and UV change trends.
- You can click the PV/UV legends to hide or show the PV/UV curves.
- You can drag the two round buttons below the trend chart left and right to adjust the time span.
![](https://main.qcloudimg.com/raw/d30865b37ab5330e7760e96da3e475ec.png)

### Top pages view
It displays the top page URLs with the highest page views. Up to 1,000 page URLs can be displayed.
![](https://main.qcloudimg.com/raw/7375295e0ce4bd0b620d1330aec6b9e8.png)


### Other views

| View Name | Description |
|---------|---------|
| ISP view | It uses a pie chart to display the number and percentage of visits from each ISP such as China Mobile, China Telecom, and China Unicom. | 
| Network/Platform view | It uses a pie chart to display the number and percentage of visits from each network type/platform, such as 3G, 4G, and Wi-Fi networks as well as macOS, Windows, and iOS platforms. |
| Region view | It uses a pie chart to display the number and percentage of visits from each region. | 
| Brand/Model view | It uses a pie chart to display the number and percentage of visits from each mobile phone brand/model. |
| Browser view | It uses a pie chart to display the number and percentage of visits from each browser. |
| Version view | It uses a pie chart to display the number and percentage of visits from each application version. You can use `new Aegis` to pass in `version` during application connection to customize the version information related to development. The SDK version is used by default. |
| ext1/ext2/ext3 views | They are custom views. You can customize their parameters passed in during reporting. |

