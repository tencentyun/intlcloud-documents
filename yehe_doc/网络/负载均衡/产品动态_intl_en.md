## June 2020
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>CLB supports the QUIC protocol</td>
<td>Layer-7 HTTPS listeners support the QUIC protocol to establish a QUIC connection between clients and CLB instances.</td>
<td>June 29, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/37353">Using QUIC Protocol on CLB
</a></td>
</tbody>
</table>

## May 2020
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Security groups can be bound to private network CLB instances</td>
<td>Security groups can be bound to private network CLB instances to isolate private network traffic.</td>
<td>May 27, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/14733">Configuring a CLB Security Group
</a></td>
</tr>
<tr>
<td>“Allow by Default” is enabled in security group</td>
<td>After “Allow by Default” is enabled, client IP and service ports to the Internet do not need to be opened in the backend CVM security group. Access traffic from a CLB instance only needs to pass through the CLB security group, while the backend CVM allows CLB traffic by default and does not need to open any ports.</td>
<td>May 27, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/14733#.E5.BC.80.E5.90.AF.E5.AE.89.E5.85.A8.E7.BB.84.E9.BB.98.E8.AE.A4.E6.94.BE.E9.80.9A">Enabling “Allow by Default” in security group</a></td>
</tr>
<tr>
<tr>
<td>The default domain name policy for Layer-7 listeners is updated</td>
<td>The default domain name is changed from optional to required for Layer-7 listeners. Each listener must and can only have one default domain name configured.</td>
<td>May 15, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/9032">Default Domain Name Policy for Forwarded Domain Name
</a></td>
</tr>
</tbody></table>

## April 2020
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>The feature for storing CLB access logs in COS is deactivated</td>
<td>You can no longer store new access logs in COS after May 15, 2020 00:00:00, (or after April 26, 2020 00:00:00 in the Guangzhou region). The feature will be officially deactivated in all regions on June 30, 2020 00:00:00. To use the updated feature, see<a href="https://intl.cloud.tencent.com/document/product/214/35063">Storing Access Logs in CLS</a>.</td>
<td>April 21, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/35906">Announcement on the Deactivation of the Feature for Storing CLB Access Logs in COS</a></td>
</tr>
</tbody></table>

## November 2019
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>CLB can be added to a bandwidth package</td>
<td>A CLB instance under the bill-by-IP account can be added to the IP bandwidth package.</td>
<td>November 20, 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/684/15245">Bandwidth Package - Product Overview</a></td>
</tr>
</tbody></table>

## October 2019
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>IPv6 is supported</td>
<td><li>IPv6 CLB can be bound to the IPv6 address of a CVM instance and provides an IPv6 VIP address.</li><li>A CLB instance using the IPv6 single-stack technology can collaborate with IPv4 CLB to implement IPv6/IPv4 dual-stack communication.</li></td>
<td>October 17, 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/34555">Creating IPv6 CLB Instances</a></td>
</tr>
<tr>
<td>Access logs can be stored in CLS</td>
<td>CLB supports storing Layer-7 access logs in CLS with online search at 1-minute granularity.</li></td>
<td>October 15, 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/35063">Storing Access Logs in CLS</a></td>
</tr>
<tr>
<td>Private network CLB supports redirection</td>
<td>Private network Layer-7 CLB supports configuring redirection.</li></td>
<td>October 15, 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/8839">Configuring Layer-7 Redirection</a></td>
</tr>
</tbody></table>

## May 2019
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Tag authentication is supported</td>
<td>CLB supports tag-based permission management.</td>
<td>May 7, 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/651/13334">Tag - Product Overview</a></td>
</tr>
</tbody></table>

## April 2019
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>ENIs can be bound</td>
<td>CLB can be bound with ENIs to forward traffic to the corresponding private IPs of ENIs on the same CVM instance.</td>
<td>April 30, 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/32520">Binding an ENI</a></td>
</tr>
</tbody></table>

## November 2018
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Anycast CLB is supported</td>
<td>Anycast CLB supports cross-region dynamic acceleration. CLB VIP is published in multiple regions. The client connects to the nearest POP and forwards traffic to a CVM instance through the high-speed internet of Tencent Cloud IDC.</td>
<td>November 27, 2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/32426">Creating an Anycast Instance</a></td>
</tr>
</tr>
</thead>
<tbody><tr>
<td>IPv6 NAT64 is supported</td>
<td>An IPv6 NAT64 CLB instance can be created. CLB VIP is an IPv6 public IP address, which will forward requests from IPv6 clients to the backend IPv4 CVM instance so that the real server can access IPv6 within seconds with no modification required.</td>
<td>November 15, 2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/34556">Creating IPv6 NAT64 CLB Instances</a></td>
</tr>
</tbody></table>

