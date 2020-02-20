## General Restrictions
2. An account can only use one type of bandwidth packages, which is determined by the account type.
  - Accounts billed by traffic on CVM can use only device bandwidth packages.
  - Accounts billed by traffic on IP can use only IP bandwidth packages.

## Restrictions on Device Bandwidth Packages
1. Only one device bandwidth package can be activated in each region.
2. The shared bandwidth package in a region cannot be used together with any other billing mode. After a device bandwidth package is activated in a region, the billing mode of all CVMs and CLBs in the current region is automatically changed to billing by bandwidth package. The paid bandwidth fee is refunded after conversion based on the number of hours actually used.

## Restrictions on IP Bandwidth Packages
1. Up to 20 bandwidth packages can be activated in one region.
2. The bandwidth package can be used together with other billing modes such as hourly bandwidth, and bill-by-traffic in the same region.
3. Currently, monthly subscription EIPs and normal public IPs cannot be added to IP bandwidth packages.
4. Up to 100 EIPs can be added to one bandwidth package.
