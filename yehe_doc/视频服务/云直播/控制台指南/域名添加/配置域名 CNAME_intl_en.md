Once you add a domain name in the CSS console, the system will automatically assign it a CNAME domain name (suffixed with `.liveplay.myqcloud.com`), which can be viewed in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**. It cannot be accessed before you complete the CNAME configuration at your DNS service provider. After the configuration takes effect, you can use CSS service.

## Notes
- CNAME resolution is required for both playback domain name and push domain name.
- Please configure a CNAME record at your DNS service provider. For detailed directions, please consult your service provider.
- The CNAME configuration will take effect in about 15 minutes. If you set multiple layers of CNAME, CSS cannot effectively monitor the resolution result. The CNAME configuration is successful if the CNAME domain name is accessible.
- If the CNAME configuration fails to take effect after a prolonged time, please see [Domain Configuration](https://intl.cloud.tencent.com/document/product/267/32478).

## Prerequisites
- You have applied for a domain name through [Tencent Cloud Domain Service](https://dnspod.cloud.tencent.com/?from=qcloudProductDns).
- You have successfully [added a domain name](https://intl.cloud.tencent.com/document/product/267/35970) on the **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** page in the CSS console, and the CNAME address status of the domain name is ![](https://main.qcloudimg.com/raw/ed1ac2f8541f629814a3f2420b1eb79c.png) (CNAME not configured).



## Directions
This document describes how to configure a CNAME record at Tencent Cloud, Alibaba Cloud, Baidu AI Cloud, DNSPod, Wanwang, and Xinnet, respectively. The directions below are for your reference only. Please follow the directions of your DNS service provider. After configuring the domain name CNAME, you can verify whether the CNAME configuration has taken effect as instructed in [Verifying Whether the CNAME Takes Effect](#check).


### Tencent Cloud[](id:tencent)
If your DNS service provider is Tencent Cloud, use the following steps to add a CNAME record:

1. Log in to the [Tencent Cloud Domain Name Service console](https://console.cloud.tencent.com/domain).
2. Select the domain name for which you want to add a CNAME record and click **Resolve**.
3. On the displayed DNS page of the domain name, click **Add Record**.
4. Set the following parameters of the CNAME record:
<table>
    <tr><th width="12%" >Parameter</th><th width="38%">Description</th><th width="50%">Configuration</th></tr>
    <tr>
    <td><a href="https://cloud.tencent.com/document/product/302/3468#.E4.B8.BB.E6.9C.BA.E8.AE.B0.E5.BD.95.E7.9A.84.E7.94.A8.E6.B3.95.E6.9C.89.E4.BB.80.E4.B9.88.EF.BC.9F">Host Record</a></td>
        <td>Prefix of the subdomain name</td>
        <td>
            <ul style="margin-bottom:0;">
                <li>If the domain name is <code>play.myqcloud.com</code>, please select: <code>play</code></li>
                <li>To resolve the primary domain name <code>myqloud.com</code>, please select: <code>@</code></li>
                <li>To resolve a wildcard domain name, please select: <code>\*</code></li>
            </ul>
        </td>
    </tr>
    <tr>
    <td><a href="https://cloud.tencent.com/document/product/302/3468#.E8.AE.B0.E5.BD.95.E7.B1.BB.E5.9E.8B.E7.9A.84.E5.90.AB.E4.B9.89.E6.98.AF.E4.BB.80.E4.B9.88.EF.BC.9F">Record Type</a></td>
        <td>Record type</td>
        <td>To point a domain name to another one, please select: <b>CNAME</b></td>
    </tr>
    <tr>
        <td><a href="https://cloud.tencent.com/document/product/302/3468#.E7.BA.BF.E8.B7.AF.E7.9A.84.E7.94.A8.E6.B3.95.E6.9C.89.E4.BB.80.E4.B9.88.EF.BC.9F">Split Zone</a></td>
        <td>Used by the DNS server to resolve a domain name to the corresponding server IP address according to the source of the visitor </td>
        <td>Please select: <b>Default</b></td>
    </tr>
    <tr>
        <td><a href="https://cloud.tencent.com/document/product/302/3468#.E8.AE.B0.E5.BD.95.E5.80.BC.E5.A6.82.E4.BD.95.E5.A1.AB.E5.86.99.EF.BC.9F">Record Value</a></td>
        <td>The domain name to point to. Enter the corresponding CNAME value of the domain name obtained on the **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>** page in the Tencent Cloud console.</td>
        <td>Go to the **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>** page, find a domain name with no CNAME configured, copy it and then enter it in **Record Value** in the format of: <ul style="margin:0">
				<li/><code><b style="color:red;">xxxx</b>.liveplay.myqcloud.com</code>
				<li/><code><b style="color:red;">xxxx</b>.livepush.myqcloud.com</code>
				</ul></td>
    </tr>
    <tr>
        <td><a href="https://cloud.tencent.com/document/product/302/3468#.E8.AE.B0.E5.BD.95.E5.80.BC.E5.A6.82.E4.BD.95.E5.A1.AB.E5.86.99.EF.BC.9F">TTL (s)</a></td>
        <td>Time to live of the cache, which is <b>600s</b> by default</td>
        <td>You’re advised to set it to <b>600s</b>.</td>
    </tr>
</table>
5. Click **Save** to complete the CNAME configuration.
![](https://main.qcloudimg.com/raw/ede56d6523c4351102ec80d51b30ebae.png)

>! 
>- DNS records of different types vary in priority. A CNAME record cannot coexist with a different type of record with the same **Host Record** in the same split zone. Therefore, you need to delete other records before adding a CNAME record.

### Alibaba Cloud[](id:ali)
If your DNS service provider is Alibaba Cloud, use the following steps to add a CNAME record:

1. Log in to the Alibaba Cloud console and go to **Alibaba Cloud DNS** > **[Manage DNS](https://dns.console.aliyun.com/#/dns/domainList)**.
2. Click the domain name for which you want to add a CNAME record to go to the **DNS Settings** page.
3. Click **Add Record** and set as follows:
  - Type: select `CNAME`.
  - Host: enter the prefix of the subdomain name; for example, if the playback domain name is `play.myqcloud.com`, enter `play`; if you want to directly resolve the primary domain name `myqloud.com`, enter `@`; and if you want to resolve a wildcard domain name, enter `\*`.
  - ISP Line: you’re advised to select `Default`.
  - Value: enter the CNAME of the domain name on the domain name management page in the Tencent Cloud console, in the format of `domain.livecdn.liveplay.myqcloud.com`.
  - TTL: you’re advised to select 10 minutes.
4. Click **OK**.

![](https://main.qcloudimg.com/raw/8c9d4b75c7f863c1b40fc8cf59160b45.png)



### Baidu AI Cloud[](id:baidu)
If your DNS service provider is Baidu AI Cloud, use the following steps to add a CNAME record:
1. Log in to the Baidu AI Cloud console and go to the [Domain Name System](https://console.bce.baidu.com/bcd/?_=1550137564099#/bcd/manage/list).
2. Select the domain name added to CSS and click **Resolve** in the **Operation** column to enter the DNS page as shown below:
3. Add a DNS record and set as follows:
 - CVM server record: enter a second-level domain name, i.e., the domain name prefix; for example, if the playback domain name is `play.myqcloud.com`, enter `play`; if you want to directly resolve the primary domain name `myqloud.com`, enter `@`; and if you want to resolve a wildcard domain name, enter `\*`.
 - Record type: select `CNAME record`.
 - Resolution line: you’re advised to select `Default`.
 - Record value: enter the CNAME value obtained on the domain name management page in the CSS console, in the format of `domain.livecdn.liveplay.myqcloud.com`.
 - TTL: you’re advised to select 10 minutes.
4. Click **Confirm**.
![](https://main.qcloudimg.com/raw/a021aaa59e562ad76757d19c2b675621.png)


### DNSPod[](id:dnspod)
If your DNS service provider is DNSPod, use the following steps to add a CNAME record:
1. Log in to the [DNSPod console](https://console.dnspod.cn/dns/list).
2. Click the target domain name in the list to enter the "Add Record" page.
3. Add a CNAME record as follows:
  1. Enter the subdomain name for the host record. For example, if you want to resolve `www.123.com`, you only need to enter `www` as the host record; if you want to resolve `123.com`, you can leave the host record empty and the system will automatically enter an `@`. A CNAME record with `@` will affect the resolution of the MX record.
  2. Select **CNAME** as the record type.
  3. Set the split zone type (required by default; if it is left empty, requests of some users may not be resolved. In the figure below, the default value means that all users except those of China Unicom will be pointed to `1.com`).
  4. Set the record value to the domain name pointed to by CNAME resolution. Only a domain name can be entered. After the record is generated, a "." will be automatically added after the domain name, which is normal.
  5. MX priority is not required.
  6. TTL (Time to Live) is the cache period for the record. The smaller the value is, the faster the modified record takes effect globally. If you leave it empty, it defaults to 600s. 
![](https://main.qcloudimg.com/raw/ee19f4ea9269c340d8622a945e86fb87.png)

### Wanwang[](id:wwwnet)
If your DNS service provider is Wanwang, use the following steps to add a CNAME record:

1. Log in to the Wanwang Member Center.
2. On the left sidebar, click **Product Management** > **My Cloud Resolution** to enter the cloud resolution list page.
3. Click the domain name to be resolved to enter the resolution record page.
4. On the resolution record page, click "Add Resolution" to set a resolution record.
5. To set a CNAME record, select CNAME as the record type. Enter the host record (such as `www`) as needed, which is the domain name prefix. Enter the domain name pointed to by the current domain name as the record value. Retain the default settings of the resolution line and TTL.
![](https://main.qcloudimg.com/raw/3ffd9282393424cd721b48b26f166d4d.png)
6. After completing the settings, click **Save**.



### Xinnet[](id:xinnet)
If your DNS service provider is Xinnet, add a CNAME record by **setting an alias (CNAME record)**.
An alias record allows you to map multiple names to the same computer and is generally used for computers providing both www and mail services. For example, a computer named `host.mydomain.com` (A record) provides both www and mail services. To facilitate user access, you can set two aliases (CNAME records) starting with `www` and `mail` for this computer, as shown below:
![](https://main.qcloudimg.com/raw/48a5cb7a7301e49edb85edbc19e1bcbd.png)


## Verifying Whether CNAME Takes Effect
The time for a CNAME record to take effect varies by DNS service provider. It is generally within half an hour. You can also check whether the CNAME record is in effect in the following ways:
- **Method 1:** Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** in the CSS console, and check whether the status of the CNAME suffixed with `.myqcloud.com` changed to ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png), which means the CNAME configuration is successful.
![](https://main.qcloudimg.com/raw/b5150f5442f48a38bf9a972a84f43122.png)
- **Method 2**: on Linux/macOS, run the `dig` command in the format of `dig your own domain name`. If the first row displays that the destination domain name provided by CSS is resolved, CNAME configuration is successful. 
![](https://main.qcloudimg.com/raw/49aa30e1edc3884c2ae93ec5fdeeb1fb.png)
- **Method 3**: on Windows, click **Start** > **Run**, enter `cmd`, press Enter, and then enter `nslookup your own domain name` on the command line. If the destination domain name provided by CSS is resolved, CNAME configuration is successful.
![](https://main.qcloudimg.com/raw/8bad41428852a7c32111933b33e8853c.png)


>If the CNAME configuration fails to take effect after a prolonged time, please see [Domain Configuration](https://intl.cloud.tencent.com/document/product/267/32478).
