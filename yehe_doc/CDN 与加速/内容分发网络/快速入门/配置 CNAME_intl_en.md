After your domain name is connected to CDN, you will be given a CNAME domain name suffixed with `.cdn.dnsv1.com`, which can be viewed on the [Domain Management](https://console.cloud.tencent.com/cdn/domains) page in the CDN console. To make the CNAME domain name accessible, you need to complete the CNAME configuration at your domain name service provider first. When the configuration takes effect, you can use the CDN acceleration service.
![img](https://main.qcloudimg.com/raw/073b948565743f7947aae8503eef995d.png)

## Configuration Directions

This document provides CNAME configuration directions on Tencent Cloud and Alibaba Cloud:

- [Settings on Tencent Cloud](#m1)
- [Settings on Alibaba Cloud](#m2)

[](id:m1)
### Settings on Tencent Cloud

> !Records of different types have different priorities. For the same host, some record types cannot exist at the same time. CNAME type conflicts with any other record types. You need to delete records of other types to add CNAME records.


1. Log in to the [DNSpod](https://www.dnspod.com/Products/dns/list), click the desired domain name in **My Domains** tab.
 
2. Click **Add Records** and then configure it as instructed below:
   ![img](https://main.qcloudimg.com/raw/36f84a0d21b51bc56d79544943f0f752.png)
	
	- **Host**: Enter the sub-domain name. For example, if you want to add the resolution for `www.dnspod.com`, select **www** as the host record. If you want to add the resolution for `dnspod.com`, select **@**.
	- **Type**: Select **CNAME**.
	- **Split Zone**: Select **Default**. DNSPod offers various split zone options for you to specify records for specific users. For more information, please see [Split Zone Description](https://docs.dnspod.cn/dns/5f4775898ae73e11c5b01afc/).
	- **Value**: Enter the target domain name (usually the CNAME, e.g., `xxx.xxx.com.cdn.dnsv1.com`). After the record is generated, a `.` will be automatically added after the domain name, which is normal.
	- **Weight**: Different record values in the same split zone of a host record can be set with different weights, so that resolution will be returned according to their weight ratios.
		Please enter an integer between 0 and 100.
	- **MX**: Priority of MX record. You can leave it blank.
	- **TTL**: TTL (Time to Live) determines how long to cache either a query or content. The smaller the value is, the less the time cost for record changes to take effect globally. The default value is 600 seconds.
3. Click **Confirm** to finish the configuration.

   

####  Additional settings
- To enable acceleration service for the whole website, you can set the **Split Zone** of a host record as **Default**.
For example, if you want to point all users to `1.com`, you can configure a CNAME record with **Default** as the split zone and `1.com` as the value.
![img](https://main.qcloudimg.com/raw/0c146a23008acc3c0e4884aa1c4d3a3c.png)

- You can also enable acceleration service for a specified split zone.
For example, if you want to point CMCC users to `1.com` and CUCC users to `2.com`, you can configure two CNAME records: one with **CMCC** as the split zone and `1.com` as the value, another one with **CUCC** as the split zone and `2.com` as the value.
 ![](https://main.qcloudimg.com/raw/ecf4d1ad94eaf897473647459b923209.png)

>?For more information on split zone configurations, please see [Split Zone Description](https://docs.dnspod.cn/dns/5f4775898ae73e11c5b01afc/).


[](id:m2)
### Settings on Alibaba Cloud

If your DNS service provider is Alibaba Cloud, you can add a CNAME record as follows.

1. Log in to the Alibaba Cloud DNS console.
2. Click the domain name to be resolved to enter the resolution record page.
3. Click **Add Record**.
4. To set a CNAME resolution record, select **CNAME** as the record type. Enter the host record as needed (e.g., `www`), which is the domain name prefix. Enter the domain name pointed to by the current domain name as the record value. Retain the default settings for ISP Line and TTL.
![img](https://main.qcloudimg.com/raw/6b8bb9ce4f998b8d17ca27fd10512dc6.png)
5. Finally, click **Confirm**.



## Verifying a CNAME Record

The time it takes for a CNAME record to take effect varies by DNS service provider. It is generally within 30 minutes. You can also check whether the CNAME record is in effect by running `nslookup` or `dig`. If the CNAME record response is the CNAME configured, it indicates that the configuration is successful and the acceleration is enabled.

- `nslookup -qt=cname <acceleration domain name>`
  ![img](https://main.qcloudimg.com/raw/89faaf228a2b88e23b82d0a839367c76.png)
- `dig <acceleration domain name>`
  ![img](https://main.qcloudimg.com/raw/2ba5ec76f1671c3b8ee345cef896de10.png)
