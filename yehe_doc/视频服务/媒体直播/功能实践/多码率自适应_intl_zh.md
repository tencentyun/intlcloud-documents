Adaptive Bitrate Streaming（ABR）是一种旨在通过HTTP网络有效的传输直播流的方式。向用户播放器提供多个内容相同但码率或分辨率不同的输出，并通过对网络的探测情况，自适应的分发适合该播放器网络的最佳链接，从而减少网络卡顿，提高直播体验。

如需配置多码率自适应，首先在**Channel Management**中选择需要配置的**Channel**，然后点击**Edit**，通过点击**Next**进入到**Output Group Setting**配置页面，这里可以根据需要配置不同码率或不同协议的输出组。具体的输出配置可参考[设置输出组](https://www.tencentcloud.com/document/product/1048/49584)。

这里以HLS的输出协议为例，介绍配置步骤：

1. 首先设置转码模版，音频转码**Acodec**仅支持AAC，设置对应的**Bitrate**字段，若输入源是TS且设置了相应的Pid Selector，这里还可以设置展示在Mainfest中的**Language字段**。
![](https://qcloudimg.tencent-cloud.cn/raw/29069263bb248e573abafb9ad89ff6b9.png)

2. 多码率自适应更主要的还是体现在视频模版中，因为视频码率相对于音频较大，更加容易受到网络速率的影响。视频转码**Vcodec**支持H264、H265两种编码格式。**Rate Control Mode**支持ABR(动态码率)和CBR(恒定码率)两种模式。同时如果想达到相同视觉效果而使用更低码率，可以使用更高阶的转码方案，开启**Top Speed Codec Transcoding**，开启该模式后，**Rate Control Mode**将不支持修改。
![](https://qcloudimg.tencent-cloud.cn/raw/5a224587b665cf507a18b65bf5949c65.png)

3. 配置好转码模版后，就可以在**Outputs**中设置多个码率组合的输出了，这里选择两个码率的输出组。
![](https://qcloudimg.tencent-cloud.cn/raw/e32e9111691a28ce11bd9aa3b561d4be.png)

4. 点击**完成Done**后，当有输入时将会生成带有两个码率的HLS输出。

