Adaptive bitrate streaming is a method of streaming over HTTP where the source content is encoded at multiple bitrates or resolutions. Which bitrate is delivered to a player depends on network conditions. This can reduce stutter and improve streaming experiences.

To enable adaptive bitrate streaming, find the target channel on the **Channel Management** page and click **Edit**. Click **Next** until you enter the **Output Group Setting** page. You can configure outputs of different bitrates or protocols on this page. For detailed directions, see [Step 4. Configure Output Groups](https://www.tencentcloud.com/document/product/1048/49584).

The following section shows you how to configure adaptive bitrate streaming for HLS outputs:

1. First, you need to configure transcoding templates. Audio templates only support the AAC codec. Specify the audio bitrate. If the input is a TS file and a PID selector is specified, you can also configure the **Language Code** displayed in the manifest.
![](https://qcloudimg.tencent-cloud.cn/raw/29069263bb248e573abafb9ad89ff6b9.png)

2. The adaptive bitrate streaming feature is more relevant for videos because videos have higher bitrates and are more likely to be affected by network conditions. The H.264 and H.265 video codecs are supported, and you can choose either of two rate control modes: ABR and CBR. You can also enable **Top Speed Codec Transcoding** to deliver the same viewing experience at lower bitrates. Note that you cannot modify the rate control mode after enabling top speed codec.
![](https://qcloudimg.tencent-cloud.cn/raw/5a224587b665cf507a18b65bf5949c65.png)

3. After configuring the transcoding templates, you can go on to configure multi-bitrate outputs in the **Outputs** area.
![](https://qcloudimg.tencent-cloud.cn/raw/e32e9111691a28ce11bd9aa3b561d4be.png)

4. After the configuration, click **Done**. Now, the input of the channel will generate HLS outputs with two bitrates.

