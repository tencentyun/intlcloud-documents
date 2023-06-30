本文介绍不同计费模式的公网网络价格，您可以按需选择合适的计费模式。
>?本文介绍常规 BGP IP 的公网网络费用。精品 BGP IP和加速 IP 目前仅支持按共享带宽包计费，请参见 [共享带宽包](#bwp)。
>
## [按流量](id:by-traffic)
根据使用的公网流量计费，付费模式为后付费，每小时结算一次。适用于业务流量峰值在不同时间段波动较大的场景。
**计费价格**
<table>
<thead>
<tr>
<th rowspan="2" width="65%">地域</th>
<th colspan="2" style="text-align:center;">价格（单位：美元/GB）</th>
</tr>
</thead>
<tbody><tr>
<td>中国大陆地区（不含港澳台地区）、中国香港、雅加达、首尔</td>
<td>0.12</td>
</tr>
<tr>
<td>东京</td>
<td>0.13</td>
</tr>
<tr>
<td>新加坡</td>
<td>0.081</td>
</tr>
<tr>
<td>圣保罗</td>
<td>0.15 </td>
</tr>
<tr>
<td>法兰克福、硅谷、多伦多</td>
<td>0.077</td>
</tr>
<tr>
<td>孟买、曼谷</td>
<td>0.1</td>
</tr>
<tr>
<td>弗吉尼亚</td>
<td>0.075</td>
</tr>
</tbody></table>



**计费示例**
假设您购买了广州地域的 EIP，选择按流量计费模式。该用户在07:00:00 - 07:59:59内共计使用流量10GB，则08:00:00时刻产生的费用为：0.12美元/GB × 10GB = 1.2美元

> ?
> - 流量的单位换算进制为1024，即：1TB = 1024GB，1GB = 1024MB。
> - 公网流量是根据下行字节数（即出方向流量字节数）统计而来的流量数据。在实际网络传输中，产生的网络流量要比纯应用层流量多5% - 15%，故腾讯云统计的流量可能会比用户在服务器自行统计的流量多10%左右。
>  - TCP/IP 包头消耗：基于 TCP/IP 协议的 HTTP 请求，每一个包的大小最大是1500个字节，包含了 TCP 和 IP 协议的40个字节的包头，包头部分会产生流量，但是无法被应用层统计到，这部分的开销大致为3%左右。
>  - TCP 重传：正常网络传输过程中，发送的网络包会有3% - 10%左右会被互联网丢掉，丢掉后服务器会对丢弃的部分进行重传，此部分流量应用层也无法统计，占比约为3% - 7%。
> 


## [共享带宽包](id:bwp)
共享带宽包是一种多 IP 聚合的计费模式，当业务中的公网流量高峰分布在不同时间段内时，可通过共享带宽包实现带宽聚合计费，大幅降低公网费用。
不同 IP 线路类型对应不同的共享带宽包类型及费用，如下表所示。
<table>
<thead>
<tr>
<th>IP 线路类型</th>
<th>共享带宽包类型</th>
</tr>
</thead>
<tbody><tr>
<td>常规 BGP IP</td>
<td><a href="https://intl.cloud.tencent.com/document/product/684/15254">常规 BGP 带宽包</a></td>
</tr>
<tr>
<td>精品 BGP IP</td>
<td><a href="https://intl.cloud.tencent.com/document/product/684/15254">精品 BGP 带宽包</a></td>
</tr>
<tr>
<td>加速 IP</td>
<td><a href="https://intl.cloud.tencent.com/document/product/684/15254">Anycast 加速 BGP 带宽包</a></td>
</tr>
</tbody></table>

## 相关文档
- [CVM 带宽上限](https://intl.cloud.tencent.com/document/product/213/12523)
