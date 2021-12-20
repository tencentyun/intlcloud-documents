
## Overview

After the CLS service is commercialized, Tencent Cloud still provides a certain free tier for all users in each region as detailed below:

| Billable Item     | Daily Free Tier |
| :--------- | :---------- |
| Write traffic | 5 GB |
| Private network read traffic | 1 GB |
| Public network read traffic | 0 |
| Index traffic | 1 GB |
| Log storage - real-time storage    | 1 GB         |
| Index storage | 1 GB |
| Topic partition | 1 |
| Service request | 1 million |

>!
>- The free tier is counted for all resources of a single user in each region.
>- **The Free Tier perk will end at 23:59:59 on December 31, 2021.**
>- The daily free tier will not be accumulated into the next billing cycle.
> - If your service is suspended due to violations or overdue payment, you will not be eligible for the Free Tier perk. Free Tier will be unavailable until the service is restarted.
>- The free tier is applicable to all regions supported by CLS.
> - To learn more about the cost estimate, use the [Price Calculator](https://buy.cloud.tencent.com/price/cls/calculator) to export the cost estimate list.
## Examples

#### NGINX log query and analysis

Company A's website receives 100 million requests per day, and each request produces a 100-byte log on average. This results in 100 million logs with a total size of approximately 9.31 GB per day. Company A decides to upload the Nginx access logs to CLS in the Beijing region, and save them for 15 days for query and statistical analysis.

<table>
   <tr>
      <th colspan="2"><center>Billable Item</center></th>
      <th><center>Description</center></th>
      <th><center>Quantity</center></th>
      <th nowrap="nowrap"><center>Unit Price (Beijing)</center></th>
      <th nowrap="nowrap"><center>Cost</center></th>
   </tr>
   <tr>
      <td rowspan="4">Traffic fees</td>
      <td>Write traffic</td>
       <td>LogListener is used to compress and upload logs, resulting in 2.33 GB traffic consumption.<b>The daily free tier is 5 GB.</td>
      <td>0 GB</td>
      <td>0.032 USD/GB/day</td>
      <td>0.00 USD/day</td>
   </tr>
     <tr>
      <td>Index traffic</td>
      <td>After full-text index is enabled, 11.2 GB of index traffic is generated (as the index is expanded), <b>and a free tier of 1 GB/day is available.</b></td>
      <td>10.2 GB</td>
      <td>0.063 USD/GB/day</td>
      <td>0.64 USD/day</td>
   </tr>
   <tr>
      <td>Private network read traffic</td>
      <td>There is no download or consumption via a private network. No private network read traffic is generated.</td>
      <td>0 GB</td>
      <td>0.032 USD/GB/day</td>
      <td>0.00 USD/day</td>
   </tr>
   <tr>
      <td>Public network read traffic</td>
      <td>There is no download or consumption via a public network. No public network read traffic is generated.</td>
      <td>0 GB</td>
      <td>0.144 USD/GB/day</td>
      <td>0.00 USD/day</td>
   </tr>
   <tr>
      <td rowspan="2">Storage fees</td>
      <td>Log storage</td>
      <td>Logs of 2.33 GB are uploaded every day.<b>The daily free tier is 1 GB.</b>The average storage capacity after 15 days is 19.95 GB (1.33 GB * 15 days).</td>
      <td>19.95 GB</td>
      <td nowrap="nowrap">0.0025 USD/GB/day</td>
      <td nowrap="nowrap">0.0499 USD/day</td>
   </tr>
   <tr>
      <td>Index storage</td>
      <td>Indexes of 11.2 GB are generated every day.<b>The daily free tier is 1 GB.</b>The average storage capacity after 15 days is 153 GB (10.2 GB * 15 days).</td>
      <td>153 GB</td>
      <td>0.0025 USD/GB/day</td>
      <td nowrap="nowrap">0.382 USD/day</td>
   </tr>
   <tr>
      <td rowspan="2">Other fees</td>
      <td>Service request</td>
      <td>LogListener is used to upload logs in batches, producing 100,000 upload requests.<b>The daily free tier is 1,000,000 requests.</b></td>
      <td>0 times</td>
      <td>0.027 USD/GB/day</td>
      <td>0.00 USD/day</td>
   </tr>
   <tr>
      <td>Topic partition tenant fees</td>
      <td>The business log peak is 8 MB/s, so two topic partitions are required, <b>and a free tier of 1 partition/day is available.</b></td>
      <td>1 partition</td>
      <td>0.0072 USD/partition/day</td>
      <td>0.0072 USD/day</td>
   </tr>
   <tr>
      <td colspan="2">Total amount</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>1.0791 USD/day</td>
   </tr>
</table>





## Note on Free Log Storage for TKE Audit and Event Center

[Tencent Kubernetes Engine (TKE)](https://intl.cloud.tencent.com/document/product/457) is a high-scalability and high-performance container management service. You can easily run applications in a managed CVM instance cluster. In response to the high complexity of daily OPS of container clusters and difficulties in troubleshooting, CLS and TKE jointly launched the cluster audit and event log center. With the aid of CLS' log data processing capabilities, you can view audit logs and cluster events in real time through visual charts, which helps you improve the efficiency of container cluster OPS with ease. For TKE audit logs and event logs, CLS offers the following **Free Tier perk**:

#### Eligibility
TKE audit/event logs written by log topics automatically created by TKE are eligible for this perk. Such log topics are marked with TKE-Audit or TKE-Event. You can view them on the **Logset** > **Log Topic** list page in the **[CLS console](https://console.cloud.tencent.com/cls/logset/desc)**.


#### Rules


1. CLS provides free log storage service, so you only need to enable [cluster audit](https://intl.cloud.tencent.com/document/product/457/38338)/event log in TKE.
2. All features of CLS, such as search and analysis, visual application, and log download and consumption, are available for eligible audit/event logs free of charge.

#### Validity period

Now through 23:59:59 on December 31, 2021.
