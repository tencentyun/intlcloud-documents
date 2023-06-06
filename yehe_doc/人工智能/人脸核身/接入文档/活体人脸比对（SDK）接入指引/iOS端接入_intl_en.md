



### Development Preparations

1. Sign up for a Tencent Cloud account and log in to the eKYC console to activate the service.
2. Download the eKYC SDK at the SDK download address and integrate it locally.
3. Apply for the license file.

### eKYC SDK for iOS Integration Process

#### Environment Requirements

1. Development environment: Xcode 11.0 or later
2. The eKYC SDK for iOS is only supported by iOS 9.0 or later.

#### **1. Manual integration**

1. Import libraries and files

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

#### 2. Integration by using pod

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

#### `Build Phases` settings

1. Click `Other Linker Flags` to add **-ObjC**.
2. Integrate `ViewController.m` and set the extension to `.mm` (for a Swift project, add the system library `libc++.tbd`).

#### Permission settings

As the SDK requires a mobile network and camera permission, include the following key-value pair in `info.plist` of the main project to add the corresponding permission declaration.

```xml
<key>Privacy - Camera Usage Description</key>
<string>eKYC requires you to grant the camera permission for face recognition.</string>
```



## Full Integration Process

#### Overall process

The following diagram shows the overall logic of interaction between the SDK, client, and server.

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan_overseas/image/clipboard_20210412_035342.png)



#### SDK APIs Use Instructions

##### Initializing configuration and pulling parameters

Before using the eKYC SDK, you need to call this method to pass in basic configuration parameters and use the callback to pull the local configuration parameter information.

```objective-c
// HuiYanOs parameters
HuiYanOsConfig *config = [[HuiYanOsConfig alloc] init];
// The path of the license file in the bundle
config.authLicense = [[NSBundle mainBundle] pathForResource:@"YTFaceSDK.license" ofType:@""];
// The timeout period of local liveness detection in ms
config.authTimeOutMs = 20000;
//Language directory file in **HuiYanSDKUI.bundle**
config.setLanguageFileName = @"th";//th.lproj
// Pull the local configuration parameter information before starting identity verification
[HuiYanOsApi startGetAuthConfigData:config withSuccCallback:^(NSString * _Nonnull result) {
  	// The configuration information is obtained successfully and sent to the server to get the verification start configuration, and the server delivers the light sequence (implemented by yourself).
  	NSString *liveData = [self getLiveDataWith:result];
} withFialCallback:^(int errCode, NSString * _Nonnull errMsg) {
  	// Failed to get configuration parameters (implemented by yourself)
    NSLog(@"errCode:%d, errMsg:%@", errCode, errMsg);
}];
```

##### Performing subsequent liveness detection steps

After you request the configuration information from the server, pass in `LightData` (identity verification light sequence) delivered by the server through this API to continue the local identity verification.

```objective-c
[HuiYanOsApi startAuthByLightData:liveData withSuccCallback:^(NSData * _Nonnull data, NSString * _Nonnull videoPath) {
     	// Result data of successful liveness detection
  		// 1. Send the local verification data to the server for comparison and verification to get the final result (implemented by yourself)
		 	[self checkAuthResultByData:data];
			// 2. Process the local identity verification video `videoPath` (implemented by yourself)
			[self dealWithAuthVideo:videoPath];
} withFialCallback:^(int errCode, NSString * _Nonnull errMsg) {
  		// An error occurred. The local identity verification failed.
      NSLog(@"errCode:%d, errMsg:%@", errCode, errMsg);
}];
```

>**Note**: If an exception occurs with `getLightData`, you need to exit the SDK by calling the `[HuiYanOsApi startAuthByLightData:nil withSuccCallback:nil withFailCallback:nil]` method to end the current SDK session, and the error will be returned in `FailCallback` of `startGetAuthConfigData`.
>
> For a Swift project, you can call `HuiYanOsApi.stopAuth`.

##### API for releasing SDK resources

Before your app exits, you can call the API to release SDK resources.

```objective-c
// Release the resources before exit
- (void)dealloc {
    [HuiYanOsApi release];
}
```

### API Description

The eKYC SDK mainly involves the following classes: HuiYanOsApi (API class), HuiYanOsConfig (configuration parameter class), and HuiYanConfigCallback and HuiYanResultCallBack (result and callback classes).

