## Purchase Instructions
Tencent Container Registry (TCR) is now in beta and available for free. You can go to the [TCR Console](https://console.cloud.tencent.com/tcr) to create an Enterprise Edition instance for free and start using it. Using TCR will require using Tencent Cloud COS, you will be billed for COS fees according to your usage. 

TCR will exit beta and become a paid service at the end of November 2020. You will be billed hourly for your running Enterprise Edition instances according to the selected regions and specifications. We will notify you before billing via the Message Center, email, and other channels.

## Billable Items for Enterprise Edition
<table>
<tr>
<th>Item</th>
<th>Notes</th>
<th>Price</th>
</tr>
<tr>
<td>Instance leasing</td>
<td>Enterprise Edition instances are pay-as-you-go, charges differ according to selected regions and specifications.</td>
td>Please refer to <a href="#price">Enterprise Edition Pricing</a>. </td>
</tr>
<tr>
<td>Storage fees</td>
<td>The cloud-native applications of the Enterprise Edition, such as container images and Helm charts, are hosted in your COS Bucket. Storage and access fees will apply based on actual usage with the selected COS billing method. Go to the <a href="https://console.cloud.tencent.com/expense/overview">Billing Center</a> to learn more.
<td>Please refer to <a href="https://intl.cloud.tencent.com/pricing/cos">COS Pricing</a>.</td>
</tr>
<tr>
<td>Traffic fees</td>
<td>Using the public network to upload and download container images and Helm charts will generate public network traffic fees in COS. <br><b>Note: </b>using the instance synchronization feature for cross-regional synchronization of container images and Helm charts will not generate COS public network traffic fees.</td></td>
<td>Currently free for most scenarios. Please submit a ticket to query if unsure.</td>
</tr>
</table>
<span id="price"></span>

## Enterprise Edition Pricing
To ensure a smooth transit to the new billing phase for existing instances created in beta, Tencent TCR will switch all instances to the pay-as-you-go billing mode and charge by the hour at the following rate: monthly subscription fees / 30 / 24hrs. For example, a basic edition instance in Guangzhou will be billed at a price of: 97.87 / 30 / 24 = 0.14 USD/hour.
The following prices are for reference only. We will offer long-term discounts after commercialization.

<table>
<tbody>
<tr>
<th colspan="2">Region</th><th>Basic Edition (USD/month)</th><th>Standard Edition (USD/month)</th><th>Advanced Edition (USD/month)</th>
</tr>
<tr><td rowspan="2"> Chinese Mainland Regions</td><td>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu and Chongqing</td><td>97.87</td><td>200.97</td><td>388.90</td></tr>
<tr><td>Hong Kong (China), and Taipei (China)</td><td>146.94</td><td>274.36</td><td>500.72</td></tr>
<tr><td rowspan="1">Asia Pacific Regions</td><td>Singapore, Seoul, Tokyo, Mumbai, and Bangkok</td><td>146.94</td><td>274.36</td><td>500.72</td></tr>
<tr><td rowspan="1">Europe and North America Regions</td><td>Toronto, Silicon Valley, Virginia, Frankfurt and Moscow</td><td>166.56</td><td>314.61</td><td>578.57</td></tr>
</tbody></table>


>? TCR is currently unavailable in some regions. To learn more, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## TCR Specifications
The TCR specifications are as follows (**✓**: supported; **-**: not supported).

<table>
<tbody><tr>
<th rowspan="2" style="
    width: 13%;
">Feature Module</th>
<th rowspan="2" style="
    width: 27%;
">Features</th>
<th rowspan="2" style="
    width: 5%;
">Personal Edition</th>
<th colspan="3" style="
    width: 55%;
">Enterprise Edition</th>
</tr>
<tr>
<th>Basic Edition</th><th>Standard Edition</th><th>Advanced Edition</th>
</tr>
<tr>
<td rowspan="4">Instance management</td>
<td>Dedicated registry service</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Dedicated domain name access</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Dedicated data storage backend</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Temporary/long-term access credential management</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<td rowspan="5">Repository management</td>
<td>Multi-level repository directory</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Helm chart hosting</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Namespace quota</td><td>10</td><td>50</td><td>100</td><td>500 (you can apply to increase the quota)</td>
</tr>
<tr>
<td>Image repository quota</td><td>500</td><td>1000</td><td>3000</td><td>5000 (you can apply to increase the quota)</td>
</tr>
<tr>
<td>Helm repository quota</td><td>-</td><td>1000</td><td>3000</td><td>5000 (you can apply to increase the quota)</td>
</tr>

<tr>
<td rowspan="5">Image security</td>
<td>Image vulnerability scanning</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Public network access control</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>VPC access control</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>VPC access quota</td><td>-</td><td>3</td><td>5</td><td>10</td>
</tr>
<tr>
<td>Operation log retention</td><td>-</td><td>7 days</td><td>15 days</td><td>30 days</td>
</tr>

<tr>
<td rowspan="3">Synchronous backup</td>
<td>Multi-region replications for single instance and nearby access</td>
<td>-</td><td>-</td><td>-</td><td>✓</td>
</tr>
<tr>
<td>Cross-instance custom synchronization rules</td><td>-</td><td>-</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Multi-AZ disaster recovery in the same city</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td rowspan="5">Container DevOps</td>
</tr>
<tr>
<td>Webhook trigger</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Container image compilation and construction</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Cloud native delivery workflow</td><td>-</td><td>-</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>P2P accelerated distribution of images</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
</tbody></table>

#### Beta Limitations
1. Each customer can only create one instance in all regions. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply to use this service in multiple regions.
2.The VPC access quota for each specification is 1. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply to increase this quota.
3. The operation log query feature is currently unavailable. To learn more, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
4. The cloud-native delivery workflow feature is available during beta with no specification limit.
