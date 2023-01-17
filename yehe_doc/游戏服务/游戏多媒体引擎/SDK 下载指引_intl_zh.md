为方便开发者接入腾讯云游戏多媒体引擎产品，本文主要为您介绍适用于游戏多媒体引擎 SDK 的下载指引。

## 更新历史
如需查看历史版本的更新信息，请查阅 [产品动态](https://intl.cloud.tencent.com/document/product/607/35323)。

## 新手入门

如果是第一次使用 SDK，下载之前可参见 [新手指引](https://intl.cloud.tencent.com/document/product/607/39696) 注册服务。

## Sample Project 指引

### Sample Project 使用

下载 SDK 及 Sample Project 后，如果使用上有问题，您可参见 [Sample Project使用问题](https://www.tencentcloud.com/document/product/607/39521)，或进行 [在线咨询](https://intl.cloud.tencent.com/contact-sales) 联系腾讯云工作人员。

> ?下载的 Sample Project 代码中，需要替换为您申请的 SDKAppid 和 Key 才可编译执行，例如 Unity Demo 需要修改 **UserConfig.cs** 代码文件。申请服务详情请参见 [语音服务开通指引](https://intl.cloud.tencent.com/document/product/607/10782)。

### Sample Project 调试

使用 Sample Project 工程进行调试，如果出现问题，可以参考以下文档：

- 进房失败问题请参见 [实时语音进房失败问题](https://intl.cloud.tencent.com/document/product/607/39523) 进行解决。
- 无声问题请参见 [实时语音无声及音频问题](https://intl.cloud.tencent.com/document/product/607/39524) 进行解决。
- 调用服务出错，可以查看 [错误码](https://intl.cloud.tencent.com/document/product/607/33223) 进行解决。
- 如果无法解决，可以获取到日志后，通过 [联系我们](https://intl.cloud.tencent.com/document/product/607/49702) 联系 GME 开发者。



### Sample Project 导出

导出 Sample Project 为可执行文件的过程中，如遇见问题详情请参见 [工程导出问题](https://intl.cloud.tencent.com/document/product/607/39522) 进行解决。



## 版本更新

v2.9.6 正式版本更新如下：

<table >
<thead>
<tr>
<th width="18%">动态名称</th>
<th width="44%">动态描述</th>
 <th width="14%">发布时间</th>  
<th width="24%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>发布 SDK v2.9.6 正式版本</td>
<td ><ul style="margin:0;">
<li >实时语音新增角色设置，加大对国战、SLG 相关游戏的支持</li>
<li >支持同时播放2路伴奏</li>
<li >在线 MP3 文件作为伴奏时支持设置伴奏进度</li>
<li >文本翻译新增返回语种检测结果。</li>
<li >语音转文本接口新增翻译功能。</li>
<li >为更好的适配 VR 场景，增加本地 3D 位置输入接口。</li>
<li >新增 3D 语音黑名单接口，调用后对方声音不具有 3D 效果。</li>
<li >优化 3D 语音功能，将 3D 音频模型内置，无需传入模型路径</li>
<li >SDK 新增支持 Unity WebGL平台、xbox gamecore平台、UnrealEngine5引擎</li>
<li >SDK 适配 Playstation 5 新版本。</li>
<li >Mac 平台 SDK 新增对 M1 Arm64 架构支持</li>
<li >Android 12 蓝牙权限优化</li>
<li >修复 Android 5.1 版本的兼容问题</li>
<li >修复循环播放语音消息产生的内存问题</li>
<li >降低 SDK 内存消耗。</li>
<li >优化硬件设备启动时间，减少实时语音功能进房耗时。</li>
</ul ></td>
<td>2023-01-18</td> 
<td><a href="https://intl.cloud.tencent.com/document/product/607/18218">3D语音</a></td>
</tr>
</tbody></table>

<dx-alert infotype="notice" title="更新注意">
-  如果从旧版本升级到 2.9.6 版本，请参见 [更新指引](https://intl.cloud.tencent.com/document/product/607/32363) 进行解决。

## SDK 下载

| 平台/引擎  |   版本          | 更新时间   | SDK 下载| Sample Project 下载| 接入文档|
| ----------------- | ---------- | ---------- | ---------------------------- | ---------------------------- | -------------------------------- |
| Unity   | v2.9.6    | 2023-01-18 | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unity_Audio_SDK_2.9.6.09d06620.zip) | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unity_Audio_Demo_2.9.6.09d06620.zip) | [快速入门](https://cloud.tencent.com/document/product/607/18248) |
| Unreal Engine 4.x | v2.9.6 | 2023-01-18 | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal422_Audio_SDK_2.9.6.09d06620.zip) | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal422_Audio_Demo_2.9.6.09d06620.zip) | [快速入门](https://cloud.tencent.com/document/product/607/18267) |
| Unreal Engine 5.x | v2.9.6 |  2023-01-18 | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal5_Audio_SDK_2.9.6.97b107ed.zip) | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal5_Audio_Demo_2.9.6.97b107ed.zip) | [快速入门](https://cloud.tencent.com/document/product/607/18267) |
| Cocos2D      |v2.9.6       |  2023-01-18 | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Cocos_Audio_SDK_2.9.6.09d06620.zip) | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Cocos_Audio_Demo_2.9.6.09d06620.zip) | [快速入门](https://cloud.tencent.com/document/product/607/18292) |
| Windows      | v2.9.6       | 2023-01-18 | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Windows/GME_Windows_audio_sdk_2.9.6.92a797e4.zip) | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Windows/GME_Windows_audio_example_project_2.9.6.92a797e4.zip) | [快速入门](https://cloud.tencent.com/document/product/607/56374) |
| iOS        | v2.9.6         | 2023-01-18 | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/iOS/GME_ios_audio_sdk_2.9.6.92a797e4.zip) | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/iOS/GME_ios_audio_example_2.9.6.92a797e4.zip) | [快速入门](https://cloud.tencent.com/document/product/607/56374) |
| Android    | v2.9.6        | 2023-01-18 | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Android/GME_android_audio_sdk_2.9.6.92a797e4.zip) | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Android/GME_android_audio_example_2.9.6.92a797e4.zip) | [快速入门](https://cloud.tencent.com/document/product/607/56374) |
| macOS     | v2.9.6          | 2023-01-18 | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Mac/GME_mac_audio_sdk_2.9.6.92a797e4.zip) | [下载](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Mac/GME_mac_audio_demo_2.9.6.92a797e4.zip) | [快速入门](https://cloud.tencent.com/document/product/607/56374) |
| Web      | -          | 2022-06-20 | [下载](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.8.1/H5/GME_Web_SDK_2.8.1.47.zip) | [下载](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.8.1/H5/GME_Web_Demo_2.8.1.47.zip) | [接口文档](https://cloud.tencent.com/document/product/607/32157) |

> ?
>
> - GME SDK 也支持**主机平台**（PlayStation、Xbox、Nintendo Switch），如果需要请 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系 GME 开发者。
> - 所有平台 SDK 具体编译工具链可参见 [编译工具链文档](https://intl.cloud.tencent.com/document/product/607/46711)。
> - 默认提供 ITMG_ROOM_TYPE_FLUENCY 音质，如需使用标准音质以及高清音质，请通过 [提交工单](https://www.tencentcloud.com/zh/document/product/607/18521#:~:text=%E6%97%A5%E5%BF%97%E5%90%8E%EF%BC%8C%E9%80%9A%E8%BF%87-,%E6%8F%90%E4%BA%A4%E5%B7%A5%E5%8D%95,-%E8%81%94%E7%B3%BB%20GME%20%E5%BC%80%E5%8F%91) 联系GME开发者。



