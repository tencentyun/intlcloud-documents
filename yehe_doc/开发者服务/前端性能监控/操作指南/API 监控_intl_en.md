This document describes how to use API monitoring to monitor API call conditions, such as HTTP code success rate and API request duration.
## Prerequisites
You have [connected your application](https://intl.cloud.tencent.com/document/product/1131/44496).

## Directions 
1. Log in to the [RUM console](https://console.cloud.tencent.com/rum).
2. On the left sidebar, click **API Monitoring**.
3. On the API monitoring page, you can view the API performance metrics.

### Aggregated analysis
It displays the change trends of key API performance metrics, including API request duration and success rate.
- You can click a legend above the chart to hide or show the corresponding data.
- You can display the trend for the specified time period or the past 14 days.
- You can drag the curve to display the API duration at a specific time point.
- You can drag the round buttons left and right to adjust the time span of the chart.
![](https://main.qcloudimg.com/raw/8f598b372c090dcd109bc61ea51d0502.png)

### Page analysis
It displays the average API request duration on each page.
![](https://main.qcloudimg.com/raw/467ce76fb4c9fdddb2d64ca877755dec.png)

### Top view
- Top API requests view: it displays the top API requests with the highest number of samples. Up to 1,000 APIs can be displayed.
- Top APIs with HTTP status code 40x view: it displays the top APIs with the highest numbers of HTTP status codes 40x. Up to 1,000 APIs can be displayed.
- Top APIs with HTTP status code 50x view: it displays the top APIs with the highest numbers of HTTP status codes 50x. Up to 1,000 APIs can be displayed.
![](https://main.qcloudimg.com/raw/5c2419b94cebd5d61e0a1252bd9de8af.png)

### Other views
| View Name | Description |
|---------|---------|
| Network/Platform view | It uses a pie chart to display the number, percentage, and average duration of API requests from each network type/platform, such as 3G, 4G, and Wi-Fi networks as well as macOS, Windows, and iOS platforms. |
| HTTP response code view | It uses a pie chart to display the number of errors, percentage, and average duration of each HTTP response code. |
| `retcode` view | It uses a pie chart to display the number of errors, percentage, and average duration of each `retcode`. |
| ISP view | It uses a pie chart to display the number, percentage, and average duration of API requests from each ISP such as China Mobile, China Telecom, and China Unicom. | 
| Region view | It uses a pie chart to display the number, percentage, and average duration of API requests from each region. | 
| Brand/Model view | It uses a pie chart to display the number, percentage, and average duration of API requests from each mobile phone brand/model. |
| Browser view | It uses a pie chart to display the number, percentage, and average duration of API requests from each browser. |
| Version view | It uses a pie chart to display the number, percentage, and average duration of API requests from each application version. You can use `new Aegis` to pass in `version` during application connection to customize the version information related to development. The SDK version is used by default. |
| ext1/ext2/ext3 views | They are custom views. You can customize their parameters passed in during reporting. |

