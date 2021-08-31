You can check your end-user distribution and resource usage in the **Data Analysis** page. However, ECDN does not support displaying the number of unique IP access requests and end-user access region distribution currently.


Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and select **Statistics** > **Data Analysis** on the left sidebar to enter the **Data Analysis** page.

- You can query data generated within a maximum time period of 31 days. Historical data is retained for 90 days.
- You can query historical data generated in the last three months.

>! ECDN does not support displaying the number of unique IP access requests and end-user access region distribution currently.


## Unique IP Access Requests
The number of unique IP access requests in the specified time period is calculated by deduplicating access client IPs in the log:
<li>If the time range is less than or equal to one day, a deduplicated IP curve with a 5-minute granularity will be provided.</li>
<li>Domain name statistics are counted by deduplicating the active quantity in a full day. If there are multiple domain names, projects or accounts, the statistics are counted by accumulating the daily active quantity of each one with a 5-minute granularity.</li>
<img src="https://main.qcloudimg.com/raw/bed86e21420fe337d6b0587090fe4b64.png" alt>


## User Access District Distribution
The district of the access requester can be identified via the source client IP, which can be displayed in a map or list, allowing you to view the district distribution of your users.
![](https://main.qcloudimg.com/raw/d89e4321c94499833d04841c7e5e3597.png)

## User ISP Distribution
The ISP of the access requester can be identified via the source client IP, which can be displayed in a pie chart or list, allowing you to view the ISP distribution of your users.
![](https://main.qcloudimg.com/raw/b6fa25e2fb72dbcd02e11fae43e888ed.png)
