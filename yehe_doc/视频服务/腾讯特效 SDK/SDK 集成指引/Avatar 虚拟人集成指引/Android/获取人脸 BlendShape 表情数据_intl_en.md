## Overview
This feature allows you to generate 52 blendshapes using the standards of Apple ARKit based on the OpenGL textures captured by the camera. For details, see [ARFaceAnchor](https://developer.apple.com/documentation/arkit/arfaceanchor/blendshapelocation). You can perform further development based on the blendshape data. For example, you can pass the data to Unity to drive your model.

## Integration
For directions on how to integrate the Tencent Effect Android SDK, see [Integrating Tencent Effect SDK](https://intl.cloud.tencent.com/document/product/1143/45385).

### API calls
1. Enable effects:
```
//XmagicApi.java
//featureName = XmagicConstant.FeatureName.ANIMOJI_52_EXPRESSION
public void setFeatureEnableDisable(String featureName, boolean enable);

```
2. Configure the callback of facial keypoints.
```java
//XmagicApi.java
void setYTDataListener(XmagicApi.XmagicYTDataListener ytDataListener)

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
  "mouth_high_vis_ratio":1.0,
  "expression_weights":[
		0.12,
		-0.32
		...
	]
 },
 ...
 ]
}
```

### Fields
- **trace_id**: The face ID. If the faces obtained from a continuous video stream have the same face ID, they belong to the same person. |
- **expression_weights**: Real-time blendshape data, which is an array of 52 elements. The value range of the elements is -1.0 to 1.0.
- The other fields are [facial keypoint information](https://intl.cloud.tencent.com/document/product/1143/45399). Whether they are returned depends on the type of license you use. If you only need facial expression data, you can ignore those fields.