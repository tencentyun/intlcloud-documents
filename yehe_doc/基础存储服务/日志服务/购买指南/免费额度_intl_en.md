## Overview

After the CLS service is commercialized, Tencent Cloud still provides a certain free tier for all users in each region as detailed below:

| Billable Item     | Free Tier |
| :----------- | :---------- |
| Write traffic | 5 GB |
| Private network read traffic | 1 GB |
| Public network read traffic | 0 |
| Standard index traffic | 1 GB |
| Standard log storage | 1 GB |
| Standard index storage | 1 GB |
| Topic partition | 1 |
| Service request | 1 million |

>!
>- The free tier is counted for all resources of a single root account in each region.
>- **The Free Tier perk will end at 23:59:59 on July 31, 2022.**
>- The free tier will not be accumulated into the next billing cycle. Excessive usage will be billed normally.
> - If your service is suspended due to violations or overdue payment, you will not be eligible for the Free Tier perk. Free Tier will be unavailable until the service is resumed.
>



## Billing Examples

#### NGINX log query and analysis

Company A's website receives 100 million requests per day, and each request produces a 100-byte log on average. This results in 100 million logs per day for a total of approximately 9.31 GB. Company A decides to upload the NGINX access logs to the CLS service in the Beijing region and save them in the STANDARD storage class for 15 days. Log search, analysis, and alarming features are used, while data processing, download, consumption, and shipping features are not used.

<table>
<thead>
<tr>
<th>Billable Item</th>
<th>Description</th>
<th>Billable Usage</th>
<th>Unit Price</th>
<th>Fees</th>
</tr>
</thead>
<tbody><tr>
<td>Write traffic</td>
<td>Logs are compressed when uploaded via LogListener, resulting in 2.33 GB traffic usage, <strong>which doesn't exceed the free tier of 5 GB.</strong></td>
<td>0 GB</td>
<td>0.032 USD/GB/day</td>
<td>0 USD/day</td>
</tr>
<tr>
<td>Standard index traffic</td>
<td>After full-text index is enabled, 9.31 GB of index traffic is generated, <strong>and a free tier of 1 GB is available.</strong></td>
<td>8.31 GB</td>
<td>0.062 USD/GB/day</td>
<td>0.51522 USD/day</td>
</tr>
<tr>
<td>Standard log storage</td>
<td>Logs of 2.33 GB are uploaded every day, the average storage capacity is 34.95 GB after storage for 15 days (2.33 * 15), <strong>and a free tier of 1 GB is available.</strong></td>
<td>33.95 GB</td>
<td>0.0024 USD/GB/day</td>
<td>0.08148 USD/day</td>
</tr>
<tr>
<td>Standard index storage</td>
<td>Indexes of 9.31 GB are generated every day, the average storage capacity is 139.65 GB after storage for 15 days (9.31 * 15), <strong>and a free tier of 1 GB is available.</strong></td>
<td>138.65 GB</td>
<td>0.0024 USD/GB/day</td>
<td>0.33276 USD/day</td>
</tr>
<tr>
<td>Service request</td>
<td>LogListener uploads logs in batches, producing 100,000 upload requests, <strong>which doesn't exceed the free tier of 1 million requests.</strong></td>
<td>0</td>
<td>0.026 USD/million requests/day</td>
<td>0 USD/day</td>
</tr>
<tr>
<td>Topic partition</td>
<td>The business log peak is 8 MB/s, so two topic partitions are required, <strong>and a free tier of one partition is available.</strong></td>
<td>1 partition</td>
<td>0.007 USD/partition/day</td>
<td>0.007 USD/day</td>
</tr>
<tr>
<td>Total</td>
<td colspan=4>0.93646 USD/day</td>
</tr>
</tbody></table>


## Note on Free Log Storage for TKE Audit and Event Center

[Tencent Kubernetes Engine (TKE)](https://intl.cloud.tencent.com/document/product/457) is a high-scalability and high-performance container management service. You can easily run applications in a managed CVM instance cluster. In response to the high complexity of daily Ops of container clusters and difficulties in troubleshooting, CLS and TKE jointly launched the cluster audit and event log center. With the aid of CLS' log data processing capabilities, you can view audit logs and cluster events in real time through visual charts, which helps you improve the efficiency of container cluster Ops with ease. For TKE audit logs and event logs, CLS offers the following **Free Tier perk**:

#### Eligibility

TKE audit/event logs written by log topics automatically created by TKE are eligible for this perk. Such log topics are marked with TKE-Audit or TKE-Event. You can view them on the **[Log Topic](https://console.cloud.tencent.com/cls/topic)** page.


#### Rules

1. CLS provides free log storage service, so you only need to enable [cluster audit](https://intl.cloud.tencent.com/document/product/457/38338)/event log in TKE.
2. All features of CLS, such as search and analysis, visual application, and log download and consumption, are available for eligible audit/event logs free of charge.

#### Validity period

Now through 23:59:59 on July 31, 2022.

