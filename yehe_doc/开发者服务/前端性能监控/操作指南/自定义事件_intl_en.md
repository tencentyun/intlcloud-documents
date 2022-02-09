
RUM's custom event module allows you to customize the events to be reported and then collects, calculates, and visually displays the data of each reported event metric. For example, if you want to know the number of times a button or link has been clicked, you can use this module to get the information you need.


## Prerequisites
- You have connected your application as instructed in [Application Connection](https://intl.cloud.tencent.com/document/product/1131/44496).
- Select an application connection method as instructed in Connection Guide. Then, use the **reportEvent** method to report the custom event as instructed in **Instance Method**.

## Directions
1. Log in to the [RUM console](https://console.cloud.tencent.com/rum).
2. On the left sidebar, click **Custom Event**.
3. Enter the custom event page to view the performance of the reported event.

### Aggregated analysis
It displays the change trend of triggers of the reported events.
- You can drag the curve to display the number of event triggers at a certain time point.
- You can drag the round buttons left and right to adjust the time span of the chart.
![](https://main.qcloudimg.com/raw/8aa8cd3ae1140f808e9ea5eceafce6dd.png)

### Top custom events view
It displays the top reported events with the highest number of triggers. Up to 1,000 reported events can be displayed. You can also download the top custom events report by clicking the download icon in the upper-right corner.
![](https://main.qcloudimg.com/raw/ce34de21ad7b96de1d2767d4ad9cb6a5.png)

| View Name | Description |
|---------|---------|
| ISP view | It uses a pie chart to display the number and percentage of events from each ISP such as China Mobile, China Telecom, and China Unicom. | 
| Network/Platform view | It uses a pie chart to display the number and percentage of events from each network type/platform, such as 3G, 4G, and Wi-Fi networks as well as macOS, Windows, and iOS platforms. |
| Region view | It uses a pie chart to display the number and percentage of events from each region. | 
| Brand/Model view | It uses a pie chart to display the number and percentage of events from each mobile phone brand/model. |
| Browser view | It uses a pie chart to display the number and percentage of events from each browser. |
| Version view | It uses a pie chart to display the number and percentage of events from each application version. You can use `new Aegis` to pass in `version` during application connection to customize the version information related to development. The SDK version is used by default. |
| ext1/ext2/ext3 views | They are custom views. You can customize their parameters passed in during reporting. |
