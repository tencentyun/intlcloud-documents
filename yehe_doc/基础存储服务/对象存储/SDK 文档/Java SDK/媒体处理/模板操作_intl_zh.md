
## 简介

本文档提供关于数据万象媒体处理任务的相关 API 概览以及 SDK 示例代码,此处以动图任务举例。

| API                                                          | 操作名             | 操作描述                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/43631) | 创建模板 | 用于创建一个新的模板 |
| [DeleteMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/43673) | 删除模板 | 删除一个模板|
| [DescribeMediaTemplates](https://intl.cloud.tencent.com/document/product/1045/43673) | 查询模板 | 查询模板列表 |
| [UpdateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/43673) | 修改模板 | 修改一个模板 |

## 基本操作

### 创建模板

#### 功能说明

用于创建一个新的模板。

#### 方法原型

```java
public MediaTemplateResponse createMediaTemplate(MediaTemplateRequest request);
```

#### 参数说明

Request 的具体参数描述如下：

| 节点名称（关键字） | 父节点  | 描述                                                     | 类型      | 必选 |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | 模板类型：Animation 动图，Snapshot 截图，<br/>Transcode 转码，Watermark 水印，SmartCover 智能封面 | String    | 是   |
| Name               | Request | 模板名称仅支持中文、英文、数字、_、-和*                    | String    | 是   |
| Container          | Request | 容器格式                                               | Container | 是   |
| Video              | Request | 视频信息                                               | Container | 否   |
| TimeInterval       | Request | 时间区间                                               | Container | 否   |
| Snapshot           | Request | 截图                                               | Container | 否   |
| Watermark          | Request | 水印                                               | Container | 否   |
| Audio              | Request | 音频信息                                               | Container | 否   |
| TransConfig        | Request | 转码配置                                               | Container | 否   |

Request 节点 Container 的具体数据描述如下：

| 节点名称（关键字） | 父节点  | 描述                                                     | 类型      | 必选 |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Format                | Request.Container | 容器格式：gif，hgif，webp  hgif 为高质量 gif，即清晰度比较高的 gif 格式图 | String    | 是   |

Request 节点 Video 的具体数据描述如下：

| 节点名称（关键字）         | 父节点        | 描述                  | 类型   | 必选 | 默认值       | 限制                                                         |
| -------------------------- | ------------- | --------------------- | ------ | ---- | ------------ | ------------------------------------------------------------ |
| Codec                      | Request.Video | 编解码格式            | String | 是   |  无  | gif、webp                                          |
| Width                      | Request.Video | 宽                    | String | 否   | 视频原始宽度 |  <li>值范围：[128，4096]<br/><li>单位：px<br/><li>若只设置 Width 时，按照视频原始比例计算 Height |
| Height                     | Request.Video | 高                    | String | 否   | 视频原始高度 | <li>值范围：[128，4096]<br/><li>单位：px<br/><li>若只设置 Height 时，按照视频原始比例计算 Width |
| Fps                        | Request.Video | 帧率                  | String | 否   | 视频原始帧率 | <li>值范围：(0，60]<br/><li>单位：fps<br/><li>如果不设置，那么播放速度按照原来的时间戳。这里设置 fps 为动图的播放帧率。 |
| AnimateOnly<br/>KeepKeyFrame    | Request.Video | 动图只保留关键帧      | String | 否   |      无        | <li>true、false<br/><li>动图保留关键帧参数                     |
| AnimateTime<br/>IntervalOfFrame | Request.Video | 动图抽帧间隔时间      | String | 否   |      无        | <li>（0，视频时长]<br/><li>动图抽帧时间间隔<br/><li>若设置 TimeInterval.Duration，则小于该值 |
| AnimateFrames<br/>PerSecond     | Request.Video | Animation 每秒抽帧帧数 | String | 否   |     无         | <li>（0，视频帧率)<br/><li>动图抽帧频率<br/><li>优先级：AnimateFrames<br/>PerSecond >  AnimateOnlyKeepKeyFrame  > AnimateTimeIntervalOfFrame |
| Quality                    | Request.Video | 设置相对质量          | String | 否   |     无         | <li>[1, 100)<br/><li>webp 图像质量设定生效，gif 没有质量参数 |


Request 节点 TimeInterval 的具体数据描述如下：

