## May 2021
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
 <tr>
<td>Supports health check logs</td> 
<td>CLB supports storing layer-4 and layer-7 health check logs in CLS, reporting logs every minute, and querying logs with multiple rules.</td> 
<td>May 21, 2021</td> 
<td>Configuring Health Check Logs</a></td> 
</tbody>
</table>


## January 2021
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
 <tr>
<td>Supports binding CLB instances with SCF functions</td> 
<td>CLB instances support binding with SCF functions, enabling more convenient and cost-effective public network access for SCF.</td> 
<td>January 28, 2021</td> 
<td><a href="https://intl.cloud.tencent.com/document/product/214/39790">Binding with SCF</a></td> 
</tbody>
</table>

## December 2020
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
 <tr>
<td>Supports static single-line IP CLB instances</td> 
<td>In some districts, the ISP of CLB instances can be China Mobile, China Unicom, or China Telecom, and the bandwidth price is lower than the general BGP IP price.</td> 
<td>December 3, 2020</td> 
<td><a href="https://intl.cloud.tencent.com/document/product/214/524">Overview</a></td> 
</tr>
 <tr>
 <td>Optimizes health check</td>
  <td>TCP listeners support HTTP health checks and UDP listeners support checking ports.</td>
  <td>December 14, 2020</td>
  <td><a href="https://intl.cloud.tencent.com/document/product/214/6097">Health Check</a></td>
  </tr>
</tbody>
</table>

## September 2020
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
 <tr>
<td>Fully supports custom layer-7 configurations on CLB instances</td> 
<td>CLB fully supports setting the layer-7 configuration parameters of CLB instances.</td> 
<td>September 22, 2020</td> 
<td><a href="https://intl.cloud.tencent.com/document/product/214/32427">Custom Configurations of CLB Instances</a></td> 
</tr>
<tr>
<td>CLB cross-region binding 2.0</td>
<td>CLB supports binding CVM instances across regions through CCN, allowing you to select CVM instances of different regions and bind to them across VPCs or regions.</td>
<td>September 10, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/38441">Cross-region Binding v2.0 (New)
</a></td>
</tr>
<tr>
<td>Supports hybrid cloud deployment</td>
<td>CLB instances can be directly bound to IPs of local IDCs.</td>
<td>September 10, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/38442">Hybrid Cloud Deployment
</a></td>
</tr>
</tbody>
</table>


## June 2020
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Supports the QUIC protocol</td>
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
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Security groups can be bound to private network CLB instances</td>
<td>Security groups can be bound to private network CLB instances to isolate private network traffic.</td>
<td>May 27, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/14733">CLB Security Group Configuration
</a></td>
</tr>
<tr>
<td>Supports "Allow Traffic by Default" on security groups</td>
<td>After "Allow Traffic by Default" is enabled, client IPs and service ports to the Internet do not need to be opened in the backend CVM security group. Access traffic from a CLB instance only needs to pass through the CLB security group, while the backend CVM allows CLB traffic by default and does not need to open any ports.</td>
<td>May 27, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/14733#open-security-group">CLB Security Group Configuration</a></td>
</tr>
<tr>
<td>Updates the default domain name policy for layer-7 listeners</td>
<td>The default domain name is changed from optional to required for layer-7 listeners. Each listener must and can only have one default domain name configured.</td>
<td>May 15, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/9032">Layer-7 Domain Name Forwarding and URL Rules
</a></td>
</tr>
</tbody></table>

## April 2020
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Deactivates the feature for storing CLB access logs in COS</td>
<td>You can no longer store new access logs in COS after May 15, 2020 00:00:00, (or after April 26, 2020 00:00:00 in the Guangzhou region). The feature has been officially deactivated in all regions since June 30, 2020 00:00:00. To use the updated feature, please see <a href="https://intl.cloud.tencent.com/document/product/214/35063">Storing Access Logs in CLS</a>.</td>
<td>April 21, 2020</td>
<td>-</td>
</tr>
</tbody></table>

