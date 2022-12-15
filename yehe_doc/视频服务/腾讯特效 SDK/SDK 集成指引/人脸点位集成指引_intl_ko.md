이 기능은 얼굴이 프레임을 벗어났거나, 가려졌거나 여러 얼굴이 있는 경우를 감지합니다. 256개의 얼굴 특징점을 인식할 수 있습니다.

## 256 얼굴 키포인트
<img src="https://qcloudimg.tencent-cloud.cn/raw/ebf9e5e6ed208b6e8571520e3ff173e5.png" width=400>


## iOS API

### iOS 통합
Tencent Effect iOS SDK 통합 방법은 [Tencent Effect SDK 통합하기](https://intl.cloud.tencent.com/document/product/1143/45384)를 참고하십시오.

### XMagic 리스너 등록
```objectivec
/// @brief SDK 이벤트 리스너
/// @param listener: 이벤트 리스너 콜백, 주로 AI 이벤트, Tips 프롬프트 이벤트, Asset 이벤트로 구분
- (void)registerSDKEventListener:(id<YTSDKEventListener> _Nullable)listener;
```

### YTSDKEventListener
```objectivec
#pragma mark - 콜백 API
/// @brief SDK 이벤트 콜백 API
@protocol YTSDKEventListener <NSObject>
/// @brief YTDataUpdate 콜백
/// @param event NSString*형식의 콜백
- (void)onYTDataEvent:(id _Nonnull)event;
/// @brief AI 이벤트 콜백
/// @param event dict 형식의 콜백
- (void)onAIEvent:(id _Nonnull)event;
/// @brief 팁 이벤트 콜백
/// @param event dict 형식의 콜백
- (void)onTipsEvent:(id _Nonnull)event;
/// @brief 리소스 이벤트 콜백
/// @param event string 형식의 콜백
- (void)onAssetEvent:(id _Nonnull)event;
@end
```

콜백이 성공적으로 구성된 후 SDK는 각 비디오 프레임에 대한 얼굴 데이터의 콜백을 보냅니다.
```objectivec
- (void)onYTDataEvent:(id _Nonnull)event;
```
반환된 data는 JSON 형식이며 다음 필드를 포함합니다(256개의 얼굴 키포인트에 대한 자세한 내용은 위 그림 참고).
```objectivec
/// @note 콜백 필드
/**
| 필드 | 유형 | 값 범위 | 설명 |
| :---- | :---- |:---- | :---- |
| trace_id | int | [1,INF) | 얼굴 id, 연속 비디오 스트림에서 얻은 얼굴의 얼굴 id가 동일하면 동일한 사람으로 간주할 수 있습니다 |
| face_256_point | float | [0,screenWidth] 또는 [0,screenHeight] | 얼굴 키포인트의 위치, 256개의 얼굴 키포인트에 대해 총 512개의 값이 있습니다. (0, 0)은 화면의 왼쪽 상단 모서리입니다 |
| face_256_visible | float | [0,1] | 얼굴 256 키 포인트 가시도 |
| out_of_screen | bool  | true/false | 얼굴이 프레임 밖에 있는지 여부 |
| left_eye_high_vis_ratio | float | [0,1] | 왼쪽 눈의 가시성이 높은 키포인트의 비율 |
| right_eye_high_vis_ratio | float | [0,1] | 오른쪽 눈의 가시성이 높은 키포인트의 비율 |
| left_eyebrow_high_vis_ratio | float | [0,1] | 왼쪽 눈썹의 가시성이 높은 키포인트의 비율 |
| right_eyebrow_high_vis_ratio | float | [0,1] | 오른쪽 눈썹의 가시성이 높은 키포인트의 비율 |
| mouth_high_vis_ratio | float | [0,1] | 입에 대한 가시성이 높은 키포인트의 비율 |
**/
- (void)onYTDataEvent:(id _Nonnull)event;
```

## Android API

### Android 통합

Tencent Effect Android SDK 통합 방법은 [Tencent Effect SDK 통합하기](https://intl.cloud.tencent.com/document/product/1143/45385)를 참고하십시오.

### Xmagic 리스너 등록

얼굴 키포인트 및 기타 데이터의 콜백을 구성합니다.
```java
void setYTDataListener(XmagicApi.XmagicYTDataListener ytDataListener)
안면 인식 정보 등 데이터 콜백 설정

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
  "mouth_high_vis_ratio":1.0
 },
 ...
 ]
}
```

### 필드 의미

| 필드                         | 유형  | 값범위                                | 설명                                                   |
| :--------------------------- | :---- | :---------------------------------- | :------------------------------------------------------- |
| trace_id                     | int   | [1,INF)                      | 얼굴 ID입니다. 연속 비디오 스트림에서 얻은 얼굴의 얼굴 ID가 동일하면 동일한 사람에 속합니다. |
| face_256_point               | float | [0,screenWidth] 또는 [0,screenHeight] | 얼굴 키포인트의 위치입니다. 256개의 얼굴 키포인트에 대해 총 512개의 값이 있습니다. (0, 0)은 화면의 왼쪽 상단 모서리입니다.          |
| face_256_visible             | float | [0,1]                               | 256개의 얼굴 키포인트의 가시성입니다.                                    |
| out_of_screen                | bool  | true/false                          | 얼굴이 프레임 밖에 있는지 여부입니다.                                           |
| left_eye_high_vis_ratio      | float | [0,1]                               | 왼쪽 눈의 가시성이 높은 키포인트의 비율입니다.                                   |
| right_eye_high_vis_ratio     | float | [0,1]                               | 오른쪽 눈의 가시성이 높은 키포인트의 비율입니다.                                   |
| left_eyebrow_high_vis_ratio  | float | [0,1]                        | 왼쪽 눈썹의 가시성이 높은 키포인트의 비율입니다.                                   |
| right_eyebrow_high_vis_ratio | float | [0,1]                        | 오른쪽 눈썹의 가시성이 높은 키포인트의 비율입니다.                                   |
| mouth_high_vis_ratio         | float | [0,1]                               | 입에 대한 가시성이 높은 키포인트의 비율입니다.                                     |

#### 매개변수

| 매개변수                                          | 의미             |
| :-------------------------------------------- | :--------------- |
| XmagicApi.XmagicYTDataListener ytDataListener | 콜백 구현 클래스입니다. |