| 节点名称（关键字） | 父节点  | 描述                                                     | 类型      | 必选 | 默认值       | 限制  |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Start                | Request.TimeInterval | 开始时间 | String    | 否   | 0 | <li>[0 视频时长] <br/><li>单位为秒 <br/><li>支持 float 格式，执行精度精确到毫秒 |
| Duration             | Request.TimeInterval | 持续时间 | String    | 否   | 视频时长 | <li> [0 视频时长] <br/><li>单位为秒 <br/><li>支持 float 格式，执行精度精确到毫秒 |

Container 类型 Snapshot 的具体数据描述如下：

| 节点名称（关键字） | 父节点  | 描述                                                     | 类型      | 必选 | 默认值       | 限制  |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Mode                | Request.Snapshot | 截图模式 | String    | 是   | Interval | <li>值范围：{Interval, Average}<br/><li>Interval 表示间隔模式 Average 表示平均模式<br/><li> Interval 模式：Start，TimeInterval，Count 参数生效。当设置 Count，未设置 TimeInterval 时，表示截取所有帧，共 Count 张图片<br/><li>Average 模式：Start，Count 参数生效。表示从 Start 开始到视频结束，按平均间隔截取共 Count 张图片|
| Start                | Request.Snapshot | 开始时间 | String    | 是   | 0 | <li>[0 视频时长] <br/><li>单位为秒 <br/><li>支持 float 格式，执行精度精确到毫秒 |
| TimeInterval         | Request.Snapshot | 截图频率 | String    | 否   | 无  | <li>(0 3600] <br/><li>单位为秒 <br/><li>支持 float 格式，执行精度精确到毫秒 |
| Count                | Request.Snapshot | 截图数量 | String    | 是   | 无  | (0 10000] |
| Width                | Request.Snapshot | 宽 | String    | 否   |  视频原始宽度 | <li>值范围：[128，4096]<br/><li>单位：px<br/><li>若只设置 Width 时，按照视频原始比例计算 Height<br/> |
| Height                | Request.Snapshot | 高 | String    | 否  | 视频原始高度  | <li>值范围：[128，4096]<br/><li>单位：px<br/><li>若只设置 Height 时，按照视频原始比例计算Width<br/> |

Container 类型 Watermark 的具体数据描述如下：

| 节点名称（关键字）     | 父节点  | 描述                                                     | 类型      | 必选 | 默认值       | 限制  |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Type                | Request.Watermark | 水印类型    | String    | 是   | 无  | Text：文字水印、 Image：图片水印 |
| Pos                 | Request.Watermark | 基准位置    | String    | 是   | 无  | TopRight、TopLeft、BottomRight、 BottomLeft |
| LocMode             | Request.Watermark | 偏移方式    | String    | 是   | 无  | Relativity：按比例、 <br/>Absolute：固定位置 |
| Dx                  | Request.Watermark | 水平偏移    | String    | 是   | 无  | <li>当 locMode 为 Relativity 时，<br/>单位为%，取值范围[0 100] <br/><li>当 locMode 为 Absolute 时，<br/>单位为px，取值范围[0 4096] |
| Dy                  | Request.Watermark | 垂直偏移    | String    | 是   | 无  | <li>当 locMode 为 Relativity 时，<br/>单位为%，取值范围[0 100] <br/><li>当 locMode 为 Absolute 时，<br/>单位为px，取值范围[0 4096]|
| StartTime           | Request.Watermark | 水印开始时间 | String    | 否   | 0   | <li>[0 视频时长] <br/><li>单位为秒 <br/><li>支持 float 格式，执行精度精确到毫秒 |
| EndTime             | Request.Watermark | 水印结束时间 | String    | 否   | 视频结束时间  | <li>[0 视频时长] <br/><li>单位为秒 <br/><li>支持 float 格式，执行精度精确到毫秒 |
| Image               | Request.Watermark | 图片水印节点 | Container    | 否   | 无  | 无 |
| Text                | Request.Watermark | 文本水印节点 | Container    | 否   | 无  | 无 |


Container 类型 Image 的具体数据描述如下：

