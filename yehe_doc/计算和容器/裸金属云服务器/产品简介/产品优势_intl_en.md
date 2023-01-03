CBM is more efficient than self-built IDCs in setting up a dedicated cloud cluster. It comes with Tencent Cloud's public cloud cross-region IDC private network interconnection, VPC, CLB, NAT Gateway, Ops, monitoring, and security protection capabilities. CBM boasts strong computing capabilities without performance loss and security isolation of physical machines, perfectly meeting your requirements for enterprise data security, regulatory business security, and reliability.

CBM has the following strengths compared to managed self-built IDCs:
<table>
<tr>
<th>Comparison Item</th>
<th>CBM</th>
<th>Managed Self-Built IDC</th>
</tr>
<tr>
	<th>Elasticity</th>
	<td>
	Elastic scalability and agile deployment.
	<ul class="params">
	<li>Based on the proprietary elastic bare metal architecture, CBM supports physical machine instance creation in minutes and out-of-the-box and quick deployment.</li>
	<li>Cloud disks and ENIs can be mounted to the new-gen models, and disks can be configured to allow for flexible capacity expansion.</li>
	<li>Thanks to the Tencent Cloud resource pool, you can quickly purchase dozens of physical machines to expand your cluster during peak hours.</li>
	</ul>
</td>
<td>
	Poor elasticity and flexibility.
	<ul class="params">
	<li>Configuration upgrade may disqualify you from the vendor's maintenance service.</li>
	<li>You need to stock up for temporary expansion needs and bear performance surplus and depreciation during off-peak hours.</li>
	</ul>
</td>
</tr>
<tr>
	<th>Ease of use</th>
	<td>
	Simple operations and flexible Ops.
	<ul class="params">
	<li>You can disable, enable, restart, or reinstall a server online in the console or through TencentCloud API. You can also view the server status out of the band through the VNC feature.</li>
	<li>It is compatible with public cloud image systems and provides various images for flexible deployment.</li>
	</ul>
	</td>
	<td>
	Server operations require assistance from IDC on-site engineers, which is troublesome and time-consuming.
	</td>
</tr>
<tr>
	<th>Comprehensiveness</th>
	<td>
	It is integrated with various types of Tencent Cloud services.
	<ul class="params">
	<li>Tencent Cloud IDCs in different regions are interconnected over the private network of the high-speed IDC internet.</li>
	<li>It provides VPC, CLB, NAT Gateway, and other Tencent Cloud services.</li>
	<li>It provides network resources, TencentCloud API, and virtualization.</li>
	</ul>
	</td>
	<td>
	The costs of self-built IDCs are high.
	<ul class="params">
	<li>Private network interconnection requires costly leased lines.</li>
	<li>You need to set up load balancers and NAT gateways on your own.</li>
	</ul>
	</td>
</tr>
<tr>
	<th>Security</th>
	<td>
	All-round and professional protection.
	<ul class="params">
	<li>The VPC allows you to decide the IP range, whether to open a server, and whether to make an instance private. This ensures the private ownership and security of your nodes.</li>
	<li>It provides basic server and security protection measures such as trojan detection, brute force protection, vulnerability scan, WAF, and login security. These free services form a solid line of defense for your business.</li>
	<li>It provides up to 10 Gbps DDoS protection free of charge, monitors network traffic in real time, cleanses attack traffic as soon as it is identified, and enables protection within seconds for public IPs in Tencent Cloud.</li>
	</ul>
	</td>
	<td>
	It is prone to hacker attacks and requires additional security protection services.
	</td>
</tr>
<tr>
	<th>Ops</th>
	<td>
	24/7 Ops service.
	<ul class="params">
	<li>To quickly recover from hardware failures, Tencent Cloud offers a dedicated hardware pool in the IDC. Failed components will be replaced after the diagnosis by on-site professional engineers.</li>
	<li>Tencent Cloud has a team of expert network engineers who can handle network failures due to ENI or switch issues.</li>
	</ul>
	</td>
	<td>
	No expert-level maintenance is available, and network issues need to be addressed by yourself after the maintenance expires.
	</td>
</tr>
<tr>
	<th>Cost effectiveness</th>
	<td>
	On-demand purchase and pay-as-you-go billing.
	<ul class="params">
	<li>CBM supports second-level pay-as-you-go billing and on-demand purchase, reducing costs by eliminating one-time investments.</li>
	<li>It provides different configurations, such as Standard, High I/O, Big Data, and heterogeneous GPU instances, which can be purchased as needed to reduce resource waste.</li>
	</ul>
	</td>
	<td>
	High rental and Ops costs.
	<ul class="params">
	<li>You need to prepare a large number of components or purchase the maintenance or on-site services of the vendor or IDC to quickly handle hardware failures.</li>
	<li>You need to purchase many servers at a time, which are costly and tend to depreciate.</li>
	</ul>
	</td>
</tr>
</table>


<style>
.params{margin-bottom:0px !important}
</style>
