为方便 Unity 开发者调试和接入腾讯云游戏多媒体引擎产品 API，这里向您介绍适用于 Unity 开发的接入技术文档。

>?此文档对应 GME sdk version：2.8。

## 使用 GME 重要事项

GME 分为两个部分，提供实时语音服务、语音消息及转文本服务。

![image](https://main.qcloudimg.com/raw/7a287c9cf60259eaea9469e110927462.png)

### 重要接口

| 重要接口      |   接口含义   |
| ------------- | :----------: |
| Init          |  初始化 GME  |
| Poll          | 触发事件回调 |
| EnterRoom     |     进房（实时语音）     |
| EnableMic     |   开麦克风（实时语音）   |
| EnableSpeaker |   开扬声器（实时语音）   |
| StartRecordingWithStreamingRecognition |    流式录制及转文字（语音消息及转文字）   |

### 重点提示
- GME 使用前请对工程进行配置，否则 SDK 不生效。
- GME 的接口调用成功后返回值为 QAVError.OK，数值为 0。
- GME 的接口调用要在同一个线程下。
- GME 需要周期性的调用 Poll 接口触发事件回调。
- 错误码详情可参考 [错误码](https://intl.cloud.tencent.com/document/product/607/33223)。

### C#类

| 类   |   含义   |
| ------ | :----------: |
| ITMGContext   |  核心接口  |
| ITMGRoom   | 房间相关接口 |
| ITMGRoomManager  |   房间管理接口   |
| ITMGAudioCtrl  |   音频相关接口   |
| ITMGAudioEffectCtrl  |   音效及伴奏相关接口   |
| ITMGPTT  |   语音消息及转文字相关接口   |

## 核心接口

未初始化前，SDK 处于未初始化阶段，需要通过接口 Init 初始化 SDK，才可以使用实时语音服务、语音消息及转文字服务。**如果切换账号，请调用 UnInit 反初始化 SDK。**

使用问题可参考 [一般性问题](https://intl.cloud.tencent.com/document/product/607/30254)。

| 接口   |   接口含义   |
| ------ | :----------: |
| Init   |  初始化 GME  |
| Poll   | 触发事件回调 |
| Pause  |   系统暂停   |
| Resume |   系统恢复   |
| Uninit | 反初始化 GME |

### 引用头文件

```
using TencentMobileGaming;
```

### 获取实例
请使用 ITMGContext 的方法获取 Context 实例，不要直接使用 QAVContext.GetInstance() 去获取实例。

### 初始化 SDK
此接口用于初始化 GME 服务，建议应用侧在应用初始化时候调用。
<b>参数 sdkAppId 获取请查看 [接入指引](https://intl.cloud.tencent.com/document/product/607/39698)</b>。
**openID 用于唯一标识一个用户，数值需大于 10000（目前只支持 INT64），规则由 App 开发者自行制定，App 内不重复即可**。

> !初始化 SDK 之后才可以进入实时语音房间。

#### 函数原型

```
ITMGContext Init(string sdkAppID, string openID)
```

| 参数     |  类型  | 含义                                                         |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | String | 来自 [腾讯云控制台](https://console.cloud.tencent.com/) 的 GME 服务提供的 AppId。                              |
| openID   | String | OpenID 只支持 Int64 类型（转为 string 传入），**数值必须大于10000，否则初始化不成功，导致进房失败**。 |

| 返回值                          | 处理                                          |
| ------------------------------- | --------------------------------------------- |
| QAVError.OK= 0                  | 初始化 SDK 成功                               |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | 检查 SDK 文件是否完整，建议删除后重新导入 SDK |

出现返回值 AV_ERR_SDK_NOT_FULL_UPDATE 时，此返回值只有提示作用，并不会造成初始化失败。

- 如果在接入过程中提示此错误，请根据提示检查 SDK 文件是否完整、SDK 文件版本是否一致。
- 如果是在导出可执行文件之后出现此返回值，请忽略此错误，并尽量不在 UI 中提示。

#### 示例代码 

```
int ret = ITMGContext.GetInstance().Init(sdkAppId, openID);
//通过返回值判断是否初始化成功
if (ret != QAVError.OK)
    {
        Debug.Log("SDK初始化失败:"+ret);
        return;
    }
```


### 触发事件回调

通过在 update 里面周期的调用 Poll 可以触发事件回调。GME 需要周期性的调用 Poll 接口触发事件回调。如果没有调用 Poll 的话，会导致整个 SDK 服务运行异常。
可参考 Demo 中的 EnginePollHelper 文件。

#### 函数原型

```
ITMGContext public abstract int Poll();
```

#### 示例代码

```
public void Update()
    {
        ITMGContext.GetInstance().Poll();
    }
```

### 系统暂停

当系统发生 Pause 事件时，需要同时通知引擎进行 Pause。

#### 函数原型

```
ITMGContext public abstract int Pause()
```

### 系统恢复

当系统发生 Resume 事件时，需要同时通知引擎进行 Resume。Resume 接口只恢复实时语音。

#### 函数原型

```
ITMGContext  public abstract int Resume()
```



### 反初始化 SDK

反初始化 SDK，进入未初始化状态。**切换账号需要反初始化**。

#### 函数原型

```
ITMGContext public abstract int Uninit()
```


## 实时语音
实时语音，即一对一或一对多的实时语音通话功能。

### 实时语音流程图

![](https://main.qcloudimg.com/raw/e536525aa47c06a5a84bb6c8d4851b22.png)



### 实时语音房间调用流程图

![](https://main.qcloudimg.com/raw/a61ca1d7cdecf09bd223766b2a5cd69f.png)

## 实时语音房间相关接口

初始化之后，SDK 调用进房后进去了房间，才可以进行实时语音通话。
使用问题可参考 [实时语音相关问题](https://intl.cloud.tencent.com/document/product/607/30257)。


| 接口           |       接口含义       |
| -------------- | :------------------: |
| GenAuthBuffer  |      初始化鉴权      |
| EnterRoom      |       加入房间       |
| IsRoomEntered  |   是否已经进入房间   |
| ExitRoom       |       退出房间       |
| ChangeRoomType | 修改用户房间音频类型 |
| GetRoomType    | 获取用户房间音频类型 |

### 鉴权信息

生成 AuthBuffer，用于相关功能的加密和鉴权，如正式发布请使用后台部署密钥，后台部署请参考 [鉴权密钥](https://intl.cloud.tencent.com/document/product/607/12218)。    
使用语音消息及转文字服务获取鉴权时，房间号参数必须填 null。

#### 函数原型

```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)

```

| 参数   |  类型  | 含义                                                         |
| ------ | :----: | ------------------------------------------------------------ |
| appId  |  int   | 来自腾讯云控制台的 AppId 号码。                              |
| roomId |string  |房间号，最大支持127字符（使用语音消息及转文字服务，房间号参数必须填 null）。|
| openId | string | 用户标识。与 Init 时候的 openID相同。                        |
| key    | string | 来自腾讯云 [控制台](https://console.cloud.tencent.com/gamegme) 的权限密钥。 |



#### 示例代码  

```
public static byte[] GetAuthBuffer(string AppID, string RoomID,string OpenId, string AuthKey){
        return QAVAuthBuffer.GenAuthBuffer(int.Parse(AppID), RoomID, OpenId, AuthKey);
}
```



### 加入房间

用生成的鉴权信息进房，会收到消息为 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM 的回调。加入房间默认不打开麦克风及扬声器。返回值为 AV_OK 的时候代表成功。

范围语音接入流程请查看 [范围语音](https://intl.cloud.tencent.com/document/product/607/17972)。
#### 函数原型

```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```

| 参数       |  类型  | 含义                    |
| ---------- | :----: | ----------------------- |
| roomId		|string    	|房间号，最大支持127字符。					|
| roomType 	|ITMGRoomType		|房间音频类型。		|
| authBuffer 	|Byte[] 	|鉴权码。					|

房间音频类型请参考 [音质选择](https://intl.cloud.tencent.com/document/product/607/18522)。

#### 示例代码  

```
ITMGContext.GetInstance().EnterRoom(strRoomId, ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);

```

### 加入房间事件的回调
加入房间后，需要通过委托函数进行回调。其中包含两个信息：result 及 error_info。
如果没有回调，请检查是否有周期性的调用 Poll 函数。
#### 函数原型
```
委托函数：
public delegate void QAVEnterRoomComplete(int result, string error_info);
事件函数：
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;
```



#### 示例代码  

```
对事件进行监听：
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);

监听处理：
void OnEnterRoomComplete(int err, string errInfo)
    {
	if (err != 0) {
  			ShowLoginPanel("错误码:" + err + " 错误信息:" + errInfo);
            return;
	}else{
		//进房成功
    }
}
```

#### 错误码

|错误码名称|错误码值|原因及建议方案|
|--------|-------|------------|
|AV_ERR_AUTH_FIALD         |7006|鉴权失败 有以下几个原因：1、AppID 不存在或者错误，2、authbuff 鉴权错误，3、鉴权过期 4、openID不符合规范。|
|AV_ERR_IN_OTHER_ROOM      |7007|已经在其它房间。|
|ERR_REPETITIVE_OPERATION  |1001   |已经在进房过程中，然后又重复了此操作。建议在进房回调返回之前不要再调用进房接口。|
|ERR_HAS_IN_THE_STATE    |1003   |已经进房了在房间中，又调用一次进房接口。|
|ERR_CONTEXT_NOT_START   |1101   |确保已经初始化 SDK，确保 OpenId 是否符合规则，或者确保在同一线程调用接口，以及确保 Poll 接口正常调用。|

### 判断是否已经进入房间

通过调用此接口可以判断是否已经进入房间，返回值为 bool 类型。

#### 函数原型  

```
ITMGContext abstract bool IsRoomEntered()
```

#### 示例代码  

```
ITMGContext.GetInstance().IsRoomEntered();
```

### 退出房间

通过调用此接口可以退出所在房间。这是一个异步接口，返回值为 AV_OK 的时候代表异步投递成功。

> !如果应用中有退房后立即进房的场景，在接口调用流程上，开发者无需要等待 ExitRoom 的回调 RoomExitComplete 通知，只需直接调用接口。

#### 函数原型  

```
ITMGContext ExitRoom()
```

#### 示例代码  

```
ITMGContext.GetInstance().ExitRoom();
```

### 退出房间回调
退出房间完成回调，通过委托传递消息。
#### 函数原型  
```
委托函数：
public delegate void QAVExitRoomComplete();
事件函数：
public abstract event QAVExitRoomComplete OnExitRoomCompleteEvent; 
```
#### 示例代码  

```
对事件进行监听：
ITMGContext.GetInstance().OnExitRoomCompleteEvent += new QAVExitRoomComplete(OnExitRoomComplete);
监听处理：
void OnExitRoomComplete(){
    //退出房间后的处理
}
```

### 获取用户房间音频类型
此接口用于获取用户房间音频类型，返回值为房间音频类型，返回值为0时代表获取用户房间音频类型发生错误，房间音频类型参考 EnterRoom 接口。

#### 函数原型  

```
ITMGContext ITMGRoom public int GetRoomType()
```


#### 示例代码  

```
ITMGContext.GetInstance().GetRoom().GetRoomType();
```

### 修改用户房间音频类型
此接口用于修改用户房间音频类型。

#### 函数原型  

```
ITMGContext ITMGRoom public int ChangeRoomType(ITMGRoomType roomtype)
```


|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| roomtype    |ITMGRoomType    |希望房间切换成的类型，房间音频类型参考 EnterRoom 接口|

#### 示例代码  

```
ITMGContext.GetInstance().GetRoom().ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);

```

### 修改房间音频类型回调
主动设置房间类型，房间类型设置后，通过委托传递修改完成的相关消息。

|返回的参数     | 含义  |
| ------------- |:-------------:|
| roomtype    |返回切换后的 roomtype 类型|


```
委托函数：
public abstract event QAVCallback OnChangeRoomtypeCallback;

事件函数：
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;
```

#### 示例代码  

```
对事件进行监听：
ITMGContext.GetInstance ().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent (OnRoomTypeChangedEvent);
监听处理：
void OnRoomTypeChangedEvent(int roomtype)
{
        ShowWarnning (string.Format ("RoomTypeChanged current:{0}",roomtype));
}

```

### 房间类型变化通知
用户主动修改房间类型，或者房间内其它用户修改房间类型，只要房间类型发生变化，该回调函数就会被调用，通过次回调函数通知业务层房间类型发生变化，返回的是房间类型，参考 EnterRoom 接口。
```
委托函数：
public delegate void QAVOnRoomTypeChangedEvent(int roomtype);

事件函数：
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;	
```
####  示例代码  
```
对事件进行监听：
ITMGContext.GetInstance().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent(OnRoomTypeChangedEvent);
监听处理：
void OnRoomTypeChangedEvent(int roomtype){
    //房间类型改变后的处理
}
```



### 成员状态变化
该事件在状态变化才通知，状态不变化的情况下不通知。如需实时获取成员状态，请在上层收到通知时缓存，事件消息为 ITMG_MAIN_EVNET_TYPE_USER_UPDATE，包含 event_id、count 及 openIdList，在 OnEvent 函数中对事件消息进行判断。
音频事件的通知有一个阈值，超过这个阈值才会发送通知。超过两秒没有收到音频包才通知“有成员停止发送音频包”消息。


| event_id                     |         含义         | 应用侧维护内容         |
| ------------- |:-------------:|-------------|
|EVENT_ID_ENDPOINT_ENTER    				|有成员进入房间			|应用侧维护成员列表		    |
|EVENT_ID_ENDPOINT_EXIT    				|有成员退出房间			|应用侧维护成员列表		    |
|EVENT_ID_ENDPOINT_HAS_AUDIO    		    |有成员发送音频包		|应用侧维护通话成员列表	    |
|EVENT_ID_ENDPOINT_NO_AUDIO    			|有成员停止发送音频包	|应用侧维护通话成员列表	    |

#### 维护房间成员流程图

![](https://main.qcloudimg.com/raw/50ef1ceda14eb244e434b8cbe85da5f3.png)

#### 示例代码

```
委托函数：
public delegate void QAVEndpointsUpdateInfo(int eventID, int count, [MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 1)]string[] openIdList);
事件函数：
public abstract event QAVEndpointsUpdateInfo OnEndpointsUpdateInfoEvent;

对事件进行监听：
ITMGContext.GetInstance().OnEndpointsUpdateInfoEvent += new QAVEndpointsUpdateInfo(OnEndpointsUpdateInfo);
监听处理：
void OnEndpointsUpdateInfo(int eventID, int count, string[] openIdList)
{
    //进行处理

		    switch (eventID)
 		    {
 		    case EVENT_ID_ENDPOINT_ENTER:
  			    //有成员进入房间
  			    break;
 		    case EVENT_ID_ENDPOINT_EXIT:
  			    //有成员退出房间
			    break;
		    case EVENT_ID_ENDPOINT_HAS_AUDIO:
			    //有成员发送音频包
			    break;
		    case EVENT_ID_ENDPOINT_NO_AUDIO:
			    //有成员停止发送音频包
			    break;
		  
		    default:
			    break;
 		    }
		break;
}

```


### 房间通话质量监控事件
质量监控事件，在进房后触发，2秒回调一次，事件消息为 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY，返回的参数为 weight、loss 及 delay，代表的信息如下，在 OnEvent 函数中对事件消息进行判断。

|参数     | 类型        | 含义         |
| ------------- |-------------|-------------|
|weight  |int  				|范围是 1 - 50，数值为50是音质评分极好，数值为1是音质评分很差，几乎不能使用，数值为0代表初始值，无含义。一般数值在 30 以下就可以提醒用户网络较差，建议切换网络。|
|loss   |double				|上行丢包率|
|delay   |int 		|音频触达延迟时间（ms）|


## 实时语音音频接口

![Image](https://main.qcloudimg.com/raw/863e0c165c7d43f9db59066befaac1e4.png)

### 实时语音音频接入须知

初始化 SDK 之后进房，在房间中，才可以调用实时音频语音相关接口。
当用户界面单击打开/关闭麦克风/扬声器按钮时，建议如下方式：

- **对于大部分的游戏类 App，推荐调用 EnableMic 及 EnableSpeaker 接口**，相当于同时调用 EnableAudioCaptureDevice/EnableAudioSend 和 EnableAudioPlayDevice/EnableAudioRecv 接口。
- 其他类型的移动端 App 例如社交类型 App，打开或者关闭采集设备，会伴随整个设备（采集及播放）重启，如果此时 App 正在播放背景音乐，那么背景音乐的播放也会被中断。利用控制上下行的方式来实现开关麦克风效果，不会中断播放设备。**具体调用方式为：在进房的时候调用 EnableAudioCaptureDevice(true) && EnableAudioPlayDevice(true) 一次，单击开关麦克风时只调用 EnableAudioSend/Recv 来控制音频流是否发送/接收**。
- 如果想单独释放采集或者播放设备，请参考接口 EnableAudioCaptureDevice 及 EnableAudioPlayDevice。
- 调用 pause 暂停音频引擎，调用 resume 恢复音频引擎。

### 实时语音音频相关接口

| 接口                        |            接口含义            |
| --------------------------- | :----------------------------: |
| EnableMic                   |           开关麦克风           |
| GetMicState                 |         获取麦克风状态         |
| EnableAudioCaptureDevice    |          开关采集设备          |
| IsAudioCaptureDeviceEnabled |        获取采集设备状态        |
| EnableAudioSend             |        打开关闭音频上行        |
| IsAudioSendEnabled          |        获取音频上行状态        |
| GetMicLevel                 |       获取实时麦克风音量       |
| GetSendStreamLevel          |      获取音频上行实时音量      |
| SetMicVolume                |         设置麦克风音量         |
| GetMicVolume                |         获取麦克风音量         |
| EnableSpeaker               |           开关扬声器           |
| GetSpeakerState             |         获取扬声器状态         |
| EnableAudioPlayDevice       |          开关播放设备          |
| IsAudioPlayDeviceEnabled    |        获取播放设备状态        |
| EnableAudioRecv             |        打开关闭音频下行        |
| IsAudioRecvEnabled          |        获取音频下行状态        |
| GetSpeakerLevel             |       获取实时扬声器音量       |
| GetRecvStreamLevel          | 获取房间内其他成员下行实时音量 |
| SetSpeakerVolume            |         设置扬声器音量         |
| GetSpeakerVolume            |         获取扬声器音量         |
| EnableLoopBack              |            开关耳返            |

## 实时语音采集相关接口

### 开启或关闭麦克风

此接口用来开启关闭麦克风。加入房间默认不打开麦克风及扬声器。
**如果有使用伴奏的情况，请参考 [实时语音伴奏流程图](https://intl.cloud.tencent.com/document/product/607/31504) 进行调用。**

EnableMic = EnableAudioCaptureDevice + EnableAudioSend


#### 函数原型  

```
ITMGAudioCtrl EnableMic(bool isEnabled)
```

| 参数      |  类型   | 含义                                                         |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled | boolean | 如果需要打开麦克风，则传入的参数为 true，如果关闭麦克风，则参数为 false |

#### 示例代码  

```
打开麦克风
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```

### 麦克风状态获取

此接口用于获取麦克风状态，返回值0为关闭麦克风状态，返回值1 为打开麦克风状态。

#### 函数原型  

```
ITMGAudioCtrl GetMicState()
```

#### 示例代码  

```
micToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetMicState();
```

### 开启或关闭采集设备

此接口用来开启/关闭采集设备。加入房间默认不打开设备。

- 只能在进房后调用此接口，退房会自动关闭设备。
- 在移动端，打开采集设备通常会伴随权限申请，音量类型调整等操作。

#### 函数原型  

```
ITMGAudioCtrl int EnableAudioPlayDevice(bool isEnabled)
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| isEnabled    |bool     |如果需要打开采集设备，则传入的参数为 true，如果关闭采集设备，则参数为 false|

#### 示例代码

```
打开采集设备
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### 采集设备状态获取

此接口用于采集设备状态获取。

#### 函数原型

```
ITMGAudioCtrl bool IsAudioCaptureDeviceEnabled()
```

#### 示例代码

```
bool IsAudioCaptureDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### 打开或关闭音频上行

此接口用于打开/关闭音频上行。如果采集设备已经打开，那么会发送采集到的音频数据。如果采集设备没有打开，那么仍旧无声。采集设备的打开关闭参见接口 EnableAudioCaptureDevice。

#### 函数原型

```
ITMGAudioCtrl int EnableAudioSend(bool isEnabled)
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| isEnabled    |bool     |如果需要打开音频上行，则传入的参数为 true，如果关闭音频上行，则参数为 false|

#### 示例代码  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioSend(true);
```

### 音频上行状态获取

此接口用于音频上行状态获取。

#### 函数原型  

```
ITMGAudioCtrl bool IsAudioSendEnabled()
```

#### 示例代码  

```
bool IsAudioSend = ITMGContext.GetInstance().GetAudioCtrl().IsAudioSendEnabled();

```

### 获取麦克风实时音量

此接口用于获取麦克风实时音量，返回值为 int 类型。建议 20ms 获取一次。值域为 0 到 100，通过此接口可以获取到麦克风采集到的实时音量情况。

>?此接口不适用于语音消息服务。

#### 函数原型  

```
ITMGAudioCtrl int GetMicLevel
```

#### 示例代码  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicLevel();
```

### 获取音频上行实时音量

此接口用于获取自己音频上行实时音量，返回值为 int 类型，取值范围为 0 到 100。
>?此接口不适用于语音消息服务。

#### 函数原型  

```
ITMGAudioCtrl int GetSendStreamLevel()
```

#### 示例代码  

```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetSendStreamLevel();
```

### 设置麦克风软件音量

此接口用于设置麦克风的音量。参数 volume 用于设置麦克风的音量，相当于对采集的声音做衰减或增益，当数值为 0 的时候表示静音，当数值为 100 的时候表示音量不增不减，默认数值为 100。
>?此接口不适用于语音消息服务。
>
#### 函数原型  

```
ITMGAudioCtrl SetMicVolume(int volume)
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| volume    |int      |设置音量，范围0到200|

#### 示例代码  

```
int micVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetMicVolume (micVol);
```

### 获取麦克风软件音量

此接口用于获取麦克风的音量。返回值为一个int类型数值，返回值为 101代表没调用过接口 SetMicVolume。
>?此接口不适用于语音消息服务。

#### 函数原型  

```
ITMGAudioCtrl GetMicVolume()
```

#### 示例代码  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicVolume();
```

## 实时语音播放相关接口

### 开启或关闭扬声器

此接口用于开启关闭扬声器。
**如果有使用伴奏的情况，请参见 [实时语音伴奏流程图](https://intl.cloud.tencent.com/document/product/607/31504) 进行调用。**

EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.

#### 函数原型  

```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| isEnabled    |bool        |如果需要关闭扬声器，则传入的参数为 false，如果打开扬声器，则参数为 true|

####  示例代码  
```
打开扬声器
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```

### 扬声器状态获取

此接口用于扬声器状态获取。返回值 0 为关闭扬声器状态，返回值1 为打开扬声器状态，返回值2 为扬声器设备正在操作中。

#### 函数原型  

```
ITMGAudioCtrl GetSpeakerState()
```

#### 示例代码  

```
speakerToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerState();
```



### 开启或关闭播放设备

此接口用于开启关闭播放设备。

#### 函数原型  

```
ITMGAudioCtrl EnableAudioPlayDevice(bool isEnabled)
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| isEnabled    |bool        |如果需要关闭播放设备，则传入的参数为 false，如果打开播放设备，则参数为 true|

#### 示例代码  

```
//打开播放设备
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioPlayDevice(true);
```

### 播放设备状态获取

此接口用于播放设备状态获取。

#### 函数原型

```
ITMGAudioCtrl bool IsAudioPlayDeviceEnabled()
```

#### 示例代码  

```
bool IsAudioPlayDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### 打开或关闭音频下行

此接口用于打开/关闭音频下行。如果播放设备已经打开，那么会播放房间里其他人的音频数据。如果播放设备没有打开，那么仍旧无声。播放设备的打开关闭参见接口 参见 EnableAudioPlayDevice。

#### 函数原型  

```
ITMGAudioCtrl int EnableAudioRecv(bool isEnabled)
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| isEnabled    |bool     |如果需要打开音频下行，则传入的参数为 true，如果关闭音频下行，则参数为 false|

#### 示例代码  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioRecv(true);
```



### 音频下行状态获取

此接口用于音频下行状态获取。

#### 函数原型  

```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

#### 示例代码  

```
bool IsAudioRecv = ITMGContext.GetInstance().GetAudioCtrl().IsAudioRecvEnabled();
```

### 获取扬声器实时音量

此接口用于获取扬声器实时音量。返回值为 int 类型数值，表示扬声器实时音量。建议 20ms 获取一次。

#### 函数原型  

```
ITMGAudioCtrl GetSpeakerLevel()
```

#### 示例代码  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerLevel();

```

### 获取房间内其他成员下行实时音量

此接口用于获取房间内其他成员下行实时音量，返回值为 int 类型，取值范围为0到200。

#### 函数原型  

```
ITMGAudioCtrl int GetRecvStreamLevel(string openId)
```

| 参数   |  类型  | 含义                 |
| ------ | :----: | -------------------- |
| openId | string | 房间其他成员的openId |

#### 示例代码  

```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetRecvStreamLevel(openId);
```

### 设置扬声器的音量

此接口用于设置扬声器的音量。
参数 volume 用于设置扬声器的音量，当数值为0时，表示静音，当数值为100时，表示音量不增不减，默认数值为 100。

#### 函数原型  

```
ITMGAudioCtrl SetSpeakerVolume(int volume)
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| volume    |int        |设置音量，范围0到200|

#### 示例代码  

```
int speVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolume(speVol);
```

### 获取扬声器的音量

此接口用于获取扬声器的音量。返回值为 int 类型数值，代表扬声器的音量，返回值为101代表没调用过接口 SetSpeakerVolume。
Level 是实时音量，Volume 是扬声器的音量，最终声音音量相当于 Level x Volume%。示例如下：
实时音量是数值是 100 ，此时 Volume 的数值是 60，则最终发出来的声音数值也是 60。

#### 函数原型  

```
ITMGAudioCtrl GetSpeakerVolume()
```

#### 示例代码  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerVolume();
```

### 启动耳返

此接口用于启动耳返，需要 EnableLoopBack+EnableSpeaker 才可以听到自己声音。

#### 函数原型  

```
ITMGContext GetAudioCtrl EnableLoopBack(bool enable)
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| enable    |bool         |设置是否启动|

#### 示例代码  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableLoopBack(true);
```

### 设备占用和释放事件回调
在房间内，占用设备和释放设备时会回调，通过委托传递事件的相关消息。

```
委托函数：
public delegate void QAVOnDeviceStateChangedEvent(int deviceType, string deviceId, bool openOrClose);
事件函数：
public abstract event QAVOnDeviceStateChangedEvent OnDeviceStateChangedEvent;
```

|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| deviceType    	|int       	|1 代表采集设备，2 代表播放设备							|
| deviceId   	 	|string 	|设备 GUID，用于标记设备，仅在 Windows 端和 Mac 端有效	|
| openOrClose    |bool  	|采集设备/播放设备占用或者释放							|

#### 示例代码  

```
对事件进行监听：
ITMGContext.GetInstance().GetAudioCtrl().OnDeviceStateChangedEvent += new QAVAudioDeviceStateCallback(OnAudioDeviceStateChange);
监听处理：
void QAVAudioDeviceStateCallback(int deviceType, string deviceId, bool openOrClose){
    //设备占用和释放事件相关回调处理
}
```
## 语音消息及转文字

语音消息，录制并发送一段语音消息，同时可以将语音消息转成文字，也可以同时将文字进行翻译。

>?建议使用流式语音转文字服务

### 语音消息及语音转文字流程图

<img src="https://main.qcloudimg.com/raw/310eaf2b780c5fc47ffeaf791a6df392.png" width="70%">


| 接口                                   |          接口含义          |
| -------------------------------------- | :------------------------: |
| ApplyPTTAuthbuffer                     |         鉴权初始化         |
| SetMaxMessageLength                    |    限制最大语音信息时长    |
| StartRecording                         |          启动录音          |
| StartRecordingWithStreamingRecognition |        启动流式录音        |
| PauseRecording                         |          暂停录音          |
| ResumeRecording                        |          恢复录音          |
| StopRecording                          |          停止录音          |
| CancelRecording                        |          取消录音          |
| GetMicLevel                            | 			获取实时麦克风音量 |
| SetMicVolume                           |    设置录制音量    |
| GetMicVolume                           |    获取录制音量    |
| GetSpeakerLevel                        | 获取实时扬声器音量 |
| SetSpeakerVolume                       |    设置播放音量    |
| GetSpeakerVolume                       |    获取播放音量    |
| UploadRecordedFile                     |        上传语音文件        |
| DownloadRecordedFile                   |        下载语音文件        |
| PlayRecordedFile                       |          播放语音          |
| StopPlayFile                           |        停止播放语音        |
| GetFileSize                            |       语音文件的大小       |
| GetVoiceFileDuration                   |       语音文件的时长       |
| SpeechToText                           |       语音识别成文字       |


### 初始化SDK

未初始化前，SDK 处于未初始化阶段，需要通过接口 Init 初始化 SDK，才可以使用实时语音及语音消息服务。

使用问题可参考 [离线语音相关问题](https://intl.cloud.tencent.com/document/product/607/30258)。

### 初始化相关接口

| 接口   |   接口含义   |
| ------ | :----------: |
| Init   |  初始化 GME  |
| Poll   | 触发事件回调 |
| Pause  |   系统暂停   |
| Resume |   系统恢复   |
| Uninit | 反初始化 GME |



### 鉴权初始化

在初始化 SDK 之后调用鉴权初始化，authBuffer 的获取参见上文实时语音鉴权信息接口。

#### 函数原型  

```
ITMGPTT int ApplyPTTAuthbuffer (byte[] authBuffer)
```

| 参数       |  类型  | 含义 |
| ---------- | :----: | ---- |
| authBuffer    |byte[]                   |鉴权|

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().ApplyPTTAuthbuffer(authBuffer);
```


## 流式语音识别


### 启动流式语音识别

此接口用于启动流式语音识别，同时在回调中会有实时的语音转文字返回，可以指定语言进行识别，也可以将语音中识别到的信息翻译成指定的语言返回。**停止录音调用StopRecording**。

#### 函数原型  

```
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath)
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath, string translateLanguage,string translateLanguage) 
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| filePath			|String	|存放的语音路径	|
| speechLanguage    		|String	|识别成指定文字的语言参数，参数请参考 [语音转文字的语言参数参考列表](https://intl.cloud.tencent.com/document/product/607/30260)|
| translateLanguage	|String	|翻译成指定文字的语言参数，参数请参考 [语音转文字的语言参数参考列表](https://intl.cloud.tencent.com/document/product/607/30260)（此参数暂不可用,请填写与 speechLanguage 相同的参数）|

#### 示例代码  

```
string recordPath = Application.persistentDataPath + string.Format("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecordingWithStreamingRecognition(recordPath, "cmn-Hans-CN","cmn-Hans-CN");
```


### 流式语音识别的回调
启动流式语音识别后，需要在回调函数 OnEvent 中监听回调消息，事件消息分为以下两个：
- ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE 是在停止录制并完成识别后才返回文字，相当于一段话说完才会返回识别的文字。
- ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING 是在录音过程中就会实时返回识别到的文字，相当于边说话边返回识别到的文字。

根据需求在 OnEvent 函数中对相应事件消息进行判断。传递的参数包含以下四个信息。

|消息名称     | 含义         |
| ------------- |:-------------:|
| result    	|用于判断流式语音识别是否成功的返回码		|
| text    		|语音转文字识别的文本	|
| file_path 	|录音存放的本地地址		|
| file_id 		|录音在后台的 url 地址，录音在服务器存放90天|

>!监听 ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING 消息时，file_id 为空。

#### 错误码

|错误码     | 含义         |处理方式|
| ------------- |:-------------:|:-------------:|
|32775	|流式语音转文本失败，但是录音成功	|调用 UploadRecordedFile 接口上传录音，再调用 SpeechToText 接口进行语音转文字操作
|32777	|流式语音转文本失败，但是录音成功，上传成功	|返回的信息中有上传成功的后台 url 地址，调用 SpeechToText 接口进行语音转文字操作
|32786  |流式语音转文本失败|在流式录制状态当中，请等待流式录制接口执行结果返回|

#### 示例代码  

```
			对事件进行监听：
			ITMGContext.GetInstance().GetPttCtrl().OnStreamingSpeechComplete +=new QAVStreamingRecognitionCallback (OnStreamingSpeechComplete);
			ITMGContext.GetInstance().GetPttCtrl().OnStreamingSpeechisRunning += new QAVStreamingRecognitionCallback (OnStreamingRecisRunning);
			监听处理：
			void OnStreamingSpeechComplete(int code, string fileid, string filepath, string result){
					//启动流式语音识别的回调
			}

			void OnStreamingRecisRunning(int code, string fileid, string filePath, string result){
					if (code == 0)
					{
						setBtnText(mStreamBtn, "流式");
						InputField field = transform.Find("recordFilePath").GetComponent<InputField>();
						field.text = filePath;

						field = transform.Find("downloadUrl").GetComponent<InputField>();
						field.text = "Stream is Running";

						field = transform.Find("convertTextResult").GetComponent<InputField>();
						field.text = result;
						showWarningText("录制中");
					}	
}
```



## 语音消息录制

### 限制最大语音信息时长

限制最大语音消息的长度，最大支持58秒。

#### 函数原型

```
ITMGPTT int SetMaxMessageLength(int msTime)
```

| 参数   | 类型 | 含义                                             |
| ------ | :--: | ------------------------------------------------ |
| msTime | int  | 语音时长，单位 ms，区间为 1000 < msTime < 58000 |

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().SetMaxMessageLength(10000); 
```

### 启动录音

此接口用于启动录音。需要将录音文件上传后才可以进行语音转文字等操作。

#### 函数原型  

```
ITMGPTT int StartRecording(string fileDir)
```

| 参数     |  类型  | 含义           |
| -------- | :----: | -------------- |
| fileDir    |string                      |存放的语音路径|

#### 示例代码  

```
string recordPath = Application.persistentDataPath + string.Format ("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecording(recordPath);
```

### 启动录音的回调
录音完成的回调，通过委托传递消息。
#### 函数原型  
```
委托函数：
public delegate void QAVRecordFileCompleteCallback(int code, string filepath); 
事件函数：
public abstract event QAVRecordFileCompleteCallback OnRecordFileComplete;
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| code    |string                      |当 code 为 0 时，录制完成|
| filepath    |string                      |录制的存放地址|

#### 错误码

| 错误码值 | 原因                     | 建议方案                                                     |
| -------- | ------------------------ | ------------------------------------------------------------ |
| 4097     | 参数为空                 | 检查代码中接口参数是否正确                                   |
| 4098     | 初始化错误               | 检查设备是否被占用，或者权限是否正常，是否初始化正常         |
| 4099     | 正在录制中               | 确保在正确的时机使用 SDK 录制功能                            |
| 4100     | 没有采集到音频数据       | 检查麦克风设备是否正常                                       |
| 4101     | 录音时，录制文件访问错误 | 确保文件存在，文件路径的合法性                               |
| 4102     | 麦克风未授权错误         | 使用 SDK 需要麦克风权限，添加权限请参考对应引擎或平台的 SDK 工程配置文档 |
| 4103     | 录音时间太短错误         | 首先，限制录音时长的单位为毫秒，检查参数是否正确；其次，录音时长要1000毫秒以上才能成功录制 |
| 4104     | 没有启动录音操作         | 检查是否已经调用启动录音接口                                 |

#### 示例代码  

```
对事件进行监听：
ITMGContext.GetInstance().GetPttCtrl().OnRecordFileComplete +=  new QAVRecordFileCompleteCallback (OnRecordFileComplete);
监听处理：
void OnRecordFileComplete(int code, string filepath){
    //启动录音的回调
}
```


### 暂停录音

此接口用于暂停录音。如需恢复录音请调用接口 ResumeRecording。

#### 函数原型  

```
ITMGPTT int PauseRecording()
```

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().PauseRecording();
```

### 恢复录音

此接口用于恢复录音。

#### 函数原型  

```
ITMGPTT int ResumeRecording()
```

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().ResumeRecording();
```

### 停止录音

此接口用于停止录音。此接口为异步接口，停止录音后会有录音完成回调，成功之后录音文件才可用。

#### 函数原型  

```
ITMGPTT int StopRecording()
```

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().StopRecording();
```



### 取消录音

调用此接口取消录音。取消之后没有回调。

#### 函数原型  

```
ITMGPTT int CancelRecording()
```

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().CancelRecording();
```

### 获取语音消息麦克风实时音量

此接口用于获取麦克风实时音量，返回值为 int 类型，值域为0到200。

#### 函数原型  

```
ITMGPTT int GetMicLevel()
```

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().GetMicLevel();

```

### 设置语音消息录制音量

此接口用于设置离线语音录制音量，值域为0到200。

#### 函数原型  

```
ITMGPTT int SetMicVolume(int vol)
```

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().SetMicVolume(100);
```

### 获取语音消息录制音量

此接口用于获取离线语音录制音量。返回值为 int 类型，值域为0到200。

#### 函数原型  

```
ITMGPTT int GetMicVolume()
```

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().GetMicVolume();
```

### 获取语音消息扬声器实时音量

此接口用于获取扬声器实时音量。返回值为 int 类型，值域为0到200。

#### 函数原型  

```
ITMGPTT int GetSpeakerLevel()
```

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().GetSpeakerLevel();
```

### 设置语音消息播放音量

此接口用于设置离线语音播放音量，值域为0到200。

#### 函数原型  

```
ITMGPTT int SetSpeakerVolume(int vol)
```

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().SetSpeakerVolume(100);
```

### 获取语音消息播放音量

此接口用于获取离线语音播放音量。返回值为 int 类型，值域为0到200。

#### 函数原型  
```
ITMGPTT int GetSpeakerVolume()
```

#### 示例代码  
```
ITMGContext.GetInstance().GetPttCtrl().GetSpeakerVolume();
```

## 语音消息播放
### 播放语音

此接口用于播放语音。

#### 函数原型  

```
ITMGPTT PlayRecordedFile (string downloadFilePath)
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| downloadFilePath    |string                       |文件的路径|

#### 错误码

| 错误码值 | 原因       | 建议方案                       |
| -------- | ---------- | ------------------------------ |
| 20485    | 播放未开始 | 确保文件存在，文件路径的合法性 |

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().PlayRecordedFile(filePath); 
```

### 播放语音的回调
播放语音的回调，通过委托传递消息。
#### 函数原型  
```
委托函数：
public delegate void QAVPlayFileCompleteCallback(int code, string filepath);
事件函数：
public abstract event QAVPlayFileCompleteCallback OnPlayFileComplete;
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| code    |int                       |当 code 为0时，播放完成|
| filepath    |string                      |录制的存放地址|

#### 错误码

| 错误码值 | 原因                                                       | 建议方案                                                     |
| -------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| 20481    | 初始化错误                                                 | 检查设备是否被占用，或者权限是否正常，是否初始化正常         |
| 20482    | 正在播放中，试图打断并播放下一个失败了（正常是可以打断的） | 检查代码逻辑是否正确                                         |
| 20483    | 参数为空                                                   | 检查代码中接口参数是否正确                                   |
| 20484    | 内部错误                                                   | 初始化播放器错误，解码失败等问题产生此错误码，需要结合日志定位问题 |

#### 示例代码

```
对事件进行监听：
ITMGContext.GetInstance().GetPttCtrl().OnPlayFileComplete +=new  QAVPlayFileCompleteCallback(OnPlayFileComplete);
监听处理：
void OnPlayFileComplete(int code, string filepath){
    //播放语音的回调
}

```



### 停止播放语音

此接口用于停止播放语音。停止播放语音也会有播放完成的回调。

#### 函数原型  

```
ITMGPTT int StopPlayFile()
```

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().StopPlayFile();
```



### 获取语音文件的大小

通过此接口，获取语音文件的大小。

#### 函数原型  

```
ITMGPTT GetFileSize(string filePath) 
```

| 参数     |  类型  | 含义           |
| -------- | :----: | -------------- |
| filePath | String | 语音文件的路径，此路径为本地路径 |

#### 示例代码  

```
int fileSize = ITMGContext.GetInstance().GetPttCtrl().GetFileSize(filepath);
```

### 获取语音文件的时长

此接口用于获取语音文件的时长，单位毫秒。

#### 函数原型  

```
ITMGPTT int GetVoiceFileDuration(string filePath)
```

| 参数     |  类型  | 含义           |
| -------- | :----: | -------------- |
| filePath | String | 语音文件的路径，此路径为本地路径 |

#### 示例代码  

```
int fileDuration = ITMGContext.GetInstance().GetPttCtrl().GetVoiceFileDuration(filepath);
```


## 语音消息上传及下载

### 上传语音文件

此接口用于上传语音文件。

#### 函数原型  

```
ITMGPTT int UploadRecordedFile (string filePath)
```

| 参数     |  类型  | 含义           |
| -------- | :----: | -------------- |
| filePath | String | 上传的语音路径，此路径为本地路径 |

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().UploadRecordedFile(filePath);
```

### 上传语音完成的回调
上传语音完成的回调，通过委托传递消息。
#### 函数原型

```
委托函数：
public delegate void QAVUploadFileCompleteCallback(int code, string filepath, string fileid);
事件函数：
public abstract event QAVUploadFileCompleteCallback OnUploadFileComplete; 
```

|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| code    |int                       |当 code 为0时，录制完成|
| filepath    |string                      |录制的存放地址|
| fileid    |string                      |文件的 url 路径，录音在服务器存放 90 天|

#### 错误码

| 错误码值 | 原因                           | 建议方案                                               |
| -------- | ------------------------------ | ------------------------------------------------------ |
| 8193     | 上传文件时，文件访问错误       | 确保文件存在，文件路径的合法性                         |
| 8194     | 签名校验失败错误               | 检查鉴权密钥是否正确，检查是否有初始化离线语音         |
| 8195     | 网络错误                       | 检查设备网络是否可以正常访问外网环境                   |
| 8196     | 获取上传参数过程中网络失败     | 检查鉴权是否正确，检查设备网络是否可以正常访问外网环境 |
| 8197     | 获取上传参数过程中回包数据为空 | 检查鉴权是否正确，检查设备网络是否可以正常访问外网环境 |
| 8198     | 获取上传参数过程中回包解包失败 | 检查鉴权是否正确，检查设备网络是否可以正常访问外网环境 |
| 8200     | 没有设置 appinfo               | 检查 apply 接口是否有调用，或者入参是否为空            |

#### 示例代码

```
对事件进行监听：
ITMGContext.GetInstance().GetPttCtrl().OnUploadFileComplete +=new QAVUploadFileCompleteCallback (OnUploadFileComplete);
监听处理：
void OnUploadFileComplete(int code, string filepath, string fileid){
    //上传语音完成的回调
}
```

### 下载语音文件

此接口用于下载语音文件。

#### 函数原型  

```
ITMGPTT DownloadRecordedFile (string fileID, string downloadFilePath)
```

| 参数             |  类型  | 含义                                  |
| ---------------- | :----: | ------------------------------------- |
| fileID           | String | 文件的 url 路径 |
| downloadFilePath | String | 文件的本地保存路径                    |

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().DownloadRecordedFile(fileId, filePath);
```

### 下载语音文件完成回调
下载语音文件完成回调，通过委托传递消息。
#### 函数原型  
```
委托函数：
public delegate void QAVDownloadFileCompleteCallback(int code, string filepath, string fileid);
事件函数：
public abstract event QAVDownloadFileCompleteCallback OnDownloadFileComplete;
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| code    |int                       |当 code 为0时，录制完成|
| filepath    |string                      |录制的存放地址|
| fileid    |string                      |文件的 url 路径，录音在服务器存放 90 天|

#### 错误码

| 错误码值 | 原因                              | 建议方案                                                     |
| -------- | --------------------------------- | ------------------------------------------------------------ |
| 12289    | 下载文件时，文件访问错误          | 检查文件路径是否合法                                         |
| 12290    | 签名校验失败                      | 检查鉴权密钥是否正确，检查是否有初始化离线语音               |
| 12291    | 网络存储系统异常                  | 服务器获取语音文件失败，检查接口参数 fileid 是否正确，检查网络是否正常，检查 cos 文件存不存在 |
| 12292    | 服务器文件系统错误                | 检查设备网络是否可以正常访问外网环境，检查服务器上是否有此文件 |
| 12293    | 获取下载参数过程中，HTTP 网络失败 | 检查设备网络是否可以正常访问外网环境                         |
| 12294    | 获取下载参数过程中，回包数据为空  | 检查设备网络是否可以正常访问外网环境                         |
| 12295    | 获取下载参数过程中，回包解包失败  | 检查设备网络是否可以正常访问外网环境                         |
| 12297    | 没有设置 appinfo                  | 检查鉴权密钥是否正确，检查是否有初始化离线语音               |

#### 示例代码

```
对事件进行监听：
ITMGContext.GetInstance().GetPttCtrl().OnDownloadFileComplete +=new QAVDownloadFileCompleteCallback(OnDownloadFileComplete);
监听处理：
void OnDownloadFileComplete(int code, string filepath, string fileid){
    //下载语音文件完成回调
}

```


## 语音转文字服务

### 将指定的语音文件识别成文字

此接口用于将指定的语音文件识别成文字。

#### 函数原型  

```
ITMGPTT int SpeechToText(String fileID)
```

| 参数   |  类型  | 含义                               |
| ------ | :----: | ---------------------------------- |
| fileID | String | 语音文件 url |

#### 示例代码  

```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID);
```



### 将指定的语音文件翻译成文字（指定语言）

此接口可以指定语言进行识别，也可以将语音中识别到的信息翻译成指定的语言返回。

#### 函数原型  

```
ITMGPTT int SpeechToText(String fileID,String language)
```

| 参数              |  类型  | 含义                                                         |
| ----------------- | :----: | ------------------------------------------------------------ |
| fileID            | String | 语音文件 url，录音在服务器存放90天                           |
| speechLanguage    | String | 识别出指定文字的语言参数，语音转文字的参数请参见 [语言参数参考列表](https://intl.cloud.tencent.com/document/product/607/30260) |
| translatelanguage | String | 翻译成指定文字的语言参数，语音转文字的参数请参见 [语言参数参考列表](https://intl.cloud.tencent.com/document/product/607/30260)（此参数暂时无效，填入参数应与 speechLanguage 一致） |

#### 示例代码  
```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID,"cmn-Hans-CN","cmn-Hans-CN");
```



### 识别回调
将指定的语音文件识别成文字，通过委托传递消息。
#### 函数原型  

```
委托函数：
public delegate void QAVSpeechToTextCallback(int code, string fileid, string result);
事件函数：
public abstract event QAVSpeechToTextCallback OnSpeechToTextComplete;
```

|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| code    |int                       |当 code 为0时，录制完成|
| fileid    |string                      |语音文件 url，录音在服务器存放 90 天	|
| result    |string                      |转换的文本结果|

#### 错误码

| 错误码值 | 原因                   | 建议方案                                                     |
| -------- | ---------------------- | ------------------------------------------------------------ |
| 32769    | 内部错误               | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| 32770    | 网络失败               | 检查设备网络是否可以正常访问外网环境                         |
| 32772    | 回包解包失败           | 分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决。 |
| 32774    | 没有设置 appinfo       | 检查鉴权密钥是否正确，检查是否有初始化离线语音               |
| 32776    | authbuffer 校验失败    | 检查 authbuffer 是否正确                                     |
| 32784    | 语音转文本参数错误     | 检查代码中接口参数 fileid 是否为空                           |
| 32785    | 语音转文本翻译返回错误 | 离线语音后台错误，请分析日志，获取后台返回给客户端的真正错误码，并联系后台同事协助解决 |

#### 示例代码

```
对事件进行监听：
ITMGContext.GetInstance().GetPttCtrl().OnSpeechToTextComplete += new QAVSpeechToTextCallback(OnSpeechToTextComplete);
监听处理：
void OnSpeechToTextComplete(int code, string fileid, string result){
    //识别回调
}

```



## 高级 API

### 获取版本号

获取 SDK 版本号，用于分析。

#### 函数原型

```
ITMGContext  abstract string GetSDKVersion()
```

#### 示例代码  

```
ITMGContext.GetInstance().GetSDKVersion();
```



### 设置打印日志等级

用于设置打印日志等级。建议保持默认等级。

#### 函数原型

```
ITMGContext  SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### 参数含义

| 参数       | 类型           | 含义                                                         |
| ---------- | -------------- | ------------------------------------------------------------ |
| levelWrite | ITMG_LOG_LEVEL | 设置写入日志的等级，TMG_LOG_LEVEL_NONE 表示不写入，默认为 TMG_LOG_LEVEL_INFO |
| levelPrint | ITMG_LOG_LEVEL | 设置打印日志的等级，TMG_LOG_LEVEL_NONE 表示不打印，默认为 TMG_LOG_LEVEL_ERROR |



| ITMG_LOG_LEVEL          | 含义                 |
| ----------------------- | -------------------- |
| TMG_LOG_LEVEL_NONE=0    | 不打印日志           |
| TMG_LOG_LEVEL_ERROR=1   | 打印错误日志（默认） |
| TMG_LOG_LEVEL_INFO=2    | 打印提示日志         |
| TMG_LOG_LEVEL_DEBUG=3   | 打印开发调试日志     |
| TMG_LOG_LEVEL_VERBOSE=4 | 打印高频日志         |

#### 示例代码  

```
ITMGContext.GetInstance().SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```



### 设置打印日志路径
用于设置打印日志路径。
默认路径为：

|平台     |路径        |
| ------------- |-------------|
|Windows 	|%appdata%\Tencent\GME\ProcessName|
|iOS    		|Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents|
|Android	|/sdcard/Android/data/xxx.xxx.xxx/files|
|Mac    		|/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents|

#### 函数原型

```
ITMGContext  SetLogPath(string logDir)
```

| 参数   |  类型  | 含义 |
| ------ | :----: | ---- |
| logDir | String | 路径 |

#### 示例代码  

```
ITMGContext.GetInstance().SetLogPath(path);
```

### 获取诊断信息

获取音视频通话的实时通话质量的相关信息。该接口主要用来查看实时通话质量、排查问题等，业务侧可以忽略。

#### 函数原型  

```
ITMGRoom GetQualityTips()
```

#### 示例代码  

```
string tips = ITMGContext.GetInstance().GetRoom().GetQualityTips();
```

### 加入音频数据黑名单

将某个 ID 加入音频数据黑名单，即不接受某人的语音， 只对本端生效。返回值为 0 表示调用成功。例如 ：A，B，C 都在同一个房间开麦说话： 
- 如果 A 设置了 C 的黑名单， 则 A 只能听见 B 的声音。
- B 因为没有设置黑名单， 仍旧可以听见 A 和 C 的声音。
- C 同样因为没有设置黑名单， 可以听见 A 和 B 的声音。

#### 函数原型  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(String openId)
```

| 参数   |  类型  | 含义              |
| ------ | :----: | ----------------- |
| openId | String | 需添加黑名单的 ID |

#### 示例代码  

```
ITMGContext.GetInstance().GetAudioCtrl ().AddAudioBlackList (id);
```

### 移除音频数据黑名单

将某个 ID 移除音频数据黑名单。返回值为 0 表示调用成功。

#### 函数原型  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(string openId)
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| openId    |NSString      |需移除黑名单的 id|

#### 示例代码  

```
ITMGContext.GetInstance().GetAudioCtrl ().RemoveAudioBlackList (id);
```

