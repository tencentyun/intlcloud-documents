## Instance type

An instance is a resource in API Gateway that can provide public IP, private IP, public network egress, computing, and storage resources required to process an API. A service must be mounted under an instance before it can run normally.

API Gateway provides shared instances and dedicated instances. For more details about their differences, see [Instance Specifications](https://intl.cloud.tencent.com/document/product/628/40305).

## Billing description

<table>
<thead>
<tr>
<th>Instance type</th>
<th>Billable item</th>
<th>Billing method</th>
<th>Billing sequence</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=2 >Shared instance</td>
<td>Number of calls</td>
<td rowspan="2">Pay as you go: The default billing mode. It is to bill per the actual usage and settle on an hourly basis. <br>
Resource pack: Discounted package offered by API Gateway, which can be used to pay for billable items (API calls/public network outbound traffic) </td>
<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/628/38406">Free tier</a> &gt; <a href="https://intl.cloud.tencent.com/document/product/628/38407">Resource pack</a> &gt; <a href="https://intl.cloud.tencent.com/document/product/628/11771">Pay as you go</a></td>
</tr>
<tr>
<td>Public outbound traffic</td>
</tr>
<tr>
<td rowspan="3">Dedicated instance</td>
<td>Instance fee</td>
<td>Monthly Subscription/Pay-as-You-Go</td>
<td><a href="https://intl.cloud.tencent.com/document/product/628/44234">Monthly subscription/Pay as you go</a></td>
</tr>
<tr>
<td rowspan="2">Public outbound traffic</td>
<td>Pay-as-You-go: billed by usage and settled hourly. </td>
<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/628/38406">Free tier</a> &gt;  <a href="https://intl.cloud.tencent.com/document/product/628/38407">Resource pack</a> &gt; <a href="https://intl.cloud.tencent.com/document/product/628/11771">Pay as you go</a></td>
</tr>
<tr>
<td>Resource pack: Discounted package offered by API Gateway, which can be used to pay ‍for billable items (public network outbound traffic)</td>
</tr>
</tbody></table>



## Free Tier

> ?The free tier policy of the API Gateway service was adjusted at 23:59:59 on October 12, 2020. After the adjustment, each account can use 1 million API calls and 1 GB public network outbound traffic free of charge every month for 12 months. There is no need to claim the free tiers, which are granted directly in the form of resource packs. Such free tiers are also fully available to existing API Gateway users.

Users who newly activate the API Gateway service can enjoy certain free tier of API calls and public network outbound traffic for one year.

| Item      | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Free tier |<li>API calls: First million calls of every month (non-calendar month) </li><li>Public outbound traffic: First GB of every month (non-calendar month) </li>|
| Effective scope | The free tier is granted in the form of resource packs under the current account.|           |
| Validity period | After the API Gateway service is activated, the free tier will be valid for 12 non-calendar months in the first year (including the month of activation) and reset once every non-calendar month.  |
| Acquisition method | After API Gateway is activated, the system will grant the free tier in the form of resource pack. [Activate>>](https://console.cloud.tencent.com/apigateway/index) |

For example, if you activate API Gateway at 17:13:14, November 10, 2019, then the one million free calls will be valid from November on. Unused calls in the free tier will not be accumulated for the next non-calendar month; therefore, the monthly free tier will be reset at 00:00:00, December 10, 2019. The free tier will become unavailable after 23:59:59, November 10, 2020.

#### Checking usage

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. On the left sidebar, click **Resource Pack** to access the resource pack list page.
3. Check the resource packs with the source as "Free tier", and the resource used and total quota are displayed under Specifications. 
 ![](https://main.qcloudimg.com/raw/ca9c5222e609a8bf1418a36eef66499c.png)
