CVMs in a Tencent Cloud VPC support DHCP. The configurable DHCP options include DNS address and domain name. This document describes how to modify the DNS address and domain name of a VPC.
>?
>+ Dynamic Host Configuration Protocol (DHCP) is a LAN network protocol that defines the standard for transferring configuration information to TCP/IP network servers. 
>+ For now, VPCs created before April 1, 2018 do not support DHCP features. If you cannot modify the DNS address and domain name in the console, it means that your VPC does not support these features.

## Notes
The new configurations will take effect on all CVMs in the VPC.
 + For newly created CVMs, the modified configurations take effect immediately.
 + For existing CVMs, the modified configurations take effect after the CVMs or network services are restarted.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the **VPC** page.
3. Click the VPC ID to access the **Basic Information** page.
4. Click the edit icon to modify DNS and domain name respectively.
   + DNS: DNS server addresses
     >?
     >+ The Tencent Cloud default DNS is “183.60.83.19” and “183.60.82.98”. If the default DNS is not used, internal services such as Windows activation, NTP, and YUM will be unavailable.
     + DNS supports a maximum of four IP addresses. Separate IPs with commas. Note that certain operating systems might be unable to support four DNS addresses.
   + Domain Name: CVM hostname suffix, such as “example.com”. You can enter up to 60 characters, or keep the default configuration if you don’t have special requirements.
    ![](https://main.qcloudimg.com/raw/50129c5b14c7c6d5923263719eec5bd2.png)
