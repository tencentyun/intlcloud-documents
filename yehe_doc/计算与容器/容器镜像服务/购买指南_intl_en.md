## Purchase Instructions
The Tencent Container Registry (TCR) Enterprise Edition is now available for commercial sale. Fees will be collected when you create new instances or use existing instances. Currently, only postpaid purchase is supported. You can go to the [TCR console](https://console.cloud.tencent.com/tcr) to create an Enterprise Edition instance and start using it. As Tencent Cloud COS is used at the same time, relevant fees will be charged based on your actual usage.

## Billable Items for Enterprise Edition
<table>
<tr>
<th>Item</th>
<th>Note</th>
<th>Price</th>
</tr>
<tr>
<td>Instance leasing</td>
<td>Enterprise Edition instances support the pay-as-you-go billing method. In this mode, users are billed based on regions and instance specifications.</td>
<td>Please refer to <a href="#price">Enterprise Edition Pricing</a>. </td>
</tr>
<tr>
<td>Storage fees</td>
<td>The cloud-native applications of the Enterprise Edition, such as container images and Helm charts, are hosted in your COS Bucket. Storage and access fees will apply based on actual usage with the selected COS billing method. Go to the <a href="https://console.cloud.tencent.com/expense/overview">Billing Center</a> to learn more.
<td>Please refer to <a href="https://intl.cloud.tencent.com/pricing/cos">COS Pricing</a>.</td>
</tr>
<tr>
<td>Traffic fees</td>
<td>Using the public network to upload and download container images and Helm charts will generate public traffic fees in COS. <br><b>Note: </b>using the instance synchronization feature for cross-regional synchronization of container images and Helm charts will not generate COS public traffic fees.</td></td>
<td>Please refer to <a href="https://intl.cloud.tencent.com/document/product/436/6239">COS Pricing</a>.</td>
</tr>
</table>

<span id="price"></span>
## Enterprise Edition Pricing
Currently, the Enterprise Edition service only supports the postpaid mode and is billed on an hourly basis. For purchase discount information, please pay attention to the latest prices on the purchase page or consult sales personnel.
<table>
<tbody>
<tr>
<th colspan="2">Region</th><th>Basic Edition (USD/hour)</th><th>Standard Edition (USD/hour)</th><th>Advanced Edition (USD/hour)</th>
</tr>
<tr><td rowspan="2"> Chinese Mainland Regions</td><td>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, and Chongqing</td><td>0.14</td><td>0.28</td><td>0.54</td></tr>
<tr><td>Hong Kong (China) and Taipei (China)</td><td>0.20</td><td>0.38</td><td>0.70</td></tr>
<tr><td rowspan="1">Asia Pacific Regions</td><td>Singapore, Seoul, Tokyo, Mumbai, and Bangkok</td><td>0.20</td><td>0.38</td><td>0.70</td></tr>
<tr><td rowspan="1">Europe and North America Regions</td><td>Toronto, Silicon Valley, Virginia, Frankfurt, and Moscow</td><td>0.28</td><td>0.50</td><td>0.87</td></tr>
</tbody></table>

Reference prices for monthly usage
>! The prices here are only for reference during conversion. The actual amount accumulated in a pay-as-you-go bill may differ. The prices here are not the actual prices of prepaid features after launch.
<table>
<tbody>
<tr>
<th colspan="2">Region</th><th>Basic Edition (USD/month)</th><th>Standard Edition (USD/month)</th><th>Advanced Edition (USD/month)</th>
</tr>
<tr><td rowspan="2"> Chinese Mainland Regions</td><td>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, and Chongqing</td><td>97.87</td><td>200.97</td><td>388.90</td></tr>
<tr><td>Hong Kong (China) and Taipei (China)</td><td>146.94</td><td>274.36</td><td>500.72</td></tr>
<tr><td rowspan="1">Asia Pacific Regions</td><td>Singapore, Seoul, Tokyo, Mumbai, and Bangkok</td><td>146.94</td><td>274.36</td><td>500.72</td></tr>
<tr><td rowspan="1">Europe and North America Regions</td><td>Toronto, Silicon Valley, Virginia, Frankfurt, and Moscow</td><td>166.56</td><td>314.61</td><td>578.57</td></tr>
</tbody></table>


>? TCR is currently unavailable in some regions. If it is needed, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

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
<td rowspan="1">Service assurance</td>
<td>SLA</td>
<td>Not supported</td><td>99.9% (compensation supported)</td><td>99.9% (compensation supported)</td><td>99.9% (compensation supported)</td>
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
<td rowspan="6">Data security</td>
<td>Encrypted storage of data</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Image vulnerability scanning</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
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

## Free Usage of the Personal Edition
The Personal Edition service is provided for individual developers. The free usage quota is limited. SLA commitments and relevant compensation are not provided.
