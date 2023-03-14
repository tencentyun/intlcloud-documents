This document describes how to integrate with and debug GME client APIs for the voice messaging and speech-to-text services for Electron.

## Key Considerations for Using GME

GME provides the real-time voice service and voice messaging and speech-to-text services, which all depend on core APIs such as `Init` and `Poll`.

#### Notes

- You have created a GME application and obtained the SDK `AppID` and key. For more information, see [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- You have activated **GME real-time voice service and voice messaging and speech-to-text services**. For more information, see [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- Configure your project before using GME; otherwise, the SDK will not take effect.
- After a GME API is called successfully, `GmeError.AV_OK` will be returned with the value being `0`.
- GME APIs should be called in the same thread.
- The `Poll` API should be called periodically for GME to trigger event callbacks.
- For detailed error codes, see <dx-tag-link link="https://cloud.tencent.com/document/product/607/15173" tag="ErrorCode">Error Codes</dx-tag-link>.

<dx-alert infotype="notice" title="">
There is a default call rate limit for speech-to-text APIs. For more information on how calls are billed within the limit, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009). If you want to increase the limit or learn more about how excessive calls are billed, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1).
- Non-streaming speech-to-text API **PttSpeechToText()**: There can be up to 10 concurrent requests per account.
- Streaming speech-to-text API **PttStartRecordingWithStreamingRecognition()**: There can be up to 50 concurrent requests per account.
</dx-alert>

## Integrating the SDK

### Directions

Key processes involved in SDK integration are as follows:

<img src="https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg"  width="70%" /></img>

<dx-steps>
-<dx-tag-link link="#Init" tag="API: Init">Initializing GME</dx-tag-link>
-<dx-tag-link link="#Poll" tag="API: Poll">Calling Poll periodically to trigger event callbacks</dx-tag-link>
-<dx-tag-link link="#ApplyPtt" tag="API: ApplyPTTAuthbuffer">Initializing authentication</dx-tag-link>
-<dx-tag-link link="#StartRWSR" tag="API: PttStartRecordingWithStreamingRecognition">Starting streaming speech recognition</dx-tag-link>
-<dx-tag-link link="#Stop" tag="API: PttStopRecording">Stopping recording</dx-tag-link>
-<dx-tag-link link="#UnInit" tag="API: UnInit">Uninitializing GME</dx-tag-link>
</dx-steps>

### TS class

```
`GmeContext`: GME business implementation APIs
`GmeError`: GME error code definition class
```

## Core APIs

| API | Description |
| ------ | :----------: |
| Init | Initializes GME |
| Poll | Triggers event callback |
| Uninit | Uninitializes GME |

### Importing the GME module

```
const { GmeContext } = require('gme-electron-sdk');
```

### Getting an instance

var m_context = new GmeContext();

[](id:Init)
### Initializing the SDK

**You need to initialize the SDK through the `Init` API** before you can use the real-time voice, voice message, and speech-to-text services. The `Init` API must be called in the same thread as other APIs. We recommend you call all APIs in the main thread.

#### API prototype

```
Init(appid: string, openid: string): number;
```

| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | string | `AppID` provided in the [GME console](https://console.cloud.tencent.com/gamegme), which can be obtained as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0). |
| openID   | string | `openID` can only be in `Int64` type, which is passed in after being converted to a string. You can customize its rules, and it must be unique in the application. To pass in `openID` as a string, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1) for application. |

#### Returned values

| Returned Value | Description |
| ------------------------------- | --------------------------------------------- |
| GmeError.AV_OK= 0                  | Initialized the SDK successfully. |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | Checks whether the SDK file is complete. It is recommended to delete it and then import the SDK again. |

<dx-alert infotype="notice" title="Notes on 7015 error code">

- The 7015 error code is judged by MD5. If this error is reported during integration, please check the integrity and version of the SDK file as prompted.
- The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is **only a reminder** but will not cause an initialization failure.
  </dx-alert>

#### Sample code 

