### Does COS have a private network domain?

COS’s default origin domain is in the format of `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com`. By default, public network and intra-region private network access are supported. You can use this domain to access COS over a private network (COS will be resolved to a private IP). In this case, traffic generated is private network traffic and will not incur traffic fees.
An example domain is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`. For more information on domains, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).