## October 2018
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>TCP SSL protocol is supported</td>
<td>CLB supports the TCP SSL protocol, which is suitable for scenarios that require ultra-high performance and large-scale TLS offloading.</td>
<td>October 12, 2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/32519">Configuring a TCP SSL Listener
</a></td>
</tr>
</tbody></table>

## August 2018
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>SNI is supported</td>
<td>CLB supports multi-domain SNI certificate to configure different certificates for domain names under one listener.</td>
<td>August 21, 2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/19048">Multi-domain SNI Certificate Supported by CLB</a></td>
</tr>
</tbody></table>

## April 2018
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Security group is supported</td>
<td>Public network CLB can be bound with security groups to control and isolate inbound and outbound traffic.</td>
<td>April 15, 2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/14733">Configuring a CLB Security Group</a></td>
</tr>
</tbody></table>

## March 2018
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>CLB supports Layer-7 custom configuration</td>
<td>CLB supports configuring Layer-7 parameters.</td>
<td>March 27, 2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/32427">Layer-7 Custom Configurations of CLB Instances</a></td>
</tr>
<tr>
<td>Access logs can be stored in COS</td>
<td>Public network Layer-7 CLB supports storing access logs in COS to facilitate analysis and troubleshooting.</td>
<td>March 2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/10329">Storing Request Logs in COS
</a></td>
</tr>
</tbody></table>

## September 2017
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Cross-region binding is supported</td>
<td>You can select and bind real servers across VPCs and regions.</td>
<td>September 2017</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/12014">Cross-Region Binding of CLB Instances</a></td>
</tr>
</tbody></table>

## June 2017
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>CAM authentication is supported</td>
<td>Cloud Access Management (CAM) is used to manage access permissions for resources under Tencent Cloud accounts. You can use identity management and policy management to control which sub-accounts can access CLB resources.</td>
<td>June 2017</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/9777">Cloud Access Management - Overview</a></td>
</tr>
</tbody></table>

## April 2017
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Layer-7 redirection is supported</td>
<td>You can configure redirection on Layer-7 HTTP/HTTPS listeners, such as redirection from HTTP to HTTPS.</td>
<td>April 8, 2017</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/8839">Configuring Layer-7 Redirection</a></td>
</tr>
<tr>
<td>Weighted least-connection scheduling is supported for round robin algorithms</td>
<td>The weighted least-connection scheduling is based on the processing capabilities and weights of real servers to balance loads.</td>
<td>April 8, 2017</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/6153">Weighted Least-Connection Scheduling</a></td>
</tr>
</tbody></table>

## November 2016
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Layer-7 domain name and URL forwarding are supported</td>
<td>CLB supports Layer-7 HTTP/HTTPS protocols to provide flexible forwarding capabilities based on domain names and URL paths.</td>
<td>November 2016</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/9032">Layer-7 Domain Name Forwarding and URL Rules</a></td>
</tr>
</tbody></table>

## April 2016
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Layer-7 HTTP and HTTPS protocols are supported</td>
<td>Layer-7 HTTP and HTTPS protocols are application layer protocols. Layer-7 listeners support session persistence based on cookies and health check based on HTTP return codes.</td>
<td>April 2016 </td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/6151">Layer-7 Listener</a></td>
</tr>
</tbody></table>

## April 2015
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>VPC is supported</td>
<td>A Virtual Private Cloud (VPC) is a logically isolated network space in Tencent Cloud. CLB instances in VPC can help you deploy and isolate services flexibly.</td>
<td>April 2015</td>
<td><a href="https://intl.cloud.tencent.com/document/product/215">Virtual Private Cloud</a></td>
</tr>
</tbody></table>

## December 2014
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>CLB has been released</td>
<td>CLB provides secure and fast traffic distribution services. It can seamlessly allocate the load balancing capacity required for application traffic, and automatically distribute application access traffic among CVM instances in the cloud to enhance fault tolerance.</td>
<td>December 2014</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214">Cloud Load Balancer</a></td>
</tr>
</tbody></table>
