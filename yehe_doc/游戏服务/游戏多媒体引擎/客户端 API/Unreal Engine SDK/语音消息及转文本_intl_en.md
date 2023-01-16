This document describes how to integrate with and debug GME client APIs for the voice messaging and speech-to-text services for Unreal Engine.

## Key Considerations for Using GME

GME provides the real-time voice and voice messaging and speech-to-text services, which all depend on core APIs such as `Init` and `Poll`.


#### Notes

- You have created a GME application and obtained the SDK AppID and key. For more information, see [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- You have activated **GME real-time voice and voice messaging and speech-to-text services**. For more information, see [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- Configure your project before using GME; otherwise, the SDK will not take effect.
- After a GME API is called successfully, `QAVError.OK` will be returned with the value being 0.
- GME APIs should be called in the same thread.
- The `Poll` API should be called periodically for GME to trigger event callbacks.
- For detailed error code, see <dx-tag-link link="https://www.tencentcloud.com/document/product/607/33223" tag="ErrorCode">Error Codes</dx-tag-link>.

<dx-alert infotype="notice" title="">
There is a default call rate limit for speech-to-text APIs. For more information on how calls are billed within the limit, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009). If you want to increase the limit or learn more about how excessive calls are billed, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1).
- Non-streaming speech-to-text API ***SpeechToText()***: There can be up to 10 concurrent requests per account.
- Streaming speech-to-text API ***StartRecordingWithStreamingRecognition()***: There can be up to 50 concurrent requests per account.
- Real-time streaming speech-to-text API ***StartRealTimeASR()***: There can be up to 50 concurrent requests per account.
</dx-alert>

## Integrating the SDK

### Directions

Key processes involved in SDK integration are as follows:

<img src="https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg"  width="70%" /></img>

<dx-steps>
-<dx-tag-link link="#Init" tag="API: Init">Initializing GME</dx-tag-link>
-<dx-tag-link link="#Poll" tag="API: Poll">Calling Poll periodically to trigger event callbacks</dx-tag-link>
-<dx-tag-link link="#ApplyPtt" tag="API: ApplyPTTAuthbuffer">Initializing authentication</dx-tag-link>
-<dx-tag-link link="#StartRWSR" tag="API: StartRecordingWithStreamingRecognition">Starting streaming speech recognition</dx-tag-link>
-<dx-tag-link link="#Stop" tag="API: StopRecording">Stop recording</dx-tag-link>
-<dx-tag-link link="#UnInit" tag="API: UnInit">Uninitializing GME</dx-tag-link>
</dx-steps>

### C++ classes

| Class | Description |
| ----------- | :----------------------: |
| ITMGContext | Key APIs |
| ITMGPTT  |   Voice messaging and speech-to-text APIs   |

## Key APIs

| API | Description |
| ------ | :----------: |
| Init | Initializes GME |
| Poll | Triggers event callback |
| Pause | Pauses the system |
| Resume | Resumes the system |
| Uninit | Uninitializes GME |


### Preparations

You need to import the header file `tmg_sdk.h` first before you can access GME. The classes in the header file inherit `ITMGDelegate` for message delivery and callback.

#### Sample code

```
#include "tmg_sdk.h"

class UEDEMO1_API AUEDemoLevelScriptActor : public ALevelScriptActor, public ITMGDelegate
{
public:
...
private:
...
｝
```

### Setting singleton

You need to get `ITMGContext` first before you can call the `EnterRoom` function, because all calls begin with `ITMGContext` and callbacks are passed to the application through `ITMGDelegate`.

#### Sample code 

```
ITMGContext* context = ITMGContextGetInstance();
context->SetTMGDelegate(this);
```

### Message delivery

The API class uses the `Delegate` method to send callback notifications to the application. `ITMG_MAIN_EVENT_TYPE` indicates the message type. The data on Windows is in json string format. For the key-value pairs, please see the relevant documentation.

