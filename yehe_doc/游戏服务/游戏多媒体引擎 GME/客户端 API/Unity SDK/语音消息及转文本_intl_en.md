This document provides a detailed description that makes it easy for Unity speech-to-text service developers to debug and integrate the APIs for Tencent Cloud’s Game Multimedia Engine (GME).

>?This document applies to GME SDK version 2.8.

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
- For detailed error code, please see <dx-tag-link link="https://intl.cloud.tencent.com/document/product/607/33223" tag="ErrorCode">Error Codes</dx-tag-link>.

### C# classes

| Class | Description |
| ----------- | :----------------------: |
| ITMGContext | Key APIs |
| ITMGPTT | Speech-to-Text APIs |

## Key APIs

Before the initialization, the SDK is in the uninitialized status, and **you need to initialize it through the `Init` API** before you can use the voice chat and speech-to-text services.

**You need to call the `Init` API before calling any APIs of GME.**


If you have any questions when using the service, please see [General Issues](https://intl.cloud.tencent.com/document/product/607/30254).

| API | Description |
| ------ | :----------: |
| Init | Initializes GME |
| Poll | Triggers event callback |
| Pause | Pauses the system |
| Resume | Resumes the system |
| Uninit | Uninitializes GME |

>!If you need to switch the account, please call `UnInit` to uninitialize the SDK. No fee is incurred for calling Init API.

### Imported header files

```
using TencentMobileGaming;
```

### Getting an instance

Get the `Context` instance by using the `ITMGContext` method instead of `QAVContext.GetInstance()`.

### [Initializing SDK](id:Init)

- This API is used to initialize the GME service. It is recommended to call it when initializing the application. No fee is incurred for calling this API.
- **For more information on how to get the `sdkAppID` parameter, please see [Voice Service Activation Guide](https://intl.cloud.tencent.com/document/product/607/39698)**.
- **The openID uniquely identifies a user with the rules stipulated by the application developer and unique in the application (currently, only INT64 is supported)**.

> !The Init API must be called in the same thread with other APIs. It is recommended to call all APIs in the main thread.

#### Function prototype

```
//class ITMGContext
public abstract int Init(string sdkAppID, string openID);
```

| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | string | `AppID` provided by the GME service from the [Tencent Cloud console](https://console.cloud.tencent.com/gamegme) |
| openId | string | `openId` can only be in Int64 type, which is passed after being converted to a string. |



#### Returned values

| Returned Value | Description |
| ------------------------------- | --------------------------------------------- |
| QAVError.OK= 0 | Initialized SDK successfully |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | Checks whether the SDK file is complete. It is recommended to delete it and then import the SDK again. |

The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is **only a reminder** but will not cause an initialization failure.


<dx-alert infotype="notice" title="Notes on 7015 error code">
- The 7015 error code is judged by md5. If this error is reported during integration, please check the integrity and version of the SDK file as prompted.
- Due to the third-party reinforcement, Unity packaging mechanism and other factors, the md5 of the library file will be affected, resulting in misjudgment. **Please ignore this error in the logic for official release**, and try to avoid displaying it in the UI.
</dx-alert>




#### Sample code 

```
int ret = ITMGContext.GetInstance().Init(sdkAppId, openID);
// Determine whether the initialization is successful by the returned value
if (ret != QAVError.OK)
    {
        Debug.Log("SDK initialization failed:"+ret);
        return;
    }
```


### [Triggering event callback](id:Poll)

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. The `Poll` API should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run exceptionally.
Refer to the EnginePollHelper file in [Demo](https://intl.cloud.tencent.com/document/product/607/18521).


<dx-alert infotype="alarm" title="Calling the `Poll` API periodically">
The `Poll` API must be called periodically and in the main thread to avoid abnormal API callbacks.
</dx-alert>




#### Function prototype

```
ITMGContext public abstract int Poll();
```

#### Sample code

```
public void Update()
    {
        ITMGContext.GetInstance().Poll();
    }
```

### Pausing the system

When a `Pause` event occurs in the system, the engine should also be notified for pause. For example, when the application switches to the background (OnApplicationPause, isPause=True), and you do not need the background to play back the audio in the room, please call `Pause` API to pause the GME service.

#### Function prototype

```
ITMGContext public abstract int Pause()
```

### Resuming the system

When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.

#### Function prototype

```
ITMGContext  public abstract int Resume()
```



### [Uninitializing SDK](id:UnInit)

This API is used to uninitialize the SDK to make it uninitialized. **Switching accounts requires uninitialization**.

#### Function prototype

```
ITMGContext public abstract int Uninit()
```


## Speech-to-Text

Voice message refers to recording and sending a voice message. At the same time, the voice message can be converted to text and translated, as shown below:

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_DsvaLv.gif" width="50%">

>?
>- It is recommended to use the streaming speech-to-text service.
>- You do not need to enter a voice chat room when using the voice message service.

#### Voice message and speech-to-text conversion flowchart

<img src="https://main.qcloudimg.com/raw/13ee122408ae95995bfce4fc0edb370f.png" width="70%">



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

If you have any questions when using the service, please see [Speech-to-text Conversion FAQs](https://intl.cloud.tencent.com/document/product/607/39716).

### Generating authentication information

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    


#### Function prototype

```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)


```

| Parameter | Type | Description |
| ------ | :----: | ------------------------------------------------------------ |
| appId | int | `AppId` from the Tencent Cloud console.|
| roomId | string | Enter null |
| openId | string | User ID, which is the same as `OpenId` during initialization. |
| key | string | Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme). |


### Application authentication

After the authentication information is generated, the authentication is assigned to the SDK.  


#### Function prototype  

```
ITMGPTT int ApplyPTTAuthbuffer (byte[] authBuffer)

```

| Parameter | Type | Description |
| ---------- | :----: | ---- |
| authBuffer | byte[] | Authentication |

#### Sample code

```
UserConfig.SetAppID(transform.Find ("appId").GetComponent<InputField> ().text);
UserConfig.SetUserID(transform.Find ("userId").GetComponent<InputField> ().text);
UserConfig.SetAuthKey(transform.Find("authKey").GetComponent<InputField>().text);
byte[] authBuffer = UserConfig.GetAuthBuffer(UserConfig.GetAppID(), UserConfig.GetUserID(), null,UserConfig.GetAuthKey());
ITMGContext.GetInstance ().GetPttCtrl ().ApplyPTTAuthbuffer(authBuffer);

```


## Streaming Speech Recognition


### [Starting streaming speech recognition](id:StartRWSR)

This API is used to start streaming speech recognition. Text obtained from speech-to-text conversion will be returned in real time in its callback. It can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation. **To stop recording, call <dx-tag-link link="#Stop" tag="API: StopRecording"> Stop recording</dx-tag-link>**.

#### Function prototype  

```
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath)
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath, string speechLanguage,string translateLanguage)

```

| Parameter | Type | Description |
| ----------------- | :----: | ------------------------------------------------------------ |
| filePath | String | Path of stored audio file |
| speechLanguage | String | The language in which the audio file is to be converted to text. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260) |
| translateLanguage | String | The language into which the audio file will be translated. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260) (This parameter is currently unavailable. Enter the same value as that of `speechLanguage`) |

#### Sample code  

```
string recordPath = Application.persistentDataPath + string.Format("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecordingWithStreamingRecognition(recordPath, "cmn-Hans-CN","cmn-Hans-CN");

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

>!The file_id is empty when the 'ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRecognition_IS_RUNNING' message is listened.

#### Error codes

| Error Code | Description | Suggested Solution |
| ------ | :--: | :------: |
| 32775 | Streaming speech-to-text conversion failed, but recording succeeded.| Call the `UploadRecordedFile` API to upload the recording file and then call the `SpeechToText` API to perform speech-to-text conversion. |
| 32777 | Streaming speech-to-text conversion failed, but recording and upload succeeded.| The message returned contains a backend URL after successful upload. Call the `SpeechToText` API to perform speech-to-text conversion. |
| 32786 | Streaming speech-to-text conversion failed. | During streaming recording, wait for the execution result of the streaming recording API to return. |

#### Sample code  

```
			// Listen on an event:
			ITMGContext.GetInstance().GetPttCtrl().OnStreamingSpeechComplete +=new QAVStreamingRecognitionCallback (OnStreamingSpeechComplete);
			ITMGContext.GetInstance().GetPttCtrl().OnStreamingSpeechisRunning += new QAVStreamingRecognitionCallback (OnStreamingRecisRunning);
			// Process the event listened on:
			void OnStreamingSpeechComplete(int code, string fileid, string filepath, string result){
					// Callback for streaming speech recognition
			}

			void OnStreamingRecisRunning(int code, string fileid, string filePath, string result){
					if (code == 0)
					{
						setBtnText(mStreamBtn, "Streaming");
						InputField field = transform.Find("recordFilePath").GetComponent<InputField>();
						field.text = filePath;

						field = transform.Find("downloadUrl").GetComponent<InputField>();
						field.text = "Stream is Running";

						field = transform.Find("convertTextResult").GetComponent<InputField>();
						field.text = result;
						showWarningText("Recording");
					}	
}

```



## Voice Message Recording

### Starting recording

This API is used to start recording. The recording file must be uploaded first before you can perform operations such as speech-to-text conversion. **To stop recording, call `StopRecording`**.

#### Function prototype  

```
ITMGPTT int StartRecording(string fileDir)

```

| Parameter | Type | Description |
| ------- | :----: | -------------- |
| fileDir | string | Path of stored audio file |

#### Sample code  

```
string recordPath = Application.persistentDataPath + string.Format ("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecording(recordPath);

```

### [Stopping recording](id:Stop)

This API is used to stop recording. It is async, and a callback for recording completion will be returned after recording stops. A recording file will be available only after recording succeeds.

#### Function prototype  

```
ITMGPTT int StopRecording()

```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().StopRecording();

```


### Callback for recording start

A callback will be executed through a delegate function to pass a message when recording is completed.


**To stop recording, call `StopRecording`**. The callback for recording start will be returned after the recording is stopped.

#### Function prototype  

```
// Delegate function
public delegate void QAVRecordFileCompleteCallback(int code, string filepath); 
// Event function
public abstract event QAVRecordFileCompleteCallback OnRecordFileComplete;

```

| Parameter | Type | Description |
| -------- | :----: | ------------------------- |
| code | string | 0: recording is completed |
| filepath | string | Path of stored recording file |

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
// Listen on an event
ITMGContext.GetInstance().GetPttCtrl().OnRecordFileComplete +=  new QAVRecordFileCompleteCallback (OnRecordFileComplete);
// Process the event listened on
void OnRecordFileComplete(int code, string filepath){
    // Callback for recording start
}

```


### Pausing recording

This API is used to pause recording. If you want to resume recording, please call the `ResumeRecording` API.

#### Function prototype  

```
ITMGPTT int PauseRecording()

```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().PauseRecording();

```

### Resuming recording

This API is used to resume recording.

#### Function prototype  

```
ITMGPTT int ResumeRecording()

```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().ResumeRecording();

```



### Canceling recording

This API is used to cancel recording. **There is no callback after cancellation**.

#### Function prototype  

```
ITMGPTT int CancelRecording()

```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().CancelRecording();

```

### Getting the real-time mic volume of voice message

This API is used to get the real-time mic volume. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGPTT int GetMicLevel()

```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().GetMicLevel();


```

### Setting the recording volume of voice message

This API is used to set the recording volume of voice message. Value range: 0-200.

#### Function prototype  

```
ITMGPTT int SetMicVolume(int vol)

```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().SetMicVolume(100);

```

### Getting the recording volume of voice message

This API is used to get the recording volume of voice message. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGPTT int GetMicVolume()

```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().GetMicVolume();

```

### Getting the real-time speaker volume of voice message

This API is used to get the real-time speaker volume. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGPTT int GetSpeakerLevel()

```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().GetSpeakerLevel();

```


## Voice Message Playback

### Playing back audio

This API is used to play back audio.

#### Function prototype  

```
ITMGPTT PlayRecordedFile(string filePath)
ITMGPTT PlayRecordedFile(string filePath,int voiceType);

```

| Parameter | Type | Description |
| --------- | :----: | ------------------------------------------------------------ |
| filePath | string | Local audio file path |
| voicetype | int | Voice changer type. For more information, please see [Real-time Sound Effect](https://intl.cloud.tencent.com/document/product/607/31503). |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ---------- | ------------------------------ |
| 20485 | Playback is not started. | Ensure the existence of the file and the validity of the file path. |

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().PlayRecordedFile(filePath); 

```

### Callback for audio playback

A callback will be executed through a delegate function to pass a message when an audio file is played back.

#### Function prototype  

```
// Delegate function
public delegate void QAVPlayFileCompleteCallback(int code, string filepath);
// Event function
public abstract event QAVPlayFileCompleteCallback OnPlayFileComplete;

```

| Parameter | Type | Description |
| -------- | :----: | ----------------------- |
| code | int | 0: playback is completed |
| filepath | string | Path of stored recording file |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| 20481 | Initialization error. | Check whether the device is being used, whether the permissions are normal, and whether the initialization is normal. |
| 20482 | During playback, the client tried to interrupt and play back the next one but failed (which should succeed normally). | Check whether the code logic is correct. |
| 20483 | Parameter is empty. | Check whether the API parameters in the code are correct. |
| 20484 | Internal error. | An error occurred while initializing the player. This error code is generally caused by failure in decoding, and the error should be located with the aid of logs. |

#### Sample code

```
// Listen on an event:
ITMGContext.GetInstance().GetPttCtrl().OnPlayFileComplete +=new  QAVPlayFileCompleteCallback(OnPlayFileComplete);
// Process the event listened on:
void OnPlayFileComplete(int code, string filepath){
    // Callback for audio playback
}


```



### Stopping audio playback

This API is used to stop audio playback. There will be a callback for playback completion when the playback stops.

#### Function prototype  

```
ITMGPTT int StopPlayFile()

```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().StopPlayFile();

```


### Setting the playback volume of voice message

This API is used to set the playback volume of voice message. Value range: 0-200.

#### Function prototype  

```
ITMGPTT int SetSpeakerVolume(int vol)

```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().SetSpeakerVolume(100);

```

### Getting the playback volume of voice message

This API is used to get the playback volume of voice message. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGPTT int GetSpeakerVolume()

```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().GetSpeakerVolume();

```

### Getting audio file size

This API is used to get the size of an audio file.

#### Function prototype  

```
ITMGPTT GetFileSize(string filePath) 

```

| Parameter | Type | Description |
| -------- | :----: | -------------------------------- |
| filePath | string | Path of audio file, which is a local path. |

#### Sample code  

```
int fileSize = ITMGContext.GetInstance().GetPttCtrl().GetFileSize(filepath);

```

### Getting audio file duration

This API is used to get the duration of an audio file in milliseconds.

#### Function prototype  

```
ITMGPTT int GetVoiceFileDuration(string filePath)

```

| Parameter | Type | Description |
| -------- | :----: | -------------------------------- |
| filePath | string | Path of audio file, which is a local path. |

#### Sample code  

```
int fileDuration = ITMGContext.GetInstance().GetPttCtrl().GetVoiceFileDuration(filepath);

```


## Voice Message Upload and Download

### Uploading an audio file

This API is used to upload an audio file.

#### Function prototype  

```
ITMGPTT int UploadRecordedFile (string filePath)

```

| Parameter | Type | Description |
| -------- | :----: | -------------------------------- |
| filePath | String | Path of uploaded audio file, which is a local path. |

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().UploadRecordedFile(filePath);

```

### Callback for audio file upload completion

A callback will be executed through a delegate function to pass a message when the upload of audio file is completed.

#### Function prototype

```
// Delegate function
public delegate void QAVUploadFileCompleteCallback(int code, string filepath, string fileid);
// Event function
public abstract event QAVUploadFileCompleteCallback OnUploadFileComplete; 

```

| Parameter | Type | Description |
| -------- | :----: | ----------------------- |
| code | int | 0: recording is completed |
| filepath | string | Path of stored recording file |
| fileid | string | File URL path |

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
// Listen on an event
ITMGContext.GetInstance().GetPttCtrl().OnUploadFileComplete +=new QAVUploadFileCompleteCallback (OnUploadFileComplete);
// Process the event listened on
void OnUploadFileComplete(int code, string filepath, string fileid){
    // Callback for audio file upload completion
}

```

### Downloading the audio file

This API is used to download an audio file.

#### Function prototype  

```
ITMGPTT DownloadRecordedFile (string fileID, string downloadFilePath)

```

| Parameter | Type | Description |
| ---------------- | :----: | ------------------ |
| fileID | String | File URL path |
| downloadFilePath | string | Local path of saved file |

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().DownloadRecordedFile(fileId, filePath);

```

### Callback for audio file download completion

A callback will be executed through a delegate function to pass a message when the download of audio file is completed.

#### Function prototype  

```
// Delegate function
public delegate void QAVDownloadFileCompleteCallback(int code, string filepath, string fileid);
// Event function
public abstract event QAVDownloadFileCompleteCallback OnDownloadFileComplete;

```

| Parameter | Type | Description |
| -------- | :----: | --------------------------------------- |
| code | int | 0: recording is completed |
| filepath | string | Path of stored recording file |
| fileid | string | URL path of file, which will be retained on the server for 90 days |

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
// Listen on an event
ITMGContext.GetInstance().GetPttCtrl().OnDownloadFileComplete +=new QAVDownloadFileCompleteCallback(OnDownloadFileComplete);
// Process the event listened on
void OnDownloadFileComplete(int code, string filepath, string fileid){
    // Callback for audio file download completion
}


```


## Speech-to-Text Service


### Converting audio file to text

This API is used to convert a specified audio file to text.

#### Function prototype  

```
ITMGPTT int SpeechToText(String fileID)

```

| Parameter | Type | Description |
| ------ | :----: | ------------ |
| fileID | String | Audio file URL |

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID);

```



### Translating audio file into text in specified language

This API can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation.

#### Function prototype  

```
ITMGPTT int SpeechToText(String fileID,String speechLanguage)

```

| Parameter | Type | Description |
| ----------------- | :----: | ------------------------------------------------------------ |
| fileID | String | URL of audio file, which will be retained on the server for 90 days |
| speechLanguage | String | The language in which the audio file is to be converted to text. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260). |
| translatelanguage | String | The language into which the audio file will be translated. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260). This parameter is currently unavailable. Enter the same value as that of speechLanguage. |

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID,"cmn-Hans-CN","cmn-Hans-CN");

```



### Callback for recognition

A callback will be executed through a delegate function to pass a message when a specified audio file is recognized and converted to text.

#### Function prototype  

```
// Delegate function
public delegate void QAVSpeechToTextCallback(int code, string fileid, string result);
// Event function
public abstract event QAVSpeechToTextCallback OnSpeechToTextComplete;

```

| Parameter | Type | Description |
| ------ | :----: | ------------------------------------ |
| code | int | 0: recording is completed |
| fileid | string | URL of recording file, which will be retained on the server for 90 days |
| result | string | Converted text |

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
// Listen on an event
ITMGContext.GetInstance().GetPttCtrl().OnSpeechToTextComplete += new QAVSpeechToTextCallback(OnSpeechToTextComplete);
// Process the event listened on
void OnSpeechToTextComplete(int code, string fileid, string result){
    // Callback for recognition
}


```



## Advanced APIs

### Getting version number

This API is used to get the SDK version number for analysis.

#### Function prototype

```
ITMGContext  abstract string GetSDKVersion()

```

#### Sample code  

```
ITMGContext.GetInstance().GetSDKVersion();

```

### Specifying the maximum duration of voice message

This API is used to specify the maximum duration of a voice message, which can be up to 58 seconds.

#### Function prototype

```
ITMGPTT int SetMaxMessageLength(int msTime)

```

| Parameter | Type | Description |
| ------ | :--: | ----------------------------------------------- |
| msTime | int | Audio duration in ms. Value range: 1000 < msTime <= 58000 |

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().SetMaxMessageLength(58000); 

```

### Setting log printing level

This API is used to set the level of logs to be printed, and needs to be called before the initialization. It is recommended to keep the default level.

#### Function prototype

```
ITMGContext  SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)

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
| Windows | %appdata%\Tencent\GME\ProcessName                            |
| iOS | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files |
| Mac | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

#### Function prototype

```
ITMGContext  SetLogPath(string logDir)

```

| Parameter | Type | Description |
| ------ | :----: | ---- |
| logDir | String | Path |

#### Sample code  

```
ITMGContext.GetInstance().SetLogPath(path);

```


