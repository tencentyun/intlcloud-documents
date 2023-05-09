## API description

The FaceID SDK mainly involves the following classes: `HuiYanOsApi` (API class), `HuiYanOsConfig` (parameter configuration class), and `HuiYanOsAuthCallBack` and `HuiYanAuthEventCallBack` (result callback classes).

### HuiYanOsApi

| API                                               | Feature Description                                           |
| ------------------------------------------------- | -------------------------------------------------- |
| [init()](#init())                                 | Initializes the service.                                         |
| [release()](#release())                           | Releases resources.                                       |
| [setAuthEventCallBack()](#setAuthEventCallBack()) | Sets the key actions in the liveness detection and face comparison process.                 |
| [startHuiYanAuth()](#startHuiYanAuth())           | Performs liveness detection and face comparison. This API can be called to complete the entire process. |



#### init()

Feature description:

This API is used to initialize the FaceID SDK.

```java
public static void init(Context context)
```

Input parameters:

| Type | Parameter | Description        |
| -------- | -------- | --------------- |
| Context  | context  | App context information |



#### release()

Feature description:

This API is used to release FaceID SDK resources.

```java
public static void release() 
```




#### setAuthEventCallBack()

Feature description:

This API is used to set callback for the key actions in the liveness detection and face comparison process.

```java
public static void setAuthEventCallBack(HuiYanAuthEventCallBack authEventCallBack)
```

Input parameters:

| Type                                            | Parameter                | Description           |
| --------------------------------------------------- | ----------------------- | ------------------ |
| [HuiYanAuthEventCallBack](#HuiYanAuthEventCallBack) | huiYanAuthEventCallBack | Callback for key liveness detection and face comparison actions |



#### startHuiYanAuth()
Feature description:

This API is used for liveness detection and face comparison. It can be called to complete the entire process.

```java
public static void startHuiYanAuth(final String startToken, final HuiYanOsConfig startConfig, HuiYanOsAuthCallBack authCallBack)
```

Input parameters:

| Type                                      | Parameter     | Description                              |
| --------------------------------------------- | ------------ | ------------------------------------- |
| String                                        | startToken   | Business token requested from the server for starting liveness detection and face comparison |
| [HuiYanOsConfig](#HuiYanOsConfig)             | startConfig  | Configuration parameter                            |
| [HuiYanOsAuthCallBack](#HuiYanOsAuthCallBack) | authCallBack | liveness detection and face comparison result                        |




### HuiYanOsConfig

`HuiYanOsConfig` is the configuration entity class during FaceID SDK startup, which mainly contains the following attributes:

| Type                              | Name               | Description                                        | Default Value               |
| --------------------------------- | ------------------ | ------------------------------------------- | -------------------- |
| [PageColorStyle](#PageColorStyle) | pageColorStyle     | Color pattern used for liveness detection and face comparison                      | PageColorStyle.Light |
| String                            | authLicense        | Name of the license file applied for by client for liveness detection and face comparison authorization        | Empty                   |
| long                              | authTimeOutMs      | Liveness detection and face comparison timeout period                      | 10000 ms (10s)    |
| boolean                           | isDeleteVideoCache | Whether to delete the local cache of the liveness detection and face comparison video                  | true                 |
| boolean                           | isShowGuidePage    | Whether to open the guide page for liveness detection and face comparison                        | true                 |
| boolean                           | isNeedBestImage    | Whether to return the best frame                          | false                |
| LanguageStyle                     | languageStyle      | Language type                                    | Auto         |
| String                            | languageCode       | Language code (see **Language codes for Android**), which is used together with `languageStyle` | Empty                   |
| String                          | backUpIPs          | List of backup IPs                                  | Empty                   |
| String                            | backUpHost         | Backup domain                                    | Empty                   |
| AuthUiConfig                      | authUiConfig       | UI configuration items                                    | Empty                   |



### PageColorStyle

This is the enumeration class of default color patterns on the default liveness detection and face comparison UI. Currently, two color patterns are supported: light and dark.

| PageColorStyle Value  | Description       |
| -------------------- | ---------- |
| PageColorStyle.Light | Light color pattern |
| PageColorStyle.Dark  | Dark color pattern |



### LanguageStyle

| LanguageStyle Value                | Description       |
| --------------------------------- | ---------- |
| LanguageStyle.AUTO                | Auto   |
| LanguageStyle.ENGLISH             | English       |
| LanguageStyle.SIMPLIFIED_CHINESE  | Simplified Chinese   |
| LanguageStyle.TRADITIONAL_CHINESE | Traditional Chinese   |
| LanguageStyle.CUSTOMIZE_LANGUAGE  | Custom language |



### AuthUiConfig

Parameter configuration of custom liveness detection and face comparison UI.

| Type                    | Name                   | Description                                                       | Default Value |
| ----------------------- | ---------------------- | ---------------------------------------------------------- | ------ |
| [VideoSize](#VideoSize) | videoSize              | Resolution during liveness detection and face comparison                                         | 480P   |
| boolean                 | isShowCountdown        | Whether to display the countdown control                                       | true   |
| boolean                 | isShowErrorDialog      | Whether to display the error dialog                                       | true   |
| int                     | authLayoutResId        | Custom layout `resID` exported from FaceID, which is -1 by default if not adjusted.                | -1     |
| int                     | feedBackErrorColor     | Color of exception `tips` (format: 0xFFFFFFFF), which is -1 by default if not adjusted.         | -1     |
| int                     | feedBackTxtColor       | Color of success `tips` (format: 0xFFFFFFFF), which is -1 by default if not adjusted.           | -1     |
| int                     | authCircleErrorColor   | Color of background round frame for incorrect action (format: 0xFFFFFFFF), which is -1 by default if not adjusted.     | -1     |
| int                     | authCircleCorrectColor | Color of background round frame of correct action (format: 0xFFFFFFFF), which is -1 by default if not adjusted. | -1     |
| int                     | authLayoutBgColor      | Color of liveness detection and face comparison UI background (format: 0xFFFFFFFF), which is -1 by default if not adjusted.         | -1     |



### VideoSize

Enumerated values of resolutions supported by FaceID.

| VideoSize Value       | Description |
| ------------------- | ---- |
| VideoSize.SIZE_480P | 480P |
| VideoSize.SIZE_720P | 720P |



### HuiYanOsAuthResult

The result type corresponding to the callback for successful liveness detection and face comparison.

| Type   | Name      | Description                       | Default Value |
| ------ | --------- | -------------------------- | ------ |
| String | token     | The token used in the current liveness detection and face comparison process.  | Empty     |
| String | bestImage | Base64-encoded data of the best frame image for liveness detection and face comparison. | Empty     |

You will need to use the token to call the [GetFaceldResultIntl](//TODO:) API to pull the liveness detection and face comparison result.



### HuiYanOsAuthCallBack

This is the callback API for the liveness detection and face comparison process.

```java
/**
 * Result callback
 *
 * @author jerrydong
 * @since 2022/6/10
 */
public interface HuiYanOsAuthCallBack {

    /**
     * Successful liveness detection and face comparison
     *
     * @param authResult Result
     */
    void onSuccess(HuiYanOsAuthResult authResult);

    /**
     * Failed liveness detection and face comparison
     *
     * @param errorCode Error code
     * @param errorMsg Error message
     * @param token Token used in this liveness detection and face comparison process
     */
    void onFail(int errorCode, String errorMsg, String token);
}
```



### HuiYanAuthEventCallBack

This callback is used to listen for key events during liveness detection and face comparison. You can use the UI with custom layout to **[bind events (see the document about custom capabilities)](https://iwiki.woa.com/pages/viewpage.action?pageId=4007948338)**.

```java
/**
 * Callback for liveness detection and face comparison event in FaceID SDK
 */
public interface HuiYanAuthEventCallBack {

    /**
     * Callback for event notification when liveness detection and face comparison `tips` change
     *
     * @param tipsEvent Key `tips` event
     */
    void onAuthTipsEvent(HuiYanAuthTipsEvent tipsEvent);

    /**
     * Liveness detection and face comparison event
     *
     * @param authEvent authEvent
     */
    void onAuthEvent(HuiYanAuthEvent authEvent);

    /**
     * Callback for the creation of the authenticated main view
     *
     * @param authView
     */
    void onMainViewCreate(View authView);

    /**
     * Callback for UI repossession
     */
    void onMainViewDestroy();

}
```



### Error Codes

Below are the error codes in the FaceID SDK (global edition) in failure callbacks and their meaning:

| Error Codes                                | Error Code | Error Description                                                   |
| ------------------------------------- | -------- | ------------------------------------------------------------ |
| HY_NETWORK_ERROR                      | 210      | Network request exception.                                             |
| HY_LOCAL_REF_FAILED_ERROR             | 211      | Check failed during local SDK initialization. The common exceptions are license file nonexistence or license expiration. |
| HY_USER_CANCEL_ERROR                  | 212      | The user actively cancels the liveness detection and face comparison process.                                         |
| HY_INNER_ERROR_CODE                   | 213      | An internal exception of the SDK occurred, causing the liveness detection and face comparison process to be stopped.                            |
| HY_DO_NOT_CHANGE_ERROR                | 214      | Applications are switched during liveness detection and face comparison, causing the process to be stopped.                       |
| HY_CAMERA_PERMISSION_ERROR            | 215      | An exception occurred while getting the camera.                                     |
| HY_INIT_SDK_ERROR                     | 216      | The liveness detection and face comparison method is directly called before the "init()" method is called.                                 |
| HY_VERIFY_LOCAL_ERROR                 | 217      | Local face detection failed.                                             |
| HY_PERMISSION_CHECK_ERROR             | 218      | The permissions required by the local SDK are insufficient.                                      |
| HY_APP_STOP_ERROR                     | 219      | If `reflectSequence` of `startAuthByLightData` is `null`, you stopped the liveness detection and face comparison process. |
| HY_CHECK_LIVE_DATA_ERROR              | 220      | Failed to verify the light sequence parameter.                                   |
| HY_INITIALIZATION_PARAMETER_EXCEPTION | 221      | An exception occurred while directly calling the method for setting light sequence parameters without getting the device configuration. |
| HY_VERIFY_LOCAL_TIME_OUT              | 222      | Local motion detection timed out.                                         |
| HY_PREPARE_TIME_OUT                   | 223      | Preparation timed out (between camera launch and the first detection of face).       |
| HY_CHECK_PERMISSION_ERROR             | 224      | Failed to apply for the camera permission inside the SDK.                                    |
