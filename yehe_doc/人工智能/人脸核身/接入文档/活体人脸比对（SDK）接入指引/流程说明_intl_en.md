# Overall SDK Integration Process

This document introduces the overall integration process of the FaceID SDK (global edition).

## Integration Preparations

- Sign up for a Tencent Cloud account. For more information, see [Signing Up](https://www.tencentcloud.com/document/product/378/17985).
- Complete enterprise identity verification. For more information, see [Enterprise Identity Verification Guide](https://www.tencentcloud.com/document/product/378/10496).
- Log in to the [FaceID console](https://console.intl.cloud.tencent.com/faceid) and activate the service. 
- [Contact us](https://www.tencentcloud.com/document/product/1061/52144) to obtain the latest SDK and license.

## Overall Architecture Diagram

The following diagram shows the architecture of the liveness detection and face comparison SDK integration.

![image.5](https://staticintl.cloudcachetci.com/yehe/backend-news/727J155_image.png)

**FaceID SDK integration includes two parts:**

**Client-side integration**: Integrate the FaceID SDK into the customer's terminal service app. 

**Server-side integration**: Expose the endpoint of your (merchant) application to your (merchant) server so that the merchant application can interact with the merchant server and then access the FaceID SaaS API to obtain the `SdkToken`, which is used throughout the liveness detection and face comparison process and to pull the final verification result.


## Overall Interaction Process

You only need to pass in the token and start the corresponding FaceID SDK's liveness detection method to complete liveness detection and return the result.

1. TencentCloud API for obtaining the token: [GetFaceldTokenIntl](https://xn--todo:-1j5hv03dzqg65khptt93cx0w9j0b/)

2. TencentCloud API for pulling the liveness detection result: [GetFaceIdResultIntl](http://)

The following diagram shows the overall logic of interaction between the SDK, client, and server:

![](https://staticintl.cloudcachetci.com/yehe/backend-news/F5n3129_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_091a5f2d-ebc2-48b3-989e-3fcc1e48881f.png)

 The recommended detailed interaction process is as follows:

1. The customer triggers the merchant application on the terminal to call the liveness verification service scenario.
2. The merchant application sends a request to the merchant server to notify that the liveness detection service token is required for starting liveness verification once.
3. The merchant server passes in relevant parameters to call the TencentCloud API [GetFaceldTokenIntl](https://xn--todo:-1j5hv03dzqg65khptt93cx0w9j0b/).
4. After receiving the request for calling [GetFaceldTokenIntl](https://xn--todo:-1j5hv03dzqg65khptt93cx0w9j0b/), the FaceID SaaS delivers the service token to the merchant server.
5. The merchant server delivers the obtained service token to the customer's merchant application.
6. The merchant application calls the FaceID SDK's startup API **startHuiYanAuth** to pass in the token and configuration information and starts liveness verification.  
7. The FaceID SDK captures and uploads the required user data, including liveness data, to the FaceID SaaS.
8. The FaceID SaaS returns the verification result to the FaceID SDK after completing liveness verification (including the liveness detection and face comparison).
9. The FaceID SDK actively triggers callback to notify the merchant application that the verification is complete and of the verification status.
10. After receiving the callback, the merchant application sends a request to notify the merchant server to obtain the verification result for confirmation.  
11. The merchant server actively calls the FaceID SaaS API [GetFaceIdResultIntl](http://) to pass in the relevant parameters and service token and obtain the verification result.
12. After receiving the request for calling [GetFaceIdResultIntl](https://xn--todo:-1j5hv03dzqg65khptt93cx0w9j0b/), the FaceID SaaS returns the verification result to the merchant server.
13. After receiving the verification result, the merchant server delivers the required information to the merchant application.
14. The merchant application displays the final result on the UI to notify the customer of the verification result.



## Integration

### Server Integration

#### 1. Integration preparations

Before server integration, you need to activate the Tencent Cloud FaceID service and obtain TencentCloud API access key SecretId and SecretKey by following the instructions in [Getting API Key](https://console.tencentcloud.com/cam/capi). In addition, you need to follow the instructions in [Connecting to TencentCloud API] (https://iwiki.woa.com/pages/viewpage.action?pageId=4007951224) to import the SDK package with the programming language you are familiar with to your server modules, to ensure that the TencentCloud API can be successfully called and API requests and responses can be properly processed.

#### 2. Integration process

To ensure that your (merchant) client application interacts with your (merchant) server, the merchant server needs to call the API [**GetFaceIdTokenIntl**](http://) provided by FaceID to obtain `SDKToken`, which is used throughout the liveness detection and face comparison process and used by the API [**GetFaceIdResultIntl**](http://) to obtain the liveness comparison result. The merchant server also needs to provide the corresponding endpoint for the merchant client to call. The following sample code with the Golang language is used as an example to show how to call TencentCloud API on the server and obtain the correct response.

**Note**: This example only demonstrates the processing logic required for interaction between the merchant server and TencentCloud API service. If necessary, you need to implement your own business logic, for example: 

* After you obtain the `SDKToken` using the API **GetFaceIdTokenIntl**, you can return other responses required by the client application to the client along with the `SDKToken`.
* After you obtain the liveness detection and face comparison result using the API **GetFaceIdResultIntl**, you can save the returned photo with the best frame rate for later business logic.

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
	request := faceid.NewApplyLivenessTokenRequest()
	request.SecureLevel = &SecureLevel
	// Step 3: call the Tencent Cloud API through FaceIdClient
	response, err := FaceIdClient.ApplyLivenessToken(request)

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
	request := faceid.NewGetLivenessResultRequest()
	request.SdkToken = &SdkToken
	// Step 3: call the Tencent Cloud API through FaceIdClient
	response, err := FaceIdClient.GetLivenessResult(request)

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

func main(){
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

#### 3. API testing 

After you complete the integration, you can test whether the current integration is correct by running the postman or curl command. To be specific, access the API (http://ip:port/api/v1/get-token) to check whether `SdkToken` is returned and access the API (http://ip:port/api/v1/get-result) to check whether the value of the `Result` field is 0. Through these results, you can determine whether the server integration is successful. For details on responses, see API introduction.


### Integration with Android

#### 1. Dependent environment

The current FaceID SDK for Android is supported by API 19 (Android 4.4) or later.

#### 2. SDK integration steps

1. Add the files **huiyansdk_android_overseas_1.0.9.6_release.aar**, **tencent-ai-sdk-youtu-base-1.0.1.39-release.aar**, **tencent-ai-sdk-common-1.1.36-release.aar**, and **tencent-ai-sdk-aicamera-1.0.22-release.aar** (the specific version numbers of the files downloaded from the official website shall prevail) to the **libs** directory of your project. 

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/SDK%E6%96%87%E6%A1%A3%E5%9B%BE%E5%BA%8A/tuyong/oversea_lib.png)

2. Configure **build.gradle** in your project as follows:

```groovy
// Set .so architecture filtering in NDK (using armeabi-v7a as an example)
ndk {
    abiFilters 'armeabi-v7a'
}

dependencies {
    // Import the FaceID SDK
    implementation files("libs/huiyansdk_android_overseas_1.0.9.5_release.aar")
    // FaceID general algorithm SDK
    implementation files("libs/tencent-ai-sdk-youtu-base-1.0.1.32-release.aar")
    // Common capability components
    implementation files("libs/tencent-ai-sdk-common-1.1.27-release.aar")
    implementation files("libs/tencent-ai-sdk-aicamera-1.0.18-release.aar")

  	// Third-Party libraries that the FaceID SDK depends on
    // gson
    implementation 'com.google.code.gson:gson:2.8.5'
}
```

3. Make the necessary permission declaration in the `AndroidManifest.xml` file.

```xml
<!-- Camera permission -->
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature
    android:name="android.hardware.camera"
    android:required="true" />
<uses-feature android:name="android.hardware.camera.autofocus" />

<!-- Permissions required by the SDK -->
<uses-permission android:name="android.permission.INTERNET" />
<!-- Optional permissions for the SDK -->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

   If your app needs to be compatible with Android 6.0 or later, in addition to declaring the above permissions in the `AndroidManifest.xml` file, you need to add the code **Dynamically apply for permissions**.

#### 3. API initialization 

	This API is called during app initialization, which is mainly used to perform some initialization operations for the SDK. We recommend you call this API in `Application`.

```java
@Override
public void onCreate() {
    super.onCreate();
    instance = this;
    // Initialize the SDK during app initialization
    HuiYanOsApi.init(getApp());
}
```

#### 4. Start the liveness verification API

```java
// HuiYanOs parameters
HuiYanOsConfig huiYanOsConfig = new HuiYanOsConfig();
// The license file is placed in `assets`.
huiYanOsConfig.setAuthLicense("YTFaceSDK.license");
if (compatCheckBox.isChecked()) {
    huiYanOsConfig.setPageColorStyle(PageColorStyle.Dark);
}
// Whether to return the best frame
if (needBestImageCB.isChecked()) {
    huiYanOsConfig.setNeedBestImage(true);
}
// Start liveness verification. `currentToken` is the token distributed by the backend.
HuiYanOsApi.startHuiYanAuth(currentToken, huiYanOsConfig, new HuiYanOsAuthCallBack() {
    @Override
    public void onSuccess(HuiYanOsAuthResult authResult) {
        showToast("Liveness verification passed.");
        if (!TextUtils.isEmpty(authResult.getBestImage())) {
           CommonUtils.decryptBestImgBase64(authResult.getBestImage(), false);
        }
    }

    @Override
    public void onFail(int errorCode, String errorMsg, String token) {
        String msg = "Liveness verification failed " + "code: " + errorCode + " msg: " + errorMsg + " token: " + token;
        Log.e(TAG, "onFail" + msg);
        showToast(msg);
    }
});
```

[HuiYanOsAuthResult](https://iwiki.woa.com/pages/viewpage.action?pageId=4007948264) is the returned result of successful liveness verification. The final liveness verification result can be obtained by accessing [GetFaceldResultIntl](//todo) through the token.

**Note**: You need to contact the customer service to apply for the **"YTFaceSDK.license"** file, and then place the license file in the `Assets Folder`.

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/license%E5%AD%98%E6%94%BE%E8%B7%AF%E5%BE%84.png)

#### 5. Release SDK resources

	Before your app exits, you can call the API to release SDK resources.

```java
@Override
protected void onDestroy() {
    super.onDestroy();
    // Release the resources upon exit
    HuiYanOsApi.release();
}
```

#### 6. Configure obfuscation rules

  If the obfuscation feature is enabled for your app, add the following to your obfuscation file to ensure the normal running of the SDK:

```java
# The following FaceID SDK obfuscation rules should be added:
-keep class com.tencent.could.huiyansdk.** {*;}
-keep class com.tencent.could.aicamare.** {*;}
-keep class com.tencent.could.component.** {*;}
-keep class com.tencent.youtu.** {*;}
-keep class com.tenpay.utils.SMUtils {*;}
```


### Integration with iOS

#### 1. Dependent environment

1. Development environment: Xcode 11.0 or later
2. The FaceID SDK for iOS is only supported by iOS 9.0 or later.

#### 2. SDK integration steps
##### Manual integration

1. Import libraries and files.

Click `Link Binary With Libraries` to add frameworks.

2. The SDK depends on the following libraries:

```
├──HuiYanSDK.framework
└──YtSDKKitSilentLiveness.framework
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

3. Click `Link Binary With Libraries` to add system frameworks.

```
├── AVFoundation.framework
├── libc++.tbd
└── Accelerate.framework
```

4. Import the model in `Copy Bundle Resources`.

```
└── face-tracker-v001.bundle
```

5. Import the resource file in `Copy Bundle Resources`.

```
└── HuiYanSDKUI.bundle
```

##### Integration by using pod

1. Copy the `CloudHuiYanSDK_FW` folder to the directory at the same level as that of the integration project `Podfile`.
2. Set the following in `Podfile`:

```ruby
target 'HuiYanAuthDemo' do
  use_frameworks! 
  pod 'CloudHuiYanSDK_FW', :path => './CloudHuiYanSDK_FW'
end
```

3. Run `pod install`.

> For the file levels and specific settings, see the demo.

##### `Build Phases` settings

1. Click `Other Linker Flags` to add **-ObjC**.
2. Integrate `ViewController.m` and set the extension to `.mm` (for a Swift project, add the system library `libc++.tbd`).

##### Permission settings

As the SDK requires a mobile network and camera permission, include the following key-value pair in `info.plist` of the main project to add the corresponding permission declaration.

```xml
<key>Privacy - Camera Usage Description</key>
<string>FaceID requires you to grant the camera permission for face recognition.</string>
```

#### 3. Start the liveness detection API

```objective-c
#import <HuiYanSDK/HuiYanOsApi.h>
#import <HuiYanSDK/HuiYanOSKit.h>

  // Get the token
    NSString *faceToken = self.tokenTextField.text;
    // Configure the SDK
    HuiYanOsConfig *config = [[HuiYanOsConfig alloc] init];
    // Set the license
    config.authLicense = [[NSBundle mainBundle] pathForResource:@"xxx.lic" ofType:@""];
    // Timeout configuration for the preparation stage
    config.prepareTimeoutMs = 20000;
    // Timeout configuration for the detection stage
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
[HuiYanOsAuthResult](https://iwiki.woa.com/pages/viewpage.action?pageId=4007948264) is the returned result of successful liveness verification. The final liveness verification result can be obtained by accessing [GetFaceldResultIntl](//todo: API released at the official website) through the token.

**Note**: Currently, you need to contact the customer service to apply for the **"xxx.lic"** file actively.

#### 4. Release SDK resources

	Before your app exits, you can call the API to release SDK resources.

```objective-c
// Release the resources before exit
- (void)dealloc {
    [HuiYanOsApi release];
}
```

//TODO: add the demo download address.