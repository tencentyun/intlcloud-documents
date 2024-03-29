直播时移依托云直播录制的能力，实现在直播过程中进行回看的功能，用户可以实时选择从开播后的某个过往时间点开始进行回看，从而达到播放之前直播内容的效果。常用于赛事直播中的精彩片段回看。

## 注意事项
- 模板创建成功后，可与推流域名进行关联。关联成功后约5分钟 - 10分钟生效。
- 开启直播时移功能将按时移数据写入量进行计费，使用直播时移功能还会产生[流量带宽费用](https://intl.cloud.tencent.com/document/product/267/2819)。
- 时移转码流需要先发起转码任务，会额外产生转码费用。请确保选择的转码模版未被误删，否则误删的时移转码流不会生效。

## 前提条件
- 已开通腾讯云直播服务，并添加 [推流域名](https://intl.cloud.tencent.com/document/product/267/35970)。

## 创建时移模板
1.登录云直播控制台，进入功能配置>[直播时移](https://console.cloud.tencent.com/live/config/time-shift/template)。
2.单击 **创建时移模板** 设置模板信息，进行如下配置：
![](https://qcloudimg.tencent-cloud.cn/raw/ffae437b96aada6754ad374093088218.png)

<table>
   <thead><tr><th width="20%" colspan=2>配置项</th><th>配置描述</th></tr></thead>
   <tbody><tr>
   <tr>
   <td colspan=2>模板名称</td>
   <td>直播时移模板名称，可自定义，支持1-10个字符（仅支持中文、英文、数字、_、-）。</td>
   </tr><tr>
   <td colspan=2>模板描述</td>
   <td>直播时移模板介绍描述，可自定义（仅支持中文、英文、数字、_、-）。</td>
   </tr><tr>
   <td colspan=2>绑定地域</td>
   <td>默认中国大陆，支持选择海外及港澳台地区。请绑定正确的时移播放加速区域，跨地域时移播放会出现卡顿或无法拉流的情况。</td>
   </tr><tr>
   <td rowspan=3 width="10%">时移内容</td>
   <td width="30%">原始流</td> 
   <td>勾选该配置时移视频内容为原始输入流，不带转码、水印及混流效果，对 WebRTC 推流原始流会丢失音频，建议选择其它内容。</ul></td>
   </tr><tr>
   <td>水印流</td>
   <td>勾选该配置时移视频内容为在直播流加水印模板配置的水印后的内容。</td>
   </tr><tr>
   <td>转码流</td>
       <td>勾选该配置时移视频内容为根据转码模板 id 发起转码后的内容，如转码模版被删除，时移回看内容将失效。转码流会产生转码费用。
</td>
   </tr><tr>
   <td colspan=2>时移天数</td>
   <td>默认1天，支持选择3天、7天、15天和30天。</td>
   </tr><tr>
   <td colspan=2>TS分片时长</td>
   <td>默认5秒，支持配置3秒-10秒。</td>
   </tr><tr>
   </tbody></table>

3.填写完成后，单击 **保存** 即可。

## 关联域名

1. 登录云直播控制台，进入 **功能配置** > [**直播时移**](https://console.cloud.tencent.com/live/config/time-shift/template)。
   - **直接关联域名：**单击左上方的 **绑定域名**。
     ![](https://qcloudimg.tencent-cloud.cn/raw/121c2a1f6a42f56c537efdcf9f9d2837.png)
   - **新时移模板创建成功后关联域名：**[时移模板创建](#C_record) 成功后，单击提醒框中的 **去绑定域名**。
     ![](https://qcloudimg.tencent-cloud.cn/raw/4e2eb59f230a83a8ee739d35992ceab0.png)
2. 在域名绑定窗口中，选择您需绑定的**时移模板**及**推流域名**，单击 **确定** 即可绑定成功。
 ![](https://qcloudimg.tencent-cloud.cn/raw/36611d57b671961122f9690ed202a998.png)
>? 支持通过单击 **添加** 为当前模板绑定多个推流域名。

## 解除绑定

1. 登录云直播控制台，进入 **功能配置** > [**直播时移**](https://console.cloud.tencent.com/live/config/time-shift/template)。
2. 选择已关联域名的时移模板，选择需要解绑的域名，单击右侧的 **解绑**。
   ![](https://qcloudimg.tencent-cloud.cn/raw/8a04377777c3eb3bee46be2b0ed38785.png)
3. 确认是否解绑当前关联域名，单击 **确定** 即可解绑。
   ![](https://main.qcloudimg.com/raw/690daf43f9b1d5f57b6033720c19860a.png)

>?  时移模板解除绑定后，不影响正在直播中的流。

[](id:change)

## 修改模板

1. 进入 **功能配置** > [**直播时移**](https://console.cloud.tencent.com/live/config/time-shift/template)。
2. 选择您已创建成功的时移模板，并单击右侧的 **编辑**，即可进入修改模板信息，单击 **保存** 即可。
 ![](https://qcloudimg.tencent-cloud.cn/raw/6e283a7e7a541da14bd58806b502f785.png)

[](id:delete)
## 删除模板

1. 登录云直播控制台，进入 **功能配置** > [**直播时移**](https://console.cloud.tencent.com/live/config/time-shift/template)。
2. 选择您已创建成功的时移模板，单击右上方 **删除**。
3. 确认是否删除当前时移模板，单击 **确定** 即可成功删除。
   ![](https://qcloudimg.tencent-cloud.cn/raw/1ca10b189eaf82a772dc3c460df2c1bd.png)

>! 
>- 若模板已被关联，需要先 [解除绑定](#unite)，才可以进行删除操作。
>- 控制台的时移模板管理为域名维度，暂时无法取消关联接口创建的规。

## 相关操作

**域名维度绑定**和**解绑**时移模板的具体操作及相关说明，请参见 时移配置。