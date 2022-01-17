This document provides a detailed description that makes it easy for Unreal Engine speech-to-text service developers to debug and integrate the APIs for Tencent Cloud’s Game Multimedia Engine (GME).



<dx-alert infotype="explain" title="">
This document applies to GME SDK version 2.8.
</dx-alert>



## Key Considerations for Using GME

GME provides two services: voice chat service and voice message and speech-to-text service, both of which rely on key APIs such as Init and Poll.

<dx-alert infotype="notice" title="Note on Init API">
If you need to use voice chat and voice message services at the same time, **you only need to call `Init` API once**.
The billing will not start after initialization. Receiving or sending a voice message in speech-to-text service is counted as a voice message DAU.
</dx-alert>

![image](https://main.qcloudimg.com/raw/99d612d90268a7248f5b55c385eeb8b8.png)

### Directions

<dx-steps>
-<dx-tag-link link="#Init" tag="API: Init">Initializing GME</dx-tag-link>
-<dx-tag-link link="#Poll" tag="API: Poll">Calling Poll periodically to trigger event callbacks</dx-tag-link>
-<dx-tag-link link="#ApplyPtt" tag="API: ApplyPTTAuthbuffer">Initializing authentication</dx-tag-link>
-<dx-tag-link link="#StartRWSR" tag="API: StartRecordingWithStreamingRecognition">Starting streaming speech recognition</dx-tag-link>
-<dx-tag-link link="#Stop" tag="API: StopRecording">Stop recording</dx-tag-link>
-<dx-tag-link link="#UnInit" tag="API: UnInit">Uninitializing GME</dx-tag-link>
</dx-steps>

### Important notes

- Configure your project before using GME; otherwise, the SDK will not take effect.
- After a GME API is called successfully, `QAVError.OK` will be returned with the value being 0.
- GME APIs should be called in the same thread.
- The `Poll` API should be called periodically for GME to trigger event callbacks.
- For detailed error code, please see <dx-tag-link link="https://cloud.tencent.com/document/product/607/15173" tag="ErrorCode">Error Codes</dx-tag-link>.

### C++ classes

| Class | Description |
| ----------- | :------------------: |
| ITMGContext | Key APIs |
| ITMGPTT | Speech-to-Text APIs |

## Key APIs

Before the initialization, the SDK is in the uninitialized status, and **you need to initialize it through the `Init` API** before you can use the voice chat and speech-to-text services.

**You need to call the `Init` API before calling any APIs of GME.**

If you have any questions when using the service, please see [General](https://intl.cloud.tencent.com/zh/document/product/607/30254).

| API | Description |
| ------ | :----------: |
| Init | Initializes GME |
| Poll | Triggers event callback |
| Pause | Pauses the system |
| Resume | Resumes the system |
| Uninit | Uninitializes GME |



<dx-alert infotype="notice" title="">
If you need to switch the account, please call `UnInit` to uninitialize the SDK. No fee is incurred for calling Init API.
</dx-alert>



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

- This API is used to initialize the GME service. It is recommended to call it when initializing the application. No fee is incurred for calling this API.
- **The openID uniquely identifies a user with the rules stipulated by the application developer and unique in the application (currently, only INT64 is supported)**.



<dx-alert infotype="notice" title="">
The Init API must be called in the same thread with other APIs. It is recommended to call all APIs in the main thread.
</dx-alert>




#### Function prototype

```
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
```

| Parameter | Type | Description |
| -------- | :---------: | ------------------------------------------------------------ |
| sdkAppId | const char* | `AppID` provided by the GME service from the [Tencent Cloud console](https://console.cloud.tencent.com/gamegme) |
| openId | const char* | `openId` can only be in Int64 type, which is passed after being converted to a const char*. |



#### Returned values

| Returned Value | Description |
| ------------------------------- | --------------------------------------------- |
| AV_OK = 0                  | Initialized SDK successfully. |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | Checks whether the SDK file is complete. It is recommended to delete it and then import the SDK again. |

The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is **only a reminder** but will not cause an initialization failure.

<dx-alert infotype="notice" title="Notes on 7015 error code">

- The 7015 error code is judged by md5. If this error is reported during integration, please check the integrity and version of the SDK file as prompted.
- Due to the third-party reinforcement, Unity packaging mechanism and other factors, the md5 of the library file will be affected, resulting in misjudgment. **Please ignore this error in the logic for official release**, and try to avoid displaying it in the UI.
  </dx-alert>



#### Sample code 

```
std::string appid = TCHAR_TO_UTF8(CurrentWidget->editAppID->GetText().ToString().operator*());
std::string userId = TCHAR_TO_UTF8(CurrentWidget->editUserID->GetText().ToString().operator*());
ITMGContextGetInstance()->Init(appid.c_str(), userId.c_str());
```

### [Triggering event callback](id:Poll)

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. The `Poll` API should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run exceptionally.
Refer to the UEDemoLevelScriptActor.cpp file in [Demo](https://intl.cloud.tencent.com/zh/document/product/607/18521).

<dx-alert infotype="alarm" title="Calling the `Poll` API periodically">
The `Poll` API must be called periodically and in the main thread to avoid abnormal API callbacks.
</dx-alert>



#### Function prototype

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

#### Function prototype

```
ITMGContext int Pause()
```

### Resuming the system

When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.

#### Function prototype

```
ITMGContext int Resume()

```



### [Uninitializing SDK](id:UnInit)

This API is used to uninitialize the SDK to make it uninitialized. **Switching accounts requires uninitialization**.

#### Function prototype

```
ITMGContext int Uninit()

```

## Speech-to-Text

Voice message refers to recording and sending a voice message. At the same time, the voice message can be converted to text and translated, as shown below:

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_DsvaLv.gif" width="50%">



<dx-alert infotype="explain" title="">
 - It is recommended to use the streaming speech-to-text service.
- You do not need to enter a voice chat room when using the voice message service.
</dx-alert>




#### Voice message and speech-to-text conversion flowchart

<img src="https://main.qcloudimg.com/raw/310eaf2b780c5fc47ffeaf791a6df392.png" width="60%">



## Accessing Voice Message and Speech-to-Text Service

### Voice message and speech-to-text APIs

| API | Description |
| -------------------------------------- | :------------------: |
| ApplyPTTAuthbuffer | Initializes authentication |
| SetMaxMessageLength | Specifies the maximum length of voice message |
| StartRecording | Starts recording |
| StartRecordingWithStreamingRecognition | Starts streaming recording |
| PauseRecording | Pauses recording |
| ResumeRecording | Resumes recording |
| StopRecording | Stops recording |
| CancelRecording | Cancels recording |
| GetMicLevel | Gets the real-time mic volume |
| SetMicVolume | Sets the recording volume |
| GetMicVolume | Gets the recording volume |
| GetSpeakerLevel | Gets the real-time speaker volume |
| SetSpeakerVolume | Sets the playback volume |
| GetSpeakerVolume | Gets the playback volume |
| UploadRecordedFile | Uploads the audio file |
| DownloadRecordedFile | Downloads the audio file |
| PlayRecordedFile | Plays back audio |
| StopPlayFile | Stops playing back audio |
| GetFileSize | Gets the audio file size |
| GetVoiceFileDuration | Gets the audio file duration |
| SpeechToText | Converts speech to text |



<dx-alert infotype="alarm" title="Maximum recording duration">
The maximum recording duration of a voice message is 58 seconds by default, and the minimum recording duration cannot be less than 1 second. If you want to customize the recording duration, for example, to modify the maximum recording duration to 10 seconds, please call the `SetMaxMessageLength` API to set it after initialization.
</dx-alert>



### Initializing the SDK

Before the initialization, the SDK is in the uninitialized status, and you need to initialize it through the `Init` API before you can use the voice chat and voice message services.

If you have any questions when using the service, please see [Speech-to-text Conversion](https://intl.cloud.tencent.com/zh/document/product/607/39716).

### Generating authentication information

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/zh/document/product/607/12218).    

#### Function prototype

```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);

```

| Parameter | Type | Description |
| ------------- | :---: | ------------------------------------------------------------ |
| dwSdkAppID | int | `AppId` from the Tencent Cloud console.|
| strRoomID     | char* | Room ID, which can contain up to 127 characters (for voice messaging and speech-to-text service, enter `null`). |
| strOpenID     | char* | User ID, which is the same as `openID` during initialization. |
| strKey        | char* | Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme). |
| strAuthBuffer | char* | Returned `authbuff`                                              |
| bufferLength  |  int  | Length of the `authbuff` passed in. 500 is recommended.                             |



### Application authentication

After the authentication information is generated, the authentication is assigned to the SDK.  

#### Function prototype  

```
ITMGPTT virtual int ApplyPTTAuthbuffer(const char* authBuffer, int authBufferLen)

```

| Parameter | Type | Description |
| ------------- | :---: | -------- |
| authBuffer    | char* | Authentication     |
| authBufferLen |  int  | Authentication length |

#### Sample code

```
ITMGContextGetInstance()->GetPTT()->ApplyPTTAuthbuffer(authBuffer,authBufferLen);

```

## Streaming Speech Recognition

### [Starting streaming speech recognition](id:StartRWSR)

This API is used to start streaming speech recognition. Text obtained from speech-to-text conversion will be returned in real time in its callback. It can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation. **To stop recording, call <dx-tag-link link="#Stop" tag="API: StopRecording"> Stop recording</dx-tag-link>**.

#### Function prototype  

```
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath) 
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath,const char* translateLanguage,const char* translateLanguage) 

```

| Parameter | Type | Description |
| ----------------- | :---: | ------------------------------------------------------------ |
| filePath          | char* | Path of stored audio file                                               |
| speechLanguage    | char* | The language in which the audio file is to be converted to text. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/zh/document/product/607/30260) |
| translateLanguage | char* | The language into which the audio file will be translated. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/zh/document/product/607/30260) (This parameter is currently unavailable. Enter the same value as that of `speechLanguage`) |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->StartRecordingWithStreamingRecognition(filePath,"cmn-Hans-CN","cmn-Hans-CN");

```

### Callback for streaming speech recognition

After streaming speech recognition is started, you need to listen for callback messages in the callback function `onEvent`. Event messages are divided into:

- `ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE` returns text after the recording is stopped and the recognition is completed, which is equivalent to returning the recognized text after a paragraph of speech.
- `ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING` returns the recognized text in real-time during the recording, which is equivalent to returning the recognized text while speaking.

The event message will be identified in the `OnEvent function` based on the actual needs. The passed parameters include the following four messages.

| Message Name | Description |
| --------- | :-----------------------------------------: |
| result | A return code for judging whether the streaming speech recognition is successful. |
| text | Text converted from speech |
| file_path | Local path of stored recording file |
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

### Starting recording

This API is used to start recording. The recording file must be uploaded first before you can perform operations such as speech-to-text conversion. **To stop recording, call `StopRecording`**.

#### Function prototype  

```
ITMGPTT virtual int StartRecording(const char* fileDir)

```

| Parameter | Type | Description |
| ------- | :---: | -------------- |
| fileDir | char* | Path of stored audio file |

#### Sample code  

```
string recordPath = Application.persistentDataPath + string.Format ("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecording(recordPath);


```

### [Stopping recording](id:Stop)

This API is used to stop recording. It is async, and a callback for recording completion will be returned after recording stops. A recording file will be available only after recording succeeds.

#### Function prototype  

```
ITMGPTT virtual int StopRecording()

```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->StopRecording();

```

### Callback for recording start

A callback will be executed through a delegate function to pass a message when recording is completed.

**To stop recording, call `StopRecording`**. The callback for recording start will be returned after the recording is stopped.

| Parameter | Type | Description |
| -------- | :-----: | ------------------------- |
| result   |  int32  | 0: recording is completed |
| filepath | FString | Path of stored recording file            |

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

#### Function prototype  

```
ITMGPTT virtual int PauseRecording()

```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->PauseRecording();

```

### Resuming recording

This API is used to resume recording.

#### Function prototype  

```
ITMGPTT virtual int ResumeRecording()

```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->ResumeRecording();

```

### Canceling recording

This API is used to cancel recording. **There is no callback after cancellation**.

#### Function prototype  

```
ITMGPTT virtual int CancelRecording()

```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->CancelRecording();

```

### Getting the real-time mic volume of voice message

This API is used to get the real-time mic volume. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGPTT virtual int GetMicLevel()

```

#### Sample code  

```
ITMGContext.GetInstance(this).GetPTT().GetMicLevel();



```

### Setting the recording volume of voice message

This API is used to set the recording volume of voice message. Value range: 0-200.

#### Function prototype  

```
ITMGPTT virtual int SetMicVolume(int vol)

```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->SetMicVolume(100);

```

### Getting the recording volume of voice message

This API is used to get the recording volume of voice message. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGPTT virtual int GetMicVolume()

```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->GetMicVolume();

```

### Getting the real-time speaker volume of voice message

This API is used to get the real-time speaker volume. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGPTT virtual int GetSpeakerLevel()

```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->GetSpeakerLevel();

```

## Voice Message Playback

### Playing back audio

This API is used to play back audio.

#### Function prototype  

```
ITMGPTT virtual int PlayRecordedFile(const char* filePath)

```

| Parameter | Type | Description |
| -------- | :---: | ------------------ |
| filePath | char* | Local audio file path |

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

#### Function prototype  

```
ITMGPTT virtual int StopPlayFile()

```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->StopPlayFile();

```

### Setting the playback volume of voice message

This API is used to set the playback volume of voice message. Value range: 0-200.

#### Function prototype  

```
ITMGPTT virtual int SetSpeakerVolume(int vol)

```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->SetSpeakerVolume(100);

```

### Getting the playback volume of voice message

This API is used to get the playback volume of voice message. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGPTT virtual int GetSpeakerVolume()

```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->GetSpeakerVolume();

```

### Getting audio file size

This API is used to get the size of an audio file.

#### Function prototype  

```
ITMGPTT virtual int GetFileSize(const char* filePath)

```

| Parameter | Type | Description |
| -------- | :---: | -------------------------------- |
| filePath | char* | Path of audio file, which is a local path |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->GetFileSize(filePath);


```

### Getting audio file duration

This API is used to get the duration of an audio file in milliseconds.

#### Function prototype  

```
ITMGPTT virtual int GetVoiceFileDuration(const char* filePath)

```

| Parameter | Type | Description |
| -------- | :---: | -------------------------------- |
| filePath | char* | Path of audio file, which is a local path |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->GetVoiceFileDuration(filePath);

```

## Voice Message Upload and Download

### Uploading an audio file

This API is used to upload an audio file.

#### Function prototype  

```
ITMGPTT virtual int UploadRecordedFile(const char* filePath)

```

| Parameter | Type | Description |
| -------- | :---: | -------------------------------- |
| filePath | char* | Path of uploaded audio file, which is a local path |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->UploadRecordedFile(filePath);

```

### Callback for audio file upload completion

A callback will be executed through a delegate function to pass a message when the upload of audio file is completed.

#### Function prototype

```
// Delegate function
public delegate void QAVUploadFileCompleteCallback(int code, string filepath, string fileid);
// Event-triggered function
public abstract event QAVUploadFileCompleteCallback OnUploadFileComplete; 


```

| Parameter | Type | Description |
| -------- | :-----: | ----------------------- |
| result   |  int32  | 0: recording is completed |
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

#### Function prototype  

```
ITMGPTT virtual int DownloadRecordedFile(const char* fileId, const char* filePath) 

```

| Parameter | Type | Description |
| -------- | :---: | ------------------ |
| fileId   | char* | URL path of file    |
| filePath | char* | Local path of saved file |

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
| 12291 | Network storage system exception | The server failed to get the audio file. Check whether the API parameter `fileid` is correct, whether the network is normal, and whether the file exists in COS. |
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

## Speech-to-Text Service

### Converting audio file to text

This API is used to convert a specified audio file to text.

#### Function prototype  

```
ITMGPTT virtual void SpeechToText(const char* fileID)

```

| Parameter | Type | Description |
| ------ | :---: | ------------ |
| fileID | char* | Audio file URL |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->SpeechToText(fileID);

```



### Translating audio file into text in specified language

This API can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation.

#### Function prototype  

```
ITMGPTT virtual int SpeechToText(const char* fileID,const char* speechLanguage,const char* translateLanguage)

```

| Parameter | Type | Description |
| ----------------- | :---: | ------------------------------------------------------------ |
| fileID | char* | URL of audio file, which will be retained on the server for 90 days |
| speechLanguage | char* | The language in which the audio file is to be converted to text. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/zh/document/product/607/30260). |
| translatelanguage | char* | The language into which the audio file will be translated. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/zh/document/product/607/30260). This parameter is currently unavailable. Enter the same value as that of speechLanguage. |

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
| -------- | ---------------------- | ------------------------------------------------------------ |
| 32769 | An internal error occurred. | Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance. |
| 32770 | Network failed. | Check whether the device can access the internet. |
| 32772 | Failed to decode the returned packet. | Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance. |
| 32774 | No `appinfo` is set. | Check whether the authentication key is correct and whether the voice message and speech-to-text feature is initialized. |
| 32776 | `authbuffer` check failed. | Check whether `authbuffer` is correct. |
| 32784 | Incorrect speech-to-text conversion parameter. | Check whether the API parameter `fileid` in the code is empty. |
| 32785 | Speech-to-text translation returned an error. | Error with the backend of voice message and speech-to-text feature. Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance. |

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



## Advanced APIs

### Getting version number

This API is used to get the SDK version number for analysis.

#### Function prototype

```
ITMGContext virtual const char* GetSDKVersion()

```

#### Sample code  

```
ITMGContextGetInstance()->GetSDKVersion();

```

### Specifying the maximum duration of voice message

This API is used to specify the maximum duration of a voice message, which can be up to 58 seconds.

#### Function prototype

```
ITMGPTT virtual int SetMaxMessageLength(int msTime)

```

| Parameter | Type | Description |
| ------ | :--: | ----------------------------------------------- |
| msTime | int | Audio duration in ms. Value range: 1000 < msTime <= 58000 |

#### Sample code  

```
int msTime = 10000;
ITMGContextGetInstance()->GetPTT()->SetMaxMessageLength(msTime);

```

### Setting log printing level

This API is used to set the level of logs to be printed, and needs to be called before the initialization. It is recommended to keep the default level.

#### Function prototype

```
ITMGContext int SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)

```

#### Parameter description

| Parameter | Type | Description |
| ---------- | -------------- | ------------------------------------------------------------ |
| levelWrite | ITMG_LOG_LEVEL | Sets the level of logs to be written. `TMG_LOG_LEVEL_NONE` indicates not to write. Default value: TMG_LOG_LEVEL_INFO |
| levelPrint | ITMG_LOG_LEVEL | Sets the level of logs to be printed. `TMG_LOG_LEVEL_NONE` indicates not to print. Default value: TMG_LOG_LEVEL_ERROR |

#### ITMG_LOG_LEVEL

| ITMG_LOG_LEVEL | Description |
| --------------------- | -------------------- |
| TMG_LOG_LEVEL_NONE | Does not print logs |
| TMG_LOG_LEVEL_ERROR | Prints error logs (default) |
| TMG_LOG_LEVEL_INFO | Prints info logs |
| TMG_LOG_LEVEL_DEBUG | Prints debug logs |
| TMG_LOG_LEVEL_VERBOSE | Prints verbose logs |

#### Sample code  

```
ITMGContext.GetInstance().SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);


