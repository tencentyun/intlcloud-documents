## 简介

将媒体播放链接，盗挂到其他站点播放的行为，称为盗链。盗链不仅威胁版权安全，还会对被盗方造成 CDN 带宽流量的损失。
云点播支持 Referer 防盗链和 Key 防盗链两种形式，防范非法盗链行为。

<table>
   <tr>
      <th style="width:150px">分类</td>
      <th>功能</td>
      <th>说明</td>
   </tr>
   <tr>
      <td rowspan="1"><nobr>Referer 防盗链</td>
      <td>来源页面地址控制</td>
			<td>基于 HTTP 协议支持的 Referer 机制，通过播放请求 Header 中携带的 Referer 字段识别请求的来源。开发者可以设置一批域名为黑名单或白名单，CDN 节点将按照名单中的域名做鉴权，从而允许或拒绝播放请求。</td>
   </tr>
   <tr>
      <td rowspan="3"><nobr>KEY 防盗链</td>
      <td>链接有效时间控制</td>
      <td>在视频 URL 中指定过期时间。如果请求的视频 URL 已过期，则视频无法播放。通过这种方式，可以为视频 URL 设置有效时间，防范他人将视频 URL 转移到其他站点后长期使用。</td>
   </tr>
   <tr>
      <td>链接播放人数控制</td>
      <td>在视频 URL 中指定链接最多能供多少人播放。不在同一内网的播放终端，它们的公网 IP 一般是不同的。通过限制一个 URL 允许最多能被多少公网 IP 播放，就能够限制同一个 URL 可以播放的人数，从而可以防范他人将视频 URL 转移到其他站点后，无限制地分发给任意多的人数观看。</td>
   </tr>
   <tr>
      <td>允许播放时长控制</td>
      <td>在视频 URL 中指定试看时长（如仅允许播放视频的前5分钟）。通过这种方式，可以实现对未付费用户的试看功能。</td>
   </tr>
</table>

## 适用场景
<table ><thead ><tr>
<th style="width:150px" >场景</th><th >说明</th></tr>
</thead><tbody ><tr>
<td>自有视频防盗链</td>
<td>平台高价值自有视频，希望仅在自己的平台站点播放。使用 Referer 和 Key 防盗链可防止他人窃取链接后在其他平台播放。</td>
</tr>
<tr>
<td>UGC 防视频床</td>
<td>UGC 视频平台，可能有恶意用户上传与平台主题无关的视频，然后使用平台链接分发，把平台当做视频床。使用防盗链可以杜绝此类问题，具体方法见 <a href="https://intl.cloud.tencent.com/document/product/266/37545" >链接</a> 。</td>
</tr>
<tr>
<td>非会员试看</td>
<td>付费视频，一般会允许做几分钟的试看。Key 防盗链可实现视频试看功能。</td>
</tr>
</tbody>
</table>


## 使用方式

* 关于 Referer 防盗链，使用方式参考 [链接](https://intl.cloud.tencent.com/document/product/266/33985)。
* 关于 Key 防盗链，使用方式参考 [链接](https://intl.cloud.tencent.com/document/product/266/33986)。
