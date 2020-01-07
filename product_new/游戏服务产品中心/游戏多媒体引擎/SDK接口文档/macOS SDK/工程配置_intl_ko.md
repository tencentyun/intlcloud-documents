## 개요

Tencent Cloud Game Multimedia Engine(GME) SDK를 이용해주셔서 감사합니다. Mac 개발자 테스트 편의성과 Tencent Cloud GME 프로덕트 API 원활한 액세스를 위해 Mac 맞춤용 개발 프로그래밍 설정을 소개드립니다.

## SDK 준비

다음 방법을 통해 SDK를 획득할 수 있습니다.

### 1. [다운로드 매뉴얼](https://intl.cloud.tencent.com/document/product/607/18521)에서 관련 Demo와 SDK를 다운로드합니다.

### 2. 인터페이스에서 Mac 버전용 SDK 리소스를 확인합니다.

3. [다운로드] 버튼을 클릭합니다.

다운로드한 SDK 리소스를 압축 해제하면 다음 파트를 포함합니다:

|명칭     | 의미   |
| ------------- |:-------------:|
|GMESDK.framework| GME 관련 리소스|

## 사전 준비

### 1. 파일을 추가합니다

상황별로 Xcode의 Link Binary With Libraries에 하기 의존 라이브러리를 추가하며, Framework Search Paths를 SDK 목록에 설정합니다. 이미지 예시:  

### 2. 종속 라이브러리 추가

참조 이미지:  

![](https://main.qcloudimg.com/raw/b6156b8c7a596248c148607070e38f67.png)


