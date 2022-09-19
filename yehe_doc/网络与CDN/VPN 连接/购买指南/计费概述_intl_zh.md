本文列出 IPSec VPN 和 SSL VPN 计费项说明和定价。
>?本文表格中罗列的价格信息仅供参考，如果购买页面显示的价格信息与文档表格中的价格信息不一致，请以购买页面为准。
>

## 计费说明
![](https://qcloudimg.tencent-cloud.cn/raw/5446aa22b46d4f04476d96aa93222129.jpg)
<table>
<tr>
<th>类型</th>
<th>计费项</th>
<th>计费模式</th>
</tr>
<tr>
<td>IPSec VPN </td>
<td>VPN 网关</td>
<td>按量计费模式，详情请参见 <a href="#IPSecdingjia">IPSec VPN 定价</a>。</td>
</tr>
<tr>
<td>SSL VPN </td>
<td>VPN 网关、SSL 连接 </td>
<td>按量计费模式，详情请参见 <a href="#dingjia">SSL VPN 定价</a>。</td>
</tr>
<tr>
<td colspan="2">公网流量费</td>
<td>流量费用请参见 <a href="https://intl.cloud.tencent.com/document/product/213/10578">公网网络-按流量计费</a>。</td>
</tr>
<table>



## IPSec VPN 定价[](id:IPSecdingjia)
>? VPN 通道、对端网关供用户**免费**使用。
>

### VPN 网关费用
VPN 网关是您在腾讯云上的网关对象，经过 VPN 网关的流量收取费用，支持按流量计费。
>?本处流量指出 VPN 网关的流量，即从 VPN 网关实例流出的流量，也叫下行流量。

### 按流量计费
按流量计费为后付费模式，包含两部分费用：访问公网产生的**流量费用**和**网关费用**（按小时计算，不满1小时按1小时计算）。
- 流量费用请参见 [公网网络-按流量计费](https://intl.cloud.tencent.com/document/product/213/10578)。
- 网关费用请参见下表：
<table>
<thead>
<tr>
<td width="12%">网关规格</td>
<td width="18%">北京、上海、广州、成都、重庆、南京</td>
<td width="18%">硅谷、法兰克福、首尔、孟买、弗吉尼亚、莫斯科、东京、中国台北、中国香港</td>
<td width="18%">多伦多、新加坡、曼谷</td>
</tr>
</thead>
<tbody><tr>
	<td >5Mbps/10Mbps/20Mbps/</br>50Mbps/100Mbps</td>
<td>0.074 USD /小时</td>
<td>0.089 USD /小时 </td>
<td>0.12 USD /小时</td>
</tr>
<tr>
<td>200Mbps/500Mbps/1000Mbps</td>
<td>0.44 USD /小时 </td>
<td>0.60 USD/小时</td>
<td>0.75 USD/小时</td>
</tr>
</tbody></table>

>?200MB、500MB和1000MB带宽目前暂不支持多伦多，上述表中其他地域如需使用请 [工单申请](https://console.cloud.tencent.com/workorder/category)。


#### 计费示例
假如某用户在北京地域购买了规格为50Mbps的 VPN 网关，计费方式为按流量计费。在07:00:00 - 07:59:59时间段，假设该用户使用流量共计5GB，则该用户在08:00:00时刻需支付费用如下：
+ 流量费用：北京地域流量单价为0.12 USD /GB，流量费用 = 流量单价 × 使用流量 = 0.12 USD /GB × 5GB = 0.6 USD
+ 网关费用：北京地域50Mbps规格的 VPN 网关费用单价为0.074 USD /小时，网关费用 = 网关费用单价 × 时长 = 0.074 USD /小时 × 1小时 = 0.074 USD

总价 = 流量费用 + 网关费用 = 0.6 USD + 0.074 USD = 0.674 USD


## SSL VPN 定价[](id:dingjia)
>? SSL 服务端、SSL 客户端供用户**免费**使用。
>
SSL VPN 按流量计费为后付费模式，包括三部分费用： 访问公网产生的**流量费用**、**网关费用**（按小时计算，不满1小时按1小时计算）和 **SSL 连接费用**（按小时计算，不满1小时按1小时计算）。
- 流量费用请参见 [公网网络-按流量计费](https://intl.cloud.tencent.com/document/product/213/10578)。
- 网关费用请参见下表：
<table>
<thead>
<tr>
<th width="12%">网关规格</th>
<th width="18%">北京、上海、广州、成都、重庆、南京</th>
<th width="18%">硅谷、法兰克福、首尔、孟买、弗吉尼亚、多伦多、曼谷、新加坡、莫斯科、东京、中国台北、中国香港</th>
</tr>
</thead>
<tbody><tr >
	<td >5Mbps/10Mbps/20Mbps/</br>50Mbps/100Mbps</td>
<td>0.074 USD /小时</td>
<td>0.12 USD /小时</td>
</tr>
</tbody></table>

- SSL 连接费用请参见下表：
<table>
<tr>
<th>连接数（个） </th>
<th>价格 （美元/小时）</th>
</tr>
<tr>
<td>(0,10]</td>
<td>0.003</td>
</tr>
<tr>
<td> (10,100]</td>
<td>0.002 </td>
</tr>
</table>



#### 计费示例
假如某用户在北京地域购买了规格为50Mbps、5条 SSL 连接的 VPN 网关，计费方式为按流量计费。在07:00:00 - 07:59:59时间段，假设该用户使用流量共计5GB，则该用户在08:00:00时刻需支付费用如下：
+ 流量费用：北京地域流量单价为0.12 USD /GB，流量费用 = 流量单价 × 使用流量 = 0.12 USD /GB × 5GB = 0.6 USD
+ 网关费用：北京地域50Mbps规格的 VPN 网关费用单价为0.074 USD /小时，网关费用 = 网关费用单价 × 时长 = 0.074 USD /小时 × 1小时 = 0.074 USD
+ SSL 连接费用：北京地域SSL连接的单价为0.003美元/个/小时，SSL 连接费用 = SSL 连接单价 × SSL 连接数 × 时长 = 0.003美元/个/小时 × 5 个 × 1小时 = 0.015USD

总价 = 流量费用 + 网关费用 + SSL 连接费用= 0.6 USD + 0.074 USD +0.015USD= 0.689USD