```



### Setting the log printing path

This API is used to set the log printing path. The default path is as follows:

| OS | Path |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName |
| iOS | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files |
| Mac | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

#### Function prototype

```
ITMGContext virtual int SetLogPath(const char* logDir) 

```

| Parameter | Type | Description |
| ------ | :---: | ---- |
| logDir | char* | Path |

#### Sample code  

```
cosnt char* logDir = ""// Set a path by yourself

ITMGContext* context = ITMGContextGetInstance();
context->SetLogPath(logDir);


```

## Callback Messages

### Message list

| Message | Description |   
| ------------- |:-------------:|
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM | Indicates that a member enters an audio room. |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM | Indicates that a member exits an audio room. |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | Indicates that a room is disconnected for network or other reasons. |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE | Indicates a room type change event. |
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE | Indicates that a new mic is added |
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE | Indicates that a mic is lost |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE | Indicates that a new speaker is added |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE | Indicates that a speaker is lost |
| ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH | Indicates that the accompaniment is over. |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | Indicates that the room members are updated. |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_USERS_UPDATE | Indicates that the room member quantity is updated. |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_AUDIOSTREAMS_UPDATE | Indicates that the room audio stream quantity is updated. |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY | Indicates the room quality information. |
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE | Indicates that PTT recording is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE | Indicates that PTT upload is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE | Indicates that PTT download is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE | Indicates that PTT playback is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE | Indicates that speech-to-text conversion is completed. |

### Data list

| Message | Data | Sample |
| ------------------------------------------------------ | :-----------------------------------------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM | result; error_info | {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM | result; error_info | {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | result; error_info | {"error_info":"waiting timeout, please check your network","result":0} |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE | result; error_info; sub_event_type; new_room_type | {"error_info":"","new_room_type":0,"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE | result; error_info | {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE | result; error_info | {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE | result; error_info | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE | result; error_info | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | user_list;  event_id | {"event_id":1,"user_list":["0"]} |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_USERS_UPDATE | AllUser; AccUser; ProxyUser | {"AllUser":3,"AccUser":2,"ProxyUser":1} |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_AUDIOSTREAMS_UPDATE | AudioStreams | {"AudioStreams":3} |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY | weight; loss; delay | {"weight":5,"loss":0.1,"delay":1} |
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE | result; file_path | {"file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE | result; file_path;file_id | {"file_id":"","file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE | result; file_path;file_id | {"file_id":"","file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE | result; file_path | {"file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE | result; text;file_id | {"file_id":"","text":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE | result; file_path; text;file_id | {"file_id":"","file_path":","text":"","result":0} |
