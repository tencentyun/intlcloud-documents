This document will instruct you to perform local tests before modifying DNS resolution.
## Directions
DNS resolution is required when a local server accesses a website. Before DNS resolution, the IP address of the destination domain name will be obtained from the local `hosts` file. Therefore, you can modify the `hosts` file to direct local access traffic to WAF so as to test the connectivity of the route to the website through WAF. This avoids direct modification of DNS resolution records that may affect Internet users' access to the website.
1. Log in to the WAF Console(https://console.cloud.tencent.com/guanjia) and choose **Web Application Firewall** -> **Defense settings** on the left sidebar. In the domain name list, view the VIP address of `waf.qcloudwaf.com`.
<img src="https://main.qcloudimg.com/raw/b03ca645ed87220d5990e924158e3ef5.png" style="zoom:85%;" /><br>
If you need to get the VIP address of the corresponding domain name, you can get it by pinging the CNAME address.
 1. In Windows, open Command Prompt.
 2. Run the command: `ping <WAF CNAME address>`.
 ![](https://main.qcloudimg.com/raw/3bd7ecefb96c13462275c0f871e90231.png)
 3. The ping command output will record the WAF IP address of the domain name, which is required for subsequent operations.
2. Modify `hosts` file.
	In Windows, modify `C:\Windows\System32\drivers\etc\hosts` by adding the following entry.
	Format: VIP address + domain name connected to WAF
 ![](https://main.qcloudimg.com/raw/1ccf20053b32d72dbf8156454517705e.png)
	In Linux, modify `/etc/hosts` by adding the following entry.
Format: VIP address + domain name connected to WAF
 ![3](https://main.qcloudimg.com/raw/76551c1dcd21686169eaf2db8110494a.png)
3. Test access. 
	1. Access the website from your local computer. If the website can be opened properly, the connectivity of the route to the real server through WAF is normal.
	2. Enter the following URL in your browser to access it:
```
http://waf.qcloudwaf.com/?test=alert(123)  
```
	3. If the browser returns a blocked message, the WAF's protection features are working properly.
	>? To view the blocked message, you can access the [default WAF prompt](http://www.qcloudwaf.com/?alert(1=1) ).

![](https://main.qcloudimg.com/raw/253fdfbae2d6529f2b1e64c1f599c8cc.png)


## Subsequent Operations
After performing the local test, you can proceed as follows:
- [Step 3. Modify DNS Resolution](https://intl.cloud.tencent.com/zh/document/product/627/35653)
- [Step 4. Set a Security Group](https://intl.cloud.tencent.com/zh/document/product/627/35654)
