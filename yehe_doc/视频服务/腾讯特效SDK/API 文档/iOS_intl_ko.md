Tencent 특수 효과 SDK 핵심 인터페이스 클래스 `XMagic.h`는 SDK 초기화, 뷰티 필터 값 업데이트, 애니메이션 호출 등 기능에 사용됩니다.

## Public 멤버 함수

| API   | 설명  |
| ------------- | ------------- |
| [initWithRenderSize](#initwithrendersize) | 인터페이스 초기화 |
| [initWithGlTexture](#initwithgltexture) | 인터페이스 초기화 |
| [configPropertyWithType](#configpropertywithtype) | 뷰티 필터의 다양한 효과 설정 |
| [emitBlurStrengthEvent](#emitblurstrengthevent) | 후처리 블러 강도 설정(모든 블러 컴포넌트에 작용) |
| [setRenderSize](#setrendersize) | renderSize 설정 |
| [deinit](#deinit) | 리소스 릴리스 인터페이스 |
| [process](#process) | 데이터 처리 인터페이스 |
| [processUIImage](#processuiimage) | 이미지 프로세스 |
| [getConfigPropertyWithName](#getconfigpropertywithname) | 뷰티 필터 매개변수 설정 정보 가져오기 |
| [registerLoggerListener](#registerloggerlistener) | 로그 등록 인터페이스 |
| [registerSDKEventListener](#registersdkeventlistener)   | SDK 이벤트 리스너 인터페이스 |
| [clearListeners](#clearlisteners) | 콜백 정리 인터페이스 등록 |
| [getCurrentGlContext](#getcurrentglcontext) | 현재 GL 컨텍스트 인터페이스 가져오기 |
| [onPause](#onpause) | SDK 일시 중지 인터페이스 |
| [onResume](#onresume) | SDK 재개 인터페이스 |

### initWithRenderSize
인터페이스 초기화
```objectivec
- (instancetype _Nonnull)initWithRenderSize:(CGSize)renderSize
                        assetsDict:(NSDictionary* _Nullable)assetsDict;
```

**매개변수**

| 매개변수       | 의미     |
| ---------- | -------- |
| renderSize | 렌더링 크기 |
| assetsDict | 리소스 Dict |

### initWithGlTexture
인터페이스 초기화

```objectivec
- (instancetype _Nonnull)initWithGlTexture:(unsigned)textureID
                        width:(int)width
                        height:(int)height
                        flipY:(bool)flipY
                        assetsDict:(NSDictionary* _Nullable)assetsDict;
```

**매개변수**

| 매개변수       | 의미         |
| ---------- | ------------ |
| textureID  | 텍스처 ID      |
| width      | 렌더링 크기     |
| height     | 렌더링 크기     |
| flipY      | 이미지 뒤집기 여부 |
| assetsDict | 리소스 Dict    |

### configPropertyWithType

뷰티 필터 효과 구성

```objectivec
- (int)configPropertyWithType:(NSString *_Nonnull)propertyType withName:(NSString *_Nonnull)propertyName withData:(NSString*_Nonnull)propertyValue withExtraInfo:(id _Nullable)extraInfo;
```

**매개변수**

| 매개변수         | 의미                        |
| ------------- | --------------------------- |
| propertyType  | 효과 유형                    |
| propertyName  | 효과 이름                    |
| propertyValue | 효과 값                    |
| extraInfo     | 예약 확장, 추가 별도 구성 Dict |

#### 뷰티 필터 효과 설정 예시

- **뷰티 필터:** 미백 효과 설정
```objectivec
NSString *propertyType = @"beauty";        //뷰티 필터 효과 유형 설정, 뷰티 필터 예시
NSString *propertyName = @"beauty.whiten"; //뷰티 필터 이름 설정, 미백 예시
NSString *propertyValue = @"60";           //미백 효과 값 설정
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:nil];
```
- **필터**: 설렘 효과 설정
```objectivec
NSString *propertyType = @"lut";        //뷰티 필터 효과 유형 설정, 필터 예시
NSString *propertyName = [@"lut.bundle/" stringByAppendingPathComponent:@"xindong_lf.png"]; //뷰티 필터 이름 설정, 설렘 예시
NSString *propertyValue = @"60";           //필터 효과 값 설정
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:nil];
```
- **몸매 보정**: 긴 다리 효과 설정
```objectivec
NSString *propertyType = @"body";        //뷰티 필터 효과 유형 설정, 몸매 보정 예시
NSString *propertyName = @"body.legStretch"; //뷰티 필터 이름 설정, 긴 다리 예시
NSString *propertyValue = @"60";           //긴 다리 효과 값 설정
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:nil];
```
- **애니메이션**: 2D 애니메이션으로 귀여운 그래피티 효과 설정
```objectivec
 NSString *motion2dResPath = [[NSBundle mainBundle] pathForResource:@"2dMotionRes" ofType:@"bundle"];//2dMotionRes 폴더의 절대 경로
 NSString *propertyType = @"motion";         //뷰티 필터 효과 유형 설정, 애니메이션 효과 예시
 NSString *propertyName = @"video_keaituya"; //뷰티 필터 이름 설정, 2D 애니메이션으로 귀여운 그래피티 효과 예시
 NSString *propertyValue = motion2dResPath;  //애니메이션 효과 경로 설정
 [self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:nil];
```
- **메이크업**: 걸그룹 메이크업 효과 설정
```objectivec
NSString *motionMakeupResPath = [[NSBundle mainBundle] pathForResource:@"makeupMotionRes" ofType:@"bundle"];//makeMotionRes 폴더의 절대 경로
NSString *propertyType = @"motion";         //뷰티 필터 효과 유형 설정, 메이크업 예시
NSString *propertyName = @"video_nvtuanzhuang"; //뷰티 필터 이름 설정, 걸그룹 메이크업 예시
NSString *propertyValue = motionMakeupResPath;  //애니메이션 효과 경로 설정
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:nil];
//아래는 메이크업 값 설정(위의 애니메이션 효과는 한 번만 호출하면 되며, 아래의 메이크업 값 설정은 여러 번 호출 가능)
 NSString *propertyTypeMakeup = @"custom";         //뷰티 필터 효과 유형 설정, 메이크업 예시
 NSString *propertyNameMakeup = @"makeup.strength"; //뷰티 필터 이름 설정, 걸그룹 메이크업 예시
 NSString *propertyValueMakeup = @"60";             //메이크업 효과값 설정
 [self.xmagicApi configPropertyWithType:propertyTypeMakeup withName:propertyNameMakeup withData:propertyValueMakeup withExtraInfo:nil];
```
- **분할**: 배경 블러 처리 설정(강한 효과)
```objectivec
NSString *motionSegResPath = [[NSBundle mainBundle] pathForResource:@"segmentMotionRes" ofType:@"bundle"];//segmentMotionRes 폴더의 절대 경로
NSString *propertyType = @"motion";         //뷰티 필터 효과 유형 설정, 분할 예시
NSString *propertyName = @"video_segmentation_blur_75"; //뷰티 필터 이름 설정, 배경 블러 처리-강함 예시
NSString *propertyValue = motionSegResPath;  //애니메이션 효과 경로 설정
NSDictionary *dic = @{@"bgName":@"BgSegmentation.bg.png", @"bgType":@0, @"timeOffset": @0},@"icon":@"segmentation.linjian.png"};//예약 필드 설정
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:dic];
```
- **사용자 정의 배경**:
```objectivec
NSString *motionSegResPath = [[NSBundle mainBundle] pathForResource:@"segmentMotionRes" ofType:@"bundle"];//segmentMotionRes 폴더의 절대 경로
NSString *propertyType = @"motion";         //뷰티 필터 효과 유형 설정, 분할 예시
NSString *propertyName = @"video_empty_segmentation"; //뷰티 필터 이름 설정, 사용자 정의 배경 예시
NSString *propertyValue = motionSegResPath;  //애니메이션 효과 경로 설정
NSString *imagePath = @"/var/mobile/Containers/Data/Application/06B00BBC-9060-450F-8D3A-F6028D185682/Documents/MediaFile/image.png"; //사용자 정의 배경 이미지의 절대 경로입니다. 사용자 정의 배경으로 비디오를 선택한 경우 비디오를 압축 및 트랜스 코딩해야 하며 압축 및 트랜스 코딩 후의 절대 경로 사용
int bgType = 0;//사용자 정의 배경 유형입니다. 0이미지, 1비디오
int timeOffset = 0；//지속 시간. 이미지 배경일 때 0; 비디오 배경 시 비디오 지속 시간
NSDictionary *dic = @{@"bgName":imagePath, @"bgType":@(bgType), @"timeOffset": @(timeOffset)},@"icon":@"segmentation.linjian.png"};//예약 필드 설정
[self.xmagicApi configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:dic];
```

### emitBlurStrengthEvent

후처리 블러 강도 설정(모든 블러 컴포넌트에 작용)

```objectivec
- (void)emitBlurStrengthEvent:(int)strength;
```

**매개변수**

| 매개변수     | 의미     |
| -------- | -------- |
| strength | 효과 값 |

### setRenderSize

renderSize 설정

```objectivec
- (void)setRenderSize:(CGSize)size;
```

**매개변수**

| 매개변수 | 의미     |
| ---- | -------- |
| size | 렌더링 크기 |

### deinit

리소스 릴리스 인터페이스

```objectivec
- (void)deinit;
```

### process

데이터 인터페이스 처리

```objectivec
- (YTProcessOutput* _Nonnull)process:(YTProcessInput * _Nonnull)input;
```

**매개변수**

| 매개변수  | 의미             |
| ----- | ---------------- |
| input | 처리 데이터 정보 입력 |

### processUIImage

이미지 처리
```objectivec
- (UIImage* _Nullable)processUIImage:(UIImage* _Nonnull)inputImage needReset:(bool)needReset;
```

**매개변수**

| 매개변수       | 의미                                                         |
| ---------- | ------------------------------------------------------------ |
| inputImage | 입력 이미지의 권장되는 최대 크기는 2160×4096입니다. 이 크기보다 큰 사진은 얼굴 인식 결과가 좋지 않거나 얼굴을 인식할 수 없으며 OOM 문제가 발생할 수 있음 |
| needReset  | 다음 시나리오에서는 needReset을 true로 설정해야 합니다: <ul style="margin:0"><li>이미지 전환</li><li>처음으로 분할 사용</li><li>처음으로 애니메이션 사용</li>< li>처음으로 메이크업 사용</li></ul> |

### getConfigPropertyWithName

뷰티 필터 매개변수 설정 정보 가져오기

```objectivec
- (YTBeautyPropertyInfo * _Nullable)getConfigPropertyWithName:(NSString *_Nonnull)propertyName;
```

**매개변수**

| 매개변수         | 의미     |
| ------------ | -------- |
| propertyName | 이름 설정 |

### registerLoggerListener

로그 등록 인터페이스

```objectivec
- (void)registerLoggerListener:(id<YTSDKLogListener> _Nullable)listener withDefaultLevel:(YtSDKLoggerLevel)level;
```

**매개변수**

| 매개변수     | 의미                       |
| -------- | -------------------------- |
| listener | 로그 콜백 인터페이스               |
| level    | 로그 출력 level, 기본 ERROR |

### registerSDKEventListener

SDK 이벤트 리스너 인터페이스

```objectivec
- (void)registerSDKEventListener:(id<YTSDKEventListener> _Nullable)listener;
```

**매개변수**

| 매개변수     | 의미                                                        |
| -------- | ----------------------------------------------------------- |
| listener | 이벤트 리스너 콜백, 주로 AI 이벤트, Tips 프롬프트 이벤트, Asset 이벤트로 구분 |

### clearListeners

콜백 정리 인터페이스 등록

```objectivec
- (void)clearListeners;
```

### getCurrentGlContext

현재 GL 컨텍스트 인터페이스 가져오기

```objectivec
- (nullable EAGLContext*)getCurrentGlContext;
```

### onPause

SDK 일시 중지 인터페이스

```objectivec
/// @brief APP는 일시 중지 시 SDK 일시 중지 인터페이스 호출
- (void)onPause;
```

### onResume

SDK 복구 인터페이스

```objectivec
/// @brief APP는 복구 시 SDK 복구 인터페이스 호출
- (void)onResume;
```

## 정적 함수

| API                                       | 설명                     |
| ----------------------------------------- | ------------------------ |
| [isBeautyAuthorized](#isbeautyauthorized) | 뷰티 필터 매개변수의 인증 정보 가져오기 |

### isBeautyAuthorized

뷰티 필터 매개변수의 인증 정보 가져오기(뷰티 필터와 몸매 보정만 지원)

```objectivec
/// @param featureId 뷰티 필터 매개변수 설정
/// @return 해당 뷰티 필터 매개변수의 인증 결과 반환
+ (BOOL)isBeautyAuthorized:(NSString * _Nullable)featureId;
```

## 콜백

| API                                       | 설명                 |
| ----------------------------------------- | -------------------- |
| [YTSDKEventListener](#ytsdkeventlistener) | SDK 내부 이벤트 콜백 인터페이스 |
| [YTSDKLogListener](#ytsdkloglistener)     | 로그 리스너 콜백         |


### YTSDKEventListener

SDK 내부 이벤트 콜백 인터페이스
```objectivec
@protocol YTSDKEventListener <NSObject>
```

#### 멤버 함수
| 반환 유형 | 이름                            |
| -------- | ------------------------------- |
| void     | [onYTDataEvent](#onytdataevent) |
| void     | [onAIEvent](#onaievent)         |
| void     | [onTipsEvent](#ontipsevent)     |
| void     | [onAssetEvent](#onassetevent)   |

#### 함수 설명

##### onYTDataEvent
YTDataUpdate 이벤트 콜백

```objectivec
/// @param event NSString*형식의 콜백
- (void)onYTDataEvent:(id _Nonnull)event;
```

JSON string 구조를 반환하고 최대 5개의 안면 인식 정보 반환:

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

**필드 의미**

| 필드                         | 유형  | 값범위                                | 설명                                                   |
| ---------------------------- | ----- | ----------------------------------- | ------------------------------------------------------ |
| trace_id                     | int   | [1,INF)                      | 안면 인식 ID. 연속 스트리밍 과정에서 동일한 ID를 가진 사람들을 동일한 얼굴로 간주할 수 있음 |
| face_256_point               | float | [0,screenWidth] 또는 [0,screenHeight] | 총 512개의 숫자, 256개의 안면 인식 키 포인트가 있으며 화면의 왼쪽 상단 모서리는 (0,0)          |
| face_256_visible             | float | [0,1]                               | 안면 인식 256 키 포인트 가시도                                    |
| out_of_screen                | bool  | true/false                          | 얼굴이 프레임 밖에 있는지 여부                                           |
| left_eye_high_vis_ratio      | float | [0,1]                               | 왼쪽 눈 높이 가시성 포인트의 비율                                   |
| right_eye_high_vis_ratio     | float | [0,1]                               | 오른쪽 눈 높이 가시성 포인트의 비율                                   |
| left_eyebrow_high_vis_ratio  | float | [0,1]                        | 왼쪽 눈썹 높이 가시성 포인트의 비율                   |
| right_eyebrow_high_vis_ratio | float | [0,1]                        | 오른쪽 눈썹 높이 가시성 포인트의 비율                   |
| mouth_high_vis_ratio         | float | [0,1]                               | 입 높이 가시성 포인트의 비율                                     |

##### onAIEvent
AI 이벤트 콜백

```objectivec
/// @param event dict 형식의 콜백
- (void)onAIEvent:(id _Nonnull)event;
```

##### onTipsEvent
프롬프트 이벤트 콜백

```objectivec
/// @param event dict 형식의 콜백
- (void)onTipsEvent:(id _Nonnull)event;
```

##### onAssetEvent
리소스 패키지 이벤트 콜백

```objectivec
/// @param event string 형식의 콜백
- (void)onAssetEvent:(id _Nonnull)event;
```

### YTSDKLogListener

로그 리스너 콜백

```objectivec
@protocol YTSDKLogListener <NSObject>
```

#### 멤버 함수

| 반환 유형 | 함수 이름 |
| -------- | -------- |
| void     | onLog    |

#### 함수 설명

##### onLog

로그 리스너 콜백

```objectivec
/// @param loggerLevel 현재 로그 수준 반환
/// @param logInfo 현재 로그 정보 반환
- (void)onLog:(YtSDKLoggerLevel) loggerLevel withInfo:(NSString * _Nonnull) logInfo;
```

