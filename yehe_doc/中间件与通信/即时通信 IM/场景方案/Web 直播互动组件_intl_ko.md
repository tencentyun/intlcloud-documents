- 본문은 UI가 있는 Web 라이브 인터랙티브 컴포넌트인 TUIPusher & TUIPlayer를 소개합니다. TUIPusher & TUIPlayer는 [IM](https://intl.cloud.tencent.com/product/im),  [TRTC](https://intl.cloud.tencent.com/product/trtc)등 기본 SDK를 통합하여, 엔터프라이즈 라이브 방송, 라이브 커머스, 업무 교육 및 원격 교육 등 다양한 라이브  시나리오를 위한 Web 라이브 푸시/풀 스트림 툴을 빠르게 런칭하기 위한 솔루션을 제공합니다.

  TUIPusher & TUIPlayer 의 장점:
  + 라이브 방송 시나리오의 요구 사항에 따라 라이브 방송 시나리오의 일반적인 기능(예: 장치 선택, 뷰티 필터, 라이브 방송 푸시 스트림, 시청자 풀 스트림, 채팅 등)을 포괄하는 UI가 있는 라이브 방송 시나리오에 대한 범용 솔루션을 제공하여 빠른 런칭을 지원합니다.
  + Tencent Cloud TRTC, Tencent Cloud IM, Tencent Cloud Superplayer TCPlayer 등 기본 SDK를 연결하여 비즈니스 기능을 유연하게 확장할 수 있습니다.
  + Web의 장점은 사용과 기능 반복의 편리성입니다.

  ## 빠른 체험

  TUIPusher와 TUIPlayer의 기능 데모는 아래 이미지를 참고하십시오. 동시에 TUIPusher & TUIPlayer의 기능을 빠르게 체험하실 수 있도록 사용자 SSM과 방 SSM을 결합하여 [TUIPusher 체험 링크](https://web.sdk.qcloud.com/component/tuiliveroom/tuipusher/login.html)와 [TUIPlayer 체험 링크](https://web.sdk.qcloud.com/component/tuiliveroom/tuiplayer/login.html)를 제공합니다.
  >! TUIPusher와 TUIPlayer를 동시에 체험하려면 두 개의 다른 계정으로 로그인해야 합니다.  

  ![TUIPusher 데모](https://qcloudimg.tencent-cloud.cn/raw/8d33df705c07c80d75ad19096e681903.png)
  ![TUIPlayer 데모](https://qcloudimg.tencent-cloud.cn/raw/6490fdf7db4980db3a98b4b103fb52f1.png)

  ## 코드 다운로드

  Web 라이브 방송 인터랙티브 컴포넌트(TUIPusher & TUIPlayer) 다운로드 방법:
  + [TUIPusher](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPusher) 
  + [TUIPlayer](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPlayer)
  
  
  ## 기능 소개
  ### TUIPusher 푸시 스트림 컴포넌트
  - 카메라 및 마이크에서 스트림 수집 및 푸시 스트림 지원
    - 필요에 따라 비디오 매개변수(프레임 레이트, 해상도, 비트 레이트) 설정 가능
    - 뷰티필터 활성화 및 비디오 뷰티필터 매개변수 설정 지원
  - 캡처 화면 스트림 공유 및 푸시 스트림 지원
  - Tencent Cloud TRTC 백그라운드 및 Tencent Cloud CDN 스트리밍 지원
  - 온라인 채팅방, 온라인 시청자와 채팅 및 인터랙션 지원
  - 시청자 리스트 가져오기 및 온라인 시청자 음소거 작업 지원
  
  ### TUIPlayer 풀 스트림 컴포넌트
  - 오디오 및 비디오 스트림과 화면 공유 스트림 동시 재생 지원
  - 온라인 채팅방 지원, 호스트 및 다른 시청자와 채팅 인터랙션
  - 초저지연 라이브 방송(딜레이 300ms), LEB(딜레이 1000ms 이내) 및 LVB(초고속 동시 시청 지원)의 3가지 풀 스트림 라인 지원
  - 데스크톱 브라우저 및 모바일 브라우저와 호환, 모바일 브라우저 가로 보기 지원
  > !
  > 일부 브라우저는 WebRTC를 지원하지 않아 LVB 채널로만 시청할 수 있으니 다른 경로를 경험하려면 브라우저를 바꿔보십시오.
  
  ## 액세스 방식
  ### 주의 사항
  - TUIPusher & TUIPlayer는 Tencent Cloud TRTC 및 IM 서비스를 기반으로 개발되었습니다. TRTC 애플리케이션과 IM 애플리케이션의 SDKAppID가 동일한 경우에만 계정 및 인증을 재사용할 수 있습니다.
  - UserSig 로컬 계산 방식은 로컬 개발 디버깅에만 사용하고 온라인에 배포하지 마십시오. SECRETKEY가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.
  
  ### 1단계: Tencent Cloud 서비스 활성화
  <dx-tabs>
  ::: 방식1: \sIM 기반
  #### 1단계: IM 애플리케이션 생성
  1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인하고 **애플리케이션 생성**을 클릭하면 팝업 창이 나타납니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/7382cbcd81df7afbad1e9af641697c87.png)
  2. 애플리케이션 이름을 입력한 후 **확인**을 클릭하면 애플리케이션이 생성됩니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/b3a630da00564cf7ef4a91b8492b646e.png)
  3. [IM 콘솔](https://console.cloud.tencent.com/im)의 전체보기 페이지에서 새로 생성된 애플리케이션의 상태, 서비스 버전, SDKAppID, 생성 시간 및 만료 시간을 확인할 수 있습니다. SDKAppID 정보를 기록해 두십시오.
  
  #### 2단계: IM 키 획득 및 TRTC 서비스 활성화
  1. [IM 콘솔](https://console.cloud.tencent.com/im)의 전체보기 페이지에서 새로 생성한 IM 애플리케이션을 클릭하여 해당 애플리케이션의 기본 설정 페이지로 이동합니다. **기본 정보**에서 **키 표시**를 클릭하여 키 정보를 복사 및 저장합니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/6f284cf687e9648d209567ed32983c84.png)
  >!키 정보가 유출되지 않도록 잘 보관하십시오.
  2. 해당 애플리케이션의 기본 설정 페이지에서 TRTC 서비스를 활성화합니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/8a9d1ca2c395fc6ebd26298a0f5226c4.png)
  :::
  ::: 방식2: TRTC 기반
  [](id:step1)
  #### 1단계: Tencent Real-Time Communication(TRTC) 애플리케이션 생성
  1. [Tencent Cloud 계정 생성](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fdocument%2Fproduct%2F647%2F49327) 및 [TRTC](https://console.cloud.tencent.com/trtc), [IM](https://console.cloud.tencent.com/im) 서비스 활성화를 완료해야 합니다.
  2. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에서 **애플리케이션 관리 > 애플리케이션 생성**을 클릭하여 새로운 애플리케이션을 생성합니다.
  ![애플리케이션 생성](https://qcloudimg.tencent-cloud.cn/raw/9a50fca02d951862a3d0d38251835f76.png)
  
  #### 2단계: TRTC 키 정보 가져오기
  1. **애플리케이션 관리 > 애플리케이션 정보**에서 SDKAppID 정보를 가져옵니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/6c39a936934a944cd1b13e2ced0869d2.png)
  2. **애플리케이션 관리 > 퀵 스타트**에서 애플리케이션의 secretKey 정보를 가져옵니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/08e836506f07f33b7b527f1eb0413b10.png)
  
  <dx-alert infotype="explain">
  - TRTC 애플리케이션을 처음 생성하는 Tencent Cloud 계정은 오디오/비디오 리소스 10,000분 무료 베타 패키지가 제공됩니다.
  - TRTC 애플리케이션 생성 후 동일한 SDKAppID를 가진 IM 애플리케이션이 자동으로 생성되며, 이 애플리케이션의 패키지 정보는 [IM 콘솔](https://console.cloud.tencent.com/im)에서 구성할 수 있습니다.</dx-alert>
  :::
  </dx-tabs>
  
  [](id:step2)
  ### 2단계: 프로젝트 준비
  
  1. [GitHub](https://github.com/tencentyun/TUILiveRoom/tree/main/Web)에서 TUIPusher & TUIPlayer 코드를 다운로드합니다.
  2. TUIPusher & TUIPlayer 종속 항목을 설치합니다.
  ```bash
  cd Web/TUIPusher
  npm install
  
  cd Web/TUIPlayer
  npm install
  ```
  3. `TUIPusher/src/config/basic-info-config.js` 및 `TUIPlayer/src/config/basic-info-config.js` 구성 파일에 sdkAppId 및 secretKey를 입력합니다.
  ![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
  4. 로컬 개발 환경에서 TUIPusher & TUIPlayer를 실행합니다.
  ```bash
  cd Web/TUIPusher
  npm run serve
  
  cd Web/TUIPlayer
  npm run serve
  ```
  5. `http://localhost:8080` 및 `http://localhost:8081`을 열어 TUIPusher 및 TUIPlayer의 기능을 체험할 수 있습니다.
  6. `TUIPusher/src/config/basic-info-config.js` 및 `TUIPlayer/src/config/basic-info-config.js` 구성 파일에서 방, 호스트 및 시청자 정보를 변경할 수 있습니다. **TUIPusher 및 TUIPlayer의 방 정보와 호스트 정보는 일치해야 합니다**.
  
  >!
  >- 상기 설정을 완료한 후, TUIPusher & TUIPlayer를 사용하여 초저지연 라이브 방송을 진행할 수 있으며, LEB와 LVB 지원이 필요한 경우, [3단계: 릴레이 라이브 방송](#step3)을 계속 읽어주십시오.
  >- UserSig 로컬 계산 방식은 로컬 개발 디버깅에만 사용하고 온라인에 배포하지 마십시오. `SECRETKEY`가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다.
  >- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.
  
  [](id:step3)
  ### 3단계: 릴레이 라이브 방송
  
  TUIPusher & TUIPlayer로 구현된 LEB 및 LVB는 Tencent Cloud [CSS 서비스](https://intl.cloud.tencent.com/document/product/267)에 의존하므로, LEB 및 LVB 회선을 지원하려면 릴레이 푸시 스트림 기능을 활성화해야 합니다.
  
  1. [**TRTC 콘솔**](https://console.cloud.tencent.com/trtc)에서 사용 중인 애플리케이션에 대한 릴레이 푸시 스트림 설정을 활성화하고 필요에 따라 특정 스트림 릴레이 또는 전역 자동 릴레이를 활성화할 수 있습니다. 
  ![](https://qcloudimg.tencent-cloud.cn/raw/b65584a5b096481ade6e302dabedcd5f.png)
  2. [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage) 페이지에 재생 도메인을 추가하십시오. 자세한 내용은 [자체 도메인 추가](https://intl.cloud.tencent.com/document/product/267/35970)를 참고하십시오.
  3. `TUIPlayer/src/config/basic-info-config.js` 구성 파일에서 재생 도메인을 구성합니다.
  
  상기 구성을 완료하면 초저지연 라이브 방송, LEB, LVB를 지원하는 TUIPusher & TUIPlayer의 모든 기능을 경험할 수 있습니다.
  
  [](id:step4)
  ### 4단계: 프로덕션 환경 애플리케이션
  
  프로덕션 애플리케이션에 TUIPusher & TUIPlayer 사용 시, TUIPusher & TUIPlayer 연결 외에도 다음을 수행해야 합니다.
  
  - 사용자 ID, 사용자 이름, 사용자 프로필 사진 등을 포함하되 이에 국한되지 않는 제품 사용자 정보 관리를 위한 사용자 SSM을 생성합니다.
  - 라이브 룸 ID, 라이브 룸 이름, 라이브 룸 호스트 정보를 포함하되 이에 국한되지 않는 제품 라이브 룸 정보를 관리하는 SSM을 생성합니다.
  - 서버의 UserSig를 생성합니다.
  > !
  > - 본문의 UserSig 생성 방법은 귀하가 입력한 sdkAppId 및 secretKey에 따라 클라이언트 측에서 userSig를 생성하는 것입니다. 이 secretKey 방식은 역컴파일로 역크래킹 되기 쉽기 때문에 키가 유출되면 공격자가 Tencent Cloud 트래픽을 도용할 수 있습니다. **이 방법은 TUIPusher & TUIPlayer 로컬 실행을 통한 기능 디버깅에만 적합합니다**.
  > - 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, 애플리케이션은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.
  - `TUIPusher/src/pusher.vue` 및 `TUIPlayer/src/player.vue` 파일을 참고하여 전역 스토리지를 위한 vuex store에 사용자 정보, 라이브 룸 정보, SDKAppId 및 UserSig 계정 정보를 제출 및 실행할 수 있으며, 두 클라이언트의 푸시/풀 스트림의 모든 기능을 실행할 수 있습니다. 자세한 비즈니스 프로세스는 아래 이미지와 같습니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/30e959d1b4605532f6d4cac190cdd1df.png)
  
  ## 관련 문제
  ### Web에서 뷰티 필터 기능을 구현하는 방법은 무엇입니까?
  [뷰티 필터 활성화](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-28-advanced-beauty.html)를 참고하십시오.
  
  ### Web에서 화면 공유를 구현하는 방법은 무엇입니까?
  자세한 내용은 [화면 공유](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-16-basic-screencast.html)를 참고하십시오.
  
  ### Web에서 클라우드 녹화를 구현하는 방법은 무엇입니까?
  1. **클라우드 녹화**기능 활성화의 구체적인 작업은 [클라우드 녹화 및 재생 구현](https://intl.cloud.tencent.com/document/product/647/35426)을 참고하십시오.
  2. **클라우드 녹화**> **특정 사용자 녹화** 활성화 후 Web에서 [TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createClient) 인터페이스를 호출할 때 userDefineRecordId 매개변수를 전달하여 녹화를 활성화할 수 있습니다.
  
  ### Web에서 CDN으로 푸시하는 방법은 무엇입니까?
  Web에서 CDN으로 푸시 스트림하려면 [CDN으로 푸시 스트림하기](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-26-advanced-publish-cdn-stream.html)를 참고하십시오.
  
  ### Web에서 LEB 풀 스트림을 구현하는 방법은 무엇입니까?
  LEB 풀 스트림을 구현하는 방법은 Web SDK를 통해 스트림을 CDN으로 푸시한 후 WebRTC 프로토콜을 사용하여 프로토콜을 가져오는 것입니다.
  
  ## 주의 사항
  ###  지원 플랫폼
  
  | 운영 체제 | 브라우저 유형                        | 브라우저 최저 버전 요구 사항 | TUIPlayer             | TUIPusher | TUIPusher 화면 공유        |
  | :-------- | :----------------------------------- | :--------------------------- | :-------------------- | :-------- | :------------------------- |
  | Mac OS    | 데스크톱 버전 Safari 브라우저        | 11+                          | 지원                  | 지원      | 지원(Safari13+ 버전 필요)  |
  | Mac OS    | 데스크톱 버전 Chrome 브라우저        | 56+                          | 지원                  | 지원      | 지원(Chrome72+ 버전 필요)  |
  | Mac OS    | 데스크톱 버전 Firefox 브라우저       | 56+                          | 지원                  | 지원      | 지원(Firefox66+ 버전 필요) |
  | Mac OS    | 데스크톱 버전 Edge 브라우저          | 80+                          | 지원                  | 지원      | 지원                       |
  | Mac OS    | 데스크톱 버전 WeChat 내장 웹 페이지  | -                            | 지원                  | 미지원    | 미지원                     |
  | Mac OS    | 데스크톱 버전 WeCom 내장 웹 페이지   | -                            | 지원                  | 미지원    | 미지원                     |
  | Windows   | 데스크톱 버전 Chrome 브라우저        | 56+                          | 지원                  | 지원      | 지원(Chrome72+ 버전 필요)  |
  | Windows   | 데스크톱 버전 QQ 브라우저(고속 커널) | 10.4+                        | 지원                  | 지원      | 미지원                     |
  | Windows   | 데스크톱 버전 Firefox 브라우저       | 56+                          | 지원                  | 지원      | 지원(Firefox66+ 버전 필요) |
  | Windows   | 데스크톱 버전 Edge 브라우저          | 80+                          | 지원                  | 지원      | 지원                       |
  | Windows   | 데스크톱 버전 WeChat 내장 웹 페이지  | -                            | 지원                  | 미지원    | 미지원                     |
  | Windows   | 데스크톱 버전 WeCom 내장 웹 페이지   | -                            | 지원                  | 미지원    | 미지원                     |
  | iOS       | WeChat 내장 브라우저                 | -                            | 지원                  | 미지원    | 미지원                     |
  | iOS       | WeCom 내장 브라우저                  | -                            | 지원                  | 미지원    | 미지원                     |
  | iOS       | 모바일 버전 Safari 브라우저          | -                            | 지원                  | 미지원    | 미지원                     |
  | iOS       | 모바일 버전 Chrome 브라우저          | -                            | 지원                  | 미지원    | 미지원                     |
  | Android   | WeChat 내장 브라우저                 | -                            | 지원                  | 미지원    | 미지원                     |
  | Android   | WeCom 브라우저                       | -                            | 지원                  | 미지원    | 미지원                     |
  | Android   | 모바일 버전 Chrome 브라우저          | -                            | 지원                  | 미지원    | 미지원                     |
  | Android   | 모바일 버전 QQ 브라우저              | -                            | 지원                  | 미지원    | 미지원                     |
  | Android   | 모바일 버전 Firefox 브라우저         | -                            | 지원                  | 미지원    | 미지원                     |
  | Android   | 모바일 UC 브라우저                   | -                            | 지원(LVB 보기만 지원) | 미지원    | 미지원                     |
  
  ### 도메인 요구 사항
  브라우저는 보안, 프라이버시 관련 문제 때문에 HTTPS 프로토콜 아래에서만 웹페이지의 TUIPusher & TUIPlayer의 모든 기능을 정상적으로 사용할 수 있도록 제한합니다. 프로덕션 환경 사용자의 원활한 액세스와 TUIPusher & TUIPlayer의 전체 기능 경험을 위해 HTTPS 프로토콜로 멀티미디어 애플리케이션 페이지에 액세스하십시오.
  >! 로컬 개발은 `http://localhost` 프로토콜을 통해 액세스할 수 있습니다.
  
  URL 도메인 및 프로토콜 지원은 다음 표 참고:
  
  | 응용 시나리오  | 프로토콜           | TUIPlayer | TUIPusher | TUIPusher 화면 공유 | 비고 |
  | -------------- | ------------------ | --------- | --------- | ------------------- | ---- |
  | 프로덕션 환경  | HTTPS 프로토콜     | 지원      | 지원      | 지원                | 권장 |
  | 프로덕션 환경  | HTTP 프로토콜      | 지원      | 미지원    | 미지원              | -    |
  | 로컬 개발 환경 | `http://localhost` | 지원      | 지원      | 지원                | 권장 |
  | 로컬 개발 환경 | `http://127.0.0.1` | 지원      | 지원      | 지원                | -    |
  | 로컬 개발 환경 | `http://[로컬 IP]` | 지원      | 미지원    | 미지원              | -    |
  
  ### 방화벽 제한
  TUIPusher & TUIPlayer는 아래 포트에 종속되어 데이터를 전송하므로  방화벽 얼로우리스트에 추가하십시오.
  - TCP 포트: 8687
  - UDP 포트: 8000, 8080, 8800, 843, 443, 16285
  - 도메인: qcloud.rtc.qq.com
  
  ## 결론
  추후 업데이트에서 TRTC Web 푸시/풀 스트림 컴포넌트는 점차적으로 iOS, Andriod 등과 연결되고 Web 에서 시청자 마이크 연결, 고급 뷰티필터, 맞춤형 레이아웃, 멀티 플랫폼 스트림 전송 외에 이미지, 텍스트 및 음악 업로드가 구현됩니다. 많이 이용해주시고 소중한 의견 부탁드립니다.
  
  요구 사항이나 피드백은 colleenyu@tencent.com으로 보내주시기 바랍니다.
