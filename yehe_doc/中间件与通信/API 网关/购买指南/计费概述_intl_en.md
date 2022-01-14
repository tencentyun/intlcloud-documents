## Instance Types

An instance is a resource in API Gateway that can provide public IP, private IP, public network egress, computing, and storage resources required to process an API. A service must be mounted under an instance before it can run normally.

API Gateway provides two instance types: shared instance and dedicated instance. For their differences and how to select an appropriate type, see [Instance Selection](https://intl.cloud.tencent.com/document/product/628/40305).

## Billing

<table>
<thead>
<tr>
<th>Instance Type</th>
<th>Billable Item</th>
<th>Billing Mode</th>
<th>Billing Sequence</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="2">Shared instance</td>
<td>Number of calls</td>
<td rowspan="2">Pay-as-You-Go: default billing mode of API Gateway, where fees are charged by the actual usage and settled hourly. Resource pack: discounted package offered by API Gateway, which can be used to deduct billable items (API calls/public network outbound traffic).</td>
<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/628/38406">Free tier</a> &gt; <a href="https://intl.cloud.tencent.com/document/product/628/38407">resource pack</a> &gt; <a href="https://intl.cloud.tencent.com/document/product/628/11771">pay-as-you-go</a></td>
</tr>
<tr>
<td>Public network outbound traffic</td>
</tr>
<tr>
<td rowspan="3">Dedicated instance</td>
<td>Instance</td>
<td>Monthly Subscription/Pay-as-You-Go</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/44234">Monthly Subscription/Pay-as-You-Go</a></td>
</tr>
<tr>
<td rowspan="2">Public network outbound traffic</td>
<td>Pay-as-You-go: billed by usage and settled hourly.</td>
<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/628/38406">Free tier</a> &gt;  <a href="https://intl.cloud.tencent.com/document/product/628/38407">resource pack</a> &gt; <a href="https://intl.cloud.tencent.com/document/product/628/11771">pay-as-you-go</a></td>
</tr>
<tr>
<td>Resource pack: discounted package offered by API Gateway, which can be used to deduct billable items (public network outbound traffic)</td>
</tr>
</tbody></table>



## Free Tier

> ?The free tier policy of the API Gateway service was adjusted at 23:59:59 on October 12, 2020. After the adjustment, each account can use 1 million API calls and 1 GB public network outbound traffic free of charge every month for 12 months. There is no need to claim the free tiers, which are granted directly in the form of resource packs. Such free tiers are also fully available to existing API Gateway users.

Users who newly activate the API Gateway service can enjoy certain free tier of API calls and public network outbound traffic for one year.

| Item      | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Free tier | <li>Number of calls: the first 1 million calls per month (non-calendar month) are free of charge. </li><li>Public network outbound traffic: the first 1 GB of traffic per month (non-calendar month) is free of charge.</li> |
| Effective scope | The free tier is implemented in the form of resource pack to deduct account-level usage. |
| Validity period | After the API Gateway service is activated, the free tier will be valid for 12 non-calendar months in the first year (including the month of activation) and reset once every non-calendar month. |
| Acquisition method | After API Gateway is activated, the system will grant the free tier in the form of resource pack. [Activate>>](https://console.cloud.tencent.com/apigateway/index) |

For example, if you activate API Gateway at 17:13:14, November 10, 2019, then the one million free calls will be valid from November on. Unused calls in the free tier will not be accumulated for the next non-calendar month; therefore, the monthly free tier will be reset at 00:00:00, December 10, 2019. The free tier will become unavailable after 23:59:59, November 10, 2020.

#### Viewing usage

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. On the left sidebar, click **Resource Pack** to access the resource pack list page.
3. View the usage of resource packs whose source is free tier. 
![](https://main.qcloudimg.com/raw/ca9c5222e609a8bf1418a36eef66499c.png)