```
number ret = m_context.Init(sdkAppId, openID);
// Determine whether the initialization is successful by the returned value
if (ret != GmeError.AV_OK)
{
	 console.log("Failed to initialize the SDK:");
		return;
}
```

[](id:Poll)
### Triggering event callback

Event callbacks can be triggered by calling the `Poll` API in the timer. The `Poll` API is GME's message pump and should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run abnormally. For more information, see the `EnginePollHelper` file in [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).

<dx-alert infotype="notice" title="">
The `Poll` API must be called periodically and in the main thread to avoid abnormal API callbacks.
</dx-alert>

#### API prototype

```
Poll();
```

#### Sample code

```
setInterval(function () {
      m_context.Poll();
    }, 50);
```

[](id:UnInit)
### Uninitializing SDK

This API is used to uninitialize the SDK to make it uninitialized. **If the game business account is bound to `openid`, switching game account requires uninitializing GME and then using the new `openid` to initialize again.**

#### API prototype

```
Uninit() : number
```

## Voice Messaging and Speech-to-Text Services

<dx-alert infotype="explain" title="">

- The speech-to-text service consists of fast recording-to-text conversion and streaming speech-to-text conversion.
- You do not need to enter a voice chat room when using the voice messaging service.
- The maximum recording duration of a voice message is 58 seconds by default, and the minimum recording duration cannot be less than 1 second. If you want to customize the recording duration, for example, to modify the maximum recording duration to 10 seconds, call the `SetMaxMessageLength` API to set it after initialization.
  </dx-alert>

### Flowchart for using the voice message service

<img src="https://qcloudimg.tencent-cloud.cn/raw/24c16c71cb2fcc6cf170a6b481067564.jpg" width="80%">

### Flowchart for using the speech-to-text service

<img src="https://qcloudimg.tencent-cloud.cn/raw/8269f413756379d574a2969ac8da0158.jpg" width="80%">

| API                        |            Description            |
| ------------------- | :------------------: |
| GenAuthBuffer | Gets the authentication information |
| SetMaxMessageLength | Specifies the maximum length of voice message |




### Generating the local authentication key

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    

#### API prototype

```
GenAuthBuffer(appId: string,roomId: string, openId:string, appKey: string) :string
```

| Parameter | Type | Description |
| ------ | :----: | ------------------------------------------------------------ |
| appId  |  string   | `AppId` from the Tencent Cloud console.|
| roomId | string | Enter `null` or an empty string                                      |
| openId | string | User ID, which is the same as `OpenId` during initialization. |
| key | string | Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme). |

### Application authentication

After the authentication information is generated, the authentication is assigned to the SDK.  

#### API prototype  

```
ApplyPTTAuthbuffer(authBuffer: string) :number
```

| Parameter   | Type | Description                                            |
| ------ | :--: | ----------------------------------------------- |
| authBuffer | string  | Authentication information |

#### Sample code

```
var authBuffer = m_context.GetAuthBuffer(UserConfig.GetAppID(), UserConfig.GetUserID(), null,UserConfig.GetAuthKey());
m_context.ApplyPTTAuthbuffer(authBuffer);
```

### Specifying the maximum duration of voice message

This API is used to specify the maximum duration of a voice message, which can be up to 58 seconds.

#### API prototype

```
PttSetMaxMessageLength(msTime: number) :number
```

| Parameter   | Type | Description                                            |
| ------ | :--: | ----------------------------------------------- |
| msTime | number  | Audio duration in ms. Value range: 1000 < `msTime` <= 58000 |

#### Sample code  

```
m_context.PttSetMaxMessageLength(58000); 
```

## Streaming Speech Recognition



### Voice messaging and speech-to-text APIs

| API | Description |
| -------------------------------------- | :----------: |
| PttStartRecordingWithStreamingRecognition | Starts streaming recording |
| PttStopRecording                          |   Stops recording |


[](id:StartRWSR)
### Starting streaming speech recognition

