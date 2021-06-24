This document provides a detailed description that makes it easy for Android voice message developers to debug and integrate the APIs for Tencent Cloud’s Game Multimedia Engine (GME).

> ?This document applies to GME SDK v2.8.

## Key Considerations for Using GME

GME provides two services: voice chat service and voice message and speech-to-text service, both of which rely on key APIs such as Init and Poll.

<dx-alert infotype="notice" title="Note on Init API">
If you need to use voice chat and voice message services at the same time, **you only need to call `Init` API once**.
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

### Voice message for Android class

| Class | Description |
| ----------- | :----------------------: |
| ITMGContext | Key APIs |
| ITMGPTT | Speech-to-Text APIs |

## Key APIs

Before the initialization, the SDK is in the uninitialized status, and **you need to initialize it through the `Init` API** before you can use the voice chat and speech-to-text services.

**You need to call the `Init` API before calling any APIs of GME.**


If you have any questions when using the service, please see [General FAQs](https://intl.cloud.tencent.com/document/product/607/30254).

| API | Description |
| ------ | :----------: |
| Init | Initializes GME |
| Poll | Triggers event callback |
| Pause | Pauses the system |
| Resume | Resumes the system |
| Uninit | Uninitializes GME |

>!If you need to switch the account, please call `UnInit` to uninitialize the SDK.
>


### Getting singleton

To use the voice feature, get the `ITMGContext` object first.

#### Sample code  

```java
import com.tencent.TMG.ITMGContext; 
ITMGContext.getInstance(this);
```

### Registering callback

The API class uses the `Delegate` method to send callback notifications to the application. Register the callback function to the SDK to receive callback messages.

#### Function prototype

Override this callback function in the constructor to process the parameters of the callback.
```java
static public abstract class ITMGDelegate {
    public void OnEvent(ITMG_MAIN_EVENT_TYPE type, Intent data){}
}
```

| Parameter | Type | Description |
| ---- | :------------------------------: | ------------------------ |
| type | ITMGContext.ITMG_MAIN_EVENT_TYPE | Event type in the callback response |
| data | Intent message type | Callback message, i.e., event data |



#### Sample code  
Register the callback function to the SDK before room entry.
```java
private ITMGContext.ITMGDelegate itmgDelegate = null;
itmgDelegate = new ITMGContext.ITMGDelegate() {
    @Override
    public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
        if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM == type)
        {
            // Analyze the returned result
            int nErrCode = data.getIntExtra("result" , -1);
            String strErrMsg = data.getStringExtra("error_info");
				}
		}
}
```



#### Function prototype 

```java
public abstract int SetTMGDelegate(ITMGDelegate delegate);
```

| Parameter | Type | Description |
| -------- | :----------: | ------------ |
| delegate | ITMGDelegate | SDK callback function |

#### Sample code  

```java
ITMGContext.GetInstance(this).SetTMGDelegate(itmgDelegate);
```


### [Initializing SDK](id:Init)

- This API is used to initialize the GME service. It is recommended to call it when initializing the application.
- **For more information on how to get the `sdkAppId` parameter, please see [Access Guide](https://intl.cloud.tencent.com/document/product/607/39698)**.
- **The openID uniquely identifies a user with the rules stipulated by the application developer and unique in the application (currently, only INT64 is supported)**.

#### Function prototype

```java
public abstract int Init(String sdkAppId, String openId);
```

| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | String | `AppId` provided by the GME service from the [Tencent Cloud console](https://console.cloud.tencent.com/gamegme) |
| OpenId |String | `OpenId` can only be in Int64 type, which is passed after being converted to a string. |

| Returned Value | Description |
| ------------------------------- | --------------------------------------------- |
| QAVError.OK= 0 | Initialized SDK successfully |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | Checks whether the SDK file is complete. It is recommended to delete it and then import the SDK again. |

The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is only a reminder but will not cause an initialization failure.

- If this error is reported during integration, please check the integrity and version of the SDK file as prompted.
- If this error is returned after executable file export, please ignore it and try to avoid displaying it in the UI.

#### Sample code 

```java
String sdkAppID = "14000*****";
String openID = "100";
int ret = ITMGContext.GetInstance(this).Init(sdkAppId, openId);
if(ret != 0){
				Log.e(TAG,"SDK initialization failed");
}
```


### [Triggering event callback](id:Poll)

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. The `Poll` API should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run exceptionally.
You can refer to the `EnginePollHelper.java` file in the demo.

#### Function prototype

```java
public abstract int Poll();
```

#### Sample code

```java
private Handler mhandler = new Handler();
private Runnable mRunnable = new Runnable() {
    @Override
    public void run() {
        if (s_pollEnabled) {
            if (ITMGContext.GetInstance(null) != null)
                ITMGContext.GetInstance(null).Poll();
        }
        mhandler.postDelayed(mRunnable, 33);
    }
};
```

### Pausing the system

When a `Pause` event occurs in the system, the engine should also be notified for pause.

#### Function prototype

```java
public abstract int Pause();
```

### Resuming the system

When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.

#### Function prototype

```java
public abstract int Resume();
```



### [Uninitializing SDK](id:UnInit)

This API is used to uninitialize the SDK to make it uninitialized. **Switching accounts requires uninitialization**.

#### Function prototype

```java
public abstract int Uninit();
```


## Speech-to-Text

Voice message refers to recording and sending a voice message. At the same time, the voice message can be converted to text and translated.

>?It is recommended to use the streaming voice-to-text service.

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


### Initializing SDK

Before the initialization, the SDK is in the uninitialized status, and you need to initialize it through the `Init` API before you can use the voice chat and voice message services.

If you have any questions when using the service, please see [Speech-to-Text Conversion](https://intl.cloud.tencent.com/document/product/607/39716).

### Authentication information

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    
To get authentication for voice message and speech-to-text, the room ID parameter must be set to `null`.

#### Function prototype

```java
AuthBuffer public native byte[] genAuthBuffer(int sdkAppId, String roomId, String openId, String key)
```

| Parameter | Type | Description |
| ------ | :----: | ------------------------------------------------------------ |
| appId | int | `AppId` from the Tencent Cloud console. |
| roomId | string | The room ID parameter must be set to `null`. |
| openId | string | User ID, which is the same as `openId` during initialization. |
| key | string | Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme). |



#### Sample code  

```java
import com.tencent.av.sig.AuthBuffer;// Header file
byte[] authBuffer = AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(sdkAppId), "0",openId, key);
```


### [Initializing authentication](id:ApplyPtt)

Call authentication initialization after initializing the SDK. For more information on how to get the `authBuffer`, please see `genAuthBuffer` (the voice chat authentication information API).

#### Function prototype  

```java
public abstract int ApplyPTTAuthbuffer(byte[] authBuffer);
```

| Parameter | Type | Description |
| ---------- | :----: | ---- |
| authBuffer | String | Authentication |

#### Sample code  

```java
byte[] authBuffer =  AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(sdkAppId), "0", openId, key);
ITMGContext.GetInstance(this).GetPTT().ApplyPTTAuthbuffer(authBuffer);
```


## Streaming Speech Recognition


### [Starting streaming speech recognition](id:StartRWSR)

This API is used to start streaming speech recognition. Text obtained from speech-to-text conversion will be returned in real time in its callback. It can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation. **To stop recording, call `StopRecording`**. The callback will be returned after the recording is stopped.

#### Function prototype  

```java
public abstract int StartRecordingWithStreamingRecognition (String filePath);
public abstract int StartRecordingWithStreamingRecognition (String filePath,String language,String translatelanguage);
public abstract int StopRecording();
```

| Parameter | Type | Description |
| ----------------- | :----: | ------------------------------------------------------------ |
| filePath | String | Path of stored audio file |
| speechLanguage | String | The language in which the audio file is to be converted to text. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260) |
| translateLanguage | String | The language into which the audio file will be translated. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260) (This parameter is currently unavailable. Enter the same value as that of `speechLanguage`) |

#### Sample code  

```java
String temple = getActivity().getExternalFilesDir(null).getAbsolutePath() + "/test_"+(index++)+".ptt";
ITMGContext.GetInstance(getActivity()).GetPTT().StartRecordingWithStreamingRecognition(temple,"cmn-Hans-CN","cmn-Hans-CN");
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
>

#### Error codes

| Error Code | Description | Suggested Solution |
| ------ | :--: | :------: |
| 32775 | Streaming speech-to-text conversion failed, but recording succeeded.| Call the `UploadRecordedFile` API to upload the recording file and then call the `SpeechToText` API to perform speech-to-text conversion. |
| 32777 | Streaming speech-to-text conversion failed, but recording and upload succeeded.| The message returned contains a backend URL after successful upload. Call the `SpeechToText` API to perform speech-to-text conversion. |
| 32786 | Streaming speech-to-text conversion failed. | During streaming recording, wait for the execution result of the streaming recording API to return. |

#### Sample code  

```java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE == type)
        	{
            	/Callback for streaming voice message and speech-to-text
                Handler mainHander = new Handler(Looper.getMainLooper());
                mainHander.post(new Runnable() {
                    @Override
                    public void run() {
                if (nErrCode ==0) {

                    String textString = templeData.getStringExtra("text");
                    EditText _editText = (EditText) root.findViewById(R.id.edit_audio_to_text);
                    _editText.setText(textString);

                    recordfilePath = templeData.getStringExtra("file_path");
                    mEditTextfiletoupload.setText(recordfilePath);

                    donwLoadUrlPath = templeData.getStringExtra("file_id");
                    mEditTextDownloadurl.setText(donwLoadUrlPath);

                    Log.e(TARGET, "STREAMINGRECOGNITION" + "nErrCode=" + nErrCode + ", content=" + textString+"recordfilePath"+recordfilePath+"donwLoadUrlPath"+donwLoadUrlPath);
                }
                else
                {

                    Toast.makeText(getActivity(), String.format("Streaming speech-to-text conversion failed. Error code: %d",nErrCode), Toast.LENGTH_SHORT).show();
                    Log.e(TARGET, "Streaming speech-to-text conversion failed. Error code"+nErrCode);
                }
                    }
                });
        	}
}
```



## Voice Message Recording

### Specifying the maximum duration of voice message

This API is used to specify the maximum duration of a voice message, which can be up to 58 seconds.

#### Function prototype

```java
public abstract int SetMaxMessageLength(int msTime);
```

| Parameter | Type | Description |
| ------ | :--: | ----------------------------------------------- |
| msTime | int | Audio duration in ms. Value range: 1000 < msTime <= 58000 |

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().SetMaxMessageLength(msTime);
```

