短视频 SDK License 用于激活短视频 SDK 的使用权限，用户可以在控制台申请测试版短视频 License 或续期、查看等操作。更多详细的短视频 SDK 功能说明，请参见 [短视频 UGSV](https://intl.cloud.tencent.com/document/product/1069/37914)。
## 申请测试版 License
您可以申请测试版 License 免费体验各项功能，其使用权限对应正式版短视频 SDK License 中的基础版。首次申请试用14天，可免费续期一次，合计28天。申请步骤如下：

### 步骤1：创建测试 License
1. 进入 [云点播控制台](https://console.cloud.tencent.com/vod/license)，管理员账号下，左侧菜单中选择【[短视频 SDK License](https://console.cloud.tencent.com/vod/license/video)】。

2. 点击右上角【编辑】，请录入App Name、Package Name以及Bundle ID。

3. 点击【确认】即可。
![](https://qcloudimg.tencent-cloud.cn/raw/5453b61401859a2599bab6ffcedbf808.png)

### 步骤2：保存测试  License
当免费测试版 License 成功创建后，页面会显示生成的 License 信息，在 SDK 初始化配置时需要传入 Key 和 LicenseUrl 这两个参数，请妥善保存以下信息。
![](https://qcloudimg.tencent-cloud.cn/raw/1500204df3029e9bbb23aa7161ad94bd.png)

## 续期测试版 License
您可以在 [云点播控制台](https://console.cloud.tencent.com/vod/license) 查看测试版 License 的有效期，测试版的 License 全程有效期为28天。当首次试用14天的测试版 License 临近到期，需对其续期1次，步骤如下：
### 步骤1：申请续期 License
进入【[短视频 SDK License](https://console.cloud.tencent.com/vod/license/video)】页面，在试用版 License 区域，单击右上角的【续期】。

### 步骤2：完成续期 License
弹出气泡提示续期成功后，随即右上角的【续期】 消失便完成测试版 License 续期14天的操作。


## 查看测试版 License
在 License 设置成功后稍等一段时间（依据网络情况而定），可以通过调用以下方法查看 License 信息。

- iOS：
```
NSLog(@"%@", [TXUGCBase getLicenceInfo]);
```
- Android：
```
TXUGCBase.getInstance().getLicenceInfo(context);
```

## License 使用方法
在调用 SDK 的相关接口前调用如下所示方法进行 License 的设置。

- iOS 建议在 `[AppDelegate application:didFinishLaunchingWithOptions:]`中添加：
```
[TXUGCBase setLicenceURL:LicenceUrl key:Key];
```
- Android 建议在 application 中添加：
```
TXUGCBase.getInstance().setLicence(context, LicenceUrl, Key);
```
