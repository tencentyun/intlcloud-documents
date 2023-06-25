## Prerequisite
You need to [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) before purchasing an Anti-DDoS Pro instance.

## Purchasing Anti-DDoS Pro (Standard)
1. Log in to the [Anti-DDoS Pro purchase page](https://buy.cloud.tencent.com/antiddos#/native), and select **Standard**.
![](https://qcloudimg.tencent-cloud.cn/raw/56e15cacb7613eec0e9f0db556ec279b.png)
2. Configure the following parameters as needed.
<table>
<thead>
<tr>
<th width="15%">Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Select line</td>
<td>It provides BGP lines and non-BGP lines (CTCC, CUCC, CMCC).</td>
</tr>
<tr>
<td>Specification description</td>
<td><ul><li>Access mode: Pass-through</li><li>Bandwidth type: Tencent Cloud multi-BGP line network</li><li>Protection capability: All-out protection</li><li>Protected targets: Public IPs of Tencent Cloud resources such as CVM, CLB, GAAP and WAF</li></ul></td>
</tr>
<tr>
<td>Region</td>
<td>Please select the region of the public IP. Currently, an Anti-DDoS Pro instance can only provide DDoS protection for public IPs of Tencent Cloud resources in the same region.</td>
</tr>
<tr>
<td>Number of protected IPs</td>
<td>Number of public IPs to be protected by an Anti-DDoS Pro instance. Available specifications: 10 (default), 50, and 100.</td>
</tr>
<tr>
<td>Application bandwidth</td>
<td>It refers to the normal bandwidth of the protected application. It is billed based on monthly 95th percentile by either the outgoing or incoming traffic (whichever is higher).</td>
</tr>
<tr>
<td>Protection period</td>
<td>Select how long the service plan you want to purchase. The fees are prepaid and calculated based on the base protection bandwidth, application bandwidth and the purchased usage period.</td>
</tr>
<tr>
<td>Protection times</td>
<td>Number of all-out protection chances for your application.</td>
</tr>
<tr>
<td>Auto-renewal</td>
<td>Optional. When auto-renewal is enabled, your subscription will be automatically renewed upon the expiration if your Tencent Cloud account has sufficient balance. The renewal cycle is 3 months for Anti-DDoS Pro instances that are purchased on a quarterly or yearly basis.</td>
</tr>
</tbody></table>
>!
>- You can enable elastic application bandwidth when you need to increase application bandwidth and QPS. After it’s enabled, the amount of bandwidth exceeding the specified amount will be billed. For billing details, see [Billing Overview (Standard)](https://www.tencentcloud.com/document/product/1029/55300).
>- Anti-DDoS Pro allows you to exceed your plan’s limit, but the all-out protection capability will become not available and only the basic protection capability remains when the limit has been exceeded for 36 hours accumulatively in a month.
>
3. Click **Pay Now** to complete your purchase.

## Purchasing Anti-DDoS Pro (Enterprise)
1. Log in to the [Anti-DDoS Pro purchase page](https://buy.cloud.tencent.com/antiddos#/native), and select **Enterprise**.
![](https://qcloudimg.tencent-cloud.cn/raw/6403ec864b5af9d362fc209a34e0d5d6.png)
2. Configure the following parameters as needed.
<table>
<thead>
<tr>
<th width="15%">Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Specification description</td>
<td><ul><li>Access mode: Pass-through</li><li>Bandwidth type: Tencent Cloud multi-BGP line network</li><li>Protection capability: Anti DDoS EIP</li><li>Notes:</li><li>Chinese mainland: Base protection + elastic protection</li><li>Outside Chinese mainland: Tencent Cloud Anti-DDoS cleansing center provides an all-out protection</li></ul></td>
</tr>
<tr>
<td>Region</td>
<td>Please select the region of the public IP. Currently, an Anti-DDoS Pro instance can only provide DDoS protection for public IPs of Tencent Cloud resources in the same region.</td>
</tr>
<tr>
<td>Number of protected IPs</td>
<td>Number of public IPs to be protected by an Anti-DDoS Pro instance. Available specifications: 10 (default), 50, and 100.</td>
</tr>
<tr>
<td>Base protection bandwidth</td>
<td>It supports monthly subscription. We recommend that you select a base protection bandwidth slightly higher than the average value of the historical attack traffic, which will allow you to handle normal attacks.</td>
</tr>
<tr>
<td>Elastic protection bandwidth</td>
<td>It is billed based on the actual protection bandwidth by day. We recommend that you select an elastic protection bandwidth slightly higher than the largest attack traffic in history to defend against normal attacks, and reduce the possibility of IP blocking caused by traffic exceeding the protection bandwidth limit.</td>
</tr>
<tr>
<td>Application bandwidth</td>
<td>It refers to the normal bandwidth of the protected application. It is billed based on monthly 95th percentile by either the outgoing or incoming traffic (whichever is higher).</td>
</tr>
<tr>
<td>Protection period</td>
<td>Select how long the service plan you want to purchase. The fees are prepaid and calculated based on the base protection bandwidth, application bandwidth and the purchased usage period.</td>
</tr>
<tr>
<td>Protection times</td>
<td>Number of all-out protection chances for your application.</td>
</tr>
<tr>
<td>Auto-renewal</td>
<td>Optional. When auto-renewal is enabled, your subscription will be automatically renewed upon the expiration if your Tencent Cloud account has sufficient balance. The renewal cycle is 3 months for Anti-DDoS Pro instances that are purchased on a quarterly or yearly basis.</td>
</tr>
</tbody></table>
>!
>- You can enable elastic application bandwidth when you need to increase application bandwidth and QPS. After it’s enabled, the amount of bandwidth exceeding the specified amount will be billed. For billing details, see [Billing Overview (Enterprise)](https://www.tencentcloud.com/document/product/1029/55301).
>- Anti-DDoS Pro allows you to exceed your plan’s limit, but the all-out protection capability will become not available and only the basic protection capability remains when the limit has been exceeded for 36 hours accumulatively in a month.
>
3. Click **Pay Now** to complete your purchase.
