## Getting Real Client IP in WAF
WAF uses a reverse proxy to protect your website. When you access a WAF-protected domain name, a `X-Forwarded-For` record will be added to the HTTP header field to record your real IP, such as `X-Forwarded-For:user IP`. If the accessed domain name has proxies at multiple levels, WAF will record the IP of the proxy server just before WAF, for example:
Scenario 1: User > WAF > real server, with `X-Forwarded-For` recorded as `X-Forwarded-For:user's real IP`
Scenario 2: User > CDN > WAF > real server, with `X-Forwarded-For` recorded as `X-Forwarded-For:user's real IP,X-Forwarded-For:CDN origin-pull address`

>?
>- In scenario 2, you need to select **Yes** for **Use proxy** when [adding a domain name](https://console.cloud.tencent.com/guanjia/waf/config/add) in WAF. After the proxy is connected, the client IP may be forged, but this will not be the case if Tencent Cloud CDN is used, as it will reset the `X-Forwarded-For` information and enter only the client IP it has obtained. (If a proxy is used, attackers can launch attacks only if they can send requests directly to the WAF VIP address. When the proxy is connected, the WAF VIP address cannot be detected by users. Be sure to keep the WAF VIP confidential.)
>- For more information on CLB WAF connection, see [Obtaining Real Client IPs over IPv4 CLBs](https://intl.cloud.tencent.com/document/product/214/3728).

Below are commonly used `X-Forwarded-For` configuration schemes for application servers:
 - [IIS 7 Configuration Scheme](#IIS7)
 - [Apache Configuration Scheme](#Apache)
 - [NGINX Configuration Scheme](#Nginx)


## [IIS 7 Configuration Scheme](id:IIS7)
1. Download and install the [F5XForwardedFor](https://devcentral.f5.com/s/articles/x-forwarded-for-log-filter-for-windows-servers) plugin module, copy `F5XFFHttpModule.dll` and `F5XFFHttpModule.ini` in the `x86\Release` or `x64\Release` directory based on your server OS to a certain directory (such as `C:\F5XForwardedFor`), and make sure that the IIS process has read permission to this directory.
2. Select **IIS Server** and double-click **Modules**.
3. Click **Configure Native Modules**.
4. In the pop-up box, click **Register**.
5. Add the downloaded DLL files.
6. After adding the files, check them and click **OK**.
7. Add the above two DLL files in "ISAPI and CGI Restrictions" and set the restrictions to "Allow".
8. Restart the IIS server for the configuration to take effect.


## [Apache Configuration Scheme](id:Apache)
1. Install the Apache "mod_rpaf" module using the following commands:
```
wget http://stderr.net/apache/rpaf/download/mod_rpaf-0.6.tar.gz
tar zxvf mod_rpaf-0.6.tar.gz
cd mod_rpaf-0.6
/usr/bin/apxs -i -c -n mod_rpaf-2.0.so mod_rpaf-2.0.c
```
2. Modify the Apache configuration file `/etc/httpd/conf/httpd.conf` by adding the following to the end of the file:
<pre>
LoadModule rpaf_module modules/mod_rpaf-2.0.so
RPAFenable On
RPAFsethostname On
<font color="red">
RPAFproxy_ips IP   // The IP address is the origin-pull IP address of the WAF-protected domain name. You can view it in the protected domain name list in the <a href="https://console.cloud.tencent.com/guanjia/waf/config">WAF console</a> or in the backend logs of the server. You only need to enter all the IP addresses that need to be viewed.
RPAFheader X-Forwarded-For
</font>
</pr>
3. After adding the above content, restart Apache.
```
/usr/sbin/apachectl restart
```


## [NGINX Configuration Scheme](id:Nginx)
1. You can use `http_realip_module` to get the real client IP when NGINX is used as the server. However, this module is not installed in NGINX by default, so you need to recompile NGINX to add `--with-http_realip_module`. The code is as follows:
```
wget  http://nginx.org/download/nginx-1.14.0.tar.gz 
tar  zxvf nginx-1.14.0.tar.gz 
cd nginx-1.14.0
./configure --user=www --group=www --with-http_stub_status_module --without-http-cache --with-http_ssl_module --with-http_realip_module
make
make install
```
2. Modify the `nginx.conf` file.
```

vi /etc/nginx/nginx.conf
```
Modify the content in red as shown below:
<div class="code">
<p>
</p>
<pre>  
fastcgi connect_timeout 300;
fastcgi send_timeout 300;
fastcgi read_timeout 300;
fastcgi buffer_size 64k;
fastcgi buffers 4 64k;
fastcgi busy_buffers_size 128k;
fastcgi temp_file_write_size 128k;
<font color="red">
set_real_ip_from IP;   // The IP address is the origin-pull IP address of the WAF-protected domain name. You can view it in the connected domain name list in the <a href="https://console.cloud.tencent.com/guanjia/instance/domain">WAF console</a>.
real_ip_header X-Forwarded-For;
 </font>
</pre>
</div>

3. Restart NGINX.
<pre>
service nginx restart
</pre>
