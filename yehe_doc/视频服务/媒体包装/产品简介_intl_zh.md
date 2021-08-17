## 概述

腾讯云StreamPackage是腾讯云新发布的的高质量视频封装及源站平台。致力于为全球用户提供专业、稳定、安全的视频封装及交付服务。StreamPackage依托腾讯云全球部署的众多可用区的计算资源，结合腾讯自研应用深耕多年的音视频技术降低视频包装分发难度，增加源弹性（origin resiliency），允许视频供应商能够大规模安全稳定地分配视频流媒体。同时，它还保证了7 * 24小时的可用性。

![img](https://main.qcloudimg.com/raw/4a892b3997e8b86ff17ca6fe26f223ba.png)

## 功能

**多协议主备流输入**

StreamPackage支持HLS、DASH两种协议的流输入模式，同时针对每一个Channel生成主备流输入地址（双通道配置），支持两个主备流input同时推流，从而稳定、可靠地保护您的视频资产。

**灵活稳定容灾机制**

Channel主备通道同时输入时，当主input出现网络不稳等异常推流情况，而备input推流正常时，可以无缝切换到备input输出。切换时间等参数支持自定义配置。

**高安全性保护**

StreamPackage从输入到输出支持多种安全鉴权模式，输入支持http-authentication 模式，可以根据username和password进行推流校验。输出支持配置IP黑白名单，支持配置Authkey，支持http-header通过 X-TENCENT-PACKAGE进行鉴权，支持CIDR级别的防护策略。

**一键对接CDN分发**

StreamPackage支持一键配置直播CDN，添加自有播放域名进行分发，全球遍布的边缘节点保证您视频的分发稳定性及分发效率。

**高可用缓存保护机制**

StreamPackage提供多级缓存保护机制，当一个节点服务器异常，内置监控提供自动剔除节点机制，保障区域资源的高可靠性。同时推流支持主备流input模式，主备流input提供无缝切换机制，保证用户的推流高稳定可用性。

**架构及故障切换**

StreamPackage支持双通道配置，pipeline A与pipeline B可同时输入直播流；StreamPackage支持故障自动切换，当StreamPackage的主通道（pipeline A）检测到直播流中断一定时间后（可通过Max segment duration进行设置），会自动切换到备用通道（pipeline B）进行输出。

StreamPackage的Channel支持多节点拉流配置，一个Channel支持多个endpoint拉流输出 。

![img](https://main.qcloudimg.com/raw/b8d01ade821b7ed659ab65a4617ed6e1.png)