## 기능 소개
커뮤니티 모드(엔터테인먼트 협업을 위한 새로운 도구)는 **커뮤니티**-**그룹**-**토픽**3단계 구조를 지원하고, 메시지를 서로 분리할 수 있으며, 초대형 참석자를 운영하고, 친구 관계를 공유하며, 또한 참석자를 그룹화하고, 참석자 그룹 보기, 말하기 및 관리 등 권한을 설정할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7429b1c2a707a4f4f553cd7c2cbcb0db.jpg)
![](https://qcloudimg.tencent-cloud.cn/raw/8db16f94e4ab49ede5dc4207e9b20075.jpg)

## 적용 시나리오
### 친구 사귀기: 새로운 사용자 증가 모델
- 초대형 동호회 모임을 지원하며 **커뮤니티**-**그룹**-**토픽**을 통해 관심사를 수직적으로 세분화 할 수 있습니다.
- 대규모 공개 커뮤니티에서는 사용자에게 폐쇄적인 작은 토픽을 제공하고, 이러한 편안한 중간 지대는 사용자가 원하는 토픽을 선택해 커뮤니케이션할 수 있어, 참석자의 적극적인 참여를 유도합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/38f61b81280afed8df7cd699bbb204fb.jpg)

### 게임 커뮤니티: 사용자 충성도 및 활성도 개선
커뮤니티의 다양한 토픽은 유저의 정보 획득, 팀원 모집, 스토리텔링, 전략 공유 등 많은 정보 요구를 완벽하게 해결할 수 있습니다. 게임을 하기 전에 의논할 수 있고, 게임 중 언제든지 음성으로 대화할 수 있으며(채팅방은 항상 온라인 상태), 게임이 끝난 후에도 토픽에 대한 깊이 있는 커뮤니케이션을 계속할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e613a51181f771a6309731f8f5b5a09a.jpg)

### 팬 운영: 효율적인 운영 툴 보유
각각의 독립된 그룹(‘선전 사용자 1그룹’ ‘선전 사용자 2그룹’ ‘광저우 사용자 1그룹’ ‘상하이 사용자 1그룹’ 등 여러 그룹 대체)을 운영할 필요 없이 하나의 커뮤니티에서 다양한 토픽을 다룰 수 있기 때문에 더 이상 여러 그룹을 동시에 관리해야 하는 걱정을 할 필요가 없어 팬 운영이 더 쉽고 정확해집니다!
![](https://qcloudimg.tencent-cloud.cn/raw/45d3d5e8818cea79dd65b3b7abbb8d86.jpg)

### 조직 관리: 명확한 레이어 커뮤니케이션 구현
조직의 모든 구성원은 동일한 커뮤니티에 참여해 커뮤니티의 레이어 기능과 권한 설정에 따라 레이어 커뮤니케이션할 수 있습니다. 예를 들어, A 부서 구성원에게만 A 토픽을, B 부서 구성원에게만 B 토픽을 표시하도록 설정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/aa633c15337fbb8befe6c3f9a9a4f890.jpg)

## 기술 경쟁력
### 초대형 규모 그룹 구성원
Tencent IM 커뮤니티는 일반 QQ, 위챗 그룹보다 용량이 1만 배 가까이 확장되어, 취미 친구 사귀기, 팬 운영, 게임 커뮤니티, 조직 관리 등, 다인원 니즈를 충족시킵니다.
### 메시지 신뢰성
Tencent IM 커뮤니티는 구성원 용량을 대폭 확대하면서 Tencent의 강력한 메시징 능력을 이어받아 20여 년의 기술 축적을 바탕으로 구축한 완벽하고 신뢰할 수 있는 메시징 시스템입니다. 99.99% 이상의 메시지 송수신 성공률 및 서비스 신뢰성을 고객에게 제공하여 고객이 수억 대의 대규모 동시성에 쉽게 대처할 수 있도록 지원합니다.
### 메시지 푸시 성능
Tencent IM 커뮤니티는 ‘빠르고 느린 채널’ + ‘2단계 결합 푸시’의 새로운 메시지 푸시 아키텍처를 채택하여 시간과 공간의 균형을 효과적으로 유지하고, 시스템 푸시 성능을 향상시키며, 단말 성능 소모를 줄이고, 초대형 그룹의 사용자에게도 일반 그룹과 동일한 메시지 인터랙션 경험을 제공할 수 있습니다.

### 메시지 상태 및 사용자 권한 관리
Tencent IM 커뮤니티는 메시지 편집, 회수, 포워딩 등 풍부한 확장 기능을 제공합니다. 음소거, 메시지 방해 금지, 읽지 않음 메시지 수, 프로필 편집 등은 사용자가 전역, 커뮤니티, 토픽 수준을 각각 사용자 정의할 수 있도록 지원합니다.

