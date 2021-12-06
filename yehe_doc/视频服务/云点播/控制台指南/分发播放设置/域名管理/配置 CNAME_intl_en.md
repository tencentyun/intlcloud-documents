After you add your domain name to VOD, the system will automatically assign you a CNAME domain name (suffixed with `.cdn.dnsv1.com`), which you can check on [Domain Management](https://console.cloud.tencent.com/vod/distribute-play/domain ) in the VOD console. The automatically assigned CNAME domain name cannot be accessed before you complete the CNAME configuration at your DNS service provider.

![](https://qcloudimg.tencent-cloud.cn/raw/9ddc932f9b5072705d5d155f7ed2c8b5.png)
## Settings for Tencent Cloud
If your DNS service provider is Tencent Cloud, use the following steps to add a CNAME record:
1. Log in to the [Domains console](https://console.cloud.tencent.com/domain) and click **Resolve** on the right of the domain name to be resolved.
2. After you are directed to the **Record Management** page of the specified domain name, click **Add Record**.
3. In the pop-up window, set the **Record Type** to CNAME, enter the domain name prefix (such as `www`) in **Host Record**, enter the CNAME domain name in **Record Value**, and click **Confirm** to add a CNAME record.

	1. Enter the subdomain name for the host record. For example, if you want to resolve `www.123.com`, you only need to enter `www` as the host record; if you want to resolve `123.com`, you can leave the host record empty and the system will automatically enter an `@`. A CNAME record with `@` will affect the resolution of the MX record.
	2. Select **CNAME** as the record type.
	3. Set the split zone type (required by default; if it is left empty, requests of some users may not be resolved. In the figure below, the default value means that all users except those of China Unicom will be pointed to `1.com`).
	4. Set the record value to the domain name pointed to by CNAME resolution. Only a domain name can be entered. After the record is generated, a "." will be automatically added after the domain name, which is normal.
	5. MX priority is not required.
	6. TTL (Time to Live) is the cache period for the record. The smaller the value is, the faster the modified record takes effect globally. If you leave it empty, it defaults to 600s. 


## Wanwang
If your DNS service provider is Wanwang, use the following steps to add a CNAME record:
1. Log in to the Wanwang Member Center.
2. On the left sidebar, click **Product Management** > **My Cloud Resolution** to enter the cloud resolution list page.
3. Click the domain name to be resolved to enter the resolution record page.
4. On the resolution record page, click "Add Resolution" to set a resolution record.
5. To set a CNAME record, select CNAME as the record type. Enter the host record (such as `www`) as needed, which is the domain name prefix. Enter the domain name pointed to by the current domain name as the record value. Retain the default settings of the resolution line and TTL.
6. After completing the settings, click **Save**.

## Xinnet
If your DNS service provider is Xinnet, you can add a CNAME record in the following steps:
**Set an alias (CNAME record)**
CNAME record, aka alias record, allows you to map multiple names to the same computer and is generally used for computers providing both www and mail services. For example, a computer named `host.mydomain.com` (A record) provides both www and mail services. To facilitate user access, you can set two aliases (CNAME records) for this computer: `WWW` and `MAIL`.

## Verifying the Effectiveness of a CNAME Record
The time for a CNAME record to take effect varies by DNS service provider. It is generally within half an hour. You can also check whether the CNAME record is in effect in the following ways:
- Method 1: Click **Start** → **Run** → enter `cmd`, press Enter, and enter the PING command to check whether the CNAME is effective. If the resolution result returned is the same as the CNAME of the domain name, the CNAME configuration is effective.
- Method 2: Click **Start** → **Run** → enter `cmd`, press Enter, and enter the nslookup command to check whether the CNAME is effective. If the resolution result returned is the same as the CNAME of the domain name, the CNAME configuration is effective.
