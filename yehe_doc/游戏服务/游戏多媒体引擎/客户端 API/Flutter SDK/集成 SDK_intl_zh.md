为方便 Flutter 开发者调试和接入腾讯云游戏多媒体引擎产品 API，本文档主要为您介绍适用于 Flutter 开发的工程配置指引。

## 支持的平台

GME Flutter SDK 支持 iOS、Android 平台。

## 引入SDK

### 步骤1：下载 GME Flutter SDK

在 [下载指引](https://intl.cloud.tencent.com/document/product/607/18521) 中下载 SDK 文件，该版本中包括 GME Plugin，请将 SDK 文件解压到本地目录里。

### 步骤2：增加 Flutter 工程中 GME 插件的依赖

在您的 Flutter 项目中的 pubspec.yaml 文件中添加 GME 的依赖，注意参数中的 path 指上述 SDK 解压的路径
``` bash
dependencies:
  flutter:
    sdk: flutter
  gme:
    path: ../
```

保存 pubspec.yaml 文件后在终端（命令行界面）中输入 flutter pub get 命令使您的项目中的 GME 插件生效（如果您的 IDE 中配置了 Flutter 的插件，保存将会自动执行该命令）。
``` bash
flutter pub get
```

## iOS 工程修改
1. 在终端环境里进入到您的 Flutter 项目内 iOS 工程目录中，执行 pod install。

2. 在 xcode 工程中配置 GME 依赖的库（如果您的工程中本来就有，此步骤可以忽略）依赖文件如下图：
![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100022348635/3b7e2b2ba91e11ed9e14525400088f3a.png?q-sign-algorithm=sha1&q-ak=AKIDXRkeWGao-4Lv3f_Eu1m3VnMKKY6x8epsBbtjkms4ddDo74Ms78vFddiSrwbcU8jQ&q-sign-time=1677574660;1677578260&q-key-time=1677574660;1677578260&q-header-list=&q-url-param-list=&q-signature=bf2bce23372294095f44ea81d6ab081e19d3cdd0&x-cos-security-token=4BxBX1TdmsXQgKiC0yuQkiNKPjqcXA3ab3ea5ec8dc478a562f373af322df1e3bt1CAEDm-_AoFFamI9r7Z0Qo4kHjZ0fSHNxd4tvhUTTLE7ZVd9s-RurQ5v-9OEjAl4WGsJvhiUrpbooKU0qFC1HtwKSU8O6NVGJ6NZocBI0EAqA6XcsnjJfn8JsFxo1Hb7WAcR2k6sMrYl9csiYZW_poBONMAAwo_5tBmXa-et6MAuFNuBH4NlLm7eFJlTn0MR3L_csg8Q_8dFfnyxl14-y7FWsHh7olUQbIS3dyyuMMVUksk6zotFcewS08U5DdgVlsK5mzH68JMn2Ee4Ne2_OqLnxFB92a0TSIahKuWuB-vditl2wbPulD9DMkdb4ZEL38Zyvff1qsrO_RmrjtWinDWnEBnCw8vJZlT70QYeP3NYnGbhVBIfysFNbB6TyHp)

3. 游戏多媒体引擎 iOS 平台所需要的隐私权限如下：

- Required background modes：允许后台运行（可选）。

- Microphone Usage Description：允许麦克风权限。


## Android 工程修改
1. 因 GME 需要获取通话等权限并使用了 flutter permission-handler 权限管理插件，所以需要使用31以上版本的 Android SDK（如在工程中已经使用请忽略），修改如图：


   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100025598411/2be82716adce11ed9e14525400088f3a.png?q-sign-algorithm=sha1&q-ak=AKIDQvqZYxEAxGk7IGQ5VxYx9ES21_DoTUx_ubBjhure4A7pxIe0GL3MHmSAchNQKAA3&q-sign-time=1677574660;1677578260&q-key-time=1677574660;1677578260&q-header-list=&q-url-param-list=&q-signature=f1191c9c7b59a54d0509ecabefe7ea96456208e6&x-cos-security-token=bK7rgYee6Vlrw9RJjpxrtdfDlY04DBKa792613b4a003612ede236793ba1a4008OaKmfZJKditLmR-Y5Yin3UxRFASPLWyamAKRx-xY-qaRj0vYqXEMUqLjdbhfW9aTel3RxGt7GuYCuOILDA8msvrLtHDmWiPW1_kpPDq947w7kHezY0h4oaFirCp7LAgBNVsUBFydps-b0HOsFPkI8ceS7EMbLtxNhdsm3vx6dMf6JfHNK2cft32BuwaeSOFm3r1nsrsm9SoJv7yD5u1k76tUzdsMbI_xC_XUUztnKz0pxI2afuCsQeYmKLjLSevui57MB2cxuPRmZCKtD2HGEDyWnJFMVibQHnFTMw90i5DoT-GGre95x3cjeEIOglo0DZwjjdZuBIcFbRQ1sijX-35MpuYAga7_-s0oZ2eiHdvgpMhUC3x2deRanGBnvyhu)

2. 在 flutter 工程文件 android/app/src/AndroidManifest.xml 中添加工程权限（如已修改请忽略）。

   ``` bash
   <uses-permission android:name="android.permission.RECORD_AUDIO" />
   <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
   <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
   <uses-permission android:name="android.permission.INTERNET" />
   <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
   ```

