After the first 3 steps, the VPN gateway and VPN tunnel on the cloud are configured. Then, you need to configure the VPN tunnel information on the “local gateway” of the IDC. The “local gateway” on the IDC side means the IPsec VPN device on the IDC side. The public IP of this device is recorded in the “customer gateway” in [Step 2](https://intl.cloud.tencent.com/document/product/1037/39678).

A local gateway is generally deployed in the following scenarios:
>!
>- In the 2 scenarios below, the VPN configuration on your local gateway must be consistent with the VPN tunnel information in [Step 3]https://intl.cloud.tencent.com/document/product/1037/39679). Otherwise, the VPN tunnel cannot be connected.
>- You can view the VPN tunnel configuration information on Tencent Cloud through [VPN tunnel console](https://console.cloud.tencent.com/vpc/vpnConn?rid=1). You can also click **Download Config File** to download the configuration information and upload it to the IPsec VPN gateway of the local IDC for configuration.
>
- **Connecting Tencent Cloud to a local IDC**
A local gateway is a network device with the VPN feature and is generally an egress router or a firewall of an IDC. You can configure a VPN on this device to complete related configuration of the “local gateway”.
>?Configurations may vary because network device manufacturers are different (such as H3C and Cisco). Please configure the local gateway according to the actual situation of the network devices.
>
- **Connecting Tencent Cloud to another public cloud**
A local gateway is the VPN gateway on the target public cloud. You need to configure the VPN of the “local gateway” on the VPN gateway on the target public cloud. For the configuration method, see the documentation about the target public cloud.
