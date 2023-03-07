## 操作场景

云点播开放 CDN 托管能力帮助用户分发自有源站的媒体资源，支持自有源站和第三方对象存储源站的回源能力。用户通过创建自定义域名并配置源站类型、回源请求协议和源站地址等信息，便可实现自定义源站功能（仅支持自定义域名配置自定义回源能力）。

## 配置指南
1. 登录 [云点播控制台](https://console.cloud.tencent.com/vod)，单击左侧导航栏**应用管理**，进入应用列表页。
2. 找到需要设置的应用，点击应用名称进入应用管理页。
3. 默认进入**媒资管理**>**音视频管理**，“已上传”页面。
4. 选择左侧导航栏**分发播放设置**>[**域名管理**](https://console.cloud.tencent.com/vod/distribute-play/domain)，进入**域名管理**页面。
5. 单击顶部**自定义源站加速域名**，进入”自定有源站加速域名“列表页。
![img](https://qcloudimg.tencent-cloud.cn/raw/f0536b39ee6156173e7cd27b3642f791.png)
6. 单击**添加域名**，根据实际需求完成域名配置和源站配置：
 - 域名配置
填写域名名称和选择域名加速区域，相关内容请参见 [添加域名](https://intl.cloud.tencent.com/document/product/266/35572)。
![](https://qcloudimg.tencent-cloud.cn/raw/ceb83e97ffdd3118c4890c13a68c6971.png)
 - 源站配置
![](https://qcloudimg.tencent-cloud.cn/raw/43279ccef236c0211c4b996f8ff92fd6.png)

**源站类型**
云点播提供自有源站和第三方对象存储的三种回源类型，用户可根据实际需求选择配置。
<table>
   <tr>
      <td >自有源站</td>
      <td >已经拥有稳定运行的业务服务器（即源站），填充对应的 IP 地址列表、或一个域名作为源站地址。</td>
   </tr>
   <tr>
      <td>第三方对象存储</td>
      <td>腾讯云以外的第三方对象存储，目前支持的第三方为：阿里云 OSS 和 AWS S3。</td>
   </tr>
</table>

**回源协议**
云点播加速节点回源到用户源站时使用的协议，HTTP 或 HTTPS。
<table>
   <tr>
      <td >HTTP 回源</td>
      <td>访问为 HTTP、HTTPS 时均使用 HTTP 回源。</td>
   </tr>
   <tr>
      <td>HTTPS 回源</td>
      <td>访问为 HTTP、HTTPS 时均使用 HTTPS 回源。</td>
   </tr>
	    <tr>
      <td>协议跟随</td>
      <td>HTTP 请求使用 HTTP 回源，HTTPS 请求使用 HTTPS 回源。</td>
   </tr>
</table>

>? 存在 HTTPS 回源情况下，请保证源站支持 HTTPS 访问，否则会导致回源失败。

**源站地址**

<table>
   <tr>
      <td>自有源站</td>
      <td>支持填充多个 IP 源站或一个域名源站（用逗号分隔）。</td>
   </tr>
   <tr>
      <td>第三方对象存储</td>
      <td><li>若资源已存储在第三方对象存储中，请输入有效的存储桶访问地址作为源站（不可包含 `http://` 或 `http://` 协议头），当前支持的第三方为：阿里云 OSS 和 AWS S3。 </li><br><li>回源至第三方私有存储桶，需填写有效密钥并开启回源鉴权，即开启私有存储桶访问，请查看 <a href="https://www.tencentcloud.com/document/product/266/53277">访问密钥获取指引</a>。</li> </td>
   </tr>
</table>

>? 自有源站可指定回源 HOST，回源 HOST 用于指定 CDN 节点在回源时，在源站访问的站点域名/ip的具体站点。若未指定回源 HOST，默认取当前所创建的加速域名。
4. 域名解析，针对已添加的自定义加速域名，您需要在该域名指定的 DNS 服务商配置 CNAME，用户才能通过域名访问到您的视频媒体，具体操作请参见 [点播加速域名-域名解析](https://intl.cloud.tencent.com/document/product/266/35572#.E8.A7.A3.E6.9E.90.E5.9F.9F.E5.90.8D)。


## 修改回源配置
针对已添加的自定义域名，可根据用户实际需求进行调整修改。修改方式如下：
1. [**域名管理**](https://console.cloud.tencent.com/vod/distribute-play/domain)>**自定义源站加速域名**页面下，选择需要修改自定义域名，单击**设置**，进入详情页面。
2. 单击**修改**，可对原配置信息进行修改，修改结果生效需要5分钟。
![](https://qcloudimg.tencent-cloud.cn/raw/5df5f46ec7dc7fdc55f9bc3b780f8ac7.png)

>?
>- 用户自定义源站切换至云点播源站时，需要先停用自定义源站域名并进行删除后，然后在点播加速域名中添加对应域名。
>- 用户需要使用自定义源站回源时，必须先停用在点播加速域名中配置的域名并删除后，再前往自定义源站加速域名下进行添加。