## November 2019
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Shared bandwidth package is supported for CLB instances</td>
<td>IP bandwidth package is supported for CLB instances of bill-by-IP accounts.</td>
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
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Supports IPv6</td>
<td><li>IPv6 CLB can be bound to the IPv6 address of a CVM instance and provides an IPv6 VIP address.</li><li>A CLB instance using the IPv6 single-stack technology can collaborate with IPv4 CLB to implement IPv6/IPv4 dual-stack communication.</li></td>
<td>October 17, 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/34555">Creating IPv6 CLB Instance</a></td>
</tr>
<tr>
<td>Access logs can be stored in CLS</td>
<td>CLB supports storing layer-7 access logs in CLS with online search at 1-minute granularity.</li></td>
<td>October 15, 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/35063">Storing Access Logs in CLS</a></td>
</tr>
<tr>
<td>Private network CLB instances support redirection</td>
<td>Private network layer-7 CLB instances support redirection configurations.</li></td>
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
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Supports tag authentication</td>
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
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Supports binding ENIs</td>
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
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Supports Anycast CLB</td>
<td>Anycast CLB supports dynamic acceleration in multiple regions. The CLB VIP is published in multiple regions, and the client connects to the nearest POP, the traffic can be forwarded to a CVM instance through the high-speed Internet of Tencent Cloud IDC.</td>
<td>November 27, 2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/32426">Creating an Anycast Instance</a></td>
</tr>
</tr>
</thead>
<tbody><tr>
<td>Supports IPv6 NAT64</td>
<td>An IPv6 NAT64 CLB instance can be created. The CLB VIP is an IPv6 public IP address, which will forward requests from IPv6 clients to the backend IPv4 CVM instance, so that the real server can access IPv6 within seconds with no modification required.</td>
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
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Supports TCP SSL protocol</td>
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
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Supports SNI</td>
<td>CLB supports multi-domain SNI certificate to configure different certificates for domain names under one listener.</td>
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
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Supports security groups</td>
<td>Public network CLB can be bound with security groups to control and isolate inbound and outbound traffic.</td>
<td>April 15, 2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/14733">CLB Security Group Configuration</a></td>
</tr>
</tbody></table>

## March 2018
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Supports custom layer-7 configurations on CLB instances</td>
<td>CLB supports setting the layer-7 configuration parameters of CLB instances.</td>
<td>March 27, 2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/32427">Custom Configurations of CLB Instances</a></td>
</tr>
<tr>
<td>Access logs can be stored in COS</td>
<td>Public network layer-7 CLB supports storing access logs in COS to facilitate analysis and troubleshooting.</td>
<td>March 2018</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/10329">Storing Access Logs in COS
</a></td>
</tr>
</tbody></table>

## September 2017
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Supports cross-region binding</td>
<td>You can select and bind real servers across VPCs and regions.</td>
<td>September 2017</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/38441">CLB Instance Cross-Region Binding</a></td>
</tr>
</tbody></table>

## June 2017
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Supports CAM authentication</td>
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
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Supports layer-7 redirection</td>
<td>You can configure redirection on layer-7 HTTP/HTTPS listeners, such as redirection from HTTP to HTTPS.</td>
<td>April 8, 2017</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/8839">Configuring Layer-7 Redirection</a></td>
</tr>
<tr>
<td>Weighted least-connection scheduling is supported for round robin algorithms</td>
<td>The weighted least-connection scheduling is based on the processing capabilities and weights of real servers to balance loads.</td>
<td>April 8, 2017</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/6153">Load Balancing Methods</a></td>
</tr>
</tbody></table>


## November 2016
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Supports layer-7 domain name and URL forwarding</td>
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
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Supports layer-7 HTTP and HTTPS protocols</td>
<td>Layer-7 HTTP and HTTPS protocols are application layer protocols. Layer-7 listeners support session persistence based on cookies and health check based on HTTP return codes.</td>
<td>April 2016</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/6151">CLB Listeners - Overview</a></td>
</tr>
</tbody></table>

## April 2015
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="40%">Description</th>
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Supports VPC</td>
<td>A Virtual Private Cloud (VPC) is a custom logically isolated network space in Tencent Cloud. CLB instances in VPC can help you deploy and isolate services flexibly.</td>
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
<th width=15%>Release Date</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Releases Cloud Load Balancer</td>
<td>CLB provides secure and fast traffic distribution services. It can seamlessly allocate the load balancing capacity required for application traffic, and automatically distribute application access traffic among CVM instances in the cloud to enhance fault tolerance.</td>
<td>December 2014</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214">Cloud Load Balancer</a></td>
</tr>
</tbody></table>
