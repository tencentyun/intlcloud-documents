## 기능 설명
이 기능을 사용하면 카메라에서 캡처한 openGL 텍스처를 기반으로 Apple ARKit의 표준을 사용하여 52개의 BlendShape를 생성할 수 있습니다. 자세한 내용은 [ARFaceAnchor](https://developer.apple.com/documentation/arkit/arfaceanchor/blendshapelocation)를 참고하십시오. blendshape 데이터를 기반으로 추가 개발을 수행할 수 있습니다. 예를 들어 Unity에 데이터를 전달하여 모델을 구동할 수 있습니다.

## Android 통합 가이드
Tencent Effect Android SDK를 통합하는 방법에 대한 지침은 [Tencent Effect SDK 통합하기](https://intl.cloud.tencent.com/document/product/1143/45385)를 참고하십시오.

### API 호출
1. 효과 활성화:
```
//XmagicApi.java
//featureName = XmagicConstant.FeatureName.ANIMOJI_52_EXPRESSION
public void setFeatureEnableDisable(String featureName, boolean enable);

```
2. 얼굴 키포인트의 콜백을 구성합니다.
```java
//XmagicApi.java
void setYTDataListener(XmagicApi.XmagicYTDataListener ytDataListener)

public interface XmagicYTDataListener {
    void onYTDataUpdate(String data)
}
```
onYTDataUpdate 는 JSON string 구조를 반환하고 최대 5개의 안면 인식 정보를 반환합니다.
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

### 필드 의미
- **trace_id**: 얼굴 ID입니다. 연속 비디오 스트림 과정에서 얻은 얼굴의 얼굴 ID가 동일하면 동일한 사람으로 간주할 수 있습니다.
- **expression_weights**: 실시간 blendshape 데이터입니다. 52개 요소의 배열이며, 요소의 값 범위는 -1.0에서 1.0입니다.
- 나머지 필드는 [얼굴 특징 정보](https://intl.cloud.tencent.com/document/product/1143/45399)입니다. 반환 여부는 사용하는 License 유형에 따라 다릅니다. 얼굴 표정 데이터만 필요한 경우 해당 필드를 무시할 수 있습니다.