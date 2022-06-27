## 컴포넌트 개요

TUIPusher & TUIPlayer는 Web 기반 오픈 소스 라이브 스트리밍 컴포넌트(UI 포함)입니다. 이를 [TRTC](https://intl.cloud.tencent.com/product/trtc) 및 [IM](https://intl.cloud.tencent.com/product/im)과 같은 Tencent Cloud의 기본 SDK에 통합하여 라이브 스트리밍 애플리케이션(기업 라이브 스트리밍, 라이브 쇼핑, 직업 교육, 원격 교육 등)에 Web 기반 게시 및 재생 기능을 신속하게 장착할 수 있습니다.

TUIPusher & TUIPlayer 의 장점:
+ 디바이스 선택, 뷰티 필터, 퍼블리싱, 재생 및 라이브 채팅과 같은 일반적인 라이브 스트리밍 기능을 포함하는 UI가 있는 범용 라이브 스트리밍 솔루션으로 서비스를 시장에 신속하게 출시할 수 있습니다.
+ 뛰어난 유연성과 확장성을 위해 TRTC, IM 및 TCPlayer를 포함한 Tencent Cloud의 기본 SDK에 쉽게 통합됩니다.
+ Web 기반, 사용하기 쉽고 빠른 업데이트.

![](https://qcloudimg.tencent-cloud.cn/raw/d1670385df8944886472e6c17d577949.png)

## 빠른 체험

사용자 및 회의실 관리 시스템이 포함된 [TUIPusher 데모](https://web.sdk.qcloud.com/component/tuiliveroom/tuipusher/login.html) 및 [TUIPlayer 데모](https://web.sdk.qcloud.com/component/tuiliveroom/tuiplayer/login.html)를 제공합니다. 기능을 체험해 볼 수 있습니다.
>! TUIPusher와 TUIPlayer를 동시에 사용하려면 두 개의 다른 계정으로 로그인해야 합니다. 

### TUIPusher 기능 개요
- 카메라 및 마이크에서 스트림 캡처 및 게시
  - 프레임 레이트, 해상도 및 비트 레이트를 포함한 비디오 매개변수 사용자 정의
  - 뷰티 필터 적용 및 뷰티 필터 매개변수 설정
- 화면에서 데이터 캡처 및 게시
- TRTC 백엔드 및 Tencent Cloud의 CDN에 게시
- 앵커 및 다른 청중과의 문자 채팅
- 시청자 리스트 가져오기 및 온라인 시청자 음소거

### TUIPlayer 기능 개요
- 오디오 및 비디오 스트림과 화면 공유 스트림 동시 재생
- 앵커 및 다른 시청자와의 문자 채팅
- 3가지 재생 옵션: 초저지연 라이브 스트리밍(대기 시간 300ms), LEB(대기 시간 1000ms 이내) 및 LVB(동시성 높음)
- 모바일 장치에서 데스크톱 및 모바일 브라우저와 가로 모드 지원

> !브라우저가 WebRTC를 지원하지 않고 표준 라이브 스트리밍 프로토콜을 통해서만 비디오를 재생할 수 있는 경우 다른 브라우저를 사용하여 WebRTC 재생을 시도하십시오.

## 컴포넌트 통합

### 1단계: Tencent Cloud 서비스 활성화

> !
> - TUIPusher & TUIPlayer는 Tencent Cloud TRTC 및 IM 서비스를 기반으로 합니다. TRTC 및 IM 애플리케이션이 계정 및 인증 정보를 공유할 수 있도록 동일한 SDKAppID를 사용해야 합니다.
> - IM의 기본 버전 콘텐츠 필터링 기능을 사용하여 채팅 메시지를 필터링할 수 있습니다. 제한된 단어를 사용자 지정하려면 IM 콘솔에서 콘텐츠 필터링으로 이동하고 **업그레이드**를 클릭합니다.
> - 로컬 UserSig 계산 방법은 로컬 개발 및 디버깅에만 사용됩니다. 온라인 시스템에 게시하지 마십시오. SECRETKEY가 공개되면 공격자가 승인 없이 Tencent Cloud 트래픽을 사용할 수 있습니다. 올바른 UserSig 배포 방법은 UserSig의 컴퓨팅 코드를 서버에 통합하고 App 지향 API를 제공하는 것입니다. UserSig가 필요한 경우 App은 동적 UserSig를 얻기 위해 비즈니스 서버에 요청을 보낼 수 있습니다. 자세한 내용은 UserSig 생성의 서버에서 [UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.


<dx-tabs>
::: 방식1: TRTC 기반
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
<li>TRTC 콘솔에서 첫 번째 애플리케이션을 생성하는 계정은 10000분 무료 평가판 패키지를 받게 됩니다.</li>
<li>TRTC 애플리케이션 생성 후 동일한 SDKAppID를 가진 IM 애플리케이션이 자동으로 생성되며, 이 애플리케이션의 패키지 정보는 [IM 콘솔](https://console.cloud.tencent.com/im)에서 구성할 수 있습니다.</li></dx-alert>

:::
::: 방식2: IM 기반
#### 1단계: IM 애플리케이션 생성
1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인하고 **애플리케이션 생성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f7497abca24a87c459d34cb849031541.png)
2. 팝업 창에서 애플리케이션 이름을 입력하고 **확인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7bef16f8bfd19208eab6051d548d05e4.png)
3. [IM 콘솔](https://console.cloud.tencent.com/im)의 전체보기 페이지에서 새로 생성된 애플리케이션의 상태, 서비스 버전, SDKAppID, 생성 시간 및 만료 시간을 확인할 수 있습니다. SDKAppID 정보를 기록해 두십시오.

#### 2단계: IM 키 획득 및 TRTC 서비스 활성화
1. [IM 콘솔](https://console.cloud.tencent.com/im)의 전체보기 페이지에서 새로 생성한 IM 애플리케이션을 클릭하여 해당 애플리케이션의 기본 설정 페이지로 이동합니다. **기본 정보**에서 **키 표시**를 클릭하여 키 정보를 복사 및 저장합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f211f03fdb78d548aba80fcdd67219a8.png)
<dx-alert infotype="notice">키 정보가 유출되지 않도록 잘 보관하십시오.</dx-alert>
2. 해당 애플리케이션의 기본 설정 페이지에서 TRTC 서비스를 활성화합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a202eda15b427b9c24cd4290a79243a7.png)
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
4. 로컬 개발 환경에서 TUIPusher & TUIPlayer를 실행합니다.
```bash
cd Web/TUIPusher
npm run serve

cd Web/TUIPlayer
npm run serve
```
5. `http://localhost:8080` 및 `http://localhost:8081`을 열어 TUIPusher 및 TUIPlayer의 기능을 체험할 수 있습니다.
6. `TUIPusher/src/config/basic-info-config.js` 및 `TUIPlayer/src/config/basic-info-config.js` 에서 방, 앵커 및 시청자 정보를 변경할 수 있습니다. **TUIPusher 및 TUIPlayer의 방 정보와 앵커 정보는 일치해야 합니다**.

>!
> - 상기 설정을 완료한 후, TUIPusher & TUIPlayer를 사용하여 초저지연 라이브 방송을 진행할 수 있으며, LEB와 LVB 지원이 필요한 경우, [3단계: 릴레이 라이브 방송](#step3)을 계속 읽어주십시오.
> - UserSig 로컬 계산 방식은 로컬 개발 디버깅에만 사용하고 온라인에 배포하지 마십시오. `SECRETKEY`가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다.
> - 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.

[](id:step3)
### 3단계: 릴레이 라이브 방송

TUIPusher & TUIPlayer로 구현된 LEB 및 LVB는 Tencent Cloud [CSS 서비스](https://intl.cloud.tencent.com/document/product/267)에 의존하므로, LEB 및 LVB 회선을 지원하려면 릴레이 푸시 스트림 기능을 활성화해야 합니다.

1. [**TRTC 콘솔**](https://console.cloud.tencent.com/trtc)에서 사용 중인 애플리케이션에 대한 릴레이 푸시 스트림 설정을 활성화하고 필요에 따라 특정 스트림 릴레이 또는 전역 자동 릴레이를 활성화할 수 있습니다.  
![img](https://qcloudimg.tencent-cloud.cn/raw/b65584a5b096481ade6e302dabedcd5f.png)
2. [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage) 페이지에 재생 도메인을 추가하십시오. 자세한 내용은 [외부 도메인 추가](https://intl.cloud.tencent.com/document/product/267/35970)를 참고하십시오.
3. `TUIPlayer/src/config/basic-info-config.js` 구성 파일에서 재생 도메인을 구성합니다.

상기 구성을 완료하면 초저지연 라이브 방송, LEB, LVB를 지원하는 TUIPusher & TUIPlayer의 모든 기능을 경험할 수 있습니다.

[](id:step4)
### 4단계: 프로덕션 환경 애플리케이션

TUIPusher & TUIPlayer를 프로덕션 환경에 적용하려면 프로젝트에 통합하는 것 외에도 다음을 수행해야 합니다.

- 사용자 ID, 사용자 이름, 프로필 사진과 같은 사용자 정보를 관리하는 사용자 관리 시스템을 구축합니다
- 방 ID, 방 이름, 앵커 등 방 정보를 관리하는 방 관리 시스템을 구축합니다.
- 서버의 UserSig를 생성합니다.

> !
> - 본문의 UserSig 생성 방법은 귀하가 입력한 sdkAppId 및 secretKey에 따라 클라이언트 측에서 userSig를 생성하는 것입니다. 이 secretKey 방식은 디컴파일 및 역크래킹 되기 쉽기 때문에 키가 유출되면 공격자가 Tencent Cloud 트래픽을 도용할 수 있습니다. **이 방법은 TUIPusher & TUIPlayer 로컬 실행을 통한 기능 디버깅에만 적합합니다**.
> - 올바른 UserSig 배포 방법은 UserSig의 계산 코드를 서버에 통합하고 App 지향 API를 제공하는 것입니다. UserSig가 필요할 때 애플리케이션은 동적 UserSig에 대한 요청을 비즈니스 서버에 보낼 수 있습니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

- `TUIPusher/src/pusher.vue` 및 `TUIPlayer/src/player.vue`와 같이 글로벌 저장을 위한 vuex의 store에 사용자 정보, 방 정보, SDKAppID 및 UserSig와 같은 계정 정보를 제출하면 모든 기능을 사용할 수 있습니다. 게시 및 재생 클라이언트의 두 컴포넌트 중 하나입니다. 아래 다이어그램은 프로세스를 자세히 보여줍니다.
![](https://qcloudimg.tencent-cloud.cn/raw/30e959d1b4605532f6d4cac190cdd1df.png)

## FAQ
### Web에서 뷰티 필터 기능을 구현하는 방법은 무엇입니까?
[뷰티 필터 활성화](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-28-advanced-beauty.html)를 참고하십시오.

### Web에서 화면 공유를 구현하는 방법은 무엇입니까?
자세한 내용은 [화면 공유](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-16-basic-screencast.html)를 참고하십시오.

### Web에서 클라우드 녹화를 구현하는 방법은 무엇입니까?
1. **클라우드 녹화**기능 활성화의 구체적인 작업은 [클라우드 녹화 및 재생 구현](https://intl.cloud.tencent.com/document/product/647/35426)을 참고하십시오.
2. **클라우드 녹화**> **특정 사용자 녹화** 활성화 후 Web에서 [TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createClient) 인터페이스를 호출할 때 userDefineRecordId 매개변수를 전달하여 녹화를 활성화할 수 있습니다.
	
### Web에서 CDN으로 푸시하는 방법은 무엇입니까?
Web에서 CDN으로 푸시 스트림하려면 [CDN으로 푸시 스트림하기](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-26-advanced-publish-cdn-stream.html)를 참고하십시오.

### Web에서 LEB 풀 스트림을 구현하는 방법은 무엇입니까?
LEB 풀 스트림을 구현하는 방법은 Web SDK를 통해 스트림을 CDN으로 푸시한 후 WebRTC 프로토콜을 사용하여 프로토콜을 가져오는 것입니다.

## 주의 사항
###  지원 플랫폼

| 운영 체제 | 브라우저 유형                   | 브라우저 최저 버전 요구 사항 | TUIPlayer                  | TUIPusher | TUIPusher 화면 공유           |
| :------- | :--------------------------- | :----------------- | :------------------------- | :-------- | :--------------------------- |
| Mac OS   | 데스크톱 버전 Safari 브라우저         | 11+                | 지원      | 지원      | 지원(Safari13+ 버전 필요)  |
| Mac OS   | 데스크톱 버전 Chrome 브라우저         | 56+                | 지원      | 지원      | 지원(Chrome72+ 버전 필요)  |
| Mac OS   | 데스크톱 버전 Firefox 브라우저        | 56+                | 지원      | 지원      | 지원(Firefox66+ 버전 필요) |
| Mac OS   | 데스크톱 버전 Edge 브라우저           | 80+                | 지원                       | 지원      | 지원                         |
| Mac OS   | 데스크톱 버전 WeChat 내장 웹 페이지            | -                  | 지원                       | 미지원    | 미지원                       |
| Mac OS   | 데스크톱 버전 WeCom 내장 웹 페이지        | -                  | 지원                       | 미지원    | 미지원                       |
| Windows  | 데스크톱 버전 Chrome 브라우저         | 56+                | 지원      | 지원      | 지원(Chrome72+ 버전 필요)  |
| Windows  | 데스크톱 버전 QQ 브라우저(고속 커널) | 10.4+              | 지원                       | 지원      | 미지원                       |
| Windows  | 데스크톱 버전 Firefox 브라우저        | 56+                | 지원      | 지원      | 지원(Firefox66+ 버전 필요) |
| Windows  | 데스크톱 버전 Edge 브라우저           | 80+                | 지원                       | 지원      | 지원                         |
| Windows  | 데스크톱 버전 WeChat 내장 웹 페이지            | -                  | 지원                       | 미지원    | 미지원                       |
| Windows  | 데스크톱 버전 WeCom 내장 웹 페이지        | -                  | 지원                       | 미지원    | 미지원                       |
| iOS      | WeChat 내장 브라우저               | -                  | 지원                       | 미지원    | 미지원                       |
| iOS      | WeCom 내장 브라우저           | -                  | 지원                       | 미지원    | 미지원                       |
| iOS      | 모바일 버전 Safari 브라우저         | -                  | 지원                       | 미지원    | 미지원                       |
| iOS      | 모바일 버전 Chrome 브라우저         | -                  | 지원                       | 미지원    | 미지원                       |
| Android  | WeChat 내장 브라우저               | -                  | 지원                       | 미지원    | 미지원                       |
| Android  | WeCom 브라우저               | -                  | 지원                       | 미지원    | 미지원                       |
| Android  | 모바일 버전 Chrome 브라우저         | -                  | 지원                       | 미지원    | 미지원                       |
| Android  | 모바일 버전 QQ 브라우저             | -                  | 지원                       | 미지원    | 미지원                       |
| Android  | 모바일 버전 Firefox 브라우저        | -                  | 지원                       | 미지원    | 미지원                       |
| Android  | 모바일 UC 브라우저             | -                  | 지원(LVB 보기만 지원) | 미지원    | 미지원                       |

### 도메인 요구 사항
보안 및 개인 정보 보호를 위해 HTTPS URL만 TUIPusher & TUIPlayer의 모든 기능에 액세스할 수 있습니다. 따라서 프로덕션 환경에서 애플리케이션의 웹 페이지에 대해 HTTPS 프로토콜을 사용하십시오.
>! 로컬 개발은 `http://localhost` 프로토콜을 통해 액세스할 수 있습니다.

URL 도메인 및 프로토콜 지원은 다음 표 참고:

| 응용 시나리오 | 프로토콜 | TUIPlayer | TUIPusher | TUIPusher 화면 공유 | 비고 |
| ------- | ------- | ------- | ------- | ------- | ------- |
| 프로덕션 환경     | HTTPS 프로토콜         | 지원      | 지원      | 지원               | 권장 |
| 프로덕션 환경     | HTTP 프로토콜 | 지원      | 미지원    | 미지원 | - |
| 로컬 개발 환경 | `http://localhost` | 지원 | 지원 | 지원 | 권장 |
| 로컬 개발 환경 | `http://127.0.0.1`| 지원 | 지원 | 지원 | - |
| 로컬 개발 환경 | `http://[로컬 IP]`  | 지원         | 미지원       | 미지원   |  -    |

### 방화벽 제한
TUIPusher & TUIPlayer는 데이터 전송을 위해 다음 포트 및 도메인에 의존하며, 이는 방화벽의 얼로우리스트에 추가되어야 합니다.
- TCP 포트: 8687
- UDP 포트: 8000, 8080, 8800, 843, 443, 16285
- 도메인: qcloud.rtc.qq.com

## 결론
추후 업데이트에서 iOS, Android 등을 위한 Web 컴포넌트와 TRTC SDK 간의 통신에 대한 지원을 추가하고 공동 앵커, 고급 필터, 사용자 지정 레이아웃, 여러 플랫폼으로 중계 및 이미지/텍스트/음악 업로드와 같은 기능을 도입할 계획입니다. 많이 이용해주시고 소중한 의견 부탁드립니다.

요구 사항이나 피드백은 colleenyu@tencent.com으로 보내주시기 바랍니다.

