## 1. 接口描述

接口请求域名： vod.tencentcloudapi.com 。

对 HLS 视频进行按时间段裁剪。

注意：裁剪出来的视频与原始视频共用 ts，仅生成新的 m3u8。原始视频删除后，该裁剪视频也会被删除。

默认接口请求频率限制：100次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见[公共请求参数](/document/api/266/31756)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：SimpleHlsClip |
| Version | 是 | String | 公共参数，本接口取值：2018-07-17 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| Url | 是 | String | 需要裁剪的腾讯云点播 HLS 视频 URL。 |
| StartTimeOffset | 否 | Float | 裁剪的开始偏移时间，单位秒。默认 0，即从视频开头开始裁剪。负数表示距离视频结束多少秒开始裁剪。比如 -10 表示从倒数第 10 秒开始裁剪。 |
| EndTimeOffset | 否 | Float | 裁剪的结束偏移时间，单位秒。默认 0，即裁剪到视频尾部。负数表示距离视频结束多少秒结束裁剪。比如 -10 表示到倒数第 10 秒结束裁剪。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| Url | String | 裁剪后的视频地址。|
| MetaData | [MediaMetaData](/document/api/266/31773#MediaMetaData) | 裁剪后的视频元信息。目前`Size`，`Rotate`，`VideoDuration`，`AudioDuration` 几个字段暂时缺省，没有真实数据。|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 裁剪 HLS 视频（时间偏移量均为正数）

裁剪视频第 2 秒到 第 10 秒

#### 输入示例

```
https://vod.tencentcloudapi.com/?Action=SimpleHlsClip
&Url=http://xxxxx.vod2.myqcloud.com/xxxxx/aaaaaa/hhh.m3u8
&StartTimeOffset=2
&EndTimeOffset=10
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "Url": "http://xxxxx.vod2.myqcloud.com/xxxxx/aaaaaa/10_50.m3u8",
    "MetaData": {
      "Size": 0,
      "Container": "hls",
      "Bitrate": 622014,
      "Height": 480,
      "Width": 640,
      "Duration": 48,
      "Rotate": 0,
      "VideoStreamSet": [
        {
          "Bitrate": 592385,
          "Height": 480,
          "Width": 640,
          "Codec": "h264",
          "Fps": 25
        }
      ],
      "AudioStreamSet": [
        {
          "Bitrate": 29629,
          "SamplingRate": 44100,
          "Codec": "aac"
        }
      ],
      "VideoDuration": 0,
      "AudioDuration": 0
    },
    "RequestId": "12ae8d8e-dce3-4151-9d4b-5594145287e1"
  }
}
```

### 示例2 裁剪 HLS 视频（时间偏移量为负数）

裁剪第 2 秒开始到倒数第 10 秒

#### 输入示例

```
https://vod.tencentcloudapi.com/?Action=SimpleHlsClip
&Url=http://xxxxx.vod2.myqcloud.com/xxxxx/aaaaaa/hhhh.m3u8
&StartTimeOffset=2
&EndTimeOffset=-10
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "Url": "http://xxxxx.vod2.myqcloud.com/xxxxx/aaaaaa/10_50.m3u8",
    "MetaData": {
      "Size": 0,
      "Container": "hls",
      "Bitrate": 622014,
      "Height": 480,
      "Width": 640,
      "Duration": 48,
      "Rotate": 0,
      "VideoStreamSet": [
        {
          "Bitrate": 592385,
          "Height": 480,
          "Width": 640,
          "Codec": "h264",
          "Fps": 25
        }
      ],
      "AudioStreamSet": [
        {
          "Bitrate": 29629,
          "SamplingRate": 44100,
          "Codec": "aac"
        }
      ],
      "VideoDuration": 0,
      "AudioDuration": 0
    },
    "RequestId": "12ae8d8e-dce3-4151-9d4b-5594145287e1"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=SimpleHlsClip)

### SDK

云 API 3.0 提供了配套的开发工具集（SDK），支持多种编程语言，能更方便的调用 API。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### 命令行工具

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. 错误码

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见[公共错误码](/document/api/266/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| InternalError | 内部错误。 |