This API is used to start streaming speech recognition. Text obtained from speech-to-text conversion will be returned in real time in its callback. It can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation. **To stop recording, call <dx-tag-link link="#Stop" tag="API: PttStopRecording"> Stop recording</dx-tag-link>**.

#### API prototype  

```
PttStartRecordingWithStreamingRecognition(filePath: string, speechLanguage: string, translateLanguage: string) :number
```

| Parameter | Type | Description |
| ----------------- | :----: | ------------------------------------------------------------ |
| filePath          | string | Path of stored audio file |
| speechLanguage    | string | The language in which the audio file is to be converted to text. For parameters, see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260). |
| translateLanguage | string | The language in which the audio file is to be translated to text. For parameters, see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260). |

#### Sample code  

```
string filePath = "xx/xxx/xxx.silk"
var ret = m_context.StartRecordingWithStreamingRecognition(filePath,"cmn-Hans-CN","cmn-Hans-CN");
if (ret == 0) {
    this.currentStatus = "Start streaming recording";
} else {
    this.currentStatus = "Failed to start streaming recording";
}
```

> ! Translation incurs additional fees. For more information, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009).
### Callback for streaming speech recognition

After streaming speech recognition is started, you need to listen on callback messages in the `OnEvent` notification, which is as detailed below:

`ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE` returns text after the recording is stopped and the recognition is completed, which is equivalent to returning the recognized text after a paragraph of speech.
`ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING` returns the recognized text in real time during the recording, which is equivalent to returning the recognized text while speaking.

The event message will be identified in the callback notification based on the actual needs. The passed parameters include the following four messages.

| Message Name | Description |
| --------- | :---------------------------------------------: |
| result    |      Return code indicating whether streaming speech recognition is successful     |
| text      |              Text converted from speech             |
| file_path |             Local path of stored recording file              |
| file_id | Backend URL address of recording file, which will be retained for 90 days |



<dx-alert infotype="notice" title="">
The file_id is empty when the 'ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRecognition_IS_RUNNING' message is listened.
</dx-alert>

#### Error codes

| Error Code | Description | Suggested Solution |
| ------ | :--: | :------: |
| 32775 | Streaming speech-to-text conversion failed, but recording succeeded.| Call the `UploadRecordedFile` API to upload the recording file and then call the `SpeechToText` API to perform speech-to-text conversion. |
| 32777 | Streaming speech-to-text conversion failed, but recording and upload succeeded.| The message returned contains a backend URL after successful upload. Call the `SpeechToText` API to perform speech-to-text conversion. |
| 32786 | Streaming speech-to-text conversion failed. | During streaming recording, wait for the execution result of the streaming recording API to return. |
| 32787     | Speech-to-text conversion succeeded, but the text translation service was not activated.         | Activate the text translation service in the console.                                 |
| 32788     | Speech-to-text conversion succeeded, but the language parameter of the text translation service was invalid.         | Check the parameter passed in.                                 |

