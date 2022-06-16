

<dx-alert infotype="explain" title="">
For more information on the differences between Lighthouse and CVM, see [Comparison with CVM](https://intl.cloud.tencent.com/document/product/1103/41521).
</dx-alert>



## General Restrictions
An instance supports the overall upgrade of the configuration (computing, storage, and network) on a bundle basis but not bundle downgrade. For more information, see [Upgrading Instance Bundle](https://intl.cloud.tencent.com/document/product/1103/41562).

## Quota Limits[](id:quotaLimit)
 - Different Lighthouse instance bundles have different quotas of purchasable instances.
    <dx-alert infotype="explain" title="">
    The instance quota refers to the maximum number of instances (including those to be repossessed) of a bundle type in a region under an account.
    For example:
 - In Singapore region, the quota of General bundles is **20 per account**. Assume that you **2 General instances** in this region, your remaining quota of General instances in this region will be **18**.
 - In Silicon Valley region, the Enterprise instance bundle has a default quota of **50 instances**. If you already have **10 Enterprise instances** in this region, your remaining quota of Enterprise instances in this region will be **40**.
</dx-alert>
 The quota of instances that can be created under each account is as shown below:
 <table>
 <tr>
	 <th>Region</th>
	 <th>Instance Package Type</th>
	 <th>Quota (Instances/Region)</th>
 </tr>
 <tr>
	 <td rowspan=3>Hong Kong/Macao/Taiwan (China) and other countries/regions</td>
	 <td>General</td>
	 <td>20</td>
 </tr>
 <tr>
	 <td>Enterprise</td>
	 <td>50</td>
 </tr>
 </table>
 <dx-alert infotype="notice" title="">
- Lighthouse instances divide into **General** and **Enterprise** bundles that come with different configurations. For more information on instance bundles, see [Basic Bundle Overview](https://intl.cloud.tencent.com/document/product/1103/41403).
- The General bundle can be upgraded to the Enterprise bundle. The upgraded instances will take up the quota of the target package.
  </dx-alert>
 - Up to **100** firewall rules can be created for each Lighthouse instance.
 - Up to **10** SSH key pairs can be created in each region under one account.
 - Up to **20** custom images can be created in each region.
 - Snapshot quota limits:
  - The maximum number of free snapshots in each region is the number of created instances multiplied by 2 and cannot exceed 10.

## Private Network Connectivity Limits
There are certain limits on private network connectivity between Lighthouse and other Tencent Cloud services. For more information, see [Region and Network Connectivity](https://intl.cloud.tencent.com/document/product/1103/41266).
