

## 接入准备

- 注册腾讯云企业账号，请见[注册指引](https://www.tencentcloud.com/zh/document/product/378/17985)
- 完成企业实名认证，请见[企业实名指引](https://www.tencentcloud.com/zh/document/product/378/10496)
- 登陆慧眼控制台[开通服务](https://console.intl.cloud.tencent.com/faceid) 
- [联系我们](https://www.tencentcloud.com/zh/document/product/1061/52144)获取最新的SDK及License

## 整体架构图

下图为活体人脸比对SDK集成的架构图

![image.5](https://staticintl.cloudcachetci.com/yehe/backend-news/727J155_image.png)

**慧眼SDK集成包括两部分：**

**客户端集成：** 将慧眼SDK集成到客户终端业务App中。 

**服务器端集成：** 在您的（商家）服务器中公开您的（商家）应用程序的端点，以便商家应用程序可以与商家服务器交互，然后访问 FaceId SaaS API 以获取串联活体比对流程的`SdkToken`以及通过`SdkToken`拉取最终的核身结果。


## 整体交互流程

集成方只需要传入Token并启动对应的慧眼SDK的活体检测方法，便可以完成活体检测，并返回活体结果。

1. Token的获取可以参考云API接口：[GetFaceldTokenIntl](https://www.tencentcloud.com/document/product/1061/54556)

2. 用户主动拉取活体结果的云API接口: [GetFaceIdResultIntl](https://www.tencentcloud.com/document/product/1061/54557)

下图展示了SDK、客户端以及服务器端的整体交互逻辑，图中负责模块解析：

![](https://staticintl.cloudcachetci.com/yehe/backend-news/F5n3129_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_091a5f2d-ebc2-48b3-989e-3fcc1e48881f.png)

 具体的推荐交互流程详细交互如下：

1. 用户触发终端 Merchant Application 准备调用核身业务场景。
2. Merchant Application 发送请求到 Merchant Server，告知启动一次核身业务需要活体业务Token。
3. Merchant Server 传入相关参数调用云API接口[GetFaceldTokenIntl](https://www.tencentcloud.com/document/product/1061/54556)。
4. FaceID SaaS 接收到[GetFaceldTokenIntl](https://www.tencentcloud.com/document/product/1061/54556)调用后，下发此次业务的token给 Merchant Server。
5. Merchant Server可以将获取到的业务Token，下发给客户的 Merchant Application。
6. Merchant Application 调用慧眼SDK的启动接口**startHuiYanAuth**传入token与配置信息，开始核身验证。
7. FaceID SDK 捕捉并上传所需的用户数据，包括活体数据等，上传至 FaceID SaaS 。
8. FaceID SaaS 在完成核身检测（包括活体与比对流程）以后，会返回结果给 FaceID SDK 。
9. FaceID SDK 主动触发回调给 Merchant Application 通知核验完成以及核验状态。
10. Merchant Application 接收到回调以后，可以发送请求通知 Merchant Server去主动获取本次核身的结果，进行确认检查。
11. Merchant Server主动调用 FaceID SaaS 的接口[GetFaceIdResultIntl](https://www.tencentcloud.com/document/product/1061/54557)传入相关参数以及本次业务的Token，去获取本次核身的结果。
12. FaceID SaaS 接收到[GetFaceIdResultIntl](https://www.tencentcloud.com/document/product/1061/54557)调用后，会返回本次核身的结果到 Merchant Server。
13. Merchant Server接收到本次核身的结果后，可以下发需要的信息到 Merchant Application。
14.  Merchant Application 展示最后的结果，呈现在UI界面上，告知用户核身的结果。



## 接入流程

### 服务器端集成

#### 1、集成准备

在服务端集成之前，你需要按照[获取API秘钥指引](https://console.tencentcloud.com/cam/capi)中的说明进行操作，开通腾讯云慧眼服务，并且拿到了腾讯云api访问秘钥SecretId和SecretKey。除此之外你还需要按照[连接腾讯云API接口](https://www.tencentcloud.com/zh/document/product/1061/54960)中的操作流程，引入你所熟悉开发语言的SDK包到你服务端模块中，以确保可以成功调用腾讯云API以及正确处理API请求和响应。

#### 2、开始集成

为了确保你的（商户）客户端应用程序能够跟你的（商户）服务端正常交互，商户服务端需要调用慧眼提供的API接口 [**GetFaceIdTokenIntl**](https://www.tencentcloud.com/document/product/1061/54556) 获取SDKToken串联整个活体比对流程以及调用 [**GetFaceIdResultIntl**](https://www.tencentcloud.com/document/product/1061/54557) 接口获取活体比对结果，商户服务端需要提供相应的端点给商户客户端调用，下面的示例代码使用 Golang语言作为案例，展示如何在服务端调用腾讯云API接口并拿到正确的响应结果。

**注意：** 该示例中仅仅演示商户服务端与腾讯云API服务交互所需要的处理逻辑，如果有需要的话你需要自己实现你的业务逻辑，比如：

* 当你通过 **GetFaceIdTokenIntl** 接口获取活体比对SDKToken之后，可以将客户端应用程序需要的其他响应同SDKToken一并返回给客户端。
* 当你通过 **GetFaceIdResultIntl** 接口获取活体比对结果之后，可以将返回的最佳帧照片保存起来，以便后续业务逻辑使用。

```go
var FaceIdClient *faceid.Client

func init() {
	// Instantiate a client configuration object. You can specify the timeout period and other configuration items
	prof := profile.NewClientProfile()
	prof.HttpProfile.ReqTimeout = 60
	// TODO replace the SecretId and SecretKey string with the API SecretId and SecretKey
	credential := cloud.NewCredential("SecretId", "SecretKey")
	var err error
	// Instantiate the client object of the requested faceid
	FaceIdClient, err = faceid.NewClient(credential, "ap-singapore", prof)
	if nil != err {
		log.Fatal("FaceIdClient init error: ", err)
	}
}

// GetFaceIdToken get token
func GetFaceIdToken(w http.ResponseWriter, r *http.Request) {
	log.Println("get face id token")
	// Step 1: ... parse parameters
	_ = r.ParseForm()
	var SecureLevel = r.FormValue("SecureLevel")

	// Step 2: instantiate the request object and provide necessary parameters
	request := faceid.NewGetFaceIdTokenIntlRequest()
	request.SecureLevel = &SecureLevel
	// Step 3: call the Tencent Cloud API through FaceIdClient
	response, err := FaceIdClient.GetFaceIdTokenIntl(request)

	// Step 4: process the Tencent Cloud API response and construct the return object
	if nil != err {
		_, _ = w.Write([]byte("error"))
		return
	}
	SdkToken := response.Response.SdkToken
	apiResp := struct {
		SdkToken *string
	}{SdkToken: SdkToken}
	b, _ := json.Marshal(apiResp)

	// ... more codes are omitted

	//Step 5: return the service response
	_, _ = w.Write(b)
}

// GetFaceIdResult get result
func GetFaceIdResult(w http.ResponseWriter, r *http.Request) {
	// Step 1: ... parse parameters
	_ = r.ParseForm()
	SdkToken := r.FormValue("SdkToken")
	// Step 2: instantiate the request object and provide necessary parameters
	request := faceid.NewGetFaceIdResultIntlRequest()
	request.SdkToken = &SdkToken
	// Step 3: call the Tencent Cloud API through FaceIdClient
	response, err := FaceIdClient.GetFaceIdResultIntl(request)

	// Step 4: process the Tencent Cloud API response and construct the return object
	if nil != err {
		_, _ = w.Write([]byte("error"))
		return
	}
	result := response.Response.Result
	apiResp := struct {
		Result *string
	}{Result: result}
	b, _ := json.Marshal(apiResp)

	// ... more codes are omitted

	//Step 5: return the service response
	_, _ = w.Write(b)
}

func main() {
	// expose endpoints
	http.HandleFunc("/api/v1/get-token", GetFaceIdToken)
	http.HandleFunc("/api/v1/get-result", GetFaceIdResult)
	// listening port
	err := http.ListenAndServe(":8080", nil)
	if nil != err {
		log.Fatal("ListenAndServe error: ", err)
	}
}
```

#### 3、接口测试

当你完成了集成之后，可以通过postman或者curl命令来测试当前的集成是否正确，通过访问http://ip:port/api/v1/get-token 接口查看是否正常返回 `SdkToken` , 访问http://ip:port/api/v1/get-result 接口查看 `Result` 字段的响应是否为0以判断服务端集成是否成功，具体的响应结果详见API接口部分的介绍。


### Android端集成

#### 1、依赖环境

当前Android端慧眼SDK适用于API 19 (Android 4.4) 及以上版本。

#### 2、SDK接入步骤

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

#### 3、初始化接口

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

#### 4、启动核身检测接口

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
// 启动方法，开始的活体，currentToken为后台下发数据
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

[HuiYanOsAuthResult](https://www.tencentcloud.com/zh/document/product/1061/54964)为活体成功的返回结果, 最终的核身结果可以通过token，访问[GetFaceldResultIntl](https://www.tencentcloud.com/zh/document/product/1061/54557)获取。

**注意：**当前的"YTFaceSDK.license"文件是需要您主动申请的，暂时您可以联系客服人员进行license申请。将申请完成后的license文件放到assets文件下。

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/license%E5%AD%98%E6%94%BE%E8%B7%AF%E5%BE%84.png)

#### 5、SDK资源释放

	在您APP退出使用的时候，可以调用SDK资源释放接口

```java
@Override
protected void onDestroy() {
    super.onDestroy();
    // 退出时做资源释放
    HuiYanOsApi.release();
}
```

#### 6、混淆规则配置

  如果您的应用开启了混淆功能，为确保SDK的正常使用，请把以下部分添加到您的混淆文件中。

```java
#慧眼SDK的混淆包含
-keep class com.tencent.could.huiyansdk.** {*;}
-keep class com.tencent.could.aicamare.** {*;}
-keep class com.tencent.could.component.** {*;}
-keep class com.tencent.youtu.** {*;}
-keep class com.tenpay.utils.SMUtils {*;}
```


### iOS端集成

#### 1、依赖环境

1. 开发环境 Xcode 11.0 或以上
2. 慧眼iOS SDK 适用于手机iOS9.0及以上版本

#### 2、SDK接入步骤
##### 手动接入方式

1. 导入相关库及文件

Link Binary With Libraries导入相关Framework

2. SDK依赖的库如下

```
├──HuiYanSDK.framework
├──YtSDKKitSilentLiveness.framework
├──YtSDKKitReflectLiveness.framework
├──YtSDKKitActionLiveness.framework
├──YtSDKKitFramework.framework
├──tnnliveness.framework
├──YTFaceAlignmentTinyLiveness.framework
├──YTFaceTrackerLiveness.framework
├──YTFaceDetectorLiveness.framework
├──YTPoseDetector.framework
├──YTCommonLiveness.framework
└──YTFaceLiveReflect.framework
```

3. Link Binary With Libraries导入系统Framework

```
├── AVFoundation.framework
├── libc++.tbd
└── Accelerate.framework
```

4. Copy Bundle Resources中导入模型

```
└── face-tracker-v001.bundle
```

5. Copy Bundle Resources导入资源文件

```
└── HuiYanSDKUI.bundle
```

##### 使用Pod方式接入

1. 将CloudHuiYanSDK_FW文件夹复制到集成项目Podfile同级目录下
2. 在Podfile设置

```ruby
target 'HuiYanAuthDemo' do
  use_frameworks! 
  pod 'CloudHuiYanSDK_FW', :path => './CloudHuiYanSDK_FW'
end
```

3. pod install 更新

>?文件层级和具体的设置可以参考demo。
>- [iOS demo](https://github.com/TencentCloud/huiyan-faceid-demo/tree/main/faceid-iOS-demo)
>- [Android demo](https://github.com/TencentCloud/huiyan-faceid-demo/tree/main/faceid-android-demo)

##### Build Phases设置

1. Other Linker Flags 新增 **-ObjC**
2. 接入ViewController.m 设置后缀为.mm(swift 工程添加系统库libc++.tbd)

##### 权限设置

SDK需要手机网络及 摄像头使用权限，请添加对应的权限声明。在主项目info.plist 配置中添加下面key-value值

```xml
<key>Privacy - Camera Usage Description</key>
<string>人脸核身需要开启您的摄像头权限，用于人脸识别</string>
```

#### 3、开启活体检测接口

```objective-c
#import <HuiYanSDK/HuiYanOsApi.h>
#import <HuiYanSDK/HuiYanOSKit.h>

  //获取token
    NSString *faceToken = self.tokenTextField.text;
    // 配置SDK
    HuiYanOsConfig *config = [[HuiYanOsConfig alloc] init];
    //设置lic
    config.authLicense = [[NSBundle mainBundle] pathForResource:@"xxx.lic" ofType:@""];
    //准备阶段超时配置
    config.prepareTimeoutMs = 20000;
    //检测阶段超时配置
    config.authTimeOutMs = 20000;
    config.isDeleteVideoCache = YES;
    config.languageType = EN;
    //    config.userLanguageFileName = @"ko";
    //    config.userLanguageBundleName = @"UseLanguageBundle";
    config.iShowTipsPage = YES;
    config.isGetBestImg = YES;

    [[HuiYanOSKit sharedInstance] startHuiYaneKYC:faceToken withConfig:config
                                  witSuccCallback:^(HuiYanOsAuthResult * _Nonnull authResult, id  _Nullable reserved) {
        NSString *bestImg = authResult.bestImage;
        NSString *token = authResult.faceToken;
        
    } withFailCallback:^(int errCode, NSString * _Nonnull errMsg, id  _Nullable reserved) {
        NSString *showMsg = [NSString stringWithFormat:@"err:%d:%@",errCode,errMsg];
        NSLog(@"err:%@",showMsg);
    }];
```

[HuiYanOsAuthResult](https://www.tencentcloud.com/zh/document/product/1061/54964)为活体成功的返回结果, 最终的核身结果可以通过token，访问[GetFaceldResultIntl](https://www.tencentcloud.com/zh/document/product/1061/54557)获取。

>!当前的"xxx.lic"文件是需要您主动申请的，暂时您可以联系客服人员进行license申请

#### 4、SDK资源释放

在您APP退出使用的时候，可以调用SDK资源释放接口


```objective-c
// 退出时做资源释放
- (void)dealloc {
    [HuiYanOsApi release];
}
//[iOS demo](https://github.com/TencentCloud/huiyan-faceid-demo/tree/main/faceid-iOS-demo)
[Android demo](https://github.com/TencentCloud/huiyan-faceid-demo/tree/main/faceid-android-demo)
```
