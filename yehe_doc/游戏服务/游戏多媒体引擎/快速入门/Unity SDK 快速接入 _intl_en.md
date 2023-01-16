This document provides a detailed description that makes it easy for Unity project developers to debug and integrate the APIs for Game Multimedia Engine (GME).

This document only provides the main APIs to help you get started with GME to debug and integrate the APIs.

## Key Considerations for Using GME

GME provides two services: Voice chat service and voice messaging and speech-to-text service, both of which rely on key APIs such as Init and Poll.

<dx-alert infotype="notice" title="Note on Init API">
If you need to use voice chat and voice messaging services at the same time, **you only need to call `Init` API once**.
</dx-alert>

### API call flowchart

![image](https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg)

### Directions

#### Integrating SDK

To integrate the SDK into the project, see [Integrating SDK](https://intl.cloud.tencent.com/document/product/607/10783).

#### Core APIs

- <dx-tag-link link="#Init" tag="API: Init">Initializing GME</dx-tag-link>
- <dx-tag-link link="#Poll" tag="API: Poll">Calling Poll periodically to trigger event callbacks</dx-tag-link>
- <dx-tag-link link="#Complete" tag="Listener: QAVEnterRoomComplete">Listening on room entry/exit notification</dx-tag-link>

#### Voice Chat

<dx-steps>
-<dx-tag-link link="#EnterRoom" tag="API: EnterRoom">Entering a voice chat room</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="API: EnableMic">Turning on or off the microphone</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="API: EnableSpeaker">Turning on or off the speaker</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="API: ExitRoom">Exiting a voice room</dx-tag-link>
</dx-steps>

#### Voice Message

<dx-steps>
-<dx-tag-link link="#ApplyPtt" tag="API: ApplyPTTAuthbuffer">Initializing authentication</dx-tag-link>
-<dx-tag-link link="#StartRWSR" tag="API: StartRecordingWithStreamingRecognition">Starting streaming speech recognition</dx-tag-link>
-<dx-tag-link link="#Stop" tag="API: StopRecording">Stop recording</dx-tag-link>
</dx-steps>

- <dx-tag-link link="#Init" tag="API: UnInit">Uninitializing GME</dx-tag-link>

## Key API Access

### 1. Download the SDK 

On the SDK download guide page, download the appropriate <dx-tag-link link="https://intl.cloud.tencent.com/document/product/607/18521" tag="DownLoad">client SDK</dx-tag-link>.

### 2. Importing the header file

```
using GME;
```

### 3. Getting the Context instance

Get the `Context` instance by using the `ITMGContext` method instead of `QAVContext.GetInstance()`.

#### Sample code  

```
int ret = ITMGContext.GetInstance().Init(sdkAppId, openID);
```

### [4. Initializing SDK](id:Init)

**You need to initialize the SDK through the `Init` API** before you can use the real-time voice, voice message, and speech-to-text services. The `Init` API must be called in the same thread as other APIs. We recommend you call all APIs in the main thread.

#### API prototype

```
//class ITMGContext
public abstract int Init(string sdkAppID, string openID);
```

| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | string | `AppID` provided in the [GME console](https://console.cloud.tencent.com/gamegme), which can be obtained as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782). |
| openID   | string | `openID` can only be in `Int64` type, which is passed in after being converted to a string. You can customize its rules, and it must be unique in the application. To pass in `openID` as a string, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1) for application. |

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

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. The `Poll` API is GME's message pump and should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run abnormally. For more information, see the `EnginePollHelper` file in [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).

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

### 7. Calculating the local authentication key

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    

#### API prototype

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

###  [1. Entering a room](id:EnterRoom)

This API is used to enter a room with the generated authentication information. The mic and speaker are not enabled by default after room entry. The returned value of `AV_OK` indicates successful API call but not successful room entry.

#### API prototype

```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```

| Parameter | Type | Description |
| ---------- | :----: | ----------------------- |
| roomId | String | Room ID, which can contain up to 127 characters |
| roomType   | ITMGRoomType | Just enter `ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY` |
| authBuffer | byte[] | Authentication code |

#### Sample code  

```
ITMGContext.GetInstance().EnterRoom(strRoomId, ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);
```

### Callback for room entry

After the user enters the room, the room entry result will be called back, which can be listened on for processing. A successful callback means that the room entry is successful, and the billing **starts**.

<dx-fold-block title="Billing references">
[Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009)
[Billing FAQs](https://intl.cloud.tencent.com/document/product/607/30255)
[Will Voice Chat still be charged when client is offlined?](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)
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





### [2. Turning on or off the microphone](id:EnableMic)

This API is used to turn on of off the mic. Mic and speaker are not turned on by default after room entry.

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
	// Turn on mic
    ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
  }
}
```

### [3. Turning on or off the speaker](id:EnableSpeaker)

This API is used to turn on/off the speaker.

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
    // Turn on the speaker
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

#### API prototype  

```
ITMGPTT int ApplyPTTAuthbuffer (byte[] authBuffer)
```

| Parameter       |  Type  | Description                    |
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

This API is used to start streaming speech recognition. Text obtained from speech-to-text conversion will be returned in real time in its callback. **To stop recording, call `StopRecording`**. The callback will be returned after the recording is stopped.

#### API prototype  

```
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath)
```

| Parameter | Type | Description |
| ----------------- | :----: | ------------------------------------------------------------ |
| filePath | String | Path of stored audio file |


#### Sample code  

```
string recordPath = Application.persistentDataPath + string.Format("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecordingWithStreamingRecognition(recordPath);
```

#### Callback for streaming speech recognition

After streaming speech recognition is started, you need to listen on callback messages in the `OnStreamingSpeechComplete` or `OnStreamingSpeechisRunning` notification, which is as detailed below:

- `OnStreamingSpeechComplete` returns text after the recording is stopped and the recognition is completed, which is equivalent to returning the recognized text after a paragraph of speech.
- `OnStreamingSpeechisRunning` returns the recognized text in real time during the recording, which is equivalent to returning the recognized text while speaking.

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

#### API prototype  

```
ITMGPTT int StopRecording()
```

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().StopRecording();
```
