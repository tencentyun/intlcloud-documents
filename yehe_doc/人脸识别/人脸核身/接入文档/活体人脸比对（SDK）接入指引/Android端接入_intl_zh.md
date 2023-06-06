### 开发准备

1. 注册腾讯云账号，点击进入慧眼控制台，即可开通相应服务。
2. 从慧眼SDK下载链接中下载SDK，并集成到本地。
3. 申请并下载license。



### Android端慧眼 SDK接入流程

​	SDK提供了文件为**huiyansdk_android_overseas_1.0.9.6_release.aar**、**tencent-ai-sdk-youtu-base-1.0.1.39-release.aar**、**tencent-ai-sdk-common-1.1.36-release.aar**、**tencent-ai-sdk-aicamera-1.0.22-release.aar**(具体版本号以官网下载为准) (具体版本号以官网下载为准)，该文件封装了人脸活体检测的功能。



#### 依赖环境

当前Android端慧眼SDK适用于API 19 (Android 4.4) 及以上版本。



#### 接入步骤

1. 将**huiyansdk_android_overseas_1.0.9.6_release.aar**具体版本号以官网下载为准) 和 **tencent-ai-sdk-youtu-base-1.0.1.39-release.aar**、**tencent-ai-sdk-common-1.1.36-release.aar**、**tencent-ai-sdk-aicamera-1.0.22-release.aar**(具体版本号以最终提供为准) 添加到您工程的libs目录下。

   ![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/SDK%E6%96%87%E6%A1%A3%E5%9B%BE%E5%BA%8A/tuyong/oversea_lib.png)

2. 在您工程的**build.gradle**中进行如下配置：

