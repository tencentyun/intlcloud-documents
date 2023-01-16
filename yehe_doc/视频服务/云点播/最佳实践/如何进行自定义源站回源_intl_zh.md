## 简介

自定义源站回源依托于云点播 CDN 能力，通过创建自定义域名并配置回源信息，用户可将存储在第三方源站媒体文件借助云点播进行加速分发，提供给用户在多云场景下的媒体分发方案。本文将介绍如何配置和使用云点播自定义源站回源能力。

## 使用场景

- **源站迁移成本高**：用户的媒体存储在其他第三方云上，其源站内容与第三方平台高度耦合难以做源站的迁移，通过自定义回源可以不迁移源站使用点播 CDN 进行内容加速分发。
- **播放质量要求高**：用户的内容对网络时延和卡顿有较高的要求，使用其他第三方平台难以满足用户需求，通过自定义回源可以保证客户的音视频播放更加流畅，保证业务服务质量。
- **多云共存降低风险**：用户的内容和业务需要多个内容加速渠道来保障业务的可靠性，提高业务容灾能力，可以选择腾讯云点播 CDN 进行音视频加速分发。


## 前提条件

1. [注册](https://www.tencentcloud.com/en/account/register?s_url=https%3A%2F%2Fconsole.tencentcloud.com%2Fvod%2Foverview) 并 [登录](https://www.tencentcloud.com/en/account/login?s_url=https%3A%2F%2Fcloud.tencent.com%2F) 腾讯云账号。
2. 已开通腾讯云点播服务。若未开通，请前往开通 [云点播服务](https://console.cloud.tencent.com/vod/overview)。
3. 前往控制台下 [功能体验](https://console.cloud.tencent.com/vod) 模块，开启**自定义源站回源**功能。


## 支持回源源站类型

- **自有源站**
- **第三方存储对象**

## 实践步骤
### 步骤1：创建自定义域名并配置回源信息

1. 自定义源站回源功能开启后，登录云点播控制台，选择左侧导航栏中**分发播放设置** > [**域名管理**](https://console.cloud.tencent.com/vod/distribute-play/domain)，进入**域名管理**页面。
2. 单击顶部**自定义源站加速域名**，进入**自定有源站加速域名**页面。
![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_496822_PrkPl3xhE0MPoRyl_1673595982?w=1976&h=890)
3. 单击**添加域名**，填写已备案的域名并选择加速区域，具体操作请参见 [点播加速域名](https://www.tencentcloud.com/document/product/266/35572)。
![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_647908_tCYpQPH7cqctptVA_1673596208?w=1401&h=238)
4. 根据用户实际回源需求填写源站配置，目前支持**自有源**和**第三方对象存储**回源方式，具体配置说明如下：     
![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_578401_ojCvcS9fd2MZRMKq_1673597051?w=772&h=377) 
   **自有源站**
若用户希望将稳定运行的业务服务器作为回源源站，借助云点播 CDN 对其上的媒体文件进行加速分发，则请按照以下方式进行源站配置：
<table>
   <tr>
      <th width="0px" style="text-align:center">配置项</td>
      <th width="0px" style="text-align:center">描述</td>
   </tr>
   <tr>
      <td>源站类型</td>
      <td>选择<b>自有源</b></td>
   </tr>
   <tr>
      <td>回源协议</td>
      <td>根据源站支持情况，选择回源请求协议，支持 HTTP、HTTPS 以及协议跟随</td>
   </tr>
	   <tr>
      <td>源站地址</td>
      <td>	支持填入多个 IP 源站（逗号分隔）或一个域名源站</td>
   </tr>
	 <tr>
      <td>回源 HOST</td>
      <td>自有源站可指定回源 HOST，回源 HOST 用于指定 CDN 节点在回源时，在源站访问的站点域名/IP的具体站点<br>若未指定回源 HOST，默认取当前所创建的加速域名</td>
   </tr>
</table>
<dx-alert infotype="explain" title="">
- 源站地址不支持使用云点播默认域名。
- 协议跟随可实现 HTTP 访问使用 HTTP 回源，HTTPS 访问使用 HTTPS 回源（源站需要支持 HTTPS 访问）。
- 支持选择域名作为回源地址，此域名不可与业务加速域名一致。
</dx-alert>
<b>第三方对象存储</b><br>
若用户希望将存储在第三方对象存储的媒体文件借助云点播 CDN 能力进行加速分发，则请按照以下方式进行源站配置：              
<table>
   <tr>
      <th width="0px" style="text-align:center">配置项</td>
      <th width="0px" style="text-align:center">描述</td>
   </tr>
   <tr>
      <td>源站类型</td>
      <td>选择<b>第三方对象存储</b></td>
   </tr>
   <tr>
      <td>第三方对象存储</td>
      <td>目前支持的第三方对象存储有百度云和七牛云</td>
   </tr>
	   <tr>
	<td>回源协议</td>
	  <td>支持 HTTP、HTTPS</td>
   </tr>
	 <tr>
      <td>源站地址</td>
      <td>输入有效的存储桶访问地址作为源站（不可包含 http:// 或 http:// 协议头）</td>
   </tr>
</table>

![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_410171_Bny9OKoDjpKFSj_1_1673596412?w=1053&h=558)<br>
若选择私有访问的第三方对象存储桶作为源站，需填写有效访问 ID 和 key 进行回源鉴权，鉴权通过后即开启私有存储桶访问。<br>
![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_817388_09QNHrxX6X1qmSaH_1673597120?w=694&h=514)

### 步骤2：自定义域名解析

针对已添加的自定义加速域名，您需要在该域名指定的 DNS 服务商配置 CNAME，用户才能通过加速域名访问到您的媒体文件，具体操作请参见 [点播加速域名-域名解析](https://www.tencentcloud.com/document/product/266/42076)。

### 步骤3：自定义源站回源配置结果查看与修改
1. 前往域名管理，进入**自定义源站加速域名**下，选择已创建域名单击**设置**。
![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_238871_hvqcOSzBJNF5-3ar_1673597406?w=1947&h=864)
2. 单击**基础配置**，可查看当前自定义域名的回源配置信息并进行修改。
![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_979899_tzCbGcP83UIMJRhJ_1673597546?w=1929&h=982)

通过以上步骤操作，用户便可完成基于自有源站或者第三方对象存储的回源配置，能够通过云点播 CDN 对自定义源站上的媒体文件进行分发。具体分发流程说明如下：

1. 若用户添加自定义域名（例如：`test.com`）并完成域名解析和配置回源后，当通过浏览器访问该域名下的媒体文件时（例如：`http://www.test.com/test.mp4`），首先会向 Local DNS 发起域名解析请求；
2. 当 Local DNS 解析域名 `test.com` 时，发现已经配置有 CNAME：`www.test.com.cdn.dnsv1.com`，将会解析请求到腾讯 GSLB（Global Server Load Balance，即腾讯自主研发的全局负载均衡系统）；
3. GSLB 会返回最佳的接入节点 IP 列表，Local DNS 获取相应的解析 IP；
4. 用户获取到最佳接入 IP 节点；
5. 用户向最佳接入 IP 节点发起对 `http://www.test.com/test.mp4` 的访问请求；
6. 如果该 CDN 节点上缓存有 test.mp4，用户将获取数据，结束该请求。如果该 CDN 节点没有缓存该资源，此时该节点会向您配置的**业务源站**发起对 test.mp4 的请求，获取资源后，默认会缓存到当前节点中，并将资源返回给用户，此时便结束请求。

>? 用户使用自定义源站回源功能进行加速分发播放媒体文件时会产生**下行流量**费用和**回源源站流量**费用，其中下行流量费用由云点播收取，具体规则请参见 [流量计费](https://www.tencentcloud.com/document/product/266/14666#.E5.8A.A0.E9.80.9F.E6.9C.8D.E5.8A.A1.3Cspan-id.3D.22speed.22.3E.3C.2Fspan.3E) 和 [流量资源包]https://www.tencentcloud.com/document/product/266/52806#2.-.E6.B5.81.E9.87.8F.E8.B5.84.E6.BA.90.E5.8C.85)，回源源站的流量费用由源站收取。