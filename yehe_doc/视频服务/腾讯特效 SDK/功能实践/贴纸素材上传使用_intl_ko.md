본 문서는 구매하거나 자체 제작한 소재를 Demo 프로젝트에 넣고 사용하는 방법을 설명합니다.

## iOS
iOS Demo 리소스 패키지 초기화 관련 코드는 'BeautyViewModel.m'에 있으며 스티커 소재 목록을 초기화하는 메소드는 **setupData**입니다.

1. **_motion2DMenuIDS** 목록에 스티커 소재 이름(디렉터리 이름)을 넣습니다.
2. 소재 패키지를 Demo의 **resources/2dMotionRes.bundle**에 복사하고 Demo를 다시 컴파일하고 실행합니다.

> ?스티커가 있는 bundle은 스티커가 있는 곳과 관련이 있을 뿐 스티커의 종류와는 상관이 없습니다.

## Android

Android Demo용 리소스 패키지 초기화 관련 코드는 **XmagicResParser.java**에 있으며, 스티커 소재 목록을 초기화하는 메소드는 **parseMotion**입니다.

1. 임의의 위치에서 **motionResStr** 문자열에 스티커 소재 이름(디렉터리 이름)을 추가합니다(쉼표에 주의).
2. 소재 패키지를 Demo의 **src/main/assets/MotionRes/2dMotionRes** 디렉터리에 복사하고 Demo를 다시 컴파일하고 실행합니다.

#### 예시:
스티커 소재 폴더의 이름이 **video_mymotion**인 경우 다음을 변경해야 합니다.
```java
final String MotionResStr = "video_lianliancaomei:사랑스러운 딸기," +
......
```
로 변경
```java
final String MotionResStr = "video_mymotion:내 스티커," +
                            "video_lianliancaomei:사랑스러운 딸기," +
......
```
> !소재 패키지는 다른 **xxxMotionRes** 디렉터리에 복사할 수 있습니다. 이것은 Demo에서 스티커가 표시되는 위치에만 영향을 주지만 스티커 유형과는 아무 관련이 없습니다.