## 단말 SDK 통합 가이드
>!커뮤니티(Community) 토픽(Topic) 기능은 IM 터미널 SDK 6.2.2363 인핸스드 버전 이상에서만 지원되며, [플래그십 버전 구매](https://www.tencentcloud.com/document/product/1047/34577) 및 [활성화 신청](https://intl.cloud.tencent.com/document/product/1047/44322) 후 사용할 수 있습니다.

다음은 Android를 예시로 커뮤니티 토픽의 인터페이스 기능을 소개합니다.

### 빠른 체험을 위한 Demo 소스 코드 다운로드 및 설정
[시작하기](https://intl.cloud.tencent.com/document/product/1047/45914)를 참고하여 IM의 기능을 빠르게 체험할 수 있습니다(커뮤니티 토픽의 UI 컴포넌트는 개발 중이니 많은 관심 부탁드립니다).
다음은 API 호출의 관점에서 커뮤니티 토픽의 사용을 소개합니다.

### 커뮤니티 토픽의 API 사용
1. 먼저 createGroup 인터페이스를 호출하여 토픽을 지원하는 커뮤니티를 생성하고, [커뮤니티 관리](https://intl.cloud.tencent.com/document/product/1047/48172) ‘커뮤니티 생성’ 단계를 참고하여 구현할 수 있습니다.
2. 그 다음 getJoinedCommunityList 인터페이스를 호출하여 이러한 유형의 생성 및 가입 커뮤니티 목록을 가져올 수 있습니다.
>!커뮤니티는 그룹 구성원을 관리하는 데 사용되지만 커뮤니티에서 메시지를 주고받을 수는 없습니다. 커뮤니티의 다른 기능에 대해서는 ‘기타 관리 인터페이스’ 목록을 참고하십시오.
>
3. 커뮤니티가 성공적으로 생성되면 커뮤니티에서 createTopicInfoCommunity를 호출하여 여러 개의 토픽을 생성할 수 있습니다. [토픽 관리](https://intl.cloud.tencent.com/document/product/1047/48172)의 ‘토픽 생성’ 단계를 참고하십시오.
4. 토픽 관리에는 ‘토픽 삭제’, ‘토픽 정보 수정’, ‘토픽 목록 가져오기’ 및 ‘토픽 콜백 수신’ 기능도 포함됩니다. 동시에 토픽은 사용자가 메시지를 주고받을 수 있는 커뮤니케이션의 장이며, 관련 인터페이스는 [토픽 메시지](https://intl.cloud.tencent.com/document/product/1047/48172) 소개를 참고하십시오.

## Web  SDK 통합 가이드
>!커뮤니티(Community) 토픽(Topic) 기능은 IM Web SDK v2.19.1 이상에서만 지원되며, [플래그십 버전 구매](https://www.tencentcloud.com/document/product/1047/34577) 및 [활성화 신청](https://intl.cloud.tencent.com/document/product/1047/44322) 후 사용 가능합니다.
>
커뮤니티 토픽의 인터페이스 기능은 다음과 같습니다.
### 빠른 체험을 위한 Demo 소스 코드 다운로드 및 설정
[시작하기](https://intl.cloud.tencent.com/document/product/1047/45912)를 참고하여 IM 기능을 빠르게 경험할 수 있습니다.
다음은 API 호출의 관점에서 커뮤니티 토픽의 사용을 소개합니다.

### 커뮤니티 토픽의 API 사용
1. 먼저 createGroup 인터페이스를 호출하여 토픽을 지원하는 커뮤니티를 생성하고, [커뮤니티 관리](https://intl.cloud.tencent.com/document/product/1047/48171) ‘커뮤니티 생성’ 단계를 참고하여 구현할 수 있습니다.
2. 그 다음 getJoinedCommunityList 인터페이스를 호출하여 이러한 유형의 생성 및 가입 커뮤니티 목록을 가져올 수 있습니다. 커뮤니티는 그룹 구성원을 관리하는 데 사용되지만 토픽을 지원하는 커뮤니티에서 메시지를 주고 받을 수는 없습니다. 커뮤니티의 다른 기능에 대해서는 일반 그룹 API를 참고하십시오.
3. 커뮤니티 생성이 완료되면 커뮤니티에 createTopicInfoCommunity를 호출하여 여러 토픽을 생성할 수 있습니다. [토픽 관리](https://intl.cloud.tencent.com/document/product/1047/48171)의 ‘토픽 생성’ 단계를 참고하십시오.
4. 토픽 관리에는 ‘토픽 삭제’, ‘토픽 정보 수정’, ‘토픽 목록 가져오기’ 및 ‘토픽 콜백 수신’ 기능도 포함됩니다. 동시에 토픽은 사용자가 메시지를 주고받을 수 있는 커뮤니케이션의 장이며, 관련 인터페이스는 [메시지 생성](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#createTextMessage) 소개를 참고하십시오.

## 관련 문서
- [그룹 관리](https://intl.cloud.tencent.com/document/product/1047/33530)
- [그룹 시스템](https://intl.cloud.tencent.com/document/product/1047/33529)
- [SDK 다운로드](https://intl.cloud.tencent.com/document/product/1047/33996)
- [SDK 매뉴얼](https://web.sdk.qcloud.com/im/doc/zh-cn/TIM.html)
- [Android](https://intl.cloud.tencent.com/document/product/1047/34306)
- [SDK Integration (iOS)](https://intl.cloud.tencent.com/document/product/1047/34307)
- [SDK Integration (Web)](https://intl.cloud.tencent.com/document/product/1047/34309)

## 문의하기
사용에 문제가 있는 경우 [문의하기](https://intl.cloud.tencent.com/document/product/1047/41676)를 통해 문의해 주시기 바랍니다.
