>! If there are problems with backend adaptation you cannot fix, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.



## Step 1: Create an HTTP/HTTPS Listener

Log in to the [GAAP console](https://console.cloud.tencent.com/gaap). Select **Access Management** > **HTTP/HTTPS Listener Management**. Click **Create** to add an HTTP/HTTPS listener, and then complete configurations required to create the listener and connection.
![](https://qcloudimg.tencent-cloud.cn/raw/c6cb5b89a3b5ecd16766c0d480dd898c.png)


## Step 2: Adapt the Backend Server

The following sections describe the X-Forwarded-For configuration schemes for Nginx, IIS 7, and Apache servers.
- [IIS 7 configuration scheme](#m1)
- [Apache configuration scheme](#m2)
- [Nginx configuration scheme](#m3)

[](id:m1)
### IIS 7 configuration scheme

1. Download and install the [F5XForwardedFor](https://devcentral.f5.com/s/articles/x-forwarded-for-log-filter-for-windows-servers) plugin module, copy `F5XFFHttpModule.dll` and `F5XFFHttpModule.ini` in the `x86\Release` or `x64\Release` directory based on your server operating system version to a certain directory (such as `C:\F5XForwardedFor` in this document), and make sure that the IIS process has read permission to this directory.
2. Select **IIS Server** and double-click **Modules**.
 ![]()
3. Click **Configure Native Modules**.
 ![]()
4. In the pop-up window, click **Register**.
 ![]()
5. Add the downloaded DLL files.
 ![]()
6. After adding the files, check them and click **OK**.
 ![]()
7. Add the above two DLL files in "ISAPI and CGI Restrictions" and set the restrictions to "Allow".
 ![]()
8. Restart the IIS server for the configuration to take effect.


[](id:m2)
### Apache configuration scheme

1. Install the Apache "mod_rpaf" module using the following commands:
```
wget http://stderr.net/apache/rpaf/download/mod_rpaf-0.6.tar.gz
tar zxvf mod_rpaf-0.6.tar.gz
cd mod_rpaf-0.6
/usr/bin/apxs -i -c -n mod_rpaf-2.0.so mod_rpaf-2.0.c
```
2. Modify the Apache configuration file `/etc/httpd/conf/httpd.conf` by adding the following to the end of the file:
```
LoadModule rpaf_module modules/mod_rpaf-2.0.so
RPAFenable On
RPAFsethostname On

RPAFproxy_ips IP address   //The IP address is the forwarding IP of the connection
RPAFheader X-Forwarded-For
```
3. After adding the above content, restart Apache.
```
/usr/sbin/apachectl restart
```

[](id:m3)
### Nginx configuration scheme

1. You can use `http_realip_module` to get the real client IP when Nginx is used as the server. However, this module is not installed in Nginx by default, and you need to recompile Nginx to add `--with-http_realip_module`. The code is as follows:
```
wget  http://nginx.org/download/nginx-1.14.0.tar.gz 
tar  zxvf nginx-1.14.0.tar.gz 
cd nginx-1.14.0
./configure --user=www --group=www --with-http_stub_status_module --without-http-cache --with-http_ssl_module --with-http_realip_module
make
make install
```
2. Modify the `nginx.conf` file.
</br>
<pre><code>vi /etc/nginx/nginx.conf
Modify the configuration fields in red as follows:</br>
fastcgi connect_timeout <span class="hljs-number">300</span><span class="hljs-comment">;</span>
fastcgi send_timeout <span class="hljs-number">300</span><span class="hljs-comment">;</span>
fastcgi read_timeout <span class="hljs-number">300</span><span class="hljs-comment">;</span>
fastcgi buffer_size <span class="hljs-number">64</span>k<span class="hljs-comment">;</span>
fastcgi buffers <span class="hljs-number">4</span> <span class="hljs-number">64</span>k<span class="hljs-comment">;</span>
fastcgi busy_buffers_size <span class="hljs-number">128</span>k<span class="hljs-comment">;</span>
fastcgi temp_file_write_size <span class="hljs-number">128</span>k<span class="hljs-comment">;</span></br>
<a style="color:red">set_real_ip_from IP address<span class="hljs-comment">;   //The IP address is the forwarding IP of the connection</span>
real_ip_header X-Forwarded-For<span class="hljs-comment">;</a></span></code></pre>
3. Restart Nginx.
```
service nginx restart
```
