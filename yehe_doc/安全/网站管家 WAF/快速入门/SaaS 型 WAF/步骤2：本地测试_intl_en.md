DNS is required when a local server accesses a website. Before DNS, the IP address of the target domain name will be obtained from the local `hosts` file preferentially. Therefore, you can modify the `hosts` file to direct local access traffic to WAF so as to test the connectivity of the route to the website through WAF. This avoids direct modification of DNS that may affect internet users' access to the website.
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia) and select **Web Application Firewall** > **Protection Settings** on the left sidebar. In the domain name list, view the VIP address of `waf.qcloudwaf.com`.
 ![](https://main.qcloudimg.com/raw/b03ca645ed87220d5990e924158e3ef5.png)
2. Modify the `hosts` file.
	- On Windows, modify `C:\Windows\System32\drivers\etc\hosts` by adding the following entry.
	Format: VIP address + domain name connected to WAF
 ![](https://main.qcloudimg.com/raw/c425c461c30311d132fccb425e752fc4.png)
	- On Linux, modify `/etc/hosts` by adding the following entry.
Format: VIP address + domain name connected to WAF
 ![3](https://main.qcloudimg.com/raw/76551c1dcd21686169eaf2db8110494a.png)
3. Test the access. 
	1. Access the website from your local computer. If the website can be opened properly, the connectivity of the route to the real server through WAF is normal.
	1. Enter the following address in your browser to access it:
```
http://waf.qcloudwaf.com/?test=alert(123)  
```
	1. If the browser returns a blocking message, the protection feature of WAF works properly.
![](https://main.qcloudimg.com/raw/253fdfbae2d6529f2b1e64c1f599c8cc.png)
