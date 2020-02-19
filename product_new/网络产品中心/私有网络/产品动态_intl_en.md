## December 2019
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="55%">Description</th>
<th width="20%">Related Documents</th>
</tr>
</thead>
<tbody><tr>
<td>Supports display the last modification time in security group rules</td>
<td>The attribute “Last Modification Time” is provided, which will record the last time of creation or modification and facilitate troubleshooting.</td>
<td>—</td>
</tr>
</tbody></table>

## November 2019
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="55%">Description</th>
<th width="20%">Related Documents</th>
</tr>
</thead>
<tbody><tr>
<td>Opens HAVIP to all users</td>
<td>A high-availability virtual IP (HAVIP) is a floating private IP address that supports binding to a server using ARP announcement to update the mapping between the IP address and MAC address. In a high-availability deployment scenario (such as keepalived), this IP address can be switched from the master server to the slave server for disaster recovery of the service.</td>
<td><a href="https://cloud.tencent.com/document/product/215/36691" target="_blank">Use cases</a></td>
</tr>
<tr>
<td>Security groups supported addition of IPv6 rules</td>
<td>By adding security group IPv6 rules, you can enable or disable public or private network access for IPv6 CVMs in a security group.</td>
<td><a href="https://cloud.tencent.com/document/product/215/39790" target="_blank">Adding Security Group Rules</a></td>
</tr>
</tbody></table>

## July 2019
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="55%">Description</th>
<th width="20%">Related Documents</th>
</tr>
</thead>
<tbody><tr>
<td>Supports tags for VPCs</td>
<td>VPCs, subnets, and route tables support resource-level tags, which can help you better manage resource permissions for sub-users and collaborators.</td>
<td>—</td>
</tr>
</tbody></table>

## December 2018
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="55%">Description</th>
<th width="20%">Related Documents</th>
</tr>
</thead>
<tbody><tr>
<td>Releases instance port verification tool</td>
<td>The instance port verification feature can help you check the accessibility of security group ports of CVM instances and quickly locate faults, improving user experience.</td>
<td><a href="https://cloud.tencent.com/document/product/215/38836" target="_blank">Instance Port Verification </a></td>
</tr>
</tbody></table>

## October 2018
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="55%">Description</th>
<th width="20%">Related Documents</th>
</tr>
</thead>
<tbody><tr>
<td>Supports open all common ports in a security group with one-click operation</td>
<td>Enabling ports in one-key operation is applicable to scenarios in which ICMP protocol rules do not need to be set and operations can be completed through ports 22, 3389, ICMP, 80, 443, 20, and 21.</td>
<td><a href="https://cloud.tencent.com/document/product/215/39790" target="_blank">Adding Security Group Rules </a></td>
</tr>
</tbody></table>

## June 2018
<table>
<thead>
<tr>
<th width="25%">Product Update</th>
<th width="55%">Description</th>
<th width="20%">Related Documents</th>
</tr>
</thead>
<tbody><tr>
<td>Supports DHCP option set</td>
<td>The Dynamic Host Configuration Protocol (DHCP) is a LAN network protocol that provides the standard for delivering configurations to TCP/IP network servers. The CVMs in Tencent Cloud VPCs support DHCP. You can configure the two parameters on the VPC details page. These settings will take effect for all CVMs under that VPC.</td>
<td><a href="https://cloud.tencent.com/document/product/215/37564" target="_blank">Modifying DNS Addresses and Domain Names</a></td>
</tr>
<tr>
<td>Releases network probe feature</td>
<td>The Tencent Cloud Network Probe service is used to monitor the quality of VPC network connections, including latency, packet loss rate, and other key metrics. You can quickly locate problems by setting alerts and multi-dimensional monitoring via network probe. You can also create a network probe object in a subnet to monitor the connection quality in real time, so as to improve business stability.</td>
<td><a href="https://cloud.tencent.com/document/product/215/20091" target="_blank">Network Probe</a></td>
</tr>
</tbody></table>

