You can add domain names to CDN console for Tencent Cloud CDN services with the following steps:

## Adding domain name

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), click **Domain Management** on the left sidebar, and click **Create Distribution**.
![](https://main.qcloudimg.com/raw/0fbebd8e30610d3e8607a60851946c42.png)
Enter the page for creating domain names to complete the domain name configuration. For information about configuration descriptions, please see [Configuring domain name](#m1). 
![](https://main.qcloudimg.com/raw/863c50ffd5fc1108dfb6696aa73a034d.png)

<span ID ="m1"> </a>
## Configuring domain name

<table >
<thead>
	<tr>
		<th scope="col" colspan = "2"  style="width: 18%;">Configuration Item</th>
		<th scope="col">Description</th>
	</tr>
</thead>
<tbody>
	<tr>
	<td style="text-align: center;" colspan = "2">Domain Name</td>
		<td>You can add domain names in batches. A maximum of 10 domain names can be added by clicking **Add**. Domain name must meet the following conditions: <li>ICP filing for the domain name has been obtained from the MIIT. <br><br>The domain name has never been added to Tencent Cloud CDN before. Currently, wildcard domain names  can also be added, but verification is required. You can upload verification files provided by Tencent Cloud to the root directory of the website, complete verification, and then add wildcard domain names. Pay attention to the following restrictions:
<li>If a wildcard domain name such as *. test.com has already been connected to Tencent Cloud, its sub-domain names cannot be connected to another account. </li>
<li>If the wildcard domain name .test.com has already been connected to your account, wildcard domain names in formats such as .path.test.com cannot be connected to this account.</li>
</td>
	</tr>
	<tr>
	<td style="text-align: center;" colspan = "2">Project</td>
	<td>Select the corresponding project in **Project** to manage the domain name by project. The project is shared by all Tencent Cloud products. You can add a project in <a href = "https://console.cloud.tencent.com/project">Project Management</a> . </td>
	</tr>
	<tr>
	<td style="text-align: center;" colspan="2">Origin Type</td>
		<td>You can select an external origin server or <a href = "https://cloud.tencent.com/product/cos">COS</a> as your origin server. </td>
	</tr>
	<tr>
		<td colspan="1" rowspan="2" style="text-align: center;" >Origin Settings</td>
			<td style="text-align: center; ">External origin server </td>
			<td >If you already have a business server (origin server) that runs stably, you can choose to connect to CDN via your own business server. No change needs to be made to the origin server. You can connect your origin server to CDN via the CDN console and complete DNS configuration to activate the acceleration service. The IP address and domain name of the origin server should meet the following conditions:<br>
<li> If a domain name is entered, it **cannot** be the same as the access domain name (i.e., the connected accelerated domain name). The "DOMAIN NAME:PORT" format is supported, and the port number should be **between 0 and 65535 (inclusive)**.
<li>You can enter multiple IP addresses in the format of "IP:PORT", and the port number should be **between 0 and 65535 (inclusive)**. Origin-pull requests will access the IP addresses in turn.
<li>When there are multiple IP addresses, weight can be configured in the format of IP:PORT:WEIGHT, where PORT can be omitted. In this case, the format is IP::WEIGHT, where WEIGHT ranges from 0 to 100 (for IPv4 addresses only).
<li>The entered IP address cannot be an intranet address. </td>
	</tr>
	<tr>
		<td style="text-align: center; ">COS origin server</td>
		<td>If you want to use <a href = "https://cloud.tencent.com/product/cos">COS</a> to store static content for fast delivery, you can directly add the domain name of COS to CDN. Use one of the following methods to add the domain name to CDN:<br>
<li> If the origin server type is COS, you can enter or select the bucket domain name from the drop-down list.
<li> If there is no bucket, you need to log into the <a href ="https://console.cloud.tencent.com/cos5">COS Console</a> to create one (for instructions, please see <a href = "https://cloud.tencent.com/document/product/436/13309">Creating Buckets</a>). You can also ask your developer account for corresponding bucket access.
<li>After selecting a bucket as the origin server, you can manage its content on the <a href ="https://console.cloud.tencent.com/cos5">COS Console</a>. 
<blockquote class="d-mod-notice">
							<div class="d-mod-title d-notice-title">
								<i class="d-icon-notice"></i>Note:
							</div>
               <p></p>
<ul>
<li> COS V5 is automatically used for connecting a COS origin server domain name to CDN. If you want to use a COS V4 bucket as an origin server, you need to go to the COS V4 console and enable acceleration service for the corresponding bucket. </li>
<li> If your COS V5 bucket is private, you need to first allow the CDN service to access the corresponding COS bucket and then enable origin-pull access. Resources in all private buckets can then be delivered over the CDN public network. Please note this creates a high security risk. </li>
</ul></blockquote>
</td>
	</tr>
</tbody>
</table>



## Configuring the acceleration service

Select the acceleration service type and basic configuration.
![](https://main.qcloudimg.com/raw/f1fd65de90d3c3fd98865e5cb30d6dc4.png)
1. **Business Type** 
   The business type determines the resource platform to be scheduled by the domain name. The acceleration configuration varies by resource platform. Please select a business type based on your business conditions:
	- Static acceleration: Suitable for static resource acceleration scenarios such as ecommerce, websites, and gaming images.
	- Download acceleration: Suitable for scenarios such as game installations, audio/video downloads, and mobile phone firmware package distribution.
	- Streaming VOD acceleration: Suitable for VOD acceleration scenarios.
2. **Basic Configuration**
   CDN provides the Ignore Query String switch, which allows you to control whether to filter parameters after **"?"** in end users' request URLs. You can use this feature for flexible version control or token-based authentication. For more information, please see [Ignore query string configuration](https://cloud.tencent.com/doc/product/228/6291).
3. **Cache expiration configuration**
   Cache expiration configuration refers to a set of expiration rules that CDN cache nodes should comply with when caching your business content. For more information, please see [Cache Expiration Configuration](https://cloud.tencent.com/doc/product/228/6290).

## Completing the connection

Click **Submit** to add the domain name and wait for the domain name configuration to be delivered over the entire network. This usually takes 5 to 10 minutes.
![](https://main.qcloudimg.com/raw/73e56349a7d26444c1e5572bffd0bdbd.png)

>After the connection is successful, CDN will assign you a corresponding CNAME address. CDN service takes effect only after you complete the CNAME configuration. For more information, please see [Configuring CNAME](https://cloud.tencent.com/document/product/228/3121).
