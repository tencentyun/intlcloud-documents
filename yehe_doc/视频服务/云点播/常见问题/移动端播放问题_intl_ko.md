본문에서는 Android 및 iOS의 몇 가지 유형의 FAQ와 관련 솔루션을 소개합니다.

### ‘no v4 play info’ 오류가 발생하면 어떻게 해야 합니까?
- FileId를 통해 재생하려면 먼저 Adaptive-HLS(10) 트랜스코딩 템플릿을 사용하여 비디오를 트랜스코딩하거나 플레이어 서명 psign을 사용하여 재생할 비디오를 지정해야 합니다. 그렇지 않으면 비디오가 재생되지 않을 수 있습니다.
- 링크 도용 방지가 비활성화된 재생 중에 ‘no v4 play info’ 예외가 발생하면 Adaptive-HLS(10) 트랜스 코딩 템플릿을 사용하여 비디오를 트랜스 코딩하거나 URL을 통해 재생할 원본 비디오의 재생 링크를 직접 가져오는 것이 좋습니다.

### 오류를 보고하기 위해 플레이어 로그를 추출하려면 어떻게 해야 합니까?
Player SDK는 실행 log를 로컬 파일로 출력합니다. [문의하기](https://intl.cloud.tencent.com/document/product/266/19905) 진행 중 문제 분석을 위해 이 실행 log가 필요합니다.

### 재생을 위해 Tencent Cloud 미디어 자산을 풀링하려면 어떻게 해야 합니까?

보안을 위해, 현재 Tencent Cloud 미디어 자산을 직접 가져오는 App용 API는 제공되지 않습니다. **App**>**App 서비스 백엔드**>**Tencent Cloud** 경로에서 미디어 자산을 풀링해야 합니다. 백엔드 서비스는 [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179) API를 호출하여 미디어 자산 목록을 가져올 수 있습니다.

## Android SDK

### 재생 중에 화면이 표시되지 않으면 어떻게 해야 하나요?

SurfaceView 또는 TextureView가 TXVodPlayer 객체에 바인딩되어 있는지 확인하십시오.

### 패키지를 축소하려면 어떻게 해야 합니까?

- SDK v9.4 이하의 [다운로드 캐시 기능](https://www.tencentcloud.com/document/product/266/47849)(TXVodDownloadManager의 API)을 사용하지 않았고 SDK v9.5 이상에서 다운로드한 파일을 재생할 필요가 없다면 설치 패키지의 크기를 줄이는 데 도움이 되는 기능의 so 파일을 사용합니다. 예를 들어 SDK v9.4 또는 이전 버전에서 TXVodDownloadManager 클래스의 setDownloadPath 및 startDownloadUrl 함수를 사용하여 캐시된 파일을 다운로드했고 TXVodDownloadManager에서 다시 호출한 getPlayPath 경로가 후속 재생을 위해 앱에 저장되어 있는 경우 getPlayPath 경로에서 파일을 재생하기 위해 libijkhlscache-master.so가 필요합니다. 그렇지 않으면 필요하지 않습니다. app/build.gradle에 다음을 추가할 수 있습니다:
  ```xml
  packagingOptions {
      exclude "lib/armeabi/libijkhlscache-master.so"
      exclude "lib/armeabi-v7a/libijkhlscache-master.so"
      exclude "lib/arm64-v8a/libijkhlscache-master.so"
  }
  ```

- App이 중국 대륙에서만 사용되는 경우 `armeabi-v7a` 및 `arm64-v8a` 아키텍처의 so 파일을 패키징하거나 jar 파일만 패키징하고 설치 후 so 파일을 동적으로 다운로드할 수 있습니다. 자세한 튜토리얼은 [설치 패키지 용량 축소 관련 질문](https://intl.cloud.tencent.com/document/product/647/35165)을 참고하십시오.

### 콘솔 출력을 더 적은 log로 만들려면 어떻게 합니까?

불필요한 로그를 필터링하기 위해 다음과 같이 LogLevel을 설정할 수 있습니다: TXLiveBase.setLogLevel(TXLiveConstants.LOG_LEVEL_DEBUG).

## iOS SDK

### 재생 제어판이 표시되지 않으면 어떻게 해야 합니까?

재생 제어판의 표시는 MPNowPlayingInfoCenter에서 제어합니다. nowPlayingInfo 속성을 설정하여 제목과 이미지를 업데이트하고 볼륨 레벨을 설정할 수 있습니다. 자세한 내용은 [LiteAVSDK/Player_iOS](https://github.com/LiteAVSDK/Player_ios)를 참고하십시오.

### 콘솔 출력을 더 적은 log로 만들려면 어떻게 합니까?

[TXLiveBase setLogLevel:LOGLEVEL_DEBUG]와 같이 TXLiveBase.h의 setLogLevel API를 통해 LogLevel을 설정할 수 있습니다. 값이 클수록 출력 로그가 줄어듭니다. 값 범위는 0 (모든 레벨의 출력 로그)~ 6 (로그 출력 없음)까지입니다. 자세한 내용은 TXLiveBase.h를 참고하십시오.