### Starting recording

This API is used to start recording. The recording file must be uploaded first before you can perform operations such as speech-to-text conversion. **To stop recording, call `StopRecording`**.

#### Function prototype  

```java
public abstract int StartRecording(String filePath);
```

| Parameter | Type | Description |
| -------- | :----: | -------------- |
| filePath | String | Path of stored audio file |

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().StartRecording(filePath);
```

### [Stopping recording](id:Stop)

This API is used to stop recording. It is async, and a callback for recording completion will be returned after recording stops. A recording file will be available only after recording succeeds.

#### Function prototype  

```java
public abstract int StopRecording();
```

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().StopRecording();
```


### Callback for recording start

**To stop recording, call `StopRecording`**. The callback for recording start will be returned after the recording is stopped.

The callback function `OnEvent` will be called after recording is started. The event message `ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE` will be returned, which will be identified in the `OnEvent` function.
The passed parameter includes `result` and `file_path`.

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

```java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE == type)
        	{
            		// Callback for recording start
					 if (nErrCode ==0)
                        {
                            recordfilePath = templeData.getStringExtra("file_path");
                            mEditTextfiletoupload.setText(recordfilePath);
                        }
        	}
}
```


### Pausing recording

This API is used to pause recording. If you want to resume recording, please call the `ResumeRecording` API.

