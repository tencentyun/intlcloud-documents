## 学习目标

学习本阶段教程，您将了解如何定制超级播放器播放的视频内容与样式，包括：

* 播放子流规格中最小分辨率为480p，最大分辨率1080p。
* 使用视频中间部分的截图作为视频封面。
* 进度条上的缩略图预览，调整为20%的间隔。

阅读之前，请先确保已经学习超级播放器指引的 [阶段1：用超级播放器播放视频](https://intl.cloud.tencent.com/document/product/266/38098) 和 [阶段2：开启防盗链后的视频播放](https://intl.cloud.tencent.com/document/product/266/38292) 篇部分，本教程使用了 [阶段1](https://intl.cloud.tencent.com/document/product/266/38098) 篇开通的账号以及上传的视频，并需要按照 [阶段2](https://intl.cloud.tencent.com/document/product/266/38292) 开启防盗链。

## 步骤1：创建自适应码流模板

1. 登录云点播控制台，选择【视频处理设置】>[【模板设置】](https://console.cloud.tencent.com/vod/video-process/template)，单击“转自适应码流模板”页签下的【创建自适应码流模板】。
<img src="https://qcloudimg.tencent-cloud.cn/raw/19f292b6dbd89cf702ba27b3e9adf042.png" width="800" />
2. 进入“模板设置”页面后，单击【添加子流】，新建子流1、子流2和子流3，填写参数如下：
	- **基本信息模块**：
	  - 【模板名称】：填写 MyTestTemplate。
	  - 【打包格式】：选择HLS
	  - 【加密类型】：选择【不加密】。
	  - 【是否允许低分辨率转高分辨率】：不开启。
	  
 - **子流信息模块**：
<table>
<thead>
<tr>
<th>子流编号</th>
<th>视频码率</th>
<th>分辨率</th>
<th>帧率</th>
<th>音频码率</th>
<th>声道</th>
</tr>
</thead>
<tbody><tr>
<td>子流1</td>
<td>512kbps</td>
<td> 视频长边空着，视频短边480px</td>
<td>24fps</td>
<td>48kbps</td>
<td>双声道</td>
</tr>
<tr>
<td>子流2</td>
<td>512kbps</td>
<td> 视频长边空着，视频短边720px</td>
<td>24fps</td>
<td>48kbps</td>
<td>双声道</td>
</tr>
<tr>
<td>子流3</td>
<td>1024kbps</td>
<td> 视频长边空着，视频短边1080px</td>
<td>24fps</td>
<td>48kbps</td>
<td>双声道</td>
</tr>
</tbody></table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/995fcae82a8d2f1a27f0b128147c285b.png" width="500" />

3.单击【创建】，则生成了一个包含3个子流的自适应码流模板，模板ID为1145464。

![](https://qcloudimg.tencent-cloud.cn/raw/1b1ffba4a8c37c8d81132e8f93c801b6.png)

## 步骤2：创建雪碧图模板

1. 登录云点播控制台，选择【视频处理设置】>[【模板设置】](https://console.cloud.tencent.com/vod/video-process/template)，单击“截图模板”页签下的【创建截图模板】。
2. 进入“模板设置”页面后，填写模板参数：
 * 【模板名称】：填写 MyTestTemplate。
 * 【模板类型】：选择【雪碧图截图】。
 * 【图片尺寸】：726px × 240px。
 * 【采样间隔】：20%。
 * 【小图行数】：10。
 * 【小图列数】：10。
![](https://qcloudimg.tencent-cloud.cn/raw/9c0f52f7a6948f693ddc2e7bda48462a.png)
3. 单击【创建】，则生成了一个模板ID为113272的雪碧图模板。
![](https://qcloudimg.tencent-cloud.cn/raw/4cf44757d6dbb339aa29c3c29fc480d7.png)

## 步骤3：创建任务流并发起处理

创建新的转自适应码流模板（ID 为1145464）和雪碧图模板（ID 为113272）后，还需要创建一个新的任务流。

1. 登录云点播控制台，选择【视频处理设置】>[【任务流设置】](https://console.cloud.tencent.com/vod/video-process/taskflow)，单击【创建任务流】：【任务流名称】：填写 MyTestProcedure。
 * 【任务类型配置】：勾选【自适应码流】、【截图】和【截取封面】：在【自适应码流任务配置】选项卡，单击【添加自适应码流模板】，在“自适应码流模版/ID”栏选择**步骤1**创建的自定义转自适应码流模板 MyTestTemplate(1145464)。
	 *  在【截图任务配置】选项卡，单击【添加截图模板】，“截图方式”栏选择【雪碧图】，“截图模板”栏选择**步骤2**创建的自定义雪碧图模板 MyTestTemplate(113272)。
	 *  在【截取封面图任务配置】选项卡，单击【添加截图模板】，“截图模板”栏选择【TimepointScreenshot】，“时间点选取”栏选择【百分比】，填写50%。
<img src="https://qcloudimg.tencent-cloud.cn/raw/0d91b5aeb8c2fe41d844e4c36c0a3d12.png" width="900" />
2. 单击【提交】，生成了一个名为 MyTestProcedure 的任务流。
![](https://main.qcloudimg.com/raw/e33008c55dcc18bed3b41f96d88c5c8c.png)
3. 在控制台选择【媒资管理】>[【视频管理】](https://console.cloud.tencent.com/vod/media)，勾选要处理的视频（FileId 为528xxx3757278095），单击【视频处理】。
4. 在视频处理弹框：
 * 【处理类型】选择【任务流】。
 * 【任务流模板】选择【MyTestProcedure】。<span></span>
 <img src="https://qcloudimg.tencent-cloud.cn/raw/649b07dfd248670d057795f3498b61ee.png" width="500" />
5. 单击【确定】，等待**视频状态**从“处理中”变为“正常”，表示视频已处理完毕。
![](https://main.qcloudimg.com/raw/2894b49729ef223941360f2f814a63fa.png)
6. 单击视频“操作”栏中的【管理】，进入管理页面：
 * 在【基本信息】栏，可以看到生成的封面，以及自适应码流输出（模板 ID 为1145464）。
 * 在【截图信息】栏，可以看到生成的雪碧图（模板 ID 为113272）。

## 步骤4：创建超级播放器配置

为了播放自定义的自适应码流和雪碧图，您需要使用自定义播放器配置。

1. 登录云点播控制台，选择【分发播放配置】>[【超级播放器配置】](https://console.cloud.tencent.com/vod/distribute-play/super-player)，单击【新建】。
2. 在超级播放器配置页面中，分别单击【添加自适应码流模板】和【添加雪碧图模板】，然后填写以下参数：
 * 【模板名称】：填写 MyTestCfg。
 * 【用于播放的自适应码流】选项卡的“自适应码流模板/ID”栏选择：MyTestTemplate(1145464)。
 * 【用于播放的雪碧图】选项卡的“截图模板”栏选择：MyTestTemplate。
<img src="https://main.qcloudimg.com/raw/2459be6bd365e9a5143146d88d44a43c.png" width="400" />
3. 单击【确定】，则生成新的超级播放器配置 MyTestCfg。

##   步骤5：预览播放体验

经过之前的步骤，您已经对视频进行了处理。现在将使用三端的超级播放器，快速体验播放效果。

1. 选择[【视频管理】](https://console.cloud.tencent.com/vod/media)的“已上传”页签，找到之前步骤上传和处理过的视频，单击“操作”栏中的【管理】，选择“超级播放器预览”页签。
2. 【播放配置】选择 MyTestCfg。
<img src="https://qcloudimg.tencent-cloud.cn/raw/4a9ea4b96588c9a2fef0ac82c5ae27e7.png" width="522" />
3. 因为默认分发域名开启了防盗链，【播放控制】选项卡支持预览时选定防盗链的过期时间、试看时长等。此处可维持默认参数（播放防盗链过期时间默认1天，试看时长和最多可播放 IP 个数不填写）。
 <img src="https://qcloudimg.tencent-cloud.cn/raw/b5d25e5c5cd9f55cf14be336f4abd967.png" width="522" />
4. 在【Web 播放器】中，单击播放器中间的按钮，即可在 Web 端播放体验。
<img src="https://main.qcloudimg.com/raw/976ec23a988bcb494c4b225e635a5dba.png" width="522" />


##  步骤6：使用 Demo 验证

开启防盗链后，超级播放器必须使用有效期内的签名，才能播放视频。下面将介绍如何使用签名工具快速生成签名。

1. 打开 [超级播放器 - 签名生成工具](https://vods.cloud.tencent.com/signature/super-player-sign.html) 页面，并填写参数：
 * 【用户 appId】：填写视频所属的 appId：1400xxx357（如果使用的是子应用，填写子应用的 appId）。
 * 【视频 fileId】：填写视频的 FileId：528xxx3757278095。
 * 【当前 Unix 时间戳】：工具自动生成出了当前的 Unix 时间（1591756516），无需填写。
 * 【超级播放器配置】：填写自定义的超级播放器配置名 MyTestCfg。
 * 【签名过期 Unix 时间戳】：签名本身的过期时间，可以不填写，默认为1天后过期。
 * 【链接过期时间】：Key 防盗链过期时间，可以填6小时后的十六进制 Unix 时间：5ee09b44。
 * 【防盗链 Key】：填写之前获取到的防盗链 Key：2WExxx48eW。
2. 单击【生成签名】，生成出来的签名显示在“生成签名结果”文本框中。
img src="https://main.qcloudimg.com/raw/c7eff5906fbf01d8f28ec37119f8caf0.png" width="700" />

获取超级播放器签名后，您可以分别使用 [Web](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html)、[Android](https://github.com/tencentyun/SuperPlayer_Android) 和 [iOS](https://github.com/tencentyun/SuperPlayer_iOS)  三端的超级播放器 Demo 进行验证，具体请参考 Demo 的源码。
>?在控制台的【媒资管理】>[【视频管理】](https://console.cloud.tencent.com/vod/media)>【超级播放器预览】中，可以获取预览视频对应的 Web 播放器源码，供您直接参考使用。
<img src="https://main.qcloudimg.com/raw/c5756910c7958aae198804c91b76a89e.png" width="500" />

## 总结

学习本教程后，您已经掌握如何定制超级播放器播放的视频内容与样式。
如果您希望对视频进行加密，并播放加密后的视频，请参考 [阶段4：播放加密视频](https://intl.cloud.tencent.com/document/product/266/38294)。
