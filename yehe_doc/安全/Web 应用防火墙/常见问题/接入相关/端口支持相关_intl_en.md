### Which ports does WAF support?
You can view and configure the ports supported by WAF in the console.
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Web security protection** > **Protection settings** on the left sidebar.
2. On the **Protection settings** page, click **Add domain name**.
3. In **Server configuration** on the **Add domain name** page, select the target protocol to view and configure the port. You can configure up to five ports for one domain name.
	- By default, WAF Premium supports HTTP (80/8080) and HTTPS (443/8443) standard ports but not non-standard ports.
	- WAF Enterprise and Ultimate support non-standard ports in addition to the default HTTP (80/8080) and HTTPS (443/8443) standard ports as listed below:
<table>
<tr><th width="14%">Protocol</th><th>Port</th></tr>
<tr><td>HTTP</td><td>80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 97, 800, 805, 808, 1000, 1090, 2020, 3333, 3501, 3601, 5000, 5222, 6001, 6666, 7000, 7001, 7002, 7003, 7004, 7005, 7006, 7007, 7008, 7009, 7010, 7011, 7012, 7013, 7014, 7015, 7016, 7018, 7019, 7020, 7021, 7022, 7023, 7024, 7025, 7026, 7040, 7070, 7081, 7082, 7083, 7088, 7097, 7510, 7621, 7777, 7800, 8000, 8002, 8003, 8004, 8005, 8006, 8007, 8008, 8009, 8010, 8011, 8012, 8020, 8021, 8022, 8060, 8025, 8026, 8060, 8077, 8078, 8080, 8081, 8082, 8083, 8086, 8087, 8088, 8089, 8090, 8106, 8181, 8182, 8184, 8210, 8215, 8334, 8336, 8445, 8686, 8800, 8888, 8889, 8999, 9000, 9001, 9002, 9003, 9021, 9023, 9027, 9037, 9080, 9081, 9082, 9180, 9182, 9200, 9201, 9205, 9207, 9208, 9209, 9210, 9211, 9212, 9213, 9898, 9908, 9916, 9918, 9919, 9928, 9929, 9939, 10000, 10001, 10080, 10083, 12601, 20080, 20083, 25060, 28080, 28080, 33702, 48800, and 52301 </td></tr>
<tr><td>HTTPS</td><td>443, 4443, 5100, 5200, 5443, 6443, 7443, 8084, 8085, 8091, 8442, 8443, 8553, 8663, 9443, 9550, 9553, 9663, 10803, and 18980</td></tr>
</table>
<blockquote class="d-mod-explain">
							<div class="d-mod-title d-explain-title">
								<i class="d-icon-explain"></i>Note:
							</div>
               <p></p>
<ul>
<li>If you use Ultimate Edition and need to protect ports not included in the HTTP or HTTPS list, WAF offers the non-standard port customization service (for ports 1–65535). You can customize up to five non-standard ports for all domain names in your plan. If you need this service, <a href="https://console.cloud.tencent.com/workorder/category?level1_id=141&amp;level2_id=642&amp;source=0&amp;data_title=T-Sec-Web%E5%BA%94%E7%94%A8%E9%98%B2%E7%81%AB%E5%A2%99&amp;level3_id=866&amp;radio_title=%E8%87%AA%E5%AE%9A%E4%B9%89%E9%98%B2%E6%8A%A4%E7%AD%96%E7%95%A5&amp;queue=15&amp;scene_code=31044&amp;step=2" target="_blank">submit a ticket</a> to contact WAF_hepler for assistance.</li>
<li>Ports already in the HTTP or HTTPS list cannot be customized for other protocols.</li>
<li><strong>If you need HTTP and HTTPS non-standard ports, <a href="https://console.cloud.tencent.com/workorder/category?level1_id=141&amp;level2_id=642&amp;source=0&amp;data_title=T-Sec-Web%E5%BA%94%E7%94%A8%E9%98%B2%E7%81%AB%E5%A2%99&amp;level3_id=866&amp;radio_title=%E8%87%AA%E5%AE%9A%E4%B9%89%E9%98%B2%E6%8A%A4%E7%AD%96%E7%95%A5&amp;queue=15&amp;scene_code=31044&amp;step=2" target="_blank">submit a ticket</a> to have them added to the allowlist by WAF_hepler<strong>.
</ul>

