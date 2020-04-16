## What is Tencent Cloud Bandwidth Package?
Tencent Cloud Bandwidth Package (BWP) is a multi-IP aggregated billing method that can significantly reduce the costs of Internet access. When peaks Internet traffic periods of the business occur at different times, BWP can be used to bill the traffic in an aggregated manner to realize noticeable cost savings. 
BWP provides [Monthly Top 5 Billing](https://intl.cloud.tencent.com/document/product/684/15255) and [Monthly 95th Percentile Billing](https://intl.cloud.tencent.com/document/product/684/15255) for different scenarios.

## Product Types
Tencent Cloud offers different bandwidth packages for different accounts: 
- **Accounts whose internet fees are billed on CVMs**: only device bandwidth packages are available
 Device Bandwidth Package applies to accounts whose internet fees are billed on CVMs, which mean that the public network capability (bandwidth cap) and billing method (bill-by-traffic or bill-by-bandwidth) are specified upon creation of the CVM instance. The public IP address and CLB acts only as public network egress. 
- **Accounts whose internet fees are billed on public IP or CLB**: only IP bandwidth packages are available
  IP Bandwidth Package applies to accounts whose internet fess are billed on public IP or CLB, which mean that the public network capability (bandwidth cap) and billing method (bill-by-traffic or bill-by-bandwidth) are specified upon creation of the IP or CLB instance.

Each account supports only one type of bandwidth packages. To learn about your account type and available bandwidth package type, please refer to [区分Your Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
>
>- The account type is defined according to the creation time of your account, and Tencent Cloud will not change it.
> - You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply to change from billing on CVMs to billing on public IPs/CLBs, but not vise versa.


## Supported Resources 
### Device Bandwidth Packages
Device Bandwidth Packages support CVMs and CLBs.

## IP Bandwidth Packages
IP Bandwidth Packages support public IPs, EIPs (bound with CVM, NAT gateway) and CLBs.
