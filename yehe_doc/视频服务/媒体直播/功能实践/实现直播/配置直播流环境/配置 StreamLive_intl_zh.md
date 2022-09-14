进入[StreamLive控制台](https://console.tencentcloud.com/mdl/input)后，左侧边栏列出了四项功能配置入口，分别为：
● 安全组管理 Security Group Management。
● 输入管理 Input Management。
● 频道管理 Channel Management。
● 水印管理 Watermark Management。
下面我们分别对上述功能进行配置，其中必要配置项为前三项，水印则为可选项按需配置。

1. 进入**Security Group Management**功能页，点击**Create Security Group**按钮，在弹出的对话框中输入安全组名称及IP白名单信息，其中IP白名单需按照CIDR 格式填写，多条可通过英文逗号或者换行进行分隔。
![](https://qcloudimg.tencent-cloud.cn/raw/46e60d979177b96851cb16dc890d6890.png)

2. 进入**Input Management**功能页，点击**Create Input**提交配置信息。
![](https://qcloudimg.tencent-cloud.cn/raw/8041139ea24469f261f31ebb1077f406.png)
- **Type**：推流协议类型，以RTMP_PUSH为例。
- **Security Group**：关联安全组，从下拉菜单中选择已创建好的安全组名称完成关联。
- **Destination**：推流目标地址，支持双通道推流，即系统可配置不同可用区推流地址，以提供冗余直播链路服务。这里至少需要填写一个推流地址的应用名**AppName**以及流名称**StreamName**。

3. 点击**Confirm**提交确认后，在**Input**列表点击刚才创建的Input进入详情页面,记录下推流目标地址**Destination**信息以备后续配置时使用。

4. 进入**Channel Management**功能页，点击**Create Channel**，按照系统提示流程逐步提交配置信息，首先在**Basic Information**中为该频道命名。
![](https://qcloudimg.tencent-cloud.cn/raw/dda466604218ebfd491cfbb0dd681fb0.png)

5. 在**Input Setting**中添加刚才配置的**Input**作为本频道的直播输入源，这里可以支持添加多个不同的Input，后续配置中可以分别进行不同的转码输出配置，本文暂以一个输入源为例。
![](https://qcloudimg.tencent-cloud.cn/raw/55c4b71f066c7e18804d029c30da04b1.png)

6. 在**Output Group Setting**中进行该频道的转码及输出配置：
- 首先配置基本信息，为**Output Group** 命名，输出类型按照协议和形式不同分为三组六项，本文选择HLS_STREAM_PACKAGE 类型，在下方**Destination Information**中填入刚才记录的**StreamPackage Channel ID**，即可快速打通直播转码及包装的工作流程，简化配置工作。
![](https://qcloudimg.tencent-cloud.cn/raw/c65352a34d5b860552f989838a6b0b2f.png)
- 进一步完善**Segment Information**切片信息，包括切片类型、切片时长、切片数量等。其中针对一些特殊的设备，如AppleTV，若存在H.265的播放需求，则这里的切片类型Segment Type 需要选为fmp4，同时H.265打包类型Packing Type 需要选为hvc1。
![](https://qcloudimg.tencent-cloud.cn/raw/407322c8d120feec4f2fab998f33e4a6.png)

7. 滑动到页面下方，继续进行转码模板配置，可配置音视频合并转码或仅针对音频或视频做独立转码配置，此外也支持配置多码率输出。
![](https://qcloudimg.tencent-cloud.cn/raw/1f0b9aa788821031bb573eb52d07bbef.png)

8. 最后在最终输出配置中，分别为不同码率输出流进行命名，并勾选对应的转码模板名称，提交确认即可完成所有信息的配置
![](https://qcloudimg.tencent-cloud.cn/raw/405e9167353c870d5f687bbc7ce8ecc1.png)

9. 最终回到频道列表后，在**Operation**列点击**Start**以激活启动该频道。
![](https://qcloudimg.tencent-cloud.cn/raw/7391eea01e3b76709be2a36f309a3f5a.png)
