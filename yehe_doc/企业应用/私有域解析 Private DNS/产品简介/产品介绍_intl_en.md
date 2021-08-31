## Overview
Private DNS is a private DNS management service based on Tencent Cloud Virtual Private Cloud (VPC). It allows you to quickly build a DNS system in one or more custom VPCs and easily use private DNS records to manage Tencent Cloud resources associated with the VPCs that are externally inaccessible, such as CVM, CLB, CDN, and COS.


## Features

### Private DNS
The private domain list contains the private domain name resource records that you need to manage. You can create multiple private domain names and add the following types of DNS records for them:


| Record Type | Description |
| :------- | :----------------------------------------------------------- |
| A        | It is used to specify the IPv4 address (such as `8.8.8.8`) of a domain. If you want to point a domain to an IP address, you need to add an A record. |
| AAAA     | It is used to specify the IPv6 address (such as `ff06:0:0:0:0:0:0:c3`) of a domain. If you want to point a domain to an IPv6 address, you need to add an AAAA record. |
| CNAME    | It is used to point a domain to another domain.                                 |
| MX       | If you want to set up your mailbox so that it can receive emails, you need to add an MX record.       |
| TXT      | You can enter anything in this record with a length limit of 255 characters. Most TXT records are used as SPF records (for anti-spam). |
| PTR      | It reversely maps an IP address to a domain.                                   |

### Associated VPC
You can associate a private domain name with one or more VPCs that need to be configured so as to map it to IP addresses.
>?Private domain names with the same name cannot be associated with the same VPC. For example, if there are two instances of `tencent.com` at the same time, you cannot associate both of them with the same VPC.

### Reverse DNS
Reverse DNS refers to mapping an IP address to a domain name, that is, the private domain name pointed to by the IP address is obtained by querying the PTR record of the IP address.

### Subdomain recursive DNS
With the aid of Private DNS, you can implement private network hijacking in VPCs without relying on the authoritative DNS. In certain scenarios, some domain names need to be opened to access public IPs in private environments. Private DNS can achieve dual DNS for one single domain name by working with the authoritative DNS and thus achieve interconnection in hybrid clouds, that is, you can use `nslookup` in CMD to resolve the same domain name and get different IP addresses.

### Custom private domain
CVM instance name management can be well planned to make the instance purposes and information easier to understand and more user-friendly.

### Internal API call
API calls are managed internally to avoid the troubles caused by IP address changes to the API use, which makes OPS easier.

### Internal domain name security isolation
The core system privacy protection feature ensures that the domain names of internal core systems are not exposed to the internet and thus improves their security.