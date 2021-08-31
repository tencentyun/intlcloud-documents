You can go to the [Conversion Funnel](https://console.cloud.tencent.com/tpns/convertfunnel) page to view and analyze the push conversion data of an application in different dimensions. We strongly recommend that you visit the conversion funnel page on a daily basis so that you can identify push conversion opportunities and stuck points in time and constantly optimize the push strategy to maximize the benefits of push.

## Metrics

- **Planned Sends:** the number of non-unique devices available for the push tasks on the day
- **Actual Sends:** the number of non-unique devices to which messages were pushed on the day
- **Total Reaches:** the number of non-unique messages pushed on the day (with TPNS or vendor channel arrival receipt)
- **Total Clicks:** the number of non-unique clicks on pushed messages
- **Send Rate (PV):** Actual sends/Planned sends x 100%
- **Reach Rate (PV):** Total reaches/Actual sends x 100%
- **Click Rate (PV):** Total clicks/Total reaches x 100%
- **Planned Target Users:** the number of unique devices available for the push tasks on the day
- **Actual Target Users:** the number of unique devices to which messages were pushed on the day
- **Unique Reaches:** the number of unique devices that the pushed messages reached on the day
- **Unique Clicks:** the number of unique devices on which messages were clicked on the day
- **Send Rate (UV):** Actual target users/Planned target users x 100%
- **Reach Rate (UV):** Unique reaches/Actual target users x 100%
- **Click Rate (UV):** Unique clicks/Unique reaches x 100%


## Conversion Overview Yesterday

You can quickly view yesterday's overall conversion effect in the **Conversion Overview Yesterday** module and view the day-over-day fluctuations of metrics in the day-over-day comparison module.


## Statistical Dimension 



1. You can view conversion data by **a specified time range**, which can be the last 90 days at maximum.
>? If you select a single day (for example, **Today**, **Yesterday**, or "2021-06-06 ~ 2021-06-06"), the data granularity for the statistics area at the bottom is hour. Otherwise, the data granularity is day.
2. You can choose to view conversion data by **Count (PV)** or **Users (UV)**. For **Count (PV)**, data is not deduplicated. For **Users (UV)**, data is deduplicated in the device dimension.
For example, if 10 messages were sent to the same device one day, and all the messages successfully reached the device and were clicked, the **Total Clicks** is 10 in the **Count (PV)** dimension and is 1 in the **Users (UV)** dimension. The same principle applies to other metrics.
3. You can view conversion data by **push plan**. We strongly recommend that you divide your business into different [push plans](https://intl.cloud.tencent.com/document/product/1024/37452) by scenario and analyze conversion rates by scenario.
For example, if custom A's application has three push plans **Operational activities**, **User engagement**, and **Gifts for new users**, customer A can view the conversion effect of each or all of these push plans, facilitating constant growth strategy optimization.
4. You can view conversion data by **push channel**.
5. You can view conversion data by **message type**. If you use TPNS to send notification bar messages, silent messages, and in-app messages, you can view the conversion effect of each or all of these message types.


## Data Analysis

In the data analysis area, you can view data trends and details, and download data. The statistics displayed in this area change dynamically with the filters you specify.

### Trend

In the **Trend** area, you can view push conversion trends in the time dimension.


### Details

1. Click the **Details** tab to view the detailed data displayed according to specified filters.
2. Click **Download Data** to export data tables to CSV files to analyze the data conversion effect in more detail.

>? If the statistical period spans days, data is classified according to the time when the data is reported. For example, if a message was delivered and reached device A on March 1, but it was clicked on March 2, the corresponding **Planned Sends**, **Actual Sends**, and **Total Reaches** will be calculated for March 1, but the corresponding **Total Clicks** will be calculated for March 2.
>









