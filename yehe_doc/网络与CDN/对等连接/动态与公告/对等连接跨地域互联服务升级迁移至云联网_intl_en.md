Dear Tencent Cloud user,
Tencent Cloud is going to discontinue the Peering Connection - Cross-Region Interconnection Service at 00:00 on October 31, 2022. You cannot create the cross-region peering connection instances after 00:00 on June 30, 2022. To ensure a more stable and high-quality network service for your cross-region interconnection business, please migrate it to CCN as instructed in **Best Practices** [Migrating Cross-Region Interconnection Service to CCN](https://intl.cloud.tencent.com/document/product/553/47418) in time.

For any questions during the upgrading migration, please contact your sales rep or [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Upgrade Process
<dx-steps>
- Work out a plan
- Assess your business
- Create a CCN instance
- Cut over and migrate the business
- Test and accept the business
- Delete the peering connection instances you no longer use
</dx-steps>

1. Tencent Cloud provides you with ready-made plans. For details, see [Migrating Cross-Region Interconnection Service to CCN](https://intl.cloud.tencent.com/document/product/553/47418).[](id:1)
2. You can select an appropriate plan in [Step 1](#1) for evaluation based on your actual business scenario.
3. Create a CCN instance according to the upgrade plan.
4. Cut over and migrate the original peering connection business to CCN.
5. After the migration is complete, test and debug your business to ensure the normal operation.
6. Delete the original peer connection instance.

## Advantages of CCN
<table>
<tr>
<th>Influence</th>
<th>Description</th>
</tr>
<tr>
<td>Performance</td>
<td>Low latency. Interconnection via the shortest path avoids the impact of linkage congestion caused by bypassing the public network.</td>
</tr>
<tr>
<td>Price</td>
<td>CCN is more affordable than Direct Connect in terms of cross-region tunnel traffic fees.</td>
</tr>
<tr>
<td>Expansion</td>
<td>Feature the public and private network interconnection of CCN resources.</td>
</tr>
</table>

## FAQs
### What risks do I face if I don't upgrade?
The cross-region peering connection will be discontinued on October 31, 2022, and will not be maintained later. If you continue to use it, you will face operational risks. In extreme scenarios, it may cause business failures and cannot be quickly recovered.

### What exactly does a cross-region peering connection refer to?
The peering connections connect two VPCs through the private network and are divided into intra-region and cross-region connections based on the VPC regions. Tencent Cloud is going to discontinue the cross-region peering connection.

### Will the intra-region peering connection be discontinued?
No. Only the cross-region peering connection will be discontinued this time.

### Can all plans support smooth migration?
 Yes. The migration plans in [Migrating the Cross-Region Interconnection Service to CCN](https://intl.cloud.tencent.com/document/product/553/47418) all support smooth migration. The migration may be jittery, but will not cause service suspension.
 - VPCs are interconnected when the two-way routes between VPCs are directed to the peering connection and CCN instances separately.
 - One or two packets may be lost when routing is enabled.

### Will the cost increase if I change a cross-region tunnel to the cross-region CCN connection?
No. Under the same service availability (99.95%), the price of CCN is lower than that of Peering Connection. CCN provides three service levels for your choices based on the business availability. For CCN billing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1003/30053).

The bandwidth price comparison between Peering Connection and CCN in the Chinese mainland (excluding Hong Kong, Macao and Taiwan) regions is as follows. For bandwidth prices in regions outside the Chinese mainland and other regions, please contact your sales rep.

<table>
<tr>
<th>Bandwidth Range (Mbps)</th>
<>Daily Peak Bandwidth Billing of Peering Connection (USD/Mbps/Day)</th>
<th>Monthly 95th Percentile Billing of Peering Connection (USD/Mbps/Day)</th>
<th>Monthly 95th Percentile Billing of Cross-Region CCN Connection (Service Level: Gold; Availability: 99.95%)</th>
<th>Monthly 95th Percentile Billing of Cross-Region CCN Connection (Service Level: Silver; Availability: 99.5%)</th>
</tr>
<tr>
<td>(0,10]</td>
<td>3.19</td>
<td>85</td>
<td>37</td>
<td>28</td>
</tr>
<tr>
<td>(10,20]</td>
<td>3.19</td>
<td>63</td>
<td>37</td>
<td>28</td>
</tr>
<tr>
<td>(20,50]</td>
<td>1.98</td>
<td>43</td>
<td>37</td>
<td>28</td>
</tr>
<tr>
<td>(50,100]</td>
<td>1.98</td>
<td>34</td>
<td>37</td>
<td>28</td>
</tr>
<tr>
<td>(100,200]</td>
<td>1.48</td>
<td>25</td>
<td>13</td>
<td>10</td>
</tr>
<tr>
<td>(200,500]</td>
<td>1.48</td>
<td>18</td>
<td>13</td>
<td>10</td>
</tr>
<tr>
<td>(500,1000]</td>
<td>1.19</td>
<td>14</td>
<td>13</td>
<td>10</td>
</tr>
<tr>
<td>(1000,2000]</td>
<td>1.19</td>
<td>11</td>
<td>9</td>
<td>7</td>
</tr>
<tr>
<td> 2,000</td>
<td>0.82</td>
<td>10</td>
<td>9</td>
<td>7</td>
</tr>
</table>

