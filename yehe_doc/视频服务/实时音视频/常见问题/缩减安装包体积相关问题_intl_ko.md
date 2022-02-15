### TRTC SDK 통합 후 파일의 용량은 얼마나 증가합니까?
TRTC 버전별로 SDK 용량의 증가량이 달라집니다. 자세한 내용은 [SDK 다운로드](https://intl.cloud.tencent.com/document/product/647/34615)를 참조하십시오.

### iOS 플랫폼에서 설치 패키지의 용량을 줄일 수 있는 방법은 무엇입니까?
<dx-tabs>
::: 방법 1: arm64 아키텍처만 포함(추천)
 Apple iPhone 5s 이상 버전의 휴대폰에서는 x64 아키텍처만을 포함할 수 있습니다. XCode의 Build Setting에서 Build Active Architecture Only를 YES로 설정하고 Valid Architectures에 arm64를 입력하면 됩니다. TRTC SDK의 단일 아키텍처 ipa는 1.9M만 증가합니다.
![](https://main.qcloudimg.com/raw/4aea00771567fcff58697bf5433ba0dd.png)
:::
:::방법 2: BitCode 활성화
 Apple iPhone 5s 및 이전 버전의 휴대폰의 경우 **항목의 모든 3rd party 라이브러리가 BitCode**를 지원한다면 BitCode를 활성화하여 설치 패키지의 용량을 줄일 수 있습니다. Build Settings > Build Options에서 Enable Bitcode 옵션을 켜면 BitCode가 활성화됩니다.
 ![](https://main.qcloudimg.com/raw/516c0065d97eee4569a1d4061ba019cb.png)
2016년부터 Apple은 XCode 개발 환경에 BitCode 컴파일 옵션을 지원하기 시작했습니다. BitCode 활성화 후 컴파일러는 실제 어셈블리 기계어 코드가 아닌 앱에 중간 코드를 생성합니다. 사용자가 App Store에서 다운로드 및 설치하는 것은 휴대폰 CPU 아키텍처에서 생성된 기계어 코드로, 이 방법을 통해 설치 패키지 용량을 대폭 줄일 수 있습니다.
:::
</dx-tabs>
### Android 플랫폼에서 설치 패키지 용량을 줄일 수 있는 방법은 무엇입니까?
<dx-tabs>
::: 방법 1: 일부 so 파일만 포함
 앱을 중국대륙에서만 사용할 경우 `armeabi-v7a` 아키텍처의 so 파일만을 포함하면 설치 패키지 용량이 5M 이내로 증가합니다. 앱을 Google Play에 출시하고자 할 경우 `armeabi-v7a`과 `arm64-v8a` 두 가지 아키텍처의 so 파일을 포함할 수 있습니다.
**구체적인 조작 방법**: 현재 항목의 build.gradle에 `abiFilters "armeabi-v7a"`를 추가하여 단일 아키텍처의 so 파일을 지정하거나 `abiFilters "armeabi-v7a","arm64-v8a"`를 추가하여 이중 아키텍처의 so 파일을 지정합니다.
 - `armeabi-v7a` 아키텍처의 so 파일만을 포함(Google Play 출시 불필요)
  ![](https://main.qcloudimg.com/raw/72065de8f9cd1c95b23fb797d383b527.png)
 - `armeabi-v7a`와 `arm64-v8a` 두 가지 아키텍처의 so 파일 포함(Google Play 출시)
  ![](https://main.qcloudimg.com/raw/a6dcbef3c71fe9f2f7b5d52d6b0784ae.png)
::: 
::: 방법 2: jar 파일만을 포함(설치 후 so 파일 다운로드)
 >! 앱을 Google Play에 등록하고자 할 경우 이 방법을 사용하지 마십시오. 등록하지 못할 수 있습니다.
 
 Android 버전 SDK의 용량은 대부분 so 파일에 기인하므로 설치 패키지 용량 증가를 1M 이내로 압축하고자 할 경우 설치 후 so를 다운로드하는 방법을 사용하는 것도 고려할 수 있습니다.
 <span id="step1"></span>
 1. [Github](https://github.com/tencentyun/TRTCSDK/tree/master/Android) 폴더에서 `LiteAVSDK_TRTC_x.x.xxx.zip`이라고 명명된 압축 파일을 찾아 압축을 해제하여 아키텍처가 지정된 so 파일을 찾을 수 있습니다.
 2. [1단계](#step1)에서 다운로드한 so 파일을 서버(또는 Tencent Cloud[COS](https://intl.cloud.tencent.com/product/cos) 객체 스토리지 서비스)에 업로드하여 `http://xxx.com/so_files.zip`처럼 다운로드 주소를 기록합니다.
 3. 사용자는 SDK 관련 기능을 실행하기 전, 예를 들면 비디오 재생 전에 우선 로딩 애니메이션으로 사용자에게 “관련 기능 모듈 로딩 중”이라고 알립니다.
  사용자 대기 시 앱은 `http://xxx.com/so_files.zip`에서 so 파일을 다운로드해 애플리케이션 디렉터리에 저장(예: 애플리케이션 루트 디렉터리의 files 폴더)할 수 있습니다. 이 과정에서 통신사 DNS 하이재킹의 영향을 받을 수 있으니 파일 다운로드 완료 후 so 파일의 완전성을 확인하여 zip 압축 파일을 통신사에서 왜곡하지 않도록 합니다.
 4. 모든 so 파일이 제자리를 잡으면 `TXLiveBase`류(LiteAVSDK 최초 기본 모듈)의 `setLibraryPath()` 인터페이스를 호출하여 so 다운로드 대상 경로를 SDK에 설정합니다. SDK는 해당 경로에서 필요한 so 파일을 로딩하여 관련 기능을 실행합니다.
:::
</dx-tabs>