#### Sample code  

```
// Function implementation:
//UEDemoLevelScriptActor.h:
class UEDEMO1_API AUEDemoLevelScriptActor : public ALevelScriptActor, public SetTMGDelegate
{
public:
	void OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data);
｝

//UEDemoLevelScriptActor.cpp:
void AUEDemoLevelScriptActor::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data){
	// Identify and manipulate `eventType` here
}
```

### [Initializing SDK](id:Init)

**You need to initialize the SDK through the `Init` API** before you can use the real-time voice, voice message, and speech-to-text services. The `Init` API must be called in the same thread as other APIs. We recommend you call all APIs in the main thread.

#### API prototype

```
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
```

| Parameter | Type | Description |
| -------- | :---------: | ------------------------------------------------------------ |
| sdkAppId | const char* | `AppID` provided in the [GME console](https://console.cloud.tencent.com/gamegme), which can be obtained as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0). |
| openID   | const char* | `openID` can only be in `Int64` type, which is passed in after being converted to a `const char*`. You can customize its rules, and it must be unique in the application. To pass in `openID` as a string, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1) for application.         |

#### Returned values

| Returned Value | Description |
| ------------------------------- | --------------------------------------------- |
| AV_OK = 0                  | Initialized SDK successfully. |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | Checks whether the SDK file is complete. It is recommended to delete it and then import the SDK again. |

<dx-alert infotype="notice" title="Notes on 7015 error code">

- The 7015 error code is judged by md5. If this error is reported during integration, please check the integrity and version of the SDK file as prompted.
- The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is **only a reminder** but will not cause an initialization failure.
- Due to the third-party reinforcement, Unity packaging mechanism and other factors, the md5 of the library file will be affected, resulting in misjudgment. **Please ignore this error in the logic for official release**, and try to avoid displaying it in the UI.
  </dx-alert>

#### Sample code 

```
std::string appid = TCHAR_TO_UTF8(CurrentWidget->editAppID->GetText().ToString().operator*());
std::string userId = TCHAR_TO_UTF8(CurrentWidget->editUserID->GetText().ToString().operator*());
ITMGContextGetInstance()->Init(appid.c_str(), userId.c_str());
```

[](id:Poll)
### Triggering event callback

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. The `Poll` API is GME's message pump and should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run abnormally. For more information, see the `EnginePollHelper` file in [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).

<dx-alert infotype="notice" title="">
The `Poll` API must be called periodically and in the main thread to avoid abnormal API callbacks.
</dx-alert>

#### API prototype

```
class ITMGContext {
protected:
    virtual ~ITMGContext() {}

public:        
    virtual void Poll()= 0;
}
```

#### Sample code

```
// Declaration in the header file
virtual void Tick(float DeltaSeconds);

void AUEDemoLevelScriptActor::Tick(float DeltaSeconds) {
	Super::Tick(DeltaSeconds);	
	ITMGContextGetInstance()->Poll();
}
```

### Pausing the system

When a `Pause` event occurs in the system, the engine should also be notified for pause. If you do not need the background to play back the audio in the room, please call `Pause` API to pause the GME service.

#### API prototype

```
ITMGContext int Pause()
```

### Resuming the system

When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.

#### API prototype

```
ITMGContext int Resume()
```

[](id:UnInit)
### Uninitializing SDK

This API is used to uninitialize the SDK to make it uninitialized. **If the game business account is bound to `openid`, switching game account requires uninitializing GME and then using the new `openid` to initialize again.**

#### API prototype

```
ITMGContext int Uninit()
```

## Voice Messaging and Speech-to-Text Services

<dx-alert infotype="explain" title="">

- The speech-to-text service consists of fast recording-to-text conversion and streaming speech-to-text conversion.
- You do not need to enter a voice chat room when using the voice message service.
- The maximum recording duration of a voice message is 58 seconds by default, and the minimum recording duration cannot be less than 1 second. If you want to customize the recording duration, for example, to modify the maximum recording duration to 10 seconds, call the `SetMaxMessageLength` API to set it after initialization.
  </dx-alert>

