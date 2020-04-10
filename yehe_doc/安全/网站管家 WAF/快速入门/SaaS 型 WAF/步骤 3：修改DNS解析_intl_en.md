To forward internet users' traffic accessing your website to WAF for protection, you need to modify your DNS record. The following uses modification of DNS of the test website `waf.qcloudwaf.com` on Tencent Cloud DNS as an example to describe how to configure DNS.

1. Log in to the [Tencent Cloud DNS Console](https://console.cloud.tencent.com/cns), click **DNS Resolution List** on the left sidebar, find the domain name `qcloudwaf.com` that needs to be connected to WAF, and click **Resolve** to enter the resolution configuration page.
	 
2. Click **Add Record**.
	 
3. Enter the corresponding information on the configuration page.
	- Enter the host record of the website for "Host Record". In this example, enter `waf` since the domain name to be protected is `waf.qcloudwaf.com`.
   
	- Select "CNAME" as "Record Type".
   
	- Enter the CNAME domain name allocated by WAF for "Record Value", which is in the format of `xxxx.qcloudcjgj.com`.
   
	- After completing the configuration, click **Save**.
 

5. After the modification, wait for the DNS record to take effect and WAF to start protecting the traffic accessing the website. If WAF detects that the protected domain name is properly resolved, "Normal Protection" will be displayed in the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/config).