If the error code 4098 is reported, see [Speech-to-text Conversion](https://www.tencentcloud.com/document/product/607/39716) for solutions.

#### Sample code  

```
m_context.setTMGDelegate(function(eventId, msg){
   switch (eventType) {
                    case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
                    {
                        HandleSTREAM2TEXTComplete(data,true);
                        break;
                        }
                    ...
                            case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING:
                    {
                        HandleSTREAM2TEXTComplete(data, false);
                        break;
                    }
                }
});

```

## Voice Message Recording

**The recording process is as follows: start recording > stop recording > return recording callback > start the next recording.**

### Voice messaging and speech-to-text APIs

| API | Description |
| --------------- | :------: |
| PttStartRecording  | Starts recording |
| PttPauseRecording  | Pauses recording |
| PttResumeRecording | Resumes recording |
| PttStopRecording   | Stops recording |
| PttCancelRecording | Cancels recording |



### Starting recording

This API is used to start recording.

#### API prototype  

```
PttStartRecording(filePath: string) : number;
```

| Parameter    |  Type  | Description           |
| ------- | :----: | -------------- |
| filePath | string | Path of stored audio file |

#### Sample code  

```
string filepath = "xxxx/xxx.silk";
var ret = m_context.PttStartRecording(filepath);
```

[](id:Stop)
### Stopping recording

This API is used to stop recording. It is async, and a callback for recording completion will be returned after recording stops. A recording file will be available only after recording succeeds.

#### API prototype  

```
PttStopRecording() :number;
```

#### Sample code  

```
m_context.PttStopRecording();
```

### Callback for recording start

A callback will be executed through a delegate function to pass a message when recording is completed.

**To stop recording, call `StopRecording`**. The callback for recording start will be returned after the recording is stopped.


| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| code | string | 0: Recording is completed |
| filepath | string | Path of stored recording file, which must be accessible and cannot be the `fileid` |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ------------------------ | ------------------------------------------------------------ |
| 4097 | Parameter is empty. | Check whether the API parameters in the code are correct. |
| 4098 | Initialization error. | Check whether the device is being used, whether the permissions are normal, and whether the initialization is normal. |
| 4099 | Recording is in progress. | Ensure that the SDK recording feature is used at the right time. |
| 4100 | Audio data is not captured. | Check whether the mic is working properly. |
| 4101 | An error occurred while accessing the file during recording. | Ensure the existence of the file and the validity of the file path. |
| 4102 | The mic is not authorized. | Mic permission is required for using the SDK. To add the permission, see the SDK project configuration document for the corresponding engine or platform. |
| 4103 | The recording duration is too short. | The recording duration should be in ms and longer than 1,000 ms. |
| 4104 | No recording operation is started. | Check whether the recording starting API has been called. |

#### Sample code  

```
m_context.setTMGDelegate(function(eventId, msg){
   switch (eventType) {
                    case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
                    {
                    // Process
                    break;
                        }
                    ...
                            case ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE:
                    {
                    // Process
                    break;
                    }
                }
});


```

### Pausing recording

This API is used to pause recording. If you want to resume recording, call the `PttResumeRecording` API.

#### API prototype  

```
PttPauseRecording() : number
```

#### Sample code  

```
number ret = m_context.PttPauseRecording();
```

### Resuming recording

This API is used to resume recording.

#### API prototype  

```
PttResumeRecording() : number;
```

#### Sample code  

```
number ret = m_context.PttResumeRecording();
```



### Canceling recording

This API is used to cancel recording. **There is no callback after cancellation**.

#### API prototype  

```
PttCancelRecording() : number
```

#### Sample code  

```
m_context.PttCancelRecording();
```


## Voice Message Upload, Download, and Playback

| API | Description |
| -------------------- | :------------: |
| PttUploadRecordedFile   |  Uploads an audio file |
| PttDownloadRecordedFile |  Downloads an audio file |
| PttPlayRecordedFile     |    Plays back an audio file |
| PttStopPlayFile         |  Stops playing back an audio file |
|  PttGetFileSize          | Gets the audio file size |
|  PttGetVoiceFileDuration | Gets the audio file duration|

### Uploading an audio file

This API is used to upload an audio file.

#### API prototype  

```
PttUploadRecordedFile(filePath: string) : number
```

| Parameter     |  Type  | Description                             |
| -------- | :----: | -------------------------------- |
| filePath | String | Path of uploaded audio file, which is a local path. |

#### Sample code  

```
var ret = m_context.PttUploadRecordedFile(filePath);
```

### Callback for audio file upload completion

After the audio file is uploaded, the event message `ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE` will be returned, which will be identified in the `OnEvent` function.
The passed parameters include `result`, `file_path`, and `file_id`.

| Parameter | Type | Description |
| ----------------- | :----: | ------------------------------------------------------------ |
| result          | number | `0`: Recording is completed |
| filepath          | string | Path of stored recording file |
| fileid          | string | File URL |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ------------------------------ | ------------------------------------------------------ |
| 8193 | An error occurred while accessing the file during upload. | Ensure the existence of the file and the validity of the file path. |
| 8194 | Signature verification failed. | Check whether the authentication key is correct and whether the voice message and speech-to-text feature is initialized. |
| 8195 | A network error occurred. | Check whether the device can access the internet. |
| 8196 | The network failed while getting the upload parameters. | Check whether the authentication is correct and whether the device can access the internet. |
| 8197 | The packet returned during the process of getting the upload parameters is empty. | Check whether the authentication is correct and whether the device network can normally access the internet. |
| 8198 | Failed to decode the packet returned during the process of getting the upload parameters. | Check whether the authentication is correct and whether the device can access the internet. |
| 8200 | No `appinfo` is set. | Check whether the `apply` API is called or whether the input parameters are empty. |

#### Sample code

```
m_context.setTMGDelegate(function(eventId, msg){
 switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
            {
            // Process
            break;
                }
            ...
                    case ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE:
            {
            // Process
            break;
            }
        }
});
```

### Downloading the audio file

This API is used to download an audio file.

#### API prototype  

```
PttDownloadRecordedFile(fileId: string, filePath: string) : number
```

| Parameter | Type | Description |
| ---------------- | :----: | ------------------------------------------------------------ |
| fileId           | string | File URL |
| filePath | string | Local path of saved file, which must be accessible and cannot be the `fileid` |

#### Sample code  

```
var ret = m_context.PttDownloadRecordedFile(fileID,filePath);
```

### Callback for audio file download completion

After the audio file is downloaded, the event message `ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE` will be returned, which will be identified in the `OnEvent` function.
The passed parameters include `result`, `file_path`, and `file_id`.

| Parameter | Type | Description |
| ----------------- | :----: | ------------------------------------------------------------ |
| result          | number | `0`: Download is completed |
| filepath          | string | Path of stored recording file |
| fileid          | string | URL of recording file, which will be retained on the server for 90 days. |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | --------------------------------- | ------------------------------------------------------------ |
| 12289 | An error occurred while accessing the file during download. | Check whether the file path is valid. |
| 12290 | Signature verification failed. | Check whether the authentication key is correct and whether the voice message and speech-to-text feature is initialized. |
| 12291 | Network storage system exception. | The server failed to get the audio file. Check whether the API parameter `fileid` is correct, whether the network is normal, and whether the file exists in COS. |
| 12292 | Server file system error. | Check whether the device can access the internet and whether the file exists on the server. |
| 12293 | The HTTP network failed during the process of getting the download parameters. | Check whether the device can access the internet. |
| 12294 | The packet returned during the process of getting the download parameters is empty. | Check whether the device can access the internet. |
| 12295 | Failed to decode the packet returned during the process of getting the download parameters. | Check whether the device can access the internet. |
| 12297 | No `appinfo` is set. | Check whether the authentication key is correct and whether the voice message and speech-to-text feature is initialized. |

#### Sample code

```
m_context.setTMGDelegate(function(eventId, msg){
 switch (eventType) {
           case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
            {
            // Process
            break;
             }
        }
});
```

### Playing back audio

This API is used to play back audio.

#### API prototype  

```
PttPlayRecordedFile(filePath: string, voiceType: ITMG_VOICE_TYPE) : number
```

| Parameter      |  Type  | Description                                                         |
| --------- | :----: | ------------------------------------------------------------ |
| filePath | string | Local audio file path |
| voicetype |  ITMG_VOICE_TYPE | Voice changer type. For more information, see [Voice Changing](https://www.tencentcloud.com/document/product/607/44995). |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ---------- | ------------------------------ |
| 20485 | Playback is not started. | Ensure the existence of the file and the validity of the file path. |

#### Sample code  

```
m_context.PlayRecordedFile(filePath); 
```

### Callback for audio playback

After the audio is played back, the event message `ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE` will be returned, which will be identified in the `OnEvent` function.
The passed parameter includes `result` and `file_path`.

| Parameter | Type | Description |
| ----------------- | :----: | ------------------------------------------------------------ |
| code          | number | `0`: Playback is completed |
| filepath          | string | Path of stored recording file |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| 20481 | Initialization error. | Check whether the device is being used, whether the permissions are normal, and whether the initialization is normal. |
| 20482 | During playback, the client tried to interrupt and play back the next one but failed (which should succeed normally). | Check whether the code logic is correct. |
| 20483 | Parameter is empty. | Check whether the API parameters in the code are correct. |
| 20484 | Internal error. | An error occurred while initializing the player. This error code is generally caused by failure in decoding, and the error should be located with the aid of logs. |

#### Sample code

```
m_context.setTMGDelegate(function(eventId, msg){
 switch (eventType) {
		case ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE:
		{
		// Process
		break;
		 }
		}
});
```



### Stopping audio playback

This API is used to stop audio playback. There will be a callback for playback completion when the playback stops.

#### API prototype  

```
PttStopPlayFile() : number
```

#### Sample code  

```
m_context.PttStopPlayFile();
```


### Getting audio file size

This API is used to get the size of an audio file.

#### API prototype  

```
PttGetFileSize(filePath: string) : number
```

| Parameter     |  Type  | Description                             |
| -------- | :----: | -------------------------------- |
| filePath | string | Path of audio file, which is a local path |

#### Sample code  

```
m_context.PttGetFileSize(filePath);
```

### Getting audio file duration

This API is used to get the duration of an audio file in milliseconds.

#### API prototype  

```
PttGetVoiceFileDuration(filePath: string) : number
```

| Parameter     |  Type  | Description                             |
| -------- | :----: | -------------------------------- |
| filePath | string | Path of audio file, which is a local path |

#### Sample code  

```
number fileDuration = m_context.PttGetVoiceFileDuration(filePath);
```


## Fast Recording-to-Text Conversion

### Translating audio file into text in specified language

This API can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation.

>!Translation incurs additional fees. For more information, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009).
>
>#### API prototype  

```
PttSpeechToText(fileID: string, speechLanguage: string, translateLanguage: string) : number
```

| Parameter | Type | Description |
| ----------------- | :----: | ------------------------------------------------------------ |
| fileID            | string | URL of audio file, which will be retained on the server for 90 days |
| speechLanguage    | string | The language in which the audio file is to be converted to text. For parameters, see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260). |
| translatelanguage | string | The language in which the audio file is to be translated to text. For parameters, see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260). |

