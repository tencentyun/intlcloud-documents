## General Restrictions
1. BWP is currently in beta test. If you want to try it out, please [submit an application](https://intl.cloud.tencent.com/apply/p/86ulv50u1e8).
2. Depending on the account type, an account can only use one specific bandwidth package.
  - A bill-by-CVM account can only use the device bandwidth package.
  - A bill-by-EIP/CLB account can only use the IP bandwidth package. 

## Restrictions on Device Bandwidth Packages
1. Only one device bandwidth package can be activated in each region.
2. The bandwidth package in a region cannot be used together with any other billing mode. After a device bandwidth package is activated in a region, all CVMs and CLBs in the current region are automatically billed by bandwidth package. The paid bandwidth fee will be refunded after conversion based on the number of hours actually used.

## Restrictions on IP Bandwidth Packages
1. Up to 20 bandwidth packages can be activated in each region.
2. The bandwidth package in a region can be used together with other billing modes such as bill-by-traffic.
3. Currently, monthly subscription public IPs and EIPs cannot be added to IP bandwidth packages.
4. Up to 100 EIPs can be added to one bandwidth package.
