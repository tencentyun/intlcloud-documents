
The custom speed test feature allows you to customize breakpoints to report data and collects, calculates, and displays the reported data. For example, if you want to know the execution time of a function or page mounted time, you can use this module to get the information you need.


## Prerequisites
- You have connected your application as instructed in [Application Connection](https://intl.cloud.tencent.com/document/product/1131/44496).
- Select an application connection method as instructed in Connection Guide. Then, use the **reportTime** or **time and timeEnd** method to customize breakpoints to report data as instructed in **Instance Method**.

## Directions
1. Log in to the [RUM console](https://console.cloud.tencent.com/rum).
2. On the left sidebar, click **Custom Speed Test**.
3. On the custom speed test page, you can view the performance metrics of reported resources.

### Aggregated analysis
It displays the change trend of the reported resource duration, including duration and percentage in different time periods.
- You can click a legend above the chart to hide or show the corresponding data.
- You can display the trend for the specified time period or the past 14 days.
- You can drag the curve to display the duration at a specific time point.
- You can drag the round buttons left and right to adjust the time span of the chart.
![](https://main.qcloudimg.com/raw/9cd7ff9028755ab8ef8b6cadb5865c26.png)

### Top resources view
It displays the top reported resources with the longest average duration. Up to 1,000 reported resources can be displayed. You can also download the report of top resources for custom speed test by clicking the download icon in the top-right corner.
![](https://main.qcloudimg.com/raw/3fd8f295ead21e3af2683b7dd234a8ff.png)


### Other views
| View Name | Description |
|---------|---------|
| ISP view | It uses a pie chart to display the number, percentage, and average duration of resources for custom speed test from each ISP such as China Mobile, China Telecom, and China Unicom. | 
| Network/Platform view | It uses a pie chart to display the number, percentage, and average duration of resources for custom speed test from each network type/platform, such as 3G, 4G, and Wi-Fi networks as well as macOS, Windows, and iOS platforms. |
| Region view | It uses a pie chart to display the number, percentage, and average duration of resources for custom speed test from each region. | 
| Brand/Model view | It uses a pie chart to display the number, percentage, and average duration of resources for custom speed test from each mobile phone brand/model. |
| Browser view | It uses a pie chart to display the number, percentage, and average duration of resources for custom speed test from each browser. |
| Version view | It uses a pie chart to display the number, percentage, and average duration of resources for custom speed test from each application version. You can use `new Aegis` to pass in `version` during application connection to customize the version information related to development. The SDK version is used by default. |
| ext1/ext2/ext3 views | They are custom views. You can customize their parameters passed in during reporting. |
