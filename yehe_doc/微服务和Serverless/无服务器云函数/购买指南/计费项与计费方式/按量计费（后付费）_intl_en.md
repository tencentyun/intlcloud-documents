


## Billing Mode

You can estimate your SCF usage and calculate the corresponding fees by using the [SCF Price Calculator](https://buy.intl.cloud.tencent.com/pricing/scf). For more information on SCF billing, see [Pricing](https://intl.cloud.tencent.com/document/product/583/12281) and [Notes on Overdue Payment](https://intl.cloud.tencent.com/document/product/583/12283).

SCF is pay-as-you-go hourly in **USD** based on your actual usage. An event-triggered or HTTP-triggered function bill consists of the following parts (each part is billed according to its statistics and calculation method, and the fees are accurate to two decimal places in **USD**).

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
</td>
<td>
<li>Resource usage fees</li>
<li>HTTP-Triggered function invocation fees</li>
<li>Public network outbound traffic fees</li>
<li>Idle provisioned concurrency fees</li>
</td>
</table>

For the unit prices of resource usage, invocations, public network outbound traffic, and idle provisioned concurrency, see [Pricing](https://intl.cloud.tencent.com/document/product/583/12281).


## Billing Principles

SCF fees will be incurred by the actual loading and execution of the function code. If the function code is not actually executed, no fees will be incurred unless provisioned concurrency is configured. Below is an example:

<table>
	<tr>
		<th>Scenario</th>
		<th>Function Execution Status</th>
		<th>Calculated</th>
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

