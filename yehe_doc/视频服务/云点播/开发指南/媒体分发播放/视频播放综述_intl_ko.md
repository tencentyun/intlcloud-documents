VOD는 업로드 및 트랜스코딩된 비디오를 재생하는 여러 방법을 지원하며 비디오 재생에는 주로 쇼트 비디오 재생, 긴 비디오 재생 및 비디오 암호화 재생과 같은 여러 시나리오로 나뉩니다.

### 쇼트 비디오 재생

쇼트 비디오는 일반적으로 다음을 포함하여 길이가 5분 미만인 동영상을 말합니다.

* 쇼트 비디오 소셜 플랫폼(예: WeSee, Kuaishou 및 TikTok)에서 공유된 비디오.
* 전자상거래 플랫폼(예: JD.com 및 Pinduoduo)에서 공유된 제품 프로모션 비디오.
* WeChat 공식 계정 및 당사 미디어에서 공유된 동영상.

<img src="https://qcloudimg.tencent-cloud.cn/raw/3a8215d3897533ec756bdd4b04e6b811.png" width="900" />


### 긴 비디오 재생

긴 비디오는 일반적으로 전문 기구에서 제작하고 주로 다음을 포함하는 비디오 웹사이트에 게시된 비디오를 나타냅니다.

* 비디오 소셜 플랫폼(예: Tencent Video, Youku 및 iQIYI)에 게시된 독점 TV 시리즈 및 버라이어티 쇼.
* 온라인 교육 웹사이트(예: Tencent Class 및 Penguin Tutoring)에 게시된 강의 동영상.
* 온라인 TV 플랫폼(CNTV 및 Mongo TV 등)에서 재생되는 TV 프로그램.

<img src="https://main.qcloudimg.com/raw/261acb48f5d44c8170d34e60bb3947c2.png" width="800" />

### 암호화된 비디오 재생

긴 비디오 재생 시나리오 중의 한 시나리오로서, 비디오 암호화는 독점 TV 시리즈 및 온라인 강의와 같은 저작권 보호 비디오의 무단 다운로드 및 배포를 방지하기 위해 암호화되는 시나리오입니다.

<img src="https://main.qcloudimg.com/raw/382d1cece21cb857c71164e905ca02d8.png" width="800" />

## 재생 아키텍처

다양한 비디오 재생 시나리오의 경우 VOD는 **Player SDK**를 사용하여 어댑티브 비트 레이트 스트리밍으로 변환된 출력 비디오를 재생하는 것이 좋습니다. 재생의 전체 아키텍처 프로세스는 다음과 같습니다.

<img src="https://main.qcloudimg.com/raw/e5ae52f1b5f15f289b6f54aa28917da4.png" width="900" />

1. **서버에서 업로드**: 비즈니스 백엔드는 콘솔, 서버 API 또는 기타 수단을 통해 비디오를 VOD에 업로드합니다.
2. **비디오 처리 트리거**: 비디오 업로드 중 어댑티브 비트 레이트 스트리밍을 지정합니다. 동영상이 업로드되면 비디오 처리가 시작됩니다.
3. **어댑티브 비트 레이트 스트리밍으로 코드 변환 및 스토리지에 쓰기**: 비디오가 어댑티브 비트 레이트 스트리밍으로 변환된 후 출력 비디오 콘텐츠가 VOD 스토리지에 기록됩니다.
4. **미디어 자산 업데이트**: 출력 비디오 정보가 미디어 자산 관리 모듈에 기록됩니다.
5. **서명 배포**: 서비스 백그라운드는 Player 서명 계산 규칙에 따라 재생 서명을 배포합니다.
6. **다운로드 주소 요청**: Player는 비디오의 FileId가 지정된 후 VOD 재생 서비스에서 비디오의 다운로드 주소를 가져옵니다.
7. **콘텐츠 다운로드**: Player는 다운로드 주소의 VOD CDN에서 콘텐츠를 다운로드합니다.
8. **재생**: Player는 출력 어댑티브 비트 레이트 스트리밍을 재생합니다.

## 가이드 문서

* 플레이어 SDK에서 지원하는 기능은 [기능 설명](https://intl.cloud.tencent.com/document/product/266/42965)을 참고하십시오. 통합 방법은 [SDK 다운로드](https://intl.cloud.tencent.com/document/product/266/43035)를 참고하십시오.
* VOD의 Player를 빠르게 통합할 수 있도록 데모를 통해 통합 단계를 설명하는 Player SDK [통합 가이드](https://intl.cloud.tencent.com/document/product/266/38098)를 제공합니다.
* 비디오 암호화 재생 시나리오의 경우, 비디오 암호화 작동 방식 및 통합 방법에 대한 자세한 내용은 [비디오 암호화 개요](https://intl.cloud.tencent.com/document/product/266/38131) 및 [4단계: 암호화된 비디오 재생](https://intl.cloud.tencent.com/document/product/266/38294)을 참고하십시오.
