This document provides FAQs about Game Multimedia Engine (GME) SDK to make it easier for developers to debug and integrate the advanced APIs for GME.

<dx-alert infotype="alarm" title="Invoking notes">
This document describes advanced APIs that don't need to be called unless necessary. Consult GME developers before calling.
</dx-alert>

## Advanced Audio APIs

### iOS Audio API

The SetAdvanceParams API is used to enable/disable the following audio options before a user enters a room. 

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
  to mix audio. Once enabled, GME can run the background music and voice chat at the same time.
- **OptionDuckOthers**
  to duck background music. If both this option and `OptionMixWithOthers` are enabled, the speaker will be enabled to broadcast audio while the background music volume is ducked.
- **ReleaseAudioFoucus**
  to release audio focus.
- If enabled, audio focus will be released when you exit a room so that other audio apps such as QQ Music can continue running.
- If disabled, other audio apps cannot continue running when you exit a room.

### Checking whether the Ring/Silent switch of iPhone is on

<dx-alert infotype="explain" title="description">
This API takes effect on GME SDK 2.8.4 or above.
</dx-alert>

#### Function prototype

```
CheckDeviceMuteState();
```

The returned value of 0 means that the Ring/Silent switch is off, while 1 means on.


### Setting Android Bluetooth device adaptation

<dx-alert infotype="explain" title="description">
This API takes effect on GME SDK 2.8.4 or above.
</dx-alert>

Calling this API can solve the problem of sound leak when the mic on Bluetooth earphones is switched on/off, as well as the problem of playing back audio with the speaker after the connection status is changed after an Android device is connected to the Bluetooth earphones.

```
SetAdvanceParams("BluetoothUseMedia", "1");
```

### Setting the Maximum Number of the Mix Audio Channels

The `SetRecvMixStreamCount` API is used to set the maximum number of the mix audio streams before a user enters a room. This API can be used on all platforms. Here, take the `SetRecvMixStreamCount` API for PC as an example.

```
virtual int SetRecvMixStreamCount(int nCount) = 0;
```

**Parameter description** 

| Parameter   | Description               |
| ------ | ------------------ |
| nCount | The number of mix audio channels, up to 20 channels |



## Room Management Advanced APIs

### Setting the Audio Type of the Room

If SetForceUseMediaVol is used before a user enters the room, the room with smooth sound quality or standard sound quality can use the media volume.

```
[[ITMGContext GetInstance] SetAdvanceParams:SetForceUseMediaVol value:1]
```

#### value

Different values indicate different features:
- 0: Both audio room type 1 and 2 revert to the call volume with the microphone on.
- 1: The volume of audio room type 1 changes into media volume(from call volume).
- 2: The volume of audio room type 2 changes into media volume(from call volume).

### Obtaining the Speaking Volume of a Member in the Room

After the TrackingVolume API is called, it will monitor the `TIMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_USER_VOLUMES` event where the key-value pair is uin-volume. Through this API, the corresponding energy histogram can be generated based on the volume of a uin speaking in the room.

If you no longer need to obtain the speaking volume of the member in the room, please call the StopTrackingVolume API.

```
//TMGAudioCtrl
public int TrackingVolume(float fTrackingTimeS)
public int StopTrackingVolume();
```

| Parameter | Type | Description |
| -------------- | ----- | --------------------------- |
| fTrackingTimeS | float | The number of seconds of the listening. `0.5f` is recommended. |

## General Advanced APIs
### Passing in `openid` as a string
>! This API takes effect on GME SDK 2.9.3 or later.

Currently, the GME SDK only supports passing in numbers to it as strings. To pass in `openid` as a string, you need to call the following API before calling the `Init` API:
```
SetAdvanceParams("StringOpenID", "1");
``` 

### Fixing print log size

<dx-alert infotype="explain" title="description">
This API takes effect on GME SDK 2.8.4 or above.
</dx-alert>

Call this API before the GME `Init` API to modify the default log file size. Currently, a single log file is 50 MB, and there can be up to 3 log files.

#### Function prototype

```
SetAdvanceParams(const char* key, const char* object)
```

| Parameter | Type | Description |
| ------ | ----------- | ------------------------------------------------------------ |
| key    | const char* | `MAX_LOG_FILE_SIZE_MB` and `MAX_LOG_FILE_COUNT` represent the size of a single log and the number of logs, respectively. |
| object | const char* | When `key` is `MAX_LOG_FILE_SIZE_MB`, `object` is the default log file size, which can be 5 to 50 M. When `key` is `MAX_LOG_FILE_COUNT`, `object` is the default number of log files, which can be 1 to 3. |

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

This API is used to translate text. You can translate a Chinese text into English. Call the API to return results through callback. Take C++ API for example.

>! This API is only available to allow-list user on SDK 291 version. If you need to apply, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

#### Function prototype

```
virtual int TranslateText(const char* text, const char* sourceLanguage, const char* translateLanguage) = 0;
```

| Parameter | Type | Description |
| ----------------- | ----------- | ------------------------------------------------------------ |
| text              | const char* | Text to be translated, not null, maximum length 5000 characters                     |
| sourceLanguage    | const char* | Specify the language of the text to be translated, can be null, background automatically detects the voice               |
| translateLanguage | const char* | Specify the translated language of the text, not null, with English commas as interval, such as "cmn-Hans-CN,en-GB", "cmn-Hans-CN" |

For language parameter, please see [Language parameter list](https://intl.cloud.tencent.com/document/product/607/30260).

#### Callback API

| Parameter       | Type                            | Description  |
| ---------- | ------------------------------- | ------------------------------------------------------------ |
| code       | int                             | Error code, 0 indicates success. Other returns, please refer to [error code](https://intl.cloud.tencent.com/document/product/607/33223).
| targetText | jason(return string format in Unity) | translated target text, e.g. {"target_text":[{"target_language_code": "cmn-Hans-CN", "target_text": "I am Chinese"},{" target_language_code": "de-DE", "target_text": "Ich bin Chinese"}]} |

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

>! This API is only available to allow-list user on SDK 291 version. If you need to apply, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

#### Function prototype

```
virtual int TextToSpeech(const char* text, const char* voiceName,const char* languageCode, float speakingRate) = 0;
```

| Parameter | Type | Description |
| ------------ | ----------- | ---------------------------------------------- |
| text         | const char* | Original text, not null, maximum length 5000 characters           |
| voiceName    | const char* | Voice type. Samples in English and Mandarin are provided. To get samples in other languages, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application. |
| languageCode | const char* | Specify the target language. Not null                         |
| speakingRate | float       | audio speed, range [0.6-1.5], 1 is the normal speed     |

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
| code   | int    | error code, 0 indicates success. Other returning codes, please refer to [error code](https://intl.cloud.tencent.com/document/product/607/33223) |
| isCos  | bool   | File uploaded to COS?                                            |
| fileID | string | File ID, provide downloading API, you can download the audio through DownloadRecordedFile API |

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
