Tencent Cloud accounts include bill-by-IP and bill-by-CVM accounts. We recommend that you upgrade your bill-by-CVM accounts to bill-by-IP accounts as the former cannot support new features later.
>! Note: Downgrading from "bill-by-IP" to "bill-by-CVM" is not allowed.
>

## Checking Account Type[](id:judge)
All Tencent Cloud accounts registered after June 17, 2020 00:00:00 will be bill-by-IP accounts. For Tencent Cloud accounts registered before June 17, 2020, check your account types in the console.
Log in to <a href="https://console.cloud.tencent.com/cvm/eip">Public IP Console</a>. Check if there is a prompt message at the top of the "Public IP" page.
 - If no, you have a bill-by-IP account.
 - If yes, you have a bill-by-CVM account.
![](https://main.qcloudimg.com/raw/5a0c24c3e886b9f09b373a1450058750.png)

## Account Types
- **Bill-by-IP account** manages bandwidth and traffic on IP or CLB. For such an account, public IP or CLB, instead of CVM, has the public network bandwidth and traffic resources.
- **Bill-by-CVM account** manages bandwidth and traffic on CVM. For such an account, network bandwidth and traffic can be purchased on CVM, instead of public IP or CLB.
![](https://qcloudimg.tencent-cloud.cn/raw/499f146e1bab182862d968705f6e111a.png)

## Account Upgrade

### Advantages
A comparison between the advantages of bill-by-IP and bill-by-CVM accounts is shown below:
<table>
<tr>
<th width="20%">Item</th>
<th width="40%">Bill-by-IP account</th>
<th width="40%">Bill-by-CVM account</th>
</tr>
<tr>
<td>Whether the network bandwidth under the account can be migrated to other CVM instances</td>
<td>Yes, as the public network fees are billed by IP.</td>
<td>No, as the public network fees are billed on the bound CVM instance.</td>
</tr>
<tr>
<td>Elastic IPv6 billing</td>
<td>IPv6 and IPv4 can be added into the same bandwidth package and billed together.</td>
<td>IPv6 can only be billed separately.</td>
</tr>
<tr>
<td>NAT gateway billing</td>
<td>Bill by traffic and bill by bandwidth package are supported.</td>
<td>Only bill by traffic is supported.</td>
</tr>
<tr>
<td>Is it necessary to purchase public network for CLB backend CVM</td>
<td>No. Only bandwidth needs to be purchased for CLB, which facilitates management.</td>
<td>Yes. Purchasing public network for all CLB backend CVMs is needed, which complicates management.</td>
</tr>
<tr>
<td>New network-related features</td>
<td>Both the existing and new features are supported.</td>
<td>Only the existing features are supported.</td>
</tr>
</table>

### Impacts of upgrade
<dx-accordion>
::: Impact on network fees
- The account upgrade has no impact on the public network price.
- After the upgrade, the network billing mode and price of the CVM billed by traffic will remain unchanged. The changes of other CVMs' network billing modes are detailed below:
<table>
<tr>
<th width="12%">CVM Billing Mode</th>
<th width="10%">Network Billing Mode</th>
<th width="35%">Public IP</th>
<th width="43%">Impact</th>
</tr>
<tr>
<td>Pay-as-you-go</td>
<td>Bill by hourly bandwidth</td>
<td>The instance has multiple public IPs</td>
<td>The network billing mode of all public IPs is converted to bill by traffic. No refund is involved.
</tr>
</table>
:::
::: Impact on bandwidth cap
 - If the public IP is bound with the CVM, its bandwidth cap after the upgrade is the same as that of the CVM before the upgrade.
 - If the public network IP is bound with NAT gateway or CLB instead of CVM, its bandwidth cap after the upgrade is the maximum value in the past 7 days.
 - If the public IP is not bound with any resources, its bandwidth cap is specified as 100 M.
:::
::: Impact on \sIP\s address
The account upgrade has no impact on the public or private IP addresses.
:::
::: Impact on network connection
When there are no more than 500 CVM instances, the upgrade lasts about 5 minutes. The more CVM instances, the longer the upgrade lasts. During the upgrade, the network will not be disconnected, but try not to purchase new services or operate in the console.
:::
::: Impact on API call
- After the upgrade, when calling the API for creating an EIP, `InternetChargeType` (billing mode) and `InternetMaxBandwidthOut` (bandwidth cap) must be specified. For details, please see the API document [AllocateAddresses](https://intl.cloud.tencent.com/document/product/215/16699).
- After the upgrade, when calling the APIs for creating CVMs or AS services, if `InternetChargeType` is set as `BANDWIDTH_PACKAGE` (bill by bandwidth package), `BandwidthPackageId` (ID of the bandwidth package to be added) must be specified.
:::
</dx-accordion>

### Upgrade mode
Tencent Cloud will send upgrade notices to bill-by-CVM accounts in batches. To upgrade your account, you can also [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>! Because some upgrade scenarios will change the CVM billing mode, if your CVM is purchased in promotional campaigns and its billing mode is non-switchable according to the campaign rules, your account upgrade is not supported.
>
