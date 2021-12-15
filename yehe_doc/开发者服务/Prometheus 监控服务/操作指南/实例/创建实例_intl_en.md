This document uses custom configuration as an example to describe how to create a TMP instance.

## Preparations

Before creating a TMP instance, you must complete the following operations:

- Sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
- [Create a VPC](https://intl.cloud.tencent.com/document/product/215/31805) in the target region and [create a subnet](https://intl.cloud.tencent.com/document/product/215/31806) in the target AZ in the VPC.

## Directions

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus).
2. Click **Create** and configure the following information as prompted:
<table>
<tr>
<th>Type</th>
<th>Required</th>
<th>Configuration Description</th>
</tr>
<tr>
<td>Region</td>
<td>Yes</td>
<td>Select a region based on the region of your Tencent Cloud service. The price may vary by region, and the real-time price displayed on the purchase page shall prevail. Tencent Cloud services in different regions cannot communicate with each other over the private network; for example, a service in the Guangzhou region cannot report data to a TMP instance in the Shanghai region over the private network. Once an instance is purchased, the region cannot be changed. Therefore, please select the region with caution.</td>
</tr>
<tr>
<td>AZ</td>
<td>Yes</td>
<td>Select as needed.</td>
</tr>
<tr>
<td>Network</td>
<td>Yes</td>
<td>It indicates a logically isolated network space in Tencent Cloud. A VPC consists of at least one subnet. The system will provide a default VPC and subnet for you in each region. If the existing VPCs/subnets don't meet your requirements, you can create new ones as instructed in <a href = "https://intl.cloud.tencent.com/document/product/215/31805">Creating VPCs</a> or <a href = "https://intl.cloud.tencent.com/document/product/215/31806">Creating Subnets</a>.</td>
</tr>
<tr>
<td>Product Specs</td>
<td>Yes</td>
<td>The price varies by product specs. For more information, please see <a href = "https://cloud.tencent.com/document/product/1416/55777">Pricing</a>.</td>
</tr>
<tr>
<td>Data Retention Period</td>
<td>Yes</td>
<td>The price varies by data retention period. For more information, please see <a href = "https://cloud.tencent.com/document/product/1416/55777">Pricing</a>.</td>
</tr>
<tr>
<td>Instance Name</td>
<td>Yes</td>
<td>Enter a custom name of the TMP instance.</td>
</tr>
<tr>
<td>Grafana/Grafana Password</td>
<td>Yes</td>
<td>Grafana is enabled by default. After the instance is successfully created, the system will generate a domain name accessible over the public network. The default account of the Grafana service is `admin`, and the password is user-defined.</td>
</tr>
<tr>
<td>Validity Period</td>
<td>Yes</td>
<td>Multiple validity periods are available for your choice.</td>
</tr>
</table>
3. After completing the configuration, click **Buy Now**.
![](https://qcloudimg.tencent-cloud.cn/raw/bbf0951c01a56460cf20fb18837bdc17.png)
