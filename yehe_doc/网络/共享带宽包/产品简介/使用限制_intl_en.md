## General Restrictions
1. BWP is currently in beta. To try it out, please [submit an application to be added to the beta list](https://intl.cloud.tencent.com/apply/p/86ulv50u1e8).
2. - A bill-by-IP account can only use the IP bandwidth package.
   - A bill-by-CVM account can only use the device bandwidth package, but elastic IPv6 public IP addresses, IPv6 CLB instances and static single-line EIPs also support using the IP bandwidth package.
>?There are two types of Tencent Cloud accounts: bill-by-IP account and bill-by-CVM account. All Tencent Cloud accounts registered after 00:00:00 on June 17, 2020 are bill-by-IP accounts. If you have registered an account before that time, you can check your account type in the console as instructed in [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).

## Restrictions on Device Bandwidth Packages 
1. Only one device bandwidth package can be activated in each region.
2. The bandwidth package in a region cannot be used together with any other billing mode. After a device bandwidth package is activated in a region, all CVMs and CLBs in the region will be automatically billed in the bandwidth package. The paid bandwidth fee is refunded after conversion based on the number of hours actually used.

## Restrictions on IP Bandwidth Packages
1. Up to 20 IP bandwidth packages can be activated in one region.
2. The bandwidth package can be used together with other billing modes such as monthly bandwidth subscription, hourly bandwidth, and bill-by-traffic in the same region.
3. Currently, monthly-subscribed public IPs and EIPs cannot be added to IP bandwidth packages.
4. Up to 100 resources, including EIPs, public IPs, and CLBs in the same region, can be added to a single bandwidth package.
