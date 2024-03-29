本文档将指导您如何在修改 DNS 解析前进行本地测试。
## 操作步骤
本地机器访问网站需要做 DNS 解析，在这之前会优先从本地 hosts 文件中获取目标域名对应的 IP 地址。所以可以用修改 hosts 文件的方式把本地的访问流量导向 Web 应用防火墙，从而测试经过 Web 应用防火墙访问 Web 站点的线路连通性，避免直接修改 DNS 解析记录，影响到公网用户对站点的访问。
1. 登录 [Web 应用防火墙控制台](https://console.cloud.tencent.com/guanjia)，在左侧导航栏中，选择【Web 安全防护】>【防护设置】，在域名列表中查看`waf.qcloudwaf.com`的 CNAME 地址。
<img src="https://main.qcloudimg.com/raw/b03ca645ed87220d5990e924158e3ef5.png" style="zoom:85%;" /><br>
如需要获取对应域名的 VIP 地址，可通过 ping 该 CNAME 地址获取。
 1. 在 Windows 操作系统中，打开 cmd 命令行工具。
 2. 执行以下命令：`ping <已复制的 WAF CNAME 地址>` 。
 ![](https://main.qcloudimg.com/raw/3bd7ecefb96c13462275c0f871e90231.png)
 3. 在 ping 命令的返回结果中，记录域名对应的 WAF IP 地址，即为后续操作需要的 VIP 地址。
2. 修改 hosts 文件。
	- 在 Windows 下修改`C:\Windows\System32\drivers\etc\hosts`，增加条目。
	格式：VIP 地址+接入网站管家的域名。
 ![](https://main.qcloudimg.com/raw/1ccf20053b32d72dbf8156454517705e.png)
	- 在 Linux 下 修改`/etc/hosts`，增加条目。
格式：VIP 地址+接入网站管家的域名。
 ![3](https://main.qcloudimg.com/raw/76551c1dcd21686169eaf2db8110494a.png)
3. 访问测试 
	1. 在本地电脑上访问 Web 站点，若站点能够正常打开，说明网站管家访问 Web 源站的线路连通性正常。
	2. 在浏览器中输入下面的网址并访问。

```
http://waf.qcloudwaf.com/?test=alert(123)  
```
	3. 浏览器返回阻断页面，说明 Web 应用防火墙防护功能正常。
	>?该拦截页面，可以通过访问： [Web应用防火墙(WAF)默认提示页面](http://www.qcloudwaf.com/?alert(1=1) ) 获取。
![](https://main.qcloudimg.com/raw/253fdfbae2d6529f2b1e64c1f599c8cc.png)



## 后续步骤
当您完成本地测试后，可执行如下步骤：
- [步骤 3：修改 DNS 解析](https://intl.cloud.tencent.com/zh/document/product/627/35653)
- [步骤 4：设置安全组](https://intl.cloud.tencent.com/zh/document/product/627/35654)
