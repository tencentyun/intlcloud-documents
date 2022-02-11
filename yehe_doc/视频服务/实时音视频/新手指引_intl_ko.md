## TRTC 빠르게 이해하기

- [플랫폼 지원](https://intl.cloud.tencent.com/document/product/647/35078)
- [기능 지원](https://intl.cloud.tencent.com/document/product/647/35428)
- [적용 시나리오](https://intl.cloud.tencent.com/document/product/647/37713)
- [기본 개념](https://intl.cloud.tencent.com/document/product/647/37714)

[](id:pay)
## 과금 방식

TRTC 서비스 항목은 서비스 유형에 따라 크게 **기본 서비스**와 **부가 서비스**로 나뉩니다. 

<table>
<tr><th>서비스 유형</th><th>적용 시나리오</th><th>과금 설명</th></tr>
<tr>
<td rowspan="4">기본 서비스</td>
<td>음성 ILVB</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34610">음성 ILVB 과금 설명</a></td>
</tr><tr>
<td>비디오 ILVB</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34610">비디오 ILVB 과금 설명</a></td>
</tr><tr>
<td>음성 통화</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34610">음성 통화 과금 설명</a></td>
</tr><tr>
<td>영상 통화</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34610">영상 통화 과금 설명</a></td>
</tr><tr>
<td rowspan="2">부가 서비스</td>
<td>클라우드 녹화</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38385">클라우드 녹화 과금 설명</a></td>
</tr><tr>
<td>클라우드 혼합 스트림 트랜스 코딩</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38929">클라우드 혼합 스트림 트랜스 코딩 과금 설명</a></td>
</tr>
</table>




## 개발 지원
[](id:demo)
### Demo 체험

TRTC는 **iOS**, **Android**, **Mac OS**, **Windows**, **데스크톱 브라우저**, **Electron**, **Flutter**의 체험 Demo를 제공합니다. 자세한 내용은 [Demo 체험](https://intl.cloud.tencent.com/document/product/647/35076)을 참조하십시오.

[](id:sdk)
### SDK 다운로드

TRTC는 Tencent Cloud의 LiteAV 시리즈 제품 중 하나입니다. LiteAV 시스템의 SDK는 모두 동일한 기본 모듈을 사용하기 때문에 프로젝트 중 동시에 두 개 이상의 LiteAV 시스템 SDK를 통합하게 되면 부호 충돌(symbol duplicate) 문제가 발생할 수 있습니다. 따라서 다양한 제품의 기능이 통합된 **라이트 버전(TRTC)**, **프로 버전(Professional)** 및 **엔터프라이즈 버전(Enterprise)**이 제공되며, 실제 비즈니스 수요에 따라 버전을 선택할 수 있습니다.

| 버전 유형                                                     | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [라이트 버전(TRTC)](https://intl.cloud.tencent.com/document/product/647/34615) | TRTC와 라이브 방송 재생(TXLivePlayer) 기능만 제공하며, App 설치 패키지 용량 증분이 가장 적어 TRTC 관련 기능만 사용하는 사용자에게 적합합니다. |
| [프로 버전(Professional)](https://intl.cloud.tencent.com/document/product/647/34615) | TRTC를 비롯한 [MLVB](https://intl.cloud.tencent.com/product/mlvb), [UGSV](https://intl.cloud.tencent.com/product/ugsv) 등의 다양한 멀티미디어 관련 핵심 기능을 포함하고 있습니다. 하위 레이어 모듈을 효율적으로 재사용하여 통합 프로 버전의 증분 용량이 독립적인 SDK 2개를 통합한 용량보다 작고, 부호 충돌(symbol duplicate) 문제를 방지할 수 있습니다. |
| [엔터프라이즈 버전(Enterprise)](https://intl.cloud.tencent.com/document/product/647/34615) | 프로 버전의 모든 기능을 포함하고 있으며, AI 뷰티 필터 특수 효과 모듈(부가 서비스)을 통합하여 눈 크게, 얼굴 갸름하게, 메이크업, 움직이는 스티커, 액세서리 등 AI 뷰티 필터 특수 효과 기능을 지원합니다. |

> ? 버전별 차이점 비교는 [SDK 다운로드](https://intl.cloud.tencent.com/document/product/647/34615)를 참조하십시오.


[](id:api)
### API 통합

- **클라이언트 API:** SDK 인터페이스 호출을 통한 기능 통합을 지원합니다. 지원 가능한 플랫폼으로는 [iOS](https://intl.cloud.tencent.com/document/product/647/35119), [Mac](https://intl.cloud.tencent.com/document/product/647/35119), [Android](https://intl.cloud.tencent.com/document/product/647/35125), [Windows(C++)](https://intl.cloud.tencent.com/document/product/647/35131), [Unity](https://intl.cloud.tencent.com/document/product/647/40139), [데스크톱 브라우저](https://intl.cloud.tencent.com/document/product/647/35143), [Electron](https://intl.cloud.tencent.com/document/product/647/35141), [Flutter](https://intl.cloud.tencent.com/document/product/647/39169)가 있습니다.
- **서버 API:** API 3.0 인터페이스 호출을 통해 [통화 품질 모니터링](https://intl.cloud.tencent.com/document/product/647/36754), [혼합 스트림 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/37760), [방 관리](https://intl.cloud.tencent.com/document/product/647/34268) 기능을 통합할 수 있습니다.



## 신규 사용자 시작하기
[](id:demo_guide)
### 1분 만에 Demo 실행하기

TRTC 콘솔에서는 플랫폼별 Demo 소스 코드를 제공합니다. 자세한 실행 방법은 다음을 참조하십시오.

| 플랫폼       | 관련 문서                                                     |
| ---------- | ------------------------------------------------------------ |
| iOS 및 Mac    | [Demo 실행(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35086) |
| Android    | [Demo 실행(Android)](https://intl.cloud.tencent.com/document/product/647/35084) |
| Windows    | [Demo 실행(Windows)](https://intl.cloud.tencent.com/document/product/647/35085) |
| Web | [Demo 실행(Web)](https://intl.cloud.tencent.com/document/product/647/35607) |
| Electron   | [Demo 실행(Electron)](https://intl.cloud.tencent.com/document/product/647/35089) |
| Flutter | [Demo 실행(Flutter)](https://intl.cloud.tencent.com/document/product/647/39243) |

[](id:sdk_guide)
### 1분 만에 SDK 통합하기

SDK 다운로드 완료 후, 다음 방법을 통해 TRTC SDK를 프로젝트에 빠르게 통합할 수 있습니다.

| 플랫폼       | 관련 문서                                                     |
| ---------- | ------------------------------------------------------------ |
| iOS        | [빠른 통합(iOS)](https://intl.cloud.tencent.com/document/product/647/35092) |
| Mac        | [빠른 통합(Mac)](https://intl.cloud.tencent.com/document/product/647/35094) |
| Android    | [빠른 통합(Android)](https://intl.cloud.tencent.com/document/product/647/35093) |
| Windows    | [빠른 통합(Windows)](https://intl.cloud.tencent.com/document/product/647/35095) |
|Web | [빠른 통합(Web)](https://intl.cloud.tencent.com/document/product/647/35096) |
| Electron   | [빠른 통합(Electron)](https://intl.cloud.tencent.com/document/product/647/35097) |
| Flutter | [빠른 통합(Flutter)](https://intl.cloud.tencent.com/document/product/647/35098) |

[](id:web_guide)
### 1분 만에 Web 라이브 방송 인터랙션 모듈 실행하기

TRTC는 완벽한 Web 라이브 방송 인터랙션 모듈 체험 Demo를 제공합니다. 자세한 통합 방법은 [1분 만에 Web 라이브 방송 인터랙션 모듈 실행하기](https://intl.cloud.tencent.com/document/product/647/38172)를 참조하십시오.

[](id:sence)
## 시나리오 사례

TRTC는 기타 Tencent Cloud 제품과 결합해 다양한 라이브 방송 시나리오 유형의 체험 Demo를 제공합니다.

<table>
<tr><th width="17%">시나리오 유형</th><th>기능 지원</th><th width="20%">참조</th>
</tr><tr>
<td>그룹 영상 통화</td>
<td>인터랙션 마이크 연결, 오프라인 수신 등 관련 기능 포함</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/36065" target="_blank">실시간 영상 통화</a></td>
</tr><tr>
<td>그룹 음성 통화</td>
<td>인터랙션 마이크 연결, 오프라인 수신 등 관련 기능 포함</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/36067" target="_blank">실시간 음성 통화</a></td>
</tr><tr>
<td>ILVB</td>
<td>인터랙션 마이크 연결, 호스트 PK, 저 딜레이 시청, 댓글 자막 채팅 등 관련 기능 포함</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/36060" target="_blank">비디오 ILVB</a></td>
</tr><tr>
<td>실시간 인터랙션 수업</td>
<td>음성, 비디오, 화면 공유 등의 수업 방식을 포함하며, 교사 문답 시작, 학생 손 들기, 학생에게 답변 요청, 답변 완료 등 관련 기능 캡슐화</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/37278" target="_blank">실시간 인터랙션 수업</a></td>
</tr><tr>
<td>그룹 화상 회의</td>
<td>화면 공유, 뷰티 필터, 저 딜레이 회의 등 관련 기능 포함</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/37284" target="_blank">그룹 화상 회의</a></td>
</tr><tr>
<td>음성 채팅방</td>
<td>마이크 위치 관리, 저 딜레이 음성 인터랙션, 문자 채팅 등 관련 기능 포함</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/37287" target="_blank">음성 채팅방</a></td>
</tr></table>

[](id:console)
## 콘솔 체험
| 콘솔 사용                                         | 참조                                                   |
| :--------------------------------------------------------- | :----------------------------------------------------------- |
| TRTC 사용 시 발생하는 **멀티미디어 인터랙션**과 **클라우드 녹화**사용량 데이터 조회 | [사용량 통계](https://intl.cloud.tencent.com/document/product/647/39066) |
| 모니터링 대시보드 기능으로 애플리케이션 룸의 통화 품질 자세히 알아보기               | [모니터링 대시보드](https://intl.cloud.tencent.com/document/product/647/39069) |
| Demo 애플리케이션 생성 및 다운로드, 베타 Demo 빠른 실행 가능                       | [Demo 빠른 실행](https://intl.cloud.tencent.com/document/product/647/39073) |
| 온라인에서 UserSig 서명을 생성하거나 기존 UserSig의 유효 여부 검증         | [UserSig 생성 및 인증](https://intl.cloud.tencent.com/document/product/647/39074)                |
| 신규 애플리케이션 생성 | [애플리케이션 생성](https://intl.cloud.tencent.com/document/product/647/39077) |
| 애플리케이션에 릴레이 푸시 스트림 또는 클라우드 녹화, 고급 권한 제어 기능 활성화         | [기능 설정](https://intl.cloud.tencent.com/document/product/647/39080) |
| 클라우드 혼합 스트림 트랜스 코딩 시 필요한 사용자 정의 배경 이미지 리소스 추가           | [리소스 관리](https://intl.cloud.tencent.com/document/product/647/39081) |
| 실제 비즈니스 수요와 결합된 콜백 키와 콜백 주소 설정 | [콜백 설정](https://intl.cloud.tencent.com/document/product/647/39559) |



[](id:faq)
## 신규 사용자 FAQ

-  [클라이언트 Native SDK에 어떤 포트 또는 도메인을 화이트리스트로 설정해야 하나요?](https://intl.cloud.tencent.com/document/product/647/35164)
-  [iOS/Android 설치 패키지 용량은 어떻게 줄이나요?](https://intl.cloud.tencent.com/document/product/647/35165)
-  [UserSig 키는 어떻게 획득하나요?](https://intl.cloud.tencent.com/document/product/647/35166)
-  [TRTC 라이트 버전, 프로 버전, 엔터프라이즈 버전의 차이점은 무엇인가요?](https://intl.cloud.tencent.com/document/product/647/36057) 
-  [TRTC RoomID란 무엇이며, 값의 범위는 어떻게 되나요?](https://intl.cloud.tencent.com/document/product/647/36057) 
-  [Android 및 Web 통신을 지원하나요?](https://intl.cloud.tencent.com/document/product/647/37341) 
-  [데스크톱 브라우저 SDK에서 지원하는 브라우저에는 어떤 것이 있나요?](https://intl.cloud.tencent.com/document/product/647/37340) 

> ? 기타 다른 문의사항은 [FAQ](https://intl.cloud.tencent.com/document/product/647/36058) 문서를 참조하십시오.


## 피드백 및 의견

Tencent Cloud TRTC 제품 및 서비스 사용에 대한 문의사항 또는 의견이 있는 경우, 다음 방법을 통해 피드백을 보낼 수 있습니다.

- 링크, 콘텐츠 등 제품 문서에 문제가 발생한 경우, 문서 페이지 오른쪽 [문서 피드백]을 클릭하거나 문제가 있는 내용을 선택하여 피드백을 보낼 수 있습니다.
- 제품 관련 문제가 발생한 경우, [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category?level1_id=29&level2_id=801&source=14&data_title=Tencent%20Real%20Time%20Communication&step=1)을 통해 도움을 요청할 수 있습니다.
