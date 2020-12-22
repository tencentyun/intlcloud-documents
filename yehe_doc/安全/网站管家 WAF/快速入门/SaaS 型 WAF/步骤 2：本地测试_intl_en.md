This document describes how to perform a local test before modifying the DNS resolution record.
## Directions
DNS resolution is required for local machines to access websites. Before performing DNS resolution, a local machine will obtain the IP of the target domain name from the local `hosts` file first. Therefore, we can direct the local access traffic to WAF by modifying the `hosts` file and test the connectivity of access to websites through WAF, instead of directly modifying the DNS resolution record which will influence the access of public network users to websites.
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia). In the left sidebar, select **Web Application Firewall** -> **Defense settings**, and then view the VIP of `waf.qcloudwaf.com` in the **Domain Name List**.
![](https://main.qcloudimg.com/raw/b03ca645ed87220d5990e924158e3ef5.png)
2. Modify the `hosts` file
	- In Windows, open `C:\Windows\System32\drivers\etc\hosts` and add the entry.
	Format: VIP+the domain name connected to WAF
 ![](https://main.qcloudimg.com/raw/c425c461c30311d132fccb425e752fc4.png)
	- In Linux, open `/etc/hosts` and add the entry.
Format: VIP+the domain name connected to WAF
 ![3](https://main.qcloudimg.com/raw/76551c1dcd21686169eaf2db8110494a.png)
3. Test the access 
	(1) Access the website via the local machine. If the website can be opened normally, the connectivity is normal for access to the website's origin server through WAF.
	(2) Open the URL in a browser:
```
http://waf.qcloudwaf.com/?test=alert(123)  
```
	(3) If the access is denied by a blocking information page, WAF protection is running normally.
![](https://main.qcloudimg.com/raw/253fdfbae2d6529f2b1e64c1f599c8cc.png)


## Subsequent Operations
After completing the local test, you can proceed:
- [Step 3. Modify DNS Resolution](https://intl.cloud.tencent.com/zh/document/product/627/35653)
- [Step 4. Set a Security Group](https://intl.cloud.tencent.com/zh/document/product/627/35654)
