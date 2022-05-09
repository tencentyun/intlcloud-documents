### Environment Requirements

1. Development environment: Xcode 11.0 or later
2. The FaceID SDK for iOS is only supported by iOS 9.0 or later.

### **1. Manual integration**

1. Import libraries and files

Click `Link Binary With Libraries` to add frameworks.

2. The SDK depends on the following libraries:

```
├──HuiYanSDK.framework
├──TXYComm.framework
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

### 2. Integration by using pod

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

### `Build Phases` settings

1. Click `Other Linker Flags` to add **-ObjC**.
2. Change the extension of `ViewController.m` to `.mm`.
3. Set `Enable BitCode` to `NO`.

### Permission Settings

As the SDK requires a mobile network and camera permission, include the following key-value pair in `info.plist` of the main project to add the corresponding permission declaration.

```xml
<key>Privacy - Camera Usage Description</key>
<string>FaceID needs to access your camera for face recognition</string>
```


### SDK APIs Use Instructions

#### Initializing configuration and pulling parameters

Before using the FaceID SDK, you need to call this method to pass in basic configuration parameters and use the callback to pull the local configuration parameters.

```objective-c
// HuiYanOs parameter
HuiYanOsConfig *config = [[HuiYanOsConfig alloc] init];
// The path of the license file in the bundle
config.authLicense = [[NSBundle mainBundle] pathForResource:@"YTFaceSDK.license" ofType:@""];
// The timeout period of local liveness detection in ms
config.authTimeOutMs = 20000;
// Pull the local configuration parameter information before starting identity verification
[HuiYanOsApi startGetAuthConfigData:config withSuccCallback:^(NSString * _Nonnull result) {
// The configuration information is obtained successfully and sent to the server to get the verification start configuration, and the server delivers the light sequence (implemented by yourself).
NSString *liveData = [self getLiveDataWith:result];
} withFialCallback:^(int errCode, NSString * _Nonnull errMsg) {
// Failed to get configuration parameters (implemented by yourself)
NSLog(@"errCode:%d, errMsg:%@", errCode, errMsg);
}];
```

#### Performing subsequent liveness detection steps

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

#### API for releasing SDK resources

Before your app exits, you can call the API to release SDK resources.

```objective-c
// Release the resources before exit
- (void)dealloc {
[HuiYanOsApi release];
}
```


## Description of iOS APIs

The FaceID SDK mainly involves the following classes: HuiYanOsApi (API class), HuiYanOsConfig (configuration parameter class), and HuiYanConfigCallback and HuiYanResultCallBack (result and callback classes).

### HuiYanOsApi

| API | Feature Description |
| ----------------------------------------------------- | ---------------------------------------------------- |
| [release()](#release()) | Releases resources|
| [startGetAuthConfigData()](#startGetAuthConfigData()) | Gets the local configuration information of the FaceID SDK |
| [startAuthByLightData()](#startAuthByLightData()) | Passes in the light sequence obtained from the server to continue the liveness detection for identity verification |


#### release()

```objective-c
+ (void)release;
```

Feature:

It is an API for releasing FaceID SDK resources.

#### startGetAuthConfigData()

```objective-c
+ (void)startGetAuthConfigData:(HuiYanOsConfig *)huiYanOsConfig
withSuccCallback:(HuiYanConfigSuccCallback)huiYanConfigSuccCallback
withFailCallback:(HuiYanConfigFailCallback)huiYanConfigFailCallback;
```

Feature:

In the local detection, the FaceID SDK pulls the configuration parameters as the parameters for getting the light sequence in subsequent steps.

Input parameters:

| Parameter Type | Parameter | Description |
| ----------------------------------------------------- | ------------------------ | ---------------------- |
| [HuiYanOsConfig](#HuiYanOsConfig) | huiYanOsConfig | Configuration parameter |
| [HuiYanConfigCallback](#HuiYanConfigCallback) | configCallback | Callback for successful pull of configuration result |
| [HuiYanConfigFailCallback](#HuiYanConfigFailCallback) | huiYanConfigFailCallback | Callback for failing to pull configuration result |


#### startAuthByLightData()

```objective-c
+ (void)startAuthByLightData:(NSString *)lightData
withSuccCallback:(HuiYanResultSuccCallback)huiYanResultSuccCallback
withFailCallback:(HuiYanResultFailCallback)huiYanResultFailCallback;
```

Feature:

It is an API used to pass in the light sequence data pulled from the server to the FaceID SDK in order to continue the identity verification process for the local detection result.

Input parameters:

| Parameter Type | Parameter | Description |
| ----------------------------------------------------- | ------------------------ | ------------------------------------ |
| NSString | lightData | The light sequence obtained from the server and used for starting the identity verification |
| [HuiYanResultSuccCallback](#HuiYanResultSuccCallback) | huiYanResultSuccCallback | Callback for successful local identity verification |
| [HuiYanResultFailCallback](#HuiYanResultFailCallback) | huiYanResultFailCallback | Callback for failed local identity verification |


### HuiYanOsConfig

`HuiYanOsConfig` is the configuration entity class used during FaceID SDK startup, which mainly covers the following attributes:

| Type | Name | Description | Default Value |
| --------- | ------------------ | ------------------------------------ | ----------------- |
| NSSString | authLicense | Name of the license file requested for user identity verification | Null |
| long | authTimeOutMs | Timeout period of liveness detection | 10,000 ms (10s) |
| BOOL | isDeleteVideoCache | Whether to delete the local cache of the identity verification video | YES |

### HuiYanConfigSuccCallback

Callback for initialization and successful acquisition of the local configuration

```java
/**
* Callback for successful initialization
*
* @param result: Initialization callback data
*/
typedef void (^HuiYanConfigSuccCallback)(NSString * _Nonnull result);
```

### HuiYanConfigFailCallback

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


### HuiYanResultSuccCallback

Callback for successful local identity verification process and local result acquisition

```objective-c
/**
* Callback for successful liveness verification
*
* @param data: Compressed binary data for comparison
* @param videoPath: Path of the liveness video
*/
typedef void (^HuiYanResultSuccCallback)(NSString * _Nonnull data, NSString * _Nonnull videoPath);
```

### HuiYanResultFailCallback

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