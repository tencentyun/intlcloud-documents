The **Data Analysis** page displays various types of charts by analyzing user sources based on access logs to help you understand your user distribution and business usage.

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and select **Statistics** > **Data Analysis** on the left sidebar to enter the **Data Analysis** page.

- You can query data generated within a maximum time period of 31 days. Historical data is retained for 90 days.
- You can query historical data generated in the last three months.

## Unique IP access requests
The number of unique IP access requests in the specified time period is calculated by deduplicating access client IPs in the log:
- If the time range is less than or equal to one day, a deduplicated IP curve with a 5-minute granularity will be provided.
- Domain name statistics are counted by deduplicating the active quantity in a full day. If there are multiple domain names, projects or accounts, the statistics are counted by accumulating the daily active quantity of each one with a 5-minute granularity.

## User access district distribution
The district of the access requester can be identified via the source client IP, which can be displayed in a map or list, allowing you to view the district distribution of your users.

## User ISP distribution
The ISP of the access requester can be identified via the source client IP, which can be displayed in a pie chart or list, allowing you to view the ISP distribution of your users.
![](https://main.qcloudimg.com/raw/eb7b45eb5458a5f6e9db70dfa9227c5c.png)
