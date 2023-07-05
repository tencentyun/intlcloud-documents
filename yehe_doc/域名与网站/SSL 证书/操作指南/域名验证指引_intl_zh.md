## 操作场景

本文档指导您在申请域名型证书后，验证域名的所有权。
>! 
>- 请尽快添加验证，若您在3天内未添加验证或验证不通过，审核机构将拒绝您此次证书申请。
>- 验证通过后可以在 [证书管理](https://console.cloud.tencent.com/ssl) 下载并安装相关的证书。

域名的所有权可通过以下方式进行验证：
<table>
<thead>
  <tr>
    <th>验证方式</th>
    <th>使用场景</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>手动 DNS 验证</td>
    <td>适用于在任何平台进行解析的域名。</td>
  </tr>
  <tr>
    <td>文件验证</td>
    <td>使用自动 DNS 验证和手动 DNS 验证存在限制的情况下。<br>（操作过程比较复杂，需要一定的建站基础）</td>
  </tr>
</tbody>
</table>

## 前提条件


- 通过 [手动 DNS 验证](#ManualVerification) 方式验证，须完成域名型证书的申请。
- 通过 [文件验证](#FileVerification) 方式验证，须获取登录服务器的帐号和密码。

## 操作步骤

<span id="ManualVerification"></span>
### 手动 DNS 验证
>!以下操作仅针对域名对应的**域名解析商**在腾讯云 DNSPod DNS 解析的情况下，若不在腾讯云 DNSPod DNS 解析，请您到域名对应的**域名解析商**处进行解析。
>
1. 登录 [SSL 证书管理控制台](https://console.cloud.tencent.com/ssl)。
2. 在 “证书列表” 页面，选择待查看证书详情的域名型证书 ID，进入 “证书详情” 页面。如下图所示：<span id="details"></span>
![](https://main.qcloudimg.com/raw/604d809100b1e09dc726de6862b255c3.png)
3. 添加解析记录。
  - 若您的域名（例如 `www.tencent.com`）对应的**域名解析商**在腾讯云 DNSPod DNS 解析。
     1. 请您先找到 [证书详情](#details) 页面，获取主机记录以及记录值。
     
    2. 登录 [DNS 解析控制台](https://console.dnspod.com/dns/list) ，查看已申请证书的域名，并单击操作栏的【解析】，进入【记录管理】页面。
    
    3. 单击【添加记录】，添加记录类型。
    
  - 若您的域名对应的**域名解析商**不在腾讯云，请您先找到 [证书详情](#details) 页面，获取主机记录以及记录值，并到域名对应的**域名解析商**处添加解析记录。
4. 添加成功后，证书对应域名添加记录值的系统会定时检查，若能检测到并且与指定的值匹配，即可完成域名所有权验证。如下图所示：
>?解析生效时间一般为**10分钟 - 24小时**，但各地解析的最终生效取决于各运营商刷新时间，请您耐心等待。
>
![](https://main.qcloudimg.com/raw/5e66519acdd6c874839abfa19a12f310.png)


<span id="FileVerification"></span>
### 文件验证
1. 登录 [SSL 证书管理控制台](https://console.cloud.tencent.com/ssl)。
2. 在 “证书列表” 页面，选择待查看证书详情的域名型证书 ID，进入 “证书详情” 页面。如下图所示：
![](https://main.qcloudimg.com/raw/3ab830438edc0a58c1d2e13209964502.png)
3. 请您登录服务器，并且确保域名已指向该服务器。
>?若您的域名对应的**域名解析商**在腾讯云 DNSPod DNS 解析，将域名指向您的服务器。
>
4. 在网站根目录下，创建指定的文件。该文件包括文件目录、文件名、文件内容。
 >?网站根目录是指您在服务器上存放网站程序的文件夹，大致这几种表示名称：wwwroot、htdocs、public_html、webroot 等。
 >
 >文件名名称与文件内容请根据购买证书后域名验证详情页提示，确定文件名名称与文件内容。
 - **示例**
您的网站根目录为 `C:/inetpub/wwwroot`，您可以在 `wwwroot` 文件夹下创建一个如下表所示的文件：

<table>
<tr><th>文件目录</th><th>文件名</th><th>文件内容</th></tr>
<tr><td>/.well-known/pki-validation</td><td>fileauth.txt</td><td>2019080603......ep939jlu32alzeo</td></tr>
</table>

 - **注意事项**
 Windows 系统下，需通过执行命令行的方式创建以点开头的文件和文件夹。
 例如，创建 `.well-known` 文件夹，请打开命令提示符，执行命令 `mkdir .well-known` 进行创建。如下图所示：
![](https://main.qcloudimg.com/raw/ad4b5c0adaa8d67d6149f7756f1aaebd.png)


5. 打开浏览器，根据验证的域名类型，访问对应的链接地址。
**链接地址格式**：`http://域名/文件目录/文件名`或者 `https://域名/文件目录/文件名`。
访问链接可获取到文件内容，例如 `2019080603......ep939jlu32alzeo`。
 - 如果申请文件验证的域名是 `example.tencent.com`，进行验证访问的链接地址则是 `http://example.tencent.com/.well-known/pki-validation/fileauth.txt` 或者是 `https://example.tencent.com/.well-known/pki-validation/fileauth.txt`。

>?
 > 对于 www 开头的二级域名，例如 `www.tencent.com`，您需进行以下两步操作：
 >- 第一步对该二级域名添加 [文件验证](#FileVerification)。
 >- 第二步对其主域名 `tencent.com` 添加 [文件验证](#FileVerification)（不需要重新申请证书），验证方法按照**链接地址格式**进行验证，验证值显示一致。
 - 如果申请文件验证的域名是泛域名 `*.tencent.com`，进行验证访问的链接地址是 `http://tencent.com/.well-known/pki-validation/fileauth.txt` 或者 `https://tencent.com/.well-known/pki-validation/fileauth.txt`。

>?
 > - 支持 HTTP 和 HTTPS，任意一个均可访问。
 > - 文件验证需要直接响应200状态码和文件内容，不支持任何形式的跳转。


6. 请耐心等待 CA 机构扫描审核。证书颁发完成后，文件和目录即可清除。

>?操作过程如果出现问题，请您 [联系我们](https://intl.cloud.tencent.com/document/product/1007/30951)。


