
본문은 iOS 개발자가 GME(Game Multimedia Engine)용 API를 쉽게 디버깅하고 통합할 수 있도록 iOS 프로젝트 내보내기에 대한 참고 사항을 주로 설명합니다.


## 구성 내보내기

1. 필요에 따라 **Xcode** > **Link Binary With Libraries** > **Build Setting**에 다음 종속 라이브러리를 추가하고 아래와 같이 SDK가 상주하는 디렉터리를 가리키도록 프레임워크 검색 경로를 설정합니다.  
<img src="https://main.qcloudimg.com/raw/79355a317302adccd7f96e898bef7845.png"  style="
    width: 80%;
"> 
2. 아래와 같이 종속 라이브러리를 추가합니다.
![](https://main.qcloudimg.com/raw/b6156b8c7a596248c148607070e38f67.png)
3. Bitcode는 프로젝트가 의존하는 모든 클래스 라이브러리에서 지원되어야 합니다. Bitcode는 SDK에서 지원하지 않으므로 비활성화할 수 있습니다. Bitcode를 비활성화하려면 Targets - Build Settings에서 Bitcode를 검색하고 해당 옵션을 NO로 설정하기만 하면 됩니다.
<img src="https://main.qcloudimg.com/raw/7020b4fadc30d29d5760873a53e64124.png"  style="
    width: 80%;
"> 
4. iOS용 GME SDK에는 다음 권한이 필요합니다.
 - Required background modes: 백그라운드에서 실행을 허용합니다(옵션).
 - Microphone Usage Description: 마이크에 대한 액세스를 허용합니다.


## GME 2.9 이상

액세스한 SDK가 v2.9 이상인 경우 [iOS Project Upgrade Guide](https://intl.cloud.tencent.com/document/product/607/46015)의 안내에 따라 설정해야 합니다.