| 节点名称（关键字）     | 父节点  | 描述                                                     | 类型      | 必选 | 默认值       | 限制  |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Url                 | Request.Watermark.Image | 水印图地址   | String    | 是   | 无  | 同 bucket 的水印图片地址 |
| Mode                 | Request.Watermark.Image | 尺寸模式    | String    | 是   | 无   | <li>Original：原有尺寸 <br/><li>Proportion：按比例 <br/><li>Fixed：固定大小 |
| Width                | Request.Watermark.Image | 宽         | String    | 否   | 无   | <li>当 Mode 为 Original，水印图宽 <br/><li>当 Mode 为 Proportion，单位为%，取值范围：[1 100]<br/><li>当 Mode 为 Fixed，单位为px，取值范围：[1，4096]<br/><li>若只设置 Width 时，按照视频原始比例计算 Height<br/> |
| Height               | Request.Watermark.Image | 高         | String    | 否   | 无   | <li>当 Mode 为 Original，水印图高 <br/><li>当 Mode 为 Proportion，单位为%，取值范围：[1 100]<br/><li>当 Mode 为 Fixed，单位为px，取值范围：[1，4096]<br/><li>若只设置 Height 时，按照视频原始比例计算 Width|
| Transparency         | Request.Watermark.Image | 透明度      | String    | 是   | 无   | 值范围：[1 100]，单位% |

