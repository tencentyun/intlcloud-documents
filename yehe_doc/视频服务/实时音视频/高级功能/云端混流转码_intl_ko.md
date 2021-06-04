## 적용 시나리오

[CDN 라이브 방송 시청](https://intl.cloud.tencent.com/document/product/647/35242)과 [클라우드 녹화 재생](https://intl.cloud.tencent.com/document/product/647/35426) 등의 응용 시나리오에서는 TRTC 방 안에 있는 여러 채널의 멀티미디어 스트림을 한 채널의 스트림으로 혼합하는 기능이 주로 필요하며, Tencent Cloud의 서버인 MCU의 혼합 스트림 트랜스 코딩 클러스터를 이용해 해당 작업을 완료할 수 있습니다. MCU 클러스터는 여러 채널의 멀티미디어 스트림을 필요에 따라 혼합하여 최종적으로 생성한 비디오 스트림을 라이브 방송 CDN과 클라우드 녹화 시스템으로 배포합니다.

클라우드 혼합 스트림에 대한 2가지 제어 방법:

- **방법1**: 서버의 REST 인터페이스 StartMCUMixTranscode([숫자 방 번호 버전](https://intl.cloud.tencent.com/document/product/647/37761) / [문자열 방 번호 버전](https://intl.cloud.tencent.com/document/product/647/39637)) 및 StopMCUMixTranscode([숫자 방 번호 버전](https://intl.cloud.tencent.com/document/product/647/37760) / [문자열 방 번호 버전](https://intl.cloud.tencent.com/document/product/647/39636)을 사용해 제어합니다. 해당 인터페이스는 CDN 시청 및 클라우드 녹화 실행도 지원합니다.
- **방법2**: 클라이언트 TRTC SDK의 [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) 인터페이스를 사용해 제어하며, 원리는 다음 이미지와 같습니다. 
  ![](https://main.qcloudimg.com/raw/fd3017e7eb263b538fba858a362eab13.png)

>! 방법2는 iOS, Android, Windows, Mac, Electron, Flutter, 데스크톱 브라우저 플랫폼의 SDK를 지원합니다.

## 원리 분석

클라우드 혼합 스트림에는 디코딩, 혼합, 인코딩 세 가지 프로세스가 포함되어 있습니다.

- **디코딩**: MCU는 비디오 디코딩 및 오디오 디코딩을 포함한 여러 채널의 멀티미디어 스트림을 디코딩합니다.
- **혼합**: MCU는 여러 채널의 화면을 하나의 화면으로 혼합하고, SDK의 혼합 스트림 명령에 따라 구체적인 레이아웃을 구현합니다. 또한 디코딩된 여러 채널의 오디오 신호를 혼합 처리합니다.
- **인코딩**: MCU는 혼합된 화면과 오디오를 2차로 인코딩하고 한 채널의 멀티미디어 스트림으로 캡슐화해 다운 스트림 시스템(예: 라이브 방송 및 녹화)으로 전송합니다.

![](https://main.qcloudimg.com/raw/fd3017e7eb263b538fba858a362eab13.png)

[](id:restapi)

## 방법1: 서버의 REST API로 스트림을 혼합하는 방법

### 혼합 스트림 실행

서버에서 REST API [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761)를 호출하여 클라우드 혼합 스트림을 실행할 수 있으며, 해당 API는 다음과 같은 세부 사항에 주의해야 합니다.

[](id:restapi_step1)

#### 1단계: 화면 레이아웃 모드 설정(필수)
`StartMCUMixTranscode`의 [LayoutParams](https://intl.cloud.tencent.com/ko/document/product/647/36760#LayoutParams) 매개변수를 통해 다음 몇 가지의 레이아웃 모드를 설정할 수 있습니다.
![](https://main.qcloudimg.com/raw/be0205b5f624679302e57ca5aa1b133f.png)

**플로팅 템플릿(LayoutParams.Template = 0)**

- 첫 번째로 방에 입장한 사용자의 비디오 화면이 전체 화면에 채워지며, 다른 사용자의 비디오 화면은 왼쪽 하단부터 순서대로 수평으로 나열되어 작은 화면으로 표시됩니다.
- 최대 4개 행까지 행별로 4개 화면이 표시되며, 작은 화면이 큰 화면 위에 플로팅됩니다.
- 최대 큰 화면 1개, 작은 화면 15개까지 지원합니다.
- 사용자가 오디오만 전송하는 경우에도 화면을 차지합니다.

**격자 템플릿(LayoutParams.Template = 1)**

- 모든 사용자의 비디오 화면 크기가 동일하며, 전체 화면을 동일하게 나눕니다. 사람이 많을수록 각 화면이 작아집니다.
- 최대 16개 화면까지 지원하며, 사용자가 오디오만 전송하는 경우에도 화면을 차지합니다.

**화면 공유 템플릿(LayoutParams.Template = 2)**

- 화상 회의 및 온라인 교육 시나리오 레이아웃에 적합합니다.
- 공유 화면(또는 호스트의 카메라)이 계속 화면 왼쪽의 큰 화면 위치를 차지하며, 다른 사용자들은 오른쪽에 수직으로 나열됩니다.
- `LayoutParams.MainVideoUserId`와 `LayoutParams.MainVideoStreamType` 매개변수를 통해 왼쪽 메인 화면의 콘텐츠를 지정해야 합니다.
- 최대 2개 열까지 열별로 8개의 작은 화면이 표시됩니다. 최대 큰 화면 1개, 작은 화면 15개까지 지원합니다.
- 사용자가 오디오만 전송하는 경우에도 화면을 차지합니다.

**화면 안의 화면 템플릿(LayoutParams.Template = 3)**

- 해당 템플릿은 '큰 화면 1개와 작은 화면 1개, 앞뒤 배열' 모드로 방 안에 있는 두 개 채널의 화면을 혼합합니다. 한 채널의 화면을 전체 화면으로 하고, 다른 채널의 화면을 작은 화면으로 하여 큰 화면 위에 플로팅합니다. 플로팅 위치는 매개변수를 통해 지정할 수 있습니다.
- `LayoutParams`의 `MainVideoUserId`와 `MainVideoStreamType` 매개변수를 통해 큰 화면을 사용할 채널의 사용자 ID와 스트림 유형을 지정할 수 있습니다.
- `LayoutParams`의 `SmallVideoLayoutParams` 매개변수를 통해 작은 화면을 사용할 채널의 사용자 ID와 스트림 유형, 레이아웃 위치 등의 정보를 지정할 수 있습니다.
- 시나리오 예시1: 온라인 교육 시나리오에서 교사 측 카메라(일반적으로 작은 화면)와 교사 측 화면(일반적으로 큰 화면)을 혼합하고, 여기에 수업 중인 학생들의 오디오를 혼합합니다.
- 시나리오 예시2: 1대1 영상 통화 시나리오에서 원격 사용자 화면(일반적으로 큰 화면)과 로컬 사용자 화면(일반적으로 작은 화면)을 혼합합니다.

**사용자 정의 템플릿(LayoutParams.Template = 4)**

- 각 채널 화면의 위치 레이아웃을 사용자 정의해야 하는 시나리오에 적용됩니다. `LayoutParams`의 `PresetLayoutConfig` 매개변수(하나의 배열)를 통해 사전에 각 채널 화면의 위치를 설정할 수 있습니다.
- `PresetLayoutConfig` 매개변수 중 `UserId` 매개변수는 지정하지 않아도 됩니다. 레이아웃 엔진이 방에 입장하는 순서에 따라 방 안에 있는 사용자를 `PresetLayoutConfig` 배열에서 지정한 각 위치에 순차적으로 할당합니다.
- `PresetLayoutConfig` 배열 중 하나가 `UserId` 매개변수로 지정되는 경우, 레이아웃 엔진은 먼저 지정된 사용자를 위해 화면 상의 위치를 남겨 놓습니다.
- 사용자가 오디오만 업스트림하고 비디오는 업스트림하지 않는 경우에도 화면을 차지합니다.
- `PresetLayoutConfig` 배열에서 사전에 설정한 위치에 사용자가 모두 들어오면 레이아웃 엔진은 다른 사용자의 화면 및 오디오는 혼합하지 않습니다.

>! 클라우드 혼합 스트림 서비스는 동시에 최대 16개 채널의 멀티미디어 스트림을 혼합할 수 있습니다. 사용자에게 오디오 스트림만 있어도 한 개 채널의 스트림으로 간주합니다.

[](id:restapi_step2)
#### 2단계: 혼합 스트림 인코딩 매개변수 설정(필수)
`StartMCUMixTranscode`의 [EncodeParams](https://intl.cloud.tencent.com/ko/document/product/647/36760#EncodeParams) 매개변수를 통해 혼합 스트림 인코딩 매개변수를 설정할 수 있습니다.

| 이름            | 설명                                         | 권장 값 |
| --------------- | -------------------------------------------- | ------ |
| AudioSampleRate | 혼합 스트림-출력 스트림의 오디오 샘플링 레이트                        | 48000  |
| AudioBitrate    | 혼합 스트림-출력 스트림의 오디오 비트 레이트, 단위: kbps               | 64     |
| AudioChannels   | 혼합 스트림-출력 스트림의 오디오 사운드 채널 수                        | 2      |
| VideoWidth      | 혼합 스트림-출력 스트림의 너비, 멀티미디어 출력 시 필수 입력 사항              | 사용자 정의 |
| VideoHeight     | 혼합 스트림-출력 스트림의 높이, 멀티미디어 출력 시 필수 입력 사항              | 사용자 정의 |
| VideoBitrate    | 혼합 스트림-출력 스트림의 비트 레이트, 단위: kbps, 멀티미디어 출력 시 필수 입력 사항 | 사용자 정의 |
| VideoFramerate  | 혼합 스트림-출력 스트림의 프레임 레이트, 멀티미디어 출력 시 필수 입력 사항            | 15     |
| VideoGop        | 혼합 스트림-출력 스트림의 GOP, 멀티미디어 출력 시 필수 입력 사항            | 3      |
| BackgroundColor | 혼합 스트림-출력 스트림의 배경색                            | 사용자 정의 |

[](id:restapi_step4)
#### 3단계: 혼합 후의 streamID 지정(필수)
- **OutputParams.StreamId**
  해당 매개변수를 통해 혼합 멀티미디어 스트림의 라이브 방송 CDN에서의 streamID를 지정할 수 있습니다. 단, 라이브 방송 서비스를 활성화하고 재생 도메인을 설정한 경우에만 CDN을 통해 해당 라이브 방송 스트림을 정상적으로 시청할 수 있습니다.
- **OutputParams.PureAudioStream**
  퓨어 오디오 라이브 방송을 원하는 경우 `OutputParams.PureAudioStream` 매개변수를 1로 설정할 수 있습니다. 이는 혼합 스트림 후의 오디오 데이터 스트림만 CDN으로 전달한다는 의미입니다.

[](id:restapi_step3)
#### 4단계: 클라우드 녹화 활성화 여부 설정(옵션)
- **OutputParams.RecordId**
  해당 매개변수는 [클라우드 녹화](https://intl.cloud.tencent.com/document/product/647/35426) 실행 여부를 지정하는 데 사용되며, 해당 매개변수를 지정하는 경우 혼합 스트림한 멀티미디어 스트림을 파일로 녹화한 후 [VOD](https://intl.cloud.tencent.com/ko/product/vod)에 저장합니다. 녹화한 파일은 `OutputParams.RecordId_시작 시간_종료 시간` 포맷으로 이름이 생성됩니다(예: `file001_2020-02-16-12-12-12_2020-02-16-13-13-13`).
- **OutputParams.RecordAudioOnly**
  오디오 녹음만 필요하고 비디오 콘텐츠는 필요 없는 경우 `OutputParams.RecordAudioOnly` 매개변수를 1로 설정할 수 있습니다. MP3 포맷의 파일로만 녹음한다는 의미입니다.

### 혼합 스트림 종료

서버에서 REST API [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)를 호출하여 혼합 스트림을 종료할 수 있습니다.

[](id:sdkapi)

## 방법2: 클라이언트 SDK API로 스트림을 혼합하는 방법

TRTC SDK를 사용한 혼합 스트림 명령은 매우 간단합니다. 각 플랫폼의 [setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) API를 호출하기만 하면 되며, 현재 SDK에서는 4가지의 주요 혼합 스트림 방법을 제공합니다.

<table>
<thead><tr><th>매개변수 항목</th>
<th width="10%">퓨어 오디오 모드(PureAudio)</th>
<th width="10%">프리셋 레이아웃 모드(PresetLayout)</th>
<th width="10%">화면 공유 모드(ScreenSharing)</th>
<th>매뉴얼 모드(Manual)</th>
</tr></thead>
<tbody><tr>
<td>호출 횟수</td>
<td>인터페이스 1회만 호출</td>
<td>인터페이스 1회만 호출</td>
<td>인터페이스 1회만 호출</td>
<td>다음 시나리오에서 혼합 스트림 인터페이스 호출이 필요합니다.<li>마이크가 연결된 사용자가 입장하는 경우</li><li>마이크가 연결된 사용자가 퇴장하는 경우</li><li>마이크가 연결된 사용자가 카메라를 끄거나 켠 경우</li><li>마이크가 연결된 사용자가 마이크를 끄거나 켠 경우</li></td>
</tr><tr>
<td>콘텐츠 혼합</td>
<td>오디오만 혼합</td>
<td>각 채널 콘텐츠 사용자 정의 설정</td>
<td>학생 측 화면 혼합하지 않음</td>
<td>각 채널 콘텐츠 사용자 정의 설정</td>
</tr><tr>
<td>audioSampleRate</td>
<td>48000 권장</td>
<td>48000 권장</td>
<td>48000 권장</td>
<td>48000 권장</td>
</tr><tr>
<td>audioBitrate</td>
<td>64 권장</td>
<td>64 권장</td>
<td>64 권장</td>
<td>64 권장</td>
</tr><tr>
<td>audioChannels</td>
<td>2 권장</td>
<td>2 권장</td>
<td>2 권장</td>
<td>2 권장</td>
</tr>
<tr><td>videoWidth</td>
<td>설정 필요 없음</td>
<td>0 불가</td>
<td>0 권장</td>
<td>0 불가</td>
</tr><tr>
<td>videoHeight</td>
<td>설정 필요 없음</td>
<td>0 불가</td>
<td>0 권장</td>
<td>0 불가</td>
</tr><tr>
<td>videoBitrate</td>
<td>설정 필요 없음</td>
<td>0 불가</td>
<td>0 권장</td>
<td>0 불가</td>
</tr><tr>
<td>videoFramerate</td>
<td>설정 필요 없음</td>
<td>15 권장</td>
<td>15 권장</td>
<td>15 권장</td>
</tr><tr>
<td>videoGOP</td>
<td>설정 필요 없음</td>
<td>3 권장</td>
<td>3 권장</td>
<td>3 권장</td>
</tr><tr>
<td>mixUsers 배열</td>
<td>설정 필요 없음</td>
<td>플레이스 홀더 설정 사용</td>
<td>설정 필요 없음</td>
<td>실제 userId 설정 사용</td>
</tr></tbody></table>


[](id:PureAudio)

### 퓨어 오디오 모드(PureAudio)

#### 적용 시나리오

퓨어 오디오 모드는 음성 통화(AudioCall) 및 음성 채팅방(VoiceChatRoom) 등 퓨어 오디오 응용 시나리오에 적용되며, 해당 유형의 시나리오에서 SDK의 [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) 인터페이스를 호출할 때 설정할 수 있습니다.
퓨어 오디오 모드에서 SDK는 자동으로 방 안에 있는 여러 채널의 오디오 스트림을 한 채널의 스트림으로 혼합합니다.

#### 사용 방법

1. `enterRoom()` 함수를 호출하여 방 입장 시 서비스 필요에 따라 AppScene 매개변수를 `TRTCAppSceneAudioCall` 또는 `TRTCAppSceneVoiceChatRoom`으로 설정하여 현재 방 안에 비디오가 존재하지 않고 오디오만 존재함을 명확하게 설정합니다.
2. [릴레이 라이브 방송](https://intl.cloud.tencent.com/document/product/647/35242)을 활성화하고 TRTCParams의 `streamId` 매개변수를 설정해 MCU가 출력하는 혼합 오디오 스트림 저장 위치를 지정합니다.
3. `startLocalAudio()`를 호출하여 로컬 오디오 수집 및 오디오 업스트림을 활성화합니다.
>? 클라우드 혼합 스트림은 본질적으로 여러 채널의 스트림을 현재 사용자(즉, 혼합 스트림을 명령한 사용자)의 멀티미디어 스트림에 혼합합니다. 따라서 현재 사용자 본인의 오디오 업스트림이 반드시 있어야만 혼합 스트림의 전제조건을 구성할 수 있습니다.
4. `setMixTranscodingConfig()` 인터페이스를 호출하여 클라우드 혼합 스트림을 실행할 경우, 호출 시 `TRTCTranscodingConfig`의 `mode` 매개변수를 **TRTCTranscodingConfigMode_Template_PureAudio**로 설정하고 `audioSampleRate`, `audioBitrate`, `audioChannels` 등 오디오 출력 품질 관련 매개변수를 지정해야 합니다.
5. 위의 절차를 진행하면 해당 사용자의 릴레이 오디오 스트림에 자동으로 방 안의 다른 사용자 오디오가 혼합됩니다. 그런 다음 [CDN 라이브 방송 시청](https://intl.cloud.tencent.com/document/product/647/35242) 문서를 참조하여 재생 도메인을 설정해 라이브 방송을 시청할 수 있으며, [클라우드 녹화](https://intl.cloud.tencent.com/document/product/647/35426) 문서를 참조하여 혼합한 오디오 스트림을 녹화할 수 있습니다.

>! 퓨어 오디오 모드에서 `setMixTranscodingConfig()` 인터페이스는 여러 번 호출할 필요 없이, 방 입장 후 로컬 오디오 업스트림을 활성화한 다음 한 번만 호출하면 됩니다.

[](id:PresetLayout)
### 프리셋 레이아웃 모드(PresetLayout)
#### 적용 시나리오
프리셋 레이아웃 모드는 영상 통화(VideoCall) 및 ILVB(LIVE) 등 오디오와 비디오가 모두 포함된 응용 시나리오에 적용되며, 해당 시나리오에서 SDK의 [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) 인터페이스를 호출할 때 설정할 수 있습니다.
프리셋 레이아웃 모드에서 SDK는 자동으로 사전 설정한 각 채널 화면의 레이아웃 규칙에 따라 방 안에 있는 여러 채널의 오디오 스트림을 한 채널의 스트림으로 혼합합니다.

#### 사용 방법
1. `enterRoom()` 함수를 호출하여 방 입장 시 서비스 필요에 따라 AppScene 매개변수를 `TRTCAppSceneVideoCall` 또는 `TRTCAppSceneLIVE`로 설정합니다.
2. [릴레이 라이브 방송](https://intl.cloud.tencent.com/document/product/647/35242)을 활성화하고 TRTCParams의 `streamId` 매개변수를 설정해 MCU가 출력하는 혼합 오디오 스트림 저장 위치를 지정합니다.
3. `startLocalPreview()` 및 `startLocalAudio()`를 호출하여 로컬 멀티미디어 업스트림을 활성화합니다.
>? 클라우드 혼합 스트림은 본질적으로 여러 채널의 스트림을 현재 사용자(즉, 혼합 스트림을 명령한 사용자)의 멀티미디어 스트림에 혼합합니다. 따라서 현재 사용자 본인의 멀티미디어 업스트림이 반드시 있어야만 혼합 스트림의 전제조건을 구성할 수 있습니다.
4. `setMixTranscodingConfig()` 인터페이스를 호출하여 클라우드 혼합 스트림을 실행할 경우, 호출 시 `TRTCTranscodingConfig`의 `mode` 매개변수를 **TRTCTranscodingConfigMode_Template_PresetLayout**으로 설정하고 `audioSampleRate`, `audioBitrate`, `audioChannels` 등 오디오 출력 품질 관련 매개변수와 `videoWidth`, `videoHeight`, `videoBitrate`, `videoFramerate` 등 비디오 출력 품질 관련 매개변수를 지정해야 합니다.
5. `mixUser` 매개변수를 어셈블리하고, 프리셋 레이아웃 모드의 `mixUser`에서 **$PLACE_HOLDER_REMOTE$**, **$PLACE_HOLDER_LOCAL_MAIN$**, **$PLACE_HOLDER_LOCAL_SUB$**의 세 가지 플레이스 홀더 문자열을 `userId` 매개변수로 사용합니다. 해당 문자열의 의미는 다음과 같습니다.
<table>
<tr><th>플레이스 홀더</th><th>의미</th><th>다중 지원 여부</th></tr><tr>
<td>$PLACE_HOLDER_LOCAL_MAIN$</td><td>로컬 카메라 채널</td><td>미지원</td>
</tr><tr>
<td>$PLACE_HOLDER_LOCAL_SUB$</td><td>로컬 화면 공유 채널(화면만)</td><td>미지원</td>
</tr><tr>
<td>$PLACE_HOLDER_REMOTE$</td><td>원격 마이크 연결 사용자(중복 설정 가능)</td><td>지원</td>
</tr></table>
6. 위의 절차를 진행하면 해당 사용자의 릴레이 오디오 스트림에 자동으로 방 안의 다른 사용자 오디오가 혼합됩니다. 그런 다음 [CDN 라이브 방송 시청](https://intl.cloud.tencent.com/document/product/647/35242) 문서를 참조하여 재생 도메인을 설정해 라이브 방송을 시청할 수 있으며, [클라우드 녹화](https://intl.cloud.tencent.com/document/product/647/35426) 문서를 참조하여 혼합한 오디오 스트림을 녹화할 수 있습니다.

![](https://main.qcloudimg.com/raw/4119e41cefe59b7a8b8edf675babdd38.png)

[](id:example_code)

#### 예시 코드
아래 예시 코드에 따라 '큰 화면 1개, 작은 화면 2개, 상하 겹침' 혼합 효과를 구현할 수 있습니다.
<dx-codeblock>
::: iOS  Objective-C 
TRTCTranscodingConfig *config = [[TRTCTranscodingConfig alloc] init];
// 해상도 720 × 1280, 비트 레이트 1500kbps, 프레임 레이트 20FPS로 설정
config.videoWidth      = 720;
config.videoHeight     = 1280;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;
// 프리셋 레이아웃 모드 사용
config.mode = TRTCTranscodingConfigMode_Template_PresetLayout;
    
NSMutableArray *mixUsers = [NSMutableArray new];
// 호스트 카메라의 화면 위치
TRTCMixUser* local = [TRTCMixUser new];
local.userId = @"$PLACE_HOLDER_LOCAL_MAIN$";
local.zOrder = 0;   // zOrder가 0인 경우, 호스트 화면이 가장 하위 레이어에 위치한다는 의미
local.rect   = CGRectMake(0, 0, videoWidth, videoHeight);
local.roomID = nil; // 로컬 사용자는 roomID 입력이 필요 없으나 원격 사용자는 필요
[mixUsers addObject:local];

// 마이크 연결 사용자의 화면 위치
TRTCMixUser* remote1 = [TRTCMixUser new];
remote1.userId = @"$PLACE_HOLDER_REMOTE$";
remote1.zOrder = 1;
remote1.rect   = CGRectMake(400, 800, 180, 240); //참고용
remote1.roomID = @"97392"; // 로컬 사용자는 roomID 입력이 필요 없으나 원격 사용자는 필요
[mixUsers addObject:remote1];

// 마이크 연결 사용자의 화면 위치
TRTCMixUser* remote2 = [TRTCMixUser new];
remote2.userId = @"$PLACE_HOLDER_REMOTE$";
remote2.zOrder = 1;
remote2.rect   = CGRectMake(400, 500, 180, 240); //참고용
remote2.roomID = @"97392"; // 로컬 사용자는 roomID 입력이 필요 없으나 원격 사용자는 필요
[mixUsers addObject:remote2];

config.mixUsers = mixUsers;
// 클라우드 혼합 스트림 요청
[_trtc setMixTranscodingConfig:config];
:::
::: Android java
TRTCCloudDef.TRTCTranscodingConfig config = new TRTCCloudDef.TRTCTranscodingConfig();
// 해상도 720 × 1280, 비트 레이트 1500kbps, 프레임 레이트 20FPS로 설정
config.videoWidth      = 720;
config.videoHeight     = 1280;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;

// 프리셋 레이아웃 모드 사용
config.mode = TRTCCloudDef.TRTC_TranscodingConfigMode_Template_PresetLayout;
config.mixUsers = new ArrayList<>();

// 호스트 카메라의 화면 위치
TRTCCloudDef.TRTCMixUser local = new TRTCCloudDef.TRTCMixUser();
local.userId = "$PLACE_HOLDER_LOCAL_MAIN$";
local.zOrder = 0;   // zOrder가 0인 경우, 호스트 화면이 가장 하위 레이어에 위치한다는 의미
local.x      = 0;
local.y      = 0;
local.width  = videoWidth;
local.height = videoHeight;
local.roomId = null; // 로컬 사용자는 roomID 입력이 필요 없으나 원격 사용자는 필요
config.mixUsers.add(local);

// 마이크 연결 사용자의 화면 위치
TRTCCloudDef.TRTCMixUser remote1 = new TRTCCloudDef.TRTCMixUser();
remote1.userId = "$PLACE_HOLDER_REMOTE$";
remote1.zOrder = 1;
remote1.x      = 400; //참고용
remote1.y      = 800; //참고용
remote1.width  = 180; //참고용
remote1.height = 240; //참고용
remote1.roomId = "97392"; // 로컬 사용자는 roomID 입력이 필요 없으나 원격 사용자는 필요
config.mixUsers.add(remote1);

// 마이크 연결 사용자의 화면 위치
TRTCCloudDef.TRTCMixUser remote2 = new TRTCCloudDef.TRTCMixUser();
remote2.userId = "$PLACE_HOLDER_REMOTE$";
remote2.zOrder = 1;
remote1.x      = 400; //참고용
remote1.y      = 500; //참고용
remote1.width  = 180; //참고용
remote1.height = 240; //참고용
remote1.roomId = "97393"; // 로컬 사용자는 roomID 입력이 필요 없으나 원격 사용자는 필요
config.mixUsers.add(remote2);

// 클라우드 혼합 스트림 요청
trtc.setMixTranscodingConfig(config);
:::
::: C++ C++
TRTCTranscodingConfig config;
// 해상도 1280 × 720, 비트 레이트 1500kbps, 프레임 레이트 20fps로 설정
config.videoWidth      = 1280;
config.videoHeight     = 720;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;

// 프리셋 레이아웃 모드 사용
config.mode == TRTCTranscodingConfigMode_Template_PresetLayout
TRTCMixUser* mixUsersArray = new TRTCMixUser[3];
mixUsersArray[0].userId      = "$PLACE_HOLDER_LOCAL_MAIN$";
mixUsersArray[0].zOrder      = 0; // zOrder가 0인 경우, 호스트 화면이 가장 하위 레이어에 위치한다는 의미
mixUsersArray[0].rect.left   = 0;
mixUsersArray[0].rect.top    = 0;    
mixUsersArray[0].rect.right  = videoWidth;
mixUsersArray[0].rect.bottom = videoHeight;
mixUsersArray[0].roomId      = nullptr; // 로컬 사용자는 roomID 입력이 필요 없으나 원격 사용자는 필요

mixUsersArray[1].userId      = "$PLACE_HOLDER_REMOTE$";
mixUsersArray[1].zOrder      = 1;
mixUsersArray[1].rect.left   = 400; //참고용
mixUsersArray[1].rect.top    = 800; //참고용
mixUsersArray[1].rect.right  = 180; //참고용
mixUsersArray[1].rect.bottom = 240; //참고용
mixUsersArray[1].roomId      = "97392"; // 로컬 사용자는 roomID 입력이 필요 없으나 원격 사용자는 필요

mixUsersArray[2].userId      = "$PLACE_HOLDER_REMOTE$";
mixUsersArray[2].zOrder      = 1;
mixUsersArray[2].rect.left   = 400; //참고용
mixUsersArray[2].rect.top    = 500; //참고용   
mixUsersArray[2].rect.right  = 180; //참고용
mixUsersArray[2].rect.bottom = 240; //참고용
mixUsersArray[2].roomId      = "97393"; // 로컬 사용자는 roomID 입력이 필요 없으나 원격 사용자는 필요
config.mixUsersArray = mixUsersArray;

// 클라우드 혼합 스트림 요청
trtc->setMixTranscodingConfig(&config);
:::
::: C# C#
TRTCTranscodingConfig config = new TRTCTranscodingConfig();
// 해상도 1280 × 720, 비트 레이트 1500kbps, 프레임 레이트 20fps로 설정
config.videoWidth      = 1280;
config.videoHeight     = 720;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;
config.mode = RTCTranscodingConfigMode.TRTCTranscodingConfigMode_Template_PresetLayout;
TRTCMixUser[] mixUsersArray = new TRTCMixUser[3];

// 호스트 카메라의 화면 위치
TRTCMixUser local = new TRTCMixUser();
local.userId = "$PLACE_HOLDER_LOCAL_MAIN$";
local.zOrder = 0; // zOrder가 0인 경우, 호스트 화면이 가장 하위 레이어에 위치한다는 의미
local.roomId = null; // 로컬 사용자는 roomID 입력이 필요 없으나 원격 사용자는 필요
RECT rtLocal = new RECT() {
    left   = 0, 
    top    = 0,
    right  = videoWidth,
    bottom = videoHeight
};
local.rect = rtLocal;
mixUsersArray[0] = local;

// 마이크 연결 사용자의 화면 위치
TRTCMixUser remote1 = new TRTCMixUser();
remote1.userId = "$PLACE_HOLDER_REMOTE$";
remote1.zOrder = 1;
remote1.roomId = “97392”; // 로컬 사용자는 roomID 입력이 필요 없으나 원격 사용자는 필요
RECT rtRemote1 = new RECT() { //참고용
    left   = 420,
    top    = 81,
    right  = 240 + left,
    bottom = 240 + top
};
remote1.rect = rtRemote1;
mixUsersArray[1] = remote1;

// 마이크 연결 사용자의 화면 위치
TRTCMixUser remote2 = new TRTCMixUser();
remote2.userId = "$PLACE_HOLDER_REMOTE$";
remote2.zOrder = 1;
remote2.roomId = “97393”; // 로컬 사용자는 roomID 입력이 필요 없으나 원격 사용자는 필요
RECT rtRemote2 = new RECT() { //참고용
    left   = 660,
    top    = 400,
    right  = 240 + left,
    bottom = 240 + top
};
rtRemote2.rect   = rtRemote2;
mixUsersArray[2] = remote2;

// 클라우드 혼합 스트림 요청
config.mixUsersArray = mixUsersArray;
trtc.setMixTranscodingConfig(config);
:::
::: Flutter java
TRTCCloud trtcCloud = await TRTCCloud.sharedInstance();
trtcCloud.setMixTranscodingConfig(TRTCTranscodingConfig(
  appId: 1252463788, //참고용
  bizId: 3891, //참고용
  // 해상도 720 × 1280, 비트 레이트 1500kbps, 프레임 레이트 20FPS로 설정
  videoWidth: 720,
  videoHeight: 1280,
  videoBitrate: 1500,
  videoFramerate: 20,
  videoGOP: 2,
  audioSampleRate: 48000,
  audioBitrate: 64,
  audioChannels: 2,

  // 프리셋 레이아웃 모드 사용
  mode: TRTCCloudDef.TRTC_TranscodingConfigMode_Template_PresetLayout,

  mixUsers: [
  // 호스트 카메라의 화면 위치
    TRTCMixUser(
      userId: "$PLACE_HOLDER_LOCAL_MAIN$",
      roomId: null, // 로컬 사용자는 roomID 입력이 필요 없으나 원격 사용자는 필요
      zOrder: 0, // zOrder가 0인 경우, 호스트 화면이 가장 하위 레이어에 위치한다는 의미
      x: 0, //참고용
      y: 0,
      streamType: 0,
      width: 300,
      height: 400),
    TRTCMixUser(
      userId: '$PLACE_HOLDER_REMOTE$',
      roomId: '256', // 로컬 사용자는 roomID 입력이 필요 없으나 원격 사용자는 필요
      zOrder: 1,
      x: 100, //참고용
      y: 100,
      streamType: 0,
      width: 160,
      height: 200)
  ],
));
:::
::: Web JavaScript
try {
  // 프리셋 레이아웃 모드
  const config = {
   mode: 'preset-layout',
   videoWidth: 720,
   videoHeight: 1280,
   videoBitrate: 1500,
   videoFramerate: 20,
   videoGOP: 2,
   audioSampleRate: 48000,
   audioBitrate: 64,
   audioChannels: 2,
   // 로컬 카메라 1개, 원격 스트림 2개의 레이아웃 위치 사전 설정
   mixUsers: [
      {
        width: 720,
        height: 1280,
        locationX: 0,
        locationY: 0,
        pureAudio: false,
        userId: 'jack', // 로컬 카메라 위치 점유, 푸시 카메라의 client userId 전송
        zOrder: 1
      },
      {
        width: 180,
        height: 240,
        locationX: 400,
        locationY: 800,
        pureAudio: false,
        userId: '$PLACE_HOLDER_REMOTE$', // 원격 스트림 위치 점유
        zOrder: 2
      },
      {
        width: 180,
        height: 240,
        locationX: 400,
        locationY: 500,
        pureAudio: false,
        userId: '$PLACE_HOLDER_REMOTE$', // 원격 스트림 위치 점유
        zOrder: 2
      }
    ];
  }
  await client.startMixTranscode(config);
} catch (error) {
  console.error('startMixTranscode failed ', error);
}
:::
</dx-codeblock>  

>! 
>- 프리셋 레이아웃 모드에서 `setMixTranscodingConfig()` 인터페이스는 여러 번 호출할 필요 없이, 방 입장 후 로컬 오디오 업스트림을 활성화한 다음 한 번만 호출하면 됩니다.
>- Web 인터페이스의 이름 생성은 다른 클라이언트와 약간의 차이가 있습니다. 자세한 내용은 [Client.startMixTranscode()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#startMixTranscode)를 참조하십시오.

[](id:ScreenSharing)
### 화면 공유 모드(ScreenSharing)
#### 적용 시나리오
화면 공유 모드는 온라인 교육 및 인터랙션 수업 등의 시나리오에 적용되며, 해당 유형의 시나리오에서 SDK의 [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) 인터페이스를 호출할 때 AppScene 매개변수를 `TRTCAppSceneLIVE`로 설정할 수 있습니다.
화면 공유 모드에서 SDK는 먼저 사용자가 선택한 타깃 해상도에 따라 캔버스를 구성합니다. 교사가 화면 공유를 활성화하지 않으면 카메라 화면 등의 비율을 해당 캔버스에 가져오고, 교사가 화면 공유를 활성화하면 공유 화면을 동일한 캔버스에 가져옵니다. 캔버스 구축을 통해 혼합 스트림 모듈의 출력 해상도를 동일하게 유지할 수 있으며, 녹화와 웹 페이지 시청에서의 비디오 호환성 문제를 방지합니다(일반 플레이어에서는 해상도가 변경되는 비디오를 지원하지 않음).

#### 사용 방법
1. `enterRoom()` 함수를 호출하여 방 입장 시 서비스 필요에 따라 AppScene 매개변수를 `TRTCAppSceneLIVE`로 설정합니다.
2. [릴레이 라이브 방송](https://intl.cloud.tencent.com/document/product/647/35242)을 활성화하고 TRTCParams의 `streamId` 매개변수를 설정해 MCU가 출력하는 혼합 멀티미디어 스트림 저장 위치를 지정합니다.
3. `startLocalPreview()` 및 `startLocalAudio()`를 호출하여 로컬 멀티미디어 업스트림을 활성화합니다.
>? 클라우드 혼합 스트림은 본질적으로 여러 채널의 스트림을 현재 사용자(즉, 혼합 스트림을 명령한 사용자)의 멀티미디어 스트림에 혼합합니다. 따라서 현재 사용자 본인의 멀티미디어 업스트림이 반드시 있어야만 혼합 스트림의 전제조건을 구성할 수 있습니다.
4. `setMixTranscodingConfig()` 인터페이스를 호출하여 클라우드 혼합 스트림을 실행할 경우, 호출 시 `TRTCTranscodingConfig`의 `mode` 매개변수를 **TRTCTranscodingConfigMode_Template_ScreenSharing**으로 설정하고 `audioSampleRate`, `audioBitrate`, `audioChannels` 등 오디오 출력 품질 관련 매개변수와 `videoWidth`, `videoHeight`, `videoBitrate`, `videoFramerate` 등 비디오 출력 품질 관련 매개변수를 지정해야 합니다.
>?`videoWidth`와 `videoHeight` 매개변수를 모두 0으로 지정하는 경우, SDK는 자동으로 사용자의 현재 화면 너비와 높이 비율에 따라 적합한 해상도를 계산합니다.
5. 위의 절차를 진행하면 해당 사용자의 릴레이 오디오 스트림에 자동으로 방 안의 다른 사용자 오디오가 혼합됩니다. 그런 다음 [CDN 라이브 방송 시청](https://intl.cloud.tencent.com/document/product/647/35242) 문서를 참조하여 재생 도메인을 설정해 라이브 방송을 시청할 수 있으며, [클라우드 녹화](https://intl.cloud.tencent.com/document/product/647/35426) 문서를 참조하여 혼합한 오디오 스트림을 녹화할 수 있습니다.

![](https://main.qcloudimg.com/raw/675e67bfaff40451b60a21aa403217d4.gif)
>! 
>- 화면 공유 모드는 Windows와 Mac 플랫폼만 지원됩니다.
>! 화면 공유 모드에서 `setMixTranscodingConfig()` 인터페이스는 여러 번 호출할 필요 없이, 방 입장 후 로컬 오디오 업스트림을 활성화한 다음 한 번만 호출하면 됩니다.
>- 교육 모드의 비디오 콘텐츠는 화면 공유가 주를 이루기 때문에, 카메라 화면과 화면 공유용 화면의 동시 전송은 불필요한 대역폭 소모입니다. 따라서 `setLocalVideoRenderCallback()` 및 `setRemoteVideoRenderCallback()` 인터페이스를 통해 카메라 화면과 학생 화면을 직접 현재 화면에 가져오는 것을 권장합니다.
>- TRTCTranscodingConfig의 `videoWidth`와 `videoHeight` 매개변수를 0으로 지정하는 경우, SDK가 출력 해상도를 직접 스마트하게 선택합니다. 교사의 현재 화면 너비가 1920px보다 작은 경우 SDK는 교사의 현재 화면의 실제 해상도를 사용하며, 1920px보다 큰 경우 현재 화면 폭과 높이 비율에 따라 1920 × 1080(16:9), 1920 × 1200(16:10) 또는 1920 × 1440(4:3)으로 선택합니다.

[](id:Manual)

### 매뉴얼 모드(Manual)
#### 적용 시나리오
매뉴얼 모드는 위의 자동 모드에 적합하지 않은 모든 시나리오에 적용할 수 있습니다. 높은 유연성으로 다양한 혼합 스트림 방법을 자유롭게 조합할 수 있지만, 활용성이 가장 낮습니다.
매뉴얼 모드에서는 `TRTCTranscodingConfig`의 모든 매개변수를 설정해야 하며, TRTCCloudDelegate의 `onUserVideoAvailable()` 및 `onUserAudioAvailable()` 콜백을 수신해 현재 방 안에 있는 각 마이크가 켜진 사용자의 멀티미디어 상태에 따라 끊임없이 `mixUsers` 매개변수를 조정해야 합니다. 그렇지 않을 경우 혼합 스트림에 실패합니다.

#### 사용 방법
1. `enterRoom()` 함수를 호출하여 방 입장 시 서비스 필요에 따라 AppScene 매개변수를 설정합니다.
2. [릴레이 라이브 방송](https://intl.cloud.tencent.com/document/product/647/35242)을 활성화하고 TRTCParams의 `streamId` 매개변수를 설정해 MCU가 출력하는 혼합 멀티미디어 스트림 저장 위치를 지정합니다.
3. 서비스 필요에 따라 `startLocalAudio()`를 호출하여 로컬 오디오 업스트림을 활성화 또는 동시에 `startLocalPreview()`를 호출해 비디오 업스트림을 활성화합니다.
>? 클라우드 혼합 스트림은 본질적으로 여러 채널의 스트림을 현재 사용자(즉, 혼합 스트림을 명령한 사용자)의 멀티미디어 스트림에 혼합합니다. 따라서 현재 사용자 본인의 멀티미디어 업스트림이 반드시 있어야만 혼합 스트림의 전제조건을 구성할 수 있습니다.
4. `setMixTranscodingConfig()` 인터페이스를 호출하여 클라우드 혼합 스트림을 실행할 경우, 호출 시 `TRTCTranscodingConfig`의 `mode` 매개변수를 **TRTCTranscodingConfigMode_Manual**로 설정하고 `audioSampleRate`, `audioBitrate`, `audioChannels` 등 오디오 출력 품질 관련 매개변수를 지정해야 합니다. 비즈니스 시나리오에 비디오가 포함되어 있는 경우 `videoWidth`, `videoHeight`, `videoBitrate`, `videoFramerate` 등 비디오 출력 품질 관련 매개변수도 함께 설정해야 합니다.
5. TRTCCloudDelegate의 `onUserVideoAvailable()` 및 `onUserAudioAvailable()` 콜백을 수신하고 필요에 따라 **mixUsers** 매개변수를 지정합니다.
 >?프리셋 레이아웃(PresetLayout) 모드와 달리 Manual 모드는 모든 `mixUser`의 `userId` 매개변수를 실제 마이크 연결 사용자의 ID로 지정해야 하며, 해당 마이크 연결 사용자의 비디오 활성화 여부에 따라 실제와 동일하게 `mixUser`의 `pureAudio` 매개변수를 설정해야 합니다.
6. 위의 절차를 진행하면 해당 사용자의 릴레이 오디오 스트림에 자동으로 방 안의 다른 사용자 오디오가 혼합됩니다. 그런 다음 [CDN 라이브 방송 시청](https://intl.cloud.tencent.com/document/product/647/35242) 문서를 참조하여 재생 도메인을 설정해 라이브 방송을 시청할 수 있으며, [클라우드 녹화](https://intl.cloud.tencent.com/document/product/647/35426) 문서를 참조하여 혼합한 오디오 스트림을 녹화할 수 있습니다.
>! 매뉴얼 모드에서는 방 안에 있는 마이크 연결 사용자가 마이크 켜거나 끄는 동작을 실시간으로 수신해야 하고, 마이크가 연결된 사용자 인원수 및 멀티미디어 상태에 따라 여러 번`setMixTranscodingConfig()` 인터페이스를 호출해야 합니다.

## 관련 요금

### 요금 계산

클라우드 혼합 스트림 트랜스 코딩은 MCU 클러스터를 입력한 멀티미디어 스트림을 디코딩한 후 다시 인코딩하여 출력하며, 별도의 서비스 요금이 발생합니다. 이에 따라 TRTC는 MCU 클러스터를 사용하여 클라우드 혼합 스트림 트랜스 코딩을 진행하는 사용자에게 별도의 부가 서비스 요금을 청구합니다. 클라우드 혼합 스트림 트랜스 코딩 요금은 **트랜스 코딩으로 출력하는 해상도 크기** 및 **트랜스 코딩 시간**에 따라 과금되며, 트랜스 코딩으로 출력하는 해상도가 높고 시간이 길수록 요금이 올라갑니다. 자세한 내용은 [클라우드 혼합 스트림 트랜스 코딩 과금 설명](https://intl.cloud.tencent.com/document/product/647/38929)을 참조하십시오.

### 요금 절약

- **서버의 REST API 혼합 스트림 상태에서 혼합 스트림을 중지하려면** 다음 조건 중 하나를 만족해야 합니다.
  - 방 안의 모든 사용자(호스트 및 시청자 포함)가 모두 방에서 퇴장한 경우
  - REST API [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)를 호출하여 직접 혼합 스트림을 중지하는 경우
- **클라이언트의 SDK API 혼합 스트림 상태에서 혼합 스트림을 중지하려면** 다음 조건 중 하나를 만족해야 합니다.
  - 혼합 스트림을 요청한(즉, 클라이언트 API `setMixTranscodingConfig`를 호출한) 호스트가 방을 퇴장한 경우
  - [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93)를 호출하고 매개변수를 `nil/null`로 설정하여 직접 혼합 스트림을 중지하는 경우

기타 상황에서 TRTC 클라우드는 최대한 혼합 스트림 상태를 유지하려 합니다. 따라서 예상하지 못한 혼합 스트림 요금이 발생하는 것을 방지하기 위해, 혼합 스트림이 필요하지 않은 경우 최대한 빨리 위의 방법을 통해 클라우드 혼합 스트림을 중지하십시오.



