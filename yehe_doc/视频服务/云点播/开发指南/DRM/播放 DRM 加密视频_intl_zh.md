## 学习目标

学习本阶段教程，您将了解并掌握如何对视频进行 DRM 加密，并使用自研播放器或第三方播放器播放加密后的视频。

>? 云点播的超级播放器 SDK （Android、iOS 和 Web 三端）预计将于5月中旬支持播放 DRM 加密视频，敬请期待。

##  前置条件
在开始本教程之前，请您确保已满足以下前置条件。

### 开通云点播
您需要开通云点播，步骤如下：

1. 注册 [腾讯云账号](https://intl.cloud.tencent.com/document/product/378/17985)，并完成 [实名认证](https://intl.cloud.tencent.com/document/product/378/3629)。
2. 购买云点播服务，具体请参见 [计费概述](https://intl.cloud.tencent.com/document/product/266/2838)。
3. 选择 **云产品**>**视频服务**>[**云点播**](https://console.cloud.tencent.com/vod)，进入云点播控制台。

至此，您已经完成了云点播的开通步骤。 

### 申请和提交 FairPlay 证书
请参考[如何申请和提交 FairPlay 证书](https://intl.cloud.tencent.com/document/product/266/46643)。FairPlay 证书提交成功后，您可以从控制台中查询得到证书 URL，用于后续播放使用。

## 步骤1：开启防盗链

以您账号下的默认分发域名开启 Key 防盗链为例：
>? 请避免直接对正在使用的现网域名开启防盗链，否则可能造成现网的视频无法播放。

1. 登录云点播控制台，选择【分发播放设置】>[【域名管理】](https://console.cloud.tencent.com/vod/distribute-play/domain)，单击“默认分发域名”的【设置】，进入设置页面。
2. 单击“Key 防盗链”右侧的【编辑】，打开【启用 Key 防盗链】，并单击【生成随机 Key】生成一个随机的 Key（2WExxx48eW），将生成好的 Key 复制下来，然后单击【确定】保存生效。防盗链 Key 可用于后续步骤中生成超级播放器签名。
   

## 步骤2：对视频进行 DRM 加密

1. 登录云点播控制台，选择 **媒资管理**>[**视频管理**](https://console.cloud.tencent.com/vod/media)，勾选要处理的视频（FileId 为528xxx3757278095），单击 **视频处理**。
2. 在视频处理界面：
 - **处理类型** 选择 **任务流**。
 - **任务流模板** 选择 **WidevineFairPlayPreset**。


>?
>- WidevineFairPlayPreset 是预置任务流：分别使用11、13模板转自适应码流，10模板截图做封面，10模板截雪碧图。
>- 11模板自适应码流是加密类型为 `FairPlay` 的多码率输出，13模板自适应码流是加密类型为 `Widevine` 的多码率输出。

3. 单击 **确定**，等待“视频状态”栏从“处理中”变为“正常”，表示视频已处理完毕：
4. 单击视频“操作”栏下的 **管理**，进入管理页面：
 - 选择“基本信息”页签，可以看到生成的封面，以及 DRM 加密的自适应码流输出（模板 ID 为11和13）。
 - 选择“截图信息”页签，可以看到生成的雪碧图（模板 ID 为10）。


##  步骤3：查询播放信息

由于超级播放器 SDK 尚未支持播放 DRM 加密视频，您可参照超级播放器 SDK 与点播后台的通信协议，查询播放信息，并使用自研播放器或第三方播放器播放 DRM 加密视频。下面将详细介绍超级播放器 SDK 与云点播后台的通信协议。

### 通信协议
请求以 HTTP GET 的方式发起，URL 为`https://{domain}/{interface}/{version}/{appId}/{fileId}?psign={psign}`。

#### 域名
- 主域名：`playvideo.qcloud.com`
- 备份域名：`bkplayvideo.qcloud.com`

#### 请求字段
##### Path 字段

| 字段含义  | 是否必填 | 字段取值                                                     |
| --------- | -------- | ------------------------------------------------------------ |
| appId     | 是       | 填写 appid（如果使用了子应用，则填写对应[子应用 id](https://intl.cloud.tencent.com/document/product/266/33987)）。 |
| fileId    | 是       | 要播放的视频文件 ID。                                        |
| version   | 是       | 固定填写 `v4`。                                                |
| interface | 是       | 固定填写 `getplayinfo`。                                       |

##### Query String 参数

| 字段含义 | 是否必填 | 字段取值                                                     |
| -------- | -------- | ------------------------------------------------------------ |
| psign    | 否       | 超级播放器签名，生成方式请参考 [超级播放器签名文档](https://intl.cloud.tencent.com/document/product/266/38099) 。超级播放器签名的 PayLoad 内容中需指定 `pcfg` 字段为 `advanceDrmPreset`。另外，云点播提供了[超级播放器 - 签名生成工具](https://vods.cloud.tencent.com/signature/super-player-sign.html) 页面，可用于快速生成超级播放器签名。 |
| context  | 否       | 透传字段，回包中原样带回。                                   |

##### 应答结构

| 参数名 | 类型 | 描述 |
| -- | -- | -- |
| code | Integer | 错误码，当 `code` 非0时表示错误。 |
| message | String | 错误信息，当 `code` 非0时此字段不为空。 |
| version | Integer | 当前返回的结果版本类型，取值固定为4。 |
| warning | String | 警告信息，如未开防盗链时携带 `psign` 参数，则返回警告。 |
| media | Object | 媒体信息，类型为 `Media` 。 |

##### Media 类型

| 参数名 | 类型 | 描述 |
| -- | -- | -- |
| basicInfo | Object | 视频基本信息，类型为 `BasicInfo` 。 |
| streamingInfo | Object | 多码率视频信息，类型为 `StreamingInfo` 。 |
| imageSpriteInfo | Object | 雪碧图信息，主要用于实现播放器对视频的预览，类型为 `ImageSpriteInfo` 。 |
| keyFrameDescInfo | Object | 视频打点信息，用于播放器在时间轴上的打点，类型为 `KeyFrameDescInfo` 。 |

##### BasicInfo 类型

| 参数名 | 类型 | 描述 |
| -- | -- | -- |
| name | String | 视频名称。 |
| size | Integer | 视频大小，单位：字节。 |
| duration | Float | 视频时长，单位：秒。 |
| description | String | 视频描述。 |
| coverUrl | String | 视频封面。 |

##### StreamingInfo 类型

| 参数名 | 类型 | 描述 |
| -- | -- | -- |
|drmOutput|Array|对视频做 DRM 加密后输出，类型为 `StreamingOutput`。 |
|drmToken|String|播放 DRM 加密输出时，使用的 DRM Token。 |
|widevineLicenseUrl|String|加密类型为 `Widevine` 的 License URL。 |
|fairplayLicenseUrl|String|加密类型为 `FairPlay` 的 License URL。 |

##### StreamingOutput 类型

| 参数名 | 类型 | 描述 |
| -- | -- | -- |
| type | String | 自适应码流保护类型，目前取值有 `plain`、`SimpleAES`、`Widevine`、`FairPlay`。`plain` 表示不加密，`SimpleAES` 表示 HLS 普通加密，`Widevine` 与 `FairPlay` 为 DRM 加密。 |
| url | String | 播放 URL。 |
| subStreams | Array | 子流信息，类型为 `SubStreamInfo`。 |

##### SubStreamInfo 类型

| 参数名 | 类型 | 描述 |
| -- | -- | -- |
| type | String | 子流的类型，目前可能的取值仅有 `video`。 |
| width | Integer | 子流视频的宽，单位：px。 |
| height | Integer | 子流视频的高，单位：px。 |
| resolutionName | String | 子流视频在播放器中展示的规格名。 |

##### ImageSpriteInfo 类型

| 参数名 | 类型 | 描述 |
| -- | -- | -- |
| imageUrls | Array | 雪碧图下载 URL 数组，类型为 `String` 。 |
| webVttUrl | String | 雪碧图 VTT 文件下载 URL 。 |

##### 示例

###### 请求示例

超级播放器签名的 PayLoad 如下：

```json
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "currentTimeStamp": 1546340400,
  "expireTimeStamp": 1546344000,
  "urlAccessInfo": {
    "t": "5c2b5640",
    "rlimit": 3,
    "us": "72d4cd1101"
  }
}
```

当 Key 为 `test`时，生成的超级播放器签名如下：

```json
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE1NDYzNDA0MDAsImV4cGlyZVRpbWVTdGFtcCI6MTU0NjM0NDAwMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNWMyYjU2NDAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSJ9fQ.aqH576UXfeUe90LlH6w1tt-N1UYrEoOtAYb1ljUT51M
```

那么，请求 URL 为：

```
https://playvideo.qcloud.com/getplayinfo/v4/1255566655/4564972818519602447?psign=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE1NDYzNDA0MDAsImV4cGlyZVRpbWVTdGFtcCI6MTU0NjM0NDAwMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNWMyYjU2NDAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSJ9fQ.s01u7fpYu0VkLBHG5e84JCgfnFGxRvrNHWQRCHWHhc0
```

##### 应答示例

```json
{
  "code": 0,
  "message": "",
  "requestId": "87cc5b712d7c402c8bb255b3777f8bf5",
  "version": 4,
  "context": "",
  "warning": "",
  "media": {
    "basicInfo": {
      "name": "drm demo",
      "size": 428106411,
      "duration": 90,
      "coverUrl": "https://xxx.vod2.myqcloud.com/xxx/xxx/coverBySnapshot/coverBySnapshot_10_0.jpg?t=7fffffff&sign=ea3197f995dae16457397d9a3c0ebc1c",
      "description": ""
    },
    "streamingInfo": {
      "drmOutput": [
        {
          "type": "Widevine",
          "url": "https://1500012293.vod2.myqcloud.com/xxx/xxx/adp.13.m3u8?t=7fffffff&sign=75152a4b4d10f32f4315783edf9944ed",
          "subStreams": [
            {
              "type": "video",
              "width": 426,
              "height": 240,
              "resolutionName": "FLU"
            },
            {
              "type": "video",
              "width": 852,
              "height": 480,
              "resolutionName": "SD"
            },
            {
              "type": "video",
              "width": 1280,
              "height": 720,
              "resolutionName": "HD"
            },
            {
              "type": "video",
              "width": 1920,
              "height": 1080,
              "resolutionName": "FHD"
            }
          ]
        },
        {
          "type": "FairPlay",
          "url": "https://1500012293.vod2.myqcloud.com/xxx/xxx/adp.11.m3u8?t=7fffffff&sign=75152a4b4d10f32f4315783edf9944ed",
          "subStreams": [
            {
              "type": "video",
              "width": 426,
              "height": 240,
              "resolutionName": "FLU"
            },
            {
              "type": "video",
              "width": 852,
              "height": 480,
              "resolutionName": "SD"
            },
            {
              "type": "video",
              "width": 1280,
              "height": 720,
              "resolutionName": "HD"
            },
            {
              "type": "video",
              "width": 1920,
              "height": 1080,
              "resolutionName": "FHD"
            }
          ]
        }
      ],
      "drmToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE2NTA1NDM3ODUsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywicmFuZG9tIjo0NzUyNDQzMTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~ebaFyERTuT8QMMN5iQ-lnVLs60LCUt1J_RmADdRiE_8",
      "widevineLicenseUrl": "https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2",
      "fairplayLicenseUrl": "https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2"
    },
    "audioVideoType": "AdaptiveDynamicStream",
    "originalInfo": null,
    "transcodeInfo": null
  }
}
```

#### 播放信息

从上述应答结构中，可以获取到以下播放信息：

1. DRM 加密视频的 URL。

2. 对应加密类型的许可证获取地址（License Server URL）。其中，许可证获取地址为`widevineLicenseUrl`或`fairplayLicenseUrl`拼接`drmToken`得到。

下面，我们来看一下示例中所获取到的播放信息。

对于`Widevine`加密：

- 加密视频 URL 为 `https://1500012293.vod2.myqcloud.com/xxx/xxx/adp.13.m3u8?t=7fffffff&sign=75152a4b4d10f32f4315783edf9944ed`
- 许可证获取地址（License Server URL）为`https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE2NTA1NDM3ODUsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywicmFuZG9tIjo0NzUyNDQzMTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~ebaFyERTuT8QMMN5iQ-lnVLs60LCUt1J_RmADdRiE_8`

对于`FairPlay`加密：

- 加密视频 URL 为 `https://1500012293.vod2.myqcloud.com/xxx/xxx/adp.11.m3u8?t=7fffffff&sign=75152a4b4d10f32f4315783edf9944ed`
- 许可证获取地址（License Server URL）为`https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE2NTA1NDM3ODUsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywicmFuZG9tIjo0NzUyNDQzMTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~ebaFyERTuT8QMMN5iQ-lnVLs60LCUt1J_RmADdRiE_8`


## 步骤4：使用播放器播放 DRM 加密视频。

### 方案一 使用点播超级播放器播放
点播超级播放器集成了播放 DRM 加密视频的功能，使用方法说明如下:


#### step 1：在页面中引入文件
在适当的地方引入播放器样式文件与相关脚本文件：

```
 <link href="//imgcache.qq.com/open/qcloud/video/tcplayer/tcplayer.css" rel="stylesheet">
 <script src="//imgcache.qq.com/open/qcloud/video/tcplayer/libs/hls.min.0.12.4.js"></script>
 <script src="//imgcache.qq.com/open/qcloud/video/tcplayer/libs/dash.all.min.2.9.3.js"></script>
 <script src="//imgcache.qq.com/open/qcloud/video/tcplayer/tcplayer.min.js"></script>
```

#### step 2：放置播放器容器
在需要展示播放器的页面位置加入播放器容器，例如：在 index.html 中加入如下代码（容器 ID 以及宽高都可以自定义）。

```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

#### step 3：初始化代码
在页面初始化的代码中加入以下初始化脚本，传入必须的初始化参数

```
var player = TCPlayer('player-container-id', {
  appID:  '', // 请传入点播账号的 appID 必须
  fileID: '', // 请传入需要播放的视频 filID 必须
  psign: '', // 请传入播放器配置签名
  plugins: {
    DRM: {
      certificateUri: '', // 使用 FairPlay 方案需要用到的证书地址，播放 FairPlay 加密内容必须
    }
  }``
});
```


>?
>- 如果需要使用 FairPlay 方案，还需要传入 FairPlay 证书
>- certificateUri 为 FairPlay 播放方案要求的证书地址，生成证书后，将该证书部署到您的服务器下，然后获得证书的地址。
>- 商业级 DRM 内容只能在 HTTPS 协议下的页面进行播放


### 方案二 使用第三方播放器（Shaka Player）播放  

使用第三方播放器也可以播放 DRM 加密视频，您需要请求云点播后台的通信协议，获取加密配置信息，并在初始化播放器过程中传入配置信息，即可播放。详情可以查阅 [Shaka player](https://github.com/shaka-project/shaka-player)。


#### step 1：在页面中引入文件
在适当的地方引入播放器脚本文件，可以通过 [npm](https://www.npmjs.com/package/shaka-player) 或者 cdn 引用脚本文件。

```
// cdn 方式引用
<script src="path/to/shaka-player.compiled.js" ></script>
```

#### step 2：放置播放器容器
在需要展示播放器的页面位置加入播放器容器，例如：在 index.html 中加入如下代码（容器 ID 以及宽高都可以自定义）。

```
  <video id="video" width="640" controls autoplay></video>
```

#### step 3：初始化代码
在页面初始化的代码中加入以下初始化脚本，传入必须的初始化参数

```
var manifestUri = 'https://1500003943.vod2.myqcloud.com/43832a63vodtranscq1500003943/06981c16387702298107746523/adp.1368258.m3u8';

function initPlayer() {
	// Create a Player instance.
	var video = document.getElementById('video');
	var player = new shaka.Player(video);

	player.configure({
	    drm: {
	      servers: {
	        'com.widevine.alpha': 'https://drm.vod2.myqcloud.com/getlicense/v1?drmType=Widevine&token=bJ%2FE5%2Bmc5atzwHKci%2Fh2IPDoON9TZWNyZXRJZD1BS0lETmNmcnZwVURrQTNxVzVoNVJ0SWV2RlVoRXdjQ21FaDUmQ3VycmVudFRpbWVTdGFtcD0xNjQ4MTk2NzU5JkV4cGlyZVRpbWVTdGFtcD0yNjQ4MTk2NzU5JlJhbmRvbT0yMDIzOTEyOTMxJkZpbGVJZD0zODc3MDIyOTgxMDc3NDY1MjMmVm9kU3ViQXBwSWQ9MTUwMDAwMzk0Mw%3D%3D',
	      }
	    }
	});
	 	
	try {
		player.load(manifestUri);
		// This runs if the asynchronous load is successful.
		console.log('The video has now been loaded!');
	} catch (e) {
		// onError is executed if the asynchronous load fails.
	}	

}
        
initPlayer();


```

## 总结

学习本教程后，您已经掌握如何对视频进行 DRM 加密，并使用播放器播放加密后的视频。