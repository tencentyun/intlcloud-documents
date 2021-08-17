## 概览
腾讯云StreamLive是腾讯云新发布的的高质量流处理平台。它可以提供广播级实时在线流媒体处理服务。使用腾讯云独特的高性能视频编码和压缩算法，并在确保更好的观看体验的前提下，设法节省您的传输流量。

StreamLive控制台基于Channel维度进行管理，您可以创建高质量的视频流，从而分发到各种类型的设备。

## 控制台概览
StreamLive控制台基于Channel维度进行管理。主要分为安全组（Security Groups）、频道输入（Input）、频道管理（Channel）三个模块。安全组主要对输入源的安全校验进行管理；频道输入可对频道输入源的协议及输入方式进行配置；频道是StreamLive的主要模块，可对输入流按照既定配置进行转码、转封装等一系列视频处理操作后输出至指定目的地或者归档存储。
![](https://main.qcloudimg.com/raw/e76d930fd73f010632e9e4571a8351d9.png) 

## 前提条件
登录[腾讯云StreamLive控制台](https://console.cloud.tencent.com/mdl/security)。

## 操作步骤

###  一、选择区域
目前腾讯云StreamLive已提供印度孟买、泰国曼谷、韩国首尔三个可用区，您可在此选择您所在的地域。日本东京等地域正在加速部署上线中，如果您有其余可用区的加速部署诉求请[联系我们](https://intl.cloud.tencent.com/contact-sales)。
![](https://main.qcloudimg.com/raw/c9da8ddd469f557487c5b6d943ef69af.png)



### 二、创建安全组

安全组是用于对输入源IPV4地址进行合法性校验的手段，通过输入安全组配置，可以使StreamLive频道的输入更加安全。

选择【Security Group Management】菜单，点击【Create Security Group】创建安全组。输入Name后，将CIDR格式的字符串添加到新的输入安全组中，并用逗号或换行符分隔。输入完毕后点击【Confirm】完成创建。
![](https://main.qcloudimg.com/raw/e5c7365ba3724802b2013b3c25cdc07b.png)

>?
>- 安全组存在两种状态，idle和occupied两种状态。
>- idle表示当前安全组没有被关联，可以编辑和删除；
>- occupied表示当前安全组已经被channel-input关联，此时的安全组只能编辑，不能被删除。
>- 控制台默认只支持5个安全组的创建，如有更多的安全组创建需求，请[提交工单](https://console.cloud.tencent.com/workorder)联系腾讯云客服人员。



### 三、创建输入

选择【Input Management】菜单，点击【Create Input】创建频道输入。

频道输入是StreamLive的媒体流输入通道，通常关联一个安全组和一个StreamLive的频道。频道输入目前支持RTP、RTP-FEC、RTMP、UDP、HLS、HTTP-MP4等协议输入，提供PULL和PUSH两种输入方式。

每一个频道输入可以关联一个安全组和一个频道，被频道关联的输入状态会显示attached。
![](https://main.qcloudimg.com/raw/eed9a73cc25fc646b1f601ac545ccc0e.png)

>?
>- 控制台默认只支持最多5个input的存在。
>- 输入的媒体源目前至少需要包含一个视频数据通道。
>- 当使用MPEG-TS多路复用通道时，最多允许8路通道同时传输。



### 四、StreamLive频道创建

1. 选择【Channel Management】菜单，点击【Create Channel】创建频道输入。

2. 自定义频道名称。用于标识您创建的不同频道。点击【Next Step】进入下一步。

   ![](https://main.qcloudimg.com/raw/824d8ad80106fb65f69df5dffae7bd0b.png)

3. 添加输入源。您可以从已创建的频道输入中选择1个或多个作为输入源添加至StreamLive频道上。**正常情况下，默认使用首位输入作为输入源**。其他输入源可能会在主备容灾（Failover）或时间计划（Plan）中被使用。 一个频道最多支持绑定5个输入源，其中最多2个PUSH输入。
    ![](https://main.qcloudimg.com/raw/72974873310b8f07ea0acc09ce3c3f64.png)

针对不同类型的输入源，您可以点开【settings】对其进行如下的配置：

a.  【音频选择器】如果您的 RTP_PUSH / RTP-FEC_PUSH / UDP_PUSH 输入源中有多个音频流，则可以根据封装在MPEGTS中的音频PID在此处创建选择器，以便您可以在后面的输出配置页面中配置多音频语言。
![](https://main.qcloudimg.com/raw/8ea9e3a78e57242e446f4ab2f4cd6850.png)

>!
>- 此处的PID必须与输入音频流的PID相同，否则转码任务可能会失败。
>- 只有首位输入（第一行的输入）才能进行音频选择器的配置，其他情况下该配置失效。若Plan的输入切换导致该输入源被使用，系统会默认挑选一路音轨对其进行转码。
>- 若输入源配置了主备容灾，则备流自动保持和主流一致的音频选择器配置，以便在主备切换时保证音频转码的可用性。

b.    【拉流设置】您可以为 MP4_PULL / HLS_PULL 输入源设置拉流转推的源端行为。两种模式：LOOP会循环拉流；ONCE会拉流一次结束后自动断掉输入流。
![](https://main.qcloudimg.com/raw/a721d60a7263dddeab3927b3331cfaa2.png)

c.    【主备容灾设置】您可以为 RTMP_PUSH / RTP_PUSH 输入源设置主备容灾，以便当主流出现异常时自动转换到备流进行输入。选择开启主备容灾后，您可以选择一个输入源作为当前输入流的备流，同时您还可以设置故障检测时间（即等待主流异常多长时间后再启用主备容灾，默认3000ms）和输入源偏好（即主流恢复后是否优先切换回主流输入。PRIMARY_PREFERRED为主流优先，EQUAL_PREFERRED为主备同优先级）
![](https://main.qcloudimg.com/raw/588efa49ee40b158793421c6ced77319.png) 
![](https://main.qcloudimg.com/raw/ebc0d3305a94534edaf97d09ecf18f9c.png)

>?
>- 最多只能配置一对主备流，且要求主流和备流要求输入源类型相同，通道数相同。
>- 主备关系确定后，备流的主备容灾开关自动锁定OFF（表示不可以继续为自己添加备流）。如果您需要调整主备关系（比如调换主备），须先解除/改变当前的主备关系后重新设置。
>- 主备容灾设置成功后，会在主流和备流输入名旁边出现“Primary”和“Backup”的标志字段。
>- 备流会自动调整顺序到主流的下面。

除了以上的设置，对于每个输入，您还可以对其进行如下的操作：

- 点击【details】查看输入地址等输入源的基本信息
- 点击【Set as First】置顶输入，将其设定为默认输入。注意：备流无法被置顶
- 点击【delete】删除某个输入源。

点击【Next Step】进入下一步。

4. 输出组设置。

a. 多输出组设置。StreamLive支持一个频道多个Output Group的输出。点击右上方加号来添加多个Output Group。

![](https://main.qcloudimg.com/raw/e6af7ba8a52e288e0d02dc3bea54871e.png)

b. 输出组名称和类型。设置当前Output Group的名称和类型。目前支持StreamLive支持HLS、DASH类型输出，同时支持输出HLS文件至腾讯云COS进行归档（具体操作详见第六节），也支持直接联合腾讯云StreamPackage一起使用，将HLS/DASH格式直播流直接输出至同账号下的StreamPackage中（具体操作详见第七节），从而帮助客户形成自己的源站，以便于直播的大规模稳定分发。

>?
>- 腾讯云对象存储COS介绍详见：[腾讯云对象存储COS详情](https://intl.cloud.tencent.com/document/product/436/6222)
>- 腾讯云StreamPackage介绍详见：[腾讯云StreamPackage详情](https://intl.cloud.tencent.com/document/product/1063/37495)

![](https://main.qcloudimg.com/raw/6b87cbe42011cc98c045af99369348a3.png)

c. CDN推入地址设置。如果您选择了HLS或者DASH协议类型输出，您可在此填写CDN的推流地址。如果您的推流地址具有验证要求，则可以填写验证信息。

![](https://main.qcloudimg.com/raw/8fb39dfab5a32ea34444b9a6f1e4edab.png)

d. Segment设置。在您的Manifest文件中设置Segment长度和Segment数量，如果您需要在标签文件中插入utc时间，那么可以打开Pdt的开关，并且设置插入utc时间的间隔。

![](https://main.qcloudimg.com/raw/36b16a1dda37c530d7b8f497688a93d9.png) 

e. DRM设置。腾讯云StreamLive支持用户自定义DRM，您可基于您的实际需求进行选择。

![](https://main.qcloudimg.com/raw/fbb528cc453be167497d4d7eca823d43.png)

>? 如果在Output Group Setting中的Output Group Type选择HLS/HLS_ARCHIVE/HLS_StreamPackage，开启DRM则会默认使用Fairplay加密；如果在Output Group Setting中的Output Group Type选择DSAH/DASH_StreamPackage，开启DRM会默认使用Widevine加密。
>-  Fairplay密钥配置。当您选择输出类型选择HLS/HLS_ARCHIVE/HLS_StreamPackage时，您此时的加密方式为Fairplay加密，您需要填写Fairplay的ContentId（KeyId）、Key、Iv，其中Key、Iv为32位的16进制字符串。
![](https://main.qcloudimg.com/raw/e172623be22b4397d9f4964d90e8eb03.png)
>-  Widevine密钥配置。当您选择输出类型选择DSAH/DASH_StreamPackage时，您此时的加密方式为Widevine加密，Widevine的ContentId及其Track Setting，其中Track类型分SD/HD/UHD1/UHD2/AUDIO。
>- 选择All Track代表指定这五种Track类型的有相同KeyId、Key。
![](https://main.qcloudimg.com/raw/06b22ae97702570f7bdfac4161219ece.png)
>- 选择Select Track则可自定义每个Track类型的KeyId和Key。
![](https://main.qcloudimg.com/raw/9c9e6b56980d6c87aea64c2b3b426ad5.png)

f. 音频设置。StreamLive支持一个输出单元来配置多个音频转码。您可在此配置音频模板，包括音频名称、音频转码格式、音频码率以及对应的音频语言，其中如果不关联音频选择器，那么会从Input输入流中选择一路默认流进行转码输出。目前支持的音频转码码率范围在6000-1024000Bit范围内。语言代码遵循ISO639标准，需要填写3个字符的语言代码。

![](https://main.qcloudimg.com/raw/c092adee1a2aeca7f9e98f18659b4aef.png)

g. 视频设置。StreamLive支持配置视频模板，包括视频模板名、编码器类型选择（当前支持H264）、视频转码码率（支持范围为50000-40000000Bit）、分辨率、帧率配置等。“Top Speed Codec Transcoding”是腾讯云视频团队开发的高性能视频转码服务，开启该功能后，可以通过AI算法能力，实时计算符合业务场景的最优动态编码参数实现低码率、高质量的转码服务；“Bitrate compression ratio”是预期需要降低的视频码率百分比。

![](https://main.qcloudimg.com/raw/92242c0a054e342a1071794db28600de.png)

>? 如果您需要更好的带有智能视频压缩算法的编解码器，您可选择“极速高清”转码.启用此功能后，AI算法可以根据业务场景实时计算最佳动态编码参数，以实现低比特率和高质量的转码服务。

h. 输出组合。配置Outputs，对已经创建的音频转码模板以及视频转码模板进行组合关联；同时支持在HLS或DASH的文件标签中传递Scte35相关的信息。

![](https://main.qcloudimg.com/raw/9e2db2401085804c20ea520364f43c3a.png)

i. 点击下方【Done】，保存配置。

![](https://main.qcloudimg.com/raw/1874e5ebae643cddbe8f41c00bc92731.png)

j. 至此，整个频道已经配置完毕。点击【Start】即可运行。

![](https://main.qcloudimg.com/raw/ec0fe249551d5db6d80697a1c5d47d36.png)



## 五、通过StreamLive输出至腾讯云COS归档

StreamLive支持输出HLS文件至腾讯云COS进行归档，需要您先在COS中完成存储桶的创建并授权StreamLive访问您的存储桶。

1. 开通COS服务并创建COS存储桶

在开始输出至COS归档前，请先确定您已经[开通腾讯云COS服务](https://console.cloud.tencent.com/cos5)。完成COS服务的开通后，在[COS存储桶控制台](https://console.cloud.tencent.com/cos5)选择【存储桶列表】，单击【创建存储通】创建就近地区的COS存储桶。

![](https://main.qcloudimg.com/raw/258a128f8e010886f7bea5b6dac83c72.png)

2. 选择输出类型为HLS_ARCHIVE。回到StreamLive控制台，在配置输出时，选择输出类型为HLS_ARCHIVE。

![](https://main.qcloudimg.com/raw/5e782e85e27d4f860d9921cc86f1165f.png)

3. 授权StreamLive访问COS存储桶。由于您暂未授权StreamLive访问您的COS存储桶，COS 目的地字段将会置灰并不允许填写。点击提示中的【click here】跳出授权提示框。点击【Authorize Now】前往授权界面。点击【Grant】完成授权。

![](https://main.qcloudimg.com/raw/5327f143f1fc7482c68225e8abad3c82.png)![](https://main.qcloudimg.com/raw/3b3a91b1e9053f9ac0b6c9bc2955e12c.png)

完成授权后回到StreamLive界面，选择【Authorization completed】，则此时COS Destination字段可以填写。

![](https://main.qcloudimg.com/raw/ee8f5a51ec6fb2642e570a9c67f91865.png)![](https://main.qcloudimg.com/raw/41fc5c9c4a18d04b54f6585241231688.png)

4. 填写COS归档地址。您可基于您创建的COS存储桶填写COS归档地址，格式为：http://<BucketName-APPID>.cos.<Region>.myqcloud.com/path

5. 保存并提交配置。此时您可接着完成【四-4】节中的其余channel配置，并提交保存。



## 六、通过StreamLive输出至腾讯云StreamPackage

StreamLive支持直接联合腾讯云StreamPackage一起使用，将HLS/DASH格式直播流直接输出至同账号下的StreamPackage中，以便于用户形成自己的源站，从而进行下一步的视频分发与播放。

1. 开通StreamPackage

在输出至StreamPackage前请先[开通StreamPackage服务](https://console.cloud.tencent.com/mdp/channel)并创建Channel。

2. 完成StreamPackage的Channel创建

点击左上方【Create Channel】创建一个频道，填写频道的名称以及与StreamLive输出类型一致的协议。例如：当StreamLive选择输出类型为HLS_StreamPackage时，则此处选择HLS。

>! StreamLive与StreamPackage需要处于同一Region下。

![](https://main.qcloudimg.com/raw/ca0ae9e483499e4489a8db47b7bb290b.png)

3. 创建Endpoint

创建Channel完毕后会进入到Channel的详情页中，此时我们创建一个Endpoint节点，您也可以根据业务实际需要选择是否开启IP黑白名单或者鉴权功能。

![](https://main.qcloudimg.com/raw/da2c4f2cefcbb73aa5ba68f75579937c.png)

4. 获得Endpoint地址及Channel ID

创建完毕后的Endpoint的URL即为播放/源站地址。

![](https://main.qcloudimg.com/raw/30594049a37593a5d8827990bd9a13a1.png)

>?Channel ID将用于StreamLive输出的填写。

![](https://main.qcloudimg.com/raw/c66b1bb5f1c9f570225310e66f8e0a66.png)

5. 选择输出类型为HLS_STREAMPACKAGE或DASH_STREAMPACKAGE

回到StreamLive控制台，在配置输出时，选择输出类型为HLS_STREAMPACKAGE或者DASH_STREAMPACKAGE（这取决于您的业务实际需求及您刚刚创建的StreamPackage的Channel类型）。再填入您StreamPackage中的Channel ID即可。

![](https://main.qcloudimg.com/raw/486e54380f8bbecd2430c01ad8265c86.png)

6. 保存并提交配置。此时您可接着完成【四-4】节中的其余Channel配置，并提交保存。



## 七、频道导入导出、克隆与编辑删除

StreamLive 支持通过导出/导入频道配置文件及频道克隆功能来快速完成频道创建工作。

1. 频道导出

StreamLive的【Channel Management】界面会显示您所有创建的频道及状态，点击右侧的【Export】按钮可快速导出频道配置json文件。

![](https://main.qcloudimg.com/raw/764c7eea7b0ea222364a5b4dad88eb41.png)

![](https://main.qcloudimg.com/raw/e67829bbee59c2148ba68ae1e652f8da.png)

2. 频道导入

打开【Channel Management】界面点击【Create Channel】按钮，选择【Import Configuration】，选中修改后的频道配置json文件保存。

提交json文件后即进入频道编辑状态，接着按照常规配置过程保存并提交频道即可。

![](https://main.qcloudimg.com/raw/1fe8fdf4c50c5be5a6fe1dc820f5469f.png)

>?
>- 频道导入功能实际上是一次快速填写的过程，我们会基于您导入的json文件快速帮您自动填写【Basic Information】、【Output Group Setting】两部分内容，【Input Setting】部分会被忽略，需要您重新选择Input。因此如果您需要通过此方法快速创建一个Channel，可以提前创建好一个新的input。
>- 编辑频道时如果导入新的配置文件，则原来频道配置信息会被覆盖。

3. 频道克隆

频道克隆本质是一次快速且特殊的频道导出/导入操作，打开【Channel Management】界面点击【Operation】下的【Clone】后即可进入克隆频道的配置状态。

此时频道会自动填写被克隆频道的基本信息（【Input Setting】部分除外），接着按照常规配置过程保存并提交频道即可。

![](https://main.qcloudimg.com/raw/92bf580af5c4f013363915688744f1f6.png)

4. 频道编辑和删除

频道正在【RUNNING】过程中无法进行编辑/删除操作，需先【Stop】频道在进行编辑/删除操作。

![](https://main.qcloudimg.com/raw/57923bc62f83d99ee10df572bebbb6e3.png)



## 八、频道质量监控

打开【Channel Management】界面点击频道名称即可进入频道详情页面。频道详情页面会显示该频道的信息、输入、输出、Alerts、Health等详细信息。

![](https://main.qcloudimg.com/raw/c97468a3a9fbeb51e9c15ae552d53efd.png)

当某个频道的任一管道中发生问题或潜在问题时，StreamLive都会为该频道生成警报。Set time为告警产生事件，Cleared time为告警消除时间。同一条告警记录会有状态更新，当告警记录为SET状态时，则Set time、State字段标红，当告警记录消除后，状态置为CLEARED，同时消除上述标红。警报会清晰记录发生问题的管道、警报类型和详细信息。数据查询只能查询最近5天，查询时间段小于24小时。

消除前：

![](https://main.qcloudimg.com/raw/a76c4bb27dd86c6e2d06f2dd6ccbb42e.png)

消除后：

![](https://main.qcloudimg.com/raw/4a986687ccdf97ce0e222aac2b936fb6.png)

Heath向用户提供频道输入（带宽、输入视频帧速率和输入音频帧速率）和输出（带宽）信息及对应的曲线图，以确定当前频道是否正常工作。数据查询只能查询最近5天，查询时间段小于24小时。

![](https://main.qcloudimg.com/raw/e49e312b0d134d0d9fb1c8dccbcee00b.png) 
![](https://main.qcloudimg.com/raw/de84757254338b428e55695b4b3a2170.png) 



## 九、设置时间计划

您可以为StreamLive频道设置时间计划，实现在推流过程中定时触发特定事件的设置（如：15:00:00 切换输入源为 input2）。

打开【Channel Management】界面点击频道名称即可进入频道详情页面，选择【Plan】，点击【Add】添加事件。

1. 有两种触发时间的模式可以选择：Fixed Time 需要您手动设置日期和时间，事件会在您设定的时间被执行；Immediate会以当前建立时间的时间作为触发时间，即立刻开始执行事件。

2. 事件类型目前仅支持“输入切换”功能，您可以为其选择目标输入源。

点击【create】完成一个时间-事件的创建。

![](https://main.qcloudimg.com/raw/b45ec0b7275bc1c4363bd683652dd541.png)

![](https://main.qcloudimg.com/raw/cb4c8a9d4f289072476364297346fb4d.png)

>!
>- 填写的时间为您所在的当地时间，且不可填写早于当前时间的时间。
>- 如果切换到的 MP4_PULL (或HLS_PULL)输入源的流设置是ONCE，则拉流一次后输入流自动断掉，后续的事件将不再被触发。

创建好的所有事件都可按照“触发时间”从早到晚由上至下排列，您可以对事件进行浏览、删除和新增。

>! 已创建的事件不支持编辑操作。