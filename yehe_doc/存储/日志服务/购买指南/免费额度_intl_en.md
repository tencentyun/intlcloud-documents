
## Introduction

Tencent Cloud CLS offers a limited free tier to all users in each region. The detailed policy is as follows:

| Billable Item     | Daily Free Tier |
| :--------- | :---------- |
| Write traffic     | 5 GB         |
| Private network read traffic | 1 GB         |
| Public network read traffic | 0           |
| Index traffic  | 1 GB         |
| Log storage   | 1 GB         |
| Index storage   | 1 GB         |
| Topic partition   | 1 partition         |
| Service request   | 1,000,000 requests     |

>!
>- The free tier is applicable to all resources under an account in each region.
>- **The free tier is expectedly valid until 23:59:59 on December 31, 2020**.
>- The daily free tier is not accrue to the next billing cycle.
> - If your service is interrupted due to violations or arrears, you will not be eligible for the free tier. Free tier will remain unavailable until the service is restarted.
>- Free tier applies to all CLS regions.

## Example

#### Nginx logs query and analysis

Company A’s website receives 100 million requests per day, and each request produces a 100-byte log on average. This results in 100 million logs with a total size of approximately 9.31 GB per day. Company A decides to upload the Nginx access logs to CLS in the Beijing region, and save them for 15 days for query and statistical analysis.

<table>
   <tr>
      <th colspan="2"><center>Billable Item</center></th>
      <th><center>Description</center></th>
      <th><center>Quantity</center></th>
      <th nowrap="nowrap"><center>Unit Price (Beijing)</center></th>
      <th nowrap="nowrap"><center>Costs</center></th>
   </tr>
   <tr>
      <td rowspan="4">Traffic fees</td>
      <td>Write traffic</td>
       <td>LogListener is used to compress and upload logs, resulting in 2.33 GB traffic consumption<b>The daily free tier is 5 GB</td>
      <td>0 GB</td>
      <td>0.032 USD/GB/day</td>
      <td>0.00 USD/day</td>
   </tr>
     <tr>
      <td>Index traffic</td>
      <td>Full-text index is enabled, generating an index traffic of 11.2 GB (index traffic is larger than the write traffic)<b>The daily free tier is 1 GB</b></td>
      <td>10.2 GB</td>
      <td>0.063 USD/GB/day</td>
      <td>0.64 USD/day</td>
   </tr>
   <tr>
      <td>Private network read traffic</td>
      <td>There is no download or consumption via a private network. No private network read traffic is generated.</td>
      <td>0 GB</td>
      <td>0.032 USD/GB/day</td>
      <td>0.00 USD/GB/day</td>
   </tr>
   <tr>
      <td>Public network read traffic</td>
      <td>There is no download or consumption via a public network. No public network read traffic is generated.</td>
      <td>0 GB</td>
      <td>0.144 USD/GB/day</td>
      <td>0.00 USD/GB/day</td>
   </tr>
   <tr>
      <td rowspan="2">Storage fees</td>
      <td>Log storage</td>
      <td>Logs of 2.33 GB are uploaded every day<b>The daily free tier is 1 GB</b>The average storage capacity after 15 days is 19.95 GB (1.33 GB * 15 days)</td>
      <td>19.95 GB</td>
      <td nowrap="nowrap">0.0025 USD/GB/day</td>
      <td nowrap="nowrap">0.0499 USD/day</td>
   </tr>
   <tr>
      <td>Index storage</td>
      <td>Indexes of 11.2 GB are generated every day<b>The daily free tier is 1 GB</b>The average storage capacity after 15 days is 153 GB (10.2 GB * 15 days)</td>
      <td>153 GB</td>
      <td>0.0025 USD/GB/day</td>
      <td nowrap="nowrap">0.382 USD/day</td>
   </tr>
   <tr>
      <td rowspan="2">Other fees</td>
      <td>Service request</td>
      <td>Loglistener is used to upload logs in batches, producing 100,000 upload requests<b>The daily free tier is 1,000,000 requests</td>
      <td>0 request</td>
      <td>0.027 USD/GB/day</td>
      <td>0.00 USD/day</td>
   </tr>
   <tr>
      <td>Topic partition tenant fees</td>
      <td>The peak bandwidth for business logs is 8 MB/sec. Two topic partitions are needed<b>The daily free tier is 1 partition</b></td>
      <td>1 partition</td>
      <td>0.06 USD/partition/day</td>
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



















