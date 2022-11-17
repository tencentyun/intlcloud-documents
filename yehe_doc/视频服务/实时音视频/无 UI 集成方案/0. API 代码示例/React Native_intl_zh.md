本文主要介绍如何快速运行腾讯云 TRTC Demo（React Native）。

## 环境要求
- ReactNative 0.63 及以上版本
- Node & Watchman，node版本需在 v12 以上
- **Android 端开发：**
  - Android Studio 3.5及以上版本
  - App 要求 Android 4.1及以上版本设备
- **iOS & macOS 端开发：**
  - Xcode 11.0及以上版本
  - osx 系统版本要求 10.11 及以上版本
  - 请确保您的项目已设置有效的开发者签名
- 环境安装请参见 [官方文档](https://reactnative.cn/docs/environment-setup)

## 前提条件
您已 [注册腾讯云](https://intl.cloud.tencent.com) 账号。

## 操作步骤

### 步骤 1：创建新的应用

1. 登录实时音视频控制台，选择【[应用管理](https://console.tencentcloud.com/trtc/app)】。
2. 单击【创建应用】输入应用名称，例如 `APIExample`；若您已创建过应用，可以勾选【选择已有应用】，然后单击【下一步】。
   ![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)

### 步骤 2：下载示例代码

1. 选择无 UI 集成后，然后您可以根据自己的业务平台，前往【[Github](https://github.com/LiteAVSDK/TRTC_ReactNative/tree/main/TRTC-Simple-Demo)】下载相关 SDK 及配套的 Demo 源码。
2. 下载完成后，单击【下一步】。
   ![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)

### 步骤 3：配置工程

1. 在示例工程跑通阶段，选择【调试阶段】即可，然后记录下您的 SDKAppID、Secret key。
   ![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. 打开下载完成的示例代码，找到并打开`/TRTC-Simple-Demo/debug/config.js`文件，设置文件中的相关参数：
   - SDKAPPID：默认为 PLACEHOLDER ，请设置为实际的 SDKAppID。
   - SECRETKEY：默认为 PLACEHOLDER ，请设置为实际的 Secret key。
3. 此时工程配置已经完成，您可以单击【下一步】，

>?
>- 本文提到的生成 UserSig 的方案是在客户端代码中配置 SECRETKEY，该方法中 SECRETKEY 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此**该方法仅适合本地跑通 TRTC-Simple-Demo 和功能调试**。
>- 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://www.tencentcloud.com/document/product/647/35166)。

### 步骤 4：权限配置

需要配置 App 权限才能运行

#### Android 端

1. 在 `AndroidManifest.xml` 中配置 App 的权限，TRTC SDK 需要以下权限

```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```

- 请勿设置 android:hardwareAccelerated="false"，关闭硬件加速之后，会导致对方的视频流无法渲染。
- 安卓音视频权限需要手动申请。

```Java
if (Platform.OS === 'android') {
  await PermissionsAndroid.requestMultiple([
    PermissionsAndroid.PERMISSIONS.RECORD_AUDIO, //音频需要
    PermissionsAndroid.PERMISSIONS.CAMERA, // 视频需要
  ]);
}
```

#### iOS 端

1. 在 `Info.plist` 中配置 App 的权限，TRTC SDK 需要以下权限

```ObjectiveC
<key>NSCameraUsageDescription</key>
<string>授权摄像头权限才能正常视频通话</string>
<key>NSMicrophoneUsageDescription</key>
<string>授权麦克风权限才能正常语音通话</string>
```

### 步骤 5：编译运行

先执行 `npm install`

#### 安卓开发调试

1. 在 Demo 目录下启动 Metros

```
npx react-native start
```

2. 在 Demo 目录下新开窗口，启动开发调试

```
npx react-native run-android
```

#### iOS 开发调试

1. 在 Demo ios 目录里执行 `pod install` 安装依赖。
2. 在 Demo 目录下启动 Metros

```
npx react-native start
```

3. 在 Demo 目录下新开窗口，启动开发调试(如果报错请打开 xcode 编译调试)

```
npx react-native run-ios
```
