This document describes how to access and debug the advanced APIs of the GME SDK.

<dx-alert infotype="alarm" title="Invoking notes">
This document describes advanced APIs that don't need to be called unless necessary. Consult GME developers before calling.
</dx-alert>

## Advanced Audio APIs

### iOS audio APIs

The `SetAdvanceParams` API is used to enable/disable the following audio options before a user enters a room. 

```
[[ITMGContext GetInstance] SetAdvanceParams:keyString value:_value]
```

| Parameter      | Description                            |
| --------- | ------------------------------- |
| keyString | Different keys represent different features. |
| value     |<li> 0: Disable<li>1: Enable |

#### Key 

The key can be replaced by one of the following parameters to represent different audio options:

- **OptionMixWithOthers**
  To mix audio. Once it is enabled, GME can play back the background music and voice chat audio at the same time.
- **OptionDuckOthers**
  To lower the volume level of the background music. If both this option and `OptionMixWithOthers` are enabled, the speaker will be enabled to play back audio while the volume level of the background music is lowered.
- **ReleaseAudioFoucus**
  To release the audio focus.
- If it is enabled, the audio focus will be released when you exit a room so that other audio applications such as QQ Music can continue running.
- If it is disabled, other audio applications cannot continue running when you exit a room.

### Checking whether the Ring/Silent switch of iPhone is on

<dx-alert infotype="explain" title="description">
This API takes effect on GME SDK 2.8.4 or later.
</dx-alert>

#### Function prototype

```
CheckDeviceMuteState();
```

The returned value `0` indicates that the Ring/Silent switch is off, while `1` indicates on.



### Setting Android Bluetooth device adaptation

<dx-alert infotype="explain" title="description">
This API takes effect on GME SDK 2.8.4 or later.
</dx-alert>

Calling this API can solve the problem of sound leak when the mic on the Bluetooth headset is switched on/off, as well as the problem of playing back audio with the speaker after the connection status is changed after an Android device is connected to the Bluetooth headset.

```
SetAdvanceParams("BluetoothUseMedia", "1");
```

### Setting the maximum number of the mix audio streams

The `SetRecvMixStreamCount` API is used to set the maximum number of the mix audio streams before a user enters a room. This API can be used on all platforms. Here, take the `SetRecvMixStreamCount` API for PC as an example.

```
virtual int SetRecvMixStreamCount(int nCount) = 0;
```

**Parameter description** 

| Parameter   | Description               |
| ------ | ------------------ |
| nCount | The number of mix audio streams. Maximum value: 20. |



## Advanced Room APIs

### Setting the audio type of the room

If `SetForceUseMediaVol` is used before a user enters the room, the room with the smooth sound quality or standard sound quality can use the media volume.

```
[[ITMGContext GetInstance] SetAdvanceParams:SetForceUseMediaVol value:1]
```

#### value

Different values indicate different features:
- 0: Both voice room types 1 and 2 still use the call volume after the mic is enabled.
- 1: Voice room type 1 uses the media volume after the mic is enabled (the call volume is used before).
- 2: Voice room type 2 uses the media volume after the mic is enabled (the call volume is used before).

### Getting the speaking volume level of a member in the room

After the `TrackingVolume` API is called, it will listen on the `TIMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_USER_VOLUMES` event where the key-value pair is `uin-volume`. Through this API, the corresponding energy column chart can be generated based on the volume level of a `uin` speaking in the room.

If you no longer need to get the speaking volume level of the member in the room, call the `StopTrackingVolume` API.

```
//TMGAudioCtrl
public int TrackingVolume(float fTrackingTimeS)
public int StopTrackingVolume();
```

| Parameter           | Type  | Description                        |
| -------------- | ----- | --------------------------- |
| fTrackingTimeS | float | The number of seconds of the listening. `0.5f` is recommended. |

## General Advanced APIs
### Passing in `openid` as a string
>! This API takes effect on GME SDK 2.9.3 or later.

Currently, the GME SDK only supports passing in numbers to it as strings. To pass in `openid` as a string, you need to call the following API before calling the `Init` API:
```
SetAdvanceParams("StringOpenID", "1");
```

### Modifying the print log size

<dx-alert infotype="explain" title="description">
This API takes effect on GME SDK 2.8.4 or later.
</dx-alert>

Call this API before the GME `Init` API to modify the default log file size. Currently, a single log file is 50 MB, and there can be up to three log files.

