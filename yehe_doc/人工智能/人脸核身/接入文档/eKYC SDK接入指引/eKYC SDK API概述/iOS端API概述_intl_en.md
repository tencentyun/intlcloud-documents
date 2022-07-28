The main API classes used in the eKYC SDK for iOS are `VerificationKit`, `VerificationConfig`, and `VerifiCommDef`. Specific APIs in these classes are described as below.

### VerificationKit

`VerificationKit` is a class of external APIs for the eKYC SDK. Main logic operations are completed with this class.

| API                                                   | Feature Description                                             |
| --------------------------------------------------- | ------------------------ |
| [initWithViewController:](#initWithViewController:) | Initializes the eKYC SDK               |
| [clearInstance](#clearInstance)                     | Releases resources           |
| [startVerifiWithConfig:](#startVerifiWithConfig:)   | Starts the eKYC process |



#### initWithViewController:

```objective-c
// Initialization method
- (void)initWithViewController:(UIViewController *)viewController;
```

Feature:

It is an API for initializing the ​eKYC SDK.

Input parameters:	

| Parameter Type | Parameter Name | Description        |
| ---------------- | -------------- | --------------------- |
| UIViewController | viewController | Calls the `viewController` object of the current SDK page |



#### clearInstance

```objective-c
/// Clear SDK resources
+ (void)clearInstance;
```

Feature:

It is an API for releasing eKYC SDK resources.



#### startVerifiWithConfig:

```objective-c
/// Start eKYC verification
- (void)startVerifiWithConfig:(VerificationConfig *)verifiConfig
            withSuccCallback:(TXYVerifiKitProcessSucceedBlock)succCallback
             withFialCallback:(TXYVerifiKitProcessFailedBlock)failCallback;
```

Feature:

It is a method for starting the eKYC process.

Input parameters:

| Parameter Type | Parameter Name | Description        |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [VerificationConfig](#VerificationConfig)                    | verifiConfig | Configuration info for starting this eKYC process |
| [TXYVerifiKitProcessSucceedBlock](#TXYVerifiKitProcessSucceedBlock) | succCallback | Callback for successful eKYC SDK detection        |
| [TXYVerifiKitProcessSucceedBlock](#TXYVerifiKitProcessSucceedBlock) | succCallback | Callback for failed eKYC SDK detection        |



### VerificationConfig

`VerificationConfig` is the configuration entity class used during the eKYC SDK startup, which mainly covers the following attributes:

| Type                          | Name           | Description                                              | Default Value            |
| ----------------------------- | -------------- | ------------------------------------------------- | ----------------- |
| NSString                      | ekycToken      | The token obtained from the server, which is used as the unique credential for identity verification. | Null                |
| NSString                      | licPath        | The path of the license file requested for user identity verification                | Null                |
| long                          | verAutoTimeOut |  The timeout period of the authentication                                | 20,000 ms (20s) |
| long                          | hyFaceTimeOut  | The timeout period of a single face authentication operation                          | 10,000 ms (10s) |
| BOOL                          | isHiddenAlbum  | Whether to hide the album button on the OCR interface            | NO                |
| BOOL                          | isHiddenFlash  | Whether to hide the OCR flashlight button                             | NO                |
| [LanguageType](#LanguageType) | languageType   | Language type of this process                                | DEFAULT (0)       |

##### OCRRegionType
This API is used to detect the type of the document.

| Enumerated Value  | Description             |
| ---------------- | ---------------- |
|OCR_TYPE_HK| Hong Kong (China) - identity card |
|OCR_TYPE_ML| Malaysia - identity card |
|OCR_TYPE_PV_ID| Philippines - driver's license |
|OCR_TYPE_PDL| Philippines - VoteID |

### LanguageType

This API provides the language configuration information of the default eKYC interface.

| LanguageType | Description             |
| ---------------- | ---------------- |
| DEFAULT          | Auto |
| EN               | English             |
| ZH_HANS          | Simplified Chinese         |
| ZH_HANT          | Traditional Chinese         |



### TXYVerifiKitProcessSucceedBlock

This is callback for successful eKYC SDK detection.

```objective-c
/// Callback API for successful detection with the SDKKIt
/// @param errorCode: Error code
/// @param resultInfo: Information returned by the callback
/// @param reserved: Reserved
typedef void (^TXYVerifiKitProcessSucceedBlock)(int errorCode,id _Nonnull resultInfo, id _Nullable reserved);
```



### TXYVerifiKitProcessFailedBlock

This is callback for failed eKYC SDK detection.

```objective-c
/// Callback API for detection failure with the SDKKIt
/// @param errorCode: Error code
/// @param errorMsg: Error message
/// @param reserved: Reserved
typedef void (^TXYVerifiKitProcessFailedBlock)(int errorCode, NSString *_Nonnull errorMsg, id _Nullable reserved);
```



### Error codes and descriptions

| Error Code                                | Value | Description               |
| ------------------------------------- | -------- | ------------------------ |
| HY_SUCCESS                            | 0        | Detection succeeded                 |
| HY_VERIFI_FAIL                        | -1       | Detection failed                 |
| HY_VERIFI_OCR_FAIL                    | -2       | Card and certificate recognition failed             |
| HY_SDK_INNER_ERR                      | -4       | Internal error of FaceID eKYC         |
| HY_INITIALIZATION_PARAMETER_EXCEPTION | 310      | Initialization parameter exception           |
| HY_BUNDLE_CONFIGURATION_EXCEPTION     | 311      | Bundle configuration exception          |
| HY_YTSDK_CONFIGURATION_EXCEPTION      | 312      | YouTu configuration exception             |
| HY_PLEASE_CALL_FIRST_INIT_API         | 313      | Failed to call the initialization API first         |
| HY_SDK_AUTH_FAILED                    | 314      | SDK authorization failed             |
| HY_USER_VOLUNTARILY_CANCELED          | 315      | The user manually canceled the detection              |
| HY_YTSDK_LOCAL_AUTH_FAILED            | 316      | Local face authentication with the SDK failed    |
| HY_CAMERA_OPEN_FAIL                   | 317      | Failed to enable the camera             |
| HY_DONOT_SWITCH_APPS                  | 318      | Do not switch the application during identity verification |
| HY_CAMEREA_PERMISSION_EXCEPTION       | 319      | Camera permission exception           |
| HY_SDK_VEDIO_CUT_EXCEPTION            | 320      | Failed to trim the video           |
| HY_LIGHT_DATA_FORMAT_EXCEPTION        | 321      | Invalid reflection data format         |
| HY_GET_REMOTE_DATA_EXCEPTION          | 322      | Error in getting reflection data       |

