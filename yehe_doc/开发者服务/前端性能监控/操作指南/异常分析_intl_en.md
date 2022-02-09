This document describes how to use the exception analysis feature. It can analyze various exceptions, such as JavaScript errors, Promise errors, Ajax request exceptions, JavaScript loading exceptions, and API return code exceptions.

### Exception Analysis
It is used to display the change trend of exceptions in each type.
- You can switch to display exceptions for the specified time period or by day.
- You can drag the two round buttons below the trend chart left and right to adjust the time span.
- You can click a legend above the chart to hide or display the corresponding data.
![](https://main.qcloudimg.com/raw/ecd9c431aa9efe813058ed39563f5df3.png)

### JavaScript Error Rankings
It displays the content and number of occurrences of JavaScript errors. You need to specify the time period first before viewing the error information.
![](https://main.qcloudimg.com/raw/6aa502ed6af965cd08cbc189906a6776.png)

### Other Views

| View Name | Description |
|---------|---------|
| Network/Platform view | It uses a pie chart to display the number and percentage of exceptions from each network type/platform, such as 3G, 4G, and Wi-Fi networks as well as macOS, Windows, and iOS platforms. |
| ISP view | It uses a pie chart to display the number and percentage of exceptions from each ISP such as China Mobile, China Telecom, and China Unicom. | 
| Region view | It uses a pie chart to display the number and percentage of exceptions from each region. | 
| Brand/Model view | It uses a pie chart to display the number and percentage of exceptions from each mobile phone brand/model. |
| Browser view | It uses a pie chart to display the number and percentage of exceptions from each browser. |
| Version view | It uses a pie chart to display the number and percentage of exceptions from each application version. You can use `new Aegis` to pass in `version` during application connection to customize the version information related to development. The SDK version is used by default. |
| ext1/ext2/ext3 views | They are custom views. You can customize their parameters passed in during reporting. |
