

Tencent Cloud MediaLive（MDL），致力于为全球用户提供极速、稳定、高质量的直播流媒体处理平台。

MediaLive依托腾讯云全球部署的众多可用区的计算资源，结合腾讯自研应用深耕多年的音视频技术平台以及全球

领先的音视频 AI 技术，将腾讯云视频直播的核心底层能力开放给用户，不仅为全球开发者提供专业、稳定、高效

的直播流转码、转封装、传输等基础服务，同时，提供数字版权保护以及SCTE35广告解决方案等增值等服务能

力。

腾讯云MediaLive是腾讯云新发布的的高质量流处理平台。

它可以提供广播级实时在线流媒体处理服务。使用此服务，您可以创建高质量的视频流，从而分发到各种类型的设

备。它的特点是使用了腾讯云独特的高性能视频编码和压缩算法，并在确保更好的观看体验的前提下，设法节省您

的传输流量。同时，它还保证了7 * 24小时的可用性。

## MediaLive主备流映射关系说明

![](https://main.qcloudimg.com/raw/62bf460b9d22d6450c828bcc8827d876.jpg)

MediaLive每一个频道支持两个pipeline配置，从input配置开始便支持主备通道输入设置。其中Pipeline A为必填项，Pipeline B为选填项。Pipeline A与Pipeline B各自独立运行，即从input A输入的stream会输出至各个output group的destination A中，从input B输入的stream会输出至各个output group的destination B中。（当输出类型选择MediaPackage时，会将Pipeline A与Pipeline B作为主备流输入至MediaPackage的channel中。）

其中output group与output之间的关系示意图如下：

![](https://main.qcloudimg.com/raw/6b2dca814f0b08a75ce6623749a00cc3.jpg)

每个output group决定一个输出协议或类型，其中可包含多个output。每个output可选取不同分辨率、码率的视频流，从而组合输出自适应码率直播流。