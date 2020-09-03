## 收费模式相关

### COS 支持哪种计费方式？

对象存储 COS 支持按量计费（后付费）方式，详情请参见 [计费概述](https://intl.cloud.tencent.com/document/product/436/16871)。


### COS 有哪些收费项？

COS 的费用由五部分组成：存储费用、请求费用、数据取回费用、流量费用和管理功能费用。关于 COS 计费项的详细介绍请参见 [计费项](https://intl.cloud.tencent.com/document/product/436/33776)。有关对象存储 COS 的定价信息，请参见 [产品定价](https://intl.cloud.tencent.com/document/product/436/6239)。 


## 免费额度相关

### COS 有免费额度吗？

COS 面向所有新用户（即首次开通 COS 服务的个人和企业用户）提供一定量的免费额度，可用于抵扣标准存储类型的数据产生的标准存储容量费用，详情请参见 [免费额度](https://intl.cloud.tencent.com/document/product/436/6240)。

### 享受免费额度为何仍会欠费（扣费）？

已享受免费额度仍然欠费（或扣费），可能原因如下：

1. 其他收费项：COS 的费用包括存储容量费用、请求费用、数据取回费用、流量费用和管理功能费用，目前 COS 免费额度只提供一定额度的标准存储容量，只能抵扣标准存储类型的存储费用。其他的计费项：如请求费用、数据取回费用、流量费用和管理功能费用，按量计费收取。
2. 超出额度的资源使用费用。例如，您享受50GB的免费标准存储容量，但是实际存储量超出了免费额度50GB，则超出部分将按量计费。
3. 免费额度过期，COS 为首次使用的用户提供6个月有效期的标准存储容量免费额度。免费额度过期后，存储费用将按量计费。您可以登录对象存储控制台，进入 [资源包管理](https://console.cloud.tencent.com/cos5/package) 页面查看免费额度有效期。


## 流量相关

### COS 的外网下行流量如何收费？

外网下行流量是数据通过互联网从 COS 传输到客户端产生的流量。用户直接通过**对象链接**下载对象或通过**静态网站源站**浏览对象产生的流量属于外网下行流量，对应费用为外网下行流量费用。外网下行流量计费详细信息请参见 [计费项](https://intl.cloud.tencent.com/document/product/436/33776) 和 [产品定价](https://intl.cloud.tencent.com/document/product/436/6239)。

### 开启 CDN 加速后为什么会产生外网下行流量？

开启 CDN 加速后，如果您仍使用 COS 的源站域名（格式如`<BucketName-APPID>.cos.<region>.myqcloud.com`）访问 COS 上的文件，则依然会产生外网下行流量费用。COS 建议您使用 CDN 加速域名访问文件，这样将仅产生 CDN 回源流量。

### COS 的 CDN 回源流量如何收费？

CDN 回源流量是数据从 COS 传输到腾讯云 CDN 边缘节点产生的流量。用户开启 CDN 加速后，通过**腾讯云 CDN 加速域名**从客户端浏览或下载 COS 的数据产生的流量为 CDN 回源流量，对应费用为 CDN 回源流量费用。COS 的 CDN 回源流量计费详细信息请参见 [计费概述](https://intl.cloud.tencent.com/document/product/436/16871) 和 [产品定价](https://intl.cloud.tencent.com/document/product/436/6239)。


### COS 与 CVM 之间传输数据，请求数和流量是否收费？

同地域的 COS 与 CVM 之间传输数据，属于内网传输，流量免费使用。关于内网访问的判断，请参见 [内网访问判断方法](https://intl.cloud.tencent.com/document/product/436/30613)。不同地域的 COS 与 CVM 之间传输数据，流量将收取费用。

COS 与 CVM 之间传输数据产生的请求次数，不区分地域和内外网，都会计费。


### 上传文件到 COS 存储桶是否会产生流量费用？

不会。用户上传文件时产生的上行流量不收取费用。


### 同地域内腾讯云产品之间相互访问会产生流量费用吗？

在相同地域内，腾讯云产品之间访问，将会自动使用内网连接，不产生流量费用。详情请参见 [内网访问判断方法](https://intl.cloud.tencent.com/document/product/436/30613)。

## 账单相关

### 如何查看账单？

您可以通过控制台费用中心查看您的账户使用对象存储服务所产生的费用信息。详细查询方式请参见 [查看消费明细](https://intl.cloud.tencent.com/document/product/436/31631)。

## 欠费停服相关


### 欠费停服后，COS 控制台能否访问文件及下载文件？

欠费停服后，COS 数据将无法读写，控制台仅提供充值操作。如需了解更多请参见 [欠费说明](https://intl.cloud.tencent.com/document/product/436/10044)。