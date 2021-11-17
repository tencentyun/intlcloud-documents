This document will guide you how to modify the DNS resolution record, so that WAF can protect the traffic generated when public network users access your website.
## Directions
To protect the public network traffic to websites with WAF, you need to modify the DNS resolution record. The following uses `waf.qcloudwaf.com` as an example to describe how to modify its DNS resolution record on Tencent Cloud DNSPod.

1. Log in to the [DNSPod Console](https://console.cloud.tencent.com/cns), click **Domain Name Resolution List** on the left sidebar, and then click **Resolve** on the right of the domain name `qcloudwaf.com` to be accessed to WAF.
2. Click **Add Record**.
3. Enter the information required on the configuration page.
	- Enter the server record of the corresponding website for Server Record. In this example, the domain name is `waf.qcloudwaf.com`, so "waf" is entered.
   
   - Select "CNAME" as the record type.
	
   - Enter the CNAME domain name assigned by WAF for Record Value. In this example, the CNAME domain name format is `xxxx.qcloudcjgj.com`.
   
	- Click **Save** after filling in all the information.
    ![6](https://main.qcloudimg.com/raw/181fd99ac73c145d359805a975540305.png)
   
5. When the modification is complete, DNS records will take effect and WAF will protect traffic accessing the website. Meanwhile, WAF will display **Normal Protection** on the [console](https://console.cloud.tencent.com/guanjia/waf/config) after detecting that the resolution of the protected domain name is normal.
>?DNS records will take effect in about 10 minutes.

## Subsequent Operations
After modifying your DNS resolution records, you can proceed to [Step 4. Configure a Security Group](https://intl.cloud.tencent.com/document/product/627/35654).

