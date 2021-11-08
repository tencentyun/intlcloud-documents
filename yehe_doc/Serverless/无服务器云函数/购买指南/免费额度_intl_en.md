## Free Tier

Starting from November 1, 2021, all SCF users will be entitled to a certain free tier of invocations, resource usage, and public network outbound traffic each month as shown below:

<dx-alert infotype="explain" title="">
The free tier in each month cannot be accumulated and will be reset at the beginning of the next month.
Upon settlement, fees are deducted in the order of free tier > resource package > pay-as-you-go billing (voucher) > pay-as-you-go billing, that is, the free tier is used first, and fees for excessive usage are deducted from valid resource packages, and if there are no valid resource packages or they have been used up, fees are charged in the pay-as-you-go manner.
The free tier of resource usage is not applicable to idle provisioned concurrency.
</dx-alert>


<table>
  <tr>
    <th class="align-left">Granting Time</th>
    <th class="align-left">Billable Item</th>
    <th class="align-left">Free Tier</th>
  </tr>
  <tr>
    <td rowspan="3">Every month in the first three months after the activation (including the month of activation)</td>
    <td>Number of invocations</td>
    <td>2 million invocations (1 million invocations of event-triggered functions and 1 million invocations of HTTP-triggered functions)</td>
  </tr>
  <tr>
    <td>Resource usage</td>
    <td>400,000 GBs</td>
  </tr>
  <tr>
    <td>Public network outbound traffic</td>
    <td>1 GB</td>
  </tr>
  <tr>
    <td rowspan="3">Every month after three months of the activation</td>
    <td>Number of invocations</td>
    <td>100,000 invocations (50,000 invocations of event-triggered functions and 50,000 invocations of HTTP-triggered functions)</td>
  </tr>
  <tr>
    <td>Resource usage</td>
    <td>20,000 GBs</td>
  </tr>
  <tr>
    <td>Public network outbound traffic</td>
    <td>0.5 GB</td>
  </tr>
</table>

>?
>- If you ever use SCF and invoke functions before November 1, 2021, the above rules will take effect from November 1, 2021.
>- If you never use SCF before November 1, 2021, the above rules will take effect when you invoke a function for the first time after activating SCF.

The following table lists free execution durations per function per month when the function is configured with different memory sizes:

| Memory (MB) | Free Duration (Seconds) |
|:----|:----|
| 64 | 6,400,000 |
| 128 | 3,200,000 |
| 256 | 1,600,000 |
| 512 | 800,000 |
| 1,024 | 400,000 |
| 1,536 | 266,667 |
| 3,072 | 133,333 |



