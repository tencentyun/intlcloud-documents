You can configure IP translation and IP port translation for Direct Connect gateways of the NAT type as follows:
- [Configuring IP translation](#.E9.85.8D.E7.BD.AE-ip-.E8.BD.AC.E6.8D.A2)
- [Configuring IP port translation](#.E9.85.8D.E7.BD.AE-ip-.E7.AB.AF.E5.8F.A3.E8.BD.AC.E6.8D.A2)
- [Sample configurations](#.E9.85.8D.E7.BD.AE.E7.A4.BA.E4.BE.8B)

## Configuring IP Translation
### Configuring local IP translation
#### Rules and limitations
 - The source IP address must fall within the CIDR block of the VPC instance.
 - The mapped IP address cannot fall within the CIDR block of the VPC instance in which the Direct Connect gateway resides.
 - The source IP address must be unique. In other words, an IP address in a VPC instance can only be mapped to one IP address.
 - The mapped IP address must be unique. In other words, multiple IP addresses in a VPC instance cannot be mapped to the same IP address.
 - Source and destination IP addresses cannot be the broadcast address (255.255.255.255), class-D addresses (224.0.0.0 - 239.255.255.255), and class-E addresses (240.0.0.0 - 255.255.255.254).
 - The local IP translation of a Direct Connect gateway supports up to 100 IP mappings, each of which supports up to 20 ACL rules. To increase the quota, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

#### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the leftside bar, click **Direct Connect Gateways** to go to the management page.
3. Click the ID of the Direct Connect gateway of the NAT type to go to its details page.
4. On the details page of the Direct Connect gateway, click the **Local IP Translation** tab.
5. In the upper-left corner of the IP mapping page, click **Add** to add a local IP mapping.
6. In the window that appears, enter the source IP address, mapped IP address, and notes. Then, click **OK**.
7. (Optional) When a new local IP mapping is created, an ACL rule that allows all inbound and outbound traffic is added by default, which means local IP translation takes effect for all dedicated tunnels. You can edit the ACL rule to change the scope of local IP translation.
>?
>- If the Direct Connect gateway is also configured with peer IP translation, the **destination IP address** for the ACL rule for local IP translation should be the **mapped IP address for peer IP translation**, instead of the source IP address.
>- For an ACL rule of local IP translation, you can configure the protocol (TCP or UDP), source port, destination IP address, and destination port. If the port and IP address are left empty, they default to ALL. If ALL is selected for the protocol, then All is also selected for the port and IP address by default.
> 
    1. On the IP mapping page, click **Edit ACL rule** for the IP mapping.
    2. At the bottom of the list of existing ACL rules, click **New line** to add an ACL rule, and then click **Save**.
    3. (Optional) You can modify or delete an existing ACL rule in the editing mode. After making the change, click **Save**.
    4. (Optional) You can click <img src="https://main.qcloudimg.com/raw/b2347f733a56962b935f57d086824290.png" style="margin:-3px 0px;width:15px"> to show all the rules of the IP mapping on the IP mapping page, and then click **Modify** or **Delete** for the rule to be modified or deleted. When making the change, confirm the operation as prompted.

8. (Optional) To modify the local IP mapping, click **Modify IP mapping** for the IP mapping on the IP mapping page. Modify the source IP address, mapped IP address, and notes of the local IP mapping as needed, and click **OK** to apply the changes.
9. (Optional) To delete the local IP mapping, click **Delete** for the IP mapping on the IP mapping page, and then confirm the operation as prompted. Deleting an IP mapping also deletes its associated ACL rules.

### Configuring peer IP translation
#### Rules and limitations
- The mapped IP address must not fall within the CIDR block of the VPC instance in which the Direct Connect gateway resides.
- The source IP address must be unique. In other words, a Direct Connect peer IP address can only be mapped to one IP address.
- The mapped IP address must be unique. In other words, multiple Direct Connect peer IP addresses cannot be mapped to the same IP address.
- Source and destination IP addresses cannot be the broadcast address (255.255.255.255), class-D addresses (224.0.0.0 - 239.255.255.255), and class-E addresses (240.0.0.0 - 255.255.255.254).
- The peer IP translation of a Direct Connect gateway supports up to 100 IP mappings. To increase the quota, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

#### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the left sidebar, click **Direct Connect Gateways** to go to the management page.
3. Click the ID of the Direct Connect gateway of the NAT type to go to its details page.
4. On the details page of the Direct Connect gateway, click the **Peer IP Translation** tab.
5. In the upper-left corner of the IP mapping page, click **Add** to add a peer IP mapping.
6. In the window that appears, enter the source IP address, mapped IP address, and notes. Then, click **OK**.
7. (Optional) To modify the peer IP mapping, click **Modify IP mapping** for the IP mapping on the IP mapping page. Modify the source IP address, mapped IP address, and notes of the peer IP mapping as needed, and click **OK** to apply the changes.
8. (Optional) To delete the peer IP mapping, click **Delete** for the IP mapping on the IP mapping page, and then confirm the operation as prompted.

## Configuring IP Port Translation
### Configuring local source IP port translation
>?If local IP translation conflicts with local IP port translation, local IP translation prevails.
>
#### Rules and limitations
 - The mapped IP pool must not fall within the CIDR block of the VPC instance in which the Direct Connect gateway resides.
 - ACL rules for multiple mapped IP pools cannot overlap. Otherwise, network address translation conflicts occur.
 - IP addresses cannot overlap between mapped IP pools.
 - Mapped IP pools only support a single IP address or continuous IP addresses, and the /24 IP ranges of continuous IP addresses must be consistent. For example, "192.168.0.1 - 192.168.0.6" is supported, but "192.168.0.1 - 192.168.1.2" is not.
 - Mapped IP pools do not support the broadcast address (255.255.255.255), class-D addresses (224.0.0.0 - 239.255.255.255), and class-E addresses (240.0.0.0 - 255.255.255.254).
 - Local source IP port translation supports up to 100 mapped IP pools, each of which supports up to 20 ACL rules. To increase the quota, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

#### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the left sidebar, click **Direct Connect Gateways** to go to the management page.
3. Click the ID of the Direct Connect gateway of the NAT type to go to its details page.
4. On the details page of the Direct Connect gateway, click the **Local Source IP Port Translation** tab.
5. In the upper-left corner of the mapped IP pool page, click **Add** to add a mapped IP pool.
6. In the window that appears, enter the mapped IP pool (IP addresses or an IP range in the format of "A - B") and notes. Then, click **OK**. 
7. By default, the ACL rule of a new mapped IP pool denies all inbound and outbound traffic. To implement network translation, you must edit the ACL rule.
>?
>- If the Direct Connect gateway is also configured with peer IP translation, the **destination IP address** for the ACL rule for local source IP port translation should be the **mapped IP address of peer IP translation**, instead of the source IP address.
>- For an ACL rule of local source IP port translation, you can configure the protocol (TCP or UDP), source IP address, source port, destination IP address, and destination port.
>
 1. On the mapped IP pool page, click **Edit ACL rule** for the mapped IP pool.
  2. At the bottom of the list of existing ACL rules, click **New Line** to add an ACL rule, and then click **Save**.
 3. (Optional) You can modify or delete an existing ACL rule in the editing mode. After making the change, click **Save**.
  4. (Optional) You can click <img src="https://main.qcloudimg.com/raw/b2347f733a56962b935f57d086824290.png" style="margin:-3px 0px;width:15px"> to show all the rules of the mapped IP pool on the mapped IP pool page, and then click **Modify** or **Delete** for the rule to be modified or deleted. When making the change, confirm the operation as prompted.
8. (Optional) To modify the mapped IP pool, click **Modify Mapped IP Pool** for the mapped IP pool on the mapped IP pool page. Then, you can modify the IP address and notes of the mapped IP pool as needed.
9. (Optional) To delete the mapped IP pool, click **Delete** for the mapped IP pool on the mapped IP pool page, and confirm the operation as prompted. Deleting a mapped IP pool also deletes its associated ACL rules.



### Configuring local destination IP port translation
#### Rules and limitations
- The source IP address must fall within the CIDR block of the VPC instance in which the Direct Connect gateway resides.
- The source IP port must be unique. In other words, an IP port in a VPC instance can only be mapped to one IP port.
- The mapped IP port most not fall within the CIDR block of the VPC instance.
- The mapped IP port must be unique. In other words, multiple IP ports in a VPC instance cannot be mapped to one IP port.
- Source IPs and mapped IPs cannot be the broadcast address (255.255.255.255), class-D addresses (224.0.0.0 - 239.255.255.255), and class-E addresses (240.0.0.0 - 255.255.255.254).
- Local destination IP port translation supports up to 100 IP mappings. To increase the quota, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

#### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the left sidebar, click **Direct Connect Gateways** to go to the management page.
3. Click the ID of the Direct Connect gateway of the NAT type to go to its details page.
4. On the details page of the Direct Connect gateway, click the **Local Destination IP Port Translation** tab.
5. In the upper-left corner of the IP port mapping page, click **Add** to add a local destination IP port mapping.
6. In the window that appears, select the protocol and enter the source IP port, mapped IP port, and notes. Then, click **OK**.
7. (Optional) To modify the local destination IP port mapping, click **Modify IP port mapping** for the IP port mapping on the IP port mapping page. Then, you can modify the mapping relationship and notes of the IP port mapping as needed.
8. (Optional) To delete the local destination IP port mapping, click **Delete** for the IP port mapping on the IP port mapping page, and then confirm the operation as prompted.

## Sample Configurations
### Sample local IP translation configuration
IP A ` 192.168.0.3` in a VPC instance is the source IP address. It is mapped to IP B `10.100.0.3` through local IP translation:
- The source IP address of network packets for active access from IP A to the Direct Connect peer is automatically changed to `10.100.0.3`.
- All network packets accessing `10.100.0.3` from the Direct Connect peer will automatically point to IP A `192.168.0.3`.

### Sample peer IP translation configuration
Direct Connect peer IP D `10.0.0.3` is the source IP address. It is mapped to IP C `172.16.0.3` through peer IP translation:
- The original Class D IP address `10.0.0.3` for VPC network access automatically changes to Class C IP address `172.16.0.3`.
- All network packets accessing IP C `172.16.0.3` from the VPC instance will automatically point to IP D `10.0.0.3`.

### Sample configuration for local source IP port translation
VPC C’s IP range `172.16.0.0/16` connects third-party banks A and B through Direct Connect. In this case, the peer IP range of bank A is `10.0.0.0/28`, requiring the connected IP range to be `192.168.0.0/28`. On the other hand, the peer IP range of bank B is `10.1.0.0/28`, requiring the connected IP range to be `192.168.1.0/28`. Then, both local source IP port translations can be configured as follows:
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
<td>ALL</td>
<td>ALL</td>
</tr>
<tr>
<td>Source IP address</td>
<td><code>172.16.0.0/16</code></td>
<td><code>172.16.0.0/16</code></td>
</tr>
<tr>
<td>Source port</td>
<td>—</td>
<td>—</td>
</tr>
<tr>
<td>Destination IP address</td>
<td><code>10.0.0.0/28</code></td>
<td><code>10.1.0.0/28</code></td>
</tr>
<tr>
<td>Destination port</td>
<td>—</td>
<td>—</td>
</tr>
</tbody></table>
After the configuration, network requests from VPC C to access banks A and B will be translated to random ports in the mapped IP pools based on the corresponding ACL rules to access the corresponding dedicated tunnels.

### Sample configuration for local destination IP port translation
VPC C’s IP range is `172.16.0.0/16`. To open only some of the ports to the active access of the Direct Connect peer, you can configure local destination IP port mappings A and B as follows:
- Local destination IP port mapping A: the source IP port is `172.16.0.1:80` and the mapped IP port is `10.0.0.1:80`.
- Local destination IP port mapping B: the source IP port is `172.16.0.1:8080` and the mapped IP port is `10.0.0.1:8080`.

After the configuration, the Direct Connect peer can access ports `10.0.0.1:80` and` 10.0.0.1:8080` to implement active access to ports `172.16.0.1:80` and `172.16.0.1:8080` in VPC C.
