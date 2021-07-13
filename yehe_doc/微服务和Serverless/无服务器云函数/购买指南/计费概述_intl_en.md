
## Free Tier

SCF users are entitled to a certain free tier of resource usage and invocations each month, as shown below. There is no free tier for public network outbound traffic.

| Billable Item | Monthly Free Tier |
| ------------| -------------- |
| Resource usage | 400,000 GBs |
| Invocations | 1 million |

For more information, please see [Free Tier](https://intl.cloud.tencent.com/document/product/583/12282).

## Billing Modes and Billable Items

SCF is pay-as-you-go **hourly** in **USD**.

SCF is billed according to the following four parts. Each part is billed according to its statistics and calculation method, and the fees in **USD** are accurate to two decimal places:

 - **Resource usage fees**: resource usage is calculated in GBs by multiplying the configured function memory size by the function execution duration.
 - **Invocation fees**: each function triggering and execution is calculated as an invocation.
 - **Public network outbound fees**: the outbound traffic consumed when the function code accesses the public network is counted as the public network outbound traffic in GB.
 - **Idle provisioned concurrency fees**: the number of idle instances is calculated by subtracting the number of actually running concurrent instances from the number of launched provisioned instances, and the idle resource usage is calculated in GBs by multiplying the number of idle instances by the configured memory size.

For more information, please see [Billing Mode](https://intl.cloud.tencent.com/document/product/583/12284).

## Pricing

The four billable items of SCF are priced as follows:

 - **Resource usage fees**: 0.0000167 USD/GBs
 - **Invocation fees**: 0.002 USD/10,000 invocations
 - **Public network outbound traffic fees**: 0.12 USD/GB for the Chinese mainland; variable by region
 - **Idle provisioned concurrency**: 0.00000847 USD/GBs

For more information, please see [Pricing](https://intl.cloud.tencent.com/document/product/583/12281).

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
<td>South Asia Pacific (Mumbai)</td><td>ap-mumbai</td>
</tr>
<tr>
<td>Southeast Asia Pacific (Singapore)</td><td>ap-singapore</td>
</tr>
<tr>
<td>Northeast Asia Pacific (Tokyo)</td><td>ap-tokyo</td>
</tr>
<tr>
<td>North America (Toronto)</td><td>na-toronto</td>
</tr>
<tr>
<td>West US (Silicon Valley)</td><td>na-siliconvalley</td>
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
<td><a href="https://intl.cloud.tencent.com/document/product/583/12284" target="_blank">View document</a></td>
</tr>
<tr>
<td>Pricing</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12281" target="_blank">View document</a></td>
</tr>
<tr>
<td>Notes on Overdue Payment</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12283" target="_blank">View document</a></td>
</tr>
<tr>
<td>Billing Example</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12285" target="_blank">View document</a></td>
</tr>
</tbody></table>
