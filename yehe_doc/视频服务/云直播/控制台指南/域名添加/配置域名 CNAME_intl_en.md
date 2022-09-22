After you add a domain name in the CSS console, the system will assign it a CNAME (suffixed with `.tlivecdn.com`), which you can view in [Domain Management](https://console.cloud.tencent.com/live/domainmanage). To make your domain accessible, you need to add a CNAME record at your DNS service provider. You can use CSS only after the configuration takes effect.


## Notes
- CNAME resolution is required for both playback and push domains.
- For detailed directions on how to add a CNAME record, please consult your DNS service provider.
- CNAME configuration generally takes effect in about 15 minutes. If you configure multiple levels of CNAMEs, CSS will be unable to track the resolution result. If your domain can be accessed, then the CNAME configuration is successful.
- If CNAME configuration fails to take effect after a long time, refer to [Domain Configuration](https://intl.cloud.tencent.com/document/product/267/32478) to troubleshoot the issue.

## Prerequisites
- You have registered a domain.
- You have verified the domain and [added it](https://intl.cloud.tencent.com/document/product/267/35970) in [Domain Management](https://console.cloud.tencent.com/live/domainmanage) of the CSS console. You haven’t added a CNAME record for the domain (the icon in the **CNAME** column is ![](https://main.qcloudimg.com/raw/ed1ac2f8541f629814a3f2420b1eb79c.png)).



## Directions
The following part shows you how to configure a CNAME record at Tencent Cloud, Alibaba Cloud, Baidu AI Cloud, DNSPod, Wanwang, and Xinnet. The directions in this document are for reference only. Please follow the directions of your DNS service provider. To check whether your CNAME configuration has taken effect, see [Verifying CNAME Records](#check).

[](id:tencent)
### One-click CNAME configuration
If your domain is hosted by DNSPod, you can add a CNAME record in the CSS console with just one click.
1. Log in to the CSS console and select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar. You can open the one-click CNAME configuration window in three ways.
  - Hover over the ![](https://main.qcloudimg.com/raw/ed1ac2f8541f629814a3f2420b1eb79c.png) icon and click **Add now**.
  - Click the name of the domain for which you want to add a CNAME record or click **Manage**. Under the **Basic Info** tab, click **Add now**.
  - When adding your domain in the CSS console, after finishing the basic settings, you will be asked to configure the CNAME.
2. If you haven’t added a CNAME record for your domain, click **Add now**. The configuration will take effect in about **15 minutes**.

3. If the configuration fails, try adding the record in the [DNSPod console](https://console.dnspod.com/).

   

[](id:dnspod)
### DNSPod
If your DNS service provider is DNSPod, use the following steps to add a CNAME record:
1. Log in to the [DNSPod console](https://console.dnspod.com/).
2. Select **DNS > My Domains** on the left sidebar, click the name of the domain for which you want to add a CNAME record. On the **Record Management** page, click **Add Record**.
3. Add a CNAME record as follows:
  1. For **Host**, enter the subdomain. For example, if you want to resolve `www.123.com`, enter `www`; if you want to resolve `123.com`, leave this empty. The input box will be auto-filled with `@`. Please note that if **Host** is `@`, the MX record for the domain will be affected.
  2. Select **CNAME** as the record type.
  3. For **Split Zone**, make sure it is **Default**, or resolution may fail for some users.
For example, to point all Baidu users to 2.com and other users to 1.com, you can add a record whose value is 1.com and whose split zone is the default and a record whose value is 2.com and whose split zone is Baidu.
  4. For **Record Value**, enter the CNAME. The system will automatically suffix it with a `.`.
  5. For **MX**, leave it empty.
  9. TTL (Time to Live) is the cache period for a record. The smaller the value, the faster record changes take effect globally. The default value is 600 (seconds).



[](id:ali)
### Alibaba Cloud
If your DNS service provider is Alibaba Cloud, use the following steps to add a CNAME record:

1. Log in to the Alibaba Cloud console and go to **Alibaba Cloud DNS** > **[Manage DNS](https://dns.console.aliyun.com/#/dns/domainList)**.
2. Click the domain for which you want to add a CNAME record to go to the **DNS Settings** page.
3. Click **Add Record** and complete the following settings:
  - Type: Select `CNAME`.
  - Host: Enter the subdomain. For example, if your playback domain is `play.myqcloud.com`, enter `play`; if you want to resolve `myqloud.com`, enter `@`; if you want to add a wildcard record, enter `\*`.
  - ISP Line: `Default` is recommended.
  - Value: Enter the CNAME of the domain. You can view your domain’s CNAME (`domain.livecdn.liveplay.myqcloud.com`) on the **Domain Management** page of the CSS console.
  - TTL: 10 minutes is recommended.
4. Click **OK**.


[](id:baidu)
### Baidu AI Cloud
If your DNS service provider is Baidu AI Cloud, use the following steps to add a CNAME record:
1. Log in to the Baidu AI Cloud console and go to [Domain Name System](https://console.bce.baidu.com/bcd/?_=1550137564099#/bcd/manage/list).
2. Select the domain you added to CSS and click **Resolve** in the **Operation** column.
3. Add a DNS record:
 - CVM server record: Enter the second-level domain (prefix) of your domain. For example, if your playback domain is `play.myqcloud.com`, enter `play`; if you want to resolve `myqloud.com`, enter `@`; if you want to add a wildcard record, enter `\*`.
 - Record type: Select `CNAME record`.
 - Resolution line: `Default` is recommended.
 - Record value: Enter the CNAME. You can view your domain’s CNAME (`domain.tlivecdn.com`) on the **Domain Management** page of the CSS console.
 - TTL: 10 minutes is recommended.
4. Click **Confirm**.


[](id:wwwnet)
### Wanwang
If your DNS service provider is Wanwang, use the following steps to add a CNAME record:

1. Log in to the Wanwang Member Center.
2. On the left sidebar, click **Product Management** > **My Cloud Resolution** to enter the cloud resolution list page.
3. Click the domain name to be resolved to enter the resolution record page.
4. On the resolution record page, click **Add Resolution**.
5. To add a CNAME record, select CNAME as the record type. For the host record, enter the domain prefix (such as `www`). For the record value, enter the CNAME to point to. Keep the default resolution line and TTL.
6. After completing the settings, click **Save**.


[](id:xinnet)
### Xinnet
If your DNS service provider is Xinnet, add a CNAME record by **setting an alias (CNAME record)**.
An alias record allows you to map multiple names to the same computer and is generally used for computers providing both www and mail services. Suppose a computer named `host.mydomain.com` (A record) provides both www and mail services. To facilitate user access, you can set two aliases (CNAME records) starting with `www` and `mail` for this computer.

[](id:check)
## Verifying CNAME Records
A new CNAME record generally takes effect within 30 minutes. The exact time needed varies with provider. You can check whether a record has taken effect using the following methods.
- **Method 1:** Go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage) of the CSS console. If the icon in the **CNAME** column is ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png), CNAME configuration is successful.
![](https://main.qcloudimg.com/raw/7930331f6eb7f4271014083cab27fb26.png)
- **Method 2:** When you [add your domain](https://console.cloud.tencent.com/live/domainmanage) in the CSS console, after completing the basic settings, in the **CNAME configuration** step, you can view the CNAME status of the domain.
- **Method 3:** On Linux/macOS, run the `dig` command (`dig your domain`). If the first row displays the destination domain provided by CSS, CNAME configuration is successful. 
![](https://main.qcloudimg.com/raw/2cbe7fdc1c9d7dbed7851aa86dd64ff1.png)
- **Method 4**: On Windows, open a Command Prompt window and enter `nslookup your domain`. If the destination domain name provided by CSS is displayed, CNAME configuration is successful.
![](https://main.qcloudimg.com/raw/765ac099e7c79a70496563f00cdab9a7.png)


>! If CNAME configuration fails to take effect after a long time, refer to [Domain Configuration](https://intl.cloud.tencent.com/document/product/267/32478) to troubleshoot the issue.