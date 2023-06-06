### 一、开发准备

1. 注册腾讯云账号，点击进入慧眼控制台，即可开通相应服务。
2. 从慧眼SDK下载链接中下载SDK，并集成到本地。
3. 申请并下载license文件。



### 二、Android端慧眼 SDK接入流程

SDK提供了文件为**huiyansdk_android_1.0.7_release.aar**(具体版本号以官网下载为准)，该文件封装了人脸活体检测的功能。



#### 1. 依赖环境

当前Android端慧眼SDK适用于API 19 (Android 4.4) 及以上版本。



#### 2. 接入步骤

1. 将**huiyansdk_android_1.0.7_release.aar**(具体版本号以官网下载为准)添加到您工程的libs目录下。

   ![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/lib%E4%B8%ADaar.png)

   

2. 在您工程的**build.gradle**中进行如下配置：

```groovy
// 设置ndk so架构过滤(以armeabi-v7a为例)
ndk {
    abiFilters 'armeabi-v7a'
}

dependencies {
    // 引入慧眼SDK
    implementation files("libs/huiyansdk_android_1.0.7_release.aar")
    // 慧眼SDK需要依赖的第三方库
    // gson
    implementation 'com.google.code.gson:gson:2.8.5'
}
```



3. 同时需要在AndroidManifest.xml文件中进行必要的权限声明

```xml
<!-- 摄像头权限 -->
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature
    android:name="android.hardware.camera"
    android:required="true" />
<uses-feature android:name="android.hardware.camera.autofocus" />

<!-- SDK需要的权限 -->
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

   对于需要兼容Android 6.0以上的用户，以上权限除了需要在AndroidManifest.xml文件中声明权以外，还需使用代码动态申请权限。



#### 3. 整体流程图

下图展示了SDK、客户端以及服务器端的整体交互逻辑。

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/%E6%B5%B7%E5%A4%96%E7%89%88%E4%BA%A4%E4%BA%92%E5%9B%BEv2.png)





#### 4. SDK接口使用说明

##### 4.1 初始化

​	在您APP初始化的时候调用，推荐在Application中调用，主要是进行一些SDK的初始化操作。

```java
@Override
public void onCreate() {
    super.onCreate();
    instance = this;
    // SDK需要在Application初始化时进行初始化
    HuiYanOsApi.init(getApp());
}
```



##### 4.2 初始化配置，并拉取配置参数

​	在使用慧眼SDK之前，需要调用此方法传入基本配置参数，同时通过回调拉取本地的配置参数信息，大概流程如下。

1. 设置启动参数信息。

2. 调用**startGetAuthConfigData**接口启动获取核身配置数据。
3. 在**onSuccess**的回调获取返回的配置信息。
4. 将**result**返回的配置信息，通过调用云API接口**GenerateReflectSequence**获取光线序列。


```java
// HuiYanOs的相关参数
HuiYanOsConfig huiYanOsConfig = new HuiYanOsConfig();
// 此license文件存放在assets下
huiYanOsConfig.setAuthLicense("YTFaceSDK.license");
// 启动核身前，拉取本地的配置参数信息
HuiYanOsApi.startGetAuthConfigData(huiYanOsConfig, new HuiYanConfigCallback() {
		@Override
		public void onSuccess(String result) {
			// 获取配置信息成功, 将配置信息发送给服务器，兑换启动核身配置，服务器下发的光线序列（客户自己实现）
			String reflectSequence = getAuthLightData(result);
      // ... 剩余步骤
		}

		@Override
		public void onFail(int errorCode, String errMsg) {
			// 获取配置参数失败（客户自己实现）
			showError(errorCode, errMsg);
		}
});
```

**注意：**当前的 **"YTFaceSDK.license"**文件是需要您主动申请的，暂时您可以联系客服人员进行license申请。将申请完成后的license文件放到assets文件下。

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/license%E5%AD%98%E6%94%BE%E8%B7%AF%E5%BE%84.png)



##### 4.3 完成剩余步骤活体核身

​	当您已经将配置信息从服务器端兑换完成之后，将服务器下发的reflectSequence也就是核身的光线序列，通过此接口传入继续完成剩余本地核身功能，大致流程如下：

1. 得到上一步从云API获取到的光线序列**reflectSequence**。
2. 调用SDK接口**startAuthByLightData**，并把**reflectSequence**作为参数传入启动后续核验流程。
3. 通过**onSuccess**可以获取到过程中的核身数据**data**以及核身主要过程的录制视频的文件地址。
4. 最后将核身数据**data**通过调用云API接口**DetectReflectLivenessAndCompare**进行核身比对，获得最终比对结果。

```java
// 启动核验，reflectSequence为上一步从服务器端兑换的光线序列的数据
HuiYanOsApi.startAuthByLightData(reflectSequence, new HuiYanResultCallBack() {
		@Override
		public void onSuccess(byte[] data, String videoPath) {
			// 1. 将本地核身的数据信息，发送到服务器端做比对验证，得到最终结果。（客户自己实现）
			checkAuthResultByData(data);
			// 2. 处理本地核身视频videoPath。（客户自己实现）
			dealWithAuthVideo(videoPath);
		}

		@Override
		public void onFail(int errorCode, String errMsg) {
			// 本地核身失败获取，发生错误
			showError(errorCode, errMsg);
		}
});
```



##### 4.4 SDK资源释放

​	在您APP退出使用的时候，可以调用SDK资源释放接口

```java
@Override
protected void onDestroy() {
    super.onDestroy();
    // 退出时做资源释放
    HuiYanOsApi.release();
}
```



#### 5. 混淆规则配置

  如果您的应用开启了混淆功能，为确保SDK的正常使用，请把以下部分添加到您的混淆文件中。

```java
#慧眼SDK的混淆包含
-keep class com.tencent.could.huiyansdk.** {*;}
-keep class com.tencent.youtu.** {*;}
-keep class com.tencent.ytcommon.** {*;}
-keep class com.tencent.could.component.common.** {*;}
```



### 三、常见接入集成问题

1. 集成慧眼后出现**Invoke-customs are only supported starting with Android O (--min-api 26)**错误？

   需要在build.gradle中添加如下配置：

```groovy
   // java版本支持1.8
   compileOptions {
       sourceCompatibility JavaVersion.VERSION_1_8
       targetCompatibility JavaVersion.VERSION_1_8
   }
```

2. 如果集成方使用了AndResGuard的混淆工具，可以添加混淆配置：

```groovy
// for HuiYanSDK
"R.string.ocr_*",
"R.string.rst_*",
"R.string.net_*",
"R.string.msg_*",
"R.string.fl_*",
```

