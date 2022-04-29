
## Free Tier

Starting from November 1, 2021, all SCF users are entitled to a certain free tier of invocations, resource usage, and public network outbound traffic each month as shown below:

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


For more information, see [Free Tier](https://intl.cloud.tencent.com/document/product/583/12282).


## Billable Items and Billing Modes
### Billable items
SCF is billed by the following four parts. Each part is billed according to its statistics and calculation method, and the fees are accurate to two decimal places in **USD**:

- **Resource usage fees**: Resource usage is calculated in GBs by multiplying the configured function memory size by the function execution duration.
- **Invocation fees**: Each function triggering and execution is calculated as an invocation.
- **Public network outbound traffic fees**: The outbound traffic consumed when the function code accesses the public network is counted as the public network outbound traffic in GB.
- **Idle provisioned concurrency fees**: The number of idle instances is calculated by subtracting the number of actually running concurrent instances from the number of started provisioned instances, and the idle resource usage is calculated in GBs by multiplying the number of idle instances by the configured memory size. For pricing details, see [Provisioned Concurrency Pricing](https://intl.cloud.tencent.com/zh/document/product/583/44256).

>? For HTTP-triggered functions using the default trigger, HTTP-triggered function response traffic will be additionally generated, which is not included in the free tier.
>
### Billing mode
SCF is [**pay-as-you-go (postpaid)**](https://intl.cloud.tencent.com/zh/document/product/583/42969).

## Pricing

The four billable items of SCF are priced as follows:

- Resource usage fees: 0.0000167 USD/GBs (0.167 USD/10000 GBs)
- Invocation fees: 0.002 USD/10000 invocations
- Public network outbound traffic fees: 0.12 USD/GB for the Chinese mainland; variable by region
- Idle provisioned concurrency fees: 0.00000847 USD/GBs (0.0847 USD/10000 GBs). For more information, see [Billing Details](https://intl.cloud.tencent.com/zh/document/product/583/42969) and [Billing Example](https://intl.cloud.tencent.com/document/product/583/12285).

HTTP-triggered functions and event-triggered functions have the same prices. For HTTP-triggered functions using the default trigger, HTTP-triggered function response traffic will be additionally generated.

## Supported Regions
SCF is currently supported in the following regions:
<table>
<tr>
<th width="50%">Region</th><th width="50%">Value</th>
</tr>
<tr>
<td>South China (Guangzhou)</td><td>ap-guangzhou</td>
</tr>
<tr>
<td>East China (Shanghai)</td><td>ap-shanghai</td>
</tr>
<tr>
<td>North China (Beijing)</td><td>ap-beijing</td>
</tr>
<tr>
<td>Southwest China (Chengdu)</td><td>ap-chengdu</td>
</tr>
<tr>
<td>Hong Kong/Macao/Taiwan (China)</td><td>ap-hongkong</td>
</tr>
<tr>
<td>South Asia (Mumbai)</td><td>ap-mumbai</td>
</tr>
<tr>
<td>Southeast Asia (Singapore)</td><td>ap-singapore</td>
</tr>
<tr>
<td>Northeast Asia (Seoul)</td><td>ap-seoul</td>
</tr>
<tr>
<td>North America (Toronto)</td><td>na-toronto</td>
</tr>
<tr>
<td>Western US (Silicon Valley)</td><td>na-siliconvalley</td>
</tr>
<tr>
<td>Europe (Frankfurt)</td><td>eu-frankfurt</td>
</tr>
</table>



## Billing Details

For billing details, see the following documents:

<table>
<thead>
<tr>
<th width="50%">Document Name</th>
<th width="50%">Link</th>
</tr>
</thead>
<tbody><tr>
<td>Free Tier</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12282" target="_blank">View document</a></td>
</tr>
<tr>
<td>Overdue Payment</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12283" target="_blank">View document</a></td>
</tr>
<tr>
<td>Billing Example</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12285" target="_blank">View document</a></td>
</tr>
</tbody></table>

## Billing of Other Products Used by SCF
Other products used by SCF, such as [CFS](https://intl.cloud.tencent.com/document/product/582/9553), [COS](https://intl.cloud.tencent.com/document/product/436/16871), and [CLS](https://intl.cloud.tencent.com/document/product/614/11254), will be billed according to their respective billing rules.

SCF execution logs are supported by and delivered to CLS by default. For more information on log delivery, see [Log Delivery Configuration](https://intl.cloud.tencent.com/document/product/583/39778). CLS provides a certain [free tier](https://intl.cloud.tencent.com/document/product/614/37889), and any excess will be billed according to its pricing.
