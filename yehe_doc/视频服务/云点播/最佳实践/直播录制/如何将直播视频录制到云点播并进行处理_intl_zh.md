直播录制方案将直播原始流经过转音视频封装（不修改音频、视频数据以及对应的时间戳等信息）得到的文件存储到腾讯云点播平台，并对录制文件进行二次制作、分发播放的标准解决方案。更多详情可参见 [直播录制解决方案](https://intl.cloud.tencent.com/document/product/1082)。

## 产品特性
- 基于腾讯云直播能力，能快速将直播流内容进行录制并存储至云平台并进行二次制作和分发。
- 基于腾讯云领先的音视频 AI 技术及全球海量直播加速节点，为您提供专业、稳定的直播推流、转码、分发及播放服务，全面满足超低延迟、超高画质、超大并发访问量的要求。
- 基于直播录制服务，能快速将您的直播活动传播到各种应用场景和 App 中。
- 适用于多种行业场景，如企业直播、电商直播、教育直播等。适用于多种分发方案，如腾讯视频等。

## 前提条件
- [注册](https://intl.cloud.tencent.com/register) 并 [登录](https://intl.cloud.tencent.com/login) 腾讯云账号，并且完成账号实名认证，未进行实名认证的用户无法购买中国大陆的直播录制转点播实例。
- 已开通腾讯云直播和云点播服务。若未开通，请前往开通 [云直播服务](https://console.cloud.tencent.com/live/livestat) 和 [云点播服务](https://console.cloud.tencent.com/vod/overview)。

## 实践步骤
### 步骤1：创建录制模板
使用录制功能需要先创建录制模板，直播录制功能的配置均保存在录制模板中。通过创建不同配置的录制模板，可以实现不同格式、不同录制文件时长等效果。
- **通过控制台创建**：
   1. 进入 [云直播控制台](https://console.cloud.tencent.com/live/config/record) ，选择**功能配置**> [**直播录制**](https://console.cloud.tencent.com/live/config/record)。
![](https://qcloudimg.tencent-cloud.cn/raw/2c70d96915ff91297434a1415aea49d0.png)

   2. 单击**创建录制模板**，选择需要的录制文件类型（至少选择一种格式）。更多配置项描述请参见 [创建录制模板](https://intl.cloud.tencent.com/document/product/267/34223)。
	![](https://qcloudimg.tencent-cloud.cn/raw/af659794c5324cec4ed060377d74f04b.png)
		
   3. 单击**保存**即可成功创建模板。
- **通过 API 创建**：
调用 [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845) 接口创建录制模板，模板创建成功后会返回对应的模板 ID。

### 步骤2：选择录制方案
云直播根据不同的场景，提供了以下几种调用直播录制功能的方案：

#### 方案一：指定域名全局录制
通过 [云直播控制台](https://console.cloud.tencent.com/live/config/record) 或者调用 API，将直播录制模板绑定到推流域名，只要通过该域名推流就会自动进行录制。

- **适用场景**：秀场直播、电商直播、在线课堂、视频监控等全录制场景。
- **操作流程**：
	1. 在创建录制模板成功后，将有弹框提醒您 [绑定域名](https://console.cloud.tencent.com/live/config/record)，单击**去绑定域名**并选择推流域名即可。
![](https://qcloudimg.tencent-cloud.cn/raw/5286148ae522898575744fe54b16938a.png)

   2. 在 [**域名管理**](https://console.cloud.tencent.com/live/domainmanage)中，单击您的 [直播推流域名](https://console.cloud.tencent.com/live/domainmanage) 将会跳转到推流详情页，选择**模板配置**>**录制配置**，单击**编辑**即可绑定您的推流域名。详情请参见 [关联录制模板](https://intl.cloud.tencent.com/document/product/267/34224)。
![](https://qcloudimg.tencent-cloud.cn/raw/c74c5d420b6ed296859532e887541e7c.png)

   3. 通过 [CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846) 接口传入录制模板的模板 ID 和推流域名，即可完成录制模板绑定推流域名。

#### 方案二：指定单个流录制
通过 API 将直播录制模板绑定到某个指定的直播流，从而实现录制某个直播流。

- **适用场景**：活动直播、展会直播、赛事直播、连麦直播等单个活动特殊录制场景。
- **操作流程**：通过 [CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846) 接口创建录制规则，传入录制模板的模板 ID 和需要绑定的域名、路径和流名称 StreamName（需精准匹配），即可完成录制模板绑定指定直播流。

#### 方案三：按指定时间段录制
您可以通过调用 API 控制录制的开始与结束时间，在指定的时间内触发录制任务进行录制。

- **适用场景**：新闻直播、活动直播等有直播流程比较明确的录制场景。
- **操作流程**：通过 [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) 接口创建录制任务，指定录制模板的模板 ID 和需要绑定的域名、路径和流名称 StreamName（需精准匹配），设置需要进行录制的开始和结束时间，则到达开始时间时即开始录制。
- **录制示例**：
 1. 最简单的情况，只需填写指定的 StreamName、DomainName、AppName 和 EndTime 参数。
例如：创建了2020年08月10日早上08点到10点的录制任务，格式为 FLV，视频录制，分片间隔30分钟，永久存储。
输入示例：
```
https://live.tencentcloudapi.com/?Action=CreateRecordTask&AppName=live&DomainName=mytest.live.push.com&StreamName=livetest&StartTime=1597017600&EndTime=1597024800&TemplateId=0&<公共请求参数>
```
 2. 您还可以指定具体录制格式、录制类型以及存储参数等。
例如：创建了2020年08月10日早上08点到10点的录制任务，格式为 MP4，分片间隔1小时，永久存储。
 3. 调用 [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845) ，先创建录制模板。
 输入示例：
 ```
 https://live.tencentcloudapi.com/?Action=CreateLiveRecordTemplate&TemplateName=templat&Description=test&Mp4Param.Enable=1&Mp4Param.RecordInterval=3600&Mp4Param.StorageTime=0&<公共请求参数>
 ```
 输出示例：
 ```
 {"Response": {"RequestId": "839d12da-95a9-43b2-a9a0-03366d01b532","TemplateId": 17016}}
 ```
 4. 调用 [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309)，创建录制任务。
 输入示例：
 ```
 https://live.tencentcloudapi.com/?Action=CreateRecordTask&StreamName=livetest&AppName=live&DomainName=mytest.live.push.com&StartTime=1597017600&EndTime=1597024800&TemplateId=17016&<公共请求参数>
 ```

#### 方案四：精彩片段录制（支持录制混流直播）
在直播过程中碰到精彩画面，可以通过调用 API 实时进行直播录制。

- **适用场景**：赛事直播、游戏直播等只需要录制部分片段的场景（或者通过全局录制后再进行剪辑）。
- **操作流程**：通过 [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) 接口创建录制任务，指定录制模板的模板 ID 和需要绑定的域名、路径和流名称 StreamName（需精准匹配），设置需要进行录制的结束时间，创建成功后即开始录制任务。
- **录制示例**：
 ```
 https://live.tencentcloudapi.com/?Action=CreateRecordTask&StreamName=test&AppName=live&DomainName=mytest.live.push.com&EndTime=1597024800&<公共请求参数>
 ```

#### 方案五：录制纯音频
若推流为纯音频，您可以配置 AAC 纯音频录制。

- **适用场景**：音频直播、音频连麦等场景。
- **操作流程**：创建录制模板时，选择录制文件类型为 ACC 纯音频录制，并关联对应的推流地址即可。
>!创建绑定规则后约5 - 10分钟生效，绑定规则的修改不影响正在推流的直播，只对新推的直播流生效。

### 步骤3：开始直播推流
根据 [步骤2](#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E9.80.89.E6.8B.A9.E5.BD.95.E5.88.B6.E6.96.B9.E6.A1.88) 将录制模板绑定推流域名后，通过该推流地址生成对应的推流域名并进行 [直播推流](https://intl.cloud.tencent.com/document/product/267/31558)。

当直播结束后，录制生成的文件会存储到 [云点播](https://console.cloud.tencent.com/vod/overview) 平台。

>?
>- 若录制模板中选择录制至子应用，则存储到对应子应用下。
>- 若需要回调录制文件地址信息，需要在推流前创建回调模板，填写录制回调地址后保存，并绑定需要回调的推流域名，详情请参见 [录制事件通知](https://intl.cloud.tencent.com/document/product/267/38082)。

### 步骤4：获取录制文件
支持通过以下方式可查询、获取录制文件：
- **通过录制回调获取**：在直播推流前配置好回调模板（模板需要 [配置录制回调地址](https://console.cloud.tencent.com/live/config/callback)），生成录制文件时会通过回调将文件发给回调服务器。更多详情请参见 [录制事件通知](https://intl.cloud.tencent.com/document/product/267/38082)。
![](https://qcloudimg.tencent-cloud.cn/raw/137836f99132f0619ca4ccb6ca128fed.png)
- **通过云点播控制台获取**：在 [云点播控制台](https://console.cloud.tencent.com/vod/media) 进行查询，具体请参见 [查看视频](https://intl.cloud.tencent.com/document/product/266/33895)。
- **通过云点播 API 获取**：调用 [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179) 接口进行文件查询。

### 步骤5：处理录制文件
#### 方案一：直播录制 + 自动转码 + 视频加速播放
- **适用场景**：直播录制后快速将录制文件自动进行转码和视频加速，供用户进行点播播放，适用于大部分不需要视频二次加工的直播场景。
- **操作流程**：
	1. 直播推流录制前先创建录制模板，单击**高级配置**进行任务流的配置。
	![](https://qcloudimg.tencent-cloud.cn/raw/643aa06605824bab31016d95a5607099.png)
	2. 绑定预先在云点播控制台创建的任务流模板。
	![](https://qcloudimg.tencent-cloud.cn/raw/f2c1fdb36cee77be20e9fa366b1994ca.png)
	3. 客户进行直播推流，具体可参见 [直播推流](https://intl.cloud.tencent.com/document/product/267/31558)。
	4. 直播录制完成后，获取点播 FileId。
	![](https://qcloudimg.tencent-cloud.cn/raw/8a70ec2190bde5eb95401ad27b71f9fa.png)
	5. 获取播放地址进行播放。

#### 方案二：直播录制 + 手动转码 + 视频加速播放
- **适用场景**：部分用户希望将直播录制的视频仅先存储到点播，且先不进行后续的转码操作，则可在新建录制到点播时，不添加其他操作。如果后续希望对视频进行转码，则可进行手动触发转码操作。同时，可配合点播云剪辑功能进行使用，效果更佳。

- **操作流程**：
	1. 客户进行直播推流，具体可参见 [直播推流](https://intl.cloud.tencent.com/document/product/267/31558)。
	2. 文件自动录制到点播。
	3. 获取点播 FileId。
	4. 配置转码模板，或者任务流进行手动转码，具体可参见 [模板设置](https://intl.cloud.tencent.com/document/product/266/14059)。
![](https://qcloudimg.tencent-cloud.cn/raw/fef42635495040b17e98868ad9cd911a.png)
	5. 客户可择需进行视频二次剪辑。
	6. 转码和处理完成后获取视频地址进行后续播放。

#### 方案三：直播录制 + 自适应码流 + 视频加速 + 超级播放器

- **适用场景**：部分用户对视频安全有极高的诉求，普调的 HLS 加密无法满足加密诉求，通过自适应和超级播放器的组合使用，可以有效完成视频安全升级，对在线教育、企业培训类客户场景适配度很高。

- **操作流程**：
	1. 客户进行直播推流，具体可参见 [直播推流](https://intl.cloud.tencent.com/document/product/267/31558)。
	2. 文件自动录制到点播。
	3. 获取点播 FileId。
	4. 配置任务流转出自适应码流，具体可参见 [任务流设置](https://intl.cloud.tencent.com/document/product/266/14058)。
	![](https://qcloudimg.tencent-cloud.cn/raw/461b55df5d688b52d94210f173368ddc.png)
	5. 设置超级播放配置，选择所创建的用于播放的自适应码流。
		![](https://qcloudimg.tencent-cloud.cn/raw/4fe2cb6836caad6861798bc38cde60cd.png)
	6. 通过 FileId 进行视频的播放。

