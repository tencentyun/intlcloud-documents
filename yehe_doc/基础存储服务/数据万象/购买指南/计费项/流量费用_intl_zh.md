您在使用数据万象（Cloud Infinite，CI）服务时产生的流量费用由 CI 收取，目前流量费用分为 **CDN 回源流量费用**和**外网出流量费用**两部分，CI 不对入流量收取费用，计费周期为**月**。

>?
>
> - 数据万象服务包括图片处理、媒体处理、内容识别、内容审核、文档处理。
> - 用户访问**带有CI数据处理参数的COS域名**，或**访问CI域名**均属于使用数据万象服务。
> - 数据万象CI是依托对象存储COS的数据处理平台，存储数据与COS打通，可直接调用存储桶中的存量或增量数据进行处理。

<table>
<thead>
<tr>
<th align="left">流量类型</th>
<th align="left">说明</th>
<th align="left">计费周期</th>
<th align="left">适用计费方式 </th>
</tr>
</thead>
<tbody><tr>
<td align="left">入流量 </td>
<td align="left">数据上传到CI所产生的流量</td>
<td align="left" rowspan=3>按月结算</td>
<td align="left" rowspan=3>按量计费</td>
</tr>
<tr>
<td align="left">CDN 回源流量</td>
<td align="left">数据从CI传输到腾讯云CDN边缘节点产生的回源流量</td>
</tr>
<tr>
<td align="left">外网出流量</td>
<td align="left">直接通过CI域名链接访问所产生的流量</td>
</tr>
</tbody></table>



### 用户开启CDN加速后产生的流量

用户访问带有CI数据处理参数的COS域名，或访问CI域名时，如开启CDN加速域名，并使用CDN加速域名进行**数据的下载访问**时，均将产生以下费用：

| 计费项      | 说明                                                         | 如何计费            |
| ----------- | ------------------------------------------------------------ | ------------------- |
| CDN回源流量 | 数据从CI传输到腾讯云CDN边缘节点产生的回源流量                | 按CI计费标准收取    |
| CDN流量     | 数据从CDN边缘节点下载到用户本地或客户端时产生的CDN流出流量   | 按 CDN 计费标准收取 |
| COS请求费用 | 数据从CI传输到腾讯云CDN边缘节点时，由于数据存储在COS中，会产生COS请求次数 | 按 COS计费标准收取  |

**示例：**

A.用户访问带有图片处理参数的COS域名，要求调整图片宽高为原图50%，则产生以下费用:

![图片生成a](https://qcloudimg.tencent-cloud.cn/raw/340a74554f0cbcc330678e54d961cfb6.jpg)



B.用户访问CI域名，如对图片进行缩放操作，调整图片宽高为原图50%，则产生以下费用:

![图片生成a](https://qcloudimg.tencent-cloud.cn/raw/c21e1f8e10f8194ddd1d8e03e8329753.jpg)

说明：

- 相同地域，如通过内网进行下载则流量免费



### 流量费用定价

<table>
<thead>
<tr>
<th align="left">流量类型</th>
<th align="left">地域 </th>
<th align="left">价格</th>
</tr>
</thead>
<tbody><tr>
<td align="left">入流量 </td>
<td align="left">不限</td>
<td align="left">免费</td>
</tr>
<tr>
<td align="left" rowspan=2>CDN 回源流量</td>
<td align="left">中国大陆地域 </td>
<td align="left">0.02美元/GB </td>
</tr>
<tr>
<td align="left">中国香港及境外地域</td>
<td align="left">0.072美元/GB（新加坡地域）<br/>0.1美元/GB（印度地域）<br/>0.08美元/GB（中国香港地域）<br/>0.07美元/GB （欧洲、加拿大、美国、日本、泰国、韩国、印尼、巴西地域）</td>
</tr>
<tr>
<td align="left" rowspan=2>外网出流量</td>
<td align="left">中国大陆地域 </td>
<td align="left">0.1美元/GB</td>
</tr>
<tr>
<td align="left">中国香港及境外地域</td>
<td align="left">0.072美元/GB（新加坡地域）<br/>0.1美元/GB（印度地域）<br/>0.08美元/GB（中国香港地域）<br/>0.07美元/GB（欧洲、加拿大、美国、日本、泰国、韩国、印尼、巴西地域）</td>
</tr>
</tbody></table>
