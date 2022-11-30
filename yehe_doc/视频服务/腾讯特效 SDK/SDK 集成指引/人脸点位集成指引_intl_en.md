This capability detects when a face is partially captured or concealed or when there are multiple faces. It can recognize 256 facial keypoints.

## 256 Facial Keypoints
<img src="https://qcloudimg.tencent-cloud.cn/raw/ebf9e5e6ed208b6e8571520e3ff173e5.png" width=400>


## iOS APIs

### iOS integration
For directions on how to integrate the Tencent Effect iOS SDK, see [Integrating Tencent Effect SDK](https://intl.cloud.tencent.com/document/product/1143/45384).

### Registering an XMagic listener
```objectivec
/// @brief The SDK event listener
/// @param listener: The listener for SDK events, including AI events, tips, and resource events.
- (void)registerSDKEventListener:(id<YTSDKEventListener> _Nullable)listener;
```

### YTSDKEventListener
```objectivec
#pragma mark - Callback APIs
/// @brief SDK event callback APIs
@protocol YTSDKEventListener <NSObject>
/// @brief `YTDataUpdate` callback
/// @param event: Callback in NSString* format
- (void)onYTDataEvent:(id _Nonnull)event;
/// @brief AI event callback
/// @param event: Callback in dict format
- (void)onAIEvent:(id _Nonnull)event;
/// @brief Tip event callback
/// @param event: Callback in dict format
- (void)onTipsEvent:(id _Nonnull)event;
/// @brief Resource event callback
/// @param event: Callback in string format
- (void)onAssetEvent:(id _Nonnull)event;
@end
```

After the callbacks are configured successfully, the SDK will send a callback of facial data for each video frame.
```objectivec
- (void)onYTDataEvent:(id _Nonnull)event;
```
The data returned is in JSON format and includes the following fields (for details about the 256 facial keypoints, see the illustration above):
```objectivec
/// @note Callback fields
/**
| Field | Type | Value Range | Description |
| :---- | :---- |:---- | :---- |
| trace_id                     | int   | [1,INF)                      | The face ID. If the faces obtained from a continuous video stream have the same face ID, they belong to the same person. |
| face_256_point               | float | [0, screenWidth/screenHeight] | The position of a facial keypoint. There are 512 values in total for 256 facial keypoints. (0, 0) is the top-left corner of the screen. |
| face_256_visible             | float | [0,1]                               | The visibility of the 256 facial keypoints.                                    |
| out_of_screen                | bool  | true/false                          | Whether only part of the face is captured.                                           |
| left_eye_high_vis_ratio      | float | [0,1]                               | The percentage of keypoints with high visibility for the left eye.                                    |
| right_eye_high_vis_ratio     | float | [0,1]                               | The percentage of keypoints with high visibility for the right eye.                                   |
| left_eyebrow_high_vis_ratio  | float | [0,1]                        | The percentage of keypoints with high visibility for the left eyebrow.                   |
| right_eyebrow_high_vis_ratio | float | [0,1]                        | The percentage of keypoints with high visibility for the right eyebrow.                   |
| mouth_high_vis_ratio         | float | [0,1]                               | The percentage of keypoints with high visibility for the mouth.                                     |
**/
- (void)onYTDataEvent:(id _Nonnull)event;
```

## Android APIs

### Android integration

For directions on how to integrate the Tencent Effect Android SDK, see [Integrating Tencent Effect SDK](https://intl.cloud.tencent.com/document/product/1143/45385).

### Registering an XMagic listener

Configure the callback of facial keypoints and other data:
```java
void setYTDataListener(XmagicApi.XmagicYTDataListener ytDataListener)
Configure the callback of facial keypoints and other data

public interface XmagicYTDataListener {
    void onYTDataUpdate(String data)
}
```
`onYTDataUpdate` returns a JSON string that contains the information of up to five faces.
```json
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

### Fields

| Field                         | Type  | Value Range                                | Remarks                                                   |
| :--------------------------- | :---- | :---------------------------------- | :------------------------------------------------------- |
| trace_id                     | int   | [1,INF)                      | The face ID. If the faces obtained from a continuous video stream have the same face ID, they belong to the same person. |
| face_256_point               | float | [0, screenWidth/screenHeight] | The position of a facial keypoint. There are 512 values in total for 256 facial keypoints. (0, 0) is the top-left corner of the screen. |
| face_256_visible             | float | [0,1]                               | The visibility of the 256 facial keypoints.                                    |
| out_of_screen                | bool  | true/false                          | Whether only part of the face is captured.                                           |
| left_eye_high_vis_ratio      | float | [0,1]                               | The percentage of keypoints with high visibility for the left eye.                                    |
| right_eye_high_vis_ratio     | float | [0,1]                               | The percentage of keypoints with high visibility for the right eye.                                   |
| left_eyebrow_high_vis_ratio  | float | [0,1]                        | The percentage of keypoints with high visibility for the left eyebrow.                   |
| right_eyebrow_high_vis_ratio | float | [0,1]                        | The percentage of keypoints with high visibility for the right eyebrow.                   |
| mouth_high_vis_ratio         | float | [0,1]                               | The percentage of keypoints with high visibility for the mouth.                                     |

#### Parameters

| Parameter       | Description                                                                                                                                        |
| :-------------------------------------------- | :--------------- |
| XmagicApi.XmagicYTDataListener ytDataListener | The callback implementation class. |
