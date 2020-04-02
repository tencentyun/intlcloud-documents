The dynamic host configuration protocol (DHCP) is a LAN protocol that defines the standard for transferring configuration information to TCP/IP network servers.
CVMs in a Tencent Cloud VPC support DHCP. Configurable DHCP options include the DNS address and domain name. You can configure the DNS address and domain name in the VPC configuration. These settings will take effect on all CVMs in the VPC.

>
> - VPC instances created before April 1, 2018 currently do not support DHCP features. If you cannot modify the DNS address and domain name in the console, that means your VPC does not support these features.
> - After the configuration is modified, it takes effect on all CVMs within the VPC:
> - For newly created CVMs, the modified configuration takes effect immediately.
> - For existing CVMs, the modified configuration takes effect after the CVMs or network services are restarted.

## Steps
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click the ID of the VPC that needs to be modified to go to the details page, where you can configure the DNS address and domain name in the basic information section.
 - DNS address
	 - DNS supports a maximum of four IP addresses. Separate multiple IP addresses with commas.
	 - Although up to four IP addresses can be specified for DNS, some operating systems may not be able to support four DNS addresses.
	 - The default DNS addresses of Tencent Cloud are `183.60.83.19` and `183.60.82.98`. If you do not use these default DNS addresses, you cannot use internal services such as Windows activation, NTP, and YUM.
 - Domain name
	 - The CVM hostname suffix, such as `example.com`.

![](https://main.qcloudimg.com/raw/0860fef79e695941eede5938fa6f4b8a.png)
