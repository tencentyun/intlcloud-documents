Once your domain name is connected to CDN, the system will automatically assign it a CNAME domain name suffixed with `.cdn.dnsv1.com`, which can be viewed on the [Domain Management](https://console.cloud.tencent.com/cdn/access) page in the CDN Console. This domain name cannot be accessed directly before you complete the CNAME configuration at your domain name service provider. After the configuration takes effect, CDN can be used properly.
![](https://main.qcloudimg.com/raw/073b948565743f7947aae8503eef995d.png)

## Configuration Steps
This document provides CNAME configuration steps for Tencent Cloud, DNSPod, Wanwang, and Xinnet:
- [Settings for Tencent Cloud](#m1)
- [Settings for DNSPod](#m2)
- [Settings for Wanwang](#m3)
- [Settings for Xinnet](#m4)

<span ID ="m1"></span>
### Settings for Tencent Cloud
>!There are differences in priority between various record types during domain name resolution. If the host records are identical, different types of records cannot coexist on the same line; otherwise, a conflict will occur. A CNAME record conflicts with records of any other types; therefore, you need to delete other records first before configuring CNAME. For more information, please see [Why do I get a "record conflict" prompt when adding a resolution record?](https://intl.cloud.tencent.com/document/product/302/3468).



1. Log in to [Domain Name Service Console](https://console.cloud.tencent.com/domain), find the domain name for which to add a CNAME record in the list, and click **Resolve** in the "Operation" column.
![](https://main.qcloudimg.com/raw/5687364cbdec038240c9b37373524d39.png)
2. On the pop-up page, click **Add Record**.
 ![](https://main.qcloudimg.com/raw/88a0cda619aeaf1a88120ad5294250fa.png)
3. Enter the domain name prefix (such as www) in **Host Record**, set **Record Type** to CNAME, enter the CNAME domain name in **Record Value**, and click **Save** to add the CNAME record.
![](https://main.qcloudimg.com/raw/24ee35e7bba9d181abbdaf65fe7fc3cb.png)

<span ID ="m2"></span>
### Settings for DNSPod
Log in to the [DNSPod Console](https://console.dnspod.cn/dns/list), find the row of the domain name for which to add a CNAME record in the list, and click the domain name to enter the "Add Record" page. You can add a CNAME record as follows:
![](https://main.qcloudimg.com/raw/c5e256fcc42261105b674151aa6561a3.png)
1. Enter the sub-domain name for the host record (for example, if you want to add the resolution for `www.123.com`, you only need to enter `www` as the host record; if you want to add the resolution for `123.com`, the host record can be left blank and the system will automatically enter an `@` into the input box. A CNAME record with `@` will affect the proper resolution of the MX record, so please be cautious when adding it).
2. Set the record type to CNAME.
3. Set the line type (required by default; if left blank, requests of some users may not be able to be resolved. In the figure above, the default value means that all users except those of China Unicom will be pointed to `1.com`).
4. The record value is the domain name pointed to by CNAME resolution. Only a domain name can be entered. After the record is generated, a "." will be automatically added after the domain name, which is normal.
5. MX priority does not need to be entered.
6. TTL does not need to be entered. The system will automatically generate it when adding the record. The default is 600 seconds (TTL is the cache time. The smaller the value, the faster the change to the record will take effect in various regions).



<span ID ="m3"></span>
### Settings for Wanwang
If your DNS service provider is Wanwang, you can add a CNAME record in the following steps:
1. Log in to the Wanwang Member Center.
2. On the left sidebar, click **Product Management** > **My Cloud Resolution** to enter the cloud resolution list page.
3. Click the domain name to be resolved to enter the resolution record page.
4. On the resolution record page, click "Add Resolution" to set a resolution record.
![](https://main.qcloudimg.com/raw/54825b2a66e6752cd451d79d72929833.png)
5. To set a CNAME resolution record, select CNAME as the record type. Enter the host record as needed (such as `www`), which is the domain name prefix. Enter the domain name pointed to by the current domain name as the record value. Retain the default settings of the resolution line and TTL.
![](https://main.qcloudimg.com/raw/b321d20332ca1b93eb78376cac43683b.png)
6. After completing the settings, click **Save**.

<span ID ="m4"></span>
### Settings for Xinnet
If your DNS service provider is Xinnet, you can add a CNAME record in the following steps:
**Set an alias (CNAME record)**
CNAME record, aka alias record, allows you to map multiple names to the same computer and is generally used for computers providing both WWW and mail services. For example, a computer named `host.mydomain.com` (A record) provides both WWW and mail server. To facilitate user access, you can set two aliases (CNAME records) for this computer: `WWW` and `MAIL`, as shown below:
![](https://main.qcloudimg.com/raw/2e93d51c7fe8502670475d71bbfb20cb.png)
## Verifying the Effect of CNAME Record
The time it takes for a CNAME record to take effect varies by DNS service provider. It is generally within half an hour. You can also check whether the CNAME record is in effect by running `nslookup` or `dig`.
- `nslookup -qt=cname <acceleration domain name>`
![](https://main.qcloudimg.com/raw/ed15d49b7d2fee9cf8830d4bf9ca51a2.png)
- `dig <acceleration domain name>`
![](https://main.qcloudimg.com/raw/2ba5ec76f1671c3b8ee345cef896de10.png)