<img src="https://qcloudimg.tencent-cloud.cn/raw/24c16c71cb2fcc6cf170a6b481067564.jpg" width="80%">

### Flowchart for using the speech-to-text service

<img src="https://qcloudimg.tencent-cloud.cn/raw/8269f413756379d574a2969ac8da0158.jpg" width="80%">

| API                        |            Description            |
| ------------------- | :------------------: |
|GenAuthBuffer| Generates the local authentication key |
| ApplyPTTAuthbuffer | Initializes authentication |
| SetMaxMessageLength | Specifies the maximum length of voice message |




### Generating the local authentication key

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    

#### API prototype

```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```

| Parameter | Type | Description |
| ------------- | :---: | ------------------------------------------------------------ |
| dwSdkAppID | int | `AppId` from the Tencent Cloud console.|
| strRoomID     | const char* | Enter `null` or an empty string |
| strOpenID     | const char* | User Identifier, which is the same as `openID` during initialization. |
| strKey        | const char* | Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme). |
| strAuthBuffer | const char* | Returned `authbuff`                                              |
| bufferLength  |  int  | Length of the `authbuff` passed in. 500 is recommended.                             |

### Application authentication

After the authentication information is generated, the authentication is assigned to the SDK.  

#### API prototype  

```
ITMGPTT virtual int ApplyPTTAuthbuffer(const char* authBuffer, int authBufferLen)
```

| Parameter       |  Type  | Description                    |
| ---------- | :----: | ---- |
| authBuffer    | const char* | Authentication     |
| authBufferLen |  int  | Authentication length |

#### Sample code

```
ITMGContextGetInstance()->GetPTT()->ApplyPTTAuthbuffer(authBuffer,authBufferLen);
```
### Specifying the maximum duration of voice message

This API is used to specify the maximum duration of a voice message, which can be up to 58 seconds.

#### API prototype

```
ITMGPTT virtual int SetMaxMessageLength(int msTime)
```

| Parameter   | Type | Description                                            |
| ------ | :--: | ----------------------------------------------- |
| msTime | int | Audio duration in ms. Value range: 1000 < msTime <= 58000 |

#### Sample code  

```
int msTime = 10000;
ITMGContextGetInstance()->GetPTT()->SetMaxMessageLength(msTime);
```

## Streaming Speech Recognition



### Voice message and speech-to-text APIs

| API | Description |
| -------------------------------------- | :----------: |
| StartRecordingWithStreamingRecognition | Starts streaming recording |
| StopRecording                          |          Stops recording          |


[](id:StartRWSR)
### Starting streaming speech recognition

This API is used to start streaming speech recognition. Text obtained from speech-to-text conversion will be returned in real time in its callback. It can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation. **To stop recording, call <dx-tag-link link="#Stop" tag="API: StopRecording"> Stop recording</dx-tag-link>**.

#### API prototype  

```
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath) 
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath,const char* translateLanguage,const char* translateLanguage) 
```

