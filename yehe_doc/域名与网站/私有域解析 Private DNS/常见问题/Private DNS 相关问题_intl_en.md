### What is Private DNS?
Private DNS is a private domain DNS and management service based on Tencent Cloud Virtual Private Cloud (VPC) that provides highly secure private DNS services.

### How do I activate Private DNS?
When you access the Private DNS console for the first time, you need to activate the service. For more information, please see [Activating Private DNS](https://cloud.tencent.com/document/product/1338/50533). After successful activation, you can use it normally.

### Do I need to modify the DNS settings of my CVM instances to use Private DNS?
No. To use the Private DNS service, you only need to [activate it](https://cloud.tencent.com/document/product/1338/50533). You don't need to modify the DNS settings of Tencent Cloud resources such as CVM instances.

### What are the differences between Private DNS and DNSPod?
- **DNSPod**
DNSPod is a DNS service offered by Tencent Cloud based on the industry-leading DNS technologies, which provides reliable and stable authoritative DNS services. DNSPod is a leading DNS service provider with a decade of experience in domain name resolution.

- **Private DNS**
Private DNS is a private DNS service based on Tencent Cloud VPC. It enables you to flexibly customize any private domain names that you need to use in your VPCs without caring about whether the domain names have been registered by others or worrying that they can be queried outside VPCs. This makes recording and management much easier.

### What is the biggest difference between Private DNS and DNSPod?
The biggest difference between Private DNS and DNSPod is that the former is DNS in VPC (LAN), while the latter is DNS on the internet (WAN).

### Do I need to register custom private domains?
Private domains created through Private DNS are virtual domain names that only take effect in the associated VPCs. You don't need to register them at a domain name registrar. You can create custom standard domain names that comply with applicable specifications.

### Can I create Chinese domain names in Private DNS?
Yes, but they need to comply with the IANA standards. For more information, please see [Root Zone Database](https://www.iana.org/domains/root/db).

### Does Private DNS support wildcard?
Wildcard is supported only after subdomain recursive DNS is enabled.

### How do I configure reverse DNS for private domains?
You need to create a private domain ending with `1- to 3-digit IP range + in-addr.arpa` and add a PTR record first.

### How do I configure private domains so that they can support both private network DNS and public network DNS?
You can create private domains the same as public domains and enable subdomain recursive DNS, so that the private domains can be resolved on both the private and public networks.

### Is the DNS of private domains within the same region or across regions?
Private domains only take effect in the associated VPCs. You can associate one or multiple VPCs in the same region, which you can choose according to your needs.

### Which record types does Private DNS support?
Currently, Private DNS supports A, AAAA, CNAME, TXT, MX, and PTR records.

### Does Private DNS support round-robin DNS?
All DNS record types except PTR in Private DNS support round-robin DNS.

### Does Private DNS support IPv6?
Yes. Domain names can be resolved to IPv6 addresses by setting an AAAA record.

### Which regions does Private DNS support?
Currently supported regions include Beijing, Shanghai, Guangzhou, Chongqing, Chengdu, and Silicon Valley, and more regions will be supported in the future.

### Does Private DNS support API calls?
Yes. It has been connected to TencentCloud API, so you can call it by yourself.

### Does Private DNS support sub-account and collaborator authorization?
Yes. Private DNS has been connected to CAM, where the root account can authorize sub-accounts and collaborators separately for service use.

### Will overdue payments affect the effect of DNS?
After a payment becomes overdue for more than 24 hours, the private domains under your account will be locked without affecting DNS. If the payment is overdue for more than 7 days, the private domains will be locked with DNS stopped.

### After a VPC is deleted, will it be synchronously disassociated from private domains?
No. You need to go to the Private DNS console to manually disassociate it.

### Does Private DNS have the remarks feature?
Yes. You can set private domain remarks according to your needs. You can also search for private domains, which makes it easier for you to manage your private domains.