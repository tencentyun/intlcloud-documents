### 语音识别如何接入？
语音识别目前支持 API 和 SDK 接入，推荐 SDK 接入，详情可参见 [语音识别入门](https://intl.cloud.tencent.com/document/product/1118/43355)。

### 影响语音识别结果准确率的因素有哪些？
远离拾音器、明显噪声、严重口音等因素会影响语音识别准确率。

### 如何查看音频格式和属性？
**Windows 系统下**：
可以下载相关软件查看和修改音频格式：Adobe Audition CS6。
**Linux 或者 macOS 系统下**：
用 **file** 命令查看，例如：**file test.wav**
结果：
![](https://main.qcloudimg.com/raw/769ec09e032d1a3d8b03749fe2039f34.png)
此音频的采样率为8k，采样精度为16bit，声道为 mono，即单声道（双声道为 stereo）。



