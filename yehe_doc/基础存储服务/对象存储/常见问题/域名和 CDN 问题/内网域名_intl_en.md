### Does COS have a private network domain?

COS' default origin domain name is in the format of `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com`. By default, public network and intra-region private network access are supported, for example, `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`. For more information on domain name, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).

You can use this domain to access COS over a private network (COS will be resolved to a private IP).

In this case, the following will be generated:
- Private network traffic: Both private network upstream traffic and downstream traffic are free of charge. For more information, see [Traffic Fees](https://intl.cloud.tencent.com/document/product/436/33776).
- Requests: The total number of read requests and write requests are calculated every day according to the number of times a request command is sent, with 10,000 times as the minimum unit. For more information, see [Request Fees](https://intl.cloud.tencent.com/document/product/436/40100).