水印位置说明：
![image.png](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

Container 类型 Text 的具体数据描述如下：

| 节点名称（关键字）     | 父节点  | 描述                                                     | 类型      | 必选 | 默认值       | 限制  |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| FontSize            | Request.Watermark.Text | 字体大小    | String    | 是   | 无  |值范围：[5 100]，单位为px |
| FontType            | Request.Watermark.Text | 字体类型    | String    | 是   | 无  | 参考下表  |
| FontColor           | Request.Watermark.Text | 字体颜色    | String    | 是   | 无  | 格式：0xRRGGBB |
| Transparency        | Request.Watermark.Text | 透明度      | String    | 是   | 无  | 值范围：[1 100]，单位为%|
| Text                | Request.Watermark.Text | 水印内容    | String    | 是   | 无  | 长度不超过64个字符，仅支持中文、英文、数字、_、-和*|


Text 的 FontType 具体数据描述如下：

| 字体名称               | 支持的语言             | 描述
| ------------------     | -------                | ------
| simfang.ttf            |  中/英                 | 仿宋
| simhei.ttf             |  中/英                 | 黑体
| simkai.ttf             |  中/英                 | 楷体
| simsun.ttc             |  中/英                 | 宋体
| STHeiti-Light.ttc      |  中/英                 | 华文黑体
| STHeiti-Medium.ttc     |  中/英                 | 华文黑体中
| youyuan.TTF            |  中/英                 | 幼圆
| ariblk.ttf             |  英                    | 无
| arial.ttf              |  英                    | 无
| ahronbd.ttf            |  英                    | 无
| Helvetica.dfont        |  英                    | 无
| HelveticaNeue.dfont    |  英                    | 无

Audio 音频视频支持的格式如下表：

| Container                  | Audio Codecs  | Video Codecs          |
| -------------------------- | ------------- | --------------------- |
| flv/mp4/ts/hls             | AAC、MP3      | H.264                 |
| aac                        | aac           | 不支持                |
| mp3                        | mp3           | 不支持                |

Audio 的具体数据描述如下：

| 节点名称（关键字） | 父节点        | 描述           | 类型   | 必选 | 默认值 | 限制                                                         |
| ------------------ | ------------- | -------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| Codec              | Request.Audio | 编解码格式     | String | 否   | aac    | 取值 aac、mp3                                                |
| Samplerate         | Request.Audio | 采样率         | String | 否   | 44100  | <li>单位：Hz<br/><li>可选 11025、22050、32000、44100、48000、96000<br/><li>不同的封装，mp3 支持不同的采样率，如下表所示|
| Bitrate            | Request.Audio | 原始音频码率   | String | 否   | 无    | <li>单位：Kbps<br/><li>值范围：[8，1000]                       |
| Channels           | Request.Audio | 声道数         | String | 否   | 无      | <li>当 Codec 设置为 aac，支持1、2、4、5、6、8<br/><li>当 Codec 设置为 mp3，支持1、2 |
| Remove             | Request.Audio | 是否删除音频流 | String | 否   | false    | 取值 true、false     |


Y表示支持这种采样率，N表示不支持

| 封装格式/音频采样率| 	11025  | 	22050| 	 32000 | 	44100|  	48000|   	96000 |
| ------------------ | ------- | ------- | ------- | ------- |------------| ------------- |
| flv	             | Y       | 	Y| 	N| 	Y| 	N| 	N|
| mp4                | N       | 	Y| 	Y| 	Y| 	Y| 	N|
| avi/hls/ts/mp3     | Y       | 	Y| 	Y| 	Y| 	Y| 	N|


TransConfig 的具体数据描述如下：

| 节点名称（关键字）    | 父节点              | 描述             | 类型   | 必选 | 默认值 | 限制                                                         |
| --------------------- | ------------------- | ---------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| AdjDarMethod          | Request.TransConfig | 分辨率调整方式   | String | 否   | none   | <li>取值 scale、crop、pad、none<br/><li>当输出视频的宽高比与原视频不等时，需要此参数进行执行调整方式 |
| IsCheckReso           | Request.TransConfig | 是否检查分辨率   | String | 否   | false  | <li>true、false <br/><li>当为 false 时，按照配置参数转码 |
| ResoAdjMethod         | Request.TransConfig | 分辨率调整方式   | String | 否   | 0      | <li>取值0、1；0 表示使用原视频分辨率；1表示返回转码失败<br/><li>当 IsCheckReso 为 true 时生效 |
| IsCheckVideoBitrate   | Request.TransConfig | 是否检查视频码率 | String | 否   | false  | <li>true、false <br/><li>当为 false 时，按照配置参数转码 |
| VideoBitrateAdjMethod | Request.TransConfig | 视频码率调整方式 | String | 否   | 0      | <li>取值0、1；0 表示使用原视频码率；1表示返回转码失败<br/><li>当 IsCheckVideoBitrate 为 true 时生效 |
| IsCheckAudioBitrate   | Request.TransConfig | 是否检查音频码率 | String | 否   | false  | <li>true、false <br/><li>当为 false 时，按照配置参数转码<br/> |
| AudioBitrateAdjMethod | Request.TransConfig | 音频码率调整方式 | String | 否   | 0      | <li>取值0、1；0 表示使用原音频码率；1表示返回转码失败<br/><li>当 IsCheckAudioBitrate 为 true 时生效 |


Video 的具体数据描述如下：

| 节点名称（关键字）         | 父节点        | 描述                  | 类型   | 必选 | 默认值       | 限制                                                         |
| -------------------------- | ------------- | --------------------- | ------ | ---- | ------------ | ------------------------------------------------------------ |
| Codec                      | Request.Video | 编解码格式            | String | 否   |   H.264 |  H.264                                          |
| Width                      | Request.Video | 宽                    | String | 否   | 视频原始宽度 | <li>值范围：[128，4096]<br/><li>单位：px<br/><li>若只设置 Width 时，按照视频原始比例计算 Height |
| Height                     | Request.Video | 高                    | String | 否   | 视频原始高度 | <li>值范围：[128，4096]<br/><li>单位：px<br/><li>若只设置 Height 时，按照视频原始比例计算 Width |
| Fps                        | Request.Video | 帧率                  | String | 否   | 无 | <li>值范围：(0，60]<br><li>单位：fps |
| Remove                     | Request.Video | 是否删除视频流        | String | 否   | false        | true、false                                               |
| Profile                    | Request.Video | 编码级别              | String | 否   | high         | <li>支持 baseline、main、high<br/><li>baseline：适合移动设备<br/><li>main：适合标准分辨率设备<br/><li>high：适合高分辨率设备<br/><li>仅 H.264 支持此参数 |
| Bitrate                    | Request.Video | 视频输出文件的码率    | String | 否   |  无           | <li>值范围：[10，50000]<br/><li>单位：Kbps                     |
| Crf                        | Request.Video | 码率-质量控制因子     | String | 否   | 无           | <li>值范围：(0，51]<br/><li>如果设置了 Crf，则 Bitrate 的设置失效 |
| Gop                        | Request.Video | 关键帧间最大帧数      | String | 否   |  无            | 值范围：[0，100000]                                          |
| Preset                     | Request.Video | 视频算法器预置        | String | 否   | medium       | <li>仅 H.264 支持该参数<br/><li>取值 veryfast、fast、medium、slow、slower |
| Bufsize                    | Request.Video | 缓冲区大小            | String | 否   | 无            | <li>值范围：[1000，128000]<br/><li>单位：Kb<br/> |
| Maxrate                    | Request.Video | 视频码率峰值          | String | 否   | 无            | <li>值范围：[10，50000]<br/><li>单位：Kbps<br/> |
| HlsTsTime                  | Request.Video | hls分片时间           | String | 否   | 5            | <li>(0 视频时长] <br/><li>单位为秒 |
| Pixfmt                     | Request.Video | 视频颜色格式           | String | 否   | 无           | 支持 yuv420p、yuv422p、yuv444p、yuvj420p、yuvj422p、yuvj444p |




#### 返回结果说明

- 成功：返回 MediaTemplateResponse 对象响应信息，内含创建的模板详情。
- 失败：发生错误（如 Bucket 不存在），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 请求示例

```java
//1.创建模板请求对象
MediaTemplateRequest request = new MediaTemplateRequest();
//2.添加请求参数 参数详情请见api接口文档
request.setBucketName("examplebucket-1250000000");
request.setTag("Animation");
request.setName("TestTemplate40");
request.getContainer().setFormat("gif");
request.getVideo().setCodec("gif");
request.getVideo().setWidth("1280");
request.getVideo().setFps("15");
request.getVideo().setAnimateOnlyKeepKeyFrame("true");
request.getTimeInterval().setStart("0");
request.getTimeInterval().setDuration("60");
//3.调用接口,获取模板响应对象
MediaTemplateResponse response = client.createMediaTemplate(request);
```

### 删除模板

#### 功能说明
删除一个模板
#### 方法原型

```java
public Boolean deleteMediaTemplate(MediaTemplateRequest request);
```

#### 参数说明

| 参数名称   | 描述                                                         | 类型   | 必选|
| ---------- | ------------------------------------------------------------ | ------ |-----|
| bucketName | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |是|
| templateId | 要取消的模板 id | String | 是 |

#### 返回结果说明

- 成功： 返回一个布尔类型，删除成功则返回 true。
- 失败： 发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 请求示例

```java
MediaTemplateRequest request = new MediaTemplateRequest();
request.setBucketName("examplebucket-1250000000");
request.setTemplateId("t19c4a60ae1a694621a01f0c7130c*****");
Boolean response = client.deleteMediaTemplate(request);
```

### 查询模板列表

#### 功能说明
查询模板列表
#### 方法原型

```java
public MediaJobResponse describeMediaJob(MediaJobsRequest req);
```

#### 参数说明

|参数名称 |描述    |   类型    |   必选    |
|:---           |:--                    |   :--     |   :--    |
| bucketName | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |是|
| tag       | 模板 Tag： Animation 动图，Snapshot 截图，Transcode 转码，Watermark 水印，SmartCover 智能封面| String |是|
| category  | Official，Custom，默认值：Custom | String  |否|
| ids       | 模板 ID，以`,`符号分割字符串  | String     |否|
| name      | 模板名称前缀              | String     |否|
| pageNumber| 第几页                   | Integer     |否|
| pageSize  | 每页个数                 | Integer     |否|


#### 返回结果说明

- 成功： 返回模板响应包装类，其中包含模板详情集合 templateList。 
- 失败： 发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 请求示例

```java
//1.创建任务请求对象
MediaTemplateRequest request = new MediaTemplateRequest();
request.setBucketName("examplebucket-1250000000");
MediaListTemplateResponse response = client.describeMediaTemplates(request);
List<MediaTemplateObject> templateList = response.getTemplateList();
```

### 修改模板

#### 功能说明
修改模板
#### 方法原型

```java
public Boolean updateMediaTemplate(MediaTemplateRequest request);   
```

#### 参数说明

|节点名称（关键字|描述|类型|必选|
|:---|:--|:--|:--|
| bucketName|Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |是|
| templateId|修改的模板 ID|String|是|

>?其余参数请参见创建模板接口，与其参数一致

#### 返回结果说明

- 成功： 修改成功则返回 true。
- 失败： 发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 请求示例

```java
MediaTemplateRequest request = new MediaTemplateRequest();
request.setBucketName("examplebucket-1250000000");
request.setTemplateId("t19c4a60ae1a694621a01f0c7130*****");
request.setTag("Animation");
request.setName("updateName");
request.getContainer().setFormat("gif");
Boolean aBoolean = client.updateMediaTemplate(request);
```
