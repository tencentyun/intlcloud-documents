## Overview
The multi-dimensional cache analysis provides a detailed image of access traffic or client requests responded by the cache on EdgeOne nodes. This helps determine your optimal configuration that can reduce the load on the origin server and response time.
>?The EdgeOne console is now only available to beta users. [Contact us](https://intl.cloud.tencent.com/contact-us) to join the beta.

## Directions
#### Query conditions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Data Analysis** > **Cache Analysis** on the left sidebar.
2. On the page that appears, select the target site and query filters.
 - Responded by EdgeOne: The client requests are directly responded by the cache on EdgeOne nodes.
![](https://qcloudimg.tencent-cloud.cn/raw/3ac1a33606794ddb25455660c2566c22.png)
 - Responded by origin: The client requests are responded by the origin server.
 ![](https://qcloudimg.tencent-cloud.cn/raw/a921b6006f6c5e8cfd2c8b7b164176a8.png)
 - You can switch between views of traffic and requests or view both while keeping filters (such as Hosts and URLs) enabled.
>?
>- Select **Responded by EdgeOne**/ **Responded by origin** to view the data you want to focus on, or select both to view two types of data.
>- Only traffic generated when EdgeOne serves client requests is recorded.

 ![](https://qcloudimg.tencent-cloud.cn/raw/bf1cc47e42c4d68916a5f6963ce61907.png)

 - You can view data for a specific time period.
>!
>- Time zone adjustment will take effect for the entire **data analysis** feature.
>- The time between the start time and end time of a single query cannot exceed 30 days.

![](https://qcloudimg.tencent-cloud.cn/raw/8ed740205ee13f06fed49ccb945fa120.png)

  - Time granularity:
     - Last 1 hour: Display data at 1-minute intervals.
     - Last 6 hours/Today/Yesterday: Display data at 5-minute intervals.
     - Last 7 days: Display data at 1-hour intervals.
     - Last 30 days: Display data at 1-day intervals.

 - Filter condition: Click **Add filter** to add the following filters: Host, URL, resource type and cache status.


 Field description:
- Host: Subdomain name under the site.
- URL: URL to request resources, such as "/content".
- Resource type: Type of resources to request, such as PNG.
- Cache status: Cache status of a request.
  - Hit: A request hit the cache on EdgeOne nodes, indicating that the requested resources are provided by EdgeOne nodes.
  - Miss: A request missed the cache on EdgeOne nodes, indicating that the requested resources are provided by the origin server.
  - Dynamic: A request for resources not eligible or not configured for node caching, indicating that the requested resources are provided by the origin server.


#### Statistics overview
The trend curve for the specified time period is displayed by the set filters and metrics.
![](https://qcloudimg.tencent-cloud.cn/raw/5829813324b108e80860fb9ef488c6cd.png)

#### Cache distribution
Types of requested resources and traffic usage are displayed based on the cache status of the requests for a specified time period.
![](https://qcloudimg.tencent-cloud.cn/raw/03de782e6967037d0684fe8311b810e3.png)

#### Data ranking

The top 5 and top 10 hosts (subdomain names), client IPs, URLs, Referers, resource types (available soon), and client device types are displayed by the selected filters. You can download the complete statistics to view more details for business analysis. You can also view the specific logs to get more data.
![](https://qcloudimg.tencent-cloud.cn/raw/5145e71da8f1550eaa4094ce41e24662.png)
**Field description:**

 - Resource types: File extensions of the requested resources.
 - Hosts: Subdomain names under the site.
 - URLs: Resource URLs that the client accesses.

