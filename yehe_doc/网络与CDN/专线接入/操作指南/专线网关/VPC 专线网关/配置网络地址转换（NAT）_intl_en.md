You can configure IP translation and IP port translation for Direct Connect gateways of NAT type as follows:
>?This document describes how to configure NAT for a V3R1 direct connect gateway of the NAT type. To do so for a V3R2 direct connect gateway, you only need to bind a private NAT gateway to the direct connect gateway when you [create the direct connect gateway](https://intl.cloud.tencent.com/document/product/216/19256). The IP mappings must be configured at the NAT gateway.
>
- [Configuring IP Translation](#.E9.85.8D.E7.BD.AE-ip-.E8.BD.AC.E6.8D.A2)
- [Configuring IP Port Translation](#.E9.85.8D.E7.BD.AE-ip-.E7.AB.AF.E5.8F.A3.E8.BD.AC.E6.8D.A2)
- [Sample Configurations](#.E9.85.8D.E7.BD.AE.E7.A4.BA.E4.BE.8B)

## Configuring IP Translation
### Configuring local IP translation
#### Rules and limitations
 - The source IP must fall within the CIDR range of the VPC.
 - The mapped IP cannot fall within the CIDR range of the VPC in which the Direct Connect gateway resides.
 - The source IP must be unique. In other words, an IP in a VPC can only be mapped to one IP.
 - The mapped IP must be unique. In other words, multiple IPs in a VPC cannot be mapped to one IP.
 - Source and destination IPs should not be broadcast address (255.255.255.255), Class D addresses (224.0.0.0 - 239.255.255.255), or Class E addresses (240.0.0.0 - 255.255.255.254).
 - The local IP translation of a Direct Connect gateway supports up to 100 IP mappings, each supporting up to 20 ACL rules. To increase the quotas, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

#### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the left sidebar, click **Direct connect gateway** to go to the management page.
3. Click the ID of the Direct Connect gateway of NAT type to go to its details page.
4. On the details page of the direct connect gateway, click the **Local IP translation** tab.
5. At the top left of the **IP mapping** page, click **Add** to add a local IP mapping.
6. In the pop-up window, enter the source IP, mapped IP, and notes, and click **OK**.
7. (Optional) When a new local IP mapping is created, an ACL rule that allows all inbound and outbound traffic is added by default, which means the local IP translation takes effect for all dedicated tunnels. You can edit the ACL rule to change the scope of the local IP translation.
>?
>- When the Direct Connect gateway is also configured with peer IP translation, the **destination IP** of the ACL rule for the local IP translation should be the **mapped IP of peer IP translation**, instead of the source IP.
>- For a ACL rule of local IP translation, you can configure protocol (TCP or UDP), source port, destination IP, and destination port. If port and IP are left blank, they default to ALL; if ALL is selected for protocol, then All is selected for port and IP by default.
>
 1. On the **IP mapping** page, click **Edit ACL rule** to the right of the IP mapping.
  2. At the bottom of the list of existing ACL rules, click **+ New line** to add an ACL rule, and click **Save**.
 3. (Optional) Modify or delete existing ACL rules when ACL rules are in the editing state, and click **Save**.
  4. (Optional) Click <img src="https://main.qcloudimg.com/raw/b2347f733a56962b935f57d086824290.png" style="margin:-3px 0px;width:15px"> to show all ACL rules of the IP mapping on the **IP mapping** page, click **Modify** or **Delete** to the right of the rule that you want to manage, and confirm the action.
 5. (Optional) To modify a local IP mapping, click **Modify IP mapping** to the right of the IP mapping on the **IP mapping** page. Modify the source IP, mapped IP, and notes of the local IP mapping as needed and click **OK** for the modification to take effect.
9. (Optional) To delete a local IP mapping, click **Delete** to the right of the IP mapping on the **IP mapping** page, and confirm the action. Deleting a IP mapping deletes the ACL rules associated with it.

### Configuring peer IP translation
#### Rules and limitations
- The mapped IP cannot fall within the CIDR range of the VPC in which the Direct Connect gateway resides.
- The source IP must be unique. In other words, a Direct Connect peer IP can only be mapped to one IP.
- The mapped IP must be unique. In other words, multiple Direct Connect peer IPs cannot be mapped to the same IP.
- Source and destination IPs should not be broadcast address (255.255.255.255), Class D addresses (224.0.0.0 - 239.255.255.255), or Class E addresses (240.0.0.0 - 255.255.255.254).
- The peer IP translation of a Direct Connect gateway supports up to 100 IP mappings. To increase the quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

#### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the left sidebar, click **Direct connect gateway** to go to the management page.
3. Click the ID of the Direct Connect gateway of NAT type to go to its details page.
4. On the details page of the direct connect gateway, click the **Peer IP Translation** tab.
5. At the top left of the **IP mapping** page, click **Add** to add a peer IP mapping.
6. In the pop-up window, enter the source IP, mapped IP, and notes, and click **OK**.
7. (Optional) To modify a peer IP mapping, click **Modify IP mapping** to the right of the IP mapping on the **IP mapping** page. Modify the source IP, mapped IP, and notes of the peer IP mapping as needed and click **OK** for the modification to take effect.
8. (Optional) To delete a peer IP mapping, click **Delete** to the right of the IP mapping on the **IP mapping** page, and confirm the action.

## Configuring IP Port Translation
### Configuring local source IP port translation
>?If local IP translation conflicts with local IP port translation, local IP translation takes precedence.
>
#### Rules and limitations
 - The mapped IP pool cannot fall within the CIDR range of the VPC in which the Direct Connect gateway resides.
 - ACL rules for multiple mapped IP pools should not overlap. Otherwise, this will cause network address translation conflicts.
 - IP addresses between multiple mapped IP pools should not overlap.
 - Mapped IP pools only support single IPs or continuous IPs, and the /24 IP range of continuous IPs should be consistent. For example, “192.168.0.1 - 192.168.0.6” is supported, but “192.168.0.1 - 192.168.1.2” is not.
 - Mapped IP pools should not be broadcast address (255.255.255.255), Class D addresses (224.0.0.0 - 239.255.255.255), and Class E addresses (240.0.0.0 - 255.255.255.254).
 - Local source IP port translation supports up to 100 mapped IP pools, each supporting up to 20 ACL rules. To increase the quotas, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

#### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the left sidebar, click **Direct connect gateway** to go to the management page.
3. Click the ID of the Direct Connect gateway of NAT type to go to its details page.
4. On the details page of the direct connect gateway, click the **Local source IP port translation** tab.
5. At the top left of the **Mapping IP pool** page, click **Add** to add a mapped IP pool.
6. In the pop-up window, enter the mapped IP pool (IPs or IP range in the form of “A - B”) and notes, and click **OK**. 
7. By default, the ACL rule of a new mapped IP pool denies all inbound and outbound traffic. You need to edit the ACL rule to implement network translation.
>? 
>- When the Direct Connect gateway is also configured with peer IP translation, the **destination IP** of the ACL rule for the local source IP port translation should be the **mapped IP of peer IP translation**, rather than the source IP.
>- For an ACL rule of local source IP port translation, you can configure protocol (TCP or UDP), source IP, source port, destination IP, and destination port.
>
 1. On the **Mapping IP pool** page, click **Edit ACL rule** to the right of the mapped IP pool.
  2. At the bottom of the list of existing ACL rules, click **+ New line** to add an ACL rule, and click **Save**.
 3. (Optional) Modify or delete existing ACL rules when ACL rules are in the editing state, and click **Save**.
  4. (Optional) Click <img src="https://main.qcloudimg.com/raw/b2347f733a56962b935f57d086824290.png" style="margin:-3px 0px;width:15px"> to show all ACL rules of the mapped IP pool on the **Mapping IP pool** page, click **Modify** or **Delete** to the right of the rule that you want to manage, and confirm the action.
 5. (Optional) To modify a mapped IP pool, click **Modify mapping IP pool** to the right of the mapped IP pool on the **Mapping IP Pool** page, and modify the IP and notes of the mapped IP pool as needed.
9. (Optional) To delete a mapped IP pool, click **Delete** to the right of the mapped IP pool on the **Mapping IP Pool** page, and confirm the action. Deleting a mapped IP pool deletes the ACL rules associated with it.



### Configuring local destination IP port translation
#### Rules and limitations
- The source IP must fall within the CIDR range of the VPC in which the Direct Connect gateway resides.
- The source IP port must be unique. In other words, an IP port in a VPC can only be mapped to one IP port.
- The mapped IP port cannot fall within the CIDR range of the VPC.
- The mapped IP port must be unique. In other words, multiple IP ports in a VPC cannot be mapped to one IP port.
- Source IPs and mapped IPs should not be broadcast address (255.255.255.255), Class D addresses (224.0.0.0 - 239.255.255.255), or Class E addresses (240.0.0.0 - 255.255.255.254).
- Local destination IP port translation supports up to 100 IP mappings. To increase the quota, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category).

#### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the left sidebar, click **Direct connect gateway** to go to the management page.
3. Click the ID of the Direct Connect gateway of NAT type to go to its details page.
4. On the details page of the direct connect gateway, click the **Local destination IP port translation** tab.
5. At the top left of the **IP port mapping** page, click **Add** to add a new local destination IP port mapping.
6. In the pop-up window, select the protocol. Enter the source IP port, mapped IP port, and notes, and click **OK**.
7. (Optional) To modify a local destination IP port mapping, click **Modify IP port mapping** to the right of the IP port mapping on the **IP port mapping** page, and modify the mapping relationship and notes of the IP port mapping as needed.
8. (Optional) To delete a local destination IP port mapping, click **Delete** to the right of the IP port mapping on the **IP port mapping** page, and confirm the action.

## Sample Configuration
### Local IP translation configuration example
IP A ` 192.168.0.3` in a VPC is the source IP, and is mapped to IP B `10.100.0.3` through local IP translation:
- The network packet source IP of the active access from IP A to the Direct Connect peer is automatically changed to `10.100.0.3`.
- All network packets accessing `10.100.0.3` from the Direct Connect peer will automatically point to IP A `192.168.0.3`.

### Peer IP translation configuration example
Direct Connect peer IP D `10.0.0.3` is the source IP, and is mapped to IP C `172.16.0.3` through peer IP translation:
- The network packet source IP of the active access from IP D `10.0.0.3` to the VPC is automatically changed to IP C `172.16.0.3`.
- All network packets accessing IP C `172.16.0.3` from the VPC will automatically point to IP D `10.0.0.3`.

### Local source IP port translation configuration example
The VPC C network IP range `172.16.0.0/16` connects the third-party bank A and B via Direct Connect, where the peer network IP range of bank A is `10.0.0.0/28`, requiring the connected network IP range `192.168.0.0/28`, and the peer network IP range of bank B is `10.1.0.0/28`, requiring the connected network IP range `192.168.1.0/28`. Two local source IP port translations can be configured as follows:
<table>
<thead>
<tr>
<th colspan="2">Configuration</th>
<th>Local Source IP Port Translation A</th>
<th>Local Source IP Port Translation B</th>
</tr>
</thead>
<tbody><tr>
<td colspan="2">Mapped IP pool</td>
<td><code>192.168.0.1 - 192.168.0.15</code></td>
<td><code>192.168.1.1 - 192.168.1.15</code></td>
</tr>
<tr>
<td rowspan="5">ACL rule</td>
<td>Protocol</td>
<td>All</td>
<td>All</td>
</tr>
<tr>
<td>Source IP</td>
<td><code>172.16.0.0/16</code></td>
<td><code>172.16.0.0/16</code></td>
</tr>
<tr>
<td>Source port</td>
<td>-</td>
<td>-</td>
</tr>
<tr>
<td>Destination IP</td>
<td><code>10.0.0.0/28</code></td>
<td><code>10.1.0.0/28</code></td>
</tr>
<tr>
<td>Destination port</td>
<td>-</td>
<td>-</td>
</tr>
</tbody></table>
After configuration, the network requests from VPC C to access bank A and bank B will be translated to random ports in the mapped IP pools based on the corresponding ACL rules to access the corresponding dedicated tunnels.

### Local destination IP port translation configuration example
For the VPC C IP range `172.16.0.0/16`, if you only want to open some of the ports to the active access of the Direct Connect peer, you can configure local destination IP port mapping A and B as follows:
- Local destination IP port mapping A: source IP port is `172.16.0.1:80` and mapped IP port is `10.0.0.1:80`.
- Local destination IP port mapping B: source IP port is `172.16.0.1:8080` and mapped IP port is `10.0.0.1:8080`.

After configuration, the Direct Connect peer can access ports `10.0.0.1:80` and` 10.0.0.1:8080` to implement active access to ports `172.16.0.1:80` and `172.16.0.1:8080` in VPC C.
