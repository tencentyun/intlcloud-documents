## Purchase Instructions
Tencent Container Registry (TCR) is now in the beta test stage and free of charge. You can go to the [TCR Console](https://console.cloud.tencent.com/tcr) to create an Enterprise Edition Instance for free and start using it. As Tencent Cloud COS is used at the same time, relevant fees will be generated based on your actual usage.

TCR will exit beta at the end of November, and will officially launch as a paid service. At that time, the running Enterprise Edition instances will be charged by hour based on different regions and specifications. Before commercial billing starts, we will notify you of this through the product launch platform, Message Center, email, and other channels.

## Billable Items for Enterprise Edition
<table>
<tr>
<th>Item</th>
<th>Notes</th>
<th>Price</th>
</tr>
<tr>
<td>Instance leasing</td>
<td>Enterprise Edition instances support the pay-as-you-go billing method, which is billed based on regions and instance specifications.</td>
<td>Please refer to <a href="#price">Enterprise Edition Pricing</a>. </td>
</tr>
<tr>
<td>Storage fees</td>
<td>The cloud-native application products of the Enterprise Edition (such as container images and Helm charts) are hosted in your COS Bucket and generate storage and access fees based on actual usage. The COS billing method is adopted. You can go to the <a href="https://console.cloud.tencent.com/expense/overview">Billing Center</a> to query billing information.
<td>Please refer to <a href="https://intl.cloud.tencent.com/pricing/cos">COS Pricing</a>.</td>
</tr>
<tr>
<td>Traffic fees</td>
<td>Using the public network to perform upload and download of container images and Helm charts will generate public network traffic fees in COS. <br><b>Note: </b>using the instance synchronization feature for cross-regional synchronization of container images and Helm charts will not generate COS public network traffic fees.</td></td>
<td>Currently, no fee is charged. For special scenarios, please submit a ticket for inquiry.</td>
</tr>
</table>
<span id="price"></span>

## Enterprise Edition Pricing
To ensure that the instances created by current beta testing customers smoothly transit to a payment status, the existing instances will automatically switch to the pay-as-you-go billing mode and be charged by hour after commercial billing starts. The specific price is “monthly subscription price / 30 / 24h”, such as a basic edition instance in Guangzhou will be deducted 97.87 / 30 / 24 = 0.14 USD/hour.
The following prices are for reference only. After billing officially starts, there will be some long-term discount activities.

<table>
<tbody>
<tr>
<th colspan="2">Region</th><th>Basic Edition (USD/month)</th><th>Standard Edition (USD/month)</th><th>Advanced Edition (USD/month)</th>
</tr>
<tr><td rowspan="2">Regions in Mainland China</td><td>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu and Chongqing</td><td>97.87</td><td>200.97</td><td>388.90</td></tr>
<tr><td>Hong Kong (China), and Taipei (China)</td><td>146.94</td><td>274.36</td><td>500.72</td></tr>
<tr><td rowspan="1">Asia Pacific Regions</td><td>Singapore, Seoul, Tokyo, Mumbai, and Bangkok</td><td>146.94</td><td>274.36</td><td>500.72</td></tr>
<tr><td rowspan="1">Europe and the North America Regions</td><td>Toronto, Silicon Valley, Virginia, Frankfurt and Moscow</td><td>166.56</td><td>314.61</td><td>578.57</td></tr>
</tbody></table>


>? TCR service is temporarily unavailable in some regions. If needed, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for it.

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
<td>Dedicated service access domain name</td>
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
<td>Namespace quota</td><td>10</td><td>50</td><td>100</td><td>500 (you can apply for increases of the quota)</td>
</tr>
<tr>
<td>Image repository quota</td><td>500</td><td>1000</td><td>3000</td><td>5000 (you can apply for increases of the quota)</td>
</tr>
<tr>
<td>Helm repository quota</td><td>-</td><td>1000</td><td>3000</td><td>5000 (you can apply for increases of the quota)</td>
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
<td>Multiple regions replications for single instance and nearby access</td>
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
<td>Container image compilation and building</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Cloud native delivery workflow</td><td>-</td><td>-</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>P2P accelerated distribution of images</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
</tbody></table>

#### Notes on the beta test
1. During beta testing, a single customer can only create one instance in all regions. You can [Submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply to use this service in multiple regions.
2. During beta testing, the VPC access quota for each specification is 1. You can [Submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply to adjust the quota based on your actual needs.
3. The operation log query feature is currently unavailable. If you need to use it, you can [Submit a ticket](https://console.cloud.tencent.com/workorder/category).
4. There is no specification limit for the cloud-native delivery workflow feature during the beta test. It is available for trial use.