## February 2018
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="55%">Description</th>
<th width="20%">Related Documents</th>
</tr>
</thead>
<tbody><tr>
<td>Supports binding a VPC-based TencentDB to a security group</td>
<td>Security groups can be bound with TencentDB and other relevant products. You can bind a security group with TencentDB instances. A security group is a stateful virtual firewall that provides data packet filtering. It can be used to set network access control for instances such as CVMs and ENIs, and also supports network access control for TencentDB instances in VPCs. Therefore, a security group can effectively enhance the security of TencentDB.</td>
<td><a href="https://cloud.tencent.com/document/product/213/39751" target="_blank">Binding instances with security groups</a></td>
</tr>
<tr>
<td>VPCs and security groups supports operation audit</td>
<td>VPCs and security groups support CloudAudit, which can obtain the historical records of API calling under your Tencent Cloud account, including API calling via the Tencent Cloud console, Tencent Cloud SDK, command line tool, and other Tencent Cloud services. This means that any deployment behavior on Tencent Cloud is monitored, and you can find out the sub-users and collaborators who use Tencent Cloud APIs, the source IP addresses from which the APIs are called, and when they are called.</td>
<td>—</td>
</tr>
</tbody></table>

## June 2017
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="55%">Description</th>
<th width="20%">Related Documents</th>
</tr>
</thead>
<tbody><tr>
<td>Supports access control for security groups</td>
<td>We provide the feature of managing user permissions in security groups to make your service more secure.</td>
<td><a href="https://cloud.tencent.com/document/product/215/39265" target="_blank">Access Control Overview</a></td>
</tr>
<tr>
<td>Security groups support parameter templates</td>
<td>A parameter template is a set of parameters. You can save IP addresses and protocol ports as a template so that you can directly import the template when adding security group rules. Parameter templates, if properly used, can enhance your efficiency in using security groups.</td>
<td><a href="https://cloud.tencent.com/document/product/215/20090" target="_blank">Managing Parameter Templates</a></td>
</tr>
<tr>
<td>Upgrades monitoring feature</td>
<td>The system supports the visualized alarm and monitoring data of multiple key metrics and can obtain data through APIs to ensure steady and smooth operation of your services.</td>
<td>—</td>
</tr>
</tbody></table>

## May 2017
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="55%">Description</th>
<th width="20%">Related Documents</th>
</tr>
</thead>
<tbody><tr>
<td>Security groups supported access control</td>
<td>We provide the feature of managing user permissions in security groups to make your service more secure.</td>
<td><a href="https://cloud.tencent.com/document/product/215/39265" target="_blank">Access Control Overview</a></td>
</tr>
</tbody></table>

## January 2017
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="55%">Description</th>
<th width="20%">Related Documents</th>
</tr>
</thead>
<tbody><tr>
<td>Supports broadcast and multicast</td>
<td>Broadcast and multicast are one-to-many communication, which can help enterprises save network bandwidth and reduce network load through efficient point-to-multipoint data transmission.<li>Broadcast: Tencent Cloud supports broadcast in the dimension of subnets.</li><li>Multicast: Tencent Cloud supports multicast in the dimension of VPC.</li></td>
<td><a href="https://cloud.tencent.com/document/product/215/36526" target="_blank">Enabling or Disabling Broadcast and Multicast</a></td>
</tr>
</tbody></table>

## October 2016
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="55%">Description</th>
<th width="20%">Related Documents</th>
</tr>
</thead>
<tbody><tr>
<td>Supports ENIs</td>
<td>The multi-ENI hot swapping service for CVMs helps you achieve isolation among three networks and deployment of high-availability services.</td>
<td><a href="https://cloud.tencent.com/document/product/215/20127" target="_blank">Managing ENIs</a></td>
</tr>
</tbody></table>

## December 2015
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="55%">Description</th>
<th width="20%">Related Documents</th>
</tr>
</thead>
<tbody><tr>
<td>Supports network topology maps</td>
<td>A network topology map can clearly display your network architecture to help you easily tackle problems in network management.</td>
<td>—</td>
</tr>
</tbody></table>

## May 2015
<table>
<thead>
<tr>
<th width="25%">Update</th>
<th width="55%">Description</th>
<th width="20%">Related Documents</th>
</tr>
</thead>
<tbody><tr>
<td>Launches VPC</td>
<td>A Virtual Private Cloud (VPC) is an independent isolated network space that supports software-defined networks, supports connection with your IDCs via VPN connection or Direct Connect, and supports flexible deployment of hybrid cloud.</td>
<td><a href="https://cloud.tencent.com/document/product/215" target="_blank">VPC</a></td>
</tr>
</tbody></table>
