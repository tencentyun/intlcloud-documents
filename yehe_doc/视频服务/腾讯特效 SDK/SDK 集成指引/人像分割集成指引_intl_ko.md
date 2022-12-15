이 기능을 사용하면 라이브 스트리밍 및 화상 회의와 같은 시나리오에서 비디오에 가상 배경을 적용할 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/4ed25f2dba2445c929e757879ae83547.png" width=900>

## iOS API

### iOS 통합

Tencent Effect iOS SDK 통합 방법은 [Tencent Effect SDK 통합하기](https://intl.cloud.tencent.com/document/product/1143/45384)를 참고하십시오.

### 가상 배경 구성
```objectivec
NSString *motionSegResPath = [[NSBundle mainBundle] pathForResource:@"segmentMotionRes" ofType:@"bundle"];//segmentMotionRes 폴더의 절대 경로
NSString *propertyType = @"motion";         //뷰티 필터 효과 유형 설정, 분할 예시
NSString *propertyName = @"video_segmentation_blur_75"; //뷰티 필터 이름 설정, 배경 블러 처리-강함 예시
NSString *propertyValue = motionSegResPath;  //애니메이션 효과 경로 설정
NSDictionary *dic = @{@"bgName":@"BgSegmentation.bg.png", @"bgType":@0, @"timeOffset": @0},@"icon":@"segmentation.linjian.png"};//예약 필드 설정
[self.beautyKit configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:dic];
```

### 배경 사용자 지정
```objectivec
NSString *motionSegResPath = [[NSBundle mainBundle] pathForResource:@"segmentMotionRes" ofType:@"bundle"];//segmentMotionRes 폴더의 절대 경로
NSString *propertyType = @"motion";         //뷰티 필터 효과 유형 설정, 분할 예시
NSString *propertyName = @"video_empty_segmentation"; //뷰티 필터 이름 설정, 사용자 정의 배경 예시
NSString *propertyValue = motionSegResPath;  //애니메이션 효과 경로 설정
NSString *imagePath = @"/var/mobile/Containers/Data/Application/06B00BBC-9060-450F-8D3A-F6028D185682/Documents/MediaFile/image.png"; //사용자 정의 배경 이미지의 절대 경로입니다. 사용자 정의 배경으로 비디오를 선택한 경우 비디오를 압축 및 트랜스 코딩해야 하며 압축 및 트랜스 코딩 후의 절대 경로 사용
int bgType = 0;//사용자 정의 배경 유형입니다. 0이미지, 1비디오
int timeOffset = 0；//지속 시간. 이미지 배경일 때 0; 비디오 배경 시 비디오 지속 시간
NSDictionary *dic = @{@"bgName":imagePath, @"bgType":@(bgType), @"timeOffset": @(timeOffset)},@"icon":@"segmentation.linjian.png"};//예약 필드 설정
[self.beautyKit configPropertyWithType:propertyType withName:propertyName withData:propertyValue withExtraInfo:dic];
```



## Android API

### Android 통합
Tencent Effect Android SDK 통합 방법은 [Tencent Effect SDK 통합하기](https://intl.cloud.tencent.com/document/product/1143/45385)를 참고하십시오.

### 속성 설정
```java
void updateProperty(XmagicProperty<?> p) 
```

**키잉 매개변수:**

| 매개변수 | 설명                                                         |
| :------- | :----------------------------------------------------------- |
| category | Category.SEGMENTATION                                        |
| ID       | **리소스 폴더의 이름**, 예시: `video_segmentation_blur_45`, <li>ID가 ‘없음’일 경우 `XmagicProperty.ID_NONE`을 사용하고 </li><li>사용자 지정 배경의 경우, `XmagicConstant.SegmentationId.CUSTOM_SEG_ID`로 설정</li> |
| resPath  | 필수, Demo 참고                                              |
| effkey   | null(사용자 지정 배경 제외), 사용자 지정 배경의 경우 이 매개변수를 리소스 경로로 설정       |
| effValue | null                                                         |


### 가상 배경 구성
```java
//XmagicProperty 초기화
XmagicProperty xmagicProperty = new XmagicProperty(Category.SEGMENTATION,"video_segmentation_blur_45",resPath,null,null);
//속성 설정
xmagicApi.updateProperty(xmagicProperty) 
```

### 배경 사용자 지정
```java
XmagicProperty xmagicProperty = new XmagicProperty(Category.SEGMENTATION,XmagicConstant.SegmentationId.CUSTOM_SEG_ID,resPath,null,null);

xmagicApi.updateProperty(xmagicProperty) 
```

