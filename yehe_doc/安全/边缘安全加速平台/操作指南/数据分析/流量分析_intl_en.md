## Overview
EdgeOne provides diverse metrics for you to stay on top of the business data in multiple dimensions by analyzing the business access log data. Due to the impact of latency and algorithm, the distribution and ranking data is for reference only, and actual log analysis data shall prevail.

## Directions
### Query conditions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Data Analysis** > **Traffic analysis** on the left sidebar.
2. On the **Traffic analysis** page, select the target site. You can also filter data by time or click **Add filter** to filter data by conditions such as country/region, host, and device type.
![](https://qcloudimg.tencent-cloud.cn/raw/fde073a08ae22992bb3253d0410cb274.png)

**Parameter description:**
 - Site: View the data of all sites or a single site.
 - Metric: You can click **Total traffic** or **Total requests** to view metrics such as hosts, client IPs, URLs, and referers collected based on the total traffic or requests. To view peak bandwidth over time and by region (country/region), you can click **Peak bandwidth**.

>!
>- Bandwidth-related metrics only support "Host", "Country/Region", and "HTTP".
>- Time zone adjustment will take effect for the entire **data analysis** feature.
>- The period between the query start time and end time cannot exceed 30 days.

 - Time granularity:
    - Within 1 hour: 1 minute.
    - 1 hour - 1 day: 5 minutes.
    - Within 7 days: 1 hour.
    - 7 days and above: 1 day.
  - Filters:
    - **Country/Region**: Country/Region of the access source. You can select multiple countries/regions.
    - **Host**: Subdomains under the site.
    - **Status code**: Access status code.
    - **Device type**: Hardware device type of the access source. Valid values include Empty, TV, Tablet, Mobile, Desktop, and Others.
    - **Browser type**: Browser of the requester
    - **System type**: OS of the requester
    - **Network protocol**: Network protocol of the request. Valid values include **http/2.0**, **http/1.1**, **https/2.0**, and **https/1.1**.
    - **TLS version**: Version of TLS. Supported versions: TLS1.0, TLS1.1, TLS1.2, and TLS1.3.
    - **URL**: URL to access, such as "/content".
    - **Referer**: Referer information, such as "example.com".
    - **Resource type**: Type of resources, such as PNG and JSON.
    
### Data Overview
The **Overview** section shows the data trend by the set filters and metrics for the specified time period.

### Distribution of Country/Region
The Country/Region module displays the top 10 countries/regions by identifying client IPs by the set filters and metrics.

### Status Codes
The Status Code module displays the numbers and distribution of status codes returned for different client access requests.

### Rankings
The data ranking module displays the top 5 and top 10 hosts (subdomains), client IPs, URLs, Referers, resource types, and client device types by the selected filters. You can download the complete statistics to view more details for business analysis. You can also view the specific logs to get more data.
