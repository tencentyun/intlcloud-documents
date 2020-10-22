## Purchase Instructions
Tencent Container Registry (TCR) is now under beta testing and free of charge. You can go to the [TCR console](https://console.cloud.tencent.com/tcr) to use it. As Tencent Cloud COS is involved during use, relevant fees will be incurred based on your actual usage.

After the beta testing is completed, this product will start commercial billing. Before commercial billing starts, we will notify you of this through the product launch platform, Message Center, email, and other channels.


## Supported Regions
TCR is now or will be available in the following regions:
<table class="table-striped">
<tbody>
<tr>
<th>Region</th><th>Value</th>
</tr>
<tr>
<td>Guangzhou</td><td>ap-guangzhou</td>
</tr>
<tr>
<td>Shanghai</td><td>ap-shanghai</td>
</tr>
<tr>
<td>Nanjing (<a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> to apply for activation)</td><td>ap-nanjing</td>
</tr>
<tr>
<td>Beijing</td><td>ap-beijing</td>
</tr>
<tr>
<td>Hong Kong, China</td><td>ap-hongkong</td>
</tr>
<tr>
<td>Singapore (<a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> to apply for activation)</td><td>ap-singapore</td>
</tr>
<tr>    
<td>Seoul</td><td>ap-seoul</td>
</tr>
<tr>
<td>Silicon Valley</td><td>na-siliconvalley</td>
</tr>
<tr>
<td>Frankfurt (<a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> to apply for activation)</td><td>eu-frankfurt</td>
</tr>

</tbody></table>

## Billable Items for Enterprise Edition
<table>
<tr>
<th>Item</th>
<th>Notes</th>
<th>Price</th>
</tr>
<tr>
<td>Instance leasing</td>
<td>Enterprise Edition instances support the monthly subscription billing method. Prices vary with instance specifications and regions</td>
<td>Free of charge during beta testing</td>
</tr>
<tr>
<td>Storage fees</td>
<td>The cloud-native application products of Enterprise Edition (such as container images and Helm charts) are hosted in your COS bucket and incur storage and traffic fees based on your actual usage. The COS billing method is adopted, and you can go to the <a href="https://console.cloud.tencent.com/expense/overview">Billing Center</a> to query the billing information.<br><b>Note: </b>using the instance synchronization feature for cross-region synchronization of container images and Helm charts does not incur COS public-network traffic fees</td>
<td>Refer to <a href="https://intl.cloud.tencent.com/document/product/436/6239">Product Pricing</a>.</td>
</tr>
<tr>
<td>Traffic fees</td>
<td>Using the public network to perform the upload, download, and cross-region synchronization of container images and Helm charts incurs traffic fees, which vary with different specifications, free quotas, and limits. To increase the cross-region data synchronization bandwidth, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a></td>
<td>Currently, no fees are charged. For special scenarios, submit a ticket for inquiry</td>
</tr>
</table>


## TCR Specifications
TCR specifications are as follows (**✓** for supported and **-** for unsupported):

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
<td rowspan="3">Instance management</td>
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
<td rowspan="5">Repository management</td>
<td>Multi-level repository directory</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Helm chart hosting</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Namespace quota</td><td>10</td><td>50</td><td>100</td><td>500 (you can apply for an increased quota)</td>
</tr>
<tr>
<td>Image repository quota</td><td>500</td><td>1000</td><td>3000</td><td>5000 (you can apply for an increased quota)</td>
</tr>
<tr>
<td>Helm repository quota</td><td>-</td><td>1000</td><td>3000</td><td>5000 (you can apply for an increased quota)</td>
</tr>
<tr>
<td rowspan="4">Security management</td>
<td>Network access control</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>VPC access quota</td><td>-</td><td>3</td><td>5</td><td>10</td>
</tr>
<tr>
<td>Image vulnerability scanning</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Operation log retention</td><td>-</td><td>7 days</td><td>15 days</td><td>30 days</td>
</tr>
<tr>
<td rowspan="2">Synchronous backup</td>
<td>Cross-instance (cross-region) automatic synchronization</td>
<td>-</td><td>-</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Multi-availability-zone disaster recovery in the same city</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td rowspan="5">Container DevOps</td>
</tr>
<tr>
<td>Webhook trigger type</td><td>-</td><td>Push<br> images</td><td>Push images and <br>Helm charts</td><td>Push/Pull/Delete images and <br>Helm charts</td>
</tr>
<tr>
<td>Container image compilation and building</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Cloud-native delivery workflow</td><td>-</td><td>-</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>P2P accelerated distribution of images</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
</tbody></table>

#### Notes on beta testing
1. During beta testing, the VPC access quota for each specification is 1. You can submit a ticket to apply to adjust the quota based on your actual needs.
2. The operation log query feature is currently unavailable. If you need to use it, submit a ticket for application.
3. During beta testing, there is no specification limit for the Webhook trigger type, and only the push and deletion scenarios are supported.
4. During best testing, there is no specification limit for the cloud-native delivery workflow feature, which is available for trial use.
