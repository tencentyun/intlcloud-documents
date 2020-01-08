## 개요

Tencent Cloud Game Multimedia Engine(GME) 엔진 SDK를 사용해주셔서 감사합니다.iOS 개발자가 Tencent Cloud GME 제품 API를 디버깅하고 액세스하는데 도움을 드리고자, iOS 개발에 적용하는 프로그래밍 설정을 소개드립니다.

## SDK  준비

다음 방법으로 SDK를 획득할 수 있습니다. 

### 1. [다운로드 안내](https://intl.cloud.tencent.com/document/product/607/18521)에서 관련 Demo와 SDK를 다운로드합니다.

### 2. 인터페이스에서 iOS버전의 SDK 리소스를 확인합니다. 

### 3. [다운로드]를 클릭합니다.

SDK 리소스를 다운로드하고나서 압축 해제 시 다음 파트가 포함됩니다:

|명칭     | 의미   |
| ------------- |:-------------:|
|GMESDK.framework|오리지널 iOS 개발 관련 리소스|
|libGMESDK.a|Unity iOS 개발 관련 리소스|

## 시스템 요청

SDK는 iOS7.0 및 이상 시스템에서 작동합니다.

## 준비 작업

### 1. SDK 파일 추가

상황별로 Xcode의 Link Binary With Libraries에 다음 의존형 라이브러리를 추가해야 하며, Framework Search Paths는 SDK가 위치한 목록을 지향해야 합니다. 참고 이미지:  

![](https://main.qcloudimg.com/raw/9dd8d458734bc6e475581049e6cf26b1.png)

### 2. 의존형 라이브러리 추가

참고 이미지:  

![](https://main.qcloudimg.com/raw/b6156b8c7a596248c148607070e38f67.png)

### 3. bitcode 종료

Bitcode는 프로그래밍에 의존하는 전체 타입의 라이브러리가 동시에 적용되어야 합니다. SDK는 일시적으로 Bitcode를 지원하지 않으므로 임시로 종료할 수 있습니다. 
이 설정을 종료하고 Targets - Build Settings에서 Bitcode를 검색합니다. 대응하는 옵션을 찾으면 NO로 설정합니다. 
참고 이미지:  
![](https://main.qcloudimg.com/raw/82c628e8a7d9a4bebc842c8545d9563a.png)

### 4. 권한 신청

텐센트 오디오/비디오 엔진 iOS 플랫폼에 필요한 프라이빗 권한은 다음과 같습니다:

|key     | 의미   |
| ------------- |:-------------:|
|Required background modes     |백그라운드 작동 허락(옵션)|
|Microphone Usage Description   |마이크 권한 허락|

### 5. 오프라인 음성 메시지에 HTTP 액세스 권한을 추가합니다.
Allow Arbitrary Loads 권한을 추가해야 합니다.

![](https://main.qcloudimg.com/raw/1aebf9111fd95e3e6b6fb4eb08193a26.png)
