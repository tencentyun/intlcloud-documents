본문은 개발자가 쉽게 통합하고 디버깅할 수 있도록 실시간 음성 채팅 클라이언트 녹음용 Game Multimedia Engine(GME) API에 대해 설명합니다.

## 전제 조건
- **음성 채팅 서비스 활성화 완료**: [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오.

- **GME SDK 통합 완료**: 핵심 API 및 음성 채팅 API 연동을 포함합니다. 자세한 내용은 [Native SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/40858), [Unity SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/44544), [Unreal SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/44545)을 참고하십시오.

- **실시간 음성 채팅 서비스를 정상적으로 사용할 수 있는 상태여야 합니다.**


## 순서도

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027871376/aaf673c2be5a11eda3d0525400c56988.png?q-sign-algorithm=sha1&q-ak=AKIDBJMrwOrhKnRxWU4MH0V8YUnaFIJMwT7wiDquTEKpq-zpGVYlo88oQY9cENXuGvLe&q-sign-time=1678417064;1678420664&q-key-time=1678417064;1678420664&q-header-list=&q-url-param-list=&q-signature=d015a3210685afff0a59c5167ce09a4360733c94&x-cos-security-token=4gOshif4iC2Hey9APavaAOL1ySi2AiIa8d96df7d8edf56d835bd5d83706119c5ZVMzDjTNq9IPFXYZmX1d4wiBfM9f-eui07dpzmKHfaDl3-7FfAeW_OsmnhN9vMPU-Sv0f_Jhh9VaLC8u4hXOiJdPNqlKNr_y5N9jaeGSkFZ0bdW6rNZkmnkNYln4KoPUUMnc2yCC1H-0DQYcoEE1L_fZCY9c3z5yw4jzjjru3mur_fgWGtQT5d9_NQx9_WRvpbKs7rjm1Et74hBml3x5QLaEYb7zG3K7GAs_rpxR1m2JQZDu99LW5fl9R50dhMguYrZcl8iOrBjAM-QWuBxn6zkDU4_y0HE_9dA9FHGz4Zib3zuYERPKN5QupYwjFQO3mDZh3tEX8BgA0BmDsPhnrwIa4Q_wtxwHconKyPPUl1n81igwIWK0gZ0tn1GrIIu0)

## 녹화 API

### 녹화 시작

이 API를 통해 방 내 사운드 녹음을 시작하려면 입장에 성공한 후에만 API를 호출할 수 있습니다. 다음 세 가지 유형의 사운드를 개별 녹음하거나 동시에 녹음할 수 있습니다:
- 마이크 사운드: 마이크에서 수집된 사운드를 녹음합니다. 먼저 EnableMic로 마이크를 켜야 합니다.

- 다른 사람의 음성: GME을 통해 수신된 음성 채팅 방 내 다른 사람들이 말하는 혼합된 음성을 녹음합니다. 먼저 EnableSpeaker로 스피커를 켜야합니다.

- 반주 사운드: GME을 통해 재생되는 로컬 반주 사운드를 녹음합니다. 먼저 StartAccompany로 반주를 재생해야합니다.


   녹음 파일 형식은 MP3 오디오 파일입니다.


#### API 프로토타입




【Unity】
``` csharp
public abstract int StartRecord(string filePath, int sampleRate, int channels, bool recordLocalMic, bool recordRemote, bool recordAccompany);
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>

<td rowspan="1" colSpan="1" >유형</td>

<td rowspan="1" colSpan="1" >설명</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >녹음 파일 저장 경로입니다.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sampleRate</td>

<td rowspan="1" colSpan="1" >int</td>

<td rowspan="1" colSpan="1" >원본 오디오 데이터의 오디오 샘플링 레이트, 48000 입력을 권장합니다.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >channels</td>

<td rowspan="1" colSpan="1" >int</td>

<td rowspan="1" colSpan="1" >원본 오디오 데이터의 오디오 채널 수, 2 입력을 권장합니다.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >recordLocalMic</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >로컬 마이크에서 수집된 사운드의 녹음 여부입니다.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >recordRemote</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >수신된 방에 있는 다른 사람들의 음성의 녹음 여부입니다.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >recordAccompany</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >GME를 통해 로컬로 재생되는 반주 사운드 녹음 여부입니다.</td>
</tr>
</table>


#### 예시 코드




【Unity】
``` csharp
string recordPath = Application.persistentDataPath + string.Format ("/{0}.mp3", filename);
ITMGContext.GetInstance().GetAudioCtrl().StartRecord(recordPath, 48000, 2, true, false, false);
```

#### 반환된 값

반환 값 0은 성공을 의미하고 0이 아닌 값은 실패를 의미합니다.

### 녹음 중지

녹음을 중지하려면 이 API를 호출합니다.

#### API 프로토타입




【Unity】
``` csharp
public abstract int StopRecord();
```

#### 예시 코드




【Unity】
``` csharp
ITMGContext.GetInstance().GetAudioCtrl().StopRecord();
```

### 녹음 일시 정지

녹음을 일시 정지하려면 이 API를 호출합니다.

#### API 프로토타입




【Unity】
``` csharp
public abstract int PauseRecord();
```

#### 예시 코드




【Unity】
``` csharp
ITMGContext.GetInstance().GetAudioCtrl().PauseRecord();
```

### 녹음 재개

녹음을 재개하려면 이 API를 호출합니다.

#### API 프로토타입




【Unity】
``` csharp
public abstract int ResumeRecord();
```

#### 예시 코드




【Unity】
``` csharp
ITMGContext.GetInstance().GetAudioCtrl().ResumeRecord();
```

### 마이크 사운드 녹음 스위치

녹음이 시작된 후, 이 API를 사용하여 마이크가 수집한 사운드에 대한 녹음을 활성화/비활성화 합니다.

#### API 프로토타입




【Unity】
``` csharp
public abstract int EnableRecordLocalMic(bool recordLocalMic);
```

<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>

<td rowspan="1" colSpan="1" >유형</td>

<td rowspan="1" colSpan="1" >설명</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnableRecordLocalMic</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >true는 녹음 활성화를 의미하고 false는 녹음 비활성화를 의미합니다.</td>
</tr>
</table>


### 다른 사람의 사운드 녹음 스위치

녹음이 시작된 후, 이 API를 통해 다른 사람의 사운드에 대한 녹음을 활성화/비활성화 합니다.

#### API 프로토타입




【Unity】
``` csharp
public abstract int EnableRecordRemote(bool recordRemote);
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>

<td rowspan="1" colSpan="1" >유형</td>

<td rowspan="1" colSpan="1" >설명</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnableRecordRemote</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >true는 녹음 활성화를 의미하고 false는 녹음 비활성화를 의미합니다.</td>
</tr>
</table>


### 반주 사운드 녹음 스위치

녹음이 시작된 후, 이 API를 통해 반주 사운드에 대한 녹음을 활성화/비활성화 합니다.

#### API 프로토타입




【Unity】
``` csharp
EnableRecordAccompany(bool recordAccompany);
```

<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>

<td rowspan="1" colSpan="1" >유형</td>

<td rowspan="1" colSpan="1" >설명</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >recordAccompany</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >true는 녹음 활성화를 의미하고 false는 녹음 비활성화를 의미합니다.</td>
</tr>
</table>


