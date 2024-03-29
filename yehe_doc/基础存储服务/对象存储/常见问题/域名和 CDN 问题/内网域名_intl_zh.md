### COS 是否有内网域名？

对象存储（Cloud Object Storage，COS）的默认源站域名格式为：&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com，默认已支持公网访问和同地域的内网访问。例如`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`，更多域名相关介绍，请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224)。

您在内网环境下通过该域名访问 COS 时，COS 会智能解析到内网 IP 上。

此时会产生：
- 内网流量：内网上行流量、内网下行流量均免费。详情请参见 [流量费用说明](https://intl.cloud.tencent.com/document/product/436/33776)。
- 请求：按发送请求指令的次数进行计算，以万次为最小计数单位，每日统计读请求、写请求的总请求次数。详情请参见 [读写请求费用说明](https://intl.cloud.tencent.com/document/product/436/40100)。







