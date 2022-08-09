To connect your IDC to a Tencent Cloud VPC via IPsec VPN connection, you need to load the VPN configurations to the network device of your local IDC after configuring the VPN gateway on Tencent Cloud. This document provides an example on how to load the IPsec VPN configuration to a Cisco firewall.

>!
>- This document is only for the configuration of an IKEv1 VPN.
>- Replace all the IPs, ports, and other parameters given in this document with your actual values for configurations.

## Prerequisites

You have [created a VPN connection](https://intl.cloud.tencent.com/document/product/1037/39688) in a Tencent Cloud VPC, and configured the [VPN tunnel](https://intl.cloud.tencent.com/document/product/1037/39635).

## Data Collection

The following table describes the IPsec VPN configuration data.

<table>
<th colspan="3">Configuration Item</th>
<th>Sample value</th>
<tr>
<td rowspan="4">Network</td>
<td rowspan="2">VPC</td>
<td>Subnet CIDR block</td>
<td>10.1.1.0/24 </td>
</tr>
<tr>
<td>Public IP of the VPN gateway</td>
<td>159.xx.xx.242</td>
</tr>
<tr>
<td rowspan="2">IDC</td>
<td>Private CIDR block</td>
<td>172.16.0.0/16</td>
</tr>
<tr>
<td>Public IP of the gateway</td>
<td>120.xx.xx.76</td>
</tr>
<tr>
<td rowspan="17">IPsec VPN connection </td>
<td rowspan="10">IKE</td>
<td>Version</td>
<td>IKEV1</td>
</tr>
<tr>
<td>ID verification methods</td>
<td>Pre-shared key</td>
</tr>
<tr>
<td>PSK</td>
<td>tencent@123</td>
</tr>
<tr>
<td>Encryption algorithm</td>
<td>AES-128</td>
</tr>
<tr>
<td>Verification algorithm</td>
<td>MD5</td>
</tr>
<tr>
<td>Negotiation model</td>
<td>main</td>
</tr>
<tr>
<td>Local identifier</td>
<td>IP Address: 120.xx.xx.76</td>
</tr>
<tr>
<td>Remote ID</td>
<td>IP Address: 159.xx.xx.242</td>
</tr>
<tr>
<td>DH group</td>
<td>DH2</td>
</tr>
<tr>
<td>IKE SA Lifetime</td>
<td>86400</td>
</tr>
<tr>
<td rowspan="7">IPsec</td>
<td>Encryption algorithm</td>
<td>AES-128</td>
</tr>
<tr>
<td>Verification algorithm</td>
<td>MD5</td>
</tr>
<tr>
<td>Packet encapsulation Mode</td>
<td>Tunnel</td>
</tr>
<tr>
<td>Security protocol</td>
<td>ESP</td>
</tr>
<tr>
<td>PFS</td>
<td>disable</td>
</tr>
<tr>
<td>IPsec SA Lifetime (in seconds)</td>
<td>3600 s</td>
</tr>
<tr>
<td>IPsec SA Lifetime (in KB)</td>
<td>1843200 KB</td>
</tr>
<tr>
<td>Firewall</td>
<td>Interface</td>
<td>Nameif</td>
<td>outside</td>
</tr>
</table>


## Directions

<dx-tabs>
::: SPD\spolicy-based\sVPN\s(IKEv1)

1. Log in to the command-line interface of the firewall device.
   <dx-codeblock>
   :::  sh
   ssh -p admin@10.XX.XX.56        

# Use the SSH command to log in to the configuration interface of the firewall.

User Access Verification
Username: admin
Password: *******
Type help or '?' for a list of available commands.   

# Enter the username and password to enter the user mode.

ASA>  
ASA> enable  
Password:       

# Input “enable” and its password to enter the privileged EXEC mode in which you can view information only.

ASA# conf t   
ASA(config ter)#

# Input “config ter” to enter the global mode in which you can configure the firewall.

:::
</dx-codeblock>

2. Configure the firewall interface.
   In the global mode, configure the firewall interface that connects to Tencent Cloud.
   <dx-codeblock>
   :::  sh
   interface GigabitEthernet0/0
   nameif outside  # Specify the security domain of the interface.
   security-level 0  # Specify the security domain level of the interface.
   ip address 120.XX.XX.76 255.255.255.252  # Configure the local public IP address of the VPN tunnel.
   :::
   </dx-codeblock>

3. Configure an ISAKMP policy.
   <dx-codeblock>
   :::  sh
   crypto ikev1 enable outside  # Enable IKE on the “outside” interface.
   crypto ikev1 policy 10  # Define the phase 1 negotiation policy for IKEv1. Enter a number between 1-65535. The smaller the number, the higher the priority. The number 10 is used here.
   authentication pre-share  # Set the authentication method to pre-shared keys.
   encryption AES-128  # Specify the packet encapsulation encryption algorithm for the phase 1 negotiation. It defaults to “AES-128”.
   hash MD5  # Set the hash algorithm to “MD5” for the IKE policy. It defaults to “SHA”.
   group 2  # Use Diffie-Hellman group 2 for the IKE policy. It defaults to “group 2”.
   lifetime 86400  # Specify the SA lifetime. It defaults to “86400” seconds.
   :::
   </dx-codeblock>

4. Configure the pre-shared key.
   <dx-codeblock>
   :::  sh
   tunnel-group 159.XX.XX.242 type ipsec-l2l  # Create a point-to-point IPsec tunnel group.
   tunnel-group 159.XX.XX.242 ipsec-attributes  # Configure the tunnel group attributes, and specify the pre-shared key.
   ikev1 pre-shared-key tencent@123  # Enter letters, numbers or strings as the key, which contains 1-128 characters.
   :::
   </dx-codeblock>

5. Configure the IPsec security protocol.
   <dx-codeblock>
   :::  sh
   crypto ipsec ikev1 transform-set TS esp-aes esp-md5-hmac  # Specify the encryption algorithm and hash algorithm for the phase 2 IPsec negotiation.
   :::
   </dx-codeblock>

6. Configure ACL.
   <dx-codeblock>
   :::  sh
   access-list INTERESTING extended permit ip 172.XX.XX.0 255.255.0.0 10.1.1.0 255.255.255.0  # Configure ACL to capture the data stream of the VPN tunnel.
   :::
   </dx-codeblock>

7. Configure an IPsec policy.
   <dx-codeblock>
   :::  sh
   crypto map CMAP 1 match address INTERESTING  # Use ACL to allow the packets that meet the source or destination IP range requirements of the ACL to flow in the VPN tunnel.
   crypto map CMAP 1 set peer 159.XX.XX.242  # Set the public IP address of the destination VPN to which the IPsec-protected traffic can be forwarded. The public IP address of the Tencent Cloud VPN is used here.
   crypto map CMAP 1 set ikev1 transform-set TS  # Configure an IKEv1 protocol for the crypto map entry.
   crypto map CMAP 1 set security-association lifetime seconds 3600  # Configure a SA lifetime.
   :::
   </dx-codeblock>

8. Apply the IPsec policy.
   <dx-codeblock>
   :::  sh
   rypto map CMAP interface outside  # Apply the crypto map configured in the previous step to the “outside” interface.
   :::
   </dx-codeblock>

9. Configure static routes.
   <dx-codeblock>
   :::  sh
   route outside 10.1.1.0 255.255.255.0 159.XX.XX.242 1  # Route the data of the IP range to be encrypted and protected to the IPsec tunnel, and configure the destination public IP of the VPN tunnel as the next hop.
   :::
   </dx-codeblock>

10. Test the VPN connectivity.
    You can use the `ping` command to test the VPN connectivity.
:::

::: Route-based\sVPN\s(IKEv1)

1. Log in to the command-line interface of the firewall device.
   <dx-codeblock>
   :::  sh
   ssh -p admin@10.XX.XX.56

# Use the SSH command to log in to the configuration interface of the firewall.

User Access Verification
Username: admin
Password: *******
Type help or '?' for a list of available commands.

# Enter the username and password to enter the user mode.

ASA>  
ASA> enable  
Password: 

# Input “enable” and its password to enter the privileged EXEC mode in which you can view information only.

ASA# conf t   
ASA(config ter)#

# Input “config ter” to enter the global mode in which you can configure the firewall.

:::
</dx-codeblock>

2. Configure the firewall interface.
   In the global mode, configure the firewall interface that connects to Tencent Cloud.
   <dx-codeblock>
   :::  sh
   interface GigabitEthernet0/0
   nameif outside  # Specify the security domain of the interface.
   security-level 0  # Specify the security domain level of the interface.
   ip address 120.XX.XX.76 255.255.255.252  # Configure the local public IP address of the VPN tunnel.
   :::
   </dx-codeblock>
3. Configure an ISAKMP policy.
   <dx-codeblock>
   :::  sh
    crypto ikev1 policy 10  # Define the phase 1 negotiation policy for IKEv1. Enter a number between 1-65535. The smaller the number, the higher the priority. The number 10 is used here.
    authentication pre-share  # Set the authentication method to pre-shared keys.
    encryption AES-128  # Specify the packet encapsulation encryption algorithm for the phase 1 negotiation. It defaults to “AES-128”.
    hash MD5  # Set the hash algorithm to “MD5” for the IKE policy. It defaults to “SHA”.
    group 2  # Use Diffie-Hellman group 2 for the IKE policy. It defaults to “group 2”.
    lifetime 86400  # Specify the SA lifetime. It defaults to “86400” seconds.
   :::
   </dx-codeblock>
4. Configure the pre-shared key.
   <dx-codeblock>
   :::  sh
   tunnel-group 159.XX.XX.242 type ipsec-l2l  # Create a point-to-point IPsec tunnel group.
   tunnel-group 159.XX.XX.242 ipsec-attributes  # Configure the tunnel group attributes, and specify the pre-shared key.
    ikev1 pre-shared-key tencent@123  # Enter letters, numbers or strings as the key, which contains 1-128 characters.
   :::
   </dx-codeblock>
5. Configure the IPsec security protocol.
   <dx-codeblock>
   :::  sh
   crypto ipsec ikev1 transform-set TS esp-aes esp-md5-hmac  # Specify the encryption algorithm and hash algorithm for the phase 2 IPsec negotiation.
   :::
   </dx-codeblock>

6. Configure an IPsec policy.
   <dx-codeblock>
   :::  sh
   crypto ipsec profile PROFILE1
   set ikev1 transform-set TS  # Specify an IKEv1 IPSec proposal policy for the crypto map entry.
   set security-association lifetime kilobytes 1843200  # Specify the data stream in kilobytes allowed between source and destination VPNs during the SA lifetime.
   set security-association lifetime seconds 3600  # Set the SA lifetime. The default value is 4,608,000 kilobytes or 28,800 seconds.
   :::
   </dx-codeblock>

7. Apply the IPsec policy.
   <dx-codeblock>
   :::  sh
   interface Tunnel100
   tunnel source interface outside  # Configure the source VPN that comes from the “outside” interface. 
   tunnel destination 159.XX.XX.242  # Configure the public IP address of the destination VPN. The public IP address of Tencent Cloud VPN is used here.
   tunnel mode ipsec ipv4  # Configure the protocol for the tunnel interface.
   tunnel protection ipsec profile PROFILE1  # Use the IPsec policy to protect data passing through the tunnel interface.
   :::
   </dx-codeblock>

8. Configure static routes.
   <dx-codeblock>
   :::  sh
   route vti 10.1.1.0 255.255.255.0 159.XX.XX.242   # Route the packets to be encrypted and protected to the tunnel interface.
   :::
   </dx-codeblock>
9. Test the VPN connectivity.
   You can use the `ping` command to test the VPN connectivity.
   :::

::: SPD\spolicy-based\sVPN\s(IKEv2)

1. Log in to the command-line interface of the firewall device.
   <dx-codeblock>
   :::  sh
   ssh -p admin@10.XX.XX.56

# Use the SSH command to log in to the configuration interface of the firewall.

User Access Verification
Username: admin
Password: *******
Type help or '?' for a list of available commands.

# Enter the username and password to enter the user mode.

ASA>  
ASA> enable  
Password: 

# Input “enable” and its password to enter the privileged EXEC mode in which you can view information only.

ASA# conf t   
ASA(config)#

# Input “config ter” to enter the global mode in which you can configure the firewall.

:::
</dx-codeblock>

2. Configure the firewall interface.
   In the global mode, configure the firewall interface that connects to Tencent Cloud.
   <dx-codeblock>
   :::  sh
   interface GigabitEthernet0/0
   nameif outside  # Specify the security domain of the interface.
   security-level 0  # Specify the security domain level of the interface.
   ip address 120.XX.XX.76 255.255.255.252  # Configure the local public IP address of the VPN tunnel.
   :::
   </dx-codeblock>

3. Configure an ISAKMP policy.
   <dx-codeblock>
   :::  sh
   crypto ikev2 enable outside  # Enable IKEv2 on the “outside” interface.
   crypto ikev1 policy 10  # Define the phase 1 negotiation policy for IKEv2. Enter a number between 1-65535. The smaller the number, the higher the priority. This document uses 10.
   authentication pre-share  # Set the authentication method to pre-shared keys.
   encryption AES-128  # Specify the packet encapsulation encryption algorithm for the phase 1 negotiation. It defaults to “AES-128”.
   integrity MD5  #   # Set the hash  algorithm to “MD5” for the IKE policy. It defaults to “SHA”.
   group 2  # Use Diffie-Hellman group 2 for the IKE policy. It defaults to “group 2”.
   prf sha # Set the encryption algorithm.
   lifetime seconds 86400  # Set the SA lifetime. It defaults to 86400s.
   :::
   </dx-codeblock>

4. Configure a group policy.
   <dx-codeblock>
   :::  sh
   group-policy group_policy internal  # Set a group policy for devices.
   group-policy group_policy attributes  # Set the group policy attributes.
   vpn-tunnel-protocol ikev2 # Set IKEv2 protocol for vpn-tunnel.
   :::
   </dx-codeblock>

5. Configure the pre-shared key.
   <dx-codeblock>
   :::  sh
   tunnel-group 159.XX.XX.242 type ipsec-l2l  # Create a point-to-point IPsec tunnel group.
   tunnel-group 159.XX.XX.242 general-attributes default-group-policy group_policy  # Apply the group policy defined in the previous step.
   tunnel-group 159.XX.XX.242 ipsec-attributes  # Configure the tunnel group attributes, and specify the pre-shared key.
   ikev2 remote-authentication pre-shared-key tencent@123
   ikev2 local-authentication pre-shared-key tencent@123 # Enter letters, numbers or strings as the key, which contains 1-128 characters.
   :::
   </dx-codeblock>
6. Specify the IPsec protocol.
   <dx-codeblock>
   :::  sh
   crypto ipsec ikev2 ipsec-proposal ikev2_proposal  # Specify the encryption algorithm and hash algorithm for the phase 2 IPsec negotiation.
   protocol esp encryption aes-128  # Configure an encryption algorithm.
   protocol esp integrity sha-1 # Configure an integrity checking algorithm.
   :::
   </dx-codeblock>
7. Configure ACL.
   <dx-codeblock>
   :::  sh
   access-list INTERESTING extended permit ip 172.XX.XX.0 255.255.0.0 10.1.1.0 255.255.255.0  # Configure ACL to capture the data stream of the VPN tunnel.
   :::
   </dx-codeblock>
8. Configure an IPsec policy.
   <dx-codeblock>
   :::  sh
   crypto map CMAP 1 match address INTERESTING  # Use ACL to allow the packets that meet the source or destination IP range requirements of the ACL to flow in the VPN tunnel.
   crypto map CMAP 1 set peer 159.XX.XX.242  # Set the public IP address of the destination VPN to which the IPsec-protected traffic can be forwarded. The public IP address of the Tencent Cloud VPN is used here.
   crypto map CMAP 1 set ikev2 ipsec-proposal ikev2_proposal # Configure an IKEv2 protocol for the crypto map entry.
   crypto map CMAP 1 set security-association lifetime seconds 3600 # Configure a SA lifetime.
   crypto map CMAP 1 set security-association lifetime kilobytes 1843200  # Specify the data stream in kilobytes allowed between source and destination VPNs during the SA lifetime. The default value is 4,608,000 kilobytes, and the default SA lifetime is 28,800 seconds.
   :::
   </dx-codeblock>
9. Apply the IPsec policy.
   <dx-codeblock>
   :::  sh 
   rypto map CMAP interface outside  # Apply the crypto map configured in the previous step to the “outside” interface.
   :::
   </dx-codeblock>
10. Configure static routes.
    <dx-codeblock>
    :::  sh
    route outside 10.1.1.0 255.255.255.0 159.XX.XX.242 1  # Route the data of the IP range to be encrypted and protected to the IPsec tunnel, and configure the destination public IP of the VPN tunnel as the next hop.
    :::
    </dx-codeblock>
11. Test the VPN connectivity.
    You can use the `ping` command to test the VPN connectivity.
    :::

::: Route-based\sVPN\s(IKEv2)

1. Log in to the command-line interface of the firewall device.
   <dx-codeblock>
   :::  sh
   ssh -p admin@10.XX.XX.56

# Use the SSH command to log in to the configuration interface of the firewall.

User Access Verification
Username: admin
Password: *******
Type help or '?' for a list of available commands.

# Enter the username and password to enter the user mode.

ASA>  
ASA> enable  
Password: 

# Input “enable” and its password to enter the privileged EXEC mode in which you can view information only.

ASA# conf t   
ASA(config ter)#

# Input “config ter” to enter the global mode in which you can configure the firewall.

:::
</dx-codeblock>

2. Configure the firewall interface.
   In the global mode, configure the firewall interface and tunnel interface used to connect Tencent Cloud.
   <dx-codeblock>
   :::  sh
   interface GigabitEthernet0/0
   nameif outside  # Specify the security domain of the interface.
   security-level 0 # Specify the security domain level of the interface.
   ip address 120.XX.XX.76 255.255.255.252  # Configure the public IP address of the Tencent Cloud VPN to connect.
   interface Tunnel100
   nameif vti
   ip address 172.XX.XX.2 255.255.255.0 # Set an IP address to activate the tunnel interface.
   :::
   </dx-codeblock>

3. Configure an ISAKMP policy.
   <dx-codeblock>
   :::  sh
   crypto ikev2 policy 1  # Define the phase 1 negotiation policy for IKEv2. Enter a number between 1-65535. The smaller the number, the higher the priority. The number 1 is used here.
   encryption AES-128  # Set “AES-128” as the packet encapsulation encryption algorithm for the phase 1 negotiation. It defaults to “AES-128”.
   integrity MD5  /# Set the hash algorithm to “MD5” for the IKE policy. It defaults to “SHA”.
   group 2  # Use Diffie-Hellman group 2 for the IKE policy. It defaults to “group 2”.
   prf sha # Configure the encryption algorithm.
   lifetime seconds 86400  # Configure the SA lifetime (namely, lifecycle). It defaults to 86400s.
   :::
   </dx-codeblock>
4. Configure a group policy.
   <dx-codeblock>
   :::  sh
   group-policy group_policy internal  # Set a group policy for devices.
   group-policy group_policy attributes  # Set the group policy attributes.
   vpn-tunnel-protocol ikev2 # Set IKEv2 protocol for vpn-tunnel.
   :::
   </dx-codeblock>
5. Configure the pre-shared key.
   <dx-codeblock>
   :::  sh
   tunnel-group 159.XX.XX.242 type ipsec-l2l  # Create a point-to-point IPsec tunnel group.
   tunnel-group 159.XX.XX.242 general-attributes default-group-policy group_policy  # Apply the group policy defined in the previous step.
   tunnel-group 159.XX.XX.242 ipsec-attributes  # Configure the tunnel group attributes, and specify the pre-shared key.
   ikev2 remote-authentication pre-shared-key tencent@123
   ikev2 local-authentication pre-shared-key tencent@123 # Enter letters, numbers or strings as the key, which contains 1-128 characters.
   :::
   </dx-codeblock>
6. Specify the IPsec protocol.
   <dx-codeblock>
   :::  sh
   crypto ipsec ikev2 ipsec-proposal ikev2_proposal  # Specify the encryption algorithm and hash algorithm for the phase 2 IPsec negotiation.
   protocol esp encryption aes-128  # Specify an encryption algorithm.
   protocol esp integrity sha-1 # Specify an integrity checking algorithm.
   :::
   </dx-codeblock>
7. Configure an IPsec policy.
   <dx-codeblock>
   :::  sh
   crypto ipsec profile PROFILE1
   set ikev2 ipsec-proposal ikev2_proposal  # Configure an IKEv2 protocol for the crypto map entry.
   set security-association lifetime kilobytes 1843200  # Specify the data stream in kilobytes allowed between source and destination VPNs during the SA lifetime.
   set security-association lifetime seconds 3600  # Set the SA lifetime. The default value is 4,608,000 kilobytes or 28,800 seconds.
   :::
   </dx-codeblock>
8. Apply the IPsec policy.
   <dx-codeblock>
   :::  sh
   interface Tunnel100
   tunnel source interface outside  # Configure the source VPN that comes from the “outside” interface. 
   tunnel destination 159.XX.XX.242  # Configure the public IP address of the destination VPN. The public IP address of Tencent Cloud VPN is used here.
   tunnel mode ipsec ipv4  # Configure the protocol for the tunnel interface.
   tunnel protection ipsec profile PROFILE1  # Use the IPsec policy to protect data passing through the tunnel interface.
   :::
   </dx-codeblock>
9. Configure static routes.
   <dx-codeblock>
   :::  sh
   route vti 10.1.1.0 255.255.255.0 159.XX.XX.242   # Route the packets to be encrypted and protected to the tunnel interface.
   :::
   </dx-codeblock>

10. Test the VPN connectivity.
   You can use the `ping` command to test the VPN connectivity.
   :::
   </dx-tabs>

