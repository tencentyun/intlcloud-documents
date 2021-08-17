# 概述

腾讯云StreamLive是腾讯云新发布的的高质量流处理平台。它可以提供广播级实时在线流媒体处理服务。使用此服务，您可以创建高质量的视频流，从而分发到各种类型的设备。

StreamLive的特点是使用了腾讯云独特的高性能视频编码和压缩算法，并在确保更好的观看体验的前提下，帮助节省您的传输流量。同时，它还保证了7 * 24小时的高可用性。

![](https://main.qcloudimg.com/raw/b007110c97f491fb447302763ad85b20.png)

 

# 功能

**多协议多样式流输入**

StreamLive支持多种流媒体输入协议，比如支持RTP、RTMP、UDP、HLS、HTTP-MP4、RTP-FEC输入，提供PULL和PUSH两种输入方式。同时针对RTP MPEG-TS输入方式下支持多音轨视频流输入，并针对每一路音轨（语言种类）可做独立的转码配置。

**高质量多样式转码**

支持多种分辨率、多种码率、多帧率的转码功能，提供SD、HD、UHD、2K、4K等分辨率供客户选择。提供腾讯云极速高清（Top Speed Codec Transcoding）高性能转码服务，开启该功能后，可以通过AI算法能力，实时计算符合业务场景的最优动态编码参数实现低码率、高质量的转码服务。

**数字版权保护（DRM）**

提供更专业的数字版权管理解决方案（DRM）全面保护您的视频流安全，支持Fairplay以及Widevine加密方案，符合绝大多数版权保护的需求。

**多协议多方式输出**

支持多样式输出封装类型，支持自适应码率HLS、DASH 、输出至COS 归档、输出至SteamPackage等多样式输出。

**独立频道灵活配置** **多样式组合输出**

StreamLive基于频道管理（Channel Management）模式进行服务，同一频道可配置不同的Input及Outputs，同一Output可对已经创建的音频转码模板以及视频转码模板进行组合关联，灵活组合配置输出，实现自适应码率分发的能力。

**流质量监控**

基于每个Channel的运行状态提供详细Health报告，展示各类Alerts信息，方便客户实时查看流质量。

**高性能**

在SSIM和VMAF双标准下，腾讯云极速高清突出编码性能全面领先 Aws Elemental Medialive-qvbr同类产品。

**低成本**

极速高清优化传输码率的特性符合客户降CDN带宽成本的需求，在码率降低10%左右的情况下，依旧保持全面领先的性能。

**架构设计**

StreamLive每一个频道支持双通道配置，从input配置开始便支持主备通道输入设置。其中 Pipeline A 为必填项，Pipeline B为选填项。

Pipeline A与Pipeline B各自独立运行，即从input A输入的stream会输出至各个output group的destination A中，从input B输入的stream会输出至各个output group的destination B中。

![](https://main.qcloudimg.com/raw/ec3ea24ca723cdb08f3b8f35d339b6ff.png)