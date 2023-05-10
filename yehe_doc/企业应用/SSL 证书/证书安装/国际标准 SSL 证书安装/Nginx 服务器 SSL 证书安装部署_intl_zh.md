以下视频将为您进一步介绍在 Nginx 服务器安装 SSL 证书的操作过程：



## 操作场景

本文档指导您如何在 Nginx 服务器中安装 SSL 证书。

> **说明**
> 
> - 本文档以证书名称 `cloud.tencent.com` 为例。
> - Nginx 版本以 `nginx/1.18.0` 为例。
> - 当前服务器的操作系统为 CentOS 7，由于操作系统的版本不同，详细操作步骤略有区别。
> - 安装 SSL 证书前，请您在 Nginx 服务器上开启 HTTPS 默认端口 `443`，避免证书安装后无法启用 HTTPS。具体可参考 [服务器如何开启443端口？](https://intl.cloud.tencent.com/document/product/1007/36738)
> - SSL 证书文件上传至服务器方法可参考 [如何将本地文件拷贝到云服务器](https://intl.cloud.tencent.com/document/product/213/34821)。


## 前提条件
- 已准备文件远程拷贝软件，例如 WinSCP（建议从官方网站获取最新版本）。
若您需部署到腾讯云云服务器，建议使用云服务器的文件上传功能。

- 已准备远程登录工具，例如 PuTTY 或者 Xshell（建议从官方网站获取最新版本）。

- 已在当前服务器中安装配置含有 `http_ssl_module` 模块的 Nginx 服务。

- 安装 SSL 证书前需准备的数据如下：

<table>
<tr>
<td rowspan="1" colSpan="1" >名称</td>
<td rowspan="1" colSpan="1" >说明</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >服务器的 IP 地址</td>
<td rowspan="1" colSpan="1" >服务器的 IP 地址，用于 PC 连接到服务器。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >用户名</td>
<td rowspan="1" colSpan="1" >登录服务器的用户名。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >密码</td>
<td rowspan="1" colSpan="1" > 登录服务器的密码。</td>
</tr>
</table>


   > **说明**
   > 
   > 在腾讯云官网购买的云服务器，您可以登录 [云服务器控制台](https://console.cloud.tencent.com/cvm)  获取服务器 IP 地址、用户名及密码。
   > 


## 操作步骤

### 证书安装
1. 请在 [SSL 证书管理控制台](https://console.cloud.tencent.com/ssl) 中选择您需要安装的证书并单击**下载**。

2. 在弹出的 “证书下载” 窗口中，服务器类型选择 **Nginx**，单击**下载**并解压缩 `cloud.tencent.com` 证书文件包到本地目录。
解压缩后，可获得相关类型的证书文件。其中包含 `cloud.tencent.com_nginx` 文件夹：

  - **文件夹名称**：`cloud.tencent.com_nginx`

  - **文件夹内容**：

    - `cloud.tencent.com_bundle.crt` 证书文件

    - `cloud.tencent.com_bundle.pem` 证书文件（可忽略该文件）

    - `cloud.tencent.com.key` 私钥文件

    - `cloud.tencent.com.csr` CSR 文件
      

         > **说明**
         > 
         > CSR 文件是申请证书时由您上传或系统在线生成的，提供给 CA 机构。安装时可忽略该文件。
         > 

3. 使用 “WinSCP”（即本地与远程计算机间的复制文件工具）登录 Nginx 服务器。
   

> **说明**
>   - WinSCP 上传文件操作可参考 [通过 WinSCP 上传文件到 Linux 云服务器](https://intl.cloud.tencent.com/document/product/213/2131)。
>   - 若您需部署到腾讯云云服务器，建议使用云服务器的文件上传功能。

4. 将已获取到的 `cloud.tencent.com_bundle.crt` 证书文件和 `cloud.tencent.com.key` 私钥文件从本地目录拷贝到 Nginx 服务器的 ` /etc/nginx` 目录（此处为 Nginx 默认安装目录，请根据实际情况操作）下。

5. 远程登录 Nginx 服务器。例如，使用 [“PuTTY” 工具](https://intl.cloud.tencent.com/document/product/213/32502) 登录。

6. 编辑 Nginx 根目录下的 `nginx.conf` 文件。修改内容如下：
   

   > **说明**
   > 
   >   - 如找不到以下内容，可以手动添加。可执行命令 nginx -t ，找到nginx的配置文件路径。

   > 如下图示例：![tapd_10132091_base64_1665978617_57.png](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027538067/adbfd11a705911ed8e7e525400463ef7.png?q-sign-algorithm=sha1&q-ak=AKID5CThzZqTVXoRP-XYu2W42mAW62aDoOr6DTPyCZ1RRCQ2qwekuFJNzWTp8i6N4A_9&q-sign-time=1677222539;1677226139&q-key-time=1677222539;1677226139&q-header-list=&q-url-param-list=&q-signature=3c4f3c6b131cc016fe546fe716e983e223eb2b12&x-cos-security-token=5xuAVtZg45zZx30psQ7oVmxUqVP8A8ya8376edc7adf43654fa9e4760c181e126Vc733LJenzJOwBNGjj5ASnnvUWi-SYW0Lm3ieNVenmwlNjhySGIa0zlYq_CpEqylsynWkMxc8b3eU8D7h6FUlSv10ulkppQrv-An-d-Sq44sdT76zQjHU5jOHhrqcH_VcRBf_r4SVKfC6tdxleYfVk9IuS2Ak7BlaPUTjsCWemcXhwiqi_eFblusvSP4WUBTw1-jNyR2PWZdzXuJocrrXCfDRX32-AiXXUEV4RUQ9a6DNqpZ1CfF0-h7skkHIP5vkHh-oF1DNW5fMCA3OgZvYOCu6L5eXVf-TPCzxdSJXdJfBA-FS11cvWB2EfUqbeHUX3HPLOBD8r5KniAxFv3bQ3UaBmn-LjxSGA80smlihp_WCCnGD71_08lW6wD_7syk)
   > 
>   - 此操作可通过执行 `vim /etc/nginx/nginx.conf` 命令行编辑该文件。
>   - 由于版本问题，配置文件可能存在不同的写法。例如：Nginx 版本为 `nginx/1.15.0` 以上请使用 `listen 443 ssl` 代替 `listen 443` 和 `ssl on`。

   ``` bash
   server {
        #SSL 默认访问端口号为 443
        listen 443 ssl; 
        #请填写绑定证书的域名
        server_name cloud.tencent.com; 
        #请填写证书文件的相对路径或绝对路径
        ssl_certificate cloud.tencent.com_bundle.crt; 
        #请填写私钥文件的相对路径或绝对路径
        ssl_certificate_key cloud.tencent.com.key; 
        ssl_session_timeout 5m;
        #请按照以下协议配置
        ssl_protocols TLSv1.2 TLSv1.3; 
        #请按照以下套件配置，配置加密套件，写法遵循 openssl 标准。
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE; 
        ssl_prefer_server_ciphers on;
        location / {
            #网站主页路径。此路径仅供参考，具体请您按照实际目录操作。
            #例如，您的网站主页在 Nginx 服务器的 /etc/www 目录下，则请修改 root 后面的 html 为 /etc/www。
            root html; 
            index  index.html index.htm;
        }
    }
   ```
7. 通过执行以下命令验证配置文件问题。

   ``` bash
   nginx -t
   ```
  - 若存在，请您重新配置或者根据提示修改存在问题。

  - 若不存在，请执行 [步骤8](https://write.woa.com/#step8)。

8. 通过执行以下命令重载 Nginx。

   ``` bash
   nginx -s reload
   ```
9. 重载成功，即可使用 `https://cloud.tencent.com` 进行访问。


### HTTP 自动跳转 HTTPS 的安全配置（可选）

如果您需要将 HTTP 请求自动重定向到 HTTPS。您可以通过以下操作设置：
1. 根据实际需求，选择以下配置方式：

  - 在页面中添加 JS 脚本。

  - 在后端程序中添加重定向。

  - 通过 Web 服务器实现跳转。

  - Nginx 支持 rewrite 功能。若您在编译时没有去掉 pcre，您可在 HTTP 的 server 中增加 `return 301 https://$host$request_uri;`，即可将默认80端口的请求重定向为 HTTPS。修改如下内容：
    

      > **说明**
      > 
>     - 未添加注释的配置语句，您按照下述配置即可。
>     - 由于版本问题，配置文件可能存在不同的写法。例如：Nginx 版本为 `nginx/1.15.0` 以上请使用 `listen 443 ssl` 代替 `listen 443` 和 `ssl on`。

      ``` bash
      server {
       #SSL 默认访问端口号为 443
       listen 443 ssl;
       #请填写绑定证书的域名
       server_name cloud.tencent.com; 
       #请填写证书文件的相对路径或绝对路径
       ssl_certificate  cloud.tencent.com_bundle.crt; 
       #请填写私钥文件的相对路径或绝对路径
       ssl_certificate_key cloud.tencent.com.key; 
       ssl_session_timeout 5m;
       #请按照以下套件配置，配置加密套件，写法遵循 openssl 标准。
       ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
       #请按照以下协议配置
       ssl_protocols TLSv1.2 TLSv1.3;
       ssl_prefer_server_ciphers on;
       location / {
         #网站主页路径。此路径仅供参考，具体请您按照实际目录操作。 
         #例如，您的网站主页在 Nginx 服务器的 /etc/www 目录下，则请修改 root 后面的 html 为 /etc/www。
         root html;
         index index.html index.htm;
       }
      }
      server {
       listen 80;
       #请填写绑定证书的域名
       server_name cloud.tencent.com; 
       #把http的域名请求转成https
       return 301 https://$host$request_uri; 
      }
      ```
2. 通过执行以下命令验证配置文件问题。

   ``` bash
   nginx -t
   ```
  - 若存在，请您重新配置或者根据提示修改存在问题。

  - 若不存在，请执行 [步骤3](https://write.woa.com/#step3)。

3. 通过执行以下命令重载 Nginx。

   ``` bash
   nginx -s reload
   ```
4. 重载成功，即可使用 `https://cloud.tencent.com` 进行访问。

  - 如果浏览器地址栏显示安全锁标识，则说明证书安装成功。

  - 如果网站访问异常，可参考以下常见问题解决方案进行处理：

    - [无法使用 HTTPS 访问网站](https://intl.cloud.tencent.com/document/product/1007/39821)

    - [部署 SSL 证书后，浏览器提示 “网站连接不安全”](https://intl.cloud.tencent.com/document/product/1007/40674)

    - [访问站点提示连接不安全？](https://intl.cloud.tencent.com/document/product/1007/30184)

    - [在服务器上部署 SSL 证书后访问资源出现 404 报错](https://intl.cloud.tencent.com/document/product/1007/39820)
      

         > **注意**
         > 
         > 操作过程如果出现问题，请您 [联系我们](https://intl.cloud.tencent.com/document/product/1007/30951)。
         > 
