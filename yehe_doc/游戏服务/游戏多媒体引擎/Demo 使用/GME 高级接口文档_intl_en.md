This document describes details of advanced GME APIs.

<dx-alert infotype="alarm" title="Invoking notes">
Consult the GME team before using these APIs.
</dx-alert>

## Audio APIs

### iOS Audio API

The `SetAdvanceParams` API is used to enable/disable the following audio options before a user enters a room. 

```
[[ITMGContext GetInstance] SetAdvanceParams:keyString value:_value]
```

| Parameter      | Description                            |
| --------- | ------------------------------- |
| keyString | Different keys represent different options       |
| value     |<li> 0: disable<li>1: enable |

#### Key 

The key can be replaced by one of the following parameters to represent different audio options:

- **OptionMixWithOthers**
  Mix audio. Once enabled, the background music and voice chat are played together with the original volume.
- **OptionDuckOthers**
  Duck background music. If both this option and `OptionMixWithOthers` are enabled, the background music is lowered down while the speaker is broadcasting audio.
- **ReleaseAudioFoucus**
  Release audio focus.
- If enabled, audio focus will be released when you exit a room so that other audio apps can continue running.
- If disabled, other audio apps cannot continue running when you exit a room.

### Checking whether the device is muted

<dx-alert infotype="explain" title="description">
This API is available for GME SDK 2.8.4 or later versions.
</dx-alert>

#### Function prototype

```
CheckDeviceMuteState();
```

The returned value of 0 means that the Ring/Silent switch is off, while 1 means on.

### Checking mic status

<dx-alert infotype="explain" title="description">
This API is available for GME SDK 2.8.4 or later versions.
</dx-alert>

#### Function prototype

```
TestMic();
```

#### Returned value handling

| Returned Value | Description | Handling |
| ------------------------------------ | ------------------- | ------------------------------------------------------------ |
| ITMG_TEST_MIC_STATUS_AVAILABLE = 0   | Normally available | No handling required |
| ITMG_TEST_MIC_STATUS_NO_GRANTED = 2 | Access not obtained/denied | The access permission needs to be obtained before the mic is enabled |
| ITMG_TEST_MIC_STATUS_INVALID_MIC = 3 | No device available      | Generally, this error will be reported on PCs with no available mics. Please prompt the user to insert earphones or mic |
| ITMG_TEST_MIC_STATUS_NOT_INIT = 5 | Not initialized | Call `EnableMic` after `Init` |

### Setting Android Bluetooth device adaptation

<dx-alert infotype="explain" title="description">
This API is available for GME SDK 2.8.4 or later versions.
</dx-alert>

Calling this API can solve the problem of sound leak when the mic on Bluetooth earphones is switched on/off, as well as the problem of playing back audio with the speaker after the connection status is changed after an Android device is connected to the Bluetooth earphones.

```
SetAdvanceParams("BluetoothUseMedia", "1");
```

### Setting the Maximum Number of the Mixed Audio Channels

`SetRecvMixStreamCount` is used to set the maximum number of the mixed audio channels. It’s invoked before a user enters the room. Take the SetRecvMixStreamCount API on PCs as an example.

```
virtual int SetRecvMixStreamCount(int nCount) = 0;
```

**Parameter description** 

| Parameter   | Description               |
| ------ | ------------------ |
| nCount | The number of mixed audio channels. Up to 20 channels allowed.|



## Room Management APIs

### Setting the Audio Type of the Room

If SetForceUseMediaVol is used before a user enters the room, the room with smooth sound quality or standard sound quality can use the media volume.

```
[[ITMGContext GetInstance] SetAdvanceParams:SetForceUseMediaVol value:1]
```

#### value

See below for details: 
- `0`: For both the room type 1 and 2, the mic volume follows the call volume.
- `1`: For rooms of type 1, the mic volume follows the media volume.
- `2`: For rooms of type 2, the mic volume follows the media volume.

### Obtaining the Speaking Volume of a Member in the Room

After the TrackingVolume API is called, it will monitor the `TIMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_USER_VOLUMES` event where the key-value pair is uin-volume. Through this API, the corresponding energy histogram can be generated based on the volume of a uin speaking in the room.

If you no longer need to obtain the speaking volume of the member in the room, please call the StopTrackingVolume API.

```
//TMGAudioCtrl
public int TrackingVolume(float fTrackingTimeS)
public int StopTrackingVolume();
```

| Parameter           | Type  | Description                        |
| -------------- | ----- | --------------------------- |
| fTrackingTimeS | float | Monitoring duration in seconds. `0.5f` is recommended. |

## General APIs

### Modifying print log size

<dx-alert infotype="explain" title="description">
This API is available for GME SDK 2.8.4 or later versions.
</dx-alert>

