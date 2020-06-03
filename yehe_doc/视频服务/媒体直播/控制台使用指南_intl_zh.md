MediaLive基于channel维度进行管理，主要分为输入安全组（input security groups）、频道输入（input）、频道管理（channel）三个模块。
安全组主要对输入源的安全校验进行管理；频道输入可对频道输入源的协议及输入方式进行配置；频道是MediaLive的主要模块，可对输入流按照既定配置进行转码、转封装等一系列操作后输出。

## 安全组
输入安全组是用于对输入源IPV4地址进行合法性校验的手段，通过输入安全组配置，可以使medialive频道的输入更加安全。
### 创建安全组
![图片描述](https://main.qcloudimg.com/raw/d6a6ae8de1db8cb120e995c11b61aec3.png)
Name：安全组的名称，限制由字母、数字以及下划线组成的32个字符的字符串。
White list：表示输入IPV4地址的合法地址段。使用CIDR格式表示，例如0.0.0.0.0/0，所有输入IP都合法。最多支持10个网段的输入，不同网段可以输入在不同的行。

**注意**：控制台默认只支持5个安全组的创建，如果大量安全组创建需求，请提交工单联系腾讯云客服人员。

### 查看安全组

![图片描述](https://main.qcloudimg.com/raw/a3c9a3f88f00d65e8993de2224244d3e.png)
安全组列表是由4部分组成，
第一列安全组的名称，上文已解释；
第二列表示安全组的状态，安全组存在两种状态，idle和occupied两种状态。idle表示当前安全组没有被关联，可以编辑和删除；occupied表示当前安全组已经被频道输入关联，此时的安全组只能编辑，不能被删除。

## 频道输入

频道输入是medialive的媒体流输入通道，通常关联一个安全组和一个medialive的频道。
### 创建输入
![图片描述](https://main.qcloudimg.com/raw/f6890473b696bfa90064d2f3edffc76d.png)
Name：频道输入的名称。
Type：支持RTP_PUSH、RTMP_PUSH、UDP_PUSH、HLS_PULL、MP4_PULL等6中输入模式。
Security Group：关联安全组，一个输入只能关联一个安全组。
**注意**

>
> 1. 控制台默认只支持最多5个input的存在。
> 2. 输入的媒体源目前至少需要包含一个视频数据通道。
> 3. 当使用MPEGTS多路复用通道时，最多允许8路通道同时传输。

## 频道
channel是medialive产品将摄入流进行转码和转封装以及转推到其他目的地址的详细信息。
创建channel的主体流程：

> 1. 关联已经存在的input。
> 2. 配置音频选择器。
> 3. 进行转码参数、转封装参数以及输出参数的配置

我们提供多种方式进行频道配置：

> 1. 从头开始创建，可以完全自定义你想要的所有选项。
> 2. 使用内置的模板或自定义模板进行创建。
> 3. 克隆现有的channel配置进行修改创建。

### 创建频道
![图片描述](https://main.qcloudimg.com/raw/010317a5d04d3019c1856dfafb1ffade.png)
1、配置channel的名称。
**注意**：channel的Name是账号下唯一的，如果设置重复的channel name会导致创建channel失败。
2、关联channel的input以及创建音频选择器。
在已经创建的input里选择可关联的input进行配置，这样channel可以通过关联的input进行流的输入。
3、channel的输出配置。
配置一个输出group：


> 1. 配置Output group name，标识当前output group的名称，同时关联了播放地址主manifest的文件名称。
> 2. 配置Output group type，配置当前output任务的package类型，当前支持hls、dash以及hls archive。
> 3. 配置输出地址，其中分为主输出地址和备份输出地址，分别对应input中的主备输入地址生效。如果你的cdn注入点开启了认证保护的话，可以输入authentication参数进行验证，其中包括UserName和Password。
> 4. 配置DRM参数，开启该功能后，可以输入自定义的Content Id，生成方法参考DRM相关文档。
> 5. 配置音频模板，包括音频名称，音频转码格式，音频码率以及对应的音频语言，其中如果不关联音频选择器，那么会从input输入流中选择一路默认流进行转码输出。目前支持的音频转码码率范围在6000-1024000bit范围内。语言代码遵循ISO639标准，需要填写3个字符的语言代码。
> 6. 配置视频模板，包括视频模板名；包括编码器类型选择，当前支持H264；包括视频转码码率，支持范围为50000-40000000bit；包括分辨率、帧率配置等等。top speed codec transcoding是腾讯云视频团队开发的高性能视频转码服务，开启该功能后，可以通过AI算法能力，实时计算符合业务场景的最优动态编码参数实现低码率、高质量的转码服务，Bitrate compression ratio是预期需要降低的视频码率百分比。
> 7. 配置Outputs，对已经创建的音频转码模板以及视频转码模板进行组合关联；同时支持在mpegts中透传scte35的信息。

至此，频道配置完成。
您可基于配置好的频道对您的输入流进行操作后输出，同时您可在频道的Alerts及Health页面查看您的频道运行状态，对一些基本的alerts信息进行定位和分析。