#### Sample code  

```
m_context.PttSpeechToText(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```



### Callback for recognition

After the specified audio file is converted to text, the event message ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE will be returned, which will be identified in the `OnEvent` function.
The passed parameters include `result`, `file_path` and `text` (recognized text).


| Parameter | Type | Description |
| ----------------- | :----: | ------------------------------------------------------------ |
| result          | number | `0`: Recording is completed |
| fileid          | string | URL of recording file, which will be retained on the server for 90 days |
| text          | string | Converted text |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ---------------------------------- | ------------------------------------------------------------ |
| 32769 | An internal error occurred. | Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance. |
| 32770  | Network failed. | Check whether the device can access the internet. |
| 32772 | Failed to decode the returned packet. | Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance. |
| 32774 | No `appinfo` is set. | Check whether the authentication key is correct and whether the voice messaging and speech-to-text feature is initialized. |
| 32776 | `authbuffer` check failed. | Check whether `authbuffer` is correct. |
| 32784  | Incorrect speech-to-text conversion parameter. | Check whether the API parameter `fileid` in the code is empty. |
| 32785  | Speech-to-text translation returned an error. | Error with the backend of voice messaging and speech-to-text feature. Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance. |
| 32787     | Speech-to-text conversion succeeded, but the text translation service was not activated.         | Activate the text translation service in the console.                                 |
| 32788     | Speech-to-text conversion succeeded, but the language parameter of the text translation service was invalid.         | Check the parameter passed in.                                 |

