This document describes how to integrate with and debug GME client APIs for the voice messaging and speech-to-text services for Flutter.

## Key Considerations for Using GME

GME provides the real-time voice service and voice messaging and speech-to-text services, which all depend on core APIs such as `Init` and `Poll`.

#### Notes
- You have created a GME application and obtained the SDK `AppID` and key. For more information, see [Activating Services](https://www.tencentcloud.com/document/product/607/10782).

- You have activated **GME real-time voice and voice messaging and speech-to-text services**. For more information, see [Activating Services](https://www.tencentcloud.com/document/product/607/10782).

- Configure your project before using GME; otherwise, the SDK will not take effect.

- After a GME API is called successfully, `GmeError.AV_OK` will be returned with the value being `0`.

- GME APIs should be called in the same thread.

- The `Poll` API should be called periodically for GME to trigger event callbacks.

- For detailed error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/607/33223).
  

   > **Note**
   > 

   > There is a default call rate limit for speech-to-text APIs. For more information on how calls are billed within the limit, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009). If you want to increase the limit or learn more about how excessive calls are billed, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1).
   > 
>   - Non-streaming speech-to-text API ***SpeechToText()***: There can be up to 10 concurrent requests per account.
>   - Streaming speech-to-text API ***StartRecordingWithStreamingRecognition()***: There can be up to 50 concurrent requests per account.


## Integrating the SDK

### Directions

Key processes involved in SDK integration are as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg)

