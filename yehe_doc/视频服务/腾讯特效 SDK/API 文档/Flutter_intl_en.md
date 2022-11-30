`TencentEffectApi` is the core API class of the Tencent Effect Flutter SDK. It offers capabilities including setting the effect strength and applying animated effects.

## Public Member APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [initXmagic](#initxmagic)                                    | Initializes data. You need to call this API before using the Tencent Effect SDK.                    |
| [setLicense](#setlicense)                                    | Configures the license.                                                 |
| [setXmagicLogLevel](#setxmagicloglevel)                      | Sets the log level of the SDK. We recommend you set it to `Log.DEBUG` for debugging and `Log.WARN` for official release. If you set it to `Log.DEBUG` in a production environment, the output of a large amount of log data may affect your application’s performance. |
| [onResume](#onresume)                                        | Resumes rendering. Call this API when the page is visible.                                     |
| [onPause](#onpause)                                          | Pauses rendering. Call this API when the page is invisible.                                   |
| [updateProperty](#updateproperty)                            | Updates an effect property. This API can be called in any thread.                    |
| [setOnCreateXmagicApiErrorListener](#setoncreatexmagicapierrorlistener) | Configures the callback for creating an effect object. The callback will be triggered if an error occurs.         |
| [setTipsListener](#settipslistener)                          | Configures the callback for animated effect tips. The tips can be displayed on the UI.       |
| [setYTDataListener](#setytdatalistener)                      | Configures the callback of facial keypoints and other data. The callback is only available in S1 - 05 and S1 - 06.   |
| [setAIDataListener](#setaidatalistener)                      | Configures the callback of face, gesture, and body detection results. |
| [isBeautyAuthorized](#isbeautyauthorized)                    | Checks whether the current license supports a particular type of effects. This API can only check the authorization of `BEAUTY` and `BODY_BEAUTY` effects. The result returned determines the value of `XmagicProperty.isAuth`.   |
| [isSupportBeauty](#issupportbeauty)                          | Checks whether the current device supports effects (OpenGL 3.0).                    |
| [getDeviceAbilities](#getdeviceabilities)                    | Gets a list of Tencent Effect capabilities supported by the current device.                                 |
| [isDeviceSupport](#isdevicesupport)                          | Checks whether a list of animated effect resources are supported. The result is indicated by `XmagicProperty.isSupport`. For unsupported resources, you can either disable tapping on the UI or delete them from the resource list. |
| [getPropertyRequiredAbilities](#getpropertyrequiredabilities) | Gets the Tencent Effect capabilities used by different animated effect resources.  |


## API Description

### initXmagic

This API is used to initialize the Tencent Effect SDK.
```dart
void initXmagic(String xmagicResDir,InitXmagicCallBack callBack);

typedef InitXmagicCallBack = void Function(bool reslut);
```

#### Parameters
| Parameter       | Description                                                                                                                                        |
| --------------------------- | ------------------ |
| String xmagicResDir         | The resource directory. |
| InitXmagicCallBack callBack | The initialization callback.     |


### setLicense

This API is used to set the license.

```dart
  ///Set the Tencent Effect license
void setLicense(String licenseKey, String licenseUrl, LicenseCheckListener checkListener);
//The callback of the authorization result
typedef LicenseCheckListener = void Function(int errorCode, String msg);
```

#### Parameters

| Parameter                               | Description             |
| ---------------------------------- | :--------------- |
| String licenseKey                  | The license key. |
| String licenseUrl                  | The license URL. |
| LicenseCheckListener checkListener | The callback of the authorization result. |


### setXmagicLogLevel

This API is used to set the log level of the SDK.

```dart
void setXmagicLogLevel(int logLevel);
```

#### Parameters

| Parameter       | Description                                                                                                                                        |
| ------------ | :--------------------------------- |
| int logLevel | You can set the log level using a type defined for `LogLevel`. |


### onResume

This API is used to resume effect rendering.

```dart
void onResume();
```

### onPause

This API is used to pause effect rendering.

```dart
void onPause();
```


### updateProperty

This API is used to set an effect value, an animated effect, or a filter. You can call it in any thread.

```dart
void updateProperty(XmagicProperty xmagicProperty);
```

#### Parameters

| Parameter       | Description                                                                                                                                        |
| ----------------------------- | :--------------- |
| XmagicProperty xmagicProperty | The object of the effect property. |


### setOnCreateXmagicApiErrorListener

This API is used to configure the callback for errors for the creation of an effect object.

```dart
  void setOnCreateXmagicApiErrorListener(OnCreateXmagicApiErrorListener? errorListener);
/// The callback for errors for the creation of an effect object
typedef OnCreateXmagicApiErrorListener = void Function(String errorMsg, int code);
```

#### Parameters

| Parameter       | Description                                                                                                                                        |
| --------------------------------------------- | :----------------------------- |
| OnCreateXmagicApiErrorListener? errorListener | The callback for errors for the creation of an effect object. |

Error codes:

| Error Code  |  Description                    |
| ---- | --------------------- |
| -1   | Unknown error.                    |
| -100 | Failed to initialize the 3D engine.                    |
| -200 | GAN materials are not supported.             |
| -300 | The device does not support this material component.           |
| -400 | The JSON template is empty.           |
| -500 | The SDK version is too old.              |
| -600 | Keying is not supported.                |
| -700 | OpenGL is not supported.                    |
| -800 | The script is not supported.                |
| 5000 | The resolution of the video to be keyed exceeds 2160 x 3840. |
| 5001 | Insufficient memory for keying.                    |
| 5002 | Failed to parse the video to be keyed.         |
| 5003 | The video to be keyed is longer than 200 seconds.                    |
| 5004 | Unsupported video format for keying.                    |


### setTipsListener

This API is used to configure the callback for animated effect tips. The tips can be displayed on the UI, asking users to nod, show their palms, or make finger hearts.

```dart
void setTipsListener(XmagicTipsListener? xmagicTipsListener);

abstract class XmagicTipsListener {
  /// Show the tip
  /// @param tips: The content of the tip (string).
  /// @param tipsIcon: The icon for the tip.
  /// @param type: The display type. If it is set to `0`, both the tip string and icon will be displayed. If it is set to `1`, only the icon will be displayed for PAG materials.
  /// @param duration: How long (milliseconds) to show the tip.
  void tipsNeedShow(String tips, String tipsIcon, int type, int duration);

  /// *
  /// Hide the tip
  /// @param tips: The content of the tip (string).
  /// @param tipsIcon: The icon for the tip.
  /// @param type: The display type. If it is set to `0`, both the tip string and icon will be displayed. If it is set to `1`, only the icon will be displayed for PAG materials.
  void tipsNeedHide(String tips, String tipsIcon, int type);
}
```

#### Parameters

| Parameter       | Description                                                                                                                                        |
| ------------------------------------- | ---------------- |
| XmagicTipsListener xmagicTipsListener | The callback implementation class.  |


### setYTDataListener

This API is used to configure the callback of facial keypoints and other data.
```dart
  /// Configure the callback of facial keypoints and other data (only available in S1 - 05 and S1 - 06)
void setYTDataListener(XmagicYTDataListener? xmagicYTDataListener);
Configure the callback of facial keypoints and other data

abstract class XmagicYTDataListener {
  // YouTu AI data
  void onYTDataUpdate(String data);
}
```
`onYTDataUpdate` returns a JSON string structure that contains the information of up to 5 faces:
```
{
 "face_info":[{
  "trace_id":5,
  "face_256_point":[
    180.0,
    112.2,
    ...
  ],
  "face_256_visible":[
    0.85,
    ...
  ],
  "out_of_screen":true,
  "left_eye_high_vis_ratio:1.0,
  "right_eye_high_vis_ratio":1.0,
  "left_eyebrow_high_vis_ratio":1.0,
  "right_eyebrow_high_vis_ratio":1.0,
  "mouth_high_vis_ratio":1.0
 },
 ...
 ]
}
```

#### Fields

| Field                           | Type    | Range                           | Description                            |
| -------------------------- |-------------------------- | --------------------------- | --------------------------- |
| trace_id                     | int   | [1,INF)                      | The face ID. If the faces obtained from a continuous video stream have the same face ID, they belong to the same person. |
| face_256_point               | float | [0,screenWidth] or [0,screenHeight] | 512 values in total for 256 facial keypoints. (0,0) is the top-left corner of the screen. |
| face_256_visible             | float | [0,1]                               | The visibility of the 256 facial keypoints.                                    |
| out_of_screen                | bool  | true/false                          | Whether only part of the face is captured.                                           |
| left_eye_high_vis_ratio      | float | [0,1]                               | The percentage of keypoints with high visibility for the left eye.                                    |
| right_eye_high_vis_ratio     | float | [0,1]                               | The percentage of keypoints with high visibility for the right eye.                                   |
| left_eyebrow_high_vis_ratio  | float | [0,1]                        | The percentage of keypoints with high visibility for the left eyebrow.                   |
| right_eyebrow_high_vis_ratio | float | [0,1]                        | The percentage of keypoints with high visibility for the right eyebrow.                   |
| mouth_high_vis_ratio         | float | [0,1]                               | The percentage of keypoints with high visibility for the mouth.                                     |

#### Parameters

| Parameter       | Description                                                                                                                                        |
| ---------------------------------------------- | ---------------- |
| XmagicYTDataListener      xmagicYTDataListener | The callback implementation class.  |


### setAIDataListener

This API is used to configure the callback of face, gesture, and body detection results.

```dart
void setAIDataListener(XmagicAIDataListener? aiDataListener);
  
abstract class XmagicAIDataListener {
  void onFaceDataUpdated(String faceDataList);

  void onHandDataUpdated(String handDataList);

  void onBodyDataUpdated(String bodyDataList);
}
```


### isBeautyAuthorized

This API is used to check whether the current license supports a particular type of effects. It can only check the authorization of `BEAUTY` and `BODY_BEAUTY` effects. The result returned determines the value of `XmagicProperty.isAuth`. If `isAuth` is `false`, you can disable the corresponding effects on the UI.

```
Future<List<XmagicProperty>> isBeautyAuthorized(
      List<XmagicProperty> properties);
```

#### Parameters

| Parameter       | Description                                                                                                                                        |
| ------------------------------- | ------------------ |
| List&lt;XmagicProperty> properties | The type of effects to check.  |


### isSupportBeauty

This API is used to check whether the current device supports effects (OpenGL 3.0).

```dart
  Future&lt;bool> isSupportBeauty();
```

#### Response

A Boolean value indicating whether effects are supported.


### getDeviceAbilities

This API is used to get a list of Tencent Effect capabilities supported by the current device. You can use it together with `getPropertyRequiredAbilities`.

```
  Future<Map<String, bool>> getDeviceAbilities();
```

#### Response

`Map<String,Boolean>`:

- key: The name of a capability (the material name).
- value: Whether the current device supports the capability.


### getPropertyRequiredAbilities

This API is used to get the Tencent Effect capabilities used by different animated effect resources.
Use case:
This API is useful if you have purchased animated effects or made your own animated effect materials. It returns the capabilities each material uses. For example, material 1 uses capabilities A, B, and C, and material 2 relies on capabilities B, C, and D. You can store such information in the server. When a user downloads the two materials from the server, call `getDeviceAbilities` first to get the capabilities supported by their device. The result is then passed to the server. For example, if a user’s device supports capabilities A, B, and C, but not D, the server will not provide material 2 to the user.

```dart
Future<Map<XmagicProperty, List<String>?>> getPropertyRequiredAbilities(
    List<XmagicProperty> assetsList);
```

#### Parameters

| Parameter       | Description                                                                                                                                        |
| ------------------------------ | ---------------- |
| List&lt;XmagicProperty> assetsList | A list of the animated effects to check.  |

#### Response

Map&lt;XmagicProperty, List&lt;String>?>:

- key: The entity class of the animated effect.
- value: A list of capabilities used by the effect.


### isDeviceSupport

This API is used to check whether a list of animated effect resources are supported. The result is indicated by `XmagicProperty.isSupport`. For unsupported resources, you can either disable tapping on the UI or delete them from the resource list.

```dart
 Future&lt;List<XmagicProperty>> isDeviceSupport(List<XmagicProperty> assetsList);
```

#### Parameters

| Parameter       | Description                                                                                                                                        |
| ------------------------------- | ------------------------ |
| List&lt;XmagicProperty> assetsList | A list of animated effect resources to check.  |