| Parameter | Type | Description |
| ----------------- | :---: | ------------------------------------------------------------ |
| filePath          | const char* | Path of stored audio file                                               |
| speechLanguage    | const char* | The language in which the audio file is to be converted to text. For parameters, see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260). |
| translateLanguage | const char* | The language in which the audio file is to be translated to text. For parameters, see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260). |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->StartRecordingWithStreamingRecognition(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```

> !Translation incurs additional fees. For more information, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009).

### Callback for streaming speech recognition

After streaming speech recognition is started, you need to listen on callback messages in the `OnEvent` notification, which is as detailed below:

- `ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE` returns text after the recording is stopped and the recognition is completed, which is equivalent to returning the recognized text after a paragraph of speech.
- `ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING` returns the recognized text in real-time during the recording, which is equivalent to returning the recognized text while speaking.

The event message will be identified in the `OnEvent` notification based on the actual needs. The passed parameters include the following four messages.

| Message Name | Description |
| --------- | :---------------------------------------------: |
| result    |    Return code indicating whether streaming speech recognition is successful     |
| text      |            Text converted from speech             |
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

If the error code 4098 is reported, see [FAQs](https://intl.cloud.tencent.com/document/product/607/39716) for solutions.

#### Sample code  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
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
}

void CTMGSDK_For_AudioDlg::HandleSTREAM2TEXTComplete(const char* data, bool isComplete)
{
					std::string strText = "STREAM2TEXT: ret=";
					strText += data;
					m_EditMonitor.SetWindowText(MByteToWChar(strText).c_str());
					Json::Reader reader;
					Json::Value root;
					bool parseRet = reader.parse(data, root);
					if (!parseRet) {
						::SetWindowText(m_EditInfo.GetSafeHwnd(),MByteToWChar(std::string("parse result Json error")).c_str());
					}
					else
					{
						if (isComplete) {
							::SetWindowText(m_EditUpload.GetSafeHwnd(), MByteToWChar(root["file_id"].asString()).c_str());
						}
						else {
							std::string isruning = "STREAMINGRECOGNITION_IS_RUNNING";
							::SetWindowText(m_EditUpload.GetSafeHwnd(), MByteToWChar(isruning).c_str());
						}
					}
}
```



## Voice Message Recording

**The recording process is as follows: start recording -> stop recording -> return recording callback -> start the next recording.**



### Voice message and speech-to-text APIs

| API | Description |
| --------------- | :------: |
| StartRecording | Starts recording |
| PauseRecording | Pauses recording |
| ResumeRecording | Resumes recording |
| StopRecording | Stops recording |
| CancelRecording | Cancels recording |



### Starting recording

This API is used to start recording.

#### API prototype  

```
ITMGPTT virtual int StartRecording(const char* fileDir)
```

| Parameter | Type | Description |
| ------- | :----: | -------------- |
| fileDir | const char* | Path of stored audio file |

#### Sample code  

```
char buffer[256]={0};
snprintf(buffer, sizeof(buffer), "%sunreal_ptt_local.file", getFilePath().c_str());
ITMGContextGetInstance()->GetPTT()->StartRecording(buffer);
```

[](id:Stop)
### Stopping recording

This API is used to stop recording. It is async, and a callback for recording completion will be returned after recording stops. A recording file will be available only after recording succeeds.

#### API prototype  

```
ITMGPTT virtual int StopRecording()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->StopRecording();
```

### Callback for recording start

The recording start result will be returned through the callback.

**To stop recording, call `StopRecording`**. The callback for recording start will be returned after the recording is stopped.

| Parameter | Type | Description |
| -------- | :-----: | ------------------------- |
| result   |  int32  | 0: recording is completed |
| filepath | FString | Path of stored recording file, which must be accessible and cannot be the `fileid` |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ------------------------ | ------------------------------------------------------------ |
| 4097 | Parameter is empty. | Check whether the API parameters in the code are correct. |
| 4098 | Initialization error. | Check whether the device is being used, whether the permissions are normal, and whether the initialization is normal. |
| 4099 | Recording is in progress. | Ensure that the SDK recording feature is used at the right time. |
| 4100 | Audio data is not captured. | Check whether the mic is working properly. |
| 4101 | An error occurred while accessing the file during recording. | Ensure the existence of the file and the validity of the file path. |
| 4102 | The mic is not authorized. | Mic permission is required for using the SDK. To add the permission, please see the SDK project configuration document for the corresponding engine or platform. |
| 4103 | The recording duration is too short. | The recording duration should be in ms and longer than 1,000 ms. |
| 4104 | No recording operation is started. | Check whether the recording starting API has been called. |

#### Sample code  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
	...
		else if (eventType == ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE) {
			int32 result = JsonObject->GetIntegerField(TEXT("result"));
			FString filepath = JsonObject->GetStringField(TEXT("file_path"));
			std::string path = TCHAR_TO_UTF8(filepath.operator*());
			int duration = 0;
			int filesize = 0;
			if (result == 0) {
				duration = ITMGContextGetInstance()->GetPTT()->GetVoiceFileDuration(path.c_str());
				filesize = ITMGContextGetInstance()->GetPTT()->GetFileSize(path.c_str());
			}
			onPttRecordFileCompleted(result, filepath, duration, filesize);
		}
	}
}
```

### Pausing recording

This API is used to pause recording. If you want to resume recording, please call the `ResumeRecording` API.

#### API prototype  

```
ITMGPTT virtual int PauseRecording()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->PauseRecording();
```

### Resuming recording

This API is used to resume recording.

#### API prototype  

```
ITMGPTT virtual int ResumeRecording()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->ResumeRecording();
```



### Canceling recording

This API is used to cancel recording. **There is no callback after cancellation**.

#### API prototype  

```
ITMGPTT virtual int CancelRecording()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->CancelRecording();
```





## Voice Message Upload, Download, and Playback

| API | Description |
| -------------------- | :------------: |
| UploadRecordedFile | Uploads the audio file |
| DownloadRecordedFile | Downloads the audio file |
| PlayRecordedFile | Plays back the audio file |
| StopPlayFile | Stops playing back the audio file |
| GetFileSize | Gets audio file size |
| GetVoiceFileDuration | Gets the audio file duration |

### Uploading an audio file

This API is used to upload an audio file.

#### API prototype  

```
ITMGPTT virtual int UploadRecordedFile(const char* filePath)
```

| Parameter | Type | Description |
| -------- | :----: | -------------------------------- |
| filePath | const char* | Path of uploaded audio file, which is a local path |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->UploadRecordedFile(filePath);
```