Call this API before the GME `Init` API to modify the default log file size. A single log file can be up to 50 MB, and there can be up to 3 log files.

#### Function prototype

```
SetAdvanceParams(const char* key, const char* object)
```

| Parameter   | Type         | Description                                                         |
| ------ | ----------- | ------------------------------------------------------------ |
| key    | const char* | `MAX_LOG_FILE_SIZE_MB`:  Max size of a single log file in MB. `MAX_LOG_FILE_COUNT`: Max number of log files. |
| object | const char* | When `key` is `MAX_LOG_FILE_SIZE_MB`, `object` is the default log file size, which can be 5 to 50 MB. When `key` is `MAX_LOG_FILE_COUNT`, `object` is the default number of log files, which can be 1 to 3. |

<dx-alert infotype="notice" title="parameter range">
If the entered `object` value exceeds the upper limit of the value range, it will be set as the upper limit; if it is below the lower limit of the value range, it will be set as the lower limit.
</dx-alert>

#### Sample code

```
SetAdvanceParams("MAX_LOG_FILE_SIZE_MB", "5");
SetAdvanceParams("MAX_LOG_FILE_COUNT", "1");
```

## Advanced Feature APIs

### Text translation APIs

This API is used to translate text. The result is returned through the callback. Take C++ API for example.

>! This API is only available to beta users and for SDK 291. To use this API, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

#### Function prototype

```
virtual int TranslateText(const char* text, const char* sourceLanguage, const char* translateLanguage) = 0;
```

| Parameter    | Type   | Description                                                                                                                    |
| ----------------- | ----------- | ------------------------------------------------------------ |
| text              | const char* | (Required) The text to be translated. Up to 5,000 characters allowed.                    |
| sourceLanguage    | const char* | (Optional) Language of the source text. If it’s not specified, GEM detects the language automatically.  |
| translateLanguage | const char* | (Required) Target language. If you want to translate the text into multiple languages, separate each of them with a comma (,) such as "cmn-Hans-CN,en-GB", "cmn-Hans-CN" |

For more information, see [Language parameter list](https://intl.cloud.tencent.com/document/product/607/30260).

#### API Callback

| Parameter       | Type                            | Description  |
| ---------- | ------------------------------- | ------------------------------------------------------------ |
| code       | int                             | 0 indicates a success operation. For the meaning of other codes, see [error codes](https://intl.cloud.tencent.com/document/product/607/33223).
| targetText | json (return string format in Unity) | translated target text, e.g. `{"target_text":[{"target_language_code": "cmn-Hans-CN", "target_text": "I am Chinese"},{" target_language_code": "de-DE", "target_text": "Ich bin Chinese"}]}` |

#### Unity project sample code

1. Add monitoring
```
ITMGContext.GetInstance().GetPttCtrl().OnTranslateTextComplete+= OnTranslateTextComplete;
```

2. Invoke API
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

3. Process callback
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

4. Cancel monitoring
```
ITMGContext.GetInstance().GetPttCtrl().OnTranslateTextComplete-= OnTranslateTextComplete;
```

### Text-to-speech APIs

This API can be used to convert a text into an audio. 

>! This API is only available to beta users and for SDK 291 and later versions. To use this API, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

#### Function prototype

```
virtual int TextToSpeech(const char* text, const char* voiceName,const char* languageCode, float speakingRate) = 0;
```

| Parameter         | Type        | Description                                           |
| ------------ | ----------- | ---------------------------------------------- |
| text              | const char* | (Required) The text to be translated. Up to 5,000 characters allowed.                    |
| voiceName    | const char* | (Optional) Language of the source text. If it’s not specified, GEM detects the language automatically.  |
| languageCode | const char* | (Required) Target language. |
| speakingRate | float       | Audio speed. Range: [0.6-1.5], `1` refers to the original speed.     |

For more information, see [Language parameter list](https://intl.cloud.tencent.com/document/product/607/30260).

#### API Callback

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------ | ------------------------------------------------------------ |
| code       | int                             | 0 indicates a success operation. For the meaning of other codes, see [error codes](https://intl.cloud.tencent.com/document/product/607/33223).
| isCos  | bool   | Whether to upload this file to COS                                            |
| fileID | string | File ID. You can use this ID to download the audio through DownloadRecordedFile API |

#### Unity project sample code

1. Add monitoring
```
ITMGContext.GetInstance().GetPttCtrl().OnTextToSpeechComplete += new QAVTextToSpeechCallback(TextToSpeechComplate);
```

2. Invoke API
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

3. Process callback
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

4. Cancel monitoring
```
ITMGContext.GetInstance().GetPttCtrl().OnTextToSpeechComplete -= new QAVTextToSpeechCallback(TextToSpeechComplate);
```
