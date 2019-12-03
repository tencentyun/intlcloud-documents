Now, the VPN gateway and VPN tunnel are successfully configured on Tencent Cloud. You need to further configure the peer side of the VPN tunnel on a local gateway.
A local gateway is generally deployed in the following scenarios:
- **Connect Tencent Cloud to a local IDC**
A local gateway is a network device with the VPN function and it is generally an egress router or a firewall of an IDC. You can configure a VPN on the local gateway to complete related configuration of the local gateway.
- **Connect Tencent Cloud to Tencent Cloud**
A local gateway is another VPN gateway deployed in the Tencent Cloud VPC on the peer side. You can repeat Steps 1 to 3 on the VPN gateway to complete related configuration of the local gateway.
- **Connect Tencent Cloud to another public cloud**
A local gateway is a VPN gateway on your destination public cloud. You need to configure the VPN gateway on the destination public cloud to complete VPN configuration of the local gateway. For the configuration method, see the documentation on destination public cloud.

>!
>- In all the three scenarios above, the VPN configuration on your local gateway must be consistent with the VPN tunnel information in [Step 3](https://cloud.tencent.com/document/product/554/18991); otherwise, the VPN tunnel cannot be connected.
>- You can view the VPN tunnel configuration information on Tencent Cloud through [Tencent Cloud Console](https://console.cloud.tencent.com/vpc/vpnGw). You can also download the profile and load it to the IPsec VPN gateway of the local IDC for configuration.