### Callback for audio file upload completion

After the audio file is uploaded, the event message `ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE` will be returned, which will be identified in the `OnEvent` function.
The passed parameters include `result`, `file_path`, and `file_id`.




| Parameter | Type | Description |
| -------- | :----: | ----------------------- |
| result   |  int32  | 0: recording is completed                 |
| filepath | FString | Path of stored recording file |
| fileid   | FString | File URL path |

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
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
	...
		else if (eventType == ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE) {
			int32 result = JsonObject->GetIntegerField(TEXT("result"));
			FString filepath = JsonObject->GetStringField(TEXT("file_path"));
			FString fileid = JsonObject->GetStringField(TEXT("file_id"));
			onPttUploadFileCompleted(result, filepath, fileid);
		}
	}
}
```

### Downloading the audio file

This API is used to download an audio file.

#### API prototype  

```
ITMGPTT virtual int DownloadRecordedFile(const char* fileId, const char* filePath) 
```

| Parameter | Type | Description |
| ---------------- | :----: | ------------------------------------------------------------ |
| fileId   | const char* | URL path of file    |
| filePath | const char* | Local path of saved file |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->DownloadRecordedFile(fileID,filePath);
```

### Callback for audio file download completion

After the audio file is downloaded, the event message `ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE` will be returned, which will be identified in the `OnEvent` function.
The passed parameters include `result`, `file_path`, and `file_id`.

