TUIKit은 주요 오디오/비디오 시나리오에서 5000+ 고객에게 서비스를 제공한 경험을 기반으로 Tencent Cloud 오디오/비디오 팀에서 개발한 오픈 소스 솔루션입니다. 여기에는 영상 통화, 라이브 스트리밍, 비디오 룸 등을 위한 여러 클라이언트 오디오/비디오 컴포넌트가 포함되어 있어 통화, 고객 서비스, 라이브 스트리밍, 오디오 채팅 및 교육 시나리오에 대한 솔루션을 빠르게 구축할 수 있습니다.

>?TUIKit 시리즈 컴포넌트는 Tencent Cloud의 두 가지 기본 PaaS 서비스, 즉 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078) 및 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047/35448)을 사용합니다. TRTC를 활성화하면 IM과 IM SDK 평가판(100 DAU만 지원)이 자동으로 활성화됩니다. IM 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

## TUIKit 패밀리 버킷
![](https://qcloudimg.tencent-cloud.cn/raw/22b2ed779af3b76550ae5eefc8704e4c.png)

상기 이미지와 같이 TUIKit은 TUICompenont 및 TUIWidget 범주로 나눌 수 있으며 기본 백엔드 서비스 옵션을 지원합니다.
```java
├── TUIComponent
│   ├── TUICalling     // WeChat의 통화 기능과 유사하며 영상 통화, 고객 서비스, 재무 검토와 같은 음성/영상 시나리오에서 사용할 수 있는 통화 컴포넌트;
│   ├── TUIRoom        // 교육, 회의, 인터뷰 등의 오디오/비디오 시나리오에서 사용할 수 있고 음소거 및 화면 정지와 같은 기능을 지원하는 그룹 비디오 룸 컴포넌트;
│   ├── TUILiveVoice   // 오디오 채팅룸 및 뮤직룸과 같은 오디오 시나리오에서 사용할 수 있는 오디오 채팅 라이브 스트리밍 컴포넌트; 
│   ├── TUILiveVideo   // 공동 앵커, PK 및 음향 효과와 같은 기능이 있는 비디오 인터랙티브 라이브 스트리밍 컴포넌트;
│   ├── TUIChatSolon   // 비즈니스 원탁 회의 및 포럼과 같은 오디오/비디오 시나리오에서 사용할 수 있는 음성 살롱 컴포넌트;
│   ├── TUIPusher      // 다양한 프로토콜 푸시, PK 등 기능과 사운드 효과, 화면 주석 등 위젯을 지원하는 완전한 UI가 있는 푸시 컴포넌트;
│   ├── TUIPlayer      // 다양한 프로토콜 스트리밍, 공동 앵커 등 기능과 화면 댓글, 선물하기 등 위젯을 지원하는 완전한 UI가 있는 풀 스트림 컴포넌트;
│   ├── TUIChorus       // Tencent Cloud의 저작권 보호 음원 라이브러리와 함께 사용 시 더 많은 기능을 지원하는 혁신적인 코러스용 오디오/비디오 컴포넌트;
│   ├── TUIKaraoke      // Tencent Cloud의 저작권 보호 음원 라이브러리와 함께 사용 시 더 많은 기능을 지원하는 온라인 KTV 등 새로운 플레이를 위한 혁신적인 오디오/비디오 컴포넌트;
├── TUWidget
│   ├── TUIBeauty      // 뷰티 필터 위젯
│   ├── TUIAudioEffect // 음향 효과 위젯
│   ├── TUIBarrage     // 화면 댓글 위젯
│   ├── TUIGift        // 선물 위젯
├── aPass (옵션)
│   ├── Room Service   // 방 목록, 방 인기도, 앵커 목록 등의 기능 제공;
```

## 기술 교류&피드백
동일한 환경과 프로세스를 사용하더라도 개발자마다 다른 유형의 오류가 발생할 수 있습니다. 요구 사항이나 피드백이 있는 경우 colleenyu@tencent.com으로 문의 주시기 바랍니다.