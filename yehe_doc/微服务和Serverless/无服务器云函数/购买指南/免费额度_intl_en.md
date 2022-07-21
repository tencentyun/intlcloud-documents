
## Free Tier
### Free tier granting

- If you ever used SCF and invoked functions before March 1, 2022, then starting from June 1, 2022, the system will no longer grant a free tier.
- If you ever used SCF and invoke functions between March 1, 2022 and May 31, 2022, the system will grant a free tier every month in the first three months after the activation (including the month of activation).
- If you never used SCF before June 1, 2022, the system will grant a free tier starting from the time of the first function invocation after the activation of SCF.
- On the first day of every month, the platform counts the function invocations in the last calendar month. If the function resource usage, number of invocations, and public network outbound traffic in the last month are all 0, the **basic package fees** will not be charged in the current month. If any function usage is generated in the current month, the basic package fees will be charged next month.
- HTTP-triggered function response traffic is not included in the free tier. For more information, see [HTTP-Triggered Function Billing](https://intl.cloud.tencent.com/document/product/583/45902).



### Every month in the first three months (including the month of activation)

Every month in the first three months after the activation of SCF (including the month of activation), you are entitled to a free tier, which will be reset in the next calendar month. The free tier will be granted when you purchase a package through free trial or will be granted automatically by the system by default. A free tier includes one million event-triggered function invocations and one million HTTP-triggered function invocations, resource usage of one million GBs, and public network outbound traffic of 2 GB. You can also get a free tier by [purchasing a Personal Advanced package through free trial](https://console.cloud.tencent.com/scf/buy), and the function concurrency quota will be **doubled**.

>? 
- Users who have used SCF for less than three months as of June 1, 2022 will still be granted a free tier for one month on June 1.
- Users who have used SCF for less than two months as of June 1, 2022 will be granted a free tier on June 1 and July 1 for the respective months.
- Users who have used SCF for less than one month as of June 1, 2022 will be granted a free tier on June 1, July 1, and August 1 for the respective months.



<table>
  <tr>
    <th width="30%">Granting Time</th>
    <th width="15%">Billable Item</th>
    <th width="30%">Free Tier</th>
    <th class="align-left">Description</th>
  </tr>
  <tr>
    <td rowspan="3">Every month in the first three months after the activation (including the month of activation)</td>
    <td>Number of invocations</td>
    <td>One million invocations (one million invocations for event-triggered functions and one million invocations for HTTP-triggered functions)</td>
    <td rowspan="3">None</td>
  </tr>
  <tr>
    <td>Resource usage</td>
    <td>One million GBs</td>
  </tr>
  <tr>
    <td>Public network outbound traffic</td>
    <td>2 GB</td>
  </tr>
</table>



The following table lists free execution durations per function per month when the function is configured with different memory sizes under the free tier plan for the first three months:


| Memory (MB) | Free Duration (Seconds) |
| :--------- | :------------- |
| 64         | 16,000,000     |
| 128        | 8,000,000      |
| 256        | 4,000,000      |
| 512        | 2,000,000      |
| 1024       | 1,000,000      |
| 1536       | 666,666        |
| 3072       | 333,333        |




### Every month after three months of activation
After three months of activation of SCF, you will no longer be entitled to a free tier, and the system will grant a basic package tier (including 500,000 invocations of event-triggered functions, 500,000 invocations of HTTP-triggered functions, resource usage of 100,000 GBs, and public network outbound traffic of 2 GB) and automatically deduct 1.8 USD (by deducting 0.06 USD per day) every month. If you have valid packages or remaining resource packs, the system will not deduct the **basic package fees**. If the function resource usage, number of invocations, and public network outbound traffic in the last calendar month are all 0, the **basic package fees** will not be charged in the current month.
<table>
  <tr>
    <th width="20%">Granting Time</th>
    <th width="15%">Billable Item</th>
    <th width="20%">Free Tier</th>
    <th width="30%">Basic Package Tier</th>
    <th class="align-left">Description</th>
  </tr>
  <tr>
    <td rowspan="3">Every month after three months of the activation</td>
    <td>Number of invocations</td>
    <td>0 invocations (0 invocations for event-triggered functions and 0 invocations for HTTP-triggered functions)</td>
    <td>500,000 invocations (500,000 invocations for event-triggered functions and 500,000 invocations for HTTP-triggered functions)</td>
    <td rowspan="3">The system will grant a basic package tier and automatically deduct 1.8 USD every month.</td>
      </tr>
  <tr>
    <td>Resource usage</td>
    <td>0 GBs</td>
    <td>100,000 GBs</td></tr>
  <tr>
    <td>Public network outbound traffic</td>
    <td>0 GB</td>
    <td>2 GB</td>  </tr>
</table>






## Notes
- The free tier for every month in the first three months cannot be accumulated and will be reset at the beginning of the next month.
- Upon settlement, fees are deducted in the order of free tier/basic package tier > namespace-specific package > region-specific package > all-region resource pack > pay-as-you-go billing, that is, the free tier/basic package tier is used first, and fees for excessive usage are deducted from valid packages/resource packs, and if there are no valid packages/resource packs or they have been used up, fees are charged in the pay-as-you-go manner.
- The free tier of resource usage is not applicable to idle provisioned concurrency.
</dx-alert>

