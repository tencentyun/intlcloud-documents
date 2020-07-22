Tencent Cloud MediaPackage（MDP），致力于为全球用户提供专业、稳定、安全的视频包装及交付服务。MediaPackage依托腾讯云全球部署的众多可用区的计算资源，结合腾讯自研应用深耕多年的音视频技术降低视频包装分发难度，增加源弹性（origin resiliency），允许视频供应商能够大规模安全稳定地分配视频流媒体。

## 主要功能

### 多协议主备流输入

MediaPackage支持HLS、DASH两种协议的流输入模式，同时针对每一个Channel生成主备流输入地址，支持两个主备流input同时推流，当主input出现网络不稳等异常推流情况，而备input推流正常时，可以无缝切换到备input。从而稳定、可靠地保护您的视频资产。

### 多样式输出方式

MediaPackage支持多个Endpoint节点回源拉流，支持一键配置对接腾讯云直播CDN 分配（distribution），助力客户形成自己的源站，保证视频供应商安全可靠地大规模分发视频流。

### 高安全性保护

MediaPackage从输入到输出支持多种安全鉴权模式，输入支持http-authentication 模式，可以根据username和password进行推流校验。输出支持配置IP黑白名单，支持配置Authkey，支持http-header通过 X-TENCENT-PACKAGE进行鉴权，支持CIDR级别的防护策略。

### 高可扩展性，可独立使用或联合腾讯云媒体服务产品使用
MediaPackage助力用户轻松形成自己的源站，从而交付给多方视频观看方。客户可基于MediaPackage降低视频包装分发的难度和复杂度。同时客户可联合腾讯云其余媒体服务产品（MediaLive、MediaConnect、LVB CDN等）集成使用，以实现大规模广播级别的一站式媒体全链路服务。

### 高可用缓存保护机制

MediaPackage提供多级缓存保护机制，当一个节点服务器异常，内置监控提供自动剔除节点机制，保障区域资源的高可靠性。同时推流支持主备流input模式，主备流input提供无缝切换机制，保证用户的推流高稳定可用性。