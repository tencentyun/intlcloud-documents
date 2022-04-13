## Overview
EdgeOne provides diverse metrics for you to stay on top of the business data in multiple dimensions by analyzing the business access log data. Due to the impact of latency and algorithm, the distribution and ranking data is for reference only, and actual log analysis data shall prevail.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.

## Directions
### Query conditions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Data analysis** > **Traffic analysis** on the left sidebar.
2. On the traffic analysis page, you can select the target site to view its metrics. You can also filter data by time or click **Add filter** to filter data by conditions such as country/region, host, and device type.
![](https://qcloudimg.tencent-cloud.cn/raw/754cbfbb37e5c40739b772e16dcf7947.png)
**Parameter description:**
 - Site: You can view the data analysis results of all sites or a single site.
 - Metric: You can click **Total traffic** or **Total requests** to view metrics such as hosts, client IPs, URLs, and referers collected based on the total traffic or requests.

>!
>- Time zone adjustment will take effect for the entire data analysis feature.
>- The time between the start time and end time of a single query cannot exceed 30 days.

 - Time granularity:
    - Within 1 hour: 1 minute.
    - 1 hour–1 day: 5 minutes.
    - Within 7 days: 1 hour.
    - 7 days or above: 1 day.
  - Filters:
    - Country/Region: Country/Region of the access source. You can select multiple countries/regions.
    - Hosts: Subdomains under the site.
    - Status code: Access status code.
    - Device type: Hardware device type of the access source. Valid values include Empty, TV, Tablet, Mobile, Desktop, and Others.
    - Browser type: Type of the browser used for user access.
    - OS type: Type of the OS used for user access.
    - Network protocol: Network protocol used for user access. Valid values include http/2.0, http/1.1, https/2.0, and https/1.1.
    
### Data overview
The overview module displays the trend curve by the set filters and metrics for the specified time period.

### Country/Region
The country/region module displays the top 10 countries/regions by identifying client IPs by the set filters and metrics.

### Status code
The status code module displays the numbers and distribution of status codes returned for different client access requests.

### Data ranking
The data ranking module displays the top 5 and top 10 hosts (subdomains), client IPs, URLs, referers, resource types (coming soon), and client device types by the selected filters. You can download the complete statistics to view more details for business analysis. You can also view the specific logs to get more data.
