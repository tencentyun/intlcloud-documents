본 문서는 GME(Game Multimedia Engine)를 시작하는 데 도움이 됩니다.

## 1. 기본 GME 지식

- [GME는 어떤 서비스를 제공합니까?](https://intl.cloud.tencent.com/document/product/607/10835)
- [GME에는 어떤 장점이 있습니까?](https://intl.cloud.tencent.com/document/product/607/10837)
- [Use Cases](https://intl.cloud.tencent.com/document/product/607/10838)
- [Glossary](https://intl.cloud.tencent.com/document/product/607/30259)

## 2. GME 과금 방식

GME는 현재 음성 채팅, 음성 메시지 및 음성-텍스트 변환 기능과 같은 여러 서비스를 제공합니다. 과금에 대한 자세한 내용은 [Pay-as-You-Go Billing Mode](https://intl.cloud.tencent.com/document/product/607/36276)를 참고하십시오.

## 3. 무료 Demo

[Free Demo](https://intl.cloud.tencent.com/document/product/607/38535)에서 QR 코드를 스캔하여 모바일 애플리케이션을 다운로드하거나 Windows 플랫폼용 실행 프로그램을 다운로드하여 3D 음향 효과를 경험할 수 있습니다.

## 4. 신규 사용자

#### 4.1 서비스 활성화

GME를 사용하기 전에 [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985)하고 GME 서비스를 활성화해야 합니다. 자세한 내용은 [Voice Service Activation Guide](https://intl.cloud.tencent.com/document/product/607/39698)를 참고하십시오.

#### 4.2 액세스 매개변수 가져오기

GME 서비스 활성화 후 생성된 애플리케이션의 상세 페이지에서 AppID와 권한 키를 확인할 수 있습니다.
- AppID 및 권한 키는 Demo 사용 시 매개변수로 입력해야 합니다.
- SDK 사용 시 초기화 API Init는 AppID를 매개변수로 사용해야 합니다. 인증 API QAVAuthBuffer.GenAuthBuffer(음성 채팅) 및 ApplyPTTAuthbuffer(음성-텍스트 변환)는 모두 권한 키가 매개변수로 필요합니다.

![](https://main.qcloudimg.com/raw/a63f14a7092169c8c9b54cfd21ce4c12.png)
#### 4.3 SDK 다운로드

다양한 플랫폼용 GME SDK를 다운로드할 수 있습니다. 자세한 내용은 [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521)를 참고하십시오. **현재 GME는 Windows, Mac, Android 및 iOS를 지원하며 GSE는 UnrealEngine4, Unity3D 및 Cocos2DX를 지원합니다**.

현재 GME는 H5에서 실시간 음성 통화를 지원합니다.

#### 4.4 SDK 액세스
각 플랫폼의 SDK에 액세스하려면 각 플랫폼의 [Project Configuration](https://intl.cloud.tencent.com/document/product/607/10783) 문서를 참고하여 프로젝트를 구성한 후 해당 플랫폼의 [API Documentation](https://intl.cloud.tencent.com/document/product/607/15228)을 확인하여 API를 호출하여 GME 서비스를 이용할 수 있습니다. 음성 채팅 API의 호출 순서는 [Init API(초기화용)]>[Poll API(콜백 트리거용)]>[EnterRoom API(음성 채팅방 입장용)]>[EnableMic API(마이크 활성화용)]>[EnableSpeaker API(스피커 활성화용)]>[ExitRoom API(방 퇴장용)]>[Unit API(초기화 취소용)]입니다.

**음성 채팅의 방 입장 과정은 다음과 같습니다.**
<img src="https://main.qcloudimg.com/raw/d23fd88b9d0ff2f044f7549168be9d79.png"  width="60%" /></img>

## 5. 콘솔 사용 가이드
음성 채팅, 음성 메시지 및 음성 분석의 백그라운드 데이터는 [Operation Guide](https://intl.cloud.tencent.com/document/product/607/17448)를 참고하십시오.

## 6. 문서 설명

<table>
<thead>
<tr>
<th>희망 작업 유형</th>
<th>참고 자료</th>
</tr>
</thead>
<tbody><tr>
<td>SDK 파일을 다운로드합니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18521" target="_blank">SDK Download Guide</a></td>
</tr>
<tr>
<td>QR 코드를 스캔하여 애플리케이션을 다운로드하고 GME를 사용해 보십시오.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/38535" target="_blank">Free Demo</a></td>
</tr>
<tr>
<td>프로젝트에 SDK에 액세스하여 프로젝트에서 SDK를 내보낼 때 필요한 구성을 확인합니다. (Unity 플랫폼을 예로 듦)</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/10783" target="_blank">Unity Project Configuration</a></td>
</tr>
<tr>
<td>SDK에 액세스하여 프로젝트에 모든 API를 확인하고 음성 채팅 및 음성-텍스트 변환 서비스를 구현합니다. (Unity 플랫폼을 예로 듦)</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/15228" target="_blank">Unity API 문서</a></td>
</tr>
<tr>
<td>프로젝트에 대한 SDK에 액세스하고 음성 채팅 서비스에 빠르게 액세스합니다. (Unity 플랫폼을 예로 듦)</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18248" target="_blank">Unity Getting Started</a></td>
</tr>
<tr>
<td>음성 채팅에서 레인지 보이스 효과를 구현합니다(PUBG의 전체/팀 전용 오디오 모드와 유사).</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/37287" target="_blank">레인지 보이스</a></td>
</tr>
<tr>
<td>게임에서 3D 실시간 음향 효과를 구현합니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18218" target="_blank">3D Sound Effect</a></td>
</tr>
<tr>
<td>GME를 사용하여 음성 채팅 방에서 반주를 재생합니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/31504" target="_blank">Accompaniment in Voice Chat</a></td>
</tr>
<tr>
<td>음성 채팅 서비스의 다양한 방 유형의 차이점에 대해 알아보십시오.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18522" target="_blank">Sound Quality</a></td>
</tr>
<tr>
<td>인증 및 백엔드 배포 스키마에 대해 자세히 알아보십시오.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/12218" target="_blank">Authentication Key</a></td>
</tr>
<tr>
<td>SDK 사용 시 발생하는 오류 코드를 분석하고 솔루션을 쿼리합니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/33223" target="_blank">Error Codes</a></td>
</tr>
<tr>
<td>GME의 제품 FAQ에 대해 알아보십시오.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/30254" target="_blank">일반 FAQ</a></td>
</tr>
<tr>
<td>서비스를 구매하기 전에 과금 규정을 확인하십시오.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/30255" target="_blank">Billing</a></td>
</tr>
<tr>
<td>음성 채팅방 FAQ를 확인하십시오.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/35611" target="_blank">Room Entering Failed</a></td>
</tr>
<tr>
<td>SDK 사용 중의 오디오 관련 문제에 대한 해결 방법을 확인하십시오.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/30257" target="_blank">Sound and Audio</a></td>
</tr>
</tbody></table>


## 7. 신규 사용자 FAQ
#### 컨설팅
[GME 음성 채팅 이용 시 트래픽 소모량은 어떻게 되나요?](https://intl.cloud.tencent.com/document/product/607/39519)
[GME에는 어떤 기능이 있습니까?](https://intl.cloud.tencent.com/document/product/607/39520)


#### Demo
[GME는 여러 장치에서 하나의 OpenId만 사용할 수 있습니까?](https://intl.cloud.tencent.com/document/product/607/30256)
[다운로드한 Demo는 어떻게 사용합니까?](https://intl.cloud.tencent.com/document/product/607/30256)
[로그는 어떻게 얻나요?](https://intl.cloud.tencent.com/document/product/607/39521)
[GME SDK를 통합하고 Apk 파일을 내보낸 후 애플리케이션을 열려고 하면 화면이 검게 변하는 경우 어떻게 해야 하나요?](https://intl.cloud.tencent.com/document/product/607/39522)
[GMESDK.framework 라이브러리를 추가한 후 Xcode에서 실행 파일을 내보내려고 할 때 컴파일 중에 오류가 발생하면 어떻게 해야 합니까?](https://intl.cloud.tencent.com/document/product/607/39522)


#### 음성 채팅
[GME SDK의 Poll 함수는 언제 호출해야 합니까?](https://intl.cloud.tencent.com/document/product/607/30254)
[GME의 음성 채팅방 또는 인원 수에 제한이 있나요?](https://intl.cloud.tencent.com/document/product/607/35611)
[EnterRoom API를 호출할 때 0이 반환되어도 방 입장이 실패하는 이유는 무엇입니까?](https://intl.cloud.tencent.com/document/product/607/39523)
[네트워크 문제는 어떻게 해결합니까?](https://intl.cloud.tencent.com/document/product/607/39519)
[클라이언트가 음성 채팅방에서 연결이 끊긴 경우 어떻게 해야 합니까?](https://intl.cloud.tencent.com/document/product/607/35611)
[일반적으로 레인지 보이스를 사용할 수 있지만 감쇠 효과가 없습니다. 3D 효과음 파일을 설정했는데 반환 값은 여전히 0입니다. 왜 이런 일이 발생합니까?](https://intl.cloud.tencent.com/document/product/607/39523)
[방에 입장한 후 휴대폰 볼륨이 매우 낮아졌다가 마이크가 켜진 후 볼륨이 너무 높아지면 어떻게 해야 합니까?](https://intl.cloud.tencent.com/document/product/607/39524)
[Android에서 마이크를 활성화한 후 스피커 대신 리시버에서 소리가 나면 어떻게 해야 하나요?](https://intl.cloud.tencent.com/document/product/607/30257)

## 8. 피드백 및 제안
Tencent Cloud GME 제품 및 서비스를 사용하면서 의문점이나 제안 사항이 있는 경우 다음 채널을 통해 피드백을 제출할 수 있습니다. 전담 직원이 귀하의 문제를 해결하기 위해 연락을 드릴 것입니다.
- 링크, 콘텐츠, API 오류 등 제품 문서에 문제가 발생하는 경우 문서 페이지 오른쪽 [피드백 보내기]를 클릭하여 문제가 있는 내용을 선택하여 피드백을 보낼 수 있습니다.
- 제품 관련 문제가 발생하는 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 도움을 요청할 수 있습니다.

>? 티켓 제출 시 SDK 버전 및 사용 플랫폼 정보를 제공해 주시기 바랍니다.
