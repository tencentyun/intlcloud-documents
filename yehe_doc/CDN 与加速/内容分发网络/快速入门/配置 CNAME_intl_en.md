After your domain name is connected to CDN, the system will automatically assign you a CNAME domain name suffixed with `.cdn.dnsv1.com` which can be viewed on the [Domain Management](https://console.cloud.tencent.com/cdn/domains) page in the CDN console. It cannot be accessed directly. Instead, you need to complete the CNAME configuration with the domain name service provider first. When the configuration takes effect, you can use the CDN acceleration service.
![img](https://main.qcloudimg.com/raw/6e3efa29d65ec9a35af7c1a762ebfcb8.png)

## Configuration Directions

This document provides CNAME configuration directions on Tencent Cloud:

- [Settings on Tencent Cloud](#m1)
- [Settings on Alibaba Cloud](#m2)

<span ID ="m1"></span>

### Settings on Tencent Cloud

> ! There are differences in priority between various record types during domain name resolution. If the host records are identical, different types of records cannot coexist in the same split zone; otherwise, a conflict will occur. A CNAME record conflicts with records of any other types; therefore, you need to delete other records first before configuring CNAME.

1. Log in to the [DNSPod console](https://console.cloud.tencent.com/domain) and click **Resolve** on the right of the domain name to be resolved.
2. On the DNSPod page, click **Add Records** and then configure it as instructed below.
![img](https://main.qcloudimg.com/raw/36f84a0d21b51bc56d79544943f0f752.png)
	- **Host**: Enter the sub-domain name. For example, if you want to add the resolution for `www.dnspod.com`, you only need to enter `www` as the host record. If you want to add the resolution for `dnspod.com`, select `@`. Please note that a CNAME record with `@` will affect the proper resolution of the MX record.
	- **Type**: Select **CNAME**.
	- **Split Zone**: Select **Default**. DNSPod offers various split zone options for you to specify records for specific users. 
	- **Value**: Enter the domain name pointed to by the CNAME. Only a domain name can be entered. After the record is generated, a `.` will be automatically added after the domain name, which is normal.
	- **Weight**: Different record values in the same split zone of a host record can be set with different weights, so that resolution will be returned according to their weight ratios. Please enter an integer between 0 and 100.
	- **MX**: Do not enter content.
	- **TTL**: It refers to the time to live. The smaller the value is, the less the time cost for record changes to take effect globally. The default value is 600 seconds.

### Split zone-based acceleration on Tencent Cloud

- To enable acceleration service for the whole website, you can set the split zone of a host record as **Default**.
	 For example, if you want to point all users to `1.com`, you can configure a CNAME record with **Default** as the split zone and `1.com` as the value.
![img](https://main.qcloudimg.com/raw/0c146a23008acc3c0e4884aa1c4d3a3c.png)
- You can also enable acceleration service for a specified split zone.
For example, if you want to point CUCC users to `2.com` and CMCC users to  `1.com`, you can configure two CNAME records: one with **CMCC** as the split zone and `1.com` as the value, another one with **CUCC** as the split zone and `2.com` as the value. 
![](https://main.qcloudimg.com/raw/ecf4d1ad94eaf897473647459b923209.png)

<span ID ="m2"></span>
### Settings on Alibaba Cloud

If your DNS service provider is Alibaba Cloud, you can add a CNAME record as follows.

1. Log in to the Alibaba Cloud DNS console.
2. Click the domain name to be resolved to enter the resolution record page.
3. Click **Add Record**.
4. To set a CNAME resolution record, select CNAME as the record type. Enter the host record as needed (e.g., `www`), which is the domain name prefix. Enter the domain name pointed to by the current domain name as the record value. Retain the default settings for **ISP Line** and **TTL**.
![img](https://main.qcloudimg.com/raw/6b8bb9ce4f998b8d17ca27fd10512dc6.png)
5. Finally, click **Confirm**.



<span ID ="m3"></span>



## Verifying the Effect of a CNAME Record

The time it takes for a CNAME record to take effect varies by DNS service provider. It is generally within half an hour. You can also check whether the CNAME record is in effect by running `nslookup` or `dig`.

- `nslookup -qt=cname <acceleration domain name>`
  
- `dig <acceleration domain name>`
  ![img](https://main.qcloudimg.com/raw/2ba5ec76f1671c3b8ee345cef896de10.png)
