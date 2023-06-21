
## Billing overview
Paid editions of Tencent Cloud Firewall include Premium Edition, Enterprise Edition, and Ultimate Edition. To meet the needs of different customers with different asset scales, the editions differ in their feature modules and default specifications. The Premium Edition, Enterprise Edition, and Ultimate Edition support elastic scaling based on performance specifications and asset scale. The billing details are listed below:

>! 
>- Please note that you cannot downgrade your Cloud Firewall subscription after purchase.
>- Enterprise security groups are available on all current editions, but will be unavailable for some editions in the future. Tencent Cloud will notify you of any changes to the feature in advance. The changes will have no impact on your usage during the subscription period.

<table>
<tr>
<th width="10%">Billing</th>
<th width="10%">Premium Edition </th>
<th width="10%">Enterprise Edition </th>
<th width="10%">Ultimate Edition</th>
<th width="10%">Elastic scaling</br></th></tr>
<tr>
<td> Billing mode </td>
<td> Monthly subscription</td>
<td> Monthly subscription</td>
<td> Monthly subscription</td>
<td> Not supported</td>
</tr>
<tr>
<td> Basic price </td>
<td>420 USD/month </td><td>1,450 USD/month</td><td>3,900 USD/month</td><td>Not supported</td>
</tr>
<tr><td>Available subscription period</td>
<td>6 months, 1 year, 2 years, 3 years, 5 years	</td>
<td colspan="2">1 month, 3 months, 6 months, 1 year, 2 years, 3 years, 5 years</td><td>Not supported</td><tr>
<tr>
<td>Discount</td>
</td><td colspan="3"><li>6-month subscription or less: No discount<li>1-year subscription: 15% off<li>2-year subscription: 30% off<li>3-year subscription or more: 50% off</td><td>Not supported</td></tr>
<tr>
<td>Edge firewall bandwidth</td>
<td>Default value: 20 Mbps; Maximum value: 200 Mbps</td><td>Default value: 100 Mbps; Maximum value: 1 Gbps</td><td>Default value: 300 Mbps; Maximum value: 30 Gbps</td><td>Extra bandwidth fee: 16 USD/Mbps/month.</td></tr>
<tr>
<td>Internet access control</td>
<td>1,000 L4/L7 outbound rules and 1,000 L4/L7 inbound rules	</td><td>2,000 L4/L7 outbound rules and 2,000 L4/L7 inbound rules</td><td>5,000 L4/L7 outbound rules and 5,000 L4/L7 inbound rules</td><td>Not supported</td></tr>
<tr>
<td>Region blocking for Internet access control</td>
<td>Not supported</td>
<td>Supported</td>
<td>Supported</td><td>Not supported</td></tr>
<tr>
<td>Number of public IP addresses for edge firewall	</td>
<td>10</td><td>	50</td><td>200	</td><td>1 public IP address for 1 Mbps of bandwidth</td></tr>
<tr>
<td>Number of regions for edge firewall	</td>
<td>1</td>
<td>3</td>
<td>5</td><td>Not supported</td></tr>
<tr>
<tr>
<td>NAT firewall throughput	</td>
<td>Match edge firewall bandwidth</td>
<td>Match edge firewall bandwidth</td>
<td>Match edge firewall bandwidth</td>
<td>Match edge firewall bandwidth</td></tr>
<tr>
<tr>
<td>Number of NAT firewall instances	</td><td>1</td><td>3</td><td>	5</td><td>Not supported</td></tr>
<tr>
<td>Inter-VPC firewall</td><td>Not supported</td><td>	Inter-VPC firewall features can be purchased for a bandwidth of 1 to 2 Gbps</td><td>	Inter-VPC firewall features can be purchased for a bandwidth of 1 to 20 Gbps</td><td>749 USD/month for 1 Gbps bandwidth</td></tr>
<tr>
<td>Honeypot</td><td>1; scalable</td><td>	3; scalable</td><td>	5; scalable</td><td>99 USD/month for each honeypot</td></tr>
<tr>
<td>Log analysis (analysis and 6-month storage): up to 50 GB of logs are stored for 7 days by default</td>
<td>Minimum purchase amount: 1,000 GB; Maximum value: 100,000 GB</td><td>	Minimum purchase amount: 1,000 GB; Maximum value: 100,000 GB	</td><td>Minimum purchase amount: 1,000 GB; Maximum value: 100,000 GB</td><td>Elastic scaling: 0.13 USD/GB/month; the storage period is identical to the subscription period</td></tr>
<tr>
<td>Traffic visualization</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Not supported</td></tr>
<tr>
<td>Intrusion prevention system (IPS)<br>(intelligent intrusion prevention)</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Not supported</td></tr>
<tr>
<tr>
<td>Blocklist</td><td>4,000 entries</td><td>10,000 entries</td><td>20,000 entries</td><td>Not supported</td></tr>
<tr>
<td>Threat intelligence integration<br>(automatic blocking of malicious outgoing requests) </td><td>Supported</td><td>Supported</td><td>Supported</td><td>Not supported</td></tr>
<tr>
<tr>
<td>Enterprise security group</td><td>Supported for a limited time</td><td>Supported</td><td>Supported</td><td>Not supported</td></tr>
<tr>
<td>Security baseline</td><td>Not supported</td><td>Not supported</td><td>Supported</td><td>Not supported</td></tr>
</table>


## Purchase method
1. Go to the [Cloud Firewall purchase page](https://buy.cloud.tencent.com/cfw) and select a package according to your demands. You can also customize your billable items, and your fees are automatically calculated.
2. After selection, click "Place Order" and complete the payment.
>? Cloud Firewall offers a trial edition to verified enterprise users. You can apply for a free trial on the [Product Overview page](https://intl.cloud.tencent.com/product/cfw). A verified individual user can [upgrade to a verified enterprise user](https://intl.cloud.tencent.com/document/product/378/37276) to try Cloud Firewall.

## Resource deletion upon expiration
- You cannot go to the console after your subscription expires.
- All your protection will be disabled 7 days after your subscription expires. Traffic protection will be disabled, but your configurations will be retained and you can renew your subscription to restore your configurations.
- All your Cloud Firewall resources will be deleted 14 days after your subscription expires. Your configurations will be deleted and cannot be recovered. In this case, you have to re-purchase and configure again.


## Next steps
After you purchase Cloud Firewall, you can use it in the following ways:
- Method 1: Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw) to perform operations.
- Method 2: Use CFW with APIs. For more information, please see [API Documentation](https://www.tencentcloud.com/document/product/1160/51320).