#### Sample code

```
m_context.setTMGDelegate(function(eventId, msg){
 switch (eventType) {
         case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
            {
            // Process
            break;
                }
            ...
                    case ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE:
            {
            // Process
            break;
            }
});
```

## Voice Message Volume Level APIs

| API | Description |
| ---------------- | :----------------: |
| PttGetMicLevel      |  Gets real-time mic volume level |
| PttSetMicVolume     |    Sets recording volume level |
| PttGetMicVolume     |    Gets recording volume level |
| PttGetSpeakerLevel  | Gets real-time speaker volume level |
| PttSetSpeakerVolume |    Sets playback volume |
| PttGetSpeakerVolume |    Gets playback volume level |

### Getting the real-time mic volume of voice message

This API is used to get the real-time mic volume. A number-type value will be returned. Value range: 0–200.

#### API prototype  

```
PttGetMicLevel():number
```

#### Sample code  

```
m_context.PttGetMicLevel();
```

### Setting the recording volume of voice message

This API is used to set the recording volume of voice message. Value range: 0-200.

#### API prototype  

```
PttSetMicVolume(vol:number) :number
```

| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| vol | number | Value range: 0–200. Default value: `100`. `0` indicates that the audio is mute, while `100` indicates that the volume level remains unchanged. |

#### Sample code  

