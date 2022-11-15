이 문서에서는 GME SDK의 고급 API에 액세스하고 디버그하는 방법을 설명합니다.

<dx-alert infotype="alarm" title="메모 호출">
본문은 필요한 경우가 아니면 호출할 필요가 없는 고급 API에 대해 설명합니다. 호출하기 전에 GME 개발자에게 문의하십시오.
</dx-alert>

## 고급 오디오 API

### iOS 오디오 API

SetAdvanceParams API는 사용자가 방에 입장하기 전에 다음 오디오 옵션을 활성화/비활성화하는 데 사용됩니다. 

```
[[ITMGContext GetInstance] SetAdvanceParams:keyString value:_value]
```

| 매개변수       | 의미                            |
| --------- | ------------------------------- |
| keyString | 각 Key는 각기 다른 기능을 표시함       |
| value     | <li> 0: 비활성화<li>1: 활성화 |

#### Key 

Key는 다음 매개변수 중 하나로 대체되어 다양한 오디오 옵션을 나타낼 수 있습니다.

- **OptionMixWithOthers**
  오디오를 믹싱합니다. 활성화되면 GME는 배경 음악과 음성 채팅 오디오를 동시에 재생할 수 있습니다.
- **OptionDuckOthers**
  배경 음악의 볼륨을 낮춥니다. 이 옵션과 OptionMixWithOthers가 모두 활성화되어 있으면 스피커에서 오디오를 재생할 때 배경 음악의 볼륨이 낮아집니다.
- **ReleaseAudioFoucus**
  오디오 포커스를 해제합니다.
- 활성화된 경우 QQ 음악과 같은 다른 오디오 애플리케이션이 계속 실행될 수 있도록 방을 나갈 때 오디오 포커스가 해제됩니다.
- 비활성화된 경우 방을 나갈 때 다른 오디오 애플리케이션을 계속 실행할 수 없습니다.

### iPhone의 벨소리/무음 스위치가 켜져 있는지 확인

<dx-alert infotype="explain" title="설명">
이 API는 GME SDK 2.8.4 이상 버전에서 적용됩니다.
</dx-alert>

#### 함수 프로토타입

```
CheckDeviceMuteState();
```

반환 값이 0이면 벨소리/무음 스위치 꺼짐을 나타내고, 1이면 켜짐을 나타냅니다.

### 마이크 상태 확인

<dx-alert infotype="explain" title="설명">
이 API는 GME SDK 2.8.4 이상 버전에서 적용됩니다.
</dx-alert>

#### 함수 프로토타입

```
TestMic();
```

#### 반환 값 처리

| 반환 값                               | 설명                | 처리                                                         |
| ------------------------------------ | ------------------- | ------------------------------------------------------------ |
| ITMG_TEST_MIC_STATUS_AVAILABLE = 0   | 정상적으로 사용 가능            | 처리가 필요하지 않음                                                     |
| ITMG_TEST_MIC_STATUS_NO_GRANTED = 2  | 액세스 권한을 얻지 못함/거부됨 | 마이크가 활성화되기 전에 액세스 권한을 얻어야 함                               |
| ITMG_TEST_MIC_STATUS_INVALID_MIC = 3 | 사용 가능한 디바이스 없음      | 일반적으로 이 오류는 사용 가능한 마이크가 없는 PC에서 보고되며, 이어폰이나 마이크를 삽입하라는 메시지가 표시됨 |
| ITMG_TEST_MIC_STATUS_NOT_INIT = 5    | 초기화되지 않음          | Init 후 EnableMic 호출                                |

### Android Bluetooth 장치 적용 설정

<dx-alert infotype="explain" title="설명">
이 API는 GME SDK 2.8.4 이상 버전에서 적용됩니다.
</dx-alert>

이 API를 호출하면 블루투스 헤드셋의 마이크를 on/off할 때 소리가 새는 문제와 Android 디바이스를 블루투스 헤드셋에 연결하고 연결 상태가 변경된 후 오디오가 스피커로 재생되는 문제를 해결할 수 있습니다.

```
SetAdvanceParams(“BluetoothUseMedia”, “1”);
```

### 오디오 믹싱 최대 스트림 수 설정

SetRecvMixStreamCount API는 사용자가 방에 입장하기 전에 오디오 믹싱 최대 스트림 수를 설정하는 데 사용됩니다. 이 API는 모든 플랫폼에서 사용할 수 있습니다. 여기서는 PC용 SetRecvMixStreamCount API를 예로 사용합니다.

```
virtual int SetRecvMixStreamCount(int nCount) = 0;
```

**매개변수 설명** 

| 매개변수   | 설명               |
| ------ | ------------------ |
| nCount | 오디오 믹싱 스트림 수, 최대값: 20 |



## 고급 방 API

### 방의 오디오 유형 설정

사용자가 방에 들어가기 전에 SetForceUseMediaVol을 사용하면 원활 또는 표준 음질의 방에서 미디어 볼륨을 사용할 수 있습니다.

