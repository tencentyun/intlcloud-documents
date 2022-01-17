This document provides a detailed description that makes it easy for Unity project developers to debug and integrate the APIs for Game Multimedia Engine (GME).

This document only provides the main APIs to help you get started with GME to debug and integrate the APIs.

## Key Considerations for Using GME

GME provides two services: voice chat service and voice message and speech-to-text service, both of which rely on key APIs such as Init and Poll.

<dx-alert infotype="notice" title="Note on Init API">
If you need to use voice chat and voice message services at the same time, **you only need to call `Init` API once**.
</dx-alert>

### API call flowchart

![image](https://main.qcloudimg.com/raw/99d612d90268a7248f5b55c385eeb8b8.png)

### Directions

#### Integrating SDK

Refer to [Integrating SDK](https://intl.cloud.tencent.com/zh/document/product/607/10783) to integrate the SDK into the project.

#### Key APIs

- <dx-tag-link link="#Init" tag="API: Init">Initializing GME</dx-tag-link>
- <dx-tag-link link="#Poll" tag="API: Poll">Calling Poll periodically to trigger event callbacks</dx-tag-link>
- <dx-tag-link link="#Complete" tag="Listener: QAVEnterRoomComplete">Listening on room entry/exit notification</dx-tag-link>

#### Voice Chat

<dx-steps>
-<dx-tag-link link="#EnterRoom" tag="API: EnterRoom">Entering a voice chat room</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="API: EnableMic">Enabling or disabling the microphone</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="API: EnableSpeaker">Enabling or disabling the speaker</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="API: ExitRoom">Exiting a voice room</dx-tag-link>
</dx-steps>

#### Voice Message

<dx-steps>
-<dx-tag-link link="#ApplyPtt" tag="API: ApplyPTTAuthbuffer">Initializing authentication</dx-tag-link>
-<dx-tag-link link="#StartRWSR" tag="API: StartRecordingWithStreamingRecognition">Starting streaming speech recognition</dx-tag-link>
-<dx-tag-link link="#Stop" tag="API: StopRecording">Stop recording</dx-tag-link>
</dx-steps>

<dx-tag-link link="#Init" tag="API: UnInit">Uninitializing GME</dx-tag-link>

## Key API Access

### 1. Downloading the SDK 

On the SDK download guide page, download the appropriate <dx-tag-link link="https://cloud.tencent.com/document/product/607/18521" tag="DownLoad">client SDK</dx-tag-link>.

### 2. Importing the header file

```
using TencentMobileGaming;
```

### 3. Getting the Context instance

Get the `Context` instance by using the `ITMGContext` method instead of `QAVContext.GetInstance()`.

#### Sample code  

```
int ret = ITMGContext.GetInstance().Init(sdkAppId, openID);
```

### [4. Initializing SDK](id:Init)

- This API is used to initialize the GME service. It is recommended to call it when initializing the application.
- **The openID uniquely identifies a user with the rules stipulated by the application developer and unique in the application (currently, only INT64 is supported)**.
-**If the user switches the login account, they need to call Uninit and then call Init again with the new OpenId.**

#### Function prototype

```
//class ITMGContext
public abstract int Init(string sdkAppID, string openID);
```

| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | String | `AppId` provided by the GME service from the [Tencent Cloud console](https://console.cloud.tencent.com/gamegme) |
| OpenId |String | `OpenId` can only be in Int64 type, which is passed after being converted to a string. |

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

### [5. Triggering event callback](id:Poll)

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. The `Poll` API should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run exceptionally.
Refer to the EnginePollHelper file in the demo.

#### Sample code

```
public void Update()
  {
      ITMGContext.GetInstance().Poll();
  }
```

### [6. Listening on room entry/exit notification](id:Complete)

#### Room entry notification

```
// Delegate function:
public delegate void QAVEnterRoomComplete(int result, string error_info);
// Event-triggered function:
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;
```

#### Room exit notification

```
Delegate function:
public delegate void QAVExitRoomComplete();
Event-triggered function:
public abstract event QAVExitRoomComplete OnExitRoomCompleteEvent;
```

### 7. Authentication

Generate `AuthBuffer` for encryption and authentication of relevant features.    
To get authentication for voice message and speech-to-text, the room ID parameter must be set to `null`.

#### Function prototype

```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```

| Parameter | Type | Description |
| ------ | :----: | ------------------------------------------------------------ |
| appId | int | `AppId` from the Tencent Cloud console.|
| roomId | string | Room ID, which can contain up to 127 characters (For voice message, enter "null".) |
| openId | string | User ID, which is the same as `openId` during initialization. |
| key | string | Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme). |

#### Sample code  

```
public static byte[] GetAuthBuffer(string AppID, string RoomID,string OpenId, string AuthKey){
    return QAVAuthBuffer.GenAuthBuffer(int.Parse(AppID), RoomID, OpenId, AuthKey);
}

```

## Voice Chat Access

### [1. Entering a room](id:EnterRoom)

This API is used to enter a room with the generated authentication information. The mic and speaker are not enabled by default after room entry. The returned value of 0 indicates successful API call but not successful room entry.

For more information on how to choose a room audio type, please see [Sound Quality Selection](https://intl.cloud.tencent.com/zh/document/product/607/18522).

#### Function prototype

```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```

| Parameter | Type | Description |
| ---------- | :----: | ----------------------- |
| roomId | String | Room ID, which can contain up to 127 characters |
| roomType | int | Room audio type |
| authBuffer | byte[] | Authentication code |

#### Sample code  

```
ITMGContext.GetInstance().EnterRoom(strRoomId, ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);
```

#### Callback for room entry

After the user enters the room, a room entry notification will be received and identified in the listener function for processing. A successful callback (err = 0) means that the room entry is successful, and the **billing** starts. If the total call duration on the day is below 700 minutes, no fees will be incurred.

<dx-fold-block title="Billing references">
[Purchase Guide](https://intl.cloud.tencent.com/zh/document/product/607/36276)
[Billing FAQs](https://intl.cloud.tencent.com/zh/document/product/607/30255)
[Will the billing continue if the client is disconnected when using the voice chat?](https://intl.cloud.tencent.com/zh/document/product/607/30255)
</dx-fold-block>

- **Sample code**  
  Sample code for processing the callback:
```
// Listen on an event:
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);
// Process the event listened on:
void OnEnterRoomComplete(int err, string errInfo)
{
  if (err != 0) {
    ShowLoginPanel("error code:" + err + " error message:" + errInfo);
    return;
  }
  else{
	// Entered room successfully
  }
}
```

- **Error code**
<table>
<thead>
<tr>
<th>Error Code Value</th>
<th>Cause and Suggested Solution</th>
</tr>
</thead>
<tbody><tr>
<td>7006</td>
<td>Authentication failed. Possible causes:<ul><li>The `AppID` does not exist or is incorrect.</li><li>An error occurred while authenticating the `authbuff`.</li><li>Authentication expired.</li><li>The `openId` does not meet the specification.</li></ul></td>
</tr>
<tr>
<td>7007</td>
<td>Already in another room.</td>
</tr>
<tr>
<td>1001</td>
<td>The user was already in the process of entering a room but repeated this operation. It is recommended not to call the room entering API until the room entry callback is returned.</td>
</tr>
<tr>
<td>1003</td>
<td>The user was already in the room and called the room entering API again.</td>
</tr>
<tr>
<td>1101</td>
<td>Make sure that the SDK is initialized, `openId` complies with the rules, the APIs are called in the same thread, and the `Poll` API is called normally.</td>
</tr>
</tbody></table>





### [2. Enabling or disabling the microphone](id:EnableMic)

This API is used to enable/disable the mic. Mic and speaker are not enabled by default after room entry.

#### Sample code  

```
// Listen on an event:
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);
// Process the event listened on:
void OnEnterRoomComplete(int err, string errInfo)
{
  if (err != 0) {
    ShowLoginPanel("error code:" + err + " error message:" + errInfo);
    return;
  }
  else{
	// Entered room successfully
	// Enable mic
    ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
  }
}
```

### [3. Enabling or disabling the speaker](id:EnableSpeaker)

This API is used to enable/disable the speaker.

#### Sample code  

```
// Listen on an event:
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);
// Process the event listened on:
void OnEnterRoomComplete(int err, string errInfo)
{
  if (err != 0) {
    ShowLoginPanel("error code:" + err + " error message:" + errInfo);
    return;
  }
  else{
	// Entered room successfully
    // Enable the speaker
    ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
  }
}
```

### [4. Exiting the room](id:ExitRoom)

This API is called to exit the current room. It needs to wait for and process the callback for exit.

#### Sample code  

```
ITMGContext.GetInstance().ExitRoom();
```

#### Callback for room exit

After the user exits a room, a callback will be returned. The sample code is as shown below:

```
Listen on an event:
ITMGContext.GetInstance().OnExitRoomCompleteEvent += new QAVExitRoomComplete(OnExitRoomComplete);
Process the event listened on:
void OnExitRoomComplete(){
// Send a callback after room exit
}
```



## Voice Message Access

### [1. Initializing authentication](id:ApplyPtt)

Call authentication initialization after initializing the SDK. For more information on how to get the `authBuffer`, please see `genAuthBuffer` (the voice chat authentication information API).

#### Function prototype  

```
ITMGPTT int ApplyPTTAuthbuffer (byte[] authBuffer)
```

| Parameter | Type | Description |
| ---------- | :----: | ---- |
| authBuffer | String | Authentication |

#### Sample code  

```
UserConfig.SetAppID(transform.Find ("appId").GetComponent<InputField> ().text);
UserConfig.SetUserID(transform.Find ("userId").GetComponent<InputField> ().text);
UserConfig.SetAuthKey(transform.Find("authKey").GetComponent<InputField>().text);
byte[] authBuffer = UserConfig.GetAuthBuffer(UserConfig.GetAppID(), UserConfig.GetUserID(), null,UserConfig.GetAuthKey());
ITMGContext.GetInstance ().GetPttCtrl ().ApplyPTTAuthbuffer(authBuffer);
```

### [2. Starting streaming speech recognition](id:StartRWSR)

This API is used to start streaming speech recognition. Text obtained from speech-to-text conversion will be returned in real time in its callback. It can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation. **To stop recording, call `StopRecording`**. The callback will be returned after the recording is stopped.

#### Function prototype  

```
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath)
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath, string speechLanguage,string translateLanguage)
```

| Parameter | Type | Description |
| ----------------- | :----: | ------------------------------------------------------------ |
| filePath | String | Path of stored audio file |
| speechLanguage | String | The language in which the audio file is to be converted to text. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/zh/document/product/607/30260) |
| translateLanguage | String | The language into which the audio file will be translated. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/zh/document/product/607/30260) (This parameter is currently unavailable. Enter the same value as that of `speechLanguage`) |

#### Sample code  

```
string recordPath = Application.persistentDataPath + string.Format("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecordingWithStreamingRecognition(recordPath, "cmn-Hans-CN","cmn-Hans-CN");
```

#### Callback for streaming speech recognition

After streaming speech recognition is started, you need to listen for callback messages in the callback function `onEvent`. The event message is `ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE`, namely returns text after the recording is stopped and the recognition is completed, which is equivalent to returning the recognized text after a paragraph of speech.

The event message will be identified in the `OnEvent function` based on the actual needs. The passed parameters include the following four messages.

| Message Name | Description |
| --------- | :-----------------------------------------: |
| result | A return code for judging whether the streaming speech recognition is successful. |
| text | Text converted from speech |
| file_path | Local path of stored recording file |
| file_id | Backend URL address of recording file, which will be retained for 90 days |

- **Sample code**  
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

- **Error code**
<table>
<thead>
<tr>
<th>Error Code</th>
<th align="center">Description</th>
<th align="center">Suggested Solution</th>
</tr>
</thead>
<tbody><tr>
<td>32775</td>
<td align="center">Streaming speech-to-text conversion failed, but recording succeeded.</td>
<td align="center">Call the `UploadRecordedFile` API to upload the recording file and then call the `SpeechToText` API to perform speech-to-text conversion.</td>
</tr>
<tr>
<td>32777</td>
<td align="center">Streaming speech-to-text converting failed, but recording and upload succeeded</td>
<td align="center">The message returned contains a backend URL after successful upload. Call the `SpeechToText` API to perform speech-to-text conversion.</td>
</tr>
<tr>
<td>32786</td>
<td align="center">Streaming speech-to-text conversion failed.</td>
<td align="center">During streaming recording, wait for the execution result of the streaming recording API to return.</td>
</tr>
</tbody></table>



### [3. Stopping recording](id:Stop)

This API is used to stop recording. It is async, and a callback for recording completion will be returned after recording stops. A recording file will be available only after recording succeeds.

#### Function prototype  

```
ITMGPTT int StopRecording()
```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().StopRecording();
```
