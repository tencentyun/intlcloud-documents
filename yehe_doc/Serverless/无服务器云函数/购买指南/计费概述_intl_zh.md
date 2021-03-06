
## 免费额度

开通了云函数服务的用户，每月可享受一定量的免费资源使用量及免费调用次数，外网出流量无免费额度。如下表所示：

| 计费项 |  每月免费额度 |
| ------------| -------------- |
| 资源使用量 | 40万GBs  |
| 调用次数    | 100万次   |

详情请参阅 [免费额度说明](https://intl.cloud.tencent.com/document/product/583/12282)。

## 计费方式及计费项

云函数按照实际使用付费，采用后付费模式，按**小时**进行结算，以**美元**为单位结算。

云函数的费用由4部分组成，每部分根据自身统计结果和计算方式进行费用计算，结果以**美元**为单位，并保留小数点后两位：

 - **资源使用费用**：由函数配置内存，乘以函数运行时长得出资源使用量，单位为 GBs。
 - **调用次数费用**：函数的每次触发执行均记为一次调用，单位为次。
 - **外网出流量费用**：在函数代码中访问外网时产生的出流量记录为外网出流量，单位为 GB。
 - **预置并发闲置费用**：由已启动的预置实例数，减去实际运行的并发数得到闲置实例数，闲置实例数乘以配置内存，再乘以闲置时长得出闲置资源量，单位为GBs。

详情请参阅 [计费方式说明](https://intl.cloud.tencent.com/document/product/583/12284)。

## 产品定价

针对组成云函数费用的4部分，定价如下：

 - **资源使用费用**：0.0000167 美元/GBs
 - **调用次数费用**：0.002 美元/万次
 - **外网出流量费用**：各地域均有不同定价，中国大陆 0.12 美元/GB
 - **预置并发闲置费用**：0.00000847 美元/GBs

详情请参阅 [产品定价说明](https://intl.cloud.tencent.com/document/product/583/12281)。

## 支持地域
下表为云函数目前所支持的地域信息：
<table>
<tr>
<th width="50%">地域</th><th width="50%">取值</th>
</tr>
<tr>
<td>华南地区（广州）</td><td>ap-guangzhou</td>
</tr>
<tr>
<td>华东地区（上海）</td><td>ap-shanghai</td>
</tr>
<tr>
<td>华北地区（北京）</td><td>ap-beijing</td>
</tr>
<tr>
<td>西南地区（成都）</td><td>ap-chengdu</td>
</tr>
<tr>
<td>港澳台地区（中国香港）</td><td>ap-hongkong</td>
</tr>
<tr>
<td>亚太南部（孟买）</td><td>ap-mumbai</td>
</tr>
<tr>
<td>亚太东南（新加坡）</td><td>ap-singapore</td>
</tr>
<tr>
<td>亚太东北（东京）</td><td>ap-tokyo</td>
</tr>
<tr>
<td>北美地区（多伦多）</td><td>na-toronto</td>
</tr>
<tr>
<td>美国西部（硅谷）</td><td>na-siliconvalley</td>
</tr>
</table>



## 计费详情

具体的计费详情，请参考以下文档：

<table>
<thead>
<tr>
<th width="50%">文档名称</th>
<th width="50%">文档链接</th>
</tr>
</thead>
<tbody><tr>
<td>免费额度</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12282" target="_blank">查看文档</a></td>
</tr>
<tr>
<td>计费方式</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12284" target="_blank">查看文档</a></td>
</tr>
<tr>
<td>产品定价</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12281" target="_blank">查看文档</a></td>
</tr>
<tr>
<td>欠费说明</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12283" target="_blank">查看文档</a></td>
</tr>
<tr>
<td>计费示例</td>
<td><a href="https://intl.cloud.tencent.com/document/product/583/12285" target="_blank">查看文档</a></td>
</tr>
</tbody></table>
