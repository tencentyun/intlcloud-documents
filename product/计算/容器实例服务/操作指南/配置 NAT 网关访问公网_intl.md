## Overview
CIS instances support configuring [NAT Gateway](https://cloud.tencent.com/document/product/215/4975) and [Route Tables](https://cloud.tencent.com/document/product/215/4954), to achieve mutual access between them and the resources on the Internet.

## Configuring the Internet to Access a CIS Instance
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/nat), click **NAT Gateway** on the left navigation bar to go to its console, and click **New** to create a NAT gateway in the same region and same VPC with the CIS instance.
![][1]
2. After the NAT gateway is created, click the **ID/Name** of the new NAT gateway to enter its details page. Click **Port forwarding** -> **Create** to create a port forwarding rule.
Configuration rule:
 - External IP/port: Select the public IP and the port of the NAT gateway to be accessed.
 - Internal IP/port: Select private IP and the occupied port of the CIS instance to be accessed.
![][2]
3. After the configuration is completed, you can access the services provided by the CIS instance via the NAT gateway's private IP and port.

## Configuring a CIS instance to Access the Internet
<a id="step1"></a>
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/nat), click **NAT Gateway** on the left navigation bar to go to its console, and click **New** to create a NAT gateway in the same region and same VPC with the CIS instance.
![][1]

2. Click **Route Tables** on the left navigation bar, click **New**, and a creation page pops up where you can create a route table in the same region and same VPC with the CIS instance.
![][3]

3. Enter the route table's name and network, and configure routing rules.
Configuration rule:
 - Destination: Select the public IP address to be accessed. You can configure CIDR. For example, if you enter 0.0.0.0/0, all traffic will be forwarded to the NAT gateway.
 - Next hop type: Select **NAT Gateway**.
 - Next hop: Select the NAT gateway created in <a href="#step1">Step 1</a>.
![][4]

4. After the routing configuration is completed, a CIS instance in the same VPC can access the Internet through the NAT gateway's public IP.

[1]:https://main.qcloudimg.com/raw/20cb03ac219ea914ebcc50a9ea36d354.png
[2]:https://main.qcloudimg.com/raw/e7827f278e950527847f34a5e77275e4.png
[3]:https://main.qcloudimg.com/raw/1ebcee1dce974c6b0d459c0d7762c1fd.png
[4]:https://main.qcloudimg.com/raw/9baf3c5e5b42da47a0385db55baf27f0.png
