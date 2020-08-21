Once your domain name is connected to LVB, the system will automatically assign it a CNAME domain name (suffixed with `.liveplay.myqcloud.com`), which can be viewed in the **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** list. It cannot be accessed directly before you complete the CNAME configuration at your domain name service provider. After the configuration takes effect, LVB can be used properly.


## Notes
- CNAME resolution is required for both playback domain name and push domain name.
- Please configure a CNAME record at your domain name resolution service provider. For detailed directions, please consult your service provider.
- The CNAME configuration will take effect in about 15 minutes. If you set multiple layers of CNAME, LVB cannot effectively monitor the resolution result, and the actual access conditions shall prevail.
- If the CNAME configuration fails to take effect after a prolonged time, please see [CNAME Configuration Troubleshooting](https://intl.cloud.tencent.com/document/product/267/32478).

## Prerequisites
- You have applied for a domain name through [Tencent Cloud Domain Service](https://dnspod.cloud.tencent.com/?from=qcloudProductDns) and obtained ICP filing for its service in Mainland China.
- You have successfully [added a domain name](https://intl.cloud.tencent.com/document/product/267/35970) in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** in the LVB Console, and the CNAME address status of the domain name is ![](https://main.qcloudimg.com/raw/ed1ac2f8541f629814a3f2420b1eb79c.png) (CNAME not configured).



## Configuration Steps
This document describes how to configure a CNAME record at Tencent Cloud, Alibaba Cloud, Baidu Cloud, DNSPod, Wanwang, and Xinnet, respectively. The directions below are for your reference only, and the actual directions shall apply. After configuring the domain name CNAME, you can verify whether the CNAME configuration has taken effect as instructed in [Verifying the Effect of CNAME Record](#check).

<span id="tencent"></span>

### Settings for Tencent Cloud
If your DNS service provider is Tencent Cloud, you can add a CNAME record in the following steps:

1. Log in to the [Tencent Cloud Domain Service Console](https://console.cloud.tencent.com/domain).
2. Select the domain name for which you want to add a CNAME record and click **Resolve**.
3. Go to the DNS page of the specified domain name and click **Add Record**.
4. Enter the domain name CNAME record in the new line as follows:
<table>
    <tr><th width="12%" >Parameter Name</th><th width="38%">Parameter Description</th><th width="50%">How to Configure</th></tr>
    <tr>
        <td>Host Record	</td>
        <td>Enter the prefix of the subdomain name	</td>
        <td>
            <ul style="margin-bottom:0;">
                <li>If the domain name is <code>play.myqcloud.com</code>, please select: <code>play</code></li>
                <li>To resolve the primary domain name <code>myqloud.com</code>, please select: <code>@</code></li>
                <li>To resolve a wildcard domain name, please select: <code>\*</code></li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Record Type</td>
        <td>Set the record type to CNAME</td>
        <td>To point a domain name to another one, please select: <b>CNAME</b></td>
    </tr>
    <tr>
        <td>Line Type</td>
        <td>This is used to return the corresponding server IP address according to the source of the visitor when the DNS server resolves the domain name</td>
        <td>Please select: <b>Default</b></td>
    </tr>
    <tr>
        <td>Record Value</td>
        <td>Domain name to point to. Enter the corresponding CNAME value of the domain name obtained on the **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>** page in the Tencent Cloud Console.</td>
        <td>Format: <code><b style="color:red;">xxxx</b>.livecdn.liveplay.myqcloud.com</code></td>
    </tr>
    <tr>
        <td>TTL (s)</td>
        <td>Time to live of the cache, which is <b>600s</b> by default</td>
        <td>You are recommended to enter <b>600s</b></td>
    </tr>
</table>
5. Click **Save** to complete the CNAME configuration.


> 
>There are differences in priority between various record types during domain name resolution. If the host records are identical, different types of records cannot coexist on the same line; otherwise, a conflict will occur. A CNAME record conflicts with records of any other types; therefore, you need to delete other records first before configuring CNAME.
<span id="ali"></span>
### Settings for Alibaba Cloud
If your DNS service provider is Alibaba Cloud and you have obtained an ICP filing for your domain name, you can set up a CNAME record in the following steps:

1. Log in to the Alibaba Cloud Console and go to **Alibaba Cloud DNS** > **[DNS](https://dns.console.aliyun.com/#/dns/domainList)**.
2. Select the domain name for which you want to add a CNAME record and click **Resolution Settings**.
3. Select **Add Record** and set as follows:
	- Record Type: select `CNAME`.
	- Host Record: enter the prefix of the sub-domain names; for example, if the playback domain name is `play.myqcloud.com`, enter `play`; if you want to directly resolve the primary domain name `myqloud.com`, enter `@`; and if you want to resolve a wildcard domain name, enter `\*`.
	- Resolution Route: you are recommended to select `Default`.
	- Record Value: enter the CNAME value in the format of `domain.livecdn.liveplay.myqcloud.com` obtained on the Domain Management page in the Tencent Cloud Console.
	- TTL: you are recommended to enter `10 minutes`.
4. Click **OK**.

<span id="baidu"></span>

### Settings for Baidu Cloud
If your domain name service provider is Baidu Cloud, you can add a CNAME record in the following steps:
1. Log in to the Baidu Cloud Console and select **[Domain Management](https://console.bce.baidu.com/bcd/?_=1550137564099#/bcd/manage/list)** to enter the domain management list page.
2. Select the domain name added to LVB and click **Resolve** in the "Operation" column to enter the DNS resolution page:
3. Add a resolution record and configure as follows:
 - Host Record: enter the prefix of the second-level domain names; for example, if the playback domain name is `play.myqcloud.com`, enter `play`; if you want to directly resolve the primary domain name `myqloud.com`, enter `@`; and if you want to resolve a wildcard domain name, enter `\*`.
 - Record Type: select `CNAME`.
 - Resolution Route: you are recommended to select `Default`.
 - Record Value: enter the CNAME value in the format of `domain.livecdn.liveplay.myqcloud.com` obtained on the Domain Management page in the LVB Console.
 - TTL: you are recommended to enter `10 minutes`.
4. Click **OK** to submit.


<span id="dnspod"></span>

### Settings for DNSPod

If your DNS service provider is DNSPod, you can add a CNAME record in the following steps:
1. Log in to the [DNSPod Console](https://console.dnspod.cn/dns/list).
2. In the list, find the row of the domain name for which to add a CNAME record, and click the domain name to enter the "Add Record" page.
3. Add a CNAME record in the following steps:
	1. Enter the sub-domain name for the host record (for example, if you want to add the resolution for `www.123.com`, you only need to enter `www` as the host record; if you want to add the resolution for `123.com`, the host record can be left empty and the system will automatically enter an `@` into the input box. A CNAME record with `@` will affect the proper resolution of the MX record, so please be cautious when adding it).
	2. Set the record type to CNAME.
	3. Set the line type (required by default; if left empty, requests of some users may not be able to be resolved. In the figure above, the default value means that all users except those of China Unicom will be pointed to `1.com`).
	4. The record value is the domain name pointed to by CNAME resolution. Only a domain name can be entered. After the record is generated, a "." will be automatically added after the domain name, which is normal.
	5. MX priority does not need to be entered.
	6. TTL does not need to be entered. The system will automatically generate it when adding the record. The default is 600 seconds (TTL is the cache time. The smaller the value, the faster the change to the record will take effect in various regions).


<span id="wwwnet"></span>

### Settings for Wanwang

If your DNS service provider is Wanwang, you can add a CNAME record in the following steps:

1. Log in to the Wanwang Member Center.
2. On the left sidebar, click **Product Management** > **My Cloud Resolution** to enter the cloud resolution list page.
3. Click the domain name to be resolved to enter the resolution record page.
4. On the resolution record page, click "Add Resolution" to set a resolution record.
5. To set a CNAME resolution record, select CNAME as the record type. Enter the host record as needed (such as `www`), which is the domain name prefix. Enter the domain name pointed to by the current domain name as the record value. Retain the default settings of the resolution line and TTL.

6. After completing the settings, click **Save**.

<span id="xinnet"></span>

### Settings for Xinnet
If your DNS service provider is Xinnet, you can add a CNAME record by **setting an alias (CNAME record)**.
An alias record allows you to map multiple names to the same computer and is generally used for computers providing both WWW and mail services. For example, a computer named `host.mydomain.com` (A record) provides both WWW and mail server. To facilitate user access, you can set two aliases (CNAME records) for this computer: `WWW` and `MAIL` .
<span id="check"></span>


## Verifying the Effect of CNAME Record
The time it takes for a CNAME record to take effect varies by DNS service provider. It is generally within half an hour. You can also check whether the CNAME record is in effect in the following ways:
- **Method 1**: enter **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** in the LVB Console and check whether the status symbol of the domain name suffixed with `.myqcloud.com` has changed to ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png), and if so, CNAME configuration is successful.

- **Method 2**: on Linux/macOS, run the `dig` command in the format of `dig your own domain name`. If the first row displays that the destination domain name provided by LVB is resolved, CNAME configuration is successful. 
![](https://main.qcloudimg.com/raw/49aa30e1edc3884c2ae93ec5fdeeb1fb.png)
- **Method 3**: on Windows, click **Start** > **Run**, enter `cmd`, press Enter, and then enter `nslookup your own domain name` on the command line. If the destination domain name provided by LVB is resolved, CNAME configuration is successful.
![](https://main.qcloudimg.com/raw/8bad41428852a7c32111933b33e8853c.png)


>If the CNAME configuration fails to take effect after a prolonged time, please see [CNAME Configuration Troubleshooting](https://intl.cloud.tencent.com/document/product/267/32478).
