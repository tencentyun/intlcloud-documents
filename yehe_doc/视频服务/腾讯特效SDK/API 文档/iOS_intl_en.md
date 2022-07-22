This document describes core APIs (`XMagic.h`) of the Tencent Effect SDK, which you can use to initialize the SDK, change beauty filter parameters, and call animated effects.

## Public Member APIs

| API | Description |
| ------------- | ------------- |
| [initWithRenderSize](#initwithrendersize) | Initialization API |
| [initWithGlTexture](#initwithgltexture) | Initialization API |
| [configPropertyWithType](#configpropertywithtype) | Configures effects. |
| [setRenderSize](#setrendersize) | Sets the render size. |
| [deinit](#deinit) | Releases resources. |
| [process](#process) | Processes data. |
| [processUIImage](#processuiimage) | Processes an image. |
| [getConfigPropertyWithName](#getconfigpropertywithname) | Gets effect information. |
| [registerLoggerListener](#registerloggerlistener) | Registers a log listener. |
| [registerSDKEventListener](#registersdkeventlistener)   | Register a listener for SDK events. |
| [clearListeners](#clearlisteners) | Removes listeners. |
| [getCurrentGlContext](#getcurrentglcontext) | Gets the current OpenGL context. |
| [onPause](#onpause) | Pauses the SDK. |
| [onResume](#onresume) | Resumes the SDK. |

### initWithRenderSize
This API is used for initialization.
```objectivec
- (instancetype _Nonnull)initWithRenderSize:(CGSize)renderSize
                        assetsDict:(NSDictionary* _Nullable)assetsDict;
```

**Parameters**

| Parameter      | Description    |
| ---------- | -------- |
| renderSize | The render size. |
| assetsDict | The resource dictionary. |

### initWithGlTexture
This API is used for initialization.

```objectivec
- (instancetype _Nonnull)initWithGlTexture:(unsigned)textureID
                        width:(int)width
                        height:(int)height
                        flipY:(bool)flipY
                        assetsDict:(NSDictionary* _Nullable)assetsDict;
```

**Parameters**

| Parameter      | Description         |
| ---------- | ------------ |
| textureID  | The texture ID.      |
| width      | The render size.     |
| height     | The render size.     |
| flipY      | Whether to flip the image. |
| assetsDict | The resource dictionary.    |

### configPropertyWithType

This API is used to configure effects.

```objectivec
- (int)configPropertyWithType:(NSString *_Nonnull)propertyType withName:(NSString *_Nonnull)propertyName withData:(NSString*_Nonnull)propertyValue withExtraInfo:(id _Nullable)extraInfo;
```

**Parameters**

| Parameter      | Description                            |
| ------------- | --------------------------- |
| propertyType  | The effect type.                    |
| propertyName  | The effect name.                    |
| propertyValue | The effect value.                    |
| extraInfo     | A reserved parameter, which can be used for dictionary configuration.   |

#### Examples

- **Beautification**: Configuring the skin brightening effect
```objectivec
NSString *propertyType = @"beauty";        //Set the effect type
NSString *propertyName = @"beauty.whiten"; //Specify the effect name
NSString *propertyValue = @"60";           //Set the effect value
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:nil];
```
- **Filter**: Configuring the Allure filter
```objectivec
NSString *propertyType = @"lut";        //Set the effect type
NSString *propertyName = [@"lut.bundle/" stringByAppendingPathComponent:@"xindong_lf.png"]; //Specify the effect name
NSString *propertyValue = @"60";           //Set the effect value
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:nil];
```
- **Body retouch**: Configuring the long leg effect
```objectivec
NSString *propertyType = @"body";        //Set the effect type
NSString *propertyName = @"body.legStretch"; //Specify the effect name
NSString *propertyValue = @"60";           //Set the effect value
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:nil];
```
- **Animated effect**: Configuring the animated 2D cute effect
```objectivec
 NSString *motion2dResPath = [[NSBundle mainBundle] pathForResource:@"2dMotionRes" ofType:@"bundle"];//The absolute path of the `2dMotionRes` folder
 NSString *propertyType = @"motion";        //Set the effect type
 NSString *propertyName = @"video_keaituya"; //Specify the effect name
 NSString *propertyValue = motion2dResPath;  //Set the path of the animated effect
 [self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:nil];
```
- **Makeup**: Configuring the girl group makeup effect
```objectivec
NSString *motionMakeupResPath = [[NSBundle mainBundle] pathForResource:@"makeupMotionRes" ofType:@"bundle"];//The absolute path of the `makeupMotionRes` folder
NSString *propertyType = @"motion";        //Set the effect type
NSString *propertyName = @"video_nvtuanzhuang"; //Specify the effect name
NSString *propertyValue = motionMakeupResPath;  //Set the path of the animated effect
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:nil];
//Below are settings for the makeup effect (you only need to configure the above parameters once and can change the following settings multiple times)
 NSString *propertyTypeMakeup = @"custom";         //Set the effect type
 NSString *propertyNameMakeup = @"makeup.strength"; //Specify the effect name
 NSString *propertyValueMakeup = @"60";             //Set the effect value
 [self.xmagicApi configPropertyWithType:propertyTypeMakeup withName:propertyNameMakeup withData:propertyValueMakeup withExtraInfo:nil];
```
- **Keying**: Configuring the background blurring effect (strong)
```objectivec
NSString *motionSegResPath = [[NSBundle mainBundle] pathForResource:@"segmentMotionRes" ofType:@"bundle"];//The absolute path of the `segmentMotionRes` folder
NSString *propertyType = @"motion";         //Set the effect type
NSString *propertyName = @"video_segmentation_blur_75"; //Specify the effect name
NSString *propertyValue = motionSegResPath;  //Set the path of the animated effect
NSDictionary *dic = @{@"bgName":@"BgSegmentation.bg.png", @"bgType":@0, @"timeOffset": @0},@"icon":@"segmentation.linjian.png"};//Configure the reserved parameter
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:dic];
```
- **Custom background**:
```objectivec
NSString *motionSegResPath = [[NSBundle mainBundle] pathForResource:@"segmentMotionRes" ofType:@"bundle"];//The absolute path of the `segmentMotionRes` folder
NSString *propertyType = @"motion";         //Set the effect type
NSString *propertyName = @"video_empty_segmentation"; //Specify the effect name
NSString *propertyValue = motionSegResPath;  //Set the path of the animated effect
NSString *imagePath = @"/var/mobile/Containers/Data/Application/06B00BBC-9060-450F-8D3A-F6028D185682/Documents/MediaFile/image.png"; //The absolute path of the background image or video (after compression)
int bgType = 0;//The background type. 0: image; 1: video
int timeOffset = 0；//The duration. If an image is used as the background, its value is 0; if a video is used, its value is the video length.
NSDictionary *dic = @{@"bgName":imagePath, @"bgType":@(bgType), @"timeOffset": @(timeOffset)},@"icon":@"segmentation.linjian.png"};//Configure the reserved parameter
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:dic];
```

### setRenderSize

This API is used to set the render size.

```objectivec
- (void)setRenderSize:(CGSize)size;
```

**Parameters**

| Parameter   | Description     |
| ---- | -------- |
| size | The render size. |

### deinit

This API is used to release resources.

```objectivec
- (void)deinit;
```

### Process

This API is used to process data.

```objectivec
- (YTProcessOutput* _Nonnull)process:(YTProcessInput * _Nonnull)input;
```

**Parameters**

| Parameter      | Description      |
| ----- | ---------------- |
| input | The input data. |

### processUIImage

This API is used to process an image.
```objectivec
- (UIImage* _Nullable)processUIImage:(UIImage* _Nonnull)inputImage needReset:(bool)needReset;
```

**Parameters**

| Parameter       | Description                                                                                                                                        |
| ---------- | ------------------------------------------------------------ |
| inputImage | The input image. If your image is larger than 2160 x 4096, we recommend you reduce its size before passing it in; otherwise, face recognition may fail or may be inaccurate. It may also cause an OOM error. |
| needReset  | This parameter must be set to `true` in the following cases: <ul style="margin:0"><li>The image processed is changed</li><li>The first time a keying effect is used</li><li>The first time an animated effect is used</li><li>The first time a makeup effect is used</li></ul> |

### getConfigPropertyWithName

This API is used to get effect information.

```objectivec
- (YTBeautyPropertyInfo * _Nullable)getConfigPropertyWithName:(NSString *_Nonnull)propertyName;
```

**Parameters**

| Parameter      | Description                            |
| ------------ | -------- |
| propertyName | The effect name. |

### registerLoggerListener

This API is used to register a log listener.

```objectivec
- (void)registerLoggerListener:(id<YTSDKLogListener> _Nullable)listener withDefaultLevel:(YtSDKLoggerLevel)level;
```

**Parameters**

| Parameter      | Description                            |
| -------- | -------------------------- |
| listener | The log callback.               |
| level    | The log output level, which is ERROR by default. |

### registerSDKEventListener

This API is used to register a listener for SDK events.

```objectivec
- (void)registerSDKEventListener:(id<YTSDKEventListener> _Nullable)listener;
```

**Parameters**

| Parameter       | Description                                                                                                                                        |
| -------- | ----------------------------------------------------------- |
| listener | The listener for SDK events, including AI events, tips, and resource events. |

### clearListeners

This API is used to remove listeners.

```objectivec
- (void)clearListeners;
```

### getCurrentGlContext

This API is used to get the current OpenGL context.

```objectivec
- (nullable EAGLContext*)getCurrentGlContext;
```

### onPause

This API is used to pause the SDK.

```objectivec
/// @brief When your app is switched to the background, you need to call this API to pause the SDK
- (void)onPause;
```

### onResume

This API is used to resume the SDK.

```objectivec
/// @brief When your app is switched back to the foreground, you need to call this API to resume the SDK
- (void)onResume;
```

## Static APIs

| API | Description |
| ----------------------------------------- | ------------------------ |
| [isBeautyAuthorized](#isbeautyauthorized) | Gets the authorization information of an effect parameter. |

### isBeautyAuthorized

This API is used to get the authorization information of an effect parameter.

```objectivec
/// @param featureId: The effect parameter.
/// @return: The authorization information of the effect parameter.
+ (BOOL)isBeautyAuthorized:(NSString * _Nullable)featureId;
```

## Callback APIs

| API | Description |
| ----------------------------------------- | -------------------- |
| [YTSDKEventListener](#ytsdkeventlistener) | The SDK event callback.  |
| [YTSDKLogListener](#ytsdkloglistener)     | The log callback.         |


### YTSDKEventListener

The callback for the internal events of the SDK.
```objectivec
@protocol YTSDKEventListener <NSObject>
```

#### Member callback APIs
| Return Type | Callback                            |
| -------- | ------------------------------- |
| void     | [onYTDataEvent](#onytdataevent) |
| void     | [onAIEvent](#onaievent)         |
| void     | [onTipsEvent](#ontipsevent)     |
| void     | [onAssetEvent](#onassetevent)   |

#### Callback description

##### onYTDataEvent
The YTDataUpdate event callback.

```objectivec
/// @param event: Callback in NSString* format
- (void)onYTDataEvent:(id _Nonnull)event;
```

The information of up to five faces is returned as JSON strings.

```objectivec
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

**Field Description**

| Field                         | Type  | Value Range                                | Remarks                                                   |
| ---------------------------- | ----- | ----------------------------------- | ------------------------------------------------------ |
| trace_id                     | int   | [1,INF)                      | The face ID. If the faces obtained continuously from a video stream have the same face ID, they belong to the same person. |
| face_256_point               | float | [0,screenWidth] or [0,screenHeight] | 512 values in total for 256 facial keypoints. (0,0) is the top-left corner of the screen. |
| face_256_visible             | float | [0,1]                               | The visibility of the 256 facial keypoints.                                    |
| out_of_screen                | bool  | true/false                          | Whether only part of the face is captured.                                           |
| left_eye_high_vis_ratio      | float | [0,1]                               | The percentage of keypoints with high visibility for the left eye.                                    |
| right_eye_high_vis_ratio     | float | [0,1]                               | The percentage of keypoints with high visibility for the right eye.                                   |
| left_eyebrow_high_vis_ratio  | float | [0,1]                        | The percentage of keypoints with high visibility for the left eyebrow.                   |
| right_eyebrow_high_vis_ratio | float | [0,1]                        | The percentage of keypoints with high visibility for the right eyebrow.                   |
| mouth_high_vis_ratio         | float | [0,1]                               | The percentage of keypoints with high visibility for the mouth.                                     |

##### onAIEvent
The callback for AI events.

```objectivec
/// @param event: Callback in dict format
- (void)onAIEvent:(id _Nonnull)event;
```

##### onTipsEvent
The callback for tips.

```objectivec
/// @param event: Callback in dict format
- (void)onTipsEvent:(id _Nonnull)event;
```

##### onAssetEvent
The callback for resource events.

```objectivec
/// @param event: Callback in string format
- (void)onAssetEvent:(id _Nonnull)event;
```

### YTSDKLogListener

The log callback.

```objectivec
@protocol YTSDKLogListener <NSObject>
```

#### Member callback APIs

| Return Type | API |
| -------- | -------- |
| void     | onLog    |

#### Callback description

##### onLog

The log callback.

```objectivec
/// @param loggerLevel: The current log level.
/// @param logInfo: The log information.
- (void)onLog:(YtSDKLoggerLevel) loggerLevel withInfo:(NSString * _Nonnull) logInfo;
```

