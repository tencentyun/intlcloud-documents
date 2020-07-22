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
<td>The layer-7 HTTPS listeners support the QUIC protocol to establish a QUIC connection between clients and CLB instances.</td>
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
<td>Security groups support allowing traffic by default</td>
<td>After "Allow Traffic by Default in Security Group" is enabled, you don't need to open the client IP and service ports to the Internet in the backend CVM security group. Access traffic from a CLB instance only needs to pass through the CLB security group, while the backend CVM instance allows the CLB traffic by default and doesn't need to open the port.</td>
<td>May 27, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/14733#.E5.BC.80.E5.90.AF.E5.AE.89.E5.85.A8.E7.BB.84.E9.BB.98.E8.AE.A4.E6.94.BE.E9.80.9A">Enabling "Allow Traffic by Default in Security Group"</a></td>
</tr>
<tr>
<tr>
<td>The default domain name policy for layer-7 listeners is updated</td>
<td>The default domain name is changed from “optional” to “required” for layer-7 listeners. Each listener can and must have only one default domain name configured.</td>
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
<td>The feature of storing CLB access logs in COS is deactivated</td>
<td>You cannot store new access logs to COS after May 15, 2020 00:00:00, (or after April 26, 2020 00:00:00 in the Guangzhou region). The feature of storing access logs in COS will be officially deactivated in all regions on June 30, 2020 00:00:00. To use the updated feature, see<a href="https://intl.cloud.tencent.com/document/product/214/35063">Storing Access Logs in CLS</a>.</td>
<td>April 21, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/35906">Announcement on the Deactivation of the Feature of Storing CLB Access Logs in COS</a></td>
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
<td>CLB supports adding to a bandwidth package</td>
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
<td>IPv6 is supported </td>
<td><li>IPv6 CLB supports binding to an IPv6 address of a CVM instance and provides an IPv6 VIP address.</li><li>A IPv6 CLB instance is a load balancer using the IPv6 single stack technology, which can collaborate with IPv4 CLB to implement IPv6/IPv4 dual-stack communication.</li></td>
<td>October 17, 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/34555">Creating IPv6 CLB Instances</a></td>
</tr>
<tr>
<td>Access logs can be stored to CLS</td>
<td>CLB supports storing the layer-7 access logs in CLS with online search supported at a 1-minute granularity.</li></td>
<td>October 15, 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/35063">Storing Access Logs in CLS</a></td>
</tr>
<tr>
<td>Private network CLB supports redirection</td>
<td>Private network layer-7 CLB supports configuring redirection.</li></td>
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
<td>CLB supports binding ENIs that can forward traffic to the private IPs corresponding to multiple ENIs on the same CVM instance.</td>
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
<td>Anycast CLB supports global dynamic acceleration. The CLB VIP is published in multiple regions around the world. The client connects to the nearest POP and forwards access traffic to a CVM instance through high-speed internet of Tencent Cloud IDC.</td>
<td>November 27, 2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/32426">Creating an Anycast Instance</a></td>
</tr>
</tr>
</thead>
<tbody><tr>
<td>IPv6 NAT64 is supported</td>
<td>An IPv6 NAT64 CLB instance can be created. The CLB VIP is an IPv6 public IP address, which will forward requests from IPv6 clients to the backend IPv4 CVM instance, so that the real server can access IPv6 in a matter of seconds without any modification required.</td>
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
<td>The TCP SSL protocol is supported</td>
<td>CLB supports the TCP SSL protocol, which is suitable for scenarios where ultra-high performance is required and large-scale TLS offload is performed.</td>
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
<td>CLB supports SNI multi-domain name certificate, so you can configure different certificates for multiple domain names under one listener as needed.</td>
<td>August 21, 2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/19048">SNI Support for Binding Multiple Certificates to a CLB Instance</a></td>
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
<td>The public network CLB supports binding security groups to control and isolate inbound and outbound traffic.</td>
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
<td>CLB supports the layer-7 custom configuration</td>
<td>CLB supports configuring the layer-7 parameters.</td>
<td>March 27, 2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/32427">Custom Configurations of CLB Instances</a></td>
</tr>
<tr>
<td>Access logs can be stored to COS</td>
<td>Public network layer-7 CLB supports storing access logs in COS for easier analysis and troubleshooting.</td>
<td>March 2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/10329">Storing Request Logs to COS
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
<td>You can select and bind real servers in different VPCs and regions.</td>
<td>September 2017</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/12014">CLB Instance Cross-Region Binding</a></td>
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
<td>Cloud Access Management (CAM) is used to manage the access permissions for the resources under Tencent Cloud accounts. You can use the identity management and policy management features to control which sub-accounts can access CLB resources.</td>
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
<td>You can configure redirection on layer-7 HTTP/HTTPS listeners, such as redirection from HTTP to HTTPS.</td>
<td>April 8, 2017</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/8839">Configuring Layer-7 Redirection</a></td>
</tr>
<tr>
<td>Weighted least-connection scheduling is supported for round robin algorithms</td>
<td>The weighted least-connection scheduling algorithm schedules requests based on the processing capabilities and weights of real servers to make the load more balanced.</td>
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
<td>Layer-7 domain name and URL forwarding is supported</td>
<td>CLB supports layer-7 HTTP/HTTPS protocols to provide flexible forwarding capabilities based on domain names and URL paths.</td>
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
<td>Layer-7 HTTP and HTTPS protocols are application layer protocols. Layer-7 listeners support session persistence by cookie and health check by HTTP return code.</td>
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
<td>A Virtual Private Cloud (VPC) is a logically isolated custom network space in Tencent Cloud. CLB instances in VPC can help you deploy and isolate services flexibly.</td>
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
<td>CLB is released.</td>
<td>CLB provides secure and fast traffic distribution services. It can seamlessly allocate the load balancing capacity required for application traffic, and automatically distribute application access traffic among CVM instances in the cloud, enhancing fault tolerance for applications.</td>
<td>December 2014</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214">Cloud Load Balancer</a></td>
</tr>
</tbody></table>
