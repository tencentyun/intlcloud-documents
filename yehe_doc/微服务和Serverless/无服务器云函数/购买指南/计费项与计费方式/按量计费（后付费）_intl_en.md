


## Billing Mode

You can estimate your SCF usage and calculate the corresponding fees by using the [SCF Price Calculator](https://intl.cloud.tencent.com/pricing/scf?rid=1&invokeCountUnit=1&invokeDurationUnit=1&publicNetOutTrafficUnit=1&timestamp=0). For more information on SCF billing, see [Pricing](https://intl.cloud.tencent.com/document/product/583/12281) and [Notes on Overdue Payment](https://intl.cloud.tencent.com/document/product/583/12283).

SCF is pay-as-you-go hourly in **USD** based on your actual usage in excess of the free tier and basic package. An event-triggered or HTTP-triggered function bill consists of the following parts (each part is billed according to its statistics and calculation method, and the fees are accurate to two decimal places in **USD**).
>? After three months of activation of SCF, you will no longer be entitled to a free tier, and the system will grant a basic package tier and automatically deduct 1.8 USD (by deducting 0.06 USD per day) every month. If you have activated SCF for less than three months and are entitled to a free tier or have valid packages or remaining resource packs, or the function resource usage, number of invocations, and public network outbound traffic in the last calendar month are all 0, the system will not deduct the basic package fees.

<table>
	<tr>
		<th>Event-Triggered Function</th>
		<th>HTTP-Triggered Function</th>
	</tr>
<td>
<li>Resource usage fees</li>
<li>Invocation fees</li>
<li>Public network outbound traffic fees</li>
<li>Idle provisioned concurrency fees</li>
<li>Basic package fees</li></td>
<td>
<li>Resource usage fees</li>
<li>HTTP-triggered function invocation fees</li>
<li>Public network outbound traffic fees</li>
<li>Idle provisioned concurrency fees</li>
<li>Basic package fees</li>	
<li>HTTP-triggered function response traffic fees (HTTP-triggered functions with different types of triggers have different billing modes. For more information, see <a href="https://intl.cloud.tencent.com/document/product/583/45902">HTTP-Triggered Function Billing</a>.)</li>
</td>
</table>
For the unit prices of resource usage, invocations, public network outbound traffic, idle provisioned concurrency, and basic package, see [Pricing](https://intl.cloud.tencent.com/document/product/583/12281).

## Billing Principles

SCF fees will be incurred by the actual loading and execution of the function code. If the function code is not actually executed, no fees will be incurred unless **provisioned concurrency** and **basic package** are configured. Below is an example:

<table>
	<tr>
		<th>Scenario</th>
		<th>Function Execution Status</th>
		<th>Billable Usage</th>
		<th>Billed</th>
	</tr>
	<tr>
		<td>A request error occurs due to an incorrect parameter, incorrect function name, or non-existent function.</td>
		<td>Not executed</td>
		<td>No</td>
		<td>No</td>
	</tr>
	<tr>
		<td>An error occurs due to function execution timeout or function execution memory overrun.</td>
		<td>Executed</td>
		<td>Yes</td>
		<td>Yes</td>
	</tr>
	<tr>
		<td>An error occurs due to a function code problem.</td>
		<td>Executed</td>
		<td>Yes</td>
		<td>Yes</td>
	</tr>
	<tr>
		<td>A request error occurs due to concurrency overrun.</td>
		<td>Not executed</td>
		<td>No</td>
		<td>No</td>
	</tr>
</table>
