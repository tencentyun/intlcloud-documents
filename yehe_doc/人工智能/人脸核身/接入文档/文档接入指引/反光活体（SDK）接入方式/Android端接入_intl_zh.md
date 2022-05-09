### 依赖环境

当前Android端慧眼SDK适用于API 19 (Android 4.4) 及以上版本。


### 接入步骤

1. 将**huiyansdk_android_1.0.7_release.aar**(具体版本号以官网下载为准)添加到您工程的libs目录下。

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/lib%E4%B8%ADaar.png)

2. 在您工程的**build.gradle**中进行如下配置：

```groovy
// 设置ndk so架构过滤(以armeabi-v7a为例)
ndk {
abiFilters 'armeabi-v7a'
}

// 过滤重复定义so的问题(以armeabi-v7a为例)
packagingOptions{
pickFirst 'lib/armeabi-v7a/libc++_shared.so'
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


### SDK接口使用说明

#### 初始化

在您APP初始化的时候调用，推荐在Application中调用，主要是进行一些SDK的初始化操作

```java
@Override
public void onCreate() {
super.onCreate();
instance = this;
// SDK需要在Application初始化时进行初始化
HuiYanOsApi.init(getApp());
}
```


#### 初始化配置，并拉取配置参数

在使用慧眼SDK之前，需要调用此方法传入基本配置参数，同时通过回调拉取本地的配置参数信息

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
String lightData = getAuthLightData(result);
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


#### 完成剩余步骤活体核身

当您已经将配置信息从服务器端兑换完成之后，将服务器下发的LightData也就是核身的光线序列，通过此接口传入继续完成剩余本地核身功能。

```java
// 启动核验，lightData为上一步从服务器端兑换的光线序列的数据
HuiYanOsApi.startAuthByLightData(lightData, new HuiYanResultCallBack() {
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


#### SDK资源释放

在您APP退出使用的时候，可以调用SDK资源释放接口

```java
@Override
protected void onDestroy() {
super.onDestroy();
// 退出时做资源释放
HuiYanOsApi.release();
}
```


### 混淆规则配置

如果您的应用开启了混淆功能，为确保SDK的正常使用，请把以下部分添加到您的混淆文件中。

```java
#慧眼SDK的混淆包含
-keep class com.tencent.could.huiyansdk.** {*;}
-keep class com.tencent.youtu.** {*;}
-keep class com.tencent.ytcommon.** {*;}
-keep class com.tencent.ytfacetrackpro.** {*;}
-keep class com.tencent.could.component.common.** {*;}
```


## Android API的详细说明

慧眼SDK主要涉及如下几个类，它们分别是API的接口类HuiYanOsApi， 参数配置类HuiYanOsConfig，结果回调类HuiYanConfigCallback以及HuiYanResultCallBack。

### HuiYanOsApi

| API | 功能描述 |
| ----------------------------------------------------- | ---------------------------------------------------- |
| [init()](#init()) | 初始化接口 |
| [release()](#release()) | 资源释放接口 |
| [startGetAuthConfigData()](#startGetAuthConfigData()) | 获取慧眼SDK本地配置信息的接口 |
| [startAuthByLightData()](#startAuthByLightData()) | 传入服务器获取的光线序列，继续完成活体核身检测的接口 |

#### init()

```java
public static void init(Context context)
```

功能介绍：

慧眼SDK的初始化接口。

传入参数: 

| 参数类型 | 参数名称 | 参数含义 |
| -------- | -------- | --------------- |
| Context | context | App的上下文信息 |


#### release()

```java
public static void release() 
```

功能介绍：

慧眼SDK资源释放的接口。


#### startGetAuthConfigData()

```java
public static void startGetAuthConfigData(HuiYanOsConfig startConfig, HuiYanConfigCallback configCallback) 
```

功能介绍：

本地检测慧眼SDK同时拉取配置参数，用来作为后续兑换光线序列的参数。

传入参数：

| 参数类型 | 参数名称 | 参数含义 |
| --------------------------------------------- | -------------- | ------------------ |
| [HuiYanOsConfig](#HuiYanOsConfig) | startConfig | 配置的参数 |
| [HuiYanConfigCallback](#HuiYanConfigCallback) | configCallback | 拉取配置结果的回调 |


#### startAuthByLightData()

```java
public static void startAuthByLightData(String lightData, HuiYanResultCallBack resultCallBack) 
```

功能介绍：

将从服务器拉取到的光线序列数据，传入慧眼SDK同时继续核身流程，并获取本地检测的结果。

传入参数：

| 参数类型 | 参数名称 | 参数含义 |
| --------------------------------------------- | -------------- | ------------------------------------ |
| String | lightData | 从服务器兑换来启动核身使用的光线序列 |
| [HuiYanResultCallBack](#HuiYanResultCallBack) | resultCallBack | 本地核身的结果回调 |


### HuiYanOsConfig

HuiYanOsConfig是在启动慧眼SDK时的配置实体类，主要包含了以下属性。

| 类型 | 名称 | 含义 | 默认值 |
| -------------- | ------------------ | ------------------------------------ | -------------------- |
| PageColorStyle | pageColorStyle | 此次人脸核身检测的配色 | PageColorStyle.Light |
| String | authLicense | 客户申请的用户核审授权的Licens文件名 | 空 |
| long | authTimeOutMs | 设置活体检测的超时时间 | 10000毫秒（10秒） |
| boolean | isDeleteVideoCache | 是否删除核身视频的本地缓存 | true |


### PageColorStyle

默认核身界面默认配色的枚举类，当前主要包括了两种配色，白色系与黑暗色系。

| PageColorStyle类型 | 含义 |
| -------------------- | ---------- |
| PageColorStyle.Light | 亮色调配色 |
| PageColorStyle.Dark | 暗色调配色 |


### HuiYanConfigCallback

初始化并且获取本地配置的回调类

```java
/**
* 新慧眼SDK初始化与拉取本地配置的回调
*/
public interface HuiYanConfigCallback {

/**
* 获取配置成功的接口
*
* @param result 配置信息
*/
void onSuccess(String result);

/**
* 获取配置失败的接口
*
* @param errorCode 错误码
* @param errMsg 错误信息
*/
void onFail(int errorCode, String errMsg);
}
```


### HuiYanResultCallBack

本地核身流程与本地结果获取的回调类

```java
/**
* 核身完成的回调类型
*/
public interface HuiYanResultCallBack {

/**
* 回调成功的数据
*
* @param data 比对数据
* @param videoPath 核身视频路径
*/
void onSuccess(byte[] data, String videoPath);

/**
* 回调失败的结果
*
* @param errorCode 错误码
* @param errMsg 错误详细信息
*/
void onFail(int errorCode, String errMsg);
}
```




### 常见问题

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

3. Android X针对一些低版本的设备报错 **android.content.res.Resources$NotFoundException:from xml type xml resource ID #0x7f0800c3** 这一类的错误，可以考虑添加矢量图依赖：

```groovy
   // 低版本的矢量图
   implementation 'androidx.vectordrawable:vectordrawable:1.1.0'
```

4. **Android Support** 如果在低版本设备上（6.0及以下）出现如下报错：

```java
android.content.res.Resources$NotFoundException: File res/drawable/$txy_face_id_logo__0.xml from color state list resource ID #0x7f070001
           at android.content.res.Resources.loadColorStateListForCookie(Resources.java:2800)
           at android.content.res.Resources.loadColorStateList(Resources.java:2749)
           at android.content.res.TypedArray.getColor(TypedArray.java:441)
           at android.content.res.XResources$XTypedArray.getColor(XResources.java:1286)
           at android.support.v4.content.res.TypedArrayUtils.getNamedColor(TypedArrayUtils.java:124)
           at android.support.graphics.drawable.VectorDrawableCompat$VFullPath.updateStateFromTypedArray(VectorDrawableCompat.java:1746)
           at android.support.graphics.drawable.VectorDrawableCompat$VFullPath.inflate(VectorDrawableCompat.java:1712)
           at android.support.graphics.drawable.VectorDrawableCompat.inflateInternal(VectorDrawableCompat.java:743)
           at android.support.graphics.drawable.VectorDrawableCompat.inflate(VectorDrawableCompat.java:631)
           at android.support.graphics.drawable.VectorDrawableCompat.createFromXmlInner(VectorDrawableCompat.java:590)
           at android.support.v7.widget.AppCompatDrawableManager$VdcInflateDelegate.createFromXmlInner(AppCompatDrawableManager.java:775)
```


	需要更新support依赖到最新版本28.0.0:

```groovy
implementation 'com.android.support:appcompat-v7:28.0.0'

// 兼容低版本矢量图依赖的组件库
implementation 'com.android.support:support-vector-drawable:28.0.0'
implementation 'com.android.support:animated-vector-drawable:28.0.0'
```