| Parameter | Type | Description |
| -------- | :-----: | --------------------------------------- |
| result   |  int32  | 0: recording is completed                 |
| filepath | FString | Path of stored recording file |
| fileid   | FString | URL path of file, which will be retained on the server for 90 days |

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
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
	...
		else if (eventType == ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE) {
			int32 result = JsonObject->GetIntegerField(TEXT("result"));
			FString filepath = JsonObject->GetStringField(TEXT("file_path"));
			FString fileid = JsonObject->GetStringField(TEXT("file_id"));
			onPttDownloadFileCompleted(result, filepath, fileid);
		}
	}
}
```

### Playing back audio

This API is used to play back audio.

#### API prototype  

```
ITMGPTT virtual int PlayRecordedFile(const char* filePath)
ITMGPTT virtual int PlayRecordedFile(const char* filePath, nt voiceType)
```

| Parameter | Type | Description |
| --------- | :----: | ------------------------------------------------------------ |
| filePath | const char\* | Local audio file path |
| voicetype | int | Voice changer type. For more information, see [Voice Changing Effects](https://intl.cloud.tencent.com/document/product/607/44995). |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ---------- | ------------------------------ |
| 20485 | Playback is not started. | Ensure the existence of the file and the validity of the file path. |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->PlayRecordedFile(filePath);
```

### Callback for audio playback

After the audio is played back, the event message `ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE` will be returned, which will be identified in the `OnEvent` function.
The passed parameter includes `result` and `file_path`.

| Parameter | Type | Description |
| -------- | :----: | ----------------------- |
| code | int | 0: playback is completed |
| filepath | FString | Path of stored recording file |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| 20481 | Initialization error. | Check whether the device is being used, whether the permissions are normal, and whether the initialization is normal. |
| 20482 | During playback, the client tried to interrupt and play back the next one but failed (which should succeed normally). | Check whether the code logic is correct. |
| 20483 | Parameter is empty. | Check whether the API parameters in the code are correct. |
| 20484 | Internal error. | An error occurred while initializing the player. This error code is generally caused by failure in decoding, and the error should be located with the aid of logs. |

#### Sample code

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
	...
		else if (eventType == ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE) {
			int32 result = JsonObject->GetIntegerField(TEXT("result"));
			FString filepath = JsonObject->GetStringField(TEXT("file_path"));
			onPttPlayFileCompleted(result, filepath);
		}
	}
}
```



### Stopping audio playback

This API is used to stop audio playback. There will be a callback for playback completion when the playback stops.

#### API prototype  

```
ITMGPTT virtual int StopPlayFile()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->StopPlayFile();
```


### Getting audio file size

This API is used to get the size of an audio file.

#### API prototype  

```
ITMGPTT virtual int GetFileSize(const char* filePath)
```

| Parameter | Type | Description |
| -------- | :----: | -------------------------------- |
| filePath | const char* | Path of audio file, which is a local path |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->GetFileSize(filePath);
```

### Getting audio file duration

This API is used to get the duration of an audio file in milliseconds.

#### API prototype  

```
ITMGPTT virtual int GetVoiceFileDuration(const char* filePath)
```

| Parameter | Type | Description |
| -------- | :----: | -------------------------------- |
| filePath | const char* | Path of audio file, which is a local path |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->GetVoiceFileDuration(filePath);
```





## Fast Recording-to-Text Conversion

| API | Description |
| ------------ | :------------: |
| SpeechToText | Converts speech to text |

### Converting audio file to text

This API is used to convert a specified audio file to text.

#### API prototype  

```
ITMGPTT virtual void SpeechToText(const char* fileID)
```

| Parameter | Type | Description |
| ------ | :----: | ------------ |
| fileID | const char* | Audio file URL |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->SpeechToText(fileID);
```



### Translating audio file into text in specified language

This API can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation.

>!Translation incurs additional fees. For more information, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009).

#### API prototype  

```
ITMGPTT virtual int SpeechToText(const char* fileID,const char* speechLanguage)
ITMGPTT virtual int SpeechToText(const char* fileID,const char* speechLanguage,const char* translateLanguage)
```

