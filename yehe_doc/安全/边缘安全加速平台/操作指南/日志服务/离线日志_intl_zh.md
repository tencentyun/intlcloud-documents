## 功能介绍
为了方便客户对用户访问进行分析，EdgeOne 对全网访问日志进行了小时粒度打包，默认存储 30 天，并且提供下载服务。


## 操作步骤
1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧菜单栏中，单击**日志服务** > **离线日志**。
2. 在离线日志页面，可选择具体站点或具体子域名的离线日志；同时支持筛选不同时间进行离线日志查询。
![](https://qcloudimg.tencent-cloud.cn/raw/281cfb26b8b14588d501770c5a09ff3a.png)

<dx-alert infotype="notice">
- 访问日志默认按小时打包，若某个小时里域名无任何请求，则不会产生该时间区间的日志包。
- 日志包通过 gzip 压缩为 .gz 格式。由于 MacOS 系统的目录系统缺陷，在MacOS 系统下双击解压可能会报错，如出现这种情况，您可以通过如下 Terminal 命令进行解压。
 ```js.
gunzip {your_file_name}.log.gz 
 ```
- 由于 EdgeOne 节点分布在各地，为同步所有时区，离线日志的存储时间和查询时间默认为：UTC +00:00。
- 离线日志从各 EdgeOne 节点收集而来，因此延迟上各有差异，一般情况下延迟30分钟左右后可查询、下载日志包，日志包会不断追加，一般24小时左右趋于稳定。</dx-alert>


## 字段说明
日志默认按照 json 格式存储，具体的日志字段解释如下。
当某字段无值时：

- 字段的数据类型为 String 且字段没有数据，字段取值为：“-”。
- 字段的数据类型为 Int 且字段没有数据，字段取值为：-1。

### 站点加速日志
<table>
<thead>
<tr>
<th width="15%">名称</th>
<th width="15%">数据类型</th>
<th width="70%">说明</th>
</tr>
</thead>
<tbody><tr>
<td>RequestID</td>
<td>String</td>
<td>客户端请求的唯一标识 ID</td>
</tr>
<tr>
<td>ClientIP</td>
<td>String</td>
<td>客户端 IP</td>
</tr>
<tr>
<td>ClientRegion</td>
<td>Sting</td>
<td>客户端 IP 解析出来的国家/地域。格式标准：<a href="https://www.iso.org/iso-3166-country-codes.html">ISO-3166-2</a></td>
</tr>
<tr>
<td>RequestTime</td>
<td>int</td>
<td>客户端请求时间，时区：UTC +00:00，格式标准：<a href="https://www.iso.org/iso-8601-date-and-time-format.html">ISO-8601</a> </td>
</tr>
<tr>
<td>RequestStatus</td>
<td>int</td>
<td>客户端请求的状态；0：未结束，1: 请求正常结束，2：异常结束</td>
</tr>
<tr>
<td>RequestHost</td>
<td>String</td>
<td>客户端请求的 Host</td>
</tr>
<tr>
<td>RequestBytes</td>
<td>int</td>
<td>客户端请求的大小，单位：Byte</td>
</tr>
<tr>
<td>RequestMethod</td>
<td>String</td>
<td>客户端请求的 HTTP Method</td>
</tr>
<tr>
<td>RequestUrl</td>
<td>String</td>
<td>客户端请求的 URL</td>
</tr>
<tr>
<td>RequestUrlQueryString</td>
<td>String</td>
<td>客户端请求的 URL 携带的查询参数</td>
</tr>
<tr>
<td>RequestUA</td>
<td>String</td>
<td>客户端请求的 User-Agent 信息</td>
</tr>
<tr>
<td>RequestRange</td>
<td>String</td>
<td>客户端请求的 Range 参数信息</td>
</tr>
<tr>
<td>RequestReferer</td>
<td>String</td>
<td>客户端请求的 Referer 信息</td>
</tr>
<tr>
<td>RequestProtocol</td>
<td>String</td>
<td>客户端请求的应用层协议：HTTP/1.0，HTTP/1.1，HTTP/2.0，HTTP/3，WebSocket</td>
</tr>
<tr>
<td>RemotePort</td>
<td>int</td>
<td>TCP 协议下客户端与节点建立连接的端口，若无则为 -</td>
</tr>
<tr>
<td>EdgeCacheStatus</td>
<td>String</td>
<td>客户端请求是否命中节点缓存：HIT（资源由节点缓存提供），MISS（资源可缓存，但由源站提供），Dynamic（资源不可缓存）</td>
</tr>
<tr>
<td>EdgeResponseStatusCode</td>
<td>int</td>
<td>节点响应返回给客户端的状态码</td>
</tr>
<tr>
<td>EdgeResponseBytes</td>
<td>int</td>
<td>节点响应返回给客户端的大小，单位：Byte</td>
</tr>
<tr>
<td>EdgeResponseTime</td>
<td>int</td>
<td>从 EdgeOne 接收到客户端发起的请求开始，到客户端接收到服务器端的响应结束，这个过程所耗费的时间；单位：ms</td>
</tr>
<tr>
<td>EdgeInternalTime</td>
<td>int</td>
<td>从 EdgeOne 向源站发起请求到收到源站返回第一个响应字节的耗时；单位：ms</td>
</tr>
<tr>
<td>EdgeServerIP</td>
<td>String</td>
<td>DNS 解析 Host 得到的 EdgeOne 服务器 IP 地址</td>
</tr>
<tr>
<td>EdgeServerID</td>
<td>String</td>
<td>客户端访问到的 EdgeOne 服务器唯一标识</td>
</tr>
<tr>
<td>SecurityAction</td>
<td>String</td>
<td>命中安全规则后的处置方式；取值：Monitor（观察），JSChallenge（JavaScript 挑战），Deny（ 拦截）， Allow（放行），BlockIP（IP 封禁），   Redirect（重定向），ReturnCustomPage（返回自定义页面），    ManagedChallenge（托管挑战）</td>
</tr>
<tr>
<td>SecurityRuleID</td>
<td>String</td>
<td>处置请求的安全规则 ID</td>
</tr>
<tr>
<td>SecurityUserNote</td>
<td>String</td>
<td>用户自定义的标签</td>
</tr>
<tr>
<td>SecurityModule</td>
<td>String</td>
<td>命中安全规则的所对应的安全功能；取值： CustomRule（自定义规则），BotManagement（Bot管理），RateLimiting（速率限制模板），RateLimitingCustomRule（速率限制规则），ManagedRule（托管规则），BotClientReputation（客户端画像），BotBehaviorAnalysis（Bot智能防护），RateLimitingClientFiltering（智能客户端过滤）</td>
</tr>
</tbody></table>


### 四层代理日志
<table>
<thead>
<tr>
<th width="15%">名称</th>
<th width="15%">数据类型</th>
<th width="70%">说明</th>
</tr>
</thead>
<tbody><tr>
<td>ServiceID</td>
<td>String</td>
<td>四层代理服务唯一标识 ID</td>
</tr>
<tr>
<td>ConnectTimeStamp</td>
<td>String</td>
<td>建连时间；使用 <a href="https://www.iso.org/iso-8601-date-and-time-format.html">ISO-8601</a> 规范，默认UTC +0 时区</td>
</tr>
<tr>
<td>DisconnetTimeStamp</td>
<td>String</td>
<td>断连时间；使用 <a href="https://www.iso.org/iso-8601-date-and-time-format.html">ISO-8601</a>  规范，默认UTC +0 时区</td>
</tr>
<tr>
<td>DisconnetReason</td>
<td>String</td>
<td>断连原因；<li>格式为 「方向：原因」</li><li>方向取值：up（源站方向）/down（客户端方向）</li><li>原因：</li><ul><ul><li>net_exception_peer_error：读写对端返回错误</li><li>net_exception_peer_close：对端已关闭连接</li><li>create_peer_channel_exception：创建到下一跳的 channel 失败</li><li>channel_eof_exception：channel 已结束（请求结束时，结束请求的节点会给相邻节点发送 channel_eof 告知相邻节点请求已结束）</li><li>net_exception_closed：连接已关闭</li><li>net_exception_timeout：读写超时</li></ul></ul></td>
</tr>
<tr>
<td>ClientRealIP</td>
<td>String</td>
<td>客户端真实 IP</td>
</tr>
<tr>
<td>ClientRegion</td>
<td>String</td>
<td>客户端所在国家/地域2位字母编码，符合 <a href="https://www.iso.org/iso-3166-country-codes.html">ISO-3166-2</a> 规范</td>
</tr>
<tr>
<td>EdgeIP</td>
<td>String</td>
<td>访问的 EdgeOne 服务器 IP 地址</td>
</tr>
<tr>
<td>ForwardProtocol</td>
<td>String</td>
<td>客户配置的转发协议 TCP/UDP</td>
</tr>
<tr>
<td>ForwardPort</td>
<td>Int</td>
<td>客户配置的转发端口</td>
</tr>
<tr>
<td>SentBytes</td>
<td>Int</td>
<td>本条日志持续期间产生的入流量，单位：Byte</td>
</tr>
<tr>
<td>ReceivedBytes</td>
<td>Int</td>
<td>本条日志持续期间产生的出流量，单位：Byte</td>
</tr>
<tr>
<td>LogTimeStamp</td>
<td>Int or String</td>
<td>日志生成时间；使用 <a href="https://www.iso.org/iso-8601-date-and-time-format.html">ISO-8601</a> 规范，默认UTC +0 时区</td>
</tr>
</tbody></table>

## 特别说明
- 通过站点加速访问日志 EdgeResponseBytes 字段中记录的字节数，统计计算而来的流量、带宽数据与 EdgeOne 计费流量或带宽数据可能不一致。原因如下：
   - 访问日志中仅可记录应用层数据，在实际网络传输中，产生的网络流量要比纯应用层流量多5% - 15%。由两部分组成：
     - TCP/IP 包头消耗，基于 TCP/IP 协议的 HTTP 请求，每一个包的大小最大是1500个字节，包含了 TCP 和 IP 协议的40-60个字节的包头，包头部分会产生流量，但是无法被应用层统计到，这部分的开销大致为3-4%左右。
     - TCP 重传，正常网络传输过程中，发送的网络包会有3% - 10%左右会被互联网丢掉，丢掉后服务器会对丢弃的部分进行重传，此部分流量应用层也无法统计，占比约为3% - 7%。
- 开启智能加速后，腾讯云 EdgeOne 会对客户端请求 EdgeOne 节点所产生的流量/带宽计费。详情请参见 [计费概述](https://www.tencentcloud.com/document/product/1145/48705)。