#### Function prototype

```
SetAdvanceParams(const char* key, const char* object)
```

| Parameter   | Type        | Description                                                         |
| ------ | ----------- | ------------------------------------------------------------ |
| key    | const char* | `MAX_LOG_FILE_SIZE_MB` and `MAX_LOG_FILE_COUNT` indicate the size of a single log and the number of logs respectively. |
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

### Text translation API

This API is used to translate text. You can translate Chinese text into English. After this API is called, the result will be returned through the callback. Take the C++ API as an example.

>!This API is only available to allowed users on SDK 291 or later. If you want to use it, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

#### Function prototype

```
virtual int TranslateText(const char* text, const char* sourceLanguage, const char* translateLanguage) = 0;
```

| Parameter              | Type        | Description                                                         |
| ----------------- | ----------- | ------------------------------------------------------------ |
| text              | const char* | Text to be translated, which cannot be empty and can contain up to 5,000 characters.                     |
| sourceLanguage    | const char* | The language of the text to be translated, which can be empty and will be detected automatically by the backend.              |
| translateLanguage | const char* | The language into which the text is to be translated, which cannot be empty. Multiple languages need to be separated by comma, such as `cmn-Hans-CN,en-GB` or `cmn-Hans-CN`. |

For language parameters, see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260).

#### API callback

| Parameter       | Type                            | Description  |
| ---------- | ------------------------------- | ------------------------------------------------------------ |
| code       | int                             | Error code. `0` indicates success. For other returned codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/607/33223) for solutions. |
| targetText | jason(return string format in Unity) | Translated target text, e.g., `{"target_text":[{"target_language_code": "cmn-Hans-CN", "target_text": "I am Chinese"},{" target_language_code": "de-DE", "target_text": "Ich bin Chinese"}]}` |

#### Unity project sample code

1. Add a listener
```
ITMGContext.GetInstance().GetPttCtrl().OnTranslateTextComplete+= OnTranslateTextComplete;
```

2. Call the API
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

3. Process the callback
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

4. Remove the listener
```
ITMGContext.GetInstance().GetPttCtrl().OnTranslateTextComplete-= OnTranslateTextComplete;
```

### Text-to-speech API

This API is used to convert text into audio. After this API is called, the audio `fileid` will be returned through the callback. You can use the `DownloadRecordedFile` API to download the audio. Here, the C++ API is used as an example.

>!This API is only available to allowed users on SDK 291 or later. If you want to use it, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

#### Function prototype

```
virtual int TextToSpeech(const char* text, const char* voiceName,const char* languageCode, float speakingRate) = 0;
```

| Parameter         | Type        | Description                                           |
| ------------ | ----------- | ---------------------------------------------- |
| text         | const char* | Source text, which cannot be empty and can contain up to 5,000 characters.           |
| voiceName    | const char* | Voice type. Samples in English and Mandarin are provided. To get samples in other languages, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application. |
| languageCode | const char* | Target language, which cannot be empty.                         |
| speakingRate | float       | Speech speed. Value range: 0.6–1.5. `1` indicates the normal speed.     |

Valid values of `voiceName`:

| Voice Type | Gender | Language |
|---------|---------|---------|
| cmn-CN-Standard-A | Female | Mandarin |
| cmn-CN-Standard-B | Male | Mandarin |
| en-US-Neural2-A | Female | American English |
| en-US-Neural2-B | Male | American English |

For language parameter, please see [Language parameter list](https://intl.cloud.tencent.com/document/product/607/30260).

#### Callback API

| Parameter | Type | Description |
| ------ | ------ | ------------------------------------------------------------ |
| code   | int    | Error code. `0` indicates success. For other returned codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/607/33223) for solutions. |
| isCos  | bool   | Whether the file is uploaded to COS                                            |
| fileID | string | File ID, which is the input parameter for audio file download through the `DownloadRecordedFile` API. |

#### Unity project sample code

1. Add a listener
```
ITMGContext.GetInstance().GetPttCtrl().OnTextToSpeechComplete += new QAVTextToSpeechCallback(TextToSpeechComplate);
```

2. Call the API
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

3. Process the callback
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

4. Remove the listener
```
ITMGContext.GetInstance().GetPttCtrl().OnTextToSpeechComplete -= new QAVTextToSpeechCallback(TextToSpeechComplate);
```
