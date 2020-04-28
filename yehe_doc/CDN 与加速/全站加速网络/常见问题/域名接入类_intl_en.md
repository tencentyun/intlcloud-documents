### How do I connect a domain name to the ECDN acceleration platform?

You can connect a domain name to the ECDN acceleration platform in the following three steps:
1. Add an acceleration domain name configuration in the console.
2. Set the `hosts` file to verify whether the configuration takes effect.
3. Configure the domain name CNAME configuration. Then, the service takes effect.

For detailed directions, please see [Domain Name Connection](https://cloud.tencent.com/document/product/570/10361) .

### Should a domain name connected to ECDN complete ICP filing?
Whether the system checks the ICP filing status depends on your selected acceleration region:
- If the acceleration region includes regions in Mainland China, according to applicable laws and regulations, your domain name must get the ICP filing before being connected.
- If the acceleration region includes regions only outside Mainland China (including Hong Kong (China), Macau (China), and Taiwan (China)), your domain name does not need ICP filing.

### Can ECDN be connected to wildcard domain names?

No. ECDN currently cannot be connected to wildcard domain names.

### What origin-pull methods are supported by ECDN?

<table style="display:table;" width="80%">
	<thead>
		<tr>
			<th colspan="1" style="text-align: center" width=15%> Origin-pull Method </th>
			<th colspan="1" style="text-align: center" width=70%> Description </th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center">Optimal route selection origin-pull </td>
			<td>It is the default origin-pull policy.</br>The best-performance node is selected for origin-pull based on the platform's detection result. </td>
		</tr>
		<tr>
			<td style="text-align: center">Weighted origin-pull </td>
			<td>The origin-pull requests are proportionally scheduled to origin servers based on their weight. </td>
		</tr>
		<tr>
			<td style="text-align: center">Master/Slave origin-pull </td>
			<td>When the master origin server is normal, it will be used for origin-pull. Only when the master is exceptional can the slave be used. </td>
		</tr>
	</tbody>
</table>



<span id="port"></span>

### What differences are there between an acceleration port (or access port) and origin-pull port?

They have the following differences when CDN or ECDN is used:

<table>
   <tr>
      <th style="width: 80px; text-align: center;">Port Type</th>
      <th style="width: 300px; text-align: center;">Acceleration Port</th>
      <th style="width: 300px; text-align: center;">Origin-pull Port</th>
   </tr>
   <tr>
      <td style="width: 80px; text-align: center;">Port difference</td>
      <td style="width: 300px; text-align: left;">It is the CDN/ECDN service port, which is also the port for client or user requests of accessing edge servers</td>
      <td style="width: 300px; text-align: left;">It is the origin server service port, which is also the port for CDN/ECDN node requests of accessing origin servers</td>
   </tr>
   <tr>
      <td style="width: 80px; text-align: center;">Port value</td>
      <td>Only the 80, 443, and 8080 ports are supported</td>
      <td>1–65535</td>
   </tr>
</table>


> 
> - After ECDN is activated, if the client request port is different from the service ports opened on the node, the client access request cannot be accelerated by the node.  
> - You can specify the origin-pull port on a node on the ECDN domain name management page.

### What should I do if I fail to connect a domain name in the console?

The common error types and their solutions for connecting domain names are as shown below:

<table style="display:table;" width="100%">
	<thead>
		<tr>
			<th colspan="1" style="text-align: center" width=30%> Error Type </th>
			<th colspan="1" style="text-align: center" width=70%> Error Description and Solution </th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>The corresponding domain name has existed in CDN configuration </td>
			<td>You can add a domain name on the ECDN platform only after confirming that it has been deactivated in and deleted from CDN in and outside Mainland China. </td>
		</tr>
		<tr>
			<td>The acceleration domain name does not have ICP filing </td>
			<td>If your acceleration region includes regions in Mainland China, according to applicable laws and regulations, your domain name must be connected to the ICP domain name filing system.</br>If you only need to ensure the access experience of users outside Mainland China, you can uncheck acceleration regions in Mainland China when adding a domain name. In this way, the domain name does not request ICP filing and auditing. </td>
		</tr>
		<tr>
			<td>The acceleration domain name has existed </td>
			<td>If the domain name has been added under the current account, it does not need to be added again and can be used directly.</br>If your domain name has been connected by another account, you can <a href='https://console.cloud.tencent.com/workorder/category'>submit a ticket</a> to provide the domain name ownership proof so as to apply for the domain name configuration permission. </td>
		</tr>
		<tr>
			<td>Restricted domain name </td>
			<td>The domain names restricted from being added in the system include but not limited to: internal domain names of Tencent or Tencent Cloud, locked domain names, and blacklisted domain names. You can <a href='https://console.cloud.tencent.com/workorder/category'>submit a ticket</a> to apply for the configuration permission of restricted domain names. </td>
		</tr>
		<tr>
			<td>The number of domain names exceeds the upper limit </td>
			<td>The platform allows up to 200 acceleration domain names to be added under each account by default. You can delete configuration of deactivated domain names or apply for increasing the maximum number of domain names. </td>
		</tr>
		<tr>
			<td>The domain name format is invalid </td>
			<td>The system can accelerate only ASCII domain names. Non-ASCII domain names contain invalid characters and therefore cannot be added. </td>
		</tr>
	</tbody>
</table>





