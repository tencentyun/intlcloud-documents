This document provides a detailed description that makes it easy for Unreal Engine project developers to debug and integrate the APIs for Game Multimedia Engine (GME).

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

Refer to [Integrating SDK](https://intl.cloud.tencent.com/zh/document/product/607/17025) to integrate the SDK into the project.

#### Key APIs

<dx-tag-link link="#Init" tag="API: Init">Initializing GME</dx-tag-link>
<dx-tag-link link="#Poll" tag="API: Poll">Calling Poll periodically to trigger event callbacks</dx-tag-link>
<dx-tag-link link="#Complete" tag="Listener: QAVEnterRoomComplete">Listening on room entry/exit notification</dx-tag-link>

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
#include "tmg_sdk.h"

class UEDEMO1_API AUEDemoLevelScriptActor : public ALevelScriptActor, public ITMGDelegate
{
public:
...
private:
...
｝
```

### 3. Setting the singleton

You need to get `ITMGContext` first before you can call the `EnterRoom` function, because all calls begin with `ITMGContext` and callbacks are passed to the application through `ITMGDelegate`.

#### Sample code 

```
ITMGContext* context = ITMGContextGetInstance();
context->SetTMGDelegate(this);
```



### [4. Initializing SDK](id:Init)

- This API is used to initialize the GME service. It is recommended to call it when initializing the application.
- **The openID uniquely identifies a user with the rules stipulated by the application developer and unique in the application (currently, only INT64 is supported)**.
-**If the user switches the login account, they need to call Uninit and then call Init again with the new OpenId.**

#### Function prototype

```
//class ITMGContext
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
```

| Parameter | Type | Description |
| -------- | :---------: | ------------------------------------------------------------ |
| sdkAppId | const char* | `AppId` provided by the GME service from the [Tencent Cloud console](https://console.cloud.tencent.com/gamegme) |
| OpenId   | const char* | `OpenId` can only be in Int64 type, which is passed after being converted to a string. |

#### Sample code 

```
std::string appid = TCHAR_TO_UTF8(CurrentWidget->editAppID->GetText().ToString().operator*());
std::string userId = TCHAR_TO_UTF8(CurrentWidget->editUserID->GetText().ToString().operator*());
ITMGContextGetInstance()->Init(appid.c_str(), userId.c_str());
```

### [5. Triggering event callback](id:Poll)

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. The `Poll` API should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run exceptionally.
Refer to the UEDemoLevelScriptActor.cpp file in the demo.

#### Sample code

```
// Declaration in the header file
virtual void Tick(float DeltaSeconds);

void AUEDemoLevelScriptActor::Tick(float DeltaSeconds) {
  Super::Tick(DeltaSeconds);  
  ITMGContextGetInstance()->Poll();
}
```

### [6. Setting the callback](id:Complete)

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

### 7. Authentication

Generate `AuthBuffer` for encryption and authentication of relevant features.    
To get authentication for voice message and speech-to-text, the room ID parameter must be set to `null`.

#### Function prototype

```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
  const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```

| Parameter | Type | Description |
| ------------- | :---: | ------------------------------------------------------------ |
| dwSdkAppID | int | `AppId` from the Tencent Cloud console.|
| strRoomID     | char* | Room ID, which can contain up to 127 characters. |
| strOpenID     | char* | User ID, which is the same as `openID` during initialization. |
| strKey        | char* | Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme). |
| strAuthBuffer | char* | Returned `authbuff`                                              |
| bufferLength  |  int  | Length of the `authbuff` passed in. 500 is recommended.                             |



#### Sample code  

```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```

## Voice Chat Access

### [1. Entering a room](id:EnterRoom)

This API is used to enter a room with the generated authentication information. The mic and speaker are not enabled by default after room entry. The returned value of 0 indicates successful API call but not successful room entry.

For more information on how to choose a room audio type, please see [Sound Quality Selection](https://intl.cloud.tencent.com/zh/document/product/607/18522).

#### Function prototype

```
ITMGContext virtual int EnterRoom(const char*  roomID, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)

```

| Parameter | Type | Description |
| ---------- | :------------: | ----------------------- |
| roomId | char* | Room ID, which can contain up to 127 characters |
| roomType   | ITMG_ROOM_TYPE | Room audio type            |
| authBuffer |     char*      | Authentication key                  |
| buffLen    |      int       | Authentication key length              |

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomID, ITMG_ROOM_TYPE_FLUENCY, (char*)retAuthBuff,bufferLen);
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
void UBaseViewController::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char *data) {

  FString jsonData = FString(UTF8_TO_TCHAR(data));
  TSharedPtr<FJsonObject> JsonObject;
  TSharedRef<TJsonReader<>> Reader = TJsonReaderFactory<>::Create(FString(UTF8_TO_TCHAR(data)));
  FJsonSerializer::Deserialize(Reader, JsonObject);


  if (eventType == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM) {
    int32 result = JsonObject->GetIntegerField(TEXT("result"));
    FString error_info = JsonObject->GetStringField(TEXT("error_info"));
    if (result == 0) {
      GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, TEXT("Enter room success."));
    }
    else {
      FString msg = FString::Printf(TEXT("Enter room failed. result=%d, info = %ls"), result, *error_info);
      GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, *msg);
    }
    onEnterRoomCompleted(result, error_info);
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
void UBaseViewController::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char *data) {

  FString jsonData = FString(UTF8_TO_TCHAR(data));
  TSharedPtr<FJsonObject> JsonObject;
  TSharedRef<TJsonReader<>> Reader = TJsonReaderFactory<>::Create(FString(UTF8_TO_TCHAR(data)));
  FJsonSerializer::Deserialize(Reader, JsonObject);


  if (eventType == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM) {
    int32 result = JsonObject->GetIntegerField(TEXT("result"));
    FString error_info = JsonObject->GetStringField(TEXT("error_info"));
    if (result == 0) {
      GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, TEXT("Enter room success."));
      // Enable mic
      ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
    }
    else {
      FString msg = FString::Printf(TEXT("Enter room failed. result=%d, info = %ls"), result, *error_info);
      GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, *msg);
    }
    onEnterRoomCompleted(result, error_info);
  }
}
```

### [3. Enabling or disabling the speaker](id:EnableSpeaker)

This API is used to enable/disable the speaker.

#### Sample code  

```
void UBaseViewController::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char *data) {

  FString jsonData = FString(UTF8_TO_TCHAR(data));
  TSharedPtr<FJsonObject> JsonObject;
  TSharedRef<TJsonReader<>> Reader = TJsonReaderFactory<>::Create(FString(UTF8_TO_TCHAR(data)));
  FJsonSerializer::Deserialize(Reader, JsonObject);


  if (eventType == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM) {
    int32 result = JsonObject->GetIntegerField(TEXT("result"));
    FString error_info = JsonObject->GetStringField(TEXT("error_info"));
    if (result == 0) {
      GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, TEXT("Enter room success."));
      // Enable the speaker
      ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
    }
    else {
      FString msg = FString::Printf(TEXT("Enter room failed. result=%d, info = %ls"), result, *error_info);
      GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, *msg);
    }
    onEnterRoomCompleted(result, error_info);
  }
}

```

### [4. Exiting the room](id:ExitRoom)

This API is called to exit the current room. It needs to wait for and process the callback for exit.

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->ExitRoom();

```

#### Callback for room exit

After the user exits a room, a callback will be returned. The sample code is as shown below:

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
  switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
    {
    // Process
    break;
    }
  }
}

```



## Voice Message Access

### [1. Initializing authentication](id:ApplyPtt)

Call authentication initialization after initializing the SDK. For more information on how to get the `authBuffer`, please see `genAuthBuffer` (the voice chat authentication information API).

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

### [2. Starting streaming speech recognition](id:StartRWSR)

This API is used to start streaming speech recognition. Text obtained from speech-to-text conversion will be returned in real time in its callback. It can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation. **To stop recording, call `StopRecording`**. The callback will be returned after the recording is stopped.

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
void UBaseViewController::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char *data) {

  FString jsonData = FString(UTF8_TO_TCHAR(data));
  TSharedPtr<FJsonObject> JsonObject;
  TSharedRef<TJsonReader<>> Reader = TJsonReaderFactory<>::Create(FString(UTF8_TO_TCHAR(data)));
  FJsonSerializer::Deserialize(Reader, JsonObject);
  ...
  else if(eventType == ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE)
    {
        int32 nResult = JsonObject->GetIntegerField(TEXT("result"));
        FString text = JsonObject->GetStringField(TEXT("text"));
        FString fileid = JsonObject->GetStringField(TEXT("file_id"));
        FString file_path = JsonObject->GetStringField(TEXT("file_path"));
        onPttStreamRecognitionCompleted(nResult,file_path, fileid, text);
    }
    else if(eventType == ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING)
    {
        int32 nResult = JsonObject->GetIntegerField(TEXT("result"));
        FString text = JsonObject->GetStringField(TEXT("text"));
        FString fileid = TEXT("STREAMINGRECOGNITION_IS_RUNNING");
        FString file_path = JsonObject->GetStringField(TEXT("file_path"));
        onPttStreamRecognitionisRunning(nResult,file_path, fileid, text);
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
ITMGPTT virtual int StopRecording()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->StopRecording();
```