```groovy
// 设置ndk so架构过滤(以armeabi-v7a为例)
ndk {
    abiFilters 'armeabi-v7a'
}

dependencies {
    // 引入慧眼SDK
    implementation files("libs/huiyansdk_android_overseas_1.0.9.5_release.aar")
    // 慧眼通用算法SDK
    implementation files("libs/tencent-ai-sdk-youtu-base-1.0.1.32-release.aar")
    // 通用能力组件库
    implementation files("libs/tencent-ai-sdk-common-1.1.27-release.aar")
    implementation files("libs/tencent-ai-sdk-aicamera-1.0.18-release.aar")

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
<uses-permission android:name="android.permission.INTERNET" />
<!-- SDK可选需要的权限 -->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

   对于需要兼容Android 6.0以上的用户，以上权限除了需要在AndroidManifest.xml文件中声明权以外，还需使用代码动态申请权限。



#### SDK接口使用说明

#### 初始化

​	在您APP初始化的时候调用，推荐在Application中调用，主要是进行一些SDK的初始化操作

```java
@Override
public void onCreate() {
    super.onCreate();
    instance = this;
    // SDK需要在Application初始化时进行初始化
    HuiYanOsApi.init(getApp());
}
```



#### 一、深度集成方式

集成方可以获取中间步骤数据，并在需求集成方负责数据转发工作。

下图展示了SDK、客户端以及服务器端的在深度集成方式下整体交互逻辑：（**与精简集成方式根据业务需要选择一种进行即可**）

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/%E6%B5%B7%E5%A4%96%E7%89%88%E4%BA%A4%E4%BA%92%E5%9B%BEv2.png)





##### 1. 初始化配置，并拉取配置参数

​	在使用慧眼SDK之前，需要调用此方法传入基本配置参数，同时通过回调拉取本地的配置参数信息

```java
// HuiYanOs的相关参数
HuiYanOsConfig huiYanOsConfig = new HuiYanOsConfig();
// 此license文件存放在assets下
huiYanOsConfig.setAuthLicense("YTFaceSDK.license");
// 启动核身前，拉取本地的配置参数信息
HuiYanOsApi.startGetAuthConfigData(huiYanOsConfig, new HuiYanConfigCallback() {
		@Override
		public void onSuccess(String result) {
			// 获取配置信息成功, 将配置信息发送给服务器，兑换启动核身配置，服务器下发的光线序列（客户自己实现上图step 4）
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



> Tips：如果集成方需要主动停止核身流程（如拉取光线序列网络异常或者产生错误时），可以调用**HuiYanOsApi.startAuthByLightData（null，HuiYanResultCallBack）**传入null，用以终止流程。

##### 2. 完成剩余步骤活体核身

​	当您已经将配置信息从服务器端兑换完成之后，将服务器下发的reflectSequence也就是核身的光线序列，通过此接口传入继续完成剩余本地核身功能。

```java
// 启动核验，reflectSequence为上一步从服务器端兑换的光线序列的数据
HuiYanOsApi.startAuthByLightData(reflectSequence, new HuiYanResultCallBack() {
		@Override
		public void onSuccess(byte[] data, String videoPath) {
			// 1. 将本地核身的数据信息，发送到服务器端做比对验证，得到最终结果。（客户自己实现上图step 9）
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



#### 前后端交互的补充说明：

**上图step 4** 需要客户自己实现，对应SDK方法的 **startGetAuthConfigData** 的回调数据，需要DeviceData数据的配套Tencent Cloud API是 [GenerateReflectSequence](https://www.tencentcloud.com/document/product/1061/47646?lang=en&from_wecom=1)

客户通过SDK获取的DeviceData 需要自己发送到类似Cos的平台上，同时确保外部网络可以访问。 [GenerateReflectSequence](https://www.tencentcloud.com/document/product/1061/47646?lang=en&from_wecom=1) 的入参 DeviceDataUrl 即上传存储平台后的URL地址，腾讯云API会从中获取SDK产生的DeviceData数据，DeviceDataMd5为数据的MD5，腾讯云服务会利用DeviceDataMd5校验数据完整性。

**上图step 9 **需要客户自己实现，对应SDK方法的 **startAuthByLightData** 的回调数据上传 LiveData（活体数据），需要LiveData数据的配套 Tencent Cloud API是[DetectReflectLivenessAndCompare](https://www.tencentcloud.com/document/product/1061/44246?lang=en&from_wecom=1)

客户通过SDK获取的 LiveData数据需要自己发送到类似COS平台上，同时确保外部网络可以访问。 [DetectReflectLivenessAndCompare](https://www.tencentcloud.com/document/product/1061/44246?lang=en&from_wecom=1) 的入参 LiveDataUrl 即上传存储平台后的URL地址，腾讯云API会从中获取SDK产生的LiveData数据，LiveDataMd5为数据的MD5，腾讯云服务会利用LiveDataMd5校验数据完整性（[DetectReflectLivenessAndCompare](https://www.tencentcloud.com/document/product/1061/44246?lang=en&from_wecom=1) 的入参ImageUrl与ImageMd5类似）。



#### 二、精简集成方式

集成方只需要传入Token并启动对应的活体建议方法，便可以完成活体检测，并放回活体结果。（**与深度集成方式根据业务需要选择一种进行即可**）

Token的获取可以参考云API接口：[ApplyLivenessToken](https://www.tencentcloud.com/document/product/1061/49955?lang=en&from_wecom=1)

下图展示了SDK、客户端以及服务器端的在精简集成方式下整体交互逻辑：

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/%E6%85%A7%E7%9C%BC%E7%A7%81%E6%9C%89%E5%8C%96%E7%B2%BE%E7%AE%80%E6%B5%81%E7%A8%8B%E5%9B%BE.png)



##### 启动精简活体核身

```java
// HuiYanOs的相关参数
HuiYanOsConfig huiYanOsConfig = new HuiYanOsConfig();
// 此license文件存放在assets下
huiYanOsConfig.setAuthLicense("YTFaceSDK.license");
if (compatCheckBox.isChecked()) {
    huiYanOsConfig.setPageColorStyle(PageColorStyle.Dark);
}
// 是否需要返回最佳帧
if (needBestImageCB.isChecked()) {
    huiYanOsConfig.setNeedBestImage(true);
}
// 启动精简方法，开始的活体，currentToken为后台下发数据
HuiYanOsApi.startHuiYanAuth(currentToken, huiYanOsConfig, new HuiYanOsAuthCallBack() {
    @Override
    public void onSuccess(HuiYanOsAuthResult authResult) {
        showToast("活体通过！");
        if (!TextUtils.isEmpty(authResult.getBestImage())) {
           CommonUtils.decryptBestImgBase64(authResult.getBestImage(), false);
        }
    }

    @Override
    public void onFail(int errorCode, String errorMsg, String token) {
        String msg = "活体失败 " + "code: " + errorCode + " msg: " + errorMsg + " token: " + token;
        Log.e(TAG, "onFail" + msg);
        showToast(msg);
    }
});
```

[HuiYanOsAuthResult](#HuiYanOsAuthResult) 为活体成功的返回结果。

**注意：**当前的 **"YTFaceSDK.license"**文件是需要您主动申请的，暂时您可以联系客服人员进行license申请。将申请完成后的license文件放到assets文件下。



#### SDK资源释放

​	在您APP退出使用的时候，可以调用SDK资源释放接口

```java
@Override
protected void onDestroy() {
    super.onDestroy();
    // 退出时做资源释放
    HuiYanOsApi.release();
}
```



#### 混淆规则配置

  如果您的应用开启了混淆功能，为确保SDK的正常使用，请把以下部分添加到您的混淆文件中。

```java
#慧眼SDK的混淆包含
-keep class com.tencent.could.huiyansdk.** {*;}
-keep class com.tencent.could.aicamare.** {*;}
-keep class com.tencent.could.component.** {*;}
-keep class com.tencent.youtu.** {*;}
-keep class com.tenpay.utils.SMUtils {*;}
```



### 常见接入集成问题

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





## API的详细说明

慧眼SDK主要涉及如下几个类，它们分别是API的接口类HuiYanOsApi， 参数配置类HuiYanOsConfig，结果回调类HuiYanConfigCallback以及HuiYanResultCallBack。

### HuiYanOsApi

| API                                                   | 功能描述                                                     |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| [init()](#init())                                     | 初始化接口                                                   |
| [release()](#release())                               | 资源释放接口                                                 |
| [startGetAuthConfigData()](#startGetAuthConfigData()) | 获取慧眼SDK本地配置信息的接口                                |
| [startAuthByLightData()](#startAuthByLightData())     | 传入服务器获取的光线序列，继续完成活体核身检测的接口         |
| [startHuiYanAuth()](#startHuiYanAuth())               | 精简流程的海外核身接口，只需调用此接口即可完成整体核身流程。 |



#### init()

```java
public static void init(Context context)
```

功能介绍：

​	慧眼SDK的初始化接口。

传入参数:	

| 参数类型 | 参数名称 | 参数含义        |
| -------- | -------- | --------------- |
| Context  | context  | App的上下文信息 |



#### release()

```java
public static void release() 
```

功能介绍：

​	慧眼SDK资源释放的接口。



#### startGetAuthConfigData()

```java
public static void startGetAuthConfigData(HuiYanOsConfig startConfig, HuiYanConfigCallback configCallback) 
```

功能介绍：

​	本地检测慧眼SDK同时拉取配置参数，用来作为后续兑换光线序列的参数。

传入参数：

| 参数类型                                      | 参数名称       | 参数含义           |
| --------------------------------------------- | -------------- | ------------------ |
| [HuiYanOsConfig](#HuiYanOsConfig)             | startConfig    | 配置的参数         |
| [HuiYanConfigCallback](#HuiYanConfigCallback) | configCallback | 拉取配置结果的回调 |



#### startAuthByLightData()

```java
public static void startAuthByLightData(String reflectSequence, HuiYanResultCallBack resultCallBack) 
```

功能介绍：

​	将从服务器拉取到的光线序列数据，传入慧眼SDK同时继续核身流程，并获取本地检测的结果。

传入参数：

| 参数类型                                      | 参数名称        | 参数含义                             |
| --------------------------------------------- | --------------- | ------------------------------------ |
| String                                        | reflectSequence | 从服务器兑换来启动核身使用的光线序列 |
| [HuiYanResultCallBack](#HuiYanResultCallBack) | resultCallBack  | 本地核身的结果回调                   |



#### startHuiYanAuth()

```java
public static void startHuiYanAuth(final String startToken, final HuiYanOsConfig startConfig, HuiYanOsAuthCallBack authCallBack)
```

功能介绍：

​	精简流程的海外核身接口，只需调用此接口即可完成整体核身流程。

传入参数：

| 参数类型                                      | 参数名称     | 参数含义                              |
| --------------------------------------------- | ------------ | ------------------------------------- |
| String                                        | startToken   | 从服务器兑换来启动核身使用的业务Token |
| [HuiYanOsConfig](#HuiYanOsConfig)             | startConfig  | 配置的参数                            |
| [HuiYanOsAuthCallBack](#HuiYanOsAuthCallBack) | authCallBack | 活体结果的回调                        |




### HuiYanOsConfig

HuiYanOsConfig是在启动慧眼SDK时的配置实体类，主要包含了以下属性。

| 类型                              | 名称               | 含义                                         | 默认值               |
| --------------------------------- | ------------------ | -------------------------------------------- | -------------------- |
| [PageColorStyle](#PageColorStyle) | pageColorStyle     | 此次人脸核身检测的配色                       | PageColorStyle.Light |
| String                            | authLicense        | 客户申请的用户核审授权的Licens文件名         | 空                   |
| long                              | authTimeOutMs      | 设置活体检测的超时时间                       | 10000毫秒（10秒）    |
| boolean                           | isDeleteVideoCache | 是否删除核身视频的本地缓存                   | true                 |
| boolean                           | isShowGuidePage    | 是否打开核身的引导页                         | true                 |
| boolean                           | isNeedBestImage    | 是否需要返回最佳帧（此配置只在精简流程有效） | false                |
| LanguageStyle | languageStyle    | 语言类型 | 跟随系统语言 |
| String| languageCode    | 语言码（见附录），配合languageStyle一起使用 |   空|



### PageColorStyle

默认核身界面默认配色的枚举类，当前主要包括了两种配色，白色系与黑暗色系。

| PageColorStyle 类型  | 含义       |
| -------------------- | ---------- |
| PageColorStyle.Light | 亮色调配色 |
| PageColorStyle.Dark  | 暗色调配色 |

### LanguageStyle

| LanguageStyle 类型  | 含义       |
| -------------------- | ---------- |
| LanguageStyle.AUTO | 跟随系统 |
| LanguageStyle.ENGLISH  | 英语 |
| LanguageStyle.SIMPLIFIED_CHINESE  | 简体中文 |
| LanguageStyle.TRADITIONAL_CHINESE  | 繁体中文 |
| LanguageStyle.CUSTOMIZE_LANGUAGE  | 自定义语言 |



### HuiYanOsAuthResult

精简活体流程的成功回调对应的结果类型。

| 类型   | 名称      | 含义                       | 模式值 |
| ------ | --------- | -------------------------- | ------ |
| String | token     | 此次活体流程中使用的token  | 空     |
| String | bestImage | 活体最佳帧图片的Base64数据 | 空     |



### 错误码

这里是SDK在失败回调中的错误码，目前慧眼海外版SDK包含的错误码与其含义如下：

| 错误码                                | 错误码值 | 错误码含义                                                   |
| ------------------------------------- | -------- | ------------------------------------------------------------ |
| HY_NETWORK_ERROR                      | 210      | 网络请求出现异常                                             |
| HY_LOCAL_REF_FAILED_ERROR             | 211      | 本地初始化SDK时，检测失败，常见异常不存在license文件或者license过期 |
| HY_USER_CANCEL_ERROR                  | 212      | 用户主动取消核身流程                                         |
| HY_INNER_ERROR_CODE                   | 213      | SDK内部产生的异常，终止了核身流程                            |
| HY_DO_NOT_CHANGE_ERROR                | 214      | 在核身过程中切换应用发生终止流程的异常                       |
| HY_CAMERA_PERMISSION_ERROR            | 215      | 获取摄像头过程中发生异常                                     |
| HY_INIT_SDK_ERROR                     | 216      | 未调用init()方法，直接调用了                                 |
| HY_VERIFY_LOCAL_ERROR                 | 217      | 本地人脸检测失败                                             |
| HY_PERMISSION_CHECK_ERROR             | 218      | 本地SDK所需要的权限不足                                      |
| HY_APP_STOP_ERROR                     | 219      | 集成者主动终止核身流程，startAuthByLightData的reflectSequence为null时 |
| HY_CHECK_LIVE_DATA_ERROR              | 220      | 传入的光线序列参数校验失败                                   |
| HY_INITIALIZATION_PARAMETER_EXCEPTION | 221      | 在未获取设备配置的前提下，直接调用了设置光线序列参数的方法时，会出现的异常 |
| HY_VERIFY_LOCAL_TIME_OUT              | 222      | 本地核身动作检测超时                                         |
| HY_PREPARE_TIME_OUT                   | 223      | 准备过程超时（启动摄像头到第一次检测到人脸的时间超时）       |
| HY_CHECK_PERMISSION_ERROR             | 224      | SDK内部申请摄像头权限失败                                    |





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



### HuiYanOsAuthCallBack

精简活体流程的回调接口

```java
/**
 * 海外精简的结果回调
 *
 * @author jerrydong
 * @since 2022/6/10
 */
public interface HuiYanOsAuthCallBack {

    /**
     * 活体成功回调
     *
     * @param authResult 结果
     */
    void onSuccess(HuiYanOsAuthResult authResult);

    /**
     * 活体失败
     *
     * @param errorCode 错误码
     * @param errorMsg 错误信息
     * @param token 本次核身使用的
     */
    void onFail(int errorCode, String errorMsg, String token);
}
```



### 新增语言

新增语言的话文件，则需要执行以下两部就可以实现：

1. 在主module（集成慧眼SDK的module）工程里新增对应语言文件夹。

2. 将**hy_customer_string.xml**拷贝到改语言文件夹下，并修改对应的value内容。

   ![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/%E6%96%B0%E5%A2%9E%E8%AF%AD%E8%A8%80.png)

3. 在代码里指定对应的语言码即可（以泰文为例）。

```java
huiYanOsConfig.setLanguageStyle(LanguageStyle.CUSTOMIZE_LANGUAGE);
huiYanOsConfig.setLanguageCode("th-TH");
```


#### 附录Android语言码

这里提供一下Android的部分语言码，以供参考。

| 语言码     | 对应使用的国家或地区       |
| ---------- | -------------------------- |
| **af-ZA**  | **公用荷兰语 - 南非**      |
| **sq-AL**  | **阿尔巴尼亚 -阿尔巴尼亚** |
| **ar-DZ**  | **阿拉伯语 -阿尔及利亚**   |
| **ar-BH**  | **阿拉伯语 -巴林**         |
| **ar-EG**  | **阿拉伯语 -埃及**         |
| **ar-IQ**  | **阿拉伯语 -伊拉克**       |
| **ar-JO**  | **阿拉伯语 -约旦**         |
| **ar-KW**  | **阿拉伯语 -科威特**       |
| **ar-LB**  | **阿拉伯语 -黎巴嫩**       |
| **ar-LY**  | **阿拉伯语 -利比亚**       |
| **ar-MA**  | **阿拉伯语 -摩洛哥**       |
| **ar-OM**  | **阿拉伯语 -阿曼**         |
| **ar-QA**  | **阿拉伯语 -卡塔尔**       |
| **eu-ES**  | **巴斯克 -巴斯克**         |
| **be-BY**  | **Belarusian-白俄罗斯**    |
| **bg-BG**  | **保加利亚 -保加利亚**     |
| **ca-ES**  | **嘉泰罗尼亚 -嘉泰罗尼亚** |
| **zh-HK**  | **华语 - 中国香港**        |
| **zh-MO**  | **华语 - 中国澳门**        |
| **zh-CN**  | **华语 -中国**             |
| **zh-SG**  | **华语 -新加坡**           |
| **zh-TW**  | **华语 - 中国台湾**        |
| **zh-CHS** | **华语 (简体化)**          |
| **zh-CHT** | **华语 (传统的)**          |
| **hr-HR**  | **克罗埃西亚 -克罗埃西亚** |
| **cs-CZ**  | **捷克 - 捷克**            |
| **da-DK**  | **丹麦文 -丹麦**           |
| **div-MV** | **Dhivehi-马尔代夫**       |
| **nl-BE**  | **荷兰 -比利时**           |
| **nl-NL**  | **荷兰 - 荷兰**            |
| **en-AU**  | **英国 -澳洲**             |
| **en-CA**  | **英国 -加拿大**           |
| **en-ZA**  | **英国 - 南非**            |
| **en-PH**  | **英国 -菲律宾共和国**     |
| **en-NZ**  | **英国 - 新西兰**          |
| **en-GB**  | **英国 - 英国**            |
| **en-US**  | **英国 - 美国**            |
| **fa-IR**  | **波斯语 -伊朗王国**       |
| **fi-FI**  | **芬兰语 -芬兰**           |
| **fr-FR**  | **法国 -法国**             |
| **fr-BE**  | **法国 -比利时**           |
| **fr-MC**  | **法国 -摩纳哥**           |
| **fr-CH**  | **法国 -瑞士**             |
| **gl-ES**  | **加利西亚 -加利西亚**     |
| **ka-GE**  | **格鲁吉亚州 -格鲁吉亚州** |
| **de-DE**  | **德国 -德国**             |
| **de-LU**  | **德国 -卢森堡**           |
| **de-CH**  | **德国 -瑞士**             |
| **el-GR**  | **希腊 -希腊**             |
| **gu-IN**  | **Gujarati-印度**          |
| **he-IL**  | **希伯来 -以色列**         |
| **hi-IN**  | **北印度语 -印度**         |
| **hu-HU**  | **匈牙利的 -匈牙利**       |
| **is-IS**  | **冰岛的 -冰岛**           |
| **it-IT**  | **意大利 -意大利**         |
| **ja-JP**  | **日本 -日本**             |
| **kk-KZ**  | **Kazakh-哈萨克**          |
| **kn-IN**  | **卡纳达语 -印度**         |
| **ko-KR**  | **韩国 -韩国**             |
| **lv-LV**  | **拉脱维亚的 -拉脱维亚**   |
| **lt-LT**  | **立陶宛 -立陶宛**         |
| **ms-BN**  | **马来 -汶莱**             |
| **ms-MY**  | **马来 -马来西亚**         |
| **mr-IN**  | **马拉地语 -印度**         |
| **mn-MN**  | **蒙古 -蒙古**             |
| **nn-NO**  | **挪威 (Nynorsk)- 挪威**   |
| **pl-PL**  | **波兰 -波兰**             |
| **pt-BR**  | **葡萄牙 -巴西**           |
| **pt-PT**  | **葡萄牙 -葡萄牙**         |
| **ro-RO**  | **罗马尼亚语 -罗马尼亚**   |
| **sa-IN**  | **梵文 -印度**             |
| **ru-RU**  | **俄国 -俄国**             |
| **sk-SK**  | **斯洛伐克 -斯洛伐克**     |
| **es-AR**  | **西班牙 -阿根廷**         |
| **es-ES**  | **西班牙 -西班牙**         |
| **sv-SE**  | **瑞典 -瑞典**             |
| **th-TH**  | **泰国 -泰国**             |
| **tr-TR**  | **土耳其语 -土耳其**       |
| **uk-UA**  | **乌克兰 -乌克兰**         |
| **ur-PK**  | **Urdu-巴基斯坦**          |
| **vi-VN**  | **越南 -越南**             |