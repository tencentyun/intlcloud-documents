StreamLive控制台基于Channel维度进行管理，您可以创建高质量的视频流，从而分发到各种类型的设备。频道是StreamLive的主要模块，可对输入流按照既定配置进行转码、转封装等一系列视频处理操作后输出至指定目的地或者归档存储。

### 创建频道

选择【Channel Management】菜单，点击【Create Channel】创建频道输入。

#### 一、自定义频道名称

用于标识您创建的不同频道。点击【Next Step】进入下一步。

![img](https://main.qcloudimg.com/raw/824d8ad80106fb65f69df5dffae7bd0b.png)

#### 二、添加输入源

您可以从已创建的频道输入中选择1个或多个作为输入源添加至StreamLive频道上。**正常情况下，默认使用首位输入作为输入源**。其他输入源可能会在主备容灾（Failover）或时间计划（Plan）中被使用。 一个频道最多支持绑定5个输入源，其中最多2个PUSH输入。
![img](https://main.qcloudimg.com/raw/72974873310b8f07ea0acc09ce3c3f64.png)

针对不同类型的输入源，您可以点开【settings】对其进行如下的配置：

a. 【音频选择器】如果您的 RTP_PUSH / RTP-FEC_PUSH / UDP_PUSH 输入源中有多个音频流，则可以根据封装在MPEGTS中的音频PID在此处创建选择器，以便您可以在后面的输出配置页面中配置多音频语言。
![img](https://main.qcloudimg.com/raw/8ea9e3a78e57242e446f4ab2f4cd6850.png)

>!
> - 此处的PID必须与输入音频流的PID相同，否则转码任务可能会失败。
> - 只有首位输入（第一行的输入）才能进行音频选择器的配置，其他情况下该配置失效。若Plan的输入切换导致该输入源被使用，系统会默认挑选一路音轨对其进行转码。
> - 若输入源配置了主备容灾，则备流自动保持和主流一致的音频选择器配置，以便在主备切换时保证音频转码的可用性。

b. 【拉流设置】您可以为 MP4_PULL / HLS_PULL 输入源设置拉流转推的源端行为。两种模式：LOOP会循环拉流；ONCE会拉流一次结束后自动断掉输入流。
![img](https://main.qcloudimg.com/raw/a721d60a7263dddeab3927b3331cfaa2.png)

c. 【主备容灾设置】您可以为 RTMP_PUSH / RTP_PUSH 输入源设置主备容灾，以便当主流出现异常时自动转换到备流进行输入。选择开启主备容灾后，您可以选择一个输入源作为当前输入流的备流，同时您还可以设置故障检测时间（即等待主流异常多长时间后再启用主备容灾，默认3000ms）和输入源偏好（即主流恢复后是否优先切换回主流输入。PRIMARY_PREFERRED为主流优先，EQUAL_PREFERRED为主备同优先级）
![img](https://main.qcloudimg.com/raw/588efa49ee40b158793421c6ced77319.png)
![img](https://main.qcloudimg.com/raw/ebc0d3305a94534edaf97d09ecf18f9c.png)

>?
> - 最多只能配置一对主备流，且要求主流和备流要求输入源类型相同，通道数相同。
> - 主备关系确定后，备流的主备容灾开关自动锁定OFF（表示不可以继续为自己添加备流）。如果您需要调整主备关系（比如调换主备），须先解除/改变当前的主备关系后重新设置。
> - 主备容灾设置成功后，会在主流和备流输入名旁边出现“Primary”和“Backup”的标志字段。
> - 备流会自动调整顺序到主流的下面。

除了以上的设置，对于每个输入，您还可以对其进行如下的操作：

- 点击【details】查看输入地址等输入源的基本信息
- 点击【Set as First】置顶输入，将其设定为默认输入。注意：备流无法被置顶
- 点击【delete】删除某个输入源。

点击【Next Step】进入下一步。

#### 三、输出组设置

a. 多输出组设置。StreamLive支持一个频道多个Output Group的输出。点击右上方加号来添加多个Output Group。

![img](https://main.qcloudimg.com/raw/e6af7ba8a52e288e0d02dc3bea54871e.png)

b. 输出组名称和类型。设置当前Output Group的名称和类型。目前支持StreamLive支持HLS、DASH类型输出，同时支持输出HLS文件至腾讯云COS进行归档（具体操作详见第六节），也支持直接联合腾讯云StreamPackage一起使用，将HLS/DASH格式直播流直接输出至同账号下的StreamPackage中（具体操作详见第七节），从而帮助客户形成自己的源站，以便于直播的大规模稳定分发。

>?
> - 腾讯云对象存储COS介绍详见：[腾讯云对象存储COS详情](https://intl.cloud.tencent.com/document/product/436/6222)
> - 腾讯云StreamPackage介绍详见：[腾讯云StreamPackage详情](https://intl.cloud.tencent.com/document/product/1063/41786)

![img](https://main.qcloudimg.com/raw/6b87cbe42011cc98c045af99369348a3.png)

c. CDN推入地址设置。如果您选择了HLS或者DASH协议类型输出，您可在此填写CDN的推流地址。如果您的推流地址具有验证要求，则可以填写验证信息。

![img](https://main.qcloudimg.com/raw/8fb39dfab5a32ea34444b9a6f1e4edab.png)

d. Segment设置。在您的Manifest文件中设置Segment长度和Segment数量，如果您需要在标签文件中插入utc时间，那么可以打开Pdt的开关，并且设置插入utc时间的间隔。

![img](https://main.qcloudimg.com/raw/36b16a1dda37c530d7b8f497688a93d9.png)

e. DRM设置。腾讯云StreamLive支持用户自定义DRM，您可基于您的实际需求进行选择。

![](https://qcloudimg.tencent-cloud.cn/raw/f1cffba329af61327687d0efbe7442e1.png)

DRM设置中同时支持选择SDMCDRM作为DRM，用户需必填Uid、SecretID、Secret Key和Url字段

![](https://qcloudimg.tencent-cloud.cn/raw/e1350792aa213fe072920231474b0f68.png)

>?
>- 如果在Output Group Setting中的Output Group Type选择HLS/HLS_ARCHIVE/HLS_StreamPackage，开启DRM则会默认使用Fairplay加密；如果在Output Group Setting中的Output Group Type选择DSAH/DASH_StreamPackage，开启DRM会默认使用Widevine加密。
>- Fairplay密钥配置。当您选择输出类型选择HLS/HLS_ARCHIVE/HLS_StreamPackage时，您此时的加密方式为Fairplay加密，您需要填写Fairplay的ContentId（KeyId）、Key、Iv，其中Key、Iv为32位的16进制字符串。
 ![img](https://main.qcloudimg.com/raw/e172623be22b4397d9f4964d90e8eb03.png)
>- Widevine密钥配置。当您选择输出类型选择DSAH/DASH_StreamPackage时，您此时的加密方式为Widevine加密，Widevine的ContentId及其Track Setting，其中Track类型分SD/HD/UHD1/UHD2/AUDIO。
>- 选择All Track代表指定这五种Track类型的有相同KeyId、Key。
 ![img](https://main.qcloudimg.com/raw/06b22ae97702570f7bdfac4161219ece.png)
>- 选择Select Track则可自定义每个Track类型的KeyId和Key。
![img](https://main.qcloudimg.com/raw/9c9e6b56980d6c87aea64c2b3b426ad5.png)

f. 音频设置。StreamLive支持一个输出单元来配置多个音频转码。您可在此配置音频模板，包括音频名称、音频转码格式、音频码率以及对应的音频语言，其中如果不关联音频选择器，那么会从Input输入流中选择一路默认流进行转码输出。目前支持的音频转码码率范围在6000-1024000Bit范围内。语言代码遵循ISO639标准，需要填写3个字符的语言代码。

![img](https://main.qcloudimg.com/raw/c092adee1a2aeca7f9e98f18659b4aef.png)

g. 视频设置。StreamLive支持配置视频模板，包括视频模板名、编码器类型选择（当前支持H264）、视频转码码率（支持范围为50000-40000000Bit）、分辨率、帧率配置等。“Top Speed Codec Transcoding”是腾讯云视频团队开发的高性能视频转码服务，开启该功能后，可以通过AI算法能力，实时计算符合业务场景的最优动态编码参数实现低码率、高质量的转码服务；“Bitrate compression ratio”是预期需要降低的视频码率百分比。

![img](https://main.qcloudimg.com/raw/92242c0a054e342a1071794db28600de.png)

>? 如果您需要更好的带有智能视频压缩算法的编解码器，您可选择“极速高清”转码.启用此功能后，AI算法可以根据业务场景实时计算最佳动态编码参数，以实现低比特率和高质量的转码服务。

h. 输出组合。配置Outputs，对已经创建的音频转码模板以及视频转码模板进行组合关联；同时支持在HLS或DASH的文件标签中传递Scte35相关的信息。

![img](https://main.qcloudimg.com/raw/9e2db2401085804c20ea520364f43c3a.png)

i. 点击下方【Done】，保存配置。

![img](https://main.qcloudimg.com/raw/1874e5ebae643cddbe8f41c00bc92731.png)

j. 至此，整个频道已经配置完毕。点击【Start】即可运行。

![img](https://main.qcloudimg.com/raw/ec0fe249551d5db6d80697a1c5d47d36.png)


### 频道导入导出、克隆与编辑删除

StreamLive 支持通过导出/导入频道配置文件及频道克隆功能来快速完成频道创建工作。

#### 频道导出

StreamLive的【Channel Management】界面会显示您所有创建的频道及状态，点击右侧的【Export】按钮可快速导出频道配置json文件。

![img](https://main.qcloudimg.com/raw/764c7eea7b0ea222364a5b4dad88eb41.png)

![img](https://main.qcloudimg.com/raw/e67829bbee59c2148ba68ae1e652f8da.png)

#### 频道导入

打开【Channel Management】界面点击【Create Channel】按钮，选择【Import Configuration】，选中修改后的频道配置json文件保存。

提交json文件后即进入频道编辑状态，接着按照常规配置过程保存并提交频道即可。

![img](https://main.qcloudimg.com/raw/1fe8fdf4c50c5be5a6fe1dc820f5469f.png)

>?
> - 频道导入功能实际上是一次快速填写的过程，我们会基于您导入的json文件快速帮您自动填写【Basic Information】、【Output Group Setting】两部分内容，【Input Setting】部分会被忽略，需要您重新选择Input。因此如果您需要通过此方法快速创建一个Channel，可以提前创建好一个新的input。
> - 编辑频道时如果导入新的配置文件，则原来频道配置信息会被覆盖。

#### 频道克隆

频道克隆本质是一次快速且特殊的频道导出/导入操作，打开【Channel Management】界面点击【Operation】下的【Clone】后即可进入克隆频道的配置状态。

此时频道会自动填写被克隆频道的基本信息（【Input Setting】部分除外），接着按照常规配置过程保存并提交频道即可。

![img](https://main.qcloudimg.com/raw/92bf580af5c4f013363915688744f1f6.png)

1. 频道编辑和删除

频道正在【RUNNING】过程中无法进行编辑/删除操作，需先【Stop】频道在进行编辑/删除操作。

![img](https://main.qcloudimg.com/raw/57923bc62f83d99ee10df572bebbb6e3.png)

### 频道质量监控

打开【Channel Management】界面点击频道名称即可进入频道详情页面。频道详情页面会显示该频道的信息、输入、输出、Alerts、Health等详细信息。

![img](https://main.qcloudimg.com/raw/c97468a3a9fbeb51e9c15ae552d53efd.png)

当某个频道的任一管道中发生问题或潜在问题时，StreamLive都会为该频道生成警报。Set time为告警产生事件，Cleared time为告警消除时间。同一条告警记录会有状态更新，当告警记录为SET状态时，则Set time、State字段标红，当告警记录消除后，状态置为CLEARED，同时消除上述标红。警报会清晰记录发生问题的管道、警报类型和详细信息。数据查询只能查询最近5天，查询时间段小于24小时。

消除前：

![img](https://main.qcloudimg.com/raw/a76c4bb27dd86c6e2d06f2dd6ccbb42e.png)

消除后：

![img](https://main.qcloudimg.com/raw/4a986687ccdf97ce0e222aac2b936fb6.png)

Heath向用户提供频道输入（带宽、输入视频帧速率和输入音频帧速率）和输出（带宽）信息及对应的曲线图，以确定当前频道是否正常工作。数据查询只能查询最近5天，查询时间段小于24小时。

![img](https://main.qcloudimg.com/raw/e49e312b0d134d0d9fb1c8dccbcee00b.png)
![img](https://main.qcloudimg.com/raw/de84757254338b428e55695b4b3a2170.png)


### 设置时间计划

您可以为StreamLive频道设置时间计划，实现在推流过程中定时触发特定事件的设置（如：15:00:00 切换输入源为 input2）。

打开【Channel Management】界面点击频道名称即可进入频道详情页面，选择【Plan】，点击【Add】添加事件。

1. 有两种触发时间的模式可以选择：Fixed Time 需要您手动设置日期和时间，事件会在您设定的时间被执行；Immediate会以当前建立时间的时间作为触发时间，即立刻开始执行事件。
2. 事件类型目前仅支持“输入切换”功能，您可以为其选择目标输入源。

点击【create】完成一个时间-事件的创建。

![img](https://main.qcloudimg.com/raw/b45ec0b7275bc1c4363bd683652dd541.png)

![img](https://main.qcloudimg.com/raw/cb4c8a9d4f289072476364297346fb4d.png)

>!
> - 填写的时间为您所在的当地时间，且不可填写早于当前时间的时间。
> - 如果切换到的 MP4_PULL (或HLS_PULL)输入源的流设置是ONCE，则拉流一次后输入流自动断掉，后续的事件将不再被触发。

创建好的所有事件都可按照“触发时间”从早到晚由上至下排列，您可以对事件进行浏览、删除和新增。

>! 已创建的事件不支持编辑操作。

### 频道配置最佳实践

StreamLive 还提供多样的自定义功能，具体可参考以下最佳实践操作指引：

[使用DRMtoday为频道配置DRM](https://intl.cloud.tencent.com/document/product/1048/45217) 
[通过StreamLive输出至腾讯云COS归档](https://intl.cloud.tencent.com/document/product/1048/45218)
[通过StreamLive输出至腾讯云StreamPackage](https://intl.cloud.tencent.com/document/product/1048/45218)
[使用StreamLive直播时移](https://intl.cloud.tencent.com/document/product/1048/45220)

