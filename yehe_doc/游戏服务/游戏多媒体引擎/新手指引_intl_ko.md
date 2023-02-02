본 문서는 GME(Game Multimedia Engine)를 시작하는 데 도움이 됩니다.
## 1. 기본 GME 지식
- [GME는 어떤 서비스를 제공합니까? 주요 기능은 무엇입니까?](https://intl.cloud.tencent.com/document/product/607/10835)
- [GME에는 어떤 장점이 있습니까?](https://intl.cloud.tencent.com/document/product/607/10837)
- [GME를 적용할 수 있는 사용 사례는 무엇인가요?](https://www.tencentcloud.com/zh/document/product/607/51558)

## 2. GME 과금 방식
GME는 현재 음성 채팅 및 음성 메시지와 같은 여러 서비스를 제공합니다. 과금 세부 정보는 [구매 가이드](https://intl.cloud.tencent.com/document/product/607/50009)를 참고하십시오.

## 3. 무료 Demo
GME를 사용하기 전에 먼저 사용해 볼 수 있습니다.

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_KuI8ov.gif"    width="37.5%"/></img>


- [기본 기능 데모](https://intl.cloud.tencent.com/document/product/607/50219): 음성 채팅, 음성 메시지, 음성 텍스트 변환, 실시간 3D 음향 효과 및 실시간 기본 음성 변조 기능
- [3D 음향 효과 데모](https://intl.cloud.tencent.com/document/product/607/50220): 실시간 3D 음향 효과 기능을 사용해 보십시오
- [고급 음성 변조 Demo](https://intl.cloud.tencent.com/document/product/607/50221): 실시간 고급 음성 변조 기능을 사용해 보십시오


## 4. 서비스 활성화
- GME를 사용하기 전에 먼저 [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985)에 가입해야 합니다.
- [GME 콘솔](https://console.cloud.tencent.com/gamegme)에서 서비스를 활성화하고 필요에 따라 기능을 활성화합니다. 자세한 내용은 [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오.

## 5. 통합 매개변수 획득

### 클라이언트 통합 매개변수


1. [GME 콘솔](https://console.cloud.tencent.com/gamegme)에서 방금 생성한 애플리케이션을 찾고 **작업** 열의 **설정**을 클릭하여 애플리케이션 설정 페이지로 이동합니다.

2. 아래와 같이 페이지에서 해당 AppID 및 권한 키를 얻을 수 있습니다.

	- Sample Project 사용 시 AppID와 권한 키가 매개변수로 필요합니다.
	- SDK 사용 시 초기화 API Init에는 AppID를 매개변수로, 로컬 인증 생성 API QAVAuthBuffer.GenAuthBuffer에는 권한 키를 매개변수로 필요로 합니다.

### TencentCloud API 통합 매개변수
TencentCloud API를 사용하는 경우 SecretId와 SecretKey가 필요하며 이는 [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 얻을 수 있습니다. [Security Best Practice](https://www.tencentcloud.com/document/product/598/10592)의 지침에 따라 계정 액세스를 관리하는 것이 좋습니다.



## 6. Sample Project 실행
GME는 다양한 플랫폼을 위한 SDK와 Sample Project를 제공합니다. SampleProject를 실행하여 GME SDK를 통합하는 방법을 더 잘 이해할 수 있습니다.
### 6.1 Sample Project 다운로드
[SDK 다운로드 가이드](https://intl.cloud.tencent.com/document/product/607/18521)의 안내에 따라 대상 플랫폼에 대한 Sample Project를 다운로드할 수 있습니다.


### 6.2 Sample Project 실행
사용하는 플랫폼에 해당하는 문서 보기:
[Quick Unreal Engine Demo Run](https://intl.cloud.tencent.com/document/product/607/46014)

## 7. 기본 기능 통합
### 7.1 SDK 다운로드
[SDK 다운로드 가이드](https://intl.cloud.tencent.com/document/product/607/18521)의 안내에 따라 대상 플랫폼에 필요한 SDK 파일을 다운로드할 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/b04f51788ab7bd527ef1662c5c5f7675.png"  width="50%"/></img>

### 7.2 프로젝트 구성
프로젝트 구성은 플랫폼별 문서를 참고하십시오. 구성이 완료된 후에야 API를 호출하여 GME 서비스를 사용할 수 있습니다.

| 플랫폼 | 구성 설명서 |
|---------|---------|
| Unity | [Integrating SDK](https://intl.cloud.tencent.com/document/product/607/10783) |
| Unreal Engine | [Integrating SDK](https://intl.cloud.tencent.com/document/product/607/44549) |
| Cocos 2D | [Project Configuration](https://intl.cloud.tencent.com/document/product/607/15216) |
| Windows | [Project Configuration](https://intl.cloud.tencent.com/document/product/607/19068) |
| Android | [Integrating SDK](https://intl.cloud.tencent.com/document/product/607/40859) |
| iOS | [Integrating SDK](https://intl.cloud.tencent.com/document/product/607/15219) |
| Mac | [Project Configuration](https://intl.cloud.tencent.com/document/product/607/18617) |
| H5 | [Project Configuration](https://intl.cloud.tencent.com/document/product/607/30261) |

### 7.3 SDK를 빠르게 통합
빠른 통합 문서는 기능을 빠르게 시험해 볼 수 있도록 통합 프로세스를 단순화합니다. 이러한 문서에 설명된 기능에는 음성 채팅 및 음성을 텍스트로 스트리밍하는 기능이 포함됩니다.

| 플랫폼 | 빠른 통합 문서 |
|---------|---------|
| Unity | [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544) |
| Unreal Engine | [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545) |
| Windows, iOS, Mac, Android | [Quick Integration of Native SDK](https://intl.cloud.tencent.com/document/product/607/40858) |



### 7.4 기본 기능 통합
사용하는 플랫폼에 해당하는 문서를 찾으려면 [여기](https://www.tencentcloud.com/document/product/607/10780)를 클릭하십시오.


### 7.5 통합 도움말 문서
사용할 수 있는 문서:

| 문서 | 사용 시기 |
|---------|---------|
| [Sound Quality](https://intl.cloud.tencent.com/document/product/607/18522) | 음성 채팅방 유형 선택이 어렵다면 이 문서를 참고하십시오. |
| [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218) | 애플리케이션의 GME 서비스와 관련된 인증 배포를 더 안전하게 하려면 이 문서를 참고하십시오. |
| [SDK Version Upgrade Guide](https://intl.cloud.tencent.com/document/product/607/32363) | 이전 GME 버전에서 새 버전으로 업그레이드하는 경우 API 변경 사항을 이해하려면 이 문서를 확인해야 합니다. |
| [에러 코드](https://intl.cloud.tencent.com/document/product/607/33223) | SDK 통합 디버깅 프로세스 중에 API 또는 콜백이 오류 코드를 반환하는 경우 이 문서를 참고하여 해결 방법을 찾으십시오. |

## 8. 고급 기능 통합


<table>
<thead>
<tr>
<th>희망 작업 유형</th>
<th>참고 자료</th>
</tr>
</thead>
<tbody>
<tr>
<td>음성 채팅에서 레인지 보이스 효과를 구현합니다(PUBG의 전체/팀 전용 오디오 모드와 유사).</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/37287" target="_blank">레인지 보이스</a></td>
</tr>
<tr>
<td>캐릭터가 움직일 때 캐릭터의 방향감이 있는 스테레오 음성을 들을 수 있습니다. 음원과의 거리가 멀어질수록 음성도 약해져서 게임 음성의 몰입도가 높아집니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18218" target="_blank">3D Sound Effect</a></td>
</tr>
<tr>
<td>방 구성원 관리, 마이크 켜기/끄기 및 음소거를 구현합니다. 예를 들어 팀 리더는 방에 있는 다른 유저를 음소거하거나 게임 호스트는 청중이 마이크를 켜기를 원합니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/51115" target="_blank">GME 채팅 방 관리 기능</a></td>
</tr>
<tr>
<td>음성 채팅방에서 GME를 이용하여 반주를 틀고, 반주의 EQ를 조절하고, 로컬 음향 효과를 재생합니다.</td>
<td ><a href="https://intl.cloud.tencent.com/document/product/607/31504" target="_blank">음성 채팅 반주</a>, <a href="https://intl.cloud.tencent.com/document/product/607/31503" target="_blank">실시간 음향 효과</a>, <a href="https://www.tencentcloud.com/document/product/607/46716" target="_blank">실시간 사운드 이퀄라이저</a></td>
</tr>
<tr>
<td>음성 채팅 중 음성 변조를 수행합니다. 유저는 ‘중년 남성’, ‘어린 소녀’ 등의 톤으로 변조할 수 있습니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/44995" target="_blank">음성 변조 효과</a></td>
</tr>
<tr>
<td>음성 채팅 방에서 현재 팀의 구성원에게만 자신의 목소리를 들려주고 일치하는 팀의 다른 낯선 유저의 목소리를 들을 수 있습니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/39525" target="_blank">사용자 지정 오디오 포워딩 라우팅</a></td>
</tr>
<tr>
<td>음성 인식을 사용하여 팀 전투에서 미성년자를 감지하여 신원 확인 및 게임 중독 방지 시스템을 우회하는 미성년자를 찾습니다.</td>
<td>미성년자 음성 인식</td>
</tr>
<tr>
<td>음성 채팅, 오디오 파일 및 음성 메시지에서 음란물, 폭력, 학대, 광고 및 기타 민감하거나 유해한 정보를 인식합니다.</td>
<td>음성 채팅 조정, 음성 메시지 조정, 타사 오디오 스트림 또는 오디오 파일 조정</td>
</tr>
<tr>
<td>플레이어의 실시간 오디오 스트림을 텍스트로 변환하여 실시간 자막을 제공합니다.</td>
<td>실시간 음성 텍스트 변환</td>
</tr>
</tbody></table>


## 9. 콘솔 운영 가이드
음성 채팅, 음성 메시지 및 기타 서비스의 사용 데이터는 [사용량 조회](https://intl.cloud.tencent.com/document/product/607/44548)를 참고하십시오.

## 10. FAQ
#### 특징
[GME 음성 채팅 이용 시 트래픽 소모량은 어떻게 되나요?](https://intl.cloud.tencent.com/document/product/607/39519)
[GME에는 어떤 기능이 있습니까?](https://intl.cloud.tencent.com/document/product/607/39520)
[GME의 음성 채팅방 또는 인원 수에 제한이 있나요?](https://intl.cloud.tencent.com/document/product/607/39523)

#### 개발
[GME는 여러 장치에서 하나의 OpenId만 사용할 수 있습니까?](https://intl.cloud.tencent.com/document/product/607/39521)
[다운로드한 Demo는 어떻게 사용합니까?](https://intl.cloud.tencent.com/document/product/607/39521)
[GME SDK를 통합하고 Apk 파일을 내보낸 후 애플리케이션을 열려고 하면 화면이 검게 변하는 경우 어떻게 해야 하나요?](https://intl.cloud.tencent.com/document/product/607/39522)
[GMESDK.framework 라이브러리를 추가한 후 Xcode에서 실행 파일을 내보내려고 할 때 컴파일 중에 오류가 발생하면 어떻게 해야 합니까?](https://intl.cloud.tencent.com/document/product/607/39522)
[GME SDK의 Poll 함수는 언제 호출해야 합니까?](https://intl.cloud.tencent.com/document/product/607/30254)



## 11. 통합

통합 중에 문제가 발생하면 다음과 같이 문제를 해결하십시오.

### 문제 확인
먼저 문제 유형을 파악한 후 해당 문서를 확인해야 합니다. [인증](https://intl.cloud.tencent.com/document/product/607/39824), [Demo](https://intl.cloud.tencent.com/document/product/607/39521), [네트워크](https://intl.cloud.tencent.com/document/product/607/39519) 또는 [프로그램 내보내기](https://intl.cloud.tencent.com/document/product/607/39522).

사용된 서비스에 따라 확인해야 하는 문제 문서를 결정할 수도 있습니다.

| 사용된 서비스  | 문서 |
|---------|---------|
| 음성 채팅 | [방 입장 실패](https://intl.cloud.tencent.com/document/product/607/39523), [사운드 및 오디오](https://intl.cloud.tencent.com/document/product/607/39524) |
| 음성 메시지 | [음성을 텍스트로 변환](https://intl.cloud.tencent.com/document/product/607/39716)|
| 음성-텍스트 | [음성을 텍스트로 변환](https://intl.cloud.tencent.com/document/product/607/39716)|

### 에러 코드
통화 오류가 발생하면 [에러 코드](https://intl.cloud.tencent.com/document/product/607/33223)를 기준으로 원인과 솔루션을 확인할 수 있습니다.

예를 들어 SDK를 사용할 때 3D 음향 효과 API가 에러 7003을 반환하면 에러 코드 문서를 확인하여 InitSpatializer가 호출되지 않은 것이 원인임을 알 수 있습니다. 그 다음 올바른 순서로 코드에서 InitSpatializer가 호출되는지 확인합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/1394eb8f4947c28728a00c873b3ecb0c.png)

### 도움 요청
문서 및 에러 코드를 통해 문제를 해결할 수 없는 경우 [문제 해결 가이드](https://www.tencentcloud.com/document/product/607/51562)의 지침에 따라 지원을 요청하십시오.


## 12. 피드백 및 제안
Tencent Cloud GME 제품 및 서비스를 사용하면서 의문점이나 제안 사항이 있는 경우 다음 채널을 통해 피드백을 제출할 수 있습니다. 전담 직원이 귀하의 문제를 해결하기 위해 연락을 드릴 것입니다.
- 링크, 콘텐츠 또는 API와 같은 제품 설명서에 대한 질문은 문서 페이지 오른쪽에 있는 **피드백 보내기**를 클릭하십시오.
- 제품 사용 중 문제가 발생하면 [온라인 고객 서비스](https://intl.cloud.tencent.com/contact-sales)에 도움을 요청하십시오.
