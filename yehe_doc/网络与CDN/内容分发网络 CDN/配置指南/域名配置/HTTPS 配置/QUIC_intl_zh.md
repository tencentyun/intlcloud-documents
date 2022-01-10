公告：

腾讯云内容分发网络 CDN 将于2022年1月5日正式发布 QUIC 访问功能。
当您启用 QUIC 访问功能后， 产生的 QUIC 请求数将按量后付费，详细说明请见 [计费说明- QUIC 访问请求数计费](https://intl.cloud.tencent.com/zh/document/product/228/2949)。
进行线上计费时，我们会提前推送消息以及在控制台和文档发布公告周知，请您关注确认。

## 功能介绍

QUIC (Quick UDP Internet Connections) 是一个通用的网络协议，能够保障网络安全性，同时减少传输和连接时的延时，避免网络拥塞。您可开启 QUIC 协议，保障客户端访问 CDN 节点时数据传输的安全性，提升访问效率。

当前默认支持 h3 Draft 28, h3-Q050, h3-Q046, h3-Q043, Q046, Q043 版本。

## 操作指引

1、开启QUIC：

成功添加域名后，可进入域名管理，切换 Tab 至【HTTPS 配置】，即可找到【QUIC】配置：默认为关闭状态，您可自助开启。
**注：**开启前请先配置 HTTPS 证书。
![img](https://tva1.sinaimg.cn/large/008i3skNgy1gy2n1viwjjj30pf034t8t.jpg)

> 注意：
>
> - 业务类型切换涉及资源平台调度，接入 QUIC 平台后，建议您不要再切换域名的业务类型。
> - 当前不支持 QUIC 回源。
> - 部分平台暂不支持QUIC，平台升级中，敬请期待。

**配置约束：**

- 流媒体点播加速业务类型的域名暂不支持 QUIC。
- 开启IPv6访问后不可开启 QUIC。

2、关闭QUIC：

进入控制台域名管理-HTTPS配置-QUIC，即可关闭QUIC功能。

## 计费规则

QUIC 访问属于增值服务，按 QUIC 请求数次数计费，按量后付费，详情见 [计费说明](https://intl.cloud.tencent.com/zh/document/product/228/2949) 。