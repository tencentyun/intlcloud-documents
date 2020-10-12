云直播控制台提供地址生成器功能，支持通过填写地址拼接信息，辅助用户快速生成推流/播放地址。其中直播地址主要由域名（domain）、应用名称（AppName）、流名称（StreamName）以及鉴权 Key 组成。
![](https://main.qcloudimg.com/raw/9094e537a4ae7cecc7feb9c88fb83a55.png)
地址生成后，可通过**选择复制**、**单击复制按钮**或**扫描二维码**的方式提取地址信息。


## 注意事项
- 云直播暂无地址生成历史记录功能，请生成地址后，复制保存。
- 若您需同时生成多个直播地址，建议使用自主拼接方法生成，具体操作文档请参见 [自主拼接直播 URL 相关](https://intl.cloud.tencent.com/document/product/267/32480)。
- 云直播默认提供测试域名`xxxx.livepush.myqcloud.com`，您可通过该域名进行推流测试，但不建议您在正式业务中使用这个域名作为推流域名。




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

<h2 id="push">生成推流地址</h2>

### 操作步骤
1. 登录云直播控制台，选择[【地址生成器】](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)，进入地址生成器。
2. 选择生成类型为**推流域名**，并选择您已添加到域名管理的推流域名。
3. 填写 AppName，默认值为：live。
4. 填写流名称 StreamName，例如：`liveteststream`。
5. 选择地址过期时间，例如：`2020-06-09 15:36:04`。
6. 单击【生成地址】即可。
![](https://main.qcloudimg.com/raw/3e9c45467ba07c5cac3250bd58ad3223.png)

### 推流地址说明
推流支持 RTMP 协议，可通过地址生成器功能生成前缀为`rtmp://`的推流地址。
![](https://main.qcloudimg.com/raw/9e2bd3bbb6c15fe4cd46a905c0fe0c27.png)


<h2 id="play">生成播放地址</h2>

### 操作步骤
1. 登录云直播控制台，选择[【地址生成器】](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)，进入地址生成器。
2. 选择生成类型为**播放域名**，并选择您已添加到域名管理的播放域名。
3. 填写 AppName，默认值为：live。
4. 填写流名称 StreamName，例如：`liveteststream`。
5. 选择地址过期时间，例如：`2020-06-09 15:36:04`。
6. 选择是否引用已创建的转码模板。
6. 单击【生成地址】即可。

![](https://main.qcloudimg.com/raw/10afad65da657a02a6f175e7d2afdc7c.png)

### 播放地址说明
若使用转码模板，生成的播放地址为转码后的直播播放地址。其中播放支持 RTMP、FLV和HLS 协议。可通过地址生成器生成前缀为 `rtmp://`和`http://`的播放地址。

![](https://main.qcloudimg.com/raw/a5b5ab5183a44e78ac7eabc757c8d16e.png)