#### Function prototype  

```java
public abstract int PauseRecording();
```

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().PauseRecording();
```

### Resuming recording

This API is used to resume recording.

#### Function prototype  

```java
public abstract  int ResumeRecording();
```

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().ResumeRecording();
```


### Canceling recording

This API is used to cancel recording. There is no callback after cancellation.

#### Function prototype  

```java
public abstract int CancelRecording();
```

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().CancelRecording();
```

### Getting the real-time mic volume of voice message

This API is used to get the real-time mic volume. An int-type value will be returned. Value range: 0-200.

**This API is different from the voice chat API and is in `ITMGPTT.java`**.

#### Function prototype  

```java
public abstract int GetMicLevel();
```

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().GetMicLevel();
```

### Setting the recording volume of voice message

This API is used to set the recording volume of voice message. Value range: 0-200.

**This API is different from the voice chat API and is in `ITMGPTT.java`**.

#### Function prototype  

```java
public abstract int SetMicVolume(int volume);
```

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().SetMicVolume(100);
```

### Getting the recording volume of voice message

This API is used to get the recording volume of voice message. An int-type value will be returned. Value range: 0-200.

**This API is different from the voice chat API and is in `ITMGPTT.java`**.

#### Function prototype  

```java
public abstract int GetMicVolume();
```

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().GetMicVolume();
```

