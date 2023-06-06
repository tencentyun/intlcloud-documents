### API description

Integration with the FaceID SDK mainly involves the following classes: `HuiYanOSKit` (API class), `HuiYanOsConfig` (configuration parameter class), and `HuiYanOKitSuccCallback` and `HuiYanOKitFailCallback` (result and callback classes).

#### HuiYanOSKit

| API                                   | Feature Description                |
| ------------------------------------- | ----------------------- |
| [startHuiYaneKYC()](#startHuiYaneKYC) | Starts the liveness detection and face comparison process in the FaceID SDK. |
| [release()](#release())               | Releases FaceID SDK resources.       |



##### release()

Feature description:

This API is used to release FaceID SDK resources.

```objective-c
+ (void)release;
```



##### startHuiYaneKYC

Feature description:

This API is used to start and configure the liveness detection and face comparison SDK and call back the result or error.

```objective-c
/// Start the liveness detection and face comparison process
/// @param faceToken token
/// @param kitConfig SDK configuration
/// @param succCallback Callback for successful liveness detection and face comparison
/// @param failCallback Callback for failed liveness detection and face comparison
- (void)startHuiYaneKYC:(NSString *)faceToken withConfig:(HuiYanOsConfig *)kitConfig
        witSuccCallback:(HuiYanOKitSuccCallback)succCallback
       withFailCallback:(HuiYanOKitFailCallback)failCallback;
```

Input parameters:

| Type                                               | Parameter     | Description         |
| ---------------------------------------------------- | ------------ | ---------------- |
| NSSting                                              | faceToken    | Liveness detection and face comparison process token     |
| [HuiYanOsConfig](#HuiYanOsConfig)                    | kitConfig    | SDK configuration class        |
| [HuiYanOKitSuccCallback](#HuiYanOKitSuccCallbackens) | succCallback | Callback for successful liveness detection and face comparison |
| [HuiYanOKitFailCallback](#HuiYanOKitFailCallback)    | failCallback | Callback for failed liveness detection and face comparison |



#### HuiYanOsAuthResult

| Type  | Parameter  | Description                                       |
| ------- | --------- | ---------------------------------------------- |
| NSSting | faceToken | Liveness detection and face comparison process token                                  |
| NSSting | bestImage | Base64-encoded best frame image returned upon success if best frame return is enabled |

You will need to use the token to call the **GetFaceldResultIntl** API to pull the liveness detection and face comparison result.



#### HuiYanOsConfig

`HuiYanOsConfig` is the configuration entity class during FaceID SDK startup, which mainly contains the following attributes:

| Type                                    | Name                   | Description                                                         | Default Value                    |
| --------------------------------------- | ---------------------- | ------------------------------------------------------------ | ------------------------- |
| NSString                                | authLicense            | Name of the license file applied for by client for liveness detection and face comparison authorization                         | Empty                        |
| long                                    | authTimeOutMs          | Liveness detection and face comparison timeout period                                       | 10000 ms (10s)         |
| long                                    | prepareTimeoutMs       | Detection timeout period in the preparation stage                                   | 0                         |
| [HYShowTimeOutMode](#HYShowTimeOutMode) | showTimeOutMode        | Stage in which the countdown is displayed                                           | HYShowTimeOutMode_PREPARE |
| BOOL                                    | isDeleteVideoCache     | Whether to delete the local cache of the liveness detection and face comparison video                                   | YES                       |
| BOOL                                    | iShowTipsPage          | Whether to display the guide page                                               | No                        |
| NSString                                | userUIBundleName       | Custom UI bundle filename; for example, set `UserUIBundle` for `UserUIBundle.bundle` | nil                       |
| NSString                                | userLanguageFileName   | Custom languageBundle` name; for example, set `UseLanguage` for `UseLanguage.bundle`. | nil                       |
| NSString                                | userLanguageBundleName | Custom local file name for internationalization; for example, set `en` for `en.lproj`.           | nil                       |
| [LanguageType](#LanguageType)           | languageType           | Text language settings inside the SDK                                          | DEFAULT                   |
| BOOL                                    | isGetBestImg           | Whether to get the best frame image                                           | No                        |
| NSString                                | setLanguageFileName    | Language file directory name added in `HuiYanSDKUI.bundle` has the highest priority by default   | nil                       |



#### HuiYanOKitSuccCallback

```objective-c
/**
 * Callback for successful liveness detection and face comparison
 *
 * @param authResult  Liveness detection and face comparison result
 * @param reserved Reserved
 */
typedef void (^HuiYanOKitSuccCallback)(HuiYanOsAuthResult * _Nonnull authResult, id _Nullable reserved);
```



#### HuiYanOKitFailCallback

```objective-c
/**
 * Callback for failed liveness detection and face comparison
 *
 * @param errCode Error code
 * @param errMsg Error message
 * @param reserved Reserved
 */
typedef void (^HuiYanOKitFailCallback)(int errCode, NSString * _Nonnull errMsg ,id _Nullable reserved);
```



#### LanguageType 

Internationalization strings included in the SDK

```objective-c
typedef enum : NSUInteger {
    DEFAULT = 0,//Auto
    ZH_HANS,//Simplified Chinese
    ZH_HANT,//Traditional Chinese
    ZH_HK,//Traditional Chinese (Hong Kong)
    ZH_TW,//Traditional Chinese (Taiwan)
    EN,//English
    MS,//Malaysian
    RU,//Russian
    JA,//Japanese
    CUSTOMIZE_LANGUAGE, //Custom language
} LanguageType;
```



#### HYShowTimeOutMode

```objective-c
typedef NS_OPTIONS(int, HYShowTimeOutMode) {
    HYShowTimeOutMode_TIMEOUT_HIDDEN = 1 << 0,// Hide the countdown in all stages
    HYShowTimeOutMode_PREPARE = 1 << 1,// Preparation stage countdown
    HYShowTimeOutMode_ACTION = 1 << 3,// Action stage countdown
};
```



### SDK Error Codes (iOS)

| Error Codes                                | Error Code | Error Description               |
| ------------------------------------- | -------- | ------------------------ |
| HY_SUCCESS                            | 0        | Successful                     |
| HY_INITIALIZATION_PARAMETER_EXCEPTION | 210      | Parameter initialization exception           |
| HY_BUNDLE_CONFIGURATION_EXCEPTION     | 211      | Bundle configuration exception           |
| HY_YTSDK_CONFIGURATION_EXCEPTION      | 212      | YouTu configuration exception             |
| HY_PLEASE_CALL_FIRST_INIT_API         | 213      | Call the API for initialization first     |
| HY_SDK_AUTH_FAILED                    | 214      | SDK authorization failure             |
| HY_USER_VOLUNTARILY_CANCELED          | 215      | Manually canceled by user             |
| HY_YTSDK_LOCAL_AUTH_FAILED            | 216      | Local face detection failure of SDK     |
| HY_CAMERA_OPEN_FAIL                   | 217      | Failed to enable the camera             |
| HY_DONOT_SWITCH_APPS                  | 218      | Do not switch the application during liveness detection and face comparison |
| HY_CAMEREA_PERMISSION_EXCEPTION       | 219      | Camera permission exception           |
| HY_SDK_VEDIO_CUT_EXCEPTION            | 220      | Failed to clip the video             |
| HY_LIGHT_DATA_FORMAT_EXCEPTION        | 221      | Incorrect light data format         |