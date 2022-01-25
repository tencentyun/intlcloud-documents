云直播控制台提供地址生成器功能，支持通过填写地址拼接信息，辅助用户快速生成推流/播放地址。其中直播地址主要由域名（domain）、应用名称（AppName）、流名称（StreamName）以及鉴权 Key 组成。
![](https://main.qcloudimg.com/raw/55879651fe2ca61a3699ab4ed9de41d4.jpg)
地址生成后，可通过**选择复制**、**单击复制按钮**或**扫描二维码**的方式提取地址信息。


## 注意事项
- 云直播暂无地址生成历史记录功能，请生成地址后，复制保存。
- 若您需同时生成多个直播地址，建议使用自主拼接方法生成，具体操作文档请参见 [自主拼接直播 URL 相关](https://intl.cloud.tencent.com/document/product/267/38393)。
- 云直播默认提供测试域名`xxxx.livepush.myqcloud.com`，您可通过该域名进行推流测试，但不建议您在正式业务中使用这个域名作为推流域名。
- 直播地址二维码可通过使用 [腾讯云工具包 App](https://intl.cloud.tencent.com/document/product/1071/38147) 扫码直接获取使用。
- 若流名称后缀和转码模板 ID 冲突，将导致流状态异常，请更换流名称。



##  前提条件
已登录 [云直播控制台](https://console.cloud.tencent.com/live/livestat)，并添加 [推流/播放域名](https://intl.cloud.tencent.com/document/product/267/35970)。

## 配置参数说明

<table>
<thead><tr><th>配置参数</th><th>说明</th></tr></thead>
<tbody><tr>
<td>生成类型与域名</td>
<td>可选择<strong>推流域名</strong>或<strong>播放域名</strong>。</td>
</tr><tr><td>AppName</td>
<td>直播的应用名称，用于区分直播流媒体文件存放路径，默认为 live。<br>仅支持填写英文字母、数字和符号。</td>
</tr><tr><td>StreamName</td>
<td>自定义的流名称，每路直播流的唯一标识符。<br>仅支持填写英文字母、数字和符号。</td>
</tr><tr><td>过期时间</td>
<td><li>播放地址过期时间为设置时间戳加播放鉴权设置的有效时间。<li>推流地址过期时间即设置时间。</td>
</tr><tr><td>转码模板</td>
<td><li>仅在选择生成类型为<strong>播放域名</strong>时使用。<li>若选择 <a href="https://intl.cloud.tencent.com/document/product/267/31071">转码模板</a>，生成的播放地址为转码后的直播播放地址。若需播放原始直播流，则无需选择转码模板生成地址。</td>
</tr>
</tbody></table>

[](id:push)
## 生成推流地址
### 操作步骤
1. 登录云直播控制台，选择 [**地址生成器**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)，进入地址生成器。
2. 选择生成类型为**推流域名**，并选择您已添加到域名管理的推流域名。
3. 填写 AppName，默认值为：live。
4. 填写流名称 StreamName，例如：`liveteststream`。
5. 选择地址过期时间，例如：`2021-12-15 10:06:22`。
6. 单击**生成地址**即可。

![](https://qcloudimg.tencent-cloud.cn/raw/68d6cc91bb1092b418f5863f7d91e832.png)

[](id:pushurl)
### 推流地址说明
推流支持 RTMP 、WebRTC和SRT协议，可通过地址生成器功能生成前缀为 `rtmp://` 、webrtc://和`srt://` 的推流地址。
![](https://qcloudimg.tencent-cloud.cn/raw/d866991901d2c780112da709d4e0ba3c.png)


[](id:play)
## 生成播放地址
### 操作步骤
1. 登录云直播控制台，选择[**地址生成器**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)，进入地址生成器。
2. 选择生成类型为**播放域名**，并选择您已添加到域名管理的播放域名。
3. 填写 AppName，默认值为：live。
4. 填写流名称 StreamName，例如：`liveteststream`。
5. 选择地址过期时间，例如：`2021-12-15 10:20:26`。
6. 选择是否引用已创建的转码模板。
6. 单击**生成地址**即可。

![](https://qcloudimg.tencent-cloud.cn/raw/838b4bc6cf9df0c308f9636b1d7c06af.png)

[](id:playurl)
### 播放地址说明
若使用转码模板，生成的播放地址为转码后的直播播放地址。其中播放支持 RTMP、FLV、HLS协议和Webrtc协议。可通过地址生成器生成前缀为 `rtmp://`、`http://` 和webrtc://的播放地址。
>! UDP 协议的播放地址为快直播地址，可通过 [快直播快速入门](https://intl.cloud.tencent.com/document/product/267/41030) 了解使用，快直播费用详细参见 [价格总览](https://intl.cloud.tencent.com/document/product/267/2819)。

![](https://qcloudimg.tencent-cloud.cn/raw/345cc01a3d77d6816d1789fe60b7184e.png)
