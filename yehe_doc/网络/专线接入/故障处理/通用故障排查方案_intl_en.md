This document provides guidance on Direct Connect troubleshooting, helping you troubleshoot network connection failures.

## Troubleshooting Sequence
Troubleshoot the following items in sequence:
<dx-steps>
- [Troubleshooting physical layer linkage failures](#1)
- [Troubleshooting data link layer failures](#2)
- [Troubleshooting network layer or transport layer failures](#3)
- [Troubleshooting security group failures](#4)
- [Troubleshooting route failures](#5)
</dx-steps>

<span id="1"></span>
## Troubleshooting Physical Layer Linkage Failures
When you encounter port failure, fiber optic components exception at either or both ends, CRC, or packet error, follow the steps below to troubleshot physical layer linkage failures.
1. Confirm that your IDC CPE device is enabled with open ports.
2. Contact your DC connection provider and obtain the relevant certificates indicating that the construction and end-to-end access has been completed.
3. Check that the fiber optic components in IDC are normal. Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to request the after-sales manager to check fiber optic components in the access point’s data center.
4. Contact your DC connection provider and access point’s carrier to test link segments.
Assume that a Direct Connect service connects IDC to the access point’s data center through the optic splice box outside the data center building, and then to the destination data center through Optical Distribution Frame (ODF), then the segment testing should be performed as follows:
(1) Test that the ODF in your local IDC can communicate with the access devices.
(2) If there are multiple ODFs in your local IDC, test that they can communicate with each other.
(3) Contact your DC connection provider to check that the connection between your local IDC and the data center’s optic splice box works.
(4) Contact the access point’s carrier to check that the optic splice box can communicate with ODF.
(5) Contact the access point’s carrier to check that ODFs can communicate.
(6) Contact the access point’s carrier to check that ODF can communicate with access devices at the access point.
![](https://main.qcloudimg.com/raw/95c325912d32dd94d3e0cf46b713ce9f.png)

<span id="2"></span>
## Troubleshooting Data Link Layer Failures
1. When VLAN ID is not 0:
 - Ensure any Layer 2/Layer 3 devices between the carrier’s connection, Tencent Cloud access devices and local IDC access devices (including the IDC access device itself) have enabled VLAN relay for your VLAN tags, that is, identify and allow your VLAN tag.
 - Ensure that any Layer 2/Layer 3 devices between the Tencent Cloud edge device and your local IDC edge device (including the IDC edge device itself) correctly relay the VLAN and there is no VLAN conversion.
2. Check that the IP addresses are correctly configured. Ensure the IP addresses are correctly configured on the local access devices, which remain stable without MAC address flapping records.
3. Ensure the layer-2 link detection protocols such as STP\Loop-detection are disabled on IDC access devices; otherwise, ports may be blocked.

<span id="3"></span>
## Troubleshooting Network Layer or Transport Layer Failures
1. Ensure that the IP addresses configured on both sides of the connection are in one subnet with the same subnet mask.
2. Ensure that each side configured a unique IP address, and no IP is reused.
3. If your connection has bidirectional forwarding Detection (BFD) enabled, ensure that the BFD message will be allowed to pass in the security policy of IDC devices.
4. If your connection has NQA detection enabled, note that Tencent Cloud supports the ICMP-echo type. Ensure that the ICMP message will be allowed to pass in the security policy of IDC devices.
5. If a BGP session is required on both sides of the connection for Tencent Cloud VPC routes and IDC routes propagation:
	- Correctly configure BGP ASN and BGP PEER IP on IDC devices.
	- Configure the same BGP MD5 authentication key on both sides.
	- Allow the BGP message to pass in the security policy of IDC devices.
	- Open the TCP 179 port for the BGP session in the security policy.

<span id="4"></span>
## Troubleshooting Security Issues
- Check the ACL settings
   - Ensure that the Tencent Cloud subnet ACL allows the traffic going from or to IDC hosts.
   - Ensure that the IDC subnet ACL allows the traffic going from or to Tencent Cloud CVMs.
- Check the security group settings
   - Ensure that the Tencent Cloud CVM security group allows the traffic going from or to IDC hosts.
   - Ensure that the IDC security group allows the traffic going from or to Tencent Cloud CVMs.

<span id="5"></span>
## Troubleshooting Route Failures
### VPC-based direct connect gateway

- Static dedicated tunnel
Check that IDC IP range is correctly configured on the dedicated tunnel and propagated to Tencent Cloud VPC. Otherwise, the Tencent Cloud VPC route to IDC server will be unreachable and cause business to be inaccessible.

#### 1. Check the CPE IP range in the dedicated tunnel
1. Log in to the [Direct Connect](https://console.cloud.tencent.com/dc/conn) console. Go to the **Dedicated Tunnels** page and click the **ID/Name** of the target dedicated tunnel to enter its details page. Select the **Advanced Configuration** tab and check whether the CPE IP range is correctly configured.
2. Reconfigure the CPE IP range if the previous configuration is incorrect. For detailed directions, see [Applying for a Tunnel](https://intl.cloud.tencent.com/document/product/216/19250).

#### 2. Check the route table
1. Log in to the [Direct Connect](https://console.cloud.tencent.com/dc/conn) console. Go to the **Dedicated Tunnels** page and click the **ID/Name** of the target dedicated tunnel to enter its details page. Select the **Basic Info** tab and click the VPC ID to view VPC details.
   ![](https://main.qcloudimg.com/raw/3980a49d7b1bf2ef27103136db0ad8fc.png)
2. Click the **Route Table**.
	 ![](https://main.qcloudimg.com/raw/ee4efa76d45324afa617866eac0a04e2.png)
3. Select the **Basic Information** tab and check if a routing policy with the CPE IP range as destination and the direct connect gateway as next hop type is enabled.
	 ![](https://main.qcloudimg.com/raw/6b3689fc7b9ad75262e5b453d7701fb1.png)
4. Reconfigure the routing policy if the previous configuration is incorrect. For detailed directions, see [Configuring the Route Table](https://intl.cloud.tencent.com/document/product/216/19259).

- BGP dedicated tunnel
 Check that IDC IP range is correctly synced to the direct connect gateway based on the BGP protocol and propagated to Tencent Cloud VPC. Otherwise, the Tencent Cloud VPC route to IDC server will be unreachable and cause business to be inaccessible.

#### 1. Check the BGP route configurations
1. Log in to the [Direct Connect](https://console.cloud.tencent.com/dc/conn) console. Go to the **Dedicated Tunnels** page and click the **ID/Name** of the target dedicated tunnel to enter its details page. Select the **Advanced Configuration** tab and check BGP configurations.
2. Reconfigure BGP if the previous configuration is incorrect. For detailed directions, see [Applying for a Tunnel](https://intl.cloud.tencent.com/document/product/216/19250).

#### 2. Check the route table
1. Log in to the [Direct Connect](https://console.cloud.tencent.com/dc/conn) console. Go to the **Dedicated Tunnels** page and click the **ID/Name** of the target dedicated tunnel to enter its details page. Select the **Basic Info** tab and click the VPC ID to view VPC details.
   ![](https://main.qcloudimg.com/raw/3980a49d7b1bf2ef27103136db0ad8fc.png)
2. Click the **Route Table**.
	 ![](https://main.qcloudimg.com/raw/ee4efa76d45324afa617866eac0a04e2.png)
3. Select the **Basic Information** tab and check if a routing policy with the CPE IP range as destination and the direct connect gateway as next hop type is enabled.
	 ![](https://main.qcloudimg.com/raw/6b3689fc7b9ad75262e5b453d7701fb1.png)
4. Reconfigure the routing policy if the previous configuration is incorrect. For detailed directions, see [Configuring the Route Table](https://intl.cloud.tencent.com/document/product/216/19259).


### CCN-based direct connect gateway
- Static dedicated tunnel
Check that IDC IP range is correctly configured on the dedicated tunnel and propagated to CCN. Otherwise, the Tencent Cloud VPC route to IDC server will be unreachable and cause business to be unaccessible.

#### 1. Check the CPE IP range in the dedicated tunnel
1. Log in to the [Direct Connect](https://console.cloud.tencent.com/dc/conn) console. Go to the **Dedicated Tunnels** page and click the **ID/Name** of the target dedicated tunnel to enter its details page. Select the **Advanced Configuration** tab and check whether the CPE IP range is correctly configured.
2. Reconfigure the CPE IP range if the previous configuration is incorrect. For detailed directions, see [Applying for a Tunnel](https://intl.cloud.tencent.com/document/product/216/19250).

#### 2. Check the IDC IP range on the direct connect gateway
1. Log in to the [Direct Connect Gateway](https://console.cloud.tencent.com/vpc/dcgw?rid=8) console and click the **ID/Name** of the target direct connect gateway to enter its details.
2. Select the **IDC IP Range** tab, and check the configurations.
	![](https://main.qcloudimg.com/raw/ffcf040f54457685153039a00c72dd1c.png)
3. Reconfigure an IDC IP range if no configuration is available. For detailed directions, see [Adding IDC IP Ranges to the Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/39083).

- BGP dedicated tunnel
Check that the dedicated tunnel BGP is correctly configured and IDC IP range is synced to direct connect gateway and propagated to CCN. Otherwise, the Tencent Cloud VPC route to IDC server will be unreachable and cause business to be unaccessible.

#### 1. Check the BGP route configurations
1. Log in to the [Direct Connect](https://console.cloud.tencent.com/dc/conn) console. Go to the **Dedicated Tunnels** page and click the **ID/Name** of the target dedicated tunnel to enter its details page. Select the **Advanced Configuration** tab and check BGP configurations.
2. Reconfigure BGP if the previous configuration is incorrect. For detailed directions, see [Applying for a Tunnel](https://intl.cloud.tencent.com/document/product/216/19250).

#### 2. Check the IDC IP range on the direct connect gateway
1. Log in to the [Direct Connect Gateway](https://console.cloud.tencent.com/vpc/dcgw?rid=8) console and click the **ID/Name** of the target direct connect gateway to enter its details.
2. Select the **IDC IP Range** tab, and check the configurations.
	![](https://main.qcloudimg.com/raw/ffcf040f54457685153039a00c72dd1c.png)
3. Reconfigure an IDC IP range if no configuration is available. For detailed directions, see [Adding IDC IP Ranges to the Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/39083).
