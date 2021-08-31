## Notes on Getting Real Client IPs by CLB
All layer-4 (TCP/UDP/TCP SSL) and layer-7 (HTTP/HTTPS) CLB services support getting a real client IP directly on a backend CVM instance with no additional configuration required.
- For layer-4 CLB, the source IP obtained on the backend CVM instance is the client IP.
- For layer-7 CLB, you can use the `X-Forwarded-For` or `remote_addr` field to directly get the client IP. For the access logs of layer-7 CLB, please see [Storing Access Logs in CLS](https://intl.cloud.tencent.com/document/product/214/35063). 

>?
>- For layer-4 CLB instances, the client IP can be directly obtained with no additional configuration required on the backend CVM instance.
>- For other layer-7 load balancing services with SNAT enabled, you need to configure the backend CVM instance and then use `X-Forwarded-For` to get the real client IP.

Below are commonly used application server configuration schemes.

## IIS 6 Configuration Scheme
1. Download and install the [F5XForwardedFor](https://devcentral.f5.com/s/articles/x-forwarded-for-log-filter-for-windows-servers) plugin module, copy `F5XForwardedFor.dll` in the `x86\Release` or `x64\Release` directory based on your server operating system version to a certain directory (such as `C:\ISAPIFilters` in this document), and make sure that the IIS process has read permission to this directory.
2. Open the IIS Manager, find the currently opened website, right-click the website, and select **Properties** to open the properties page.
3. On the properties page, switch to **ISAPI Filters** and click **Add** to pop up the "Add" window.
4. In the "Add" window, enter "F5XForwardedFor" for "Filter Name" and the full path to `F5XForwardedFor.dll` for "Executable" and then click **OK**.
5. Restart the IIS server for the configuration to take effect.

## IIS 7 Configuration Scheme
1. Download and install the [F5XForwardedFor](https://devcentral.f5.com/s/articles/x-forwarded-for-log-filter-for-windows-servers) plugin module, copy `F5XFFHttpModule.dll` and `F5XFFHttpModule.ini` in the `x86\Release` or `x64\Release` directory based on your server operating system version to a certain directory (such as `C:\x_forwarded_for` in this document), and make sure that the IIS process has read permission to this directory.
2. Select **IIS Server** and double-click **Modules**.
![](https://main.qcloudimg.com/raw/21372379584488e72ae3d22af44a5017.png)
3. Click **Configure Native Modules**.
![](https://main.qcloudimg.com/raw/280f11e95b7ac8cd4a754d98ad0cd2b7.png)
4. In the pop-up box, click **Register**.
![](https://main.qcloudimg.com/raw/1d6f7bd38077f2c9f089eb84a1995aa1.png)
5. Add the downloaded DLL files as shown below:
![](https://main.qcloudimg.com/raw/354a35a203c24d802d59782c91dfe02a.png)
6. After adding the files, check them and click **OK**.
![](https://main.qcloudimg.com/raw/9fffdfa02fba225f13090ef2598e1c0e.png)
7. Add the above two DLL files in "ISAPI and CGI Restrictions" and set the restrictions to "Allow".
![](https://main.qcloudimg.com/raw/8585122da39f14d734eb9d6ded7e486c.png)
8. Restart the IIS server for the configuration to take effect.

## Apache Configuration Scheme
1. Install the third-party Apache module "mod_rpaf".
```
wget http://stderr.net/apache/rpaf/download/mod_rpaf-0.6.tar.gz
tar zxvf mod_rpaf-0.6.tar.gz
cd mod_rpaf-0.6
/usr/bin/apxs -i -c -n mod_rpaf-2.0.so mod_rpaf-2.0.c
```
2. Modify the Apache configuration `/etc/httpd/conf/httpd.conf` by adding the following to the end of the file:
```
LoadModule rpaf_module modules/mod_rpaf-2.0.so
RPAFenable On
RPAFsethostname On
RPAFproxy_ips IP address (this is not the public IP provided by CLB. For the specific IP, please query the Apache logs. Generally, there are two IP addresses and you need to enter both of them)
RPAFheader X-Forwarded-For
```
3. After adding the above content, restart Apache.
```
/usr/sbin/apachectl restart
```

## Nginx Configuration Scheme
1. You can use `http_realip_module` to get the real client IP when Nginx is used as the server. However, this module is not installed in Nginx by default, and you need to recompile Nginx to add `--with-http_realip_module`.
```
wget  http://nginx.org/download/nginx-1.14.0.tar.gz 
tar  zxvf nginx-1.14.0.tar.gz 
cd nginx-1.14.0
./configure --user=www --group=www --with-http_stub_status_module --without-http-cache --with-http_ssl_module --with-http_realip_module
make
make install
```
2. Modify `nginx.conf`.
```
vi /etc/nginx/nginx.conf
```
Modify the content in red as follows:
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
<font color="#f2777a">
set_real_ip_from IP address; (this is not the public IP provided by CLB. For the specific IP, please query the Nginx logs. You need to enter all IP addresses if there are multiple ones)
real_ip_header X-Forwarded-For;
 </font>
</pre>
</div>
3. Restart Nginx.
```
service nginx restart
```
