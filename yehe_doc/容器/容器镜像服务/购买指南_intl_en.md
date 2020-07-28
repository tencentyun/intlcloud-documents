## Purchase Instructions
Tencent Container Registry (TCR) is currently in beta and free of charge. To apply for trial use, go to the [TCR console](https://console.cloud.tencent.com/tcr). During TCR usage, Cloud Object Storage (COS) is involved and will be charged based on your actual usage.

After the beta test is completed, TCR will be charged for. We will notify you of TCR commercial use through channels such as the product release platform, message center, and email.


## Supported Regions
The following table describes the regions that TCR has supported and will support in the near future.
<table>
<tbody>
<tr>
<th width="33%">Region</th><th width="33%">Abbreviation</th><th width="33%">Description</th>
</tr>
<tr>
<td>Guangzhou</td><td>ap-guangzhou</td><td>-</td>
</tr>
<tr>
<td>Qingyuan</td><td>ap-qingyuan</td><td>Supported in July 2020</td>
</tr>

<tr>
<td>Shanghai</td><td>ap-shanghai</td><td>-</td>
</tr>

<tr>
<td>Nanjing</td><td>ap-nanjing</td><td>Supported in July 2020</td>
</tr>

<tr>
<td>Beijing</td><td>ap-beijing</td><td>-</td>
</tr>

<tr>
<td>Hong Kong</td><td>ap-hongkong</td><td>Submit a <a href="https://console.cloud.tencent.com/workorder/category">ticket</a> for application.</td>
</tr>

<tr>
<td>Seoul</td><td>ap-seoul</td><td>Supported in July 2020</td>
</tr>

<tr>
<td>Silicon Valley</td><td>na-siliconvalley</td><td>-</td>
</tr>

</tbody></table>

## Charging Items of the TCR Enterprise Edition
<table>
<tr>
<th>Item</th>
<th>Description</th>
<th>Price</th>
</tr>
<tr>
<td>Instance leasing</td>
<td>The prices of TCR instances of the enterprise edition vary depending on the instance specifications and region.</td>
<td>In the beta test period, instance leasing is free of charge.</td>
</tr>
<tr>
<td>Storage</td>
<td>Cloud-native applications of the TCR enterprise edition, such as container images and Helm charts, are hosted in your COS bucket, which will generate storage and traffic fees based on actual usage. The storage and traffic fees are charged in COS billing mode. To view the fees, go to the <a href="https://console.cloud.tencent.com/expense/overview">billing center</a>. <br><b>Note: </b>Cross-region synchronization of container images or Helm charts will not generate COS public traffic fees.</td>
<td>For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/6239">Product Pricing</a>.</td>
</tr>
<tr>
<td>Traffic</td>
<td>If you upload, download, or synchronize container images and Helm charts cross regions through a public network, traffic fees will be generated. The free traffic quota and traffic limit vary depending on specifications. To improve the cross-region data synchronization bandwidth, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</td>
<td>Traffic is not charged for currently. In special scenarios, submit a ticket for consulting.</td>
</tr>
</table>


## TCR Specifications
The following table describes the TCR specifications. **✓** indicates supported, and **-** indicates not supported.

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
<td>Dedicated service access domain</td>
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
<td>Namespace quota</td><td>10</td><td>50</td><td>100</td><td>500</td>
</tr>
<tr>
<td>Image repository quota</td><td>500</td><td>1000</td><td>3000</td><td>5000</td>
</tr>
<tr>
<td>Helm chart repository quota</td><td>-</td><td>1000</td><td>3000</td><td>5000</td>
</tr>
<tr>
<td rowspan="4">Security control</td>
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
<td>Operation logs retention</td><td>-</td><td>7 days</td><td>15 days</td><td>30 days</td>
</tr>
<tr>
<td rowspan="2">Synchronization and backup</td>
<td>Cross-instance (region) automatic synchronization</td>
<td>-</td><td>-</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Same-region multi-availability zone disaster recovery</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td rowspan="5">Container DevOps</td>
</tr>
<tr>
<td>Webhook trigger type</td><td>-</td><td>Pushing <br>images</td><td>Pushing images and <br>Helm charts</td><td>Pushing, pulling, and deleting images and <br>Helm charts</td>
</tr>
<tr>
<td>Container image compilation and building</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Cloud-native delivery workflow</td><td>-</td><td>-</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>P2P accelerated image distribution</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
</tbody></table>

#### Beta precautions
- The VPC access quota is 1 for all specifications in the beta test period. Submit a ticket to adjust the quota based on your actual requirements.
- The operations log query feature is unavailable. To use it, submit a ticket.
- Webhook triggers apply to all specifications in the beta test period and only support push and deletion.
- The cloud-native delivery workflow feature apply to all specifications in the beta test period. You can submit a ticket to apply for it.
