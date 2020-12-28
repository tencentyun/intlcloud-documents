After your domain name is connected to CDN, the system automatically assigns you a CNAME domain name suffixed with `.cdn.dnsv1.com`. You can check it on the [Domain Management](https://console.cloud.tencent.com/cdn/access) page in the CDN console. The CNAME domain name cannot be accessed directly. You need to complete the CNAME configuration with the domain name service provider first. When the configuration takes effect, you can use the CDN acceleration service.
![img](https://main.qcloudimg.com/raw/073b948565743f7947aae8503eef995d.png)

## Configuration Directions

This document describes how to configure DNSPod CNAME.

### Settings on Tencent Cloud

>? Records of different types have different priorities. For the same host, some record types can not exist at the same time. CNAME type conflicts with any other record types. You need to delete records of other types to add CNAME records. 

If your DNS service provider is DNSPod, please log in to the [DNSPod console](https://console.dnspod.cn/dns/list), locate and click the desired domain name. In the "Add Record" page. You can add a CNAME record as follows:

![img](https://main.qcloudimg.com/raw/36f84a0d21b51bc56d79544943f0f752.png)

1. Enter the sub-domain name in **host** field. For example, if you want to add the resolution for `www.123.com`, you only need to enter `www` as the host record. If you want to add the resolution for `123.com`, leave **host** filed blank, and the system will automatically enter an `@`. Please note that a CNAME record with `@` will affect the proper resolution of the MX record. 
2. Choose **CNAME* in **Record type**.
3. Set the split zone type (required by default; if it is left empty, requests of some users may not be resolved. In the figure above, the default value means that all users except those of China Unicom will be pointed to `1.com`).
4. The record value is the domain name pointed to by CNAME resolution. Only a domain name can be entered. After the record is generated, a `.` will be automatically added after the domain name, which is normal.
5. Set the weight of the record.
6. TTL (Time to Live) is the cache period for the record. The smaller the value is, the faster the modified record takes effect globally. If you leave it blank, it defaults to 600 seconds. 

## Verifying the Effect of a CNAME Record

The time it takes for a CNAME record to take effect varies by DNS service provider. It is generally within half an hour. You can also check whether the CNAME record is in effect by running `nslookup` or `dig`.

E.g., `nslookup -qt=cname <acceleration domain name>` or `dig <acceleration domain name>`