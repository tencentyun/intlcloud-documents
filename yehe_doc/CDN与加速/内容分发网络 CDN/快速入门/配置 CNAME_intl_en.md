![](https://qcloudimg.tencent-cloud.cn/raw/1d6aa270579356fd95585e86c8d375b2.png)

## Preparations

### Adding domain name
Before configuring a CNAME record, you need to [add a domain name](https://intl.cloud.tencent.com/document/product/228/5734) first. If you have already added one, proceed directly.


## Directions

### Configuration steps

You need to complete the configuration at the DNS service provider of your domain name. This document describes the configuration steps in Tencent Cloud and Alibaba Cloud:

- [Settings for Tencent Cloud](#m1)
- [Settings for Alibaba Cloud](#m2)

[](id:m1)
### Tencent Cloud

#### Quick configuration

If your domain service provider is Tencent Cloud, we recommend you use the quick CNAME record configuration feature. For more information, see [Configuring CNAME via DNSPod](https://intl.cloud.tencent.com/document/product/228/42353).



#### Manual configuration

1. Log in to the [CDN console](https://console.cloud.tencent.com/cdn) and copy the CNAME address.
   Before your domain name is successfully resolved, a prompt icon is displayed next to the CNAME record. Copy the CNAME record value.

2. Log in to the [DNSPod console](https://console.cloud.tencent.com/cns) and click **Record**.

3. Add a CNAME record and click **OK**.

4. Wait for the configuration to take effect.

**Configuration description:**

| Configuration | Description                                                     |
| :------- | :----------------------------------------------------------- |
| Host | It is the domain name prefix. <br><br>**Example:** to add a record for `dnspod.com`, select **@** for **Host**. To add a record for `www.dnspod.com`, select **www** for **Host**. |
| Record Type | Select **CNAME**.                                               |
| Split Zone | Select **Default**. DNSPod offers various split zone options for you to specify records for specific users. For more information, see [Split Zone Description](https://docs.dnspod.cn/dns/5f4775898ae73e11c5b01afc/). |
| Value | Enter the domain name pointed to by the CNAME, e.g., `xxx.xxx.com.cdn.dnsv1.com`. After the record is generated, a `.` will be automatically added after the domain name. |
| Weight     | Different record values in the same split zone of a host record can be set with different weights, so that resolution will be returned according to their weight ratios. Value range: 1–100. |
| MX       | It refers to the priority. The lower the value, the higher the priority. We recommend you leave it empty.       |
| TTL      | It refers to the time to live. The smaller the value is, the less the time cost for record changes to take effect globally. The default value is 600 seconds.  |

[](id:m2)
### Alibaba Cloud

If your DNS service provider is Alibaba Cloud, you can add a CNAME record as follows.

1. Log in to the [CDN console](https://console.cloud.tencent.com/cdn) and copy the CNAME address.
   Before your domain name is successfully resolved, a prompt icon is displayed next to the CNAME record. Copy the CNAME record value.

2. Log in to the Alibaba Cloud DNS console.
3. Click the domain name to be resolved to enter the resolution record page.
4. Click **Add Record**.
5. Select ***CNAME** as the record type. Enter the host record as needed (such as `www`), which is the domain name prefix. Enter the CNAME record copied in step 1 as the record value. Retain the default settings of the split zone and TTL.
<img src="https://main.qcloudimg.com/raw/6b8bb9ce4f998b8d17ca27fd10512dc6.png" width="80%">
6. Finally, click **Confirm**.

## Subsequent Operations

### CNAME verification

The time it takes for a CNAME record to take effect varies by DNS service provider. It is generally within half an hour. You can also check whether the CNAME record is in effect by running `nslookup` or `dig`. If the CNAME record response is the CNAME configured, it indicates that the configuration is successful and the acceleration is enabled.

- nslookup -qt=cname <acceleration domain name>
<img src="https://main.qcloudimg.com/raw/1f94ea7e3ee46fc761e8e839ce68a86d.png" width="70%">
- dig <acceleration domain name></br>
<img src="https://main.qcloudimg.com/raw/fe9b8f9a1a26d3a7df5db614762caeaf.png" width="70%">

### Directions

You have completed the basic configuration of the CDN service. For more CDN configurations, see the corresponding document in [Configuration Guide](https://intl.cloud.tencent.com/document/product/228/15417).

