After your domain name is connected to CDN, the system automatically assigns you a CNAME domain name suffixed with `.cdn.dnsv1.com`. You can check it on the [Domain Management](https://console.cloud.tencent.com/cdn/access) page in the CDN console. The CNAME domain name cannot be accessed directly. You need to complete the CNAME configuration with the domain name service provider first. When the configuration takes effect, you can use the CDN acceleration service.
![img](https://main.qcloudimg.com/raw/073b948565743f7947aae8503eef995d.png)

## Configuration Directions

This document describes DNSPod CNAME configuration directions.

### Settings for Tencent Cloud

>? In domain name resolution, record types have priority. If the host records are the same, some record types cannot exist in a split zone at the same time, otherwise there will be conflicts. As a CNAME record conflicts with other types of records, you need to delete other types of records first for CNAME record configuration. For more information, please see [How to Fill In Host Name and Record Value](https://cloud.tencent.com/document/product/302/3468#.E4.B8.BA.E4.BB.80.E4.B9.88.E6.B7.BB.E5.8A.A0.E8.A7.A3.E6.9E.90.E8.AE.B0.E5.BD.95.E7.9A.84.E6.97.B6.E5.80.99.E6.8F.90.E7.A4.BA-.26quot.3B.E8.AE.B0.E5.BD.95.E6.9C.89.E5.86.B2.E7.AA.81.26quot.3B-.EF.BC.9F).

If your DNS service provider is DNSPod, please log in to the [DNSPod console](https://console.dnspod.cn/dns/list), find the row of the domain name for which to add a CNAME record in the list, and click the domain name to enter the "Add Record" page. You can add a CNAME record as follows:

![img](https://main.qcloudimg.com/raw/36f84a0d21b51bc56d79544943f0f752.png)

1. Enter the sub-domain name for the host record (for example, if you want to add the resolution for `www.123.com`, you only need to enter `www` as the host record; if you want to add the resolution for `123.com`, the host record can be left empty and the system will automatically enter an `@` into the input box. A CNAME record with `@` will affect the proper resolution of the MX record, so please be cautious when adding it).
2. Record type is CNAME.
3. Set the split zone type (required by default; if it is left empty, requests of some users may not be resolved. In the figure above, the default value means that all users except those of China Unicom will be pointed to `1.com`).
4. The record value is the domain name pointed to by CNAME resolution. Only a domain name can be entered. After the record is generated, a `.` will be automatically added after the domain name, which is normal.
5. Set the weight of the record.
6. TTL is not required as the system will automatically generate one. The default value is 600 seconds. TTL is Time to Live for cache. The smaller the value is, the faster the modified record takes effect globally.

## Verifying the Effect of a CNAME Record

The time it takes for a CNAME record to take effect varies by DNS service provider. It is generally within half an hour. You can also check whether the CNAME record is in effect by running `nslookup` or `dig`.

E.g., `nslookup -qt=cname <acceleration domain name>` or `dig <acceleration domain name>`