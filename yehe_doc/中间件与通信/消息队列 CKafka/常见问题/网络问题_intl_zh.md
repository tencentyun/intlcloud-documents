## CKafka 是否支持公网访问？

CKafka 默认内网传输，如需通过公网访问，需要单独开通一条公网路由，具体操作参考 [添加路由策略](https://intl.cloud.tencent.com/document/product/597/32555)，当前单台 Broker 默认提供3Mbps 免费公网带宽。

CKafka 专业版实例支持升配公网带宽，最高可提升至198Mbps，若您有更高的带宽需求，您可以额外支付费用购买。具体价格请参考 [计费概述](https://intl.cloud.tencent.com/document/product/597/11745)。

由于公网访问会涉及延时、网络环境和安全性等问题，不建议客户长期开启公网传输。

## 公网开启 SASL 之后，VPC 内网如何继续访问？

如果您在开通公网访问路由的同时还使用了 PLAINTEXT 方式接入 CKafka，那么之前为 Topic 设置的 ACL 仍然会生效。若您希望 PLAINTEXT 方式的访问不受影响，请为 PLAINTEXT 需要访问的 Topic 添加全部用户的可读写的权限。

>?在添加 ACL 策略时，不需要选择任何用户，则默认为**全部用户**添加了读写权限。

![img](https://main.qcloudimg.com/raw/8d75061c412c78fef7f3f0c13024ec69.png)

添加完成效果如下：

![img](https://main.qcloudimg.com/raw/eb922f7fe6a3cfe97be6498b05676c5c.png)
