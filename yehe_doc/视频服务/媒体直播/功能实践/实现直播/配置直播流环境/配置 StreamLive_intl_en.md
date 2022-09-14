Go to the [StreamLive console](https://console.tencentcloud.com/mdl/input). The left sidebar displays four sections:
● Security Group Management
● Input Management
● Channel Management
● Watermark Management
We will show you how to configure security groups, inputs, and channels (required), as well as watermarks (optional).

1. Select **Security Group Management** on the left sidebar and click **Create Security Group**. In the pop-up window, enter a security group name and specify the IP allowlist. IP addresses must be in CIDR format. Separate addresses with commas or line breaks.
![](https://qcloudimg.tencent-cloud.cn/raw/46e60d979177b96851cb16dc890d6890.png)

2. Select **Input Management** on the left sidebar, click **Create Input**, and complete the settings in the pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/8041139ea24469f261f31ebb1077f406.png)
- **Type**: The streaming protocol. RTMP_PUSH is selected in this example.
- **Security Group**: The security group to associate. Select from the drop-down list a created security group.
- **Destination**: The push destination. Enter at least one **AppName** and **StreamName**. You can configure two destinations to offer redundancy.

3. Click **Confirm**. Find the input you created in the input list to enter the details page. Note the push destination for later user.

4. Click **Channel Management** on the left sidebar and click **Create Channel**. In the **Basic Information** step, enter a channel name.
![](https://qcloudimg.tencent-cloud.cn/raw/dda466604218ebfd491cfbb0dd681fb0.png)

5. In the **Input Setting** step, add the input you just created (you can add multiple inputs, for which you can configure different transcoding templates and outputs).
![](https://qcloudimg.tencent-cloud.cn/raw/55c4b71f066c7e18804d029c30da04b1.png)

6. In the **Output Group Setting** step, configure transcoding templates and outputs for the channel.
- For **Basic Information**, enter an output group name and select an output group type (two protocols and three output types are supported). In the **Destination Information** area, enter the **StreamPackage Channel ID** you noted previously. This allows you to quickly implement transcoding and packaging for your live streams.
![](https://qcloudimg.tencent-cloud.cn/raw/04e6469dc287247e50bf0ff198b04c78.png)
- You can also specify the **Segment Information** on this page, including the segment type, segment duration, and segment number. For some devices, such as Apple TV, to play H.265-encoded videos, you need to select **fmp4** as the **Segment Type** and **hvc1** as the **Packaging Type**.
![](https://qcloudimg.tencent-cloud.cn/raw/407322c8d120feec4f2fab998f33e4a6.png)

7. Scroll down to the **Template Information** area to configure transcoding templates. You can configure joint transcoding templates or separate transcoding templates for audio and video. Multi-bitrate outputs are also supported.
![](https://qcloudimg.tencent-cloud.cn/raw/1f0b9aa788821031bb573eb52d07bbef.png)

8. In the **Outputs** area, enter a name for each output and select the transcoding templates to use. Click **Done**.
![](https://qcloudimg.tencent-cloud.cn/raw/405e9167353c870d5f687bbc7ce8ecc1.png)

9. Return to the channel list and click **Start** in the **Operation** column to start the channel.
![](https://qcloudimg.tencent-cloud.cn/raw/7391eea01e3b76709be2a36f309a3f5a.png)