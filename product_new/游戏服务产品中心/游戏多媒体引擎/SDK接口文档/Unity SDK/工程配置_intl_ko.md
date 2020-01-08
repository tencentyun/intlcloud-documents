Tencent Cloud Game Multimedia Engine(GME) SDK를 사용해주셔서 감사합니다. Unity 개발자가 Tencent Cloud GME 제품 API를 디버깅하고 액세스하는데 도움을 드리고자 Unity 개발에 적용하는 프로그래밍 설정을 소개드립니다.

## SDK 준비

다음 프로세스를 통해 SDK를 획득합니다.

### SDK 다운로드

[다운로드 안내](https://intl.cloud.tencent.com/document/product/607/18521)에서 관련 Demo와 SDK를 다운로드합니다.

인터페이스에서 Unity 버전의 SDK 리소스를 확인합니다.

[다운로드] 버튼을 클릭합니다. 다운로드 완료 시 SDK 리소스를 압축 해제하면 다음 파트가 포함됩니다:

![](https://main.qcloudimg.com/raw/55494d9bb9145938f0594416f73b29f7.png)

파일 설명:

|파일 명칭       | 설명     |
| ------------- |:-------------:|
| Plugins   |SDK 라이브러리 파일|
| Scripts     |SDK 코드 파일|

## 준비 작업

### 1. Plugins 파일을 추가합니다.
개발툴 패킷의 Plugins 폴더 파일을 Unity 프로그래밍 Assets의 Plugins 폴더에 복사합니다. 예시 이미지:  
![](https://main.qcloudimg.com/raw/1221a25f62cedd3831cf2bb27bb1ea45.png)

### 2. 코드 파일 추가
개발툴 패킷의 Scripts 폴더 파일을 Unity 프로그래밍에서 코드를 저장하는 폴더에 복사합니다. 예시 이미지:  
![](https://main.qcloudimg.com/raw/8904a83c6173fa7c5b04ddb0e48138ca.png)

### 3. 가청 주파수 설정
Unity 에디터에서 Edit-Project Setting-Audio는 시스템 디폴트로 적용합니다. 혹 수정할 경우, Unity 재생 효과는 iOS에서 하드웨어 캐시존을 설정하는 영향을 받아, 효과음이 중단됩니다. 
![](https://main.qcloudimg.com/raw/df14517cac7fc29383c90720627572c7.png)

혹 다음 이미지와 같은 모드로 설정하면, Unity 재생 효과는 OS에서 하드웨어 캐시존을 설정하는 영향을 받아, 효과음이 중단됩니다. 
![](https://main.qcloudimg.com/raw/69857f53bdc2ee7c7ad5e48777620df1.png)


## 다양한 플랫폼 출력

Unity 엔진으로부터 다양한 플랫폼을 출력하려면, 대응하는 프로그래밍을 설정해야 합니다:

|플랫폼       | 프로그래밍 설정           |
| ------------- |:-------------:|
| Android |[Android 프로그래밍 설정 파일](https://intl.cloud.tencent.com/document/product/607/10783)|
| iOS     |[iOS 프로그래밍 설정 파일](https://intl.cloud.tencent.com/document/product/607/10783)|
| Mac     |[Mac 프로그래밍 설정 파일](https://intl.cloud.tencent.com/document/product/607/10783)|