Tencent Real-Time Communication(TRTC)은 저지연 양방향 라이브 스트리밍과 음성/영상 통화라는 두 가지 주요 솔루션을 제공합니다. 저지연 라이브 스트리밍, 실시간 녹화, 화면 공유, 뷰티 필터, 스테레오 사운드 등 다양한 기능을 갖추고 있으며 CDN과 끊김 없이 연결할 수 있습니다. 인터랙티브 공동 앵커링, 크로스 룸 커뮤니케이션, 라디오, 노래방, 온라인 수업, 음성 채팅, 화상 채팅 및 온라인 회의와 같은 시나리오에 이상적입니다. 본 문서에서는 두 가지 주요 솔루션이 다루는 비즈니스 시나리오에 대해 설명합니다.

 

## 인터랙티브 오디오 라이브 스트리밍

### 음성 채팅방

TRTC를 사용하면 최대 50명의 사용자가 동시에 마이크를 켜고 채팅할 수 있으며 300ms 미만의 지연 시간으로 원활하게 마이크를 켜고 끌 수 있습니다. 음성 변경, 음향 효과 및 리버브와 같은 다양한 오디오 효과를 지원하여 풍부한 오디오 채팅 경험을 제공합니다. Tencent Cloud IM과 연동하여 공개 채팅, 비공개 채팅, 그룹 채팅, 좋아요, 선물하기 등 다양한 상호작용을 지원합니다. 또한 시나리오 기반의 음성 채팅방 컴포넌트를 제공하여 직접 재사용하여 개발 비용을 최소화할 수 있습니다. 컴포넌트 사용 방법에 대한 자세한 내용은 [음성 채팅방](https://intl.cloud.tencent.com/document/product/647/37287)을 참고하십시오.

<img src="https://main.qcloudimg.com/raw/6cfa30cdad7901bcba9450c242834f12.png" width="800px">


### 라디오

TRTC는 48kHz 샘플링 레이트, 192kbps 비트 레이트 및 스테레오 사운드를 지원합니다. MP3, AAC, WAV 등 다양한 포맷의 로컬 음악을 배경 음악으로 재생할 수 있어 고품질 라디오 방송국을 구축할 수 있습니다. 라디오 쇼를 더 즐겁게 만드는 다양한 음성 변경 효과를 제공합니다. 또한 시나리오 기반 무선 컴포넌트를 제공하므로 직접 재사용하여 개발 비용을 최소화할 수 있습니다. 컴포넌트를 사용하는 방법에 대한 자세한 내용은 [음성 채팅방](https://intl.cloud.tencent.com/document/product/647/37287)을 참고하십시오.

<img src="https://main.qcloudimg.com/raw/102527ee25e9f61fbab458036af3b083.png" width="800px">

### 온라인 노래방

TRTC는 48kHz 샘플링 레이트와 128kbps 비트 레이트, 및 스테레오 사운드를 지원하여 녹음 스튜디오에 필적하는 음질로 온라인 노래방 경험을 제공합니다. 300ms 미만의 매우 짧은 대기 시간을 특징으로 하여 그룹 노래에 이상적입니다. 메시지 패스스루 및 타임스탬프와 같은 다중 동기화 메커니즘은 반주, 보컬 및 가사가 온라인 노래방 중에 정확하게 동기화되도록 합니다. 또한 사용자가 쉽게 곡을 연주할 수 있도록 인이어 모니터링을 지원합니다.

<img src="https://main.qcloudimg.com/raw/7b40ba0b78d6a1fb21b171bada61fd55.png" width="800px">


## 인터랙티브 비디오 라이브 스트리밍

### 라이브 쇼

TRTC는 크로스 룸 커뮤니케이션을 위해 300ms 미만의 대기 시간을 제공하고 시청자와 앵커 간의 원활한 상호 작용을 가능하게 하여 라이브 스트리밍 쇼 중 빈번한 상호 작용에 대한 요구 사항을 충족하는 데 도움이 됩니다. 쇼를 더 매력적으로 만들고 앵커와 게스트가 최상의 모습을 보일 수 있도록 해주는 스마트 뷰티 필터를 지원합니다. 또한 시나리오 기반 라이브 쇼 스트리밍 컴포넌트를 제공하므로 직접 재사용하여 개발 비용을 최소화할 수 있습니다. 컴포넌트를 사용하는 방법에 대한 자세한 내용은 [인터랙티브 비디오 스트리밍](https://intl.cloud.tencent.com/document/product/647/36060)을 참고하십시오.

<img src="https://main.qcloudimg.com/raw/22ccbf4fdd523e99bbbc5df82986ba56.png" width="800px">

### 대규모 인터랙션 수업

TRTC를 사용하면 최대 10만명의 학생이 300ms 미만의 대기 시간으로 온라인 수업을 동시에 시청할 수 있습니다. 교사와 학생은 수업 중에 중단 없는 토론과 상호 작용을 위해 원활하게 마이크를 켜고 끌 수 있습니다. 화면 공유, 인터랙티브 화이트보드, 녹음 및 재생 등의 다양한 기능을 지원하여 보다 풍성한 대규모 온라인 인터랙션 수업이 가능합니다. 또한 시나리오 기반의 인터랙티브 대형 클래스 컴포넌트를 제공하므로 직접 재사용하여 개발 비용을 최소화할 수 있습니다. 컴포넌트를 사용하는 방법에 대한 자세한 내용은 [실시간 인터랙티브 수업](https://intl.cloud.tencent.com/document/product/647/37278)을 참고하십시오.

<img src="https://main.qcloudimg.com/raw/1a70063b1adb7eb7c8d29334e94bb009.png" width="800px">

### 소규모 인터랙션 수업

TRTC는 **1대1**, **1대2**, **1대6**, **1대32** 등 학생을 위한 수업을 포함하여 여러 소규모 수업을 지원하며 교사와 학생은 300ms 미만의 지연 시간으로 서로 상호 작용할 수 있습니다. 화면 공유, 강의 자료 공유, 인터랙티브 화이트보드 등 다양한 기능을 제공하여 교사가 온라인 수업 중에 다양한 교수법을 사용할 수 있습니다. 전체 강의를 녹음한 다음 나중에 재생할 수 있으므로 학생들은 수업을 다시 보고 학습 효과를 향상시킬 수 있습니다.

<img src="https://main.qcloudimg.com/raw/7537df580734cee29d1e5cb75e153c30.png" width="800px">






### 라이브 방송 퀴즈 풀기

TRTC는 높은 동시성(high-concurrency) 상황에서 저지연 라이브 스트리밍을 지원하므로 질문이 뷰어 클라이언트에 동기적으로 표시되어야 하는 Q&A 시나리오에 이상적입니다. 메시지 통과, 타임스탬프 및 신호 채널과 같은 다중 동기화 메커니즘을 지원하여 ‘오디오, 이미지 및 질문이 동기화’되어 초고도 동시(ultra-high-concurrence) IM 상호 작용에 대한 요구 사항을 충족합니다. 또한 퀴즈 상호 작용, 결과 통계 수집 및 라이브 스트리밍의 공동 앵커를 지원하여 온라인 Q&A를 더욱 흥미롭게 만듭니다. 또한 실시간으로 인터랙티브 라이브 스트리밍 중에 키워드 및 답변 힌트를 필터링할 수 있으므로 사용자 경험을 개선하고 규정 미준수의 위험을 줄이는 데 도움이 됩니다.

<img src="https://main.qcloudimg.com/raw/160233f65c098f14cc8cc3a3d29efd21.png" width="800px">


## 음성 통화

### 그룹 음성 통화

TRTC를 사용하면 300명의 사용자가 동시에 그룹 통화에 참여할 수 있으며 최대 50명의 사용자가 동시에 마이크를 켤 수 있습니다. 48kHz의 샘플 속도, 128kbps의 비트 레이트 및 Tencent Cloud의 3A 처리 기술과의 통합으로 부드럽고 높은 품질의 음성 통화 경험을 제공합니다. 또한 시나리오 기반의 그룹 음성 통화 컴포넌트를 제공하므로 직접 재사용하여 개발 비용을 최소화할 수 있습니다. 컴포넌트를 사용하는 방법에 대한 자세한 내용은 [음성 통화](https://intl.cloud.tencent.com/document/product/647/36067)를 참고하십시오.

<img src="https://main.qcloudimg.com/raw/ed6170c3b98a20897b4a37e7f6cc3d94.png" width="800px">

### 2인 음성 통화

300ms 미만의 통화 지연, 80% 이상의 패킷 손실 방지율, 1,000ms 이상의 네트워크 지터 방지 기능을 갖춘 TRTC는 약한 네트워크 환경에서도 부드럽고 안정적인 일대일 음성 통화를 가능하게 합니다. Tencent Cloud IM이 제공하는 다양한 통화 신호 관리 API와 통합하면 다양한 음성 통화 시나리오에 이상적입니다. 또한 시나리오 기반의 일대일 음성 통화 컴포넌트를 제공하므로 직접 재사용하여 개발 비용을 최소화할 수 있습니다. 컴포넌트를 사용하는 방법에 대한 자세한 내용은 [음성 통화](https://intl.cloud.tencent.com/document/product/647/36067)를 참고하십시오.

<img src="https://main.qcloudimg.com/raw/3466caeb004d88267dc45931558da18e.png" width="800px">

### 파티 게임

TRTC는 300ms 미만의 통화 지연, 80% 이상의 패킷 손실 방지율, 1000ms 이상의 네트워크 지터 방지 기능으로 약한 네트워크 환경에서도 원활하고 안정적인 파티 게임을 보장합니다. 뛰어난 게임 경험을 보장하기 위해 사용자 네트워크 상태의 실시간 모니터링을 지원합니다. 또한 사용자 오디오 장치를 테스트하여 비정상적인 오디오를 제거하고 게임 경험을 더욱 향상시킬 수 있습니다.

<img src="https://main.qcloudimg.com/raw/99d3c8a140ff1b05ce38a468c7b5ea80.png" width="800px">

### 음성 회의

TRTC는 플랫폼 간 호환성을 지원하므로 사용자가 휴대폰, PC 및 태블릿에서 회의에 참여할 수 있습니다. 뛰어난 3A 처리 기술로 에코와 하울링을 제거하고 부드럽고 깨끗한 회의 통화를 보장합니다. 또한 인터랙티브 화이트보드 및 파일 공유를 지원하여 참가자가 오디오 회의 중에 보다 효율적으로 커뮤니케이션할 수 있습니다.

<img src="https://main.qcloudimg.com/raw/359a772654440bb4c1458e15989796f2.png" width="800px">


## 비디오 통화

### 그룹 비디오 통화

TRTC는 그룹 화상 통화를 지원하며 720p 및 1080p의 HD 화질을 제공합니다. 한 방에 최대 300명의 동시 온라인 사용자를 수용할 수 있으며 최대 50명의 사용자가 동시에 비디오를 켤 수 있습니다. IM, VOD, 녹화 및 음란물 감지와 같은 다양한 기능이 있어 많은 시나리오에 이상적입니다. 또한 시나리오 기반의 그룹 화상 통화 컴포넌트를 제공하여 직접 재사용하여 개발 비용을 최소화할 수 있습니다. 컴포넌트를 사용하는 방법에 대한 자세한 내용은 [영상 통화](https://intl.cloud.tencent.com/document/product/647/36065)를 참고하십시오.

<img src="https://main.qcloudimg.com/raw/15a6549e052f1df2fe2dd8373cb62a08.png" width="800px">

### 2인 비디오 통화

TRTC는 일대일 화상 통화를 지원하며 720p, 1080p의 HD 화질을 제공합니다. IM, 화면 공유, 녹화 및 인터랙티브 화이트보드와 같은 다양한 기능이 포함되어 있어 많은 사용 사례에 이상적입니다. 또한 시나리오 기반의 일대일 영상 통화 컴포넌트를 제공하여 직접 재사용하여 개발 비용을 최소화할 수 있습니다. 컴포넌트를 사용하는 방법에 대한 자세한 내용은 [영상 통화](https://intl.cloud.tencent.com/document/product/647/36065)를 참고하십시오.

<img src="https://main.qcloudimg.com/raw/2016778a35bfba78f8e06866caf62b36.png" width="800px">

### 온라인 회의

TRTC는 화면 공유, 파일 공유 및 인터랙티브 화이트보드와 같은 기능을 지원하여 온라인 회의를 보다 효율적으로 만듭니다. Tencent Cloud IM과 통합하여 회의 프로세스를 중단하지 않고 텍스트/이미지 기반 통신과 같은 다양한 토론 방법을 제공합니다. 또한 시나리오 기반의 온라인 회의 컴포넌트를 제공하므로 직접 재사용하여 개발 비용을 최소화할 수 있습니다. 컴포넌트를 사용하는 방법에 대한 자세한 내용은 [그룹 오디오/비디오 인터랙션 방](https://intl.cloud.tencent.com/document/product/647/37284)을 참고하십시오.

<img src="https://main.qcloudimg.com/raw/40a47062a2edd0a39192e0a4fc51f12a.png" width="800px">

### 온라인 의료

TRTC는 1080p FHD 이미지 품질을 지원하며 비디오 장치의 초점을 유연하게 조정할 수 있습니다. 이것은 온라인 의료 진단 및 기타 온라인 의료 서비스를 실제 병원에 가는 경험과 비교할 수 있게 합니다. 파일 공유, 화면 공유, 의료 기록 및 영상 공유를 위한 IM 등의 편리한 기능이 많아 진단의 효율성을 크게 높였습니다. 또한 다자간 화상 통화로 여러 의사와 환자가 동시에 온라인 회진에 참가할 수 있어 의료 관련 소통 및 협업이 보다 원활해집니다.

<img src="https://main.qcloudimg.com/raw/a4ef3a5089727f1cc2d5cca2b4e8f15c.png" width="800px">

### 비디오 고객 서비스

TRTC는 300ms 미만의 통화 지연, 70% 이상의 패킷 손실 방지율, 1000ms 이상의 네트워크 지터 방지 기능으로 약한 네트워크 환경에서도 원활하고 안정적인 통화를 보장합니다. 모바일 APP, PC, web 등 다양한 플랫폼 간의 상호 연결이 가능하여 언제 어디서나 영상 고객 서비스를 이용할 수 있습니다. 화상 통화를 녹음하고 재생할 수 있어 고객 서비스 품질을 크게 향상시키는 데 도움이 됩니다.

<img src="https://main.qcloudimg.com/raw/0ce02fc63807d5bd38e83b5481bb4647.png" width="800px">

### 금융 녹음 및 녹화

TRTC는 전체 통화에 걸쳐 실시간 클라우드 녹화 기능을 제공합니다. 녹화 파일 저장, 재생 및 다운로드는 물론 로컬 서버에 배포를 지원하여 비즈니스 규정 준수를 보장합니다. 또한 Tencent의 21년 데이터 보안 경험을 활용하여 최상의 데이터 보안을 보장합니다.

<img src="https://main.qcloudimg.com/raw/cba7a0e43b2268271ae267cebe834f08.png" width="800px">
