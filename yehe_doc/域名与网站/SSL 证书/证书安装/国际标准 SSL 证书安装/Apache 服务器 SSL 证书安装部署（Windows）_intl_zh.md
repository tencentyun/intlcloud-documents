## 操作场景

本文档指导您如何在 Apache 服务器中安装 SSL 证书。

>?
>
> - 本文档以证书名称 `cloud.tencent.com` 为例。
> - Apache 版本以 `Apache/2.4.53` 为例。默认端口为 `80`。您可前往 [Apache 官网](https://httpd.apache.org/download.cgi/) 进行下载，若您需要采用其余版本，请您 [联系我们](https://intl.cloud.tencent.com/document/product/1007/30951)。
> - 当前服务器的操作系统为 Windows Server 2012 R2，由于操作系统的版本不同，详细操作步骤略有区别。
> - 安装 SSL 证书前，请您在 Apache 服务器上开启 “443” 端口，避免证书安装后无法启用 HTTPS。具体可参考 [服务器如何开启443端口？](https://intl.cloud.tencent.com/document/product/1007/36738)
> - SSL 证书文件上传至服务器方法可参考 [如何将本地文件拷贝到云服务器](https://intl.cloud.tencent.com/document/product/213/34821)。


## 前提条件
- 已在当前服务器中安装配置 Apache 服务。

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


   >?
   >
   > 在腾讯云官网购买的云服务器，您可以登录 [云服务器控制台](https://console.cloud.tencent.com/cvm)  获取服务器 IP 地址、用户名及密码。
   >


## 操作步骤

### 步骤1：上传证书文件
1. 请在 [SSL 证书管理控制台](https://console.cloud.tencent.com/ssl) 中选择您需要安装的证书并单击**下载**。

2. 在弹出的 “证书下载” 窗口中，服务器类型选择 **Apache**，单击**下载**并解压缩 `cloud.tencent.com` 证书文件包到本地目录。
解压缩后，可获得相关类型的证书文件。 其中包含 `cloud.tencent.com_apache` 文件：

  - **文件夹名称**：`cloud.tencent.com_apache`

  - **文件夹内容**：

    - `root_bundle.crt` 证书文件

    - `cloud.tencent.com.crt` 证书文件

    - `cloud.tencent.com.key` 私钥文件

    - `cloud.tencent.com.csr` CSR 文件
      

         >?
         > CSR 文件是申请证书时由您上传或系统在线生成的，提供给 CA 机构。安装时可忽略该文件。
         >

3. 通过 RDP 登录 Apache 服务器。
   

   >?
   >   - 通过 RDP 上传文件可参考 [通过 RDP 方式上传文件到云服务器](https://intl.cloud.tencent.com/document/product/213/34822)。
   >   - 若您需部署到腾讯云云服务器，建议使用云服务器的文件上传功能。

4. 将已获取到的 `root_bundle.crt` 证书文件、`cloud.tencent.com.crt` 证书文件以及 `cloud.tencent.com.key` 私钥文件从本地目录拷贝到 Apache 服务器目录的 `\conf` 目录的下的 `ssl.crt` 与 `ssl.key` 文件夹。

<table>
<tr>
<td rowspan="1" colSpan="1" >SSL 证书文件</td>
<td rowspan="1" colSpan="1" >对应文件夹</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >root_bundle.crt</td>
<td rowspan="2" colSpan="1" >ssl.crt</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >cloud.tencent.com.crt</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >cloud.tencent.com.key</td>
<td rowspan="1" colSpan="1" >ssl.key</td>
</tr>
</table>


### 步骤2：配置文件
1. 使用文本编辑器，打开 Apache 服务器 `conf` 目录下 `httpd.conf` 文件，并删除以下字段前 `#` 注释符。

   ``` java
   #LoadModule ssl_module modules/mod_ssl.so
   #Include conf/extra/httpd-ssl.conf
   ```
2. 使用文本编辑器，打开 Apache 服务器 `conf\extra` 目录下 `httpd-ssl.conf` 文件。

3. 修改 `httpd-ssl.conf` 文件，将以下字段参数设置为上传的证书文件路径，如下所示：

   ``` java
   SSLCertificateFile "C:/apache/conf/ssl.crt/cloud.tencent.com.crt"
   SSLCertificateKeyFile "C:/apache/conf/ssl.key/cloud.tencent.com.key"
   SSLCACertificateFile "C:/apache/conf/ssl.crt/root_bundle.crt"
   ```
4. 重新启动 Apache 服务器，即可使用 `https://cloud.tencent.com` 进行访问。

- 如果浏览器地址栏显示安全锁标识，则说明证书安装成功。

- 如果网站访问异常，可参考以下常见问题解决方案进行处理：

    - [无法使用 HTTPS 访问网站](https://intl.cloud.tencent.com/document/product/1007/39821)

    - [部署 SSL 证书后，浏览器提示 “网站连接不安全”](https://intl.cloud.tencent.com/document/product/1007/40674)

    - [访问站点提示连接不安全？](https://intl.cloud.tencent.com/document/product/1007/30184)

    - [在服务器上部署 SSL 证书后访问资源出现 404 报错](https://intl.cloud.tencent.com/document/product/1007/39820)


### HTTP 自动跳转 HTTPS 的安全配置（可选）
1. 使用文本编辑器，打开 Apache 服务器 `conf` 目录下 `httpd.conf` 文件，并删除以下字段前 `#` 注释符。

   ``` java
   #LoadModule rewrite_module modules/mod_rewrite.so
   ```
2. 并在网站运行目录配置字段。如： `<Directory "C:/xampp/htdocs">` 字段中添加如下内容：

   ``` java
   <Directory "C:/xampp/htdocs">
   RewriteEngine on
   RewriteCond %{SERVER_PORT} !^443$
   RewriteRule ^(.*)?$ https://%{SERVER_NAME}%{REQUEST_URI} [L,R]
   </Directory>
   ```
3. 重新启动 Apache 服务器，即可使用 `https://www.tencentcloud.com/` 与 `https://www.tencentcloud.com/` 进行访问。访问后都将自动跳转到 `https://www.tencentcloud.com/`。