```
m_context.PttSetMicVolume(vol);
```

### Getting the recording volume of voice message

This API is used to get the recording volume of voice message. A number-type value will be returned. Value range: 0–200.

#### API prototype  

```
PttGetMicVolume() : number
```

#### Sample code  

```
m_context.PttGetMicVolume();
```

### Getting the real-time speaker volume of voice message

This API is used to get the real-time speaker volume. A number-type value will be returned. Value range: 0-200.

#### API prototype  

```
PttGetSpeakerLevel() : number;
```

#### Sample code  

```
m_context.PttGetSpeakerLevel();
```

### Setting the playback volume of voice message

This API is used to set the playback volume of voice message. Value range: 0-200.

#### API prototype  

```
PttSetSpeakerVolume(vol: number) : number
```

#### Sample code  

```
m_context.PttSetSpeakerVolume(100);
```

### Getting the playback volume of voice message

This API is used to get the playback volume of voice message. A number-type value will be returned. Value range: 0-200.

#### API prototype  

```
PttGetSpeakerVolume() : number
```

#### Sample code  

```
m_context.PttGetSpeakerVolume();
```

## Advanced APIs

### Getting version number

This API is used to get the SDK version number for analysis.

#### API prototype

```
GetSDKVersion() :string
```

#### Sample code  

```
string sdkVersion = m_context.GetSDKVersion();
```


### Setting log printing level

This API is used to set the level of logs to be printed, and needs to be called before the initialization. It is recommended to keep the default level.

#### API prototype

```
SetLogLevel(level: number) : number
```

#### Parameter description

| Parameter | Type | Description |
| ---------- | -------------- | ------------------------------------------------------------ |
| level | ITMG_LOG_LEVEL | Sets the log level. `TMG_LOG_LEVEL_NONE` indicates not to log. Default value: `TMG_LOG_LEVEL_INFO`. |

`level` description:

| Value of `level`       | Description                 |
| --------------------- | -------------------- |
| TMG_LOG_LEVEL_NONE | Does not print logs |
| TMG_LOG_LEVEL_ERROR | Prints error logs (default) |
| TMG_LOG_LEVEL_INFO | Prints info logs |
| TMG_LOG_LEVEL_DEBUG | Prints debug logs |
| TMG_LOG_LEVEL_VERBOSE | Prints verbose logs |

#### Sample code  

```
m_context.SetLogLevel(TMG_LOG_LEVEL_INFO);
```



### Setting the log printing path

This API is used to set the log printing path. The default path is as follows. It needs to be called before Init.

| OS | Path |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\GMEGLOBAL\GME\ProcessName                           |

#### API prototype

```
SetLogPath(logPath: string)
```

| Parameter | Type | Description |
| ------ | :----: | ---- |
| logPath | string | Path |

#### Sample code  

```
string logDir = ""// Set a path by yourself
m_context.SetLogPath(logDir);
```
