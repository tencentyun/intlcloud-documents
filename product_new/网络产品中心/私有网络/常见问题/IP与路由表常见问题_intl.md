### 1. What IP address ranges can be used in VPCs and subnets?
- VPC supports private IPs within three network segments: `10.a.0.0/8` (a ranges from 0 to 255), `172.b.0.0/16` (b ranges from 0 to 31), and `192.168.0.0/16`. CIDR of VPC can be the above three network segments, or a part of a network segment.
- The number of IPs contained in a network block =` 2^(32-mask)`. So the `10.1.0.0/16` network block may contain up to 65,536 IP addresses.

### 2. What is CIDR, and what should be paid attention to when assigning a CIDR for a VPC?
CIDR (Classless Inter-Domain Routing) is a user-specified independent network space address block, which achieves the division of the whole network by combining IP and mask. Click to view [what should be paid attention to when assigning a CIDR for a VPC](http://intl.cloud.tencent.com/document/product/215/4927).

### 3. In the routing table, the access to the public network within a subnet is set to be made through NAT gateways, but the CVMs in the subnet are configured with elastic IPs. So whether these CVMs access the public network through NAT gateways or elastic IPs?
Through the NAT gateways. Click to view [routing rule priority](https://intl.cloud.tencent.com/document/product/215/4954).

### 4. How to modify the private IP of a CVM?
The primary private IP of the primary ENI of a CVM can be modified, while the primary private IP of the secondary ENI cannot be modified. The steps are as follows:
(1) Enter the [CVM Console](https://console.cloud.tencent.com/cvm/), click the CVM in the left navigation bar to enter the CVM list page.
(2) Click the CVM ID to enter the CVM details page, and click the top tab: ENI.
(3) Click to modify the main IP.
(4) Input the new IP and save it.
![](https://mc.qcloudimg.com/static/img/c9a84dfc1784b3a51f21fb80626447ee/step6.jpg)

You can also modify the primary private IP on the ENI details page. Click to view [details.](https://intl.cloud.tencent.com/document/product/215/6513)

