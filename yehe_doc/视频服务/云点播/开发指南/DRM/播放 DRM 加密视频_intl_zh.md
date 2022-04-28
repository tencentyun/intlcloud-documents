## 学习目标

学习本阶段教程，您将了解并掌握如何对视频进行 DRM 加密，并使用播放器播放加密后的视频 。

##  前置条件
在开始本教程之前，请您确保已满足以下前置条件。

### 开通云点播
您需要开通云点播，步骤如下：

1. 注册 [腾讯云账号](https://intl.cloud.tencent.com/document/product/378/17985)，并完成 [实名认证](https://intl.cloud.tencent.com/document/product/378/3629)。
2. 购买云点播服务，具体请参见 [计费概述](https://intl.cloud.tencent.com/document/product/266/2838)。
3. 选择 **云产品**>**视频服务**>[**云点播**](https://console.cloud.tencent.com/vod)，进入云点播控制台。

至此，您已经完成了云点播的开通步骤。 

### 申请和提交 FairPlay 证书
请参考 [如何申请和提交 FairPlay 证书](https://intl.cloud.tencent.com/document/product/266/46643)。FairPlay 证书提交成功后，您可以从控制台中查询得到证书 URL，用于后续播放使用。

## 步骤1：开启防盗链

以您账号下的默认分发域名开启 Key 防盗链为例：
>? 请避免直接对正在使用的现网域名开启防盗链，否则可能造成现网的视频无法播放。

1. 登录云点播控制台，选择【分发播放设置】>[【域名管理】](https://console.cloud.tencent.com/vod/distribute-play/domain)，单击“默认分发域名”的【设置】，单机【访问控制】，进入设置页面。
   <img src="https://main.qcloudimg.com/raw/06259e41a62ea14ce8eb19ef6480182c.png" width="800" />
2. 打开【启用 Key 防盗链】，并单击【生成随机 Key】生成一个随机的 Key，本教程为`testtest`，将生成好的 Key 复制下来，然后单击【确定】保存生效。防盗链 Key 可用于后续步骤中生成超级播放器签名。
   ![image-KEY](https://qcloudimg.tencent-cloud.cn/raw/1b4f1f0d9e3d36c153b1e91f64160f00.png)

## 步骤2：对视频进行 DRM 加密

1. 登录云点播控制台，选择 **媒资管理**>[**视频管理**](https://console.cloud.tencent.com/vod/media)，勾选要处理的视频（FileId 为387702299667618135），单击 **视频处理**。

   ![image-20220426211316803](https://qcloudimg.tencent-cloud.cn/raw/4eab2858c67f4efbf1383a3b03810428.png)

2. 在视频处理界面：
 - **处理类型** 选择 **任务流**。
 - **任务流模板** 选择 **WidevineFairPlayPreset**。
 ![image-20220425192205432](https://qcloudimg.tencent-cloud.cn/raw/cef2c1e79343ea9688654791b6fb6762.png)

>?
>- WidevineFairPlayPreset 是预置任务流：分别使用11、13模板转自适应码流，10模板截图做封面，10模板截雪碧图。
>- 11模板自适应码流是加密类型为 `FairPlay` 的多码率输出，13模板自适应码流是加密类型为 `Widevine` 的多码率输出。

3. 单击 **确定**，等待“视频状态”栏从“处理中”变为“正常”，表示视频已处理完毕：
<img src="https://main.qcloudimg.com/raw/885b68427d36faefe8f2bb5b489e1e19.png" width="" />
4. 单击视频“操作”栏下的 **管理**，进入管理页面：
 - 选择“基本信息”页签，可以看到生成的封面，以及 DRM 加密的自适应码流输出（模板 ID 为11和13）。

   ![image-20220426201159056](https://qcloudimg.tencent-cloud.cn/raw/696e894ed0c3665990c12cc57ebf23bf.png)

 - 选择“截图信息”页签，可以看到生成的雪碧图（模板 ID 为10）。

   ![image-20220426201309975](https://qcloudimg.tencent-cloud.cn/raw/1a5878fd0286c46ef487bdf81ad8503a.png)

## 步骤3：生成超级播放器签名

超级播放器签名，用于后续查询播放信息，生成方式请参考 [超级播放器签名文档](https://intl.cloud.tencent.com/document/product/266/38099) 。 本教程的超级播放器签名的 PayLoad 如下：

```json
{
  "appId": 1500012416,
  "fileId": "387702299667618135",
  "currentTimeStamp": 1650886156,
  "expireTimeStamp": 1966435200,
  "urlAccessInfo": {
    "t": "75356B80",
    "us": "72d4cd1101"
  },
  "pcfg":"advanceDrmPreset"
}
```

本教程的 Key 为 `testtest`时，生成的超级播放器签名（`psign`）如下：

`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDg4NjE1NiwiZXhwaXJlVGltZVN0YW1wIjoxOTY2NDM1MjAwLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI3NTM1NkI4MCIsInVzIjoiNzJkNGNkMTEwMSJ9LCJwY2ZnIjoiYWR2YW5jZURybVByZXNldCJ9.kkyOyscuV3WIlFV0IFPsPPWomZEcuNGclaBzpEO8DEg`

##  步骤4：查询播放信息

下面将详细介绍通过 URL 查询播放信息。

查询请求以 HTTP GET 的方式发起，URL 为`https://playvideo.qcloud.com/getplayinfo/v4/{appId}/{fileId}?psign={psign}`。

其中，`{appId}`为应用Id，如果使用了子应用，则填写对应 [子应用 id](https://intl.cloud.tencent.com/document/product/266/33987) ，fileId 为要播放的视频文件 ID。

本教程使用步骤3获取到的`psign`，则请求 URL 为：

`https://playvideo.qcloud.com/getplayinfo/v4/1500012416/387702299667618135?psign=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDg4NjE1NiwiZXhwaXJlVGltZVN0YW1wIjoxOTY2NDM1MjAwLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI3NTM1NkI4MCIsInVzIjoiNzJkNGNkMTEwMSJ9LCJwY2ZnIjoiYWR2YW5jZURybVByZXNldCJ9.kkyOyscuV3WIlFV0IFPsPPWomZEcuNGclaBzpEO8DEg`

则应答为：

```json
{
  "code": 0,
  "message": "",
  "requestId": "9c7fab8704994c6b96375393e6544b5c",
  ...
  "media": {
	...
    "streamingInfo": {
      "drmOutput": [
        {
          "type": "FairPlay",
          "url": "http://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.11.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b",
          ...
        },
        {
          "type": "Widevine",
          "url": "http://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.13.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b",
          ...
        }
      ],
      "drmToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~VfpyAFQL59xD-TJkr8kSAiXTZpd-dQdvmPkzw1PVIa8",
      "widevineLicenseUrl": "https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2",
      "fairplayLicenseUrl": "https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2"
    },
    ...
  }
}
```



从上述应答结构中，可以获取到以下播放信息：

1. 视频内容 URL。
2. 播放许可证地址（License Server URL）：
   - `Widevine`播放许可证地址：`drmToken`作为 query string 参数拼接`widevineLicenseUrl`得到；
   - `FairPlay`播放许可证地址：`drmToken`作为 query string 参数拼接`fairplayLicenseUrl`得到。

本教程的播放信息如下：

对于`Widevine`加密：

- 视频内容 URL 为 `https://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.13.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b`
- 播放许可证地址为 `https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~VfpyAFQL59xD-TJkr8kSAiXTZpd-dQdvmPkzw1PVIa8`

对于`FairPlay`加密：

- 视频内容 URL 为 `https://1500012416.vod2.myqcloud.com/4394a0devodtranscq1500012416/d811753f387702299667618135/adp.11.m3u8?t=75356B80&us=72d4cd1101&sign=73558bdac4a3ea43913806201ba0315b`
- 播放许可证地址为 `https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxMjQxNiwiZmlsZUlkIjoiMzg3NzAyMjk5NjY3NjE4MTM1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsIm92ZXJsYXlLZXkiOiIiLCJvdmVybGF5SXYiOiIiLCJjaXBoZXJlZE92ZXJsYXlLZXkiOiIiLCJjaXBoZXJlZE92ZXJsYXlJdiI6IiIsImtleUlkIjowLCJzdHJpY3RNb2RlIjowfQ~VfpyAFQL59xD-TJkr8kSAiXTZpd-dQdvmPkzw1PVIa8`


## 步骤5：使用播放器播放 DRM 加密视频。

下面分别介绍使用播放器播放 Widevine 和 FairPlay 加密视频。

#### 播放`Widevine`加密视频

使用`Chrome`浏览器打开 [Shaka Player在线播放器页面](https://shaka-player-demo.appspot.com/demo/#audiolang=zh-CN;textlang=zh-CN;uilang=zh-CN;panel=CUSTOM%20CONTENT;build=uncompiled)。

![image-20220426163418989](https://qcloudimg.tencent-cloud.cn/raw/e58eb9f3795a328b2ba01d15943389e7.png)

点击 **+**，`Manifest URL`填写步骤3中得到的视频内容 URL，`Name`可写入任意值，此处填写`Widevine`。

![image-20220426163853470](https://qcloudimg.tencent-cloud.cn/raw/0846706a160112ccea2712cd9c6b4d4c.png)

`Custom License Server URL`填写为步骤3中得到的 Widevine 播放许可证地址，最后点击**Save**按钮。

![image-20220426163939777](https://qcloudimg.tencent-cloud.cn/raw/702199c544c829db6f5d4815dcd4ff48.png)

保存之后，可以看到页面中出现了一个名为`Widevine`的播放选项。

![image-20220426164129657](https://qcloudimg.tencent-cloud.cn/raw/7d70df750e283d8a5a0d42596e08c14b.png)

点击**Play**，则可以播放解密视频。

#### 播放`FairPlay`加密视频

使用`Safari`浏览器打开 [Shaka Player在线播放器页面](https://shaka-player-demo.appspot.com/demo/#audiolang=zh-CN;textlang=zh-CN;uilang=zh-CN;panel=CUSTOM%20CONTENT;build=uncompiled)。

![image-20220426163418989](https://qcloudimg.tencent-cloud.cn/raw/0b9b5ae58e65c6b3c0789b8d98af57a1.png)

点击 **+**，`Manifest URL`填写步骤3中得到的视频内容 URL，`Name`可写入任意值，此处填写`FairPlay`。

![image-20220426164907499](https://qcloudimg.tencent-cloud.cn/raw/70f01463b0afdf231dd014ea4782728f.png)

`Custom License Server URL`填写为步骤3中得到的 FairPlay 播放许可证地址，`Custom License Certificate URL`填写为上述步骤中所设置的`FairPlay`证书地址（可在控制台中查询得到），最后点击**Save**按钮。

![image-20220426164950762](https://qcloudimg.tencent-cloud.cn/raw/bdd9c3ecd2882537df76d657768855e9.png)

保存之后，可以看到页面中出现了一个名为`FairPlay`的播放选项。

![image-20220426165137520](https://qcloudimg.tencent-cloud.cn/raw/9da228ea1db9ab54a1631f605e24d806.png)

点击**Play**，则可以播放解密视频。

## 总结

学习本教程后，您已经掌握如何对视频进行 DRM 加密，并使用播放器播放加密后的视频。