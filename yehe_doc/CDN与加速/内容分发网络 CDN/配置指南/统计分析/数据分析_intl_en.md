You can check your end-user distribution and resource usage on the **Data Analysis** page.

Log in to the [CDN console](https://console.cloud.tencent.com/cdn) and select **Statistics** > **Data Analysis** on the left sidebar to access the **Data Analysis** page.

- The maximum time period for query is 31 days. Historical data is retained for 90 days.
- You can query historical data generated in the last three months.

>! ECDN does not support displaying the number of unique IP access requests and user access region distribution currently.

## Data Overview

Data overview in your specified report dimension is displayed. 
The data overview varies according to the billing method.
For bill-by-traffic, total traffic, average traffic hit rate and total requests are displayed.
For bill-by-bandwidth, peak bandwidth, peak origin-pull bandwidth, and total requests are displayed. 


## User Access District Distribution

The user access district distribution is displayed in your specified report dimension. Based on the source client IP, the user access district can be determined, and displayed in a map or list, allowing you to view the district distribution of your users. You can view statistics of provinces in the Chinese mainland and regions outside the Chinese mainland.


## Traffic

Traffic curve in your specified report dimension is displayed. You can choose to view the curve of billed traffic or origin-pull traffic.


## Bandwidth

Bandwidth curve in your specified report dimension is displayed. You can choose to view the curve of billable bandwidth or origin-pull bandwidth. The peak bandwidth curve is supported.


## Requests

Total request curve in your specified report dimension is displayed.


## Error Codes

Numbers and proportions of error codes in your specified report dimension are displayed.


## TOP10 URLs

The top 10 URLs in your specified report dimension are displayed. You can sort them by usage or total requests.


## TOP 10 Projects

The top 10 projects in your specified report dimension are displayed.

## TOP 10 Domain Names

The top 10 domain names in your specified report dimension are displayed.

## Unique IP Access Requests

The unique IP access requests in the specified time period are counted by deduplicating the access client IPs in the log:
If the time range is less than or equal to one day, a deduplicated IP curve with a 5-minute granularity will be provided.
Domain name statistics are counted by deduplicating the active quantity in a full day. If there are multiple domain names, projects or accounts, the statistics are counted by accumulating the daily active quantity of each one with a 5-minute granularity.
>! Only data for the last 30 days can be queried.



## User ISP Distribution

Based on the source client IP, the user ISP can be determined and displayed in a pie chart or list, allowing you to view the ISP distribution of your users.