```
[[ITMGContext GetInstance] SetAdvanceParams:SetForceUseMediaVol value:1]
```

#### value

각 value는 각기 다른 기능을 나타냅니다.
- 0: 음성방 유형1과 2 모두 마이크가 활성화된 후에도 통화 볼륨을 계속 사용합니다.
- 1: 음성방 유형1은 마이크가 활성화된 후 미디어 볼륨을 사용합니다(기존의 통화 볼륨).
- 2: 음성방 유형2는 마이크가 활성화된 후 미디어 볼륨을 사용합니다(기존의 통화 볼륨).

### 방에 있는 구성원 말하기 볼륨 가져오기

TrackingVolume API가 호출되면 키-값 쌍이 uin-volume인 `TIMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_USER_VOLUMES` 이벤트를 수신 대기합니다. 이 API를 통해 방에서 말하는 uin-volume을 기반으로 해당 에너지 컬럼 차트를 생성할 수 있습니다.

더 이상 방에 있는 구성원의 말하기 볼륨을 가져올 필요가 없으면 StopTrackingVolume API를 호출하십시오.

```
//TMGAudioCtrl
public int TrackingVolume(float fTrackingTimeS)
public int StopTrackingVolume();
```

| 매개변수              | 유형  | 의미                                                         |
| -------------- | ----- | --------------------------- |
| fTrackingTimeS | float | 리스닝 시간(초). 0.5f 권장 |

## 일반 고급 API
### openid 문자열로 전달
>! 이 API는 GME SDK 2.9.3 이상 버전에서 적용됩니다.

현재 GME SDK는 숫자를 문자열로 전달하는 것만 지원합니다. openid를 문자열로 전달하려면 Init API를 호출하기 전에 다음 API를 호출해야 합니다.
```
SetAdvanceParams("StringOpenID", "1");
``` 

### 로그 출력 크기 수정

<dx-alert infotype="explain" title="설명">
이 API는 GME SDK 2.8.4 이상 버전에서 적용됩니다.
</dx-alert>

기본 로그 파일 크기를 수정하려면 GME Init API 전에 이 API를 호출하십시오. 현재 단일 로그 파일은 50m이며 최대 3개의 로그 파일이 존재할 수 있습니다.

#### 함수 프로토타입

```
SetAdvanceParams（const char* key, const char* object）
```

| 매개변수   | 유형        | 의미                                                         |
| ------ | ----------- | ------------------------------------------------------------ |
| key    | const char* | MAX_LOG_FILE_SIZE_MB와 MAX_LOG_FILE_COUNT는 각각 단일 로그의 크기와 로그 수를 나타냅니다. |
| object | const char* | key가 MAX_LOG_FILE_SIZE_MB인 경우 object는 5-50M의 기본 Log 파일 크기입니다. key가 MAX_LOG_FILE_COUNT인 경우 object는 1-3의 기본 Log 파일 수 입니다. |

<dx-alert infotype="notice" title="매개변수 범위">
입력된 object 값이 값 범위의 상한을 초과하면 상한으로 설정됩니다. 값 범위의 하한 미만인 경우 하한으로 설정됩니다.
</dx-alert>

#### 예시 코드

```
SetAdvanceParams("MAX_LOG_FILE_SIZE_MB", "5");
SetAdvanceParams("MAX_LOG_FILE_COUNT", "1");
```

## 고급 기능 API

### 텍스트 번역 API

이 API는 텍스트를 번역하는 데 사용됩니다. 중국어 텍스트를 영어로 번역할 수 있습니다. 이 API가 호출된 후 콜백을 통해 결과가 반환됩니다. C++ API를 예로 들어 보겠습니다.

>!이 API는 SDK 291 이상에서 허용된 사용자만 사용할 수 있습니다. 사용을 원하시면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하여 신청하십시오.

#### 함수 프로토타입

```
virtual int TranslateText(const char* text, const char* sourceLanguage, const char* translateLanguage) = 0;
```

| 매개변수              | 유형        | 의미                                                         |
| ----------------- | ----------- | ------------------------------------------------------------ |
| text              | const char* | 번역할 텍스트. 비워둘 수 없으며 최대 5,000자까지 허용                     |
| sourceLanguage    | const char* | 번역할 텍스트 언어. 비워 둘 수 있으며 백엔드에서 자동으로 감지               |
| translateLanguage | const char* | 텍스트를 번역할 언어. 비워둘 수 없으며, 여러 언어는 "cmn-Hans-CN,en-GB", "cmn-Hans-CN"과 같이 쉼표(,)로 구분 |

언어 매개변수는 [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260)를 참고하십시오.

#### API 콜백

