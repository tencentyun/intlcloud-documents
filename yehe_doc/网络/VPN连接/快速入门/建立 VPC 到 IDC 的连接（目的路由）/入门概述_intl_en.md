This document describes how to quickly create a VPN connection and configure routing and forwarding policies with a route table to ensure the secure communication between VPC and IDC.
> ?The VPN route table is currently in a beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Directions
Below is the flowchart of activating a VPN connection:
![](https://main.qcloudimg.com/raw/1aa819dbe82889063db1afc22ec7097e.png)

## Example
With an IPsec VPN connection, you can connect the subnet A: `192.168.1.0/24` in your VPC in **Tokyo** to the subnet: `10.0.1.0/24` in your local IDC.
![](https://main.qcloudimg.com/raw/f9137cdb844c5d0f095e884a044b0171.png)

