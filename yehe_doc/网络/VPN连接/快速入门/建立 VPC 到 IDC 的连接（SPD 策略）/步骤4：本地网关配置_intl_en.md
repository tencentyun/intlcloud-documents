After the first 3 steps, the VPN gateway and VPN tunnel on the Tencent Cloud are configured. Then, you need to configure the VPN tunnel on the local gateway of the IDC. For more information about local gateway, see [Local Gateway Configurations](https://cloud.tencent.com/document/product/554/56361). The local gateway refers to the IPsec VPN device on the IDC side. The public IP of this device is recorded in the “customer gateway” created in [Step 2](https://intl.cloud.tencent.com/document/product/1037/32691).

A local gateway is generally deployed in the following scenarios:
>!
>- In both scenarios below, you should configure the same VPN tunnel on your local gateway as that configured in [Step 3](https://intl.cloud.tencent.com/document/product/1037/32692). Otherwise, the VPN tunnel cannot be connected.
>- You can view the VPN tunnel configurations in the [VPN Tunnel console](https://console.cloud.tencent.com/vpc/vpnConn?rid=1). You can also click **Download config file** to download the configuration information and upload it to the IPsec VPN gateway of the local IDC for configuration.
>
- **Connecting Tencent Cloud to a local IDC**
A local gateway is a network device with the VPN feature and is generally an egress router or a firewall of an IDC. You can configure the VPN connection on the local gateway.
>?Configurations may vary with network device manufacturers (such as H3C and Cisco). Please configure the local gateway as needed.
>
- **Connecting Tencent Cloud to another public cloud**
A local gateway is the VPN gateway on the target public cloud. You need to configure the VPN connection on the VPN gateway of the target public cloud. For more information about configuration method, see the documentation of the target public cloud.