### Getting the real-time speaker volume of voice message

This API is used to get the real-time speaker volume. An int-type value will be returned. Value range: 0-200.

**This API is different from the voice chat API and is in `ITMGPTT.java`**.

#### Function prototype  

```java
public abstract int GetSpeakerLevel();
```

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().GetSpeakerLevel();
```

### Setting the playback volume of voice message

This API is used to set the playback volume of voice message. Value range: 0-200.

**This API is different from the voice chat API and is in `ITMGPTT.java`**.

#### Function prototype  

```java
public abstract int SetSpeakerVolume(int volume);
```

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().SetSpeakerVolume(100);
```

### Getting the playback volume of voice message

This API is used to get the playback volume of voice message. An int-type value will be returned. Value range: 0-200.

**This API is different from the voice chat API and is in `ITMGPTT.java`**.

#### Function prototype  

```java
public abstract int GetSpeakerVolume();
```

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().GetSpeakerVolume();
```

## Voice Message Playback

### Playing back audio

This API is used to play back audio.

#### Function prototype  

```java
public abstract int PlayRecordedFile(String filePath);public abstract int PlayRecordedFile(String filePath,int voicetype);
```

| Parameter | Type | Description |
| ---------------- | :----: | ------------------------------------------------------------ |
| downloadFilePath | String | Local audio file path |
| voicetype | int | Voice changer type. For more information, please see [Real-time Sound Effect](https://intl.cloud.tencent.com/document/product/607/31503). |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ---------- | ------------------------------ |
| 20485 | Playback is not started. | Ensure the existence of the file and the validity of the file path. |

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().PlayRecordedFile(downloadFilePath);
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

```java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE== type)
       	 	{
			//Callback for audio playback 
		}
}
```



### Stopping audio playback

This API is used to stop audio playback. There will be a callback for playback completion when the playback stops.

#### Function prototype  

```java
public abstract int StopPlayFile();
```

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().StopPlayFile();
```



### Getting audio file size

This API is used to get the size of an audio file.

#### Function prototype  

```java
public abstract int GetFileSize(String filePath);
```

| Parameter | Type | Description |
| -------- | :----: | -------------------------------- |
| filePath | string | Path of audio file, which is a local path. |

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().GetFileSize(path);
```

### Getting audio file duration

This API is used to get the duration of an audio file in milliseconds.

#### Function prototype  

```java
public abstract int GetVoiceFileDuration(String filePath);
```

| Parameter | Type | Description |
| -------- | :----: | -------------------------------- |
| filePath | string | Path of audio file, which is a local path. |

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().GetVoiceFileDuration(path);
```


## Voice Message Upload and Download

### Uploading an audio file

This API is used to upload an audio file.

#### Function prototype  

```java
public abstract int UploadRecordedFile(String filePath);
```

| Parameter | Type | Description |
| -------- | :----: | -------------------------------- |
| filePath | String | Path of uploaded audio file, which is a local path. |

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().UploadRecordedFile(filePath);
```

### Callback for audio file upload completion

After the audio file is uploaded, the event message `ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE` will be returned, which will be identified in the `OnEvent` function.
The passed parameters include `result`, `file_path`, and `file_id`.

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

```java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE== type)
       	 {
           	//Callback for audio file upload completion
       	 }
}
```

### Downloading the audio file

This API is used to download an audio file.

#### Function prototype  

```java
public abstract int DownloadRecordedFile(String fileID, String filePath);
```

| Parameter | Type | Description |
| ---------------- | :----: | ------------------ |
| fileID | String | File URL path |
| downloadFilePath | string | Local path of saved file |

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().DownloadRecordedFile(url,path);
```

### Callback for audio file download completion

After the audio file is downloaded, the event message `ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE` will be returned, which will be identified in the `OnEvent` function. The passed parameters include `result`、`file_path` and `file_id`.

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

```java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE== type)
        {
            //Download succeeded        
	}
}
```


## Speech-to-Text Service


### Converting audio file to text

This API is used to convert a specified audio file to text.

#### Function prototype  

```java
public abstract int SpeechToText(String fileID);
```

