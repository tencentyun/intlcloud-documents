### How do I connect a domain name to the ECDN acceleration platform?



You can connect a domain name to the ECDN acceleration platform in the following three steps:

1. Add an acceleration domain name configuration in the console.

2. Set the `hosts` file to verify whether the configuration takes effect.

3. Configure the domain name CNAME resolution. Then, the service will work.



For detailed directions, please see [Domain Name Connection](https://intl.cloud.tencent.com/document/product/570/10361).



### Should I obtain an ICP filing for services in Mainland China for a domain name connected to ECDN?

Whether the system checks the ICP filing status depends on your selected acceleration region:

- If the acceleration region includes regions in Mainland China, according to applicable laws and regulations, an ICP filing for services in Mainland China should have been obtained from the MIIT for the domain name before connection.

- If the acceleration region includes regions only outside Mainland China (including Hong Kong (China), Macao (China), and Taiwan (China)), your domain name does not need ICP filing.



### Does ECDN support connecting wildcard domain names?



ECDN supports acceleration for wildcard domain names.



### What origin-pull methods are supported by ECDN?



<table style=""display:table;"" width=""80%"">

<thead>

<tr>

<th colspan=""1"" style=""text-align: center"" width=15%> Origin-pull Method </th>

<th colspan=""1"" style=""text-align: center"" width=70%> Description </th>

</tr>

</thead>

<tbody>

<tr>

<td style=""text-align: center"">Optimal route selection origin-pull </td>

<td>It is the default origin-pull policy.</br>The best-performing node is selected for origin-pull based on the platform's detection result. </td>

</tr>

<tr>

<td style=""text-align: center"">Weighted origin-pull </td>

<td>Origin-pull requests are proportionally scheduled to origin servers based on their weights. </td>

</tr>

<tr>

<td style=""text-align: center"">Primary/secondary origin-pull </td>

<td>When the primary origin server is normal, it will be used for origin-pull. Only when it is exceptional will the secondary origin server be used. </td>

</tr>

</tbody>

</table>







<span id="port"></span>



### What differences are there between an acceleration port (or access port) and origin-pull port?


They have the following differences when CDN or ECDN is used:
<table>
   <tr>
      <th style=""width: 80px; text-align: center;"">Port Type</th>
      <th style=""width: 300px; text-align: center;"">Acceleration Port</th>
      <th style=""width: 300px; text-align: center;"">Origin-Pull Port</th>
   </tr>
   <tr>
      <td style=""width: 80px; text-align: center;"">Port difference</td>
      <td style=""width: 300px; text-align: left;"">It is the CDN/ECDN service port, which is also the port for client or user requests to access edge servers</td>
      <td style=""width: 300px; text-align: left;"">It is the origin server service port, which is also the port for CDN/ECDN node requests to access origin servers</td>
   </tr>
   <tr>
      <td style=""width: 80px; text-align: center;"">Port number</td>
      <td>Only ports 80, 443, and 8080 are supported</td>
      <td>1–65535</td>
   </tr>
</table>

>!
>- After ECDN is activated, if the client request port is different from the service ports opened on the node, client access requests cannot be accelerated by the node. 
>- You can specify the origin-pull port on a node on the ECDN domain management page.


### What should I do if domain name connection failed in the console?



Common errors during connecting domain names and their solutions are as follows:



<table style=""display:table;"" width=""100%"">

<thead>

<tr>

<th colspan=""1"" style=""text-align: center"" width=30%> Error Type </th>

<th colspan=""1"" style=""text-align: center"" width=70%> Error Description and Solution </th>

</tr>

</thead>

<tbody>

<tr>

<td>The corresponding domain name already exists in CDN configuration </td>

<td>You can add a domain name on the ECDN platform only after confirming that it has been deactivated in and deleted from Mainland China CDN and Overseas CDN. </td>

</tr>

<tr>

<td>The acceleration domain name has no ICP filing </td>

<td>If your acceleration region includes regions in Mainland China, according to applicable laws and regulations, your domain name must be connected to the domain name ICP filing system of MIIT.</br>If you only need to ensure the access experience of users outside Mainland China, you can uncheck acceleration regions in Mainland China when adding the domain name. In this case, the domain name does not need an ICP filing for auditing. </td>

</tr>

<tr>

<td>The acceleration domain name already exists </td>

<td>If the domain name has been added under the current account, it does not need to be added again and can be used directly.</br>If your domain name has been connected by another account, you can <a href='https://console.cloud.tencent.com/workorder/category'>submit a ticket</a> to provide your domain name ownership proof and reclaim the domain name configuration permission. </td>

</tr>

<tr>

<td>The domain name is restricted </td>

<td>The domain names restricted from being added in the system include but not limited to internal domain names of Tencent or Tencent Cloud and locked or blocked domain names. You can <a href='https://console.cloud.tencent.com/workorder/category'>submit a ticket</a> to apply for the configuration permission for restricted domain names. </td>

</tr>

<tr>

<td>The number of domain names exceeds the upper limit </td>

<td>The platform allows to add up to 200 acceleration domain names under one account by default. You can delete configurations of deactivated domain names or apply for increasing the maximum number of domain names. </td>

</tr>

<tr>

<td>The domain name format is invalid </td>

<td>The system can accelerate only ASCII domain names. Non-ASCII domain names contain invalid characters and therefore cannot be added. </td>

</tr>

</tbody>

</table>
