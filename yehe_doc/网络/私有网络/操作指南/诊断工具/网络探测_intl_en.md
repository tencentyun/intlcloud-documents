Tencent Cloud network probe is a service for monitoring VPC network connection quality. It can monitor various key metrics in network connections, such as the latency and packet loss rate.

Under the hybrid cloud network architecture, you can use a VPN or establish a direct connection to connect the VPC on Tencent Cloud with your own IDC. To monitor the network quality of connections in real time, you can create a network probe object in the subnet that needs to communicate with the IDC. After the object is created, the packet loss rate and latency of the probed link will be returned, fulfilling the following purposes:
- Real-time monitoring of connection quality
- Real-time connection failure alarm

## Instructions
- The network probe service adopts ping detection with a frequency of 20 times per minute.
- A maximum of 50 network probes can be created in each VPC.

## Creating a Network Probe
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Diagnostic Tools** > **Network Probe** in the left sidebar to enter the management page.
3. Click **+Create**. In the pop-up box, complete or confirm the following parameters in sequence:
 - Name: the name of the network probe.
 - Probe Source: two idle private IP addresses in the subnet are automatically selected as the source IP addresses for the network probe. Therefore, you do not need to enter the value.
 - Destination IP Address to Probe: a maximum of two destination IP addresses are supported for the network probe. Enable the ICMP firewall policy for the destination server of network probe.
 - Next Hop: the next-hop route that the traffic of the network probe flows through. After the next-hop object is configured, an appropriate 32-bit route is automatically added in the route table associated with the subnet.
![](https://main.qcloudimg.com/raw/2174c50676f92290be0e367d7efc6a22.png)
4. After finishing the configuration, click **Create**.

>
> 1. We recommend that you verify the probe result before creating a network probe instance. If a connection fails, check whether the subnet route is correctly configured or whether the network ACL, security group, and other firewalls are permitted by the destination object to be probed.
> 2. The network probe route is a system route and cannot be modified.
> 3. When the subnet switches a route, the system route will be deleted from the route table originally associated with the subnet, and be added to the new route table associated with the subnet.

## Checking the Latency and Packet Loss Rate of a Network Probe
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Diagnostic Tools** > **Network Probe** in the left sidebar to enter the management page.
3. Click the monitoring icon of a network probe instance to view the latency and packet loss rate of the network probe.
![](https://main.qcloudimg.com/raw/b1a8a96df051a50cf58fd6f34b09a228.png)

## Modifying a Network Probe
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Diagnostic Tools** > **Network Probe** in the left sidebar to enter the management page.
3. In the list, find the network probe instance that you want to modify. Then, click **Edit** in the operation column.
![1](https://main.qcloudimg.com/raw/04ada38a6d656c5d956a361067f90446.png)
4. In the pop-up box, make required changes and click **Submit** to save the changes.
![](https://main.qcloudimg.com/raw/d92a1320d63fc08151bd1f32f4c0ae3e.png)

## Deleting a Network Probe
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Diagnostic Tools** > **Network Probe** in the left sidebar to enter the management page.
3. In the list, find the network probe instance that you want to delete. Then, click **Delete** in the operation column, and select **Delete** in the pop-up window to confirm the deletion.
 > Deleting a network probe instance also deletes all its routes.
 >
![](https://main.qcloudimg.com/raw/f4e41ac5686d3c3bff4722f35bde995c.png)

