Tencent Cloud Game Multimedia Engine(GME) 엔진 SDK를 사용해주셔서 감사합니다. Cocos2D 개발자가 Tencent Cloud GME 제품 API를 디버깅하고 액세스하는데 도움을 드리고자, Cocos2D 개발에 적용하는 프로그래밍 설정을 소개드립니다.

## SDK 준비

[다운로드 안내](https://intl.cloud.tencent.com/document/product/607/18521)에서 관련 Demo와 SDK를 다운로드합니다.

### SDK 리소스 압축 해제

1. 획득한 SDK 리소스를 압축 해제합니다.
2. 폴더 내용은 다음과 같습니다:

|폴더 명칭                    | 폴더 상세내역|
| ----------------------|-----------------------------------        |
| TMG_SDK                    |게임 오디오/비디오 SDK framework 파일        |
| TMGCocosDemo          |게임 오디오/비디오 SDK 예시 프로그래밍                        |

## 시스템 요청

SDK는 Mac 시스템 컴파일링을 지원합니다.

## iOS Xcode 준비 작업

### 1. SDK 관련 framework 파일을 추가합니다.

framework을 Xcode 프로그래밍에 추가하고 헤더 파일 인용 위치를 설정합니다.

TMG_SDK 폴더에 GMESDK.framework 게임 오디오/비디오 SDK framework 파일이 존재하며, 반드시 프로그래밍에 추가해야 합니다.

### 2. 의존형 라이브러리
참고 이미지:  
![](https://main.qcloudimg.com/raw/b6156b8c7a596248c148607070e38f67.png)

## Android 준비 작업

### 1. gmesdk, jar를 libs 라이브러리에 추가합니다.
![](https://main.qcloudimg.com/raw/167b3fb575b65539aeaf9c700383e7c8.png)

### 2. Activity에 so 파일 추가

```
public class AppActivity extends Cocos2dxActivity {
    static final String TAG = "AppActivity";
    static OpensdkGameWrapper gameWrapper ;
    static {
        OpensdkGameWrapper.loadSdkLibrary();
    }
}
```

### 3. 초기화

oncreate 함수에서 초기화하며, 순서는 틀리지 말아야 합니다.
```
protected void onCreate(Bundle savedInstanceState) {
        super.setEnableVirtualButton(false);
        super.onCreate(savedInstanceState);

        //초기화, 순서는 틀리지 말아야 합니다
        gameWrapper = new OpensdkGameWrapper(this);
        runOnGLThread(new Runnable() {
            @Override
            public void run() {
                gameWrapper.initOpensdk();
            }
        });
}
```

## 다양한 플랫폼 출력

Cocos2D 엔진으로부터 다양한 플랫폼을 출력하려면, 대응하는 프로그래밍을 설정해야 합니다:

|플랫폼       | 프로그래밍 설정           |
| ------------- |:-------------:|
| Android |[Android 프로그래밍 설정 파일](https://intl.cloud.tencent.com/document/product/607/10783)|
| iOS     |[iOS 프로그래밍 설정 파일](https://intl.cloud.tencent.com/document/product/607/10783)|
| Mac     |[Mac 프로그래밍 설정 파일](https://intl.cloud.tencent.com/document/product/607/10783)|