| Parameter | Type | Description |
| ------ | :----: | ------------ |
| fileID | String | Audio file URL |

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().SpeechToText(fileID);
```



### Translating audio file into text in specified language

This API can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation.

#### Function prototype  

```java
public abstract int SpeechToText(String fileID, String speechLanguage,String translatelanguage);
```

| Parameter | Type | Description |
| ----------------- | :----: | ------------------------------------------------------------ |
| fileID | String | URL of audio file, which will be retained on the server for 90 days |
| speechLanguage | String | The language in which the audio file is to be converted to text. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260). |
| translatelanguage | String | The language into which the audio file will be translated. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260). This parameter is currently unavailable. Enter the same value as that of speechLanguage. |

#### Sample code  

```java
ITMGContext.GetInstance(this).GetPTT().SpeechToText(fileID,"cmn-Hans-CN","cmn-Hans-CN");
```



### Callback for recognition

After the specified audio file is converted to text, the event message ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE will be returned, which will be identified in the `OnEvent` function.
The passed parameters include `result`, `file_path` and `text` (recognized text).

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

```java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if(ITMGContext.ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE == type)
       	 {
            //Recognized audio file successfully       
	 }
}
```



## Advanced APIs

### Getting version number

This API is used to get the SDK version number for analysis.

#### Function prototype

```java
public abstract String GetSDKVersion();
```

#### Sample code  

```java
ITMGContext.GetInstance(this).GetSDKVersion();
```

### Checking mic permission

This API is used to return the mic permission status.

#### Function prototype

```java
public abstract ITMG_RECORD_PERMISSION  CheckMicPermission();
```

#### Parameter description

| Parameter | Value | Description |
| ----------------------------- | ---- | ---------------------------- |
| ITMG_PERMISSION_GRANTED | 0 | Mic permission is granted |
| ITMG_PERMISSION_Denied | 1 | Mic is disabled |
| ITMG_PERMISSION_NotDetermined | 2 | No authorization box has been popped up to request the permission |
| ITMG_PERMISSION_ERROR | 3 | An error occurred while calling the API |

#### Sample code  

```java
ITMGContext.GetInstance(this).CheckMicPermission();
```



### Setting log printing level

This API is used to set the level of logs to be printed. It is recommended to keep the default level.

#### Function prototype

```java
public abstract int SetLogLevel(int levelWrite, int levelPrint);
```

#### Parameter description

| Parameter | Type | Description |
| ---------- | -------------- | ------------------------------------------------------------ |
| levelWrite | ITMG_LOG_LEVEL | Sets the level of logs to be written. `TMG_LOG_LEVEL_NONE` indicates not to write. Default value: TMG_LOG_LEVEL_INFO |
| levelPrint | ITMG_LOG_LEVEL | Sets the level of logs to be printed. `TMG_LOG_LEVEL_NONE` indicates not to print. Default value: TMG_LOG_LEVEL_ERROR |



| ITMG_LOG_LEVEL | Description |
| --------------------- | -------------------- |
| TMG_LOG_LEVEL_NONE | Does not print logs |
| TMG_LOG_LEVEL_ERROR | Prints error logs (default) |
| TMG_LOG_LEVEL_INFO | Prints info logs |
| TMG_LOG_LEVEL_DEBUG | Prints debug logs |
| TMG_LOG_LEVEL_VERBOSE | Prints verbose logs |

#### Sample code  

```java
ITMGContext.GetInstance(this).SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```



### Setting the log printing path

This API is used to set the log printing path, which is /sdcard/Android/data/xxx.xxx.xxx/files by default.

#### Function prototype

```java
public abstract int SetLogPath(String logDir);
```

| Parameter | Type | Description |
| ------ | :----: | ---- |
| logDir | String | Path |

#### Sample code  

```java
ITMGContext.GetInstance(this).SetLogPath(path);
```

## Callback Messages

### Message list

| Message | Description |
| ------------- |:-------------:|
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE | Indicates that PTT recording is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE | Indicates that PTT upload is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE | Indicates that PTT download is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE | Indicates that PTT playback is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE | Indicates that speech-to-text conversion is completed. |

### Data list

| Message | Data | Sample |
| ------------------------------------------------------ | :-----------------------------: | ------------------------------------------------- |
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE | result; file_path | {"file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE | result; file_path;file_id | {"file_id":"","file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE | result; file_path;file_id | {"file_id":"","file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE | result; file_path | {"file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE | result; text;file_id | {"file_id":"","text":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE | result; file_path; text;file_id | {"file_id":"","file_path":","text":"","result":0} |
