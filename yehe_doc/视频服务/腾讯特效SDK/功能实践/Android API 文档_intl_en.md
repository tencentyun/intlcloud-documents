This document describes core API class `XmagicApi.java` of the Tencent Effect SDK used to initialize the SDK, update beauty filter values, and call animated effects.

## Public Member Functions

| API | Description |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [XmagicApi](#xmagicapi)                                      | Constructor.                                                   |
| [updateProperty](#updateproperty)                            | Updates an attribute and can be called in any thread.                                |
| [updateProperties](#updateproperties)                        | Updates attributes and can be called in any thread.                                 |
| [setTipsListener](#settipslistener)                          | Sets the callback function for the animated effect prompt to display the prompt on the frontend page.       |
| [setYTDataListener](#setytdatalistener)                      | Sets the callback for data such as face point information (only available in S1-05 and S1-06 packages). |
| [setAIDataListener](#setaidatalistener)                      | Sets the callback of face, gesture, and body detection status. |
| [onPause](#onpause)                                          | Pauses sound playback and can be bound to the `onPause` lifecycle of `Activity`.           |
| [onResume](#onresume)                                        | Resumes rendering and can be bound to the `onResume` lifecycle of `Activity`.               |
| [onDestroy](#ondestroy)                                      | Terminates xMagic, which needs to be called in the GL thread.                            |
| [process](#process)                                          | Method to receive data by SDK rendering, which can be used within the camera data callback function.         |
| [onPauseAudio](#onpauseaudio)                                | Call this function when you only need to stop the audio but don't need to release the GL thread.         |
| [sensorChanged](#sensorchanged)                              | Used to determine the current rotation angle of the phone, so as to adjust the basis for AI to recognize the angle of the face. |
| [isDeviceSupport](#isdevicesupport)                          | Passes in the list of animated effect resources into the SDK for check, after which the `XmagicProperty.isSupport` field identifies whether the atomic capability is available. According to the value of `XmagicProperty.isSupport`, click restrictions can be controlled at the UI layer or removed from the resource list directly. |
| [getPropertyRequiredAbilities](#getpropertyrequiredabilities) | Passes in a list of animated effect resources and returns a list of the SDK atomic capabilities used by each resource. |
| [getDeviceAbilities](#getdeviceabilities)                    | Returns the list of atomic capabilities supported by the current device.                                 |
| [isSupportBeauty](#issupportbeauty)                          | Determines whether the current model supports beauty filters (OpenGL3.0).                      |
| [isBeautyAuthorized](#isbeautyauthorized)                    | Determines which beauty filters are supported by the current `lic`. Only beauty filters of the `BEAUTY` and `BODY_BEAUTY` types can be checked. The check result is assigned to the `XmagicProperty.isAuth` field of each beauty filter object. |
| [setXmagicStreamType](#setxmagicstreamtype)                  | Sets the input data type, which is Android camera data stream by default.               |
| [setXmagicLogLevel](#setxmagicloglevel)                      | Sets the log level of the SDK. We recommend you set it to `Log.DEBUG` during developing and debugging and to `Log.WARN` after official release. If it is set to `Log.DEBUG` after release, many logs will be generated and affect the performance. <br><b>It should be called after `new XmagicApi()`.</b> |

## Static Functions

| API               | Description         |
| ----------------- | ---------- |
| [setLibPathAndLoad](#setlibpathandload) | Sets `libPath`. |

## Public Member Function Description

### XmagicApi

Constructor.
```
XmagicApi(Context context, String resDir)
XmagicApi(Context context, String resDir,OnXmagicPropertyErrorListener xmagicPropertyErrorListener)
```

#### Parameters
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Context context</td>
<td>Context.</td>
</tr>
<tr>
<td>String resDir</td>
<td>Resource file directory.<ul style="margin:0">
<li>If the SDK resource files are built into `assets`, before using the SDK for the first time, you need to copy the resources to the app's private directory: set the resource path through <code>XmagicResParser.setResPath(new File(getFilesDir(), "xmagic").getAbsolutePath())</code> first and then copy the resources through <code>XmagicResParser.copyRes(getApplicationContext())</code>. For more information, see the <code>LaunchActivity.java</code> of the demo.</li>
<li>If the SDK resource files are downloaded from the internet, after the download succeeds, set the resource path through <code>XmagicResParser.setResPath(validAssetsDirectory)</code>.</li>
<li>Get the previously set path through <code>XmagicResParser.getResPath()</code>.</li></ul></td>
</tr>
<tr>
<td>OnXmagicPropertyErrorListener xmagicPropertyErrorListener</td>
<td>Error callback API.</td>
</tr>
</tbody></table>
Error codes and descriptions:

| Error Code  | Description                    |
| ---- | --------------------- |
| -1   | An unknown error occurred.                |
| -100 | Failed to initialize 3D SDK resources.          |
| -200 | The GAN material is not supported.             |
| -300 | The device does not support this material component.           |
| -400 | The template JSON content is empty.           |
| -500 | The SDK version is too low.              |
| -600 | Keying is not supported.                |
| -700 | OpenGL is not supported.            |
| -800 | The script is not supported.                |
| 5000 | The resolution of the background image to be keyed exceeds 2160 x 3840. |
| 5001 | The memory required by background image keying is insufficient.        |
| 5002 | Failed to parse the background video to be keyed.         |
| 5003 | The background video to be keyed exceeds 200 seconds.       |
| 5004 | The format of the background video to be keyed is not supported.        |

------

### updateProperty

Modifies a beauty filter value, animated effect, or filter and can be called in any thread.

```
void updateProperty(XmagicProperty<?> p) 
```

#### Parameters
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>XmagicProperty&lt;?&gt; p</td>
<td>Tencent Effect SDK data entity class.
<ul style="margin:0"><li>Taking "skin smoothening" as an example, you can create an instance as follows: <br><code>new XmagicProperty&lt;&gt;(Category.BEAUTY,  null,  null,  BeautyConstant.BEAUTY_SMOOTH, new XmagicPropertyValues(0, 100, 50, 0, 1)));</code>. </li><li>Taking "2D animated effect Bunny" as an example, you can create an instance as follows:<br><code>new XmagicProperty&lt;&gt;(Category.MOTION, "video_tutujiang" ,  "animated effect file path",  null, null);</code>.<br>For more examples, see the <code>XmagicResParser.java</code> of the demo project.</li></ul></td>
</tr>
</tbody></table>

***

### updateProperties

Batch modifies beauty values, animated effects, or filters and can be called in any thread.

```
void updateProperties(List<XmagicProperty<?>> properties)
```

#### Parameters

| Parameter | Description |
| ----------------------------------- | ---------------------------- |
| (List&lt;XmagicProperty&lt;?>> properties | See the `updateProperty` method description. |

***

### setTipsListener

Sets the callback function for the animated effect prompt to display the prompt on the frontend page; for example, some materials will prompt the user to nod, stretch out their palms, or make a finger heart.

```
void setTipsListener(XmagicApi.XmagicTipsListener effectTipsListener) 
```

#### Parameters

| Parameter | Description |
| ----------------------------------------------- | ------------------------------------ |
| XmagicApi.XmagicTipsListener effectTipsListener | Callback function implementation class. The callback is not necessarily in the main thread. |

------

### setYTDataListener
Sets the callback for data such as face point information.
```
void setYTDataListener(XmagicApi.XmagicYTDataListener ytDataListener)
Sets the callback for data such as face information.

public interface XmagicYTDataListener {
    void onYTDataUpdate(String data)
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

#### Field description

| Field                           | Type    | Range                           | Description                            |
| -------------------------- |-------------------------- | --------------------------- | --------------------------- |
| trace_id                     | int   | [1,INF)                      | Face ID. The same ID points to the same face in the process of continuous stream fetching. |
| face_256_point               | float | [0,screenWidth] or [0,screenHeight] | 512 values in total for 256 facial keypoints. (0,0) is the top-left corner of the screen. |
| face_256_visible             | float | [0,1]                        | Visibility of the 256 facial keypoints.                  |
| out_of_screen                | bool  | true/false                   | Whether the face is out of the screen.                       |
| left_eye_high_vis_ratio      | float | [0,1]                        | Percentage of the highly visible points of the left eye.                   |
| right_eye_high_vis_ratio     | float | [0,1]                        | Percentage of the highly visible points of the right eye.                   |
| left_eyebrow_high_vis_ratio  | float | [0,1]                        | Percentage of the highly visible points of the left eyebrow.                   |
| right_eyebrow_high_vis_ratio | float | [0,1]                        | Percentage of the highly visible points of the right eyebrow.                   |
| mouth_high_vis_ratio         | float | [0,1]                        | Percentage of the highly visible points of the mouth.                    |

#### Parameters

| Parameter                                            | Description       |
| --------------------------------------------- | -------- |
| XmagicApi.XmagicYTDataListener ytDataListener | Callback function implementation class. |

------

### setAIDataListener

Calls back the point information of the detected face, body parts, and gestures.

```
public interface OnAIDataListener {

    void onFaceDataUpdated(List<FaceData> faceDataList);
    void onHandDataUpdated(List<HandData> handDataList);
    void onBodyDataUpdated(List<BodyData> bodyDataList);

}
```

### onPause

Pauses rendering, can be bound to the `onPause` lifecycle of `Activity`, and internally calls `onPauseAudio` only.

```
void onPause() 
```

------

### onResume

Resumes rendering and can be bound to the `onResume` lifecycle of `Activity`.

```
void onResume() 
```

------

### onDestroy

Clears GL thread resources and needs to be called within the GL thread. Sample code:

```java
// See the sample code in `MainActivity.java`
glSurfaceView.queueEvent(() -> {
                if (mXmagicApi != null) {
                    mXmagicApi.onPause();
                    mXmagicApi.onDestroy();
                }
            });
            
// See the sample code in `ImageInputActivity.java`
@Override
protected void onDestroy() {

    if (mHandler != null) {
        mHandler.destroy(() -> {
            if (mXmagicApi != null) {
                mXmagicApi.onPause();
                mXmagicApi.onDestroy();
        		}
    		});
    		mHandler.waitDone();
    }

    XmagicPanelDataManager.getInstance().clearData();
    super.onDestroy();
}
```

### process

Method to receive data by SDK rendering, which can be used within the camera data callback function.

```
// Render the texture
int process(int srcTextureId, int srcTextureWidth, int srcTextureHeight) 
// Render the bitmap
Bitmap process(Bitmap bitmap, boolean needReset){
```

#### Parameters

| Parameter | Description |
| ---------------------- | ------------------------------------------------------------ |
| int srcTextureId       | Texture that needs to be rendered.  |
| id int srcTextureWidth | Width of the texture that needs to be rendered. |
| int srcTextureHeight   | Height of the texture that needs to be rendered. |
| Bitmap bitmap          | The recommended maximum size is 2160 x 4096. Larger images have poor face recognition results or cannot get faces recognized and are likely to cause OOM problems. Shrink such images first before passing them in. |
| boolean needReset      | Set `needReset` to `true` for the following scenarios. <br><li/>Switch image.<li/>Use keying for the first time.<li/>Use animated effect for the first time.<li/>Use makeup for the first time. |

------

### onPauseAudio

Call this function when you only need to stop the audio but don't need to release the GL thread.

```
void onPauseAudio() 
```

------

### sensorChanged

Used to determine the current rotation angle of the phone, so as to adjust the basis for AI to recognize the angle of the face. This needs to be called in the callback function of the G-sensor.

```
void sensorChanged(SensorEvent event, Sensor accelerometer) 
```

#### Parameters

| Parameter                   | Description                                   |
| -------------------- | ------------------------------------ |
| SensorEvent event    | Event entity class returned by the G-sensor callback function `onSensorChanged`. |
| Sensor accelerometer | Sample G-sensor.                            |

------

### isDeviceSupport

Passes in the list of animated effect resources into the SDK for check, after which the `XmagicProperty.isSupport` field identifies whether the material is available. According to the value of `XmagicProperty.isSupport`, click restrictions can be controlled at the UI layer or removed from the resource list directly.

```
void isDeviceSupport(List<XmagicProperty<?>> assetsList)
```

#### Parameters

| Parameter                                 | Description           |
| ---------------------------------- | ------------ |
| List&lt;XmagicProperty&lt;?>> assetsList | List of animated effect materials to be checked. |

------

### getPropertyRequiredAbilities

Passes in a list of animated effect resources and returns a list of the SDK atomic capabilities used by each resource.
Use case of this method:
If you have purchased or made several animated effect materials, calling this method will return the list of atomic capabilities that each material needs to use. For example, material 1 needs to use capabilities A, B, and C, while material 2 needs to use capabilities B, C, and D. Then, you can keep this list on the server. After that, when a user wants to download the materials from the server, the user first gets the list of atomic capabilities supported by the user's phone through the `getDeviceAbilities` method (for example, the phone has capabilities A, B, and C but not D), and the list is then sent to the server. The server determines that the phone does not have capability D, so it will not deliver material 2 to the user.

#### Parameters

| Parameter                             | Description               |
| ------------------------------ | ---------------- |
| List&lt;XmagicProperty&lt;?>> assets | List of animated effect resources for which to check the atomic capabilities. |

#### Response

Returned value `Map<XmagicProperty<?>,ArrayList<String>>`:

- key: animated effect resource material entity class.
- value: list of used atomic capabilities.

------

### getDeviceAbilities

Returns the list of atomic capabilities supported by the current device and needs to be used together with the `getPropertyRequiredAbilities` method. For more information, see the `getPropertyRequiredAbilities` description.

```
Map<String,Boolean> getDeviceAbilities() 
```

#### Response

Returned value `Map<String,Boolean>`:
- key: atomic capability name (corresponding to the material capability name).
- value: whether it is supported by the current device.

------

### isSupportBeauty

Determines whether the current model supports beauty filters (OpenGL3.0).

```
boolean isSupportBeauty() 
```

#### Response

Returned value `boolean`: whether beauty filter is supported.

------

### isBeautyAuthorized

Determines which face/body beauty filters are supported by the current license. Only beauty filters of the `BEAUTY` and `BODY_BEAUTY` types can be checked. The check result is assigned to the `XmagicProperty.isAuth` field of each beauty filter object. Access to these items can be blocked on the UI if the `isAuth` field is `false`.

```
void isBeautyAuthorized(List<XmagicProperty<?>> properties) 
```

#### Parameters

| Parameter                                 | Description        |
| ---------------------------------- | --------- |
| List&lt;XmagicProperty&lt;?>> properties | Beauty filters that need to be checked. |

------

### setXmagicStreamType

Sets the input data type, which is Android camera data stream (XmagicApi.PROCESS_TYPE_CAMERA_STREAM) by default.

```
void setXmagicStreamType(int type)
```

#### Parameters

| Parameter       | Description                                                                                                                                        |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| int type | Data source type. Valid values:<ul style="margin:0"><li/><code>XmagicApi.PROCESS_TYPE_CAMERA_STREAM</code>: camera data source<li/><code>XmagicApi.PROCESS_TYPE_PICTURE_DATA</code>: image data source</ul> |

------

## Static Function Description

### setLibPathAndLoad

Sets the `so` file path and triggers loading. If the `so` file is built into `assets`, you don't need to call this method. If it is downloaded dynamically, this method needs to be called before authentication and `new XmagicApi`. 
- If a null value is passed in, the `so` library will be loaded from the default path. Make sure that it is built into the APK package.
- If a non-null value is passed in, such as `data/data/package name/files/xmagic_libs`, the `so` library will be loaded from this directory.

```
static boolean setLibPathAndLoad(String path) 
```

#### Parameters

| Parameter          | Description      |
| ----------- | ------- |
| String path | Path to store the `so` library. |