| Parameter | Type | Description |
| ----------------- | :---: | ------------------------------------------------------------ |
| fileID            | const char* | The URL of the audio file, which will be retained on the server for 90 days.                           |
| speechLanguage    | const char* | The language in which the audio file is to be converted to text. For parameters, see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260). |
| translatelanguage | const char* | The language in which the audio file is to be translated to text. For parameters, see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260). |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->SpeechToText(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```



### Callback for recognition

After the specified audio file is converted to text, the event message ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE will be returned, which will be identified in the `OnEvent` function.
The passed parameters include `result`, `file_path` and `text` (recognized text).

| Parameter | Type | Description |
| ------ | :-----: | ------------------------------------ |
| result |  int32  | 0: recording is completed              |
| fileid | FString | URL of recording file, which will be retained on the server for 90 days |
| text   | FString | Converted text                       |

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
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
	...
		else if (eventType == ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE) {
			int32 result = JsonObject->GetIntegerField(TEXT("result"));
			FString text = JsonObject->GetStringField(TEXT("text"));
			FString fileid = JsonObject->GetStringField(TEXT("file_id"));
			onPttSpeech2TextCompleted(result, fileid, text);
		}
	}
}
```

## Voice Message Volume Level APIs

| API | Description |
| ---------------- | :----------------: |
| GetMicLevel | Gets real-time mic volume level |
| SetMicVolume | Sets recording volume level |
| GetMicVolume | Gets recording volume level |
| GetSpeakerLevel | Gets real-time speaker volume |
| SetSpeakerVolume | Sets playback volume level |
| GetSpeakerVolume | Gets playback volume level |

### Getting the real-time mic volume of voice message

This API is used to get the real-time mic volume. An int-type value will be returned. Value range: 0-200.

#### API prototype  

```
ITMGPTT virtual int GetMicLevel()
```

#### Sample code  

```
ITMGContext.GetInstance(this).GetPTT().GetMicLevel();
```

### Setting the recording volume of voice message

This API is used to set the recording volume of voice message. Value range: 0-200.

#### API prototype  

```
ITMGPTT virtual int SetMicVolume(int vol)
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->SetMicVolume(100);
```

### Getting the recording volume of voice message

This API is used to get the recording volume of voice message. An int-type value will be returned. Value range: 0-200.

#### API prototype  

```
ITMGPTT virtual int GetMicVolume()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->GetMicVolume();
```

### Getting the real-time speaker volume of voice message

This API is used to get the real-time speaker volume. An int-type value will be returned. Value range: 0-200.

#### API prototype  

```
ITMGPTT virtual int GetSpeakerLevel()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->GetSpeakerLevel();
```

### Setting the playback volume of voice message

This API is used to set the playback volume of voice message. Value range: 0-200.

#### API prototype  

```
ITMGPTT virtual int SetSpeakerVolume(int vol)
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->SetSpeakerVolume(100);
```

### Getting the playback volume of voice message

This API is used to get the playback volume of voice message. An int-type value will be returned. Value range: 0-200.

#### API prototype  

```
ITMGPTT virtual int GetSpeakerVolume()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->GetSpeakerVolume();
```

## Advanced APIs

### Getting version number

This API is used to get the SDK version number for SDK usage analysis.

#### API prototype

```
ITMGContext virtual const char* GetSDKVersion()
```

#### Sample code  

```
ITMGContextGetInstance()->GetSDKVersion();
```


### Setting log printing level

This API is used to set the level of logs to be printed, and needs to be called before the initialization. It is recommended to keep the default level.

#### API prototype

```
ITMGContext int SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### Parameter description

| Parameter | Type | Description |
| ---------- | -------------- | ------------------------------------------------------------ |
| levelWrite | ITMG_LOG_LEVEL | Sets the level of logs to be written. `TMG_LOG_LEVEL_NONE` indicates not to write. Default value: TMG_LOG_LEVEL_INFO |
| levelPrint | ITMG_LOG_LEVEL | Sets the level of logs to be printed. `TMG_LOG_LEVEL_NONE` indicates not to print. Default value: TMG_LOG_LEVEL_ERROR |

`ITMG_LOG_LEVEL` description:

| ITMG_LOG_LEVEL | Description |
| --------------------- | -------------------- |
| TMG_LOG_LEVEL_NONE | Does not print logs |
| TMG_LOG_LEVEL_ERROR | Prints error logs (default) |
| TMG_LOG_LEVEL_INFO | Prints info logs |
| TMG_LOG_LEVEL_DEBUG | Prints debug logs |
| TMG_LOG_LEVEL_VERBOSE | Prints verbose logs |

#### Sample code  

```
ITMGContextGetInstance()->SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```



### Setting the log printing path

This API is used to set the log printing path. The default path is as follows. It needs to be called before Init.

| OS | Path |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName |
| iOS | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files |
| Mac | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

#### API prototype

```
ITMGContext virtual int SetLogPath(const char* logDir) 
```

| Parameter | Type | Description |
| ------ | :----: | ---- |
| logDir | const char* | Path |

#### Sample code  

```
cosnt char* logDir = ""// Set a path by yourself
ITMGContext* context = ITMGContextGetInstance();
context->SetLogPath(logDir);
```

## Callback Messages


| Message										| Description | Parameter | Sample |
| ----------------------------------------	|-----| :-----------------------------------------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM						| A member entered the audio room			|result; error_info	| {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM						| A member exited the audio room			|result; error_info	| {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT					| The room was disconnected for network or other reasons |result; error_info	| {"error_info":"waiting timeout, please check your network","result":0} |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE						| Room members were updated |user_list; event_id| {"event_id":1,"user_list":["0"]}                             |
| ITMG_MAIN_EVENT_TYPE_RECONNECT_START					| The reconnection to the room started |result; error_info	| {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS				| The reconnection to the room succeeded |result; error_info	| {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_SWITCH_ROOM						| The room was quickly switched |result; error_info	| {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE					| The room status was changed |result; error_info; sub_event_type; new_room_type | {"error_info":"","new_room_type":0,"result":0}               |
| ITMG_MAIN_EVENT_TYPE_ROOM_SHARING_START				| Cross-room mic connect started |result;			| {"result":0} |
| ITMG_MAIN_EVENT_TYPE_ROOM_SHARING_STOP				| Cross-room mic connect stopped |result;			| {"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_DEFAULT_DEVICE_CHANGED	| The default speaker device was changed |result; error_info	| {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE				| A new speaker device was added |                result; error_info                 | {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE				| A speaker device was lost | result; error_info                 | {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE			| A new mic device was added |result; error_info                 | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE			| A mic device was lost |result; error_info                 | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_DEFAULT_DEVICE_CHANGED	| The default mic device was changed |result; error_info                 | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY		| The room quality changed |weight; loss; delay                | {"weight":5,"loss":0.1,"delay":1}                            |
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE		| Voice message recording was completed |          result; file_path                 | {"file_path":"","result":0}                                  |
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE		| Voice message upload was completed |result; file_path;file_id             | {"file_id":"","file_path":"","result":0}                     |
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE		| Voice message download was completed |result; file_path;file_id             | {"file_id":"","file_path":"","result":0}                     |
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE		| Voice message playback was completed |result; file_path                 | {"file_path":"","result":0}                                  |
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE		| Fast speech-to-text conversion was completed |result; text;file_id                | {"file_id":"","text":"","result":0}                          |
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE| Streaming speech-to-text conversion was completed |result; file_path; text;file_id          | {"file_id":"","file_path":","text":"","result":0}            |
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING | Streaming speech-to-text conversion is in progress |result; file_path; text;file_id          | {"file_id":"","file_path":","text":"","result":0}            |
| ITMG_MAIN_EVNET_TYPE_PTT_TEXT2SPEECH_COMPLETE		| Text-to-speech conversion was completed |result; text;file_id                | {"file_id":"","text":"","result":0}                          |
| ITMG_MAIN_EVNET_TYPE_PTT_TRANSLATE_TEXT_COMPLETE	| Text translation was completed |result; text;file_id                | {"file_id":"","text":"","result":0}                          |