#### HuiYanOsApi

| API                                                   | Feature Description                                             |
| ----------------------------------------------------- | ---------------------------------------------------- |
| [release()](#release())                               | Releases resources                                         |
| [startGetAuthConfigData()](#startGetAuthConfigData()) | Gets the local configuration information of the eKYC SDK                        |
| [startAuthByLightData()](#startAuthByLightData())     | Passes in the light sequence obtained by the server to continue the liveness detection for identity verification  |



#### release()

```objective-c
+ (void)release;
```

Feature:

	It is an API for releasing eKYC SDK resources.

#### startGetAuthConfigData()

```objective-c
+ (void)startGetAuthConfigData:(HuiYanOsConfig *)huiYanOsConfig
              withSuccCallback:(HuiYanConfigSuccCallback)huiYanConfigSuccCallback
              withFailCallback:(HuiYanConfigFailCallback)huiYanConfigFailCallback;
```

Feature:

It is a configuration parameter pulled by the eKYC SDK during local detection in order to obtain the light sequence in subsequent steps.

Input parameters:

| Parameter Type | Parameter | Description        |
| ----------------------------------------------------- | ------------------------ | ---------------------- |
| [HuiYanOsConfig](#HuiYanOsConfig)                     | huiYanOsConfig           | Configuration parameter             |
| [HuiYanConfigCallback](#HuiYanConfigCallback) | configCallback | Callback for successful pull of configuration result |
| [HuiYanConfigFailCallback](#HuiYanConfigFailCallback) | huiYanConfigFailCallback | Callback for failing to pull configuration result |



#### startAuthByLightData()

```objective-c
+ (void)startAuthByLightData:(NSString *)lightData
         withSuccCallback:(HuiYanResultSuccCallback)huiYanResultSuccCallback
         withFailCallback:(HuiYanResultFailCallback)huiYanResultFailCallback;
```

Feature:

​	It is an API used to pass in the light sequence data pulled from the server to the eKYC SDK in order to continue the identity verification process for the local detection result.

Input parameters:

| Parameter Type | Parameter | Description        |
| ----------------------------------------------------- | ------------------------ | ------------------------------------------ |
| NSString                                              | lightData                | Base64-encoded light sequence requested from the server for starting identity verification |
| [HuiYanResultSuccCallback](#HuiYanResultSuccCallback) | huiYanResultSuccCallback | Callback for local identity verification success                     |
| [HuiYanResultFailCallback](#HuiYanResultFailCallback) | huiYanResultFailCallback | Callback for local identity verification failure                     |



#### HuiYanOsConfig

"HuiYanOsConfig" is the configuration entity class during eKYC SDK startup, which mainly covers the following attributes:

| Type           | Name               | Description                                 | Default Value               |
| ----------------------------- | ---------------------- | ------------------------------------------------------------ | ----------------- |
| NSString                     | authLicense        | Name of the license file requested for user identity verification | Empty                |
| long | authTimeOutMs|Liveness detection timeout period | 10,000 ms (10s) |
| long | prepareTimeoutMs|Detection timeout period in the preparation stage | 0 |
| [HYShowTimeOutMode](#HYShowTimeOutMode) | showTimeOutMode|Stage in which the countdown is displayed | HYShowTimeOutMode_PREPARE|HYShowTimeOutMode_ACTION |
| BOOL                                                         | isDeleteVideoCache     | Whether to delete the local cache of the identity verification video                                   | YES               |
| BOOL                          | iShowTipsPage          | Whether to display the guide page                                               | NO                |
| NSString | userUIBundleName| Custom UI bundle filename; for example, set `UserUIBundle` for `UserUIBundle.bundle` | nil |
| NSString | userLanguageFileName   | Custom languageBundle name; for example, set `UseLanguage` for `UseLanguage.bundqle` | nil               |
| NSString | userLanguageBundleName | Custom local filename for internationalization; for example, set `en` for `en.lproj`           | nil               |
| [LanguageType](#LanguageType) | languageType           | Text language settings inside the SDK                                          | DEFAULT           |
| BOOL                          | isGetBestImg           | Whether to get the best frame image in simplified mode                             | NO               |
| NSString | setLanguageFileName | Language file directory name added in **HuiYanSDKUI.bundle** has the highest priority by default | nil |
#### HuiYanConfigSuccCallback

Callback for initialization and successful acquisition of the local configuration

```objective-c
/**
 * Callback for successful initialization
 *
 * @param result: Initialization callback data
 */
typedef void (^HuiYanConfigSuccCallback)(NSString * _Nonnull result);
```

#### HuiYanConfigFailCallback

Callback for initialization and failed acquisition of the local configuration

```objective-c
/**
 * Callback for failed initialization
 *
 * @param errCode: Error code
 * @param errMsg: Error message
 */
typedef void (^HuiYanConfigFailCallback)(int errCode, NSString * _Nonnull errMsg);
```



#### HuiYanResultSuccCallback

Callback for successful local identity verification process and local result acquisition

```objective-c
/**
 * Callback for successful liveness verification
 *
 * @param data Data for comparison after Gzip compression
 * @param videoPath: Path of the liveness video
 */
typedef void (^HuiYanResultSuccCallback)(NSData * _Nonnull data, NSString * _Nonnull videoPath);
```

#### HuiYanResultFailCallback

Callback for failed local identity verification and local result acquisition

```objective-c
/**
 * Callback for failed liveness verification
 *
 * @param errCode: Error code
 * @param errMsg: Error message
 */
typedef void (^HuiYanResultFailCallback)(int errCode, NSString * _Nonnull errMsg);
```

#### LanguageType 

Internationalized strings included in the SDK

```objective-c
typedef enum : NSUInteger {
    DEFAULT = 0,// Same as the system settings
    ZH_HANS,// Simplified Chinese
    ZH_HANT,// Traditional Chinese
    ZH_HK,// Traditional Chinese (Hong Kong, China)
    ZH_TW,// Traditional Chinese (Taiwan, China)
    EN,// English
    MS,// Malay
    RU,// Russian
    JA,// Japanese
    CUSTOMIZE_LANGUAGE, // Custom language
} LanguageType;
```

#### HYShowTimeOutMode
```objective-c
typedef NS_OPTIONS(int, HYShowTimeOutMode) {
    HYShowTimeOutMode_TIMEOUT_HIDDEN = 1 << 0,// Hidden the countdown in all stages
    HYShowTimeOutMode_PREPARE = 1 << 1,// Preparation stage countdown
    HYShowTimeOutMode_ACTION = 1 << 3,// Action stage countdown
};
```

## Simplified Integration Process

The current version includes interactions with backend APIs for getting a token to start the verification process.

1. Get the verification token by using the server API
2. Start the eKYC SDK to enter the verification page
3. Process the best frame (if any) after verification ends
4. Get the verification result through the token

Overall Process

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan_overseas/image/huiyan_overseas_2.png)

#### SDK APIs Use Instructions
Start the liveness detection process in the eKYC SDK.

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



### API Description

Integration with the simplified eKYC SDK mainly involves the following classes: HuiYanOSKit (API class), HuiYanOsConfig (configuration parameter class), and HuiYanOKitSuccCallback and HuiYanOKitFailCallback (result and callback classes).

#### HuiYanOSKit
| API                                                   | Feature Description                                             |
| ------------------------------------- | ----------------------- |
| [startHuiYaneKYC()](#startHuiYaneKYC) | Starts the liveness detection process in the eKYC SDK. |
| [sdkVersion()](#release())            | Gets the SDK version number.           |

#### startHuiYaneKYC

Feature:

Starts and configures the liveness detection SDK and calls back the result or error.

```objective-c
/// Start the liveness detection process
/// @param faceToken token
/// @param kitConfig SDK configuration
/// @param succCallback Callback for successful liveness detection
/// @param failCallback Callback for failed liveness detection
- (void)startHuiYaneKYC:(NSString *)faceToken withConfig:(HuiYanOsConfig *)kitConfig
        witSuccCallback:(HuiYanOKitSuccCallback)succCallback
       withFailCallback:(HuiYanOKitFailCallback)failCallback;
```

Input parameters:

| Parameter Type | Parameter Name | Description        |
| ------------------------------------------------- | ------------ | ---------------- |
| NSSting                                           | faceToken    | Liveness verification process token     |
| [HuiYanOsConfig](#HuiYanOsConfig)                 | kitConfig    | SDK configuration class        |
| [HuiYanOKitSuccCallback](#HuiYanOKitSuccCallback) | succCallback | Callback for successful liveness detection |
| [HuiYanOKitFailCallback](#HuiYanOKitFailCallback) | failCallback | Callback for failed liveness detection |

#### HuiYanOsAuthResult

| Parameter Type | Parameter Name | Description        |
| ------- | --------- | ---------------------------------------------- |
| NSSting | faceToken | Liveness verification process token                                 |
| NSSting | bestImage | Base64-encoded best frame image returned upon success if best frame return is enabled |

#### HuiYanOKitSuccCallback

```objective-c
/**
 * Callback for successful liveness detection
 *
 * @param authResult  Liveness verification result
 * @param reserved: Reserved
 */
typedef void (^HuiYanOKitSuccCallback)(HuiYanOsAuthResult * _Nonnull authResult, id _Nullable reserved);
```

#### HuiYanOKitFailCallback

```objective-c
/**
 * Callback for failed liveness detection
 *
 * @param errCode: Error code
 * @param errMsg: Error message
 * @param reserved: Reserved
 */
typedef void (^HuiYanOKitFailCallback)(int errCode, NSString * _Nonnull errMsg ,id _Nullable reserved);
```



## SDK Error Codes (iOS)

```
    HY_SUCCESS                              = 0,
    // Parameter initialization exception
    HY_INITIALIZATION_PARAMETER_EXCEPTION   = 210,
    // Bundle configuration exception
    HY_BUNDLE_CONFIGURATION_EXCEPTION       = 211,
    // YouTu configuration exception
    HY_YTSDK_CONFIGURATION_EXCEPTION        = 212,
    // Call the initialization API first
    HY_PLEASE_CALL_FIRST_INIT_API           = 213,
    // SDK authorization failed
    HY_SDK_AUTH_FAILED                      = 214,
    // The user manually canceled the detection
    HY_USER_VOLUNTARILY_CANCELED            = 215,
    // Local face authentication with the SDK failed
    HY_YTSDK_LOCAL_AUTH_FAILED              = 216,
    // Failed to enable the camera
    HY_CAMERA_OPEN_FAIL                     = 217,
    // Do not switch the application during identity verification
    HY_DONOT_SWITCH_APPS                    = 218,
    // Camera permission exception
    HY_CAMEREA_PERMISSION_EXCEPTION         = 219,
    // Failed to trim the video
    HY_SDK_VEDIO_CUT_EXCEPTION              = 220,
    // Invalid reflection data format
    HY_LIGHT_DATA_FORMAT_EXCEPTION          = 221
```



## Setting a Custom SDK Language

1. Add the custom `UseLanguage.bundle` to the project (Copy Bundle Resources).



![image_1](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/SDK%E6%96%87%E6%A1%A3%E5%9B%BE%E5%BA%8A/iOS%E6%96%87%E6%A1%A3%E5%9B%BE%E5%BA%8A/huiyan/img_10.png)

2. Configure the settings as follows.

```
HuiYanOsConfig *config = [[HuiYanOsConfig alloc] init];
config.languageType = CUSTOMIZE_LANGUAGE;  
config.userLanguageFileName = @"ko";// For example, set `ko.lproj`  
config.userLanguageBundleName = @"UseLanguage";// Custom bundle name, such as `UseLanguage.bundle`
```

If `config.languageType = DEFAULT;` is set, the system will find the language file for the current region in the custom bundle, and if it cannot be found, the language will be `en` by default.



## Setting Custom UI

### 1. Custom UI

1. Icon: You can replace Icon to the following list, with the name unchanged.

![image-20230110144933817](https://qcloudimg.tencent-cloud.cn/raw/ca4171a7a422b149bf6f2908f9608b8d.png)

2. xib layout adjustment: For the TXYOsAuthingViewController recognition page, you can modify control layout in xib by adding static components, but not deleting components. The logic of this page is implemented by the internal **.m** file of SDK. You are allowed to modify the layout and add non-logical components only. (For example, add a background image.)

![image-20230110145052550](https://qcloudimg.tencent-cloud.cn/raw/4f588059f114b5e8ff598e66bcc81025.png)

3. You can add settings to SDK by setting the **userUIBundleName** field.
```object-c
HuiYanOsConfig *config = [[HuiYanOsConfig alloc] init];
config.userUIBundleName = @"UserUIBundle"
```

