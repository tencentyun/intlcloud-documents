### License

通过购买特定类型的点播套餐包，可获取对应的 SDK License，开启对应的短视频 SDK 功能服务 。

>! 购买点播套餐包并绑定 License 后，请确认 [Bundle ID 和 Package Name](https://intl.cloud.tencent.com/document/product/1069/46320) 无误再单击**确定**提交。一旦提交，**License 信息不能再做修改**。

### 播放器签名

播放器签名用于 App 播放服务对终端的授权播放。若 App 播放服务允许终端播放，则派发一个合法的签名，终端在签名有效时间内可以播放视频内容。当有如下情况之一时，App 终端需要超级播放器签名才能播放：

- 域名开启了 [KEY 防盗链](https://intl.cloud.tencent.com/document/product/266/33986)。
- 使用了 default 以外的 [播放器配置](https://intl.cloud.tencent.com/document/product/266/38296)。
- 需要播放 [加密](https://intl.cloud.tencent.com/document/product/266/38294) 的视频内容。

>? 播放器签名的具体功能和使用方式，请参见 [播放器签名文档](https://intl.cloud.tencent.com/document/product/266/38099)。

### 帧率
帧率（Frame Rate）是单位时间内视频显示帧数的量度单位，测量单位为“每秒显示帧数”（Frame Per Second，FPS）。

### 码率
码率（Bitrate）是单位时间播放连续媒体（如压缩后的音频或视频）所需的比特数量，测量单位为“比特每秒”（bit/s 或 bps）。

### 转码
转码是将视频码流转换成另一个视频码流的过程，并可改变原始码流的编码格式、分辨率和码率等参数，从而适应不同终端和网络环境的播放。使用转码功能可以实现：
- 适配更多终端：将原始视频转码成拥有更强终端适配能力的格式（如 MP4），使视频资源能够在更多设备上播放。
- 适配不同带宽：将视频转换成流畅、标清、高清以及超清等输出，用户可以根据当前网络环境选择合适码率的视频播放。
- 改善播放效率：转码可以将 MP4 位于尾部的元信息 MOOV 提前到头部，播放器无需下载完整视频即可立即播放。
- 为视频打水印：为视频打上水印，标识视频的归属或版权。
- 节省带宽：采用更先进的编码方式（如 H.265）转码，在不损失原始画质的情况下显著降低码率，节省播放带宽。

### 关键帧
帧是组成视频图像的基本单位，视频文件是由多个连续的帧组成。

### 时间戳
时间戳记录数据发生的时间。

### GOP
GOP（Group of Pictures）是一组以 MPEG 编码的影片或视讯串流内部连续图像，以 I 帧开头，到下一个 I 帧结束。一个 GOP 包含如下图像类型：
- I 帧（Intra Coded Picture）：节点编码图像。一个固定影像，且独立于其它的图像类型，每个 GOP 由此类型的图像开始。
- P 帧（Predictive Coded Picture）：预测编码图像。包含来自先前的 I 帧或 P 帧的差异信息。
- B 帧（Bidirectionally Predictive Coded Pictures）：前后预测编码图像。包含来自先前或之后的 I 帧或 P 帧的差异信息。

一个 GOP 内的帧数，称为 GOP 长度。

### 编码方式
编码方式（Codec）能够对数字视频进行压缩或者解压缩（视频解码）的程序或者设备。常见的编码方式包括：
- H.26X 系列，由 ITU（国际电信联盟）主导。该系列标准中，目前应用最广泛的是 H.264，其继任者为 H.265。同等画质下，H.265 的压缩率可以比 H.264 提高一倍，但受制于专利等因素，H.265 的应用尚未普及。
- MPEG 系列，由 ISO（国际标准组织机构）下属的 MPEG（运动图象专家组）主导。
- 其他系列，例如 Google 主导的 VP8、VP9，Real 公司主导的 RealVideo 等。

### 事件通知
对云点播中的视频发起上传、删除、视频处理等的操作，都可以被称为一个事件。事件的执行需要一段时间才能完成，云点播在事件结束时，会立即通知 App 服务操作的执行结果，即事件通知。
