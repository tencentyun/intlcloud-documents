You need to change your DNS resolution records so that WAF protects traffic to your website when users access it over the Internet. Here, the DNS resolution of the test site `waf.qcloudwaf.com` is modified on Tencent Cloud DNSPod.

1. Log in to the [DNSPod Console](https://console.cloud.tencent.com/cns) and click **DNS List** on the left sidebar. On the pop-up page, find the domain name `qcloudwaf.com` that needs to connect to WAF and click **Resolve** to go to the resolution configuration page.
	 ![](https://main.qcloudimg.com/raw/b41c71dec079758fa5b2c2fccadb1681.png)
2. Click **Add Record**.
	 ![](https://main.qcloudimg.com/raw/2f7380ecb4a2a2d6a12878b5eef4e4f9.png)
3. Enter the corresponding information on the current configuration page.
	- Enter the corresponding host record in **Host Record**. In this example, `waf.qcloudwaf.com` needs to be protected, so `waf` is entered.
   ![4](https://main.qcloudimg.com/raw/881fa62631473226eec39fe97cc032d1.png)
	- Set **Record Type** to `CNAME`.
   ![3](https://main.qcloudimg.com/raw/fb4d9604279ad05a8d2db97eb7858422.png)
	- Enter the CNAME domain name assigned by WAF in **Record Value**. The format of the CNAME domain name is `xxxx.qcloudcjgj.com`.
   ![5](https://main.qcloudimg.com/raw/660137182993991acb43fde45d53053d.png)
	- After completing the settings, click **Save**.
 ![6](https://main.qcloudimg.com/raw/181fd99ac73c145d359805a975540305.png)

5. After the modified DNS records take effect, WAF can protect traffic that accesses your website. If WAF detects that the resolution of the protected domain name is normal, the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/config) displays “Normal Protection”.
>? It takes about 10 minutes for DNS records to take effect.

![](https://main.qcloudimg.com/raw/c3dfeae5cf9442df882946bb0bbec902.png)
