Once your domain name is connected to ECDN, the system will automatically assign it a CNAME domain name (suffixed with `.dsa.dnsv1.com`), which cannot be accessed directly before you complete the CNAME configuration at your domain name service provider. After the configuration takes effect, ECDN can be used properly.
![](https://main.qcloudimg.com/raw/69802e106ed7b373195179d6b9773438.png)

## Settings for Tencent Cloud
If your DNS service provider is Tencent Cloud, you can add a CNAME record in the following steps:
1. Log in to [Domain Name Management Console](https://console.cloud.tencent.com/domain). In "My Domain Names", find the domain name for which to add a CNAME record and click **Resolve** in the "Operation" column.
![](https://main.qcloudimg.com/raw/5687364cbdec038240c9b37373524d39.png)
2. Go to the **Record Management** page of the specified domain name and click **Add Record**.
![](https://main.qcloudimg.com/raw/7c91ba3dffd64c7829e2cb1667e3c86b.png)
3. In the pop-up box, set **Record Type** to CNAME, **Host Record** to the domain name prefix (such as www), and **Record Value** to the CNAME domain name and click **OK** to add the CNAME record.
![](https://main.qcloudimg.com/raw/62a4fa35db0aafebae75c151cfc9f449.png)

## Settings for DNSPod
If your DNS service provider is DNSPod, you can add a CNAME record in the following steps:

1. Enter the sub-domain name for the host record (for example, if you want to add the resolution for `www.123.com`, you only need to enter `www` as the host record; if you want to add the resolution for `123.com`, the host record can be left blank and the system will automatically enter an "@" into the input box. A CNAME record with `@` will affect the proper resolution of the MX record, so please be cautious when adding it).
2. Set the record type to CNAME.
3. Set the line type (required by default; if left blank, requests of some users may not be able to be resolved. In the figure above, the default value means that all users except those of China Unicom will be pointed to `1.com`).
4. The record value is the domain name pointed to by CNAME resolution. Only a domain name can be entered. After the record is generated, a "." will be automatically added after the domain name, which is normal.
5. MX priority does not need to be entered.
6. TTL does not need to be entered. The system will automatically generate it when adding the record. The default is 600 seconds (TTL is the cache time. The smaller the value, the faster the change to the record will take effect in various regions).

## Settings for Wanwang
If your DNS service provider is Wanwang, you can add a CNAME record in the following steps:

1. Log in to the Wanwang Member Center.
2. On the left sidebar, click **Product Management** > **My Cloud Resolution** to enter the cloud resolution list page.
3. Click the domain name to be resolved to enter the resolution record page.
4. On the resolution record page, click "Add Resolution" to set a resolution record.
5. To set a CNAME resolution record, select CNAME as the record type. Enter the host record as needed (such as `www`), which is the domain name prefix. Enter the domain name pointed to by the current domain name as the record value. Retain the default settings of the resolution line and TTL.
6. After completing the settings, click **Save**.

## Settings for Xinnet
If your DNS service provider is Xinnet, you can add a CNAME record in the following steps:
**Setting alias (CNAME record)**
CNAME record, aka alias record, allows you to map multiple names to the same computer and is generally used for computers providing both WWW and mail services. For example, a computer named `host.mydomain.com` (A record) provides both WWW and mail server. To facilitate user access, you can set two aliases (CNAME records) for this computer: `WWW` and `MAIL`.

## Verifying the Effect of CNAME Record
The time it takes for a CNAME record to take effect varies by DNS service provider. It is generally within half an hour. You can also run `ping` on the command line to check whether the CNAME record is in effect. If a domain name suffixed with `.dsa.sp.spcdntip.com` or `.dsa.p23.tc.cdntip.com` can be pinged, the domain name CNAME record has taken effect.
