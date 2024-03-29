文件传输（上传/下载）场景通过文件上传/下载，获取应用的数据资源的传输速率，反映真实的带宽的波动性。本文将为您介绍如何新建传输任务。

## 操作步骤

1. 登录 [云拨测控制台](https://console.cloud.tencent.com/cat/probe/tasklist)。
2. 在左侧菜单栏中单击**任务列表**。
3. 单击任务列表页面上方的**新建任务**。
4. 根据下列说明配置基本信息。
<table>
<tr>
<th> 配置项</th>
<th> 说明</th>
</tr>
<tr>
<td> 拨测类型</td>
<td> 选择“自定义拨测”</td>
</tr>
<tr>
<td> 任务类型</td>
<td> 选择 PC 端或移动端的“文件传输（上传/下载）”任务类型。</td>
</tr>
<tr>
<td> 拨测地址</td>
<td> 请填写需要拨测的 Web 应用地址（以 <code>http://</code> 或 <code>https://</code> 开头）<br>例如：<br>1. 域名:http://www.tencent.com<br/>2.
域名端口：http://www.tencent.com:80<br/>备注：Ping 监测下使用 TCP 或 UDP 协议时，需要填写端口。
</td>
</tr>
<tr>
<td> 拨测任务名称</td>
<td> 自定义拨测任务名称。</td>
</tr>
<tr>
<td> 拨测频率</td>
<td> 支持1分钟、5分钟、10分钟、15分钟、30分钟、60分钟、120分钟的拨测频率。例如选择5分钟频率，表示每个拨测点每5分钟拨测一次。</td>
</tr>
</table>
5. 根据下列说明配置拨测点。
  1. 选择方式：选择推荐拨测点组或自定义拨测点组（推荐的拨测节点为常用的节点）。
  2. 选择拨测点：
	- 可用性拨测点组：仅支持网络质量、端口性能任务类型，适用于网络质量监控、接口可用性监控、劫持和封堵检测。
	- 高级场景拨测点组：页面用户体验监控、直播卡顿监控、弱网环境可用性探测、CDN 选型与路径优化。覆盖境内外的 IDC、PC 终端、移动端探测点。
     - 推荐拨测点组：为您推荐常用拨测点组。
     - 自定义拨测点组：**选择拨测点地域** > **选择拨测点类型** > 在右侧框中勾选拨测点。拨测点类型说明如下：
<table>
<tr>
	<th> 拨测点类型</th>
	<th> 说明</th>
</tr>
<tr>
<td> 机房（IDC）</td>
<td> 部署在 PC 电脑上的拨测点，代表 PC 用户体验。</td>
</tr>
<tr>
<td> 网民（LastMile）</td>
<td> 部署在终端用户 PC 电脑上的拨测点，代表终端 PC 用户体验。</td>
</tr>
<tr>
<td> 手机端</td>
<td> 部署在终端移动手机上的拨测点，代表终端移动用户。</td>
</tr>
</table>
 - 我的拨测点组：您可以在“高级场景拨测点”中选择常用的拨测点组，并单击右下角的**新建拨测点组**即可。下次创建任务时，直接选择我的拨测点组，即可快速选择您创建的常用拨测点。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ZGrZ150_23intl_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.png)
<dx-alert infotype="explain" title="选择建议">
由于机房（IDC）和网民（LastMile）网络环境不同，机房（IDC）比网民（LastMile）更稳定。
- 若是要监测业务的可用性，可以选择比较稳定的机房 IDC。
- 若要看终端用户的访问体验、网络情况等建议多选网民 LastMile 或移动端，可以模拟终端用户访问应用的体验。
</dx-alert>
6. 配置拨测参数（可选），配置说明如下：
**文件上传：**
<table>
<thread>
<tr>
<th> 配置项</th>
<th> 说明</th>
<th> 默认取值</th>
</tr>
<tr>
<td> IP 类型</td>
<td> 支持自动、IPV4、IPV6 三种 IP 协议类型</td>
<td> 自动</td>
</tr>
<tr>
<td> 上传方式</td>
<td> 可选 POST 或 PUT 两种上传方式</td>
<td> POST</td>
</tr>
<tr>
<td> 指定文件URL</td>
<td> 可选配置，若不填写则由拨测点自动生成上传测试文件</td>
<td> -</td>
</tr>
<tr>
<td> 文件 MD5</td>
<td> 可选配置，若不填写则由拨测点自动生成上传测试文件</td>
<td> -</td>
</tr>
<tr>
<td> 传输大小</td>
<td> 定义上传文件大小，传输大小须大于 0KB 且小于等于 51200KB</td>
<td> 1024KB</td>
</tr>
<tr>
<td> 自定义 Host</td>
<td> 支持按 IP 地址轮询或随机监测，多个 IP 请用半角逗号分隔符，<br>例如：<ul style = "margin-bottom: 0px;">
<li>IPv4：<code>192.168.2.1,192.168.2.5:img.a.com&#124;192.168.2.1?]:img.a.com&#124;</code></li><li>IPv6：<code>[0:0:0:0:0:0:0:1][8080],[0:0:0:0:0:0:0:2][8081]:www.a.com|]</code></li></ul></td>
<td>-</td>
</tr>
</table>

   <b>文件下载：</b>
<table>
<tr>
<th> 配置项</th>
<th> 说明</th>
<th> 默认取值</th>
</tr>
<tr>
<td> IP 类型</td>
<td> 支持自动、IPV4、IPV6 三种 IP 协议类型</td>
<td> 自动</td>
</tr>
<tr>
<td> 传输大小（KB）</td>
<td> 定义下载文件大小，下载文件大小必须大于 0KB 且小于等于 51200KB</td>
<td> 1024KB</td>
</tr>
<tr>
<td> 自定义 Host</td>
<td> 支持按 IP 地址轮询或随机监测，多个 IP 请用半角逗号分隔符，<br>例如：<ul style = "margin-bottom: 0px;"><li>IPv4：<code>192.168.2.1,192.168.2.5:img.a.com&#124;192.168.2.1?]:img.a.com&#124;</code></li><li>IPv6：<code>[0:0:0:0:0:0:0:1][8080],[0:0:0:0:0:0:0:2][8081]:www.a.com|]</code></li></ul>
</td>
<td> -</td>
</tr>
<tr>
<td>DNS 劫持白名单</td>
<td> 当任务的目标 IP 在 DNS 白名单内，则认定为没有发生了 DNS 劫持，详情请参见 <a href="https://www.tencentcloud.com/document/product/1169/52000">劫持监测参数说明</a>。</td>
<td> -</td>
</tr>
<tr>
<td>DNS 劫持黑名单</td>
<td>  当任务的目标 IP 在 DNS 黑名单内，则认定为发生了 DNS 劫持，详情请参见 <a href="https://www.tencentcloud.com/document/product/1169/52000">劫持监测参数说明</a>。</td>
<td> -</td>
</tr>
</table>
