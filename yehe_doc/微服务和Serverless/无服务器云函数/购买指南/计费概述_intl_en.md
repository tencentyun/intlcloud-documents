
## Free Tier

Starting from November 1, 2021, all SCF users will be entitled to a certain free tier of invocations, resource usage, and public network outbound traffic each month as shown below:

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


For more information, please see [Free Tier](https://intl.cloud.tencent.com/document/product/583/12282).

## Billable Items and Billing Modes
### Billable items
SCF is billed by the following four parts. Each part is billed according to its statistics and calculation method, and the fees are accurate to two decimal places in **USD**:

- **Resource usage fees**: resource usage is calculated in GBs by multiplying the configured function memory size by the function execution duration.
- **Invocation fees**: each function triggering and execution is calculated as an invocation.
- **Public network outbound fees**: the outbound traffic consumed when the function code accesses the public network is counted as the public network outbound traffic in GB.
- **Idle provisioned concurrency fees**: the number of idle instances is calculated by subtracting the number of actually running concurrent instances from the number of started provisioned instances, and the idle resource usage is calculated in GBs by multiplying the number of idle instances by the configured memory size.

>? HTTP-Triggered functions and event-triggered functions are billed in the same way.

### Billing mode
For more information on SCF billing mode, please see [Billing Mode](https://intl.cloud.tencent.com/zh/document/product/583/12284).

## Pricing

The four billable items of SCF are priced as follows:

- Resource usage fees: 0.0000167 USD/GBs (0.167 USD/10000 GBs)
- Invocation fees: 0.002 USD/10000 invocations
- Public network outbound traffic fees: 0.12 USD/GB for the Chinese mainland; variable by region
- Idle provisioned concurrency fees: 0.00000847 USD/GBs (0.0847 USD/10000 GBs). For more information, please see [Billing Example](https://intl.cloud.tencent.com/document/product/583/12285).

HTTP-Triggered functions and event-triggered functions have the same prices. For more information, please see [Pricing](https://intl.cloud.tencent.com/document/product/583/12281).

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
<td>Hong Kong/Macao/Taiwan (China Region) (Hong Kong, China)</td><td>ap-hongkong</td>
</tr>
<tr>
<td>South Asia Pacific (Mumbai)</td><td>ap-mumbai</td>
</tr>
<tr>
<td>Southeast Asia Pacific (Singapore)</td><td>ap-singapore</td>
</tr>
<tr>
<td>Northeast Asia Pacific (Seoul)</td><td>ap-seoul</td>
</tr>
<tr>
<td>North America (Toronto)</td><td>na-toronto</td>
</tr>
<tr>
<td>West US (Silicon Valley)</td><td>na-siliconvalley</td>
</tr>
<tr>
<td>Europe (Frankfurt)</td><td>eu-frankfurt</td>
</tr>
</table>



## Billing Details

For billing details, please see the following documents:

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
<td>Billing Mode</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/583/12284" target="_blank">View document</a></td>
</tr>
<tr>
<td>Pricing</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12281" target="_blank">View document</a></td>
</tr>
<tr>
<td>Notes on Arrears</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12283" target="_blank">View document</a></td>
</tr>
<tr>
<td>Billing Example</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12285" target="_blank">View document</a></td>
</tr>
</tbody></table>