1. [Initializing GME](https://www.tencentcloud.com/document/product/607/53819)

2. [Call `Poll` periodically to trigger event callbacks](https://www.tencentcloud.com/document/product/607/53819).

3. [Initialize authentication](https://www.tencentcloud.com/document/product/607/53819).

4. [Start streaming speech recognition](https://www.tencentcloud.com/document/product/607/53819).

5. [Stop recording](https://www.tencentcloud.com/document/product/607/53819).

6. [Uninitialize GME](https://www.tencentcloud.com/document/product/607/53819).


### .dart files
``` bash
gme.dart      GME business implementation APIs
gmeType.dart  GME type definition file
gmeError.dart GME error type definition file
```

## Core APIs
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >InitSDK</td>

<td rowspan="1" colSpan="1" >Initializes GME.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Poll</td>

<td rowspan="1" colSpan="1" >Triggers the event callback.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Uninit</td>

<td rowspan="1" colSpan="1" >Uninitializes GME.</td>
</tr>
</table>


### Importing the GME module
``` bash
import 'package:gme/gme.dart';
import 'package:gme/gmeType.dart';
```

### Getting an instance

var m_context = await ITMGContext.GetInstance();

### Initializing the SDK

**You need to initialize the SDK through the `Init` API** before you can use the real-time voice chat, voice messaging, and speech-to-text services. The `Init` API must be called in the same thread as other APIs. We recommend you call all APIs in the main thread.

#### API prototype
``` bash
Future<int> InitSDK(String appID, String openID)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sdkAppId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`AppID` provided in the [GME console](https://console.cloud.tencent.com/gamegme), which can be obtained as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openID</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`openID` can only be in `Int64` type, which is passed in after being converted to a string. You can customize its rules, and it must be unique in the application. To pass in `openID` as a string, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1) for application.</td>
</tr>
</table>


#### Returned values
<table>
<tr>
<td rowspan="1" colSpan="1" >Returned Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GmeError.AV_OK= 0</td>

<td rowspan="1" colSpan="1" >SDK initialized successfully.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >AV_ERR_SDK_NOT_FULL_UPDATE=7015</td>

<td rowspan="1" colSpan="1" >Solution: Check whether the SDK file is complete. We recommend that you delete it and then import the SDK again.</td>
</tr>
</table>


> **Notes on 7015 error code**
> 
> - The 7015 error code is identified by MD5. If this error is reported during integration, check the integrity and version of the SDK file as prompted.
> - The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is **only a reminder** but will not cause an initialization failure.


#### Sample code
``` bash
int res = await ITMGContext.GetInstance().InitSDK(_editAppID.text,_editOpenID.text);
// Determine whether the initialization is successful by the returned value
if (ret != GmeError.AV_OK)
{
    print("Failed to initialize the SDK:");
    return;
}
```

### Triggering event callback

Event callbacks can be triggered by calling the `Poll` API in the timer. The `Poll` API is GME's message pump and should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run abnormally. For more information, see the `EnginePollHelper` file in [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).

> **Note**
> 

> The `Poll` API must be called periodically and in the main thread to avoid abnormal API callbacks.
> 


#### API prototype
``` bash
Future<void> Poll()
```

#### Sample code
``` bash
Future<void> pollTimer() async {
  _pollTimer = Timer.periodic(Duration(milliseconds: 100), (Timer timer) {
  ITMGContext.GetInstance().Poll();
  });
}
```

### Uninitializing SDK

This API is used to uninitialize the SDK to make it uninitialized. **If the game business account is bound to `openid`, switching game account requires uninitializing GME and then using the new `openid` to initialize again.**

#### API prototype
``` bash
Future<int> Uninit()
```

## Voice Messaging and Speech-to-Text Services

> **Notes**
> 
> - The speech-to-text service consists of fast recording-to-text conversion and streaming speech-to-text conversion.
> - You do not need to enter a voice chat room when using the voice messaging service.
> - The maximum recording duration of a voice message is 58 seconds by default, and the minimum recording duration cannot be less than 1 second. If you want to customize the recording duration, for example, to change the maximum recording duration to 10 seconds, call the `SetMaxMessageLength` API to set it after initialization.


### Flowchart for using the voice message service

![](https://qcloudimg.tencent-cloud.cn/raw/24c16c71cb2fcc6cf170a6b481067564.jpg)

### Flowchart for using the speech-to-text service

![](https://qcloudimg.tencent-cloud.cn/raw/8269f413756379d574a2969ac8da0158.jpg)
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GenAuthBuffer</td>

<td rowspan="1" colSpan="1" >Gets the authentication information.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SetMaxMessageLength</td>

<td rowspan="1" colSpan="1" >Specifies the maximum duration of a voice message.</td>
</tr>
</table>


### Generating the local authentication key

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, use the backend deployment key as detailed in [Authentication Key](https://www.tencentcloud.com/document/product/607/12218).    

#### API prototype
``` bash
Future<Uint8List> GenAuthBuffer(String appID, String roomID, String openID, String key)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >appId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`AppId` from the Tencent Cloud console</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >roomId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Enter `null` or an empty string.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >User ID, which is the same as `OpenId` during initialization.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >key</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme).</td>
</tr>
</table>


### Application authentication

After the authentication information is generated, the authentication is assigned to the SDK.  

#### API prototype
``` bash
Future<int> ApplyPTTAuthbuffer(Uint8List authBuffer) 
```

#### Sample code
``` bash
Uint8List authBuffer = await ITMGContext.GetInstance().GenAuthBuffer(_editAppID.text, _editRoomID.text, _editOpenID.text, _editKey.text);
m_context.ApplyPTTAuthbuffer(authBuffer);
```

### Specifying the maximum duration of voice message

This API is used to specify the maximum duration of a voice message, which can be up to 58 seconds.

#### API prototype
``` bash
Future<int> SetMaxMessageLength(int msTime)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >msTime</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >Voice message duration in ms. Value range: 1000 < `msTime` <= 58000</td>
</tr>
</table>


#### Sample code
``` bash
ITMGContext.GetInstance().GetPTT().SetMaxMessageLength(fileLen);
```

## Streaming Speech Recognition

### Voice messaging and speech-to-text APIs
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >StartRecordingWithStreamingRecognition</td>

<td rowspan="1" colSpan="1" >Starts streaming recording.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >StopRecording</td>

<td rowspan="1" colSpan="1" >Stops recording.</td>
</tr>
</table>


### Starting streaming speech recognition

This API is used to start streaming speech recognition. Text obtained from speech-to-text conversion will be returned in real time in its callback. It can specify a language for recognition or translate the text recognized in speech into a specified language and return the translation. **To stop recording, call [StopRecording](https://www.tencentcloud.com/document/product/607/53819).**

#### API prototype
``` bash
Future<int> StartRecordingWithStreamingRecognition(String filePath, String speechLanguage, String translateLanguage) 
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Path of the stored audio file</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >speechLanguage</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >The language in which the voice message file is to be converted to text. For parameters, see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >translateLanguage</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >The language in which the voice message file is to be translated to text. For parameters, see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260).</td>
</tr>
</table>


#### Sample code
``` bash
string filePath = "xx/xxx/xxx.silk"
int res = await ITMGContext.GetInstance().GetPTT().StartRecordingWithStreamingRecognition(filePath, strCurLanguage, strCurLanguage);
if (ret == 0) {
    this.currentStatus = "Start streaming recording";
} else {
    this.currentStatus = "Failed to start streaming recording";
}
```

> **Note**
> 

>  Translation incurs additional fees. For more information, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009).
> 


### Callback for streaming speech recognition

After streaming speech recognition is started, you need to listen on callback messages in the `OnEvent` notification, which is as detailed below:

`ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE` returns text after the recording is stopped and the recognition is completed, which is equivalent to returning the recognized text after a paragraph of speech.
`ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING` returns the recognized text in real time during the recording, which is equivalent to returning the recognized text while speaking.

The event message will be identified in the callback notification based on the actual needs. The passed parameters include the following four messages.
<table>
<tr>
<td rowspan="1" colSpan="1" >Message</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >result</td>

<td rowspan="1" colSpan="1" >Return code indicating whether streaming speech recognition is successful</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >text</td>

<td rowspan="1" colSpan="1" >Text converted from speech</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >file_path</td>

<td rowspan="1" colSpan="1" >Local path of the stored recording file</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >file_id</td>

<td rowspan="1" colSpan="1" >Backend URL address of the recording file, which will be retained for 90 days</td>
</tr>
</table>


> **Note**
> 

> The `file_id` is empty when the 'ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING' message is listened for.
> 


#### Error codes
<table>
<tr>
<td rowspan="1" colSpan="1" >Error Code</td>

<td rowspan="1" colSpan="1" >Description</td>

<td rowspan="1" colSpan="1" >Solution</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32775</td>

<td rowspan="1" colSpan="1" >Streaming speech-to-text conversion failed, but recording succeeded.</td>

<td rowspan="1" colSpan="1" >Call the `UploadRecordedFile` API to upload the recording file and then call the `SpeechToText` API to perform speech-to-text conversion.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32777</td>

<td rowspan="1" colSpan="1" >Streaming speech-to-text conversion failed, but recording and upload succeeded.</td>

<td rowspan="1" colSpan="1" >The message returned contains a backend URL after successful upload. Call the `SpeechToText` API to perform speech-to-text conversion.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32786</td>

<td rowspan="1" colSpan="1" >Streaming speech-to-text conversion failed.</td>

<td rowspan="1" colSpan="1" >During streaming recording, wait for the execution result of the streaming recording API to return.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32787</td>

<td rowspan="1" colSpan="1" >Speech-to-text conversion succeeded, but the text translation service was not activated.</td>

<td rowspan="1" colSpan="1" >Activate the text translation service in the console.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32788</td>

<td rowspan="1" colSpan="1" >Speech-to-text conversion succeeded, but the language parameter of the text translation service was invalid.</td>

<td rowspan="1" colSpan="1" >Check the parameter passed in.</td>
</tr>
</table>


If the error code 4098 is reported, see [Speech-to-text Conversion](https://intl.cloud.tencent.com/document/product/607/39716) for solutions.

#### Sample code
``` bash
void handleEventMsg(int eventType, String data){
   switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
        {
            HandleSTREAM2TEXTComplete(data,true);
            break;
        }
        ...
        case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING:
        {
            HandleSTREAM2TEXTComplete(data, false);
            break;
        }
    }
}
ITMGContext.GetInstance().SetEvent(handleEventMsg);
```

## Voice Message Recording

**The recording process is as follows: start recording > stop recording > return recording callback > start the next recording.**

### Voice messaging and speech-to-text APIs
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >StartRecording</td>

<td rowspan="1" colSpan="1" >Starts recording.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PauseRecording</td>

<td rowspan="1" colSpan="1" >Pauses recording.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ResumeRecording</td>

<td rowspan="1" colSpan="1" >Resumes recording.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >StopRecording</td>

<td rowspan="1" colSpan="1" >Stops recording.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >CancelRecording</td>

<td rowspan="1" colSpan="1" >Cancels recording.</td>
</tr>
</table>


### Starting recording

This API is used to start recording.

#### API prototype
``` bash
Future<int> StartRecording(String filePath)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Path of the stored voice message file</td>
</tr>
</table>


#### Sample code
``` bash
string filepath = "xxxx/xxx.silk";
int res = await ITMGContext.GetInstance().GetPTT().StartRecording(filepath);
```



### Stopping recording

This API is used to stop recording. It is async, and a callback for recording completion will be returned after recording stops. A recording file will be available only after recording succeeds.

#### API prototype
``` bash
Future<int> StopRecording() 
```

#### Sample code
``` bash
ITMGContext.GetInstance().GetPTT().StopRecording();
```

### Callback for recording start

A callback will be executed through a delegate function to pass a message when recording is completed.

**To stop recording, call `StopRecording`**. The callback for recording start will be returned after the recording is stopped.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >code</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`0`: Recording is completed.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filepath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Path of the stored recording file, which must be accessible and cannot be the `fileid`.</td>
</tr>
</table>


#### Error codes
<table>
<tr>
<td rowspan="1" colSpan="1" >Error Code</td>

<td rowspan="1" colSpan="1" >Cause</td>

<td rowspan="1" colSpan="1" >Solution</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4097</td>

<td rowspan="1" colSpan="1" >A parameter is empty.</td>

<td rowspan="1" colSpan="1" >Check whether the API parameters in the code are correct.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4098</td>

<td rowspan="1" colSpan="1" >An initialization error occurred.</td>

<td rowspan="1" colSpan="1" >Check whether the device is being used, whether the permissions are normal, and whether the initialization is normal.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4099</td>

<td rowspan="1" colSpan="1" >Recording is in progress.</td>

<td rowspan="1" colSpan="1" >Make sure that the SDK recording feature is used at the right time.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4100</td>

<td rowspan="1" colSpan="1" >No audio data is captured.</td>

<td rowspan="1" colSpan="1" >Check whether the mic is working properly.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4101</td>

<td rowspan="1" colSpan="1" >An error occurred while accessing the file during recording.</td>

<td rowspan="1" colSpan="1" >Ensure the existence of the file and the validity of the file path.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4102</td>

<td rowspan="1" colSpan="1" >The mic is not authorized.</td>

<td rowspan="1" colSpan="1" >The mic permission is required for using the SDK. To add the permission, see the SDK project configuration document for the corresponding engine or platform.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4103</td>

<td rowspan="1" colSpan="1" >The recording duration is too short.</td>

<td rowspan="1" colSpan="1" >The recording duration should be in ms and longer than 1,000 ms.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >4104</td>

<td rowspan="1" colSpan="1" >No recording operation is started.</td>

<td rowspan="1" colSpan="1" >Check whether the recording starting API has been called.</td>
</tr>
</table>


#### Sample code
``` bash
void handleEventMsg(int eventType, String data){
   switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
          // Process
          break;
        }
        ...
        case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE:
        {
          // Process
          break;
        }
    }
}
ITMGContext.GetInstance().SetEvent(handleEventMsg);
```

### Pausing recording

This API is used to pause recording. If you want to resume recording, call the `ResumeRecording` API.

#### API prototype
``` bash
Future<int> PauseRecording()
```

#### Sample code
``` bash
ITMGContext.GetInstance().GetPTT().PauseRecording();
```

### Resuming recording

This API is used to resume recording.

#### API prototype
``` bash
Future<int> ResumeRecording()
```

#### Sample code
``` bash
ITMGContext.GetInstance().GetPTT().ResumeRecording();
```

### Canceling recording

This API is used to cancel recording. **There is no callback after cancellation**.

#### API prototype
``` bash
Future<int> CancelRecording()
```

#### Sample code
``` bash
ITMGContext.GetInstance().GetPTT().CancelRecording();
```

## Voice Message Upload, Download, and Playback
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >UploadRecordedFile</td>

<td rowspan="1" colSpan="1" >Uploads an audio file.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >DownloadRecordedFile</td>

<td rowspan="1" colSpan="1" >Downloads an audio file.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlayRecordedFile</td>

<td rowspan="1" colSpan="1" >Plays back audio.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >StopPlayFile</td>

<td rowspan="1" colSpan="1" >Stops playing back audio.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetFileSize</td>

<td rowspan="1" colSpan="1" >Gets the audio file size.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetVoiceFileDuration</td>

<td rowspan="1" colSpan="1" >Gets the audio file duration.</td>
</tr>
</table>


### Uploading an audio file

This API is used to upload an audio file.

#### API prototype
``` bash
Future<int> UploadRecordedFile(String filePath) 
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >Path of the uploaded audio file, which is a local path.</td>
</tr>
</table>


#### Sample code
``` bash
ITMGContext.GetInstance().GetPTT().UploadRecordedFile(_filePath);
```

### Callback for audio file upload completion

After the audio file is uploaded, the event message `ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE` will be returned, which will be identified in the `OnEvent` function.
The passed parameters include `result`, `file_path`, and `file_id`.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >result</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >`0`: Recording is completed.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filepath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Path of the stored recording file</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fileid</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >File URL</td>
</tr>
</table>


#### Error codes
<table>
<tr>
<td rowspan="1" colSpan="1" >Error Code</td>

<td rowspan="1" colSpan="1" >Cause</td>

<td rowspan="1" colSpan="1" >Solution</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >8193</td>

<td rowspan="1" colSpan="1" >An error occurred while accessing the file during upload.</td>

<td rowspan="1" colSpan="1" >Ensure the existence of the file and the validity of the file path.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >8194</td>

<td rowspan="1" colSpan="1" >Signature verification failed.</td>

<td rowspan="1" colSpan="1" >Check whether the authentication key is correct and whether the voice messaging and speech-to-text feature is initialized.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >8195</td>

<td rowspan="1" colSpan="1" >A network error occurred.</td>

<td rowspan="1" colSpan="1" >Check whether the device can access the internet.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >8196</td>

<td rowspan="1" colSpan="1" >The network failed while getting the upload parameters.</td>

<td rowspan="1" colSpan="1" >Check whether the authentication is correct and whether the device network can normally access the internet.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >8197</td>

<td rowspan="1" colSpan="1" >The packet returned during the process of getting the upload parameters is empty.</td>

<td rowspan="1" colSpan="1" >Check whether the authentication is correct and whether the device network can normally access the internet.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >8198</td>

<td rowspan="1" colSpan="1" >Failed to decode the packet returned during the process of getting the upload parameters.</td>

<td rowspan="1" colSpan="1" >Check whether the authentication is correct and whether the device network can normally access the internet.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >8200</td>

<td rowspan="1" colSpan="1" >No `appinfo` is set.</td>

<td rowspan="1" colSpan="1" >Check whether the `apply` API is called or whether the input parameters are empty.</td>
</tr>
</table>


#### Sample code
``` bash
void handleEventMsg(int eventType, String data){
 switch (eventType) {
        ...
        case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE:
        {
            // Process
            break;
        }
    }
}
ITMGContext.GetInstance().SetEvent(handleEventMsg);
```

### Downloading the audio file

This API is used to download an audio file.

#### API prototype
``` bash
Future<int> DownloadRecordedFile(String fileId, String filePath)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fileId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >File URL</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Local path of the saved file, which must be accessible and cannot be the `fileid`.</td>
</tr>
</table>


#### Sample code
``` bash
ITMGContext.GetInstance().GetPTT().DownloadRecordedFile(_fileId, _filePath);
```

### Callback for audio file download completion

After the audio file is downloaded, the event message `ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE` will be returned, which will be identified in the `OnEvent` function.
The passed parameters include `result`, `file_path`, and `file_id`.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >result</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >`0`: Download is completed.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filepath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Path of the stored recording file</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fileid</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >URL of the recording file, which will be retained on the server for 90 days.</td>
</tr>
</table>


#### Error codes
<table>
<tr>
<td rowspan="1" colSpan="1" >Error Code</td>

<td rowspan="1" colSpan="1" >Cause</td>

<td rowspan="1" colSpan="1" >Solution</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12289</td>

<td rowspan="1" colSpan="1" >An error occurred while accessing the file during download.</td>

<td rowspan="1" colSpan="1" >Check whether the file path is valid.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12290</td>

<td rowspan="1" colSpan="1" >Signature verification failed.</td>

<td rowspan="1" colSpan="1" >Check whether the authentication key is correct and whether the voice messaging and speech-to-text feature is initialized.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12291</td>

<td rowspan="1" colSpan="1" >A network storage system exception occurred.</td>

<td rowspan="1" colSpan="1" >The server failed to get the audio file. Check whether the API parameter `fileid` is correct, whether the network is normal, and whether the file exists in COS.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12292</td>

<td rowspan="1" colSpan="1" >A server file system error occurred.</td>

<td rowspan="1" colSpan="1" >Check whether the device can access the internet and whether the file exists on the server.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12293</td>

<td rowspan="1" colSpan="1" >The HTTP network failed while getting the download parameters.</td>

<td rowspan="1" colSpan="1" >Check whether the device can access the internet.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12294</td>

<td rowspan="1" colSpan="1" >The packet returned during the process of getting the download parameters is empty.</td>

<td rowspan="1" colSpan="1" >Check whether the device can access the internet.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12295</td>

<td rowspan="1" colSpan="1" >Failed to decode the packet returned during the process of getting the download parameters.</td>

<td rowspan="1" colSpan="1" >Check whether the device can access the internet.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >12297</td>

<td rowspan="1" colSpan="1" >No `appinfo` is set.</td>

<td rowspan="1" colSpan="1" >Check whether the authentication key is correct and whether the voice messaging and speech-to-text feature is initialized.</td>
</tr>
</table>


#### Sample code
``` bash
void handleEventMsg(int eventType, String data){
    switch (eventType) {
        ...
        case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
          // Process
          break;
        }
    }
}
ITMGContext.GetInstance().SetEvent(handleEventMsg);
```

### Playing back audio

This API is used to play back audio.

#### API prototype
``` bash
Future<int> PlayRecordedFile(String filePath, int voiceType)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Local audio file path</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >voicetype</td>

<td rowspan="1" colSpan="1" >ITMG_VOICE_TYPE</td>

<td rowspan="1" colSpan="1" >Voice changing type. For more information, see [Voice Changing](https://intl.cloud.tencent.com/document/product/607/44995).</td>
</tr>
</table>


#### Error codes
<table>
<tr>
<td rowspan="1" colSpan="1" >Error Code</td>

<td rowspan="1" colSpan="1" >Cause</td>

<td rowspan="1" colSpan="1" >Solution</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >20485</td>

<td rowspan="1" colSpan="1" >Playback is not started.</td>

<td rowspan="1" colSpan="1" >Ensure the existence of the file and the validity of the file path.</td>
</tr>
</table>


#### Sample code
``` bash
int res = await ITMGContext.GetInstance().GetPTT().PlayRecordedFile(_filePath, _nVoiceType);
```

### Callback for audio playback

After the audio is played back, the event message `ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE` will be returned, which will be identified in the `OnEvent` function.
The passed parameter includes `result` and `file_path`.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >code</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >`0`: Playback is completed.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filepath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Path of the stored recording file</td>
</tr>
</table>


#### Error codes
<table>
<tr>
<td rowspan="1" colSpan="1" >Error Code</td>

<td rowspan="1" colSpan="1" >Cause</td>

<td rowspan="1" colSpan="1" >Solution</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >20481</td>

<td rowspan="1" colSpan="1" >An initialization error occurred.</td>

<td rowspan="1" colSpan="1" >Check whether the device is being used, whether the permissions are normal, and whether the initialization is normal.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >20482</td>

<td rowspan="1" colSpan="1" >During playback, the client tried to interrupt and play back the next one but failed (which should succeed normally).</td>

<td rowspan="1" colSpan="1" >Check whether the code logic is correct.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >20483</td>

<td rowspan="1" colSpan="1" >A parameter is empty.</td>

<td rowspan="1" colSpan="1" >Check whether the API parameters in the code are correct.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >20484</td>

<td rowspan="1" colSpan="1" >An internal error occurred.</td>

<td rowspan="1" colSpan="1" >An error occurred while initializing the player. This error code is generally caused by failure in decoding, and the error should be located with the aid of logs.</td>
</tr>
</table>


#### Sample code
``` bash
void handleEventMsg(int eventType, String data){
 switch (eventType) {
    case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE:
    {
        // Process
        break;
    }
   }
}
```

### Stopping audio playback

This API is used to stop audio playback. There will be a callback for playback completion when the playback stops.

#### API prototype
``` bash
Future<int> StopPlayFile()
```

#### Sample code
``` bash
ITMGContext.GetInstance().GetPTT().StopPlayFile();
```

### Getting audio file size

This API is used to get the size of an audio file.

#### API prototype
``` bash
Future<int> GetFileSize(String filePath)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Path of the audio file, which is a local path</td>
</tr>
</table>


#### Sample code
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().GetFileSize(_filePath);
```

### Getting audio file duration

This API is used to get the duration of an audio file in milliseconds.

#### API prototype
``` bash
Future<int> GetVoiceFileDuration(String filePath)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Path of the audio file, which is a local path</td>
</tr>
</table>


#### Sample code
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().GetVoiceFileDuration(_filePath);
```

## Fast Recording-to-Text Conversion

### Translating audio file into text in specified language

This API can specify a language for recognition or translate the text recognized in speech into a specified language and return the translation.

> **Note**
> 

> Translation incurs additional fees. For more information, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009).
> 


#### API prototype
``` bash
Future<int> SpeechToText(String fileId, String speechLanguage, String translateLanguage)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fileID</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >URL of the audio file, which will be retained on the server for 90 days.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >speechLanguage</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >The language in which the audio file is to be converted to text. For parameters, see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >translatelanguage</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >The language in which the audio file is to be translated to text. For parameters, see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260).</td>
</tr>
</table>


#### Sample code
``` bash
ITMGContext.GetInstance().GetPTT().SpeechToText(_fileId, "cmn-Hans-CN", "cmn-Hans-CN");
```

### Callback for recognition

After the specified audio file is converted to text, the event message ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE will be returned, which will be identified in the `OnEvent` function.
The passed parameters include `result`, `file_path` and `text` (recognized text).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >result</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >`0`: Recording is completed.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fileid</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >URL of the audio file, which will be retained on the server for 90 days.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >text</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Converted text</td>
</tr>
</table>


#### Error codes
<table>
<tr>
<td rowspan="1" colSpan="1" >Error Code</td>

<td rowspan="1" colSpan="1" >Cause</td>

<td rowspan="1" colSpan="1" >Solution</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32769</td>

<td rowspan="1" colSpan="1" >An internal error occurred.</td>

<td rowspan="1" colSpan="1" >Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32770</td>

<td rowspan="1" colSpan="1" >A network error occurred.</td>

<td rowspan="1" colSpan="1" >Check whether the device can access the internet.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32772</td>

<td rowspan="1" colSpan="1" >Failed to decode the returned packet.</td>

<td rowspan="1" colSpan="1" >Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32774</td>

<td rowspan="1" colSpan="1" >No `appinfo` is set.</td>

<td rowspan="1" colSpan="1" >Check whether the authentication key is correct and whether the voice messaging and speech-to-text feature is initialized.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32776</td>

<td rowspan="1" colSpan="1" >`authbuffer` check failed.</td>

<td rowspan="1" colSpan="1" >Check whether `authbuffer` is correct.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32784</td>

<td rowspan="1" colSpan="1" >The speech-to-text conversion parameter is incorrect.</td>

<td rowspan="1" colSpan="1" >Check whether the API parameter `fileid` in the code is empty.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32785</td>

<td rowspan="1" colSpan="1" >Speech-to-text translation returned an error.</td>

<td rowspan="1" colSpan="1" >An error occurred in the voice messaging and speech-to-text feature on the backend. Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32787</td>

<td rowspan="1" colSpan="1" >Speech-to-text conversion succeeded, but the text translation service was not activated.</td>

<td rowspan="1" colSpan="1" >Activate the text translation service in the console.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >32788</td>

<td rowspan="1" colSpan="1" >Speech-to-text conversion succeeded, but the language parameter of the text translation service was invalid.</td>

<td rowspan="1" colSpan="1" >Check the parameter passed in.</td>
</tr>
</table>


#### Sample code
``` bash
void handleEventMsg(int eventType, String data){
 switch (eventType) {
    case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
       {
         // Process
         break;
       }
       ...
       case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE:
       {
         // Process
         break;
       }
    }
}
```

## Voice Message Volume Level APIs
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetMicLevel</td>

<td rowspan="1" colSpan="1" >Gets the real-time mic volume level.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SetMicVolume</td>

<td rowspan="1" colSpan="1" >Sets the recording volume level.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetMicVolume</td>

<td rowspan="1" colSpan="1" >Gets the recording volume level.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetSpeakerLevel</td>

<td rowspan="1" colSpan="1" >Gets the real-time speaker volume level.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SetSpeakerVolume</td>

<td rowspan="1" colSpan="1" >Sets the playback volume level.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetSpeakerVolume</td>

<td rowspan="1" colSpan="1" >Gets the playback volume level.</td>
</tr>
</table>


### Getting the real-time mic volume of voice message

This API is used to get the real-time mic volume. A number-type value will be returned. Value range: 0-200.

#### API prototype
``` bash
Future<int> GetMicLevel() 
```

#### Sample code
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().GetMicLevel();
```

### Setting the recording volume of voice message

This API is used to set the recording volume of voice message. Value range: 0-200.

#### API prototype
``` bash
Future<int> SetMicVolume(int volume)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >vol</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >Value range: 0-200. Default value: `100`. `0` indicates that the audio is mute, while `100` indicates that the volume level remains unchanged.</td>
</tr>
</table>


#### Sample code
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().SetMicVolume(100);
```

### Getting the recording volume of voice message

This API is used to get the recording volume of a voice message. A number-type value will be returned. Value range: 0-200.

#### API prototype
``` bash
Future<int> GetMicVolume() 
```

#### Sample code
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().GetMicVolume();
```

### Getting the real-time speaker volume of voice message

This API is used to get the real-time speaker volume. A number-type value will be returned. Value range: 0-200.

#### API prototype
``` bash
Future<int> GetSpeakerLevel()
```

#### Sample code
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().GetSpeakerLevel();
```

### Setting the playback volume of voice message

This API is used to set the playback volume of voice message. Value range: 0-200.

#### API prototype
``` bash
Future<int> SetSpeakerVolume(int volume)
```

#### Sample code
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().SetSpeakerVolume(100);
```

### Getting the playback volume of voice message

This API is used to get the playback volume of a voice message. A number-type value will be returned. Value range: 0-200.

#### API prototype
``` bash
Future<int> GetSpeakerVolume()
```

#### Sample code
``` bash
final int res = await ITMGContext.GetInstance().GetPTT().GetSpeakerVolume();
```

## Advanced APIs

### Getting version number

This API is used to get the SDK version number for analysis.

#### API prototype
``` bash
Future<String> GetSDKVersion() 
```

#### Sample code
``` bash
_sdkVersions = await ITMGContext.GetInstance().GetSDKVersion();
```

### Setting log printing level

This API is used to set the level of logs to be printed, and needs to be called before the initialization. It is recommended to keep the default level.

#### API prototype
``` bash
Future<int> SetLogLevel(int levelWrite, int levelPrint)
```

#### Parameter description
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >level</td>

<td rowspan="1" colSpan="1" >ITMG_LOG_LEVEL</td>

<td rowspan="1" colSpan="1" >Sets the log level. `TMG_LOG_LEVEL_NONE` indicates not to log. Default value: `TMG_LOG_LEVEL_INFO`.</td>
</tr>
</table>


`level` description:
<table>
<tr>
<td rowspan="1" colSpan="1" >level</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_NONE</td>

<td rowspan="1" colSpan="1" >Does not print logs</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_ERROR</td>

<td rowspan="1" colSpan="1" >Prints error logs (default)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_INFO</td>

<td rowspan="1" colSpan="1" >Prints info logs</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_DEBUG</td>

<td rowspan="1" colSpan="1" >Prints debug logs</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_VERBOSE</td>

<td rowspan="1" colSpan="1" >Prints verbose logs</td>
</tr>
</table>


#### Sample code
``` bash
ITMGContext.GetInstance().SetLogLevel(ITMG_LOG_LEVEL.TMG_LOG_LEVEL_ERROR,ITMG_LOG_LEVEL.TMG_LOG_LEVEL_ERROR);
```

### Setting the log printing path

This API is used to set the log printing path. The default path is as follows. It needs to be called before Init.

#### API prototype
``` bash
Future<int> SetLogPath(String logDir)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >logPath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Path</td>
</tr>
</table>


#### Sample code
``` bash
String logDir = ""// Set a path by yourself
ITMGContext.GetInstance().SetLogPath(curPath);
```