| 매개변수       | 유형                      | 의미                                                         |
| ---------- | ------------------------------- | ------------------------------------------------------------ |
| code       | int                             | 에러 코드. 0은 작업 성공을 의미하며, 다른 반환 코드는 [에러 코드](https://intl.cloud.tencent.com/document/product/607/33223)의 해결 방법 참고. |
| targetText | jason(Unity에서 string 형식 반환) | 번역본 텍스트, 예시     {"target_text":[{"target_language_code":"cmn-Hans-CN","target_text":"나는 중국인입니다"},{"target_language_code":"de-DE","target_text":"Ich bin Chinese"}]} |

#### Unity 프로젝트 예시 코드

1. 리스너 추가
```
ITMGContext.GetInstance().GetPttCtrl().OnTranslateTextComplete+= OnTranslateTextComplete;
```

2. API 호출
```
private void OnTranslateTextBtn()
{
     mTargetText.text = "";
    int ret = ITMGContext.GetInstance().GetPttCtrl().TranslateText(mSourceText. text, mSourceLanguageText.text, mTargetLanguageText.text);
    if (0 != ret)
    {
         mTargetText.text = "Invalid Atgument";
    }
}
```

3. 콜백 처리
```
void OnTranslateTextComplete(int code, string targetText)
{
    if (0 == code)
    {
        mTargetText.text = targetText;
    }
    else
    {
        mTargetText.text = String.Format(
            "Translate Text Error, Error Code:{0}", code);
    }
}
```

4. 리스너 취소
```
ITMGContext.GetInstance().GetPttCtrl().OnTranslateTextComplete-= OnTranslateTextComplete;
```

### 텍스트-음성 변환 API

이 API는 텍스트를 오디오로 변환하는 데 사용됩니다. 이 API가 호출되면 콜백을 통해 오디오 fileid가 반환됩니다. DownloadRecordedFile API를 사용하여 오디오를 다운로드할 수 있습니다. 여기서는 C++ API를 예로 사용합니다.

>!이 API는 사용자와 SDK 291 이상에서 허용된 사용자만 사용할 수 있습니다. 사용을 원하시면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하여 신청하십시오.

#### 함수 프로토타입

```
virtual int TextToSpeech(const char* text, const char* voiceName,const char* languageCode, float speakingRate) = 0;
```

| 매개변수        | 유형        | 의미                                           |
| ------------ | ----------- | ---------------------------------------------- |
| text         | const char* | 소스 텍스트. 비워둘 수 없으며 최대 5,000자까지 허용            |
| voiceName    | const char* | 음성 유형. 영어와 표준 중국어로 된 샘플이 제공되며 다른 언어 샘플은 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하여 신청 |
| languageCode | const char* | 대상 언어. 비워둘 수 없음.                         |
| speakingRate | float       | 오디오 속도. 값 범위: [0.6-1.5], 1은 정상 속도     |

voiceName의 유효한 값:

| 음성 유형 | 성별 | 언어 |
|---------|---------|---------|
| cmn-CN-Standard-A | 여성 | 표준 중국어 |
| cmn-CN-Standard-B | 남성 | 표준 중국어 |
| en-US-Neural2-A | 여성 | 영어 |
| en-US-Neural2-B | 남성 | 영어 |

언어 매개변수는 [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260)를 참고하십시오.

#### API 콜백

| 매개변수   | 유형   | 의미                                                         |
| ------ | ------ | ------------------------------------------------------------ |
| code   | int    | 에러 코드. 0은 작업 성공을 의미하며, 다른 반환 코드는 [에러 코드](https://intl.cloud.tencent.com/document/product/607/33223)의 해결 방법 참고. |
| isCos  | bool   | 파일 COS 업로드 여부                                            |
| fileID | string | 파일 ID. DownloadRecordedFile API를 통한 오디오 파일 다운로드를 위한 입력 매개변수. |

#### Unity 프로젝트 예시 코드

1. 리스너 추가
```
ITMGContext.GetInstance().GetPttCtrl().OnTextToSpeechComplete += new QAVTextToSpeechCallback(TextToSpeechComplate);
```

2. API 호출
```
void OnTextToSpeech()
{
    float fSpeakingRate;
    if (!float.TryParse(mSpeakingRate.text, out fSpeakingRate))
    {
        mReturnData.text = "SpeakingRate invalid";
         return;
    }

    int iRet = ITMGContext.GetInstance().GetPttCtrl().TextToSpeech(
        mSouceText.text, mVoiceName.text,
        mLanguageCode.text, fSpeakingRate);

    Debug.Log(string.Format("TextToSpeech Code:{0}", iRet));

    if (0 != iRet)
    {
        mReturnData.text = string.Format("TextToSpeech Error, errorCode:{0}", iRet);
        return;
    }
}
```

3. 콜백 처리
```
void TextToSpeechComplate(int code, bool isCos, string fileID)
{
    Debug.Log(string.Format("TextToSpeechComplate Code:{0}", code));

    if (0 != code)
    {
        mReturnData.text = string.Format("TextToSpeech Error, errorCode:{0}", code);
        return;
    }

    mReturnData.text = string.Format("code:{0}\r\nisCos:{1}\r\nfileID:{2}", code, isCos, fileID);
    mDownloadUrl.text = fileID;
}
```

4. 리스너 취소
```
ITMGContext.GetInstance().GetPttCtrl().OnTextToSpeechComplete -= new QAVTextToSpeechCallback(TextToSpeechComplate);
```
