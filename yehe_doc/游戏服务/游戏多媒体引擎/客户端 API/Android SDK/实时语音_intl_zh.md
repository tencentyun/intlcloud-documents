为方便 Android 开发者调试和接入腾讯云游戏多媒体引擎客户端 API，本文为您介绍适用于 Android 实时语音功能的开发接入技术文档。

## 使用 GME 重要事项

GME 提供实时语音服务、语音消息服务及转文本服务，使用 GME 服务都依赖 Init 和 Poll 等核心接口。

#### 重点提示

- 已完成 GME 应用创建，并获取 SDK AppID 和 Key。请参考 [服务开通指引](https://intl.cloud.tencent.com/document/product/607/10782)。
- 已开通 **GME 实时语音服务、语音消息服务以及转文本服务**。请参考 [服务开通指引](https://intl.cloud.tencent.com/document/product/607/10782)。
- GME 使用前请对工程进行配置，否则 SDK 不生效。
- GME 的接口调用成功后返回值为 QAVError.OK，数值为 0。
- GME 的接口调用要在同一个线程下。
- GME 需要周期性的调用 Poll 接口触发事件回调。
- 错误码详情可参考 <dx-tag-link link="https://cloud.tencent.com/document/product/607/15173" tag="ErrorCode">错误码</dx-tag-link>。

## 接入 SDK

### 重要步骤

接入 SDK 重要流程如下：

<img src="https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg"  width="70%" /></img>

<dx-steps>
-<dx-tag-link link="#Init" tag="接口：Init">初始化 GME</dx-tag-link>
-<dx-tag-link link="#Poll" tag="接口：Poll">周期性调用 Poll 触发回调</dx-tag-link>
-<dx-tag-link link="#EnterRoom" tag="接口：EnterRoom">进入实时语音房间</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="接口：EnableMic">打开麦克风</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="接口：EnableSpeaker">打开扬声器</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="接口：ExitRoom">退出语音房间</dx-tag-link>
-<dx-tag-link link="#UnInit" tag="接口：UnInit">反初始化 GME</dx-tag-link>
</dx-steps>

### 实时语音功能 Android 类

| 类                  |        含义        |
| ------------------- | :----------------: |
| ITMGContext         |      核心接口      |
| ITMGRoom            |    房间相关接口    |
| ITMGRoomManager     |    房间管理接口    |
| ITMGAudioCtrl       |    音频相关接口    |
| ITMGAudioEffectCtrl | 音效及伴奏相关接口 |

## 核心接口

| 接口   |   接口含义   |
| ------ | :----------: |
| Init   |  初始化 GME  |
| Poll   | 触发事件回调 |
| Pause  |   系统暂停   |
| Resume |   系统恢复   |
| Uninit | 反初始化 GME |



<dx-alert infotype="notice" title="">
如果切换账号，请调用 UnInit 反初始化 SDK。Init 接口调用不会产生计费。
</dx-alert>






### 获取单例

在使用语音功能时，需要首先获取 ITMGContext 对象。

#### 示例代码  

```java
import com.tencent.TMG.ITMGContext; 
ITMGContext.getInstance(this);
```

### 注册回调

接口类采用 Delegate 方法用于向应用程序发送回调通知。将回调函数注册给 SDK，用于接收回调的信息。

#### 接口原型

```java
static public abstract class ITMGDelegate {
    public void OnEvent(ITMG_MAIN_EVENT_TYPE type, Intent data){}
}
```

在构造函数中重写这个回调函数，对回调的参数进行处理。

| 参数 |               类型               | 含义                     |
| ---- | :------------------------------: | ------------------------ |
| type | ITMGContext.ITMG_MAIN_EVENT_TYPE | 回调的事件类型           |
| data |         Intent 消息类型          | 回调的相关信息，事件数据 |



#### 示例代码  

```java
private ITMGContext.ITMGDelegate itmgDelegate = null;
itmgDelegate = new ITMGContext.ITMGDelegate() {
    @Override
    public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
        if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM == type)
        {
            //对事件返回的 Data 进行解析
            int nErrCode = data.getIntExtra("result" , -1);
            String strErrMsg = data.getStringExtra("error_info");
				}
		}
}
```

将回调函数注册给 SDK，要在进房之前设置。

#### 接口原型

```java
public abstract int SetTMGDelegate(ITMGDelegate delegate);
```

| 参数     |     类型     | 含义         |
| -------- | :----------: | ------------ |
| delegate | ITMGDelegate | SDK 回调函数 |

#### 示例代码  

```java
ITMGContext.GetInstance(this).SetTMGDelegate(itmgDelegate);
```


### [初始化 SDK](id:Init)

未初始化前，SDK 处于未初始化阶段，**需要通过接口 Init 初始化 SDK**，才可以使用实时语音服务、语音消息服务及转文本服务，**启动后会收集个人信息**。调用 Init 接口的线程必须于其他接口在同一线程,建议都在主线程调用接口。

<dx-alert infotype="alarm" title="注意">
确保在用户阅读 APP 隐私政策并取得用户授权之后，按 APP 功能需要在合适时机调用正式初始化函数 Init 初始化 SDK。反之，如果用户不同意《隐私政策》授权，则不能调用正式初始化函数。
</dx-alert>

#### 接口原型

```java
public abstract int Init(String sdkAppId, String openId);
```

| 参数     |  类型  | 含义                                                         |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | String |来自 [腾讯云控制台](https://console.cloud.tencent.com/gamegme) 的 GME 服务提供的 AppID，获取请参考 [语音服务开通指引](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0) |
| OpenId   | String |openID 只支持 Int64 类型（转为 const char* 传入）。 规则由 App 开发者自行制定，App 内不重复即可。如需使用字符串作为 Openid 传入，可 [通过工单](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1) 联系开发者。         |

#### 返回值

| 返回值                          | 处理                                          |
| ------------------------------- | --------------------------------------------- |
| QAVError.OK= 0                  | 初始化 SDK 成功                               |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | 检查 SDK 文件是否完整，建议删除后重新导入 SDK |

<dx-alert infotype="notice" title="关于7015错误提示">
- 7015错误码是通过 md5 进行判断，在接入过程中若出现此错误，请根据提示检查 SDK 文件是否完整、SDK 文件版本是否一致。
- 出现返回值 AV_ERR_SDK_NOT_FULL_UPDATE 时，此返回值**只有提示作用**，并不会造成初始化失败。
- 由于第三方加固、Unity 打包机制等因素会影响库文件 md5，造成误判，所以**正式发布请在逻辑中忽略此错误**，并尽量不在 UI 中提示。
</dx-alert>


#### 示例代码 

```java
String sdkAppID = "14000xxxxx";
String openID = "100";
int ret = 0;
//在用户同意APP隐私政策之后，按APP功能需要在合适时机再正式初始化SDK
//ret = 0，表示用户同意APP隐私合规政策
//ret = 1，表示用户不同意APP隐私合规政策
//如果用户不授权隐私策略，则 ret 修改为非 0 
if(ret != 0){
    Log.e(TAG,"用户不同意APP隐私合规政策");
}else{
		ITMGContext.GetInstance(this).Init(sdkAppId, openId);
}
```


### [触发事件回调](id:Poll)

通过在 update 里面周期的调用 Poll 可以触发事件回调。Poll 是 GME 的消息泵，GME 需要周期性的调用 Poll 接口触发事件回调。如果没有调用 Poll ，将会导致整个 SDK 服务运行异常。
可参考 [Demo](https://intl.cloud.tencent.com/document/product/607/18521) 中的 EnginePollHelper.java 文件。

<dx-alert infotype="alarm" title="务必周期性调用 Poll 接口">
务必周期性调用 Poll 接口且在主线程调用，以免接口回调异常。
</dx-alert>

#### 接口原型

```java
public abstract int Poll();
```

#### 示例代码

```java
private Handler mhandler = new Handler();private Runnable mRunnable = new Runnable() {    @Override    public void run() {        if (s_pollEnabled) {            if (ITMGContext.GetInstance(null) != null)                ITMGContext.GetInstance(null).Poll();        }        mhandler.postDelayed(mRunnable, 33);    }};
```

### 系统暂停

当系统发生 Pause 事件时，需要同时通知引擎进行 Pause。如果不需要后台播放房间内声音，请调用 Pause 接口暂停整个 GME 服务。

#### 接口原型

```java
public abstract int Pause();
```

### 系统恢复

当系统发生 Resume 事件时，需要同时通知引擎进行 Resume。Resume 接口只恢复实时语音。

#### 接口原型

```java
public abstract int Resume();
```

### [反初始化 SDK](id:UnInit)

反初始化 SDK，进入未初始化状态。**如果游戏业务侧账号与 openid 是绑定的，那切换游戏账号需要反初始化 GME，再用新的 openid 初始化**。


<dx-alert infotype="notice" title="注意">
终端用户撤销同意处理其个人信息的授权时，您可通过调用 Uninit 接口停止使用SDK功能并停止采集与关闭功能相应的用户数据。
</dx-alert>




#### 接口原型

```java
public abstract int Uninit();
```

## 实时语音房间相关接口

初始化之后，SDK 调用进房后进去了房间，才可以进行实时语音通话。
使用问题可参考 [实时语音相关问题](https://intl.cloud.tencent.com/document/product/607/39524)。

![](https://qcloudimg.tencent-cloud.cn/raw/02f98895d0b7bfe1bac774d5983289c1.jpg)

| 接口          |       接口含义       |
| ------------- | :------------------: |
| GenAuthBuffer |     本地鉴权计算     |
| EnterRoom     |       加入房间       |
| ExitRoom      |       退出房间       |
| IsRoomEntered | 判断是否已经进入房间 |
| SwitchRoom    |     快速切换房间     |
|StartRoomSharing |跨房连麦|

### 本地鉴权计算

生成 AuthBuffer，用于相关功能的加密和鉴权，如正式发布请使用后台部署密钥，后台部署请参考 [鉴权密钥](https://intl.cloud.tencent.com/document/product/607/12218)。    

#### 接口原型

```java
AuthBuffer public native byte[] genAuthBuffer(int sdkAppId, String roomId, String openId, String key)
```

| 参数          | 类型  | 含义                                                         |
| ------ | :----: | ------------------------------------------------------------ |
| appId  |  int   | 来自腾讯云控制台的 AppId 号码。                              |
| roomId | string | 房间号，最大支持127字符。                                    |
| openId | string | 用户标识。与 Init 时候的 OpenId相同。                        |
| key    | string | 来自腾讯云 [控制台](https://console.cloud.tencent.com/gamegme) 的权限密钥。 |



#### 示例代码  

```java
import com.tencent.av.sig.AuthBuffer;//头文件
byte[] authBuffer = AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(sdkAppId), strRoomID,openId, key);
```

[](id:EnterRoom)
### 加入房间

用生成的鉴权信息进房，加入房间默认不打开麦克风及扬声器。
<dx-alert infotype="notice" title="注意">
- 加入房间事件回调结果 result 为 0 代表进房成功，进房接口 EnterRoom 返回值为 0 不代表进房成功。
- 房间的音频类型由第一个进房的人确定，此后房间里有成员修改房间类型，将对此房间所有成员生效。例如第一个进入房间的人使用的房间音频类型是流畅音质，第二个进房的是即使进房时候调用接口的音频类型参数是高清音质，进入房间之后也会变成流畅音质。需要有成员调用 ChangeRoomType 才会修改房间的音频类型。
</dx-alert>

#### 接口原型

```java
public abstract int EnterRoom(String roomID, int roomType, byte[] authBuffer);
```

| 参数       |  类型  | 含义                    |
| ---------- | :----: | ----------------------- |
| roomId     | String | 房间号，最大支持127字符 |
| roomType   |  int   | 房间类型，建议填 ITMG_ROOM_TYPE_FLUENCY 。房间音频类型请参考 [音质选择](https://intl.cloud.tencent.com/document/product/607/18522)。             |
| authBuffer | byte[] | 鉴权码                  |


#### 示例代码  

```java
ITMGContext.GetInstance(this).EnterRoom(roomId,roomType, authBuffer);    
```

#### 加入房间的事件回调

加入房间完成后会发送信息 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM，在 OnEvent 函数中进行判断回调后处理。如果回调为成功，即此时进房成功，开始进行**计费**。

<dx-fold-block title="计费问题参考">
[购买指南。](https://intl.cloud.tencent.com/document/product/607/50009)
[计费相关问题。](https://intl.cloud.tencent.com/document/product/607/30255)
[使用实时语音后，如果客户端掉线了，是否还会继续计费？](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)
</dx-fold-block>

#### 函数原型

```java
private ITMGContext.ITMGDelegate itmgDelegate = null;
itmgDelegate= new ITMGContext.ITMGDelegate() {
            @Override
 			public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
                }
};
```



#### 示例代码  

回调处理相关参考代码，包括加入房间事件以及断网事件。

```java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM == type)
        {
           	//对事件返回的 Data 进行解析
            int nErrCode = data.getIntExtra("result" , -1);
            String strErrMsg = data.getStringExtra("error_info");

            if (nErrCode == AVError.AV_OK)
            {
                //收到进房信令，进房成功，可以操作设备
                ScrollView_ShowLog("EnterRoom success");
                Log.i(TAG,"EnterRoom success!");
            }
            else
            {
                //进房失败，需分析返回的错误信息
                ScrollView_ShowLog("EnterRoom fail :" + strErrMsg);
                Log.i(TAG,"EnterRoom fail!");
            }  
        }
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT == type)
        {
			//waiting timeout, please check your network
		}
	}
```

#### Data 详情

| 消息                                 |        Data        | 例子                                                         |
| ------------------------------------ | :----------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM      | result; error_info | {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | result; error_info | {"error_info":"waiting timeout, please check your network","result":0} |

如果断网，将会有断网的回调提示 `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT`，此时 SDK 会自动进行重连，回调是  `ITMG_MAIN_EVENT_TYPE_RECONNECT_START`，当重连成功时，会有 `ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS` 回调。

#### 错误码

| 错误码值 | 原因及建议方案                                               |
| -------- | ------------------------------------------------------------ |
| 7006     | 鉴权失败原因。<li>AppID 不存在或者错误<li>authbuff 鉴权错误<li>鉴权过期 <li>OpenId 不符合规范 |
| 7007     | 已经在其它房间                                               |
| 1001     | 已经在进房过程中，然后又重复了此操作。建议在进房回调返回之前不要再调用进房接口 |
| 1003     | 已经进房了在房间中，又调用一次进房接口                       |
| 1101     | 确保已经初始化 SDK，确保 OpenId 是否符合规则，或者确保在同一线程调用接口，以及确保 Poll 接口正常调用 |


[](id:ExitRoom)	
### 退出房间

通过调用此接口可以退出所在房间。这是一个异步接口，返回值为 AV_OK 的时候代表异步投递成功。如果应用中有退房后立即进房的场景，在接口调用流程上，开发者无需要等待 ExitRoom 的回调 RoomExitComplete 通知，只需直接调用接口。

#### 接口原型  

```java
public abstract int ExitRoom();
```

#### 示例代码  

```java
ITMGContext.GetInstance(this).ExitRoom();
```

#### 退出房间事件回调

退出房间完成后会有回调，消息为 ITMG_MAIN_EVENT_TYPE_EXIT_ROOM。

#### 示例代码  

```java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM == type)
        {
            //收到退房成功事件
        }
}
```
#### Data详情

| 消息                           |        Data        | 例子                         |
| ------------------------------ | :----------------: | ---------------------------- |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM | result; error_info | {"error_info":"","result":0} |

### 判断是否已经进入房间

通过调用此接口可以判断是否已经进入房间，返回值为 bool 类型。请勿在进房过程中调用。

#### 接口原型  

```java
public abstract boolean IsRoomEntered();
```

#### 示例代码  

```java
ITMGContext.GetInstance(this).IsRoomEntered();
```

### 快速切换房间

调用此接口快速切换实时语音房间。此接口在进房后调用。切换房间后，不重置设备，即如果在此房间已经是打开麦克风状态，在切换房间后也会是打开麦克风状态。
快速切换房间的回调是 ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_SWITCH_ROOM，字段是 error_info 以及 result。

#### 接口原型

```java
public abstract int SwitchRoom(String targetRoomID, byte[] authBuffer);
```

#### 类型说明

| 参数         | 类型   | 含义                           |
| ------------ | ------ | ------------------------------ |
| targetRoomID | String | 将要进入的房间号               |
| authBuffer   | byte[] | 用将要进入的房间号生成的新鉴权 |

#### 回调示例代码

```java
if(ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_SWITCH_ROOM == type) {    
int result = data.getIntExtra("result", 1);    
String errorInfo = data.getStringExtra("error_info");         
if (result == 0) {              
			Toast.makeText(getActivity(), "switch room success.", Toast.LENGTH_SHORT).show();     
			} 
else {              
			Toast.makeText(getActivity(), "switch room failed.. error info=" + errorInfo, Toast.LENGTH_SHORT).show();         
			}
}
```


### 跨房连麦

调用此接口进行跨房连麦，此接口在进房后调用。调用接口后，本端可以与目标房间的目标 OpenID 用户进行连麦交流。目标房间与本端房间类型相同才能成功。

#### 场景示例
a 用户在 A 房间中，b 用户在 B 房间中，a 用户可以通过跨房接口与 b 进行通话，A 房间中的用户 c 说话，B 房间的 b 与 d 无法听到；A 房间中的用户 c 只能听到 A 房间的声音以及 B 房间中 b 的声音，B 房间其他人说话 c 无法听到。

#### 接口原型

```java
/// <summary> 开启房间共享，与另外的房间中的OpenID进行连麦</summary>
public abstract int StartRoomSharing(String targetRoomID, String targetOpenID, byte[] authBuffer);
/// <summary> 结束已经开启的房间共享</summary>
public abstract int StopRoomSharing();
```

#### 类型说明

| 参数         | 类型   | 含义                    |
| ------------ | ------ | ----------------------- |
| targetRoomID | String | 将要连麦的房间号        |
| targetOpenID | String | 将要连麦的目标 OpenID   |
| authBuffer   | byte[] | 保留标志位，只需填 NULL |

#### 示例代码

```java
if (mSwtichRoomShareStart.isChecked())
    {
        String strRoomID = mEditRoomShareRoomID.getText().toString();
        String strOpenID = mEditRoomShareOpenID.getText().toString();
        int nRet = ITMGContext.GetInstance(getActivity()).GetRoom().StartRoomSharing(strRoomID, strOpenID, null);
        if (nRet != 0)
            {
                Toast.makeText(getActivity(), String.format("StartRoomSharing failed nRet=" + nRet), Toast.LENGTH_SHORT).show();
            }else
            {
                int nRet = ITMGContext.GetInstance(getActivity()).GetRoom().StopRoomSharing();
                    if (nRet != 0)
                        {
                            Toast.makeText(getActivity(), String.format("StopRoomSharing failed nRet=" + nRet), Toast.LENGTH_SHORT).show();
                        }
                }
}
```

## 房间内状态维护

此部分接口用于业务层显示说话成员、进退房成员，以及将房间内某成员禁言等功能。

![](https://main.qcloudimg.com/raw/33eecfcd9e18a361aa0b732ffd0fb7dd.png)

| 接口/通知                        |       含义       |
| -------------------------------- | :--------------: |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | 成员状态变化通知 |
| AddAudioBlackList                | 房间中禁言某成员 |
| RemoveAudioBlackList             |     移除禁言     |

### 成员进房、说话状态通知


此接口适用于获取房间中说话的人并在 UI 中展示，以及有人进入、退出语音房间的一个通知。
该事件在状态变化才通知，状态不变化的情况下不通知。如需实时获取成员状态，请在上层收到通知时缓存，事件消息为 ITMG_MAIN_EVNET_TYPE_USER_UPDATE，其中 data 包含两个信息，event_id 及 user_list，在 OnEvent 函数中对事件消息进行判断。
音频事件的通知有一个阈值，超过这个阈值才会发送通知。超过两秒没有收到音频包才通知“有成员停止发送音频包”消息。

| event_id                     |                             含义                             | 应用侧维护内容         |
| ---------------------------- | :----------------------------------------------------------: | ---------------------- |
| ITMG_EVENT_ID_USER_ENTER     |                     有成员进入房间，返回此时进房的 openid                       | 应用侧维护成员列表     |
| ITMG_EVENT_ID_USER_EXIT      |                 有成员退出房间，返回此时退房的 openid           | 应用侧维护成员列表     |
| ITMG_EVENT_ID_USER_HAS_AUDIO | 有成员发送音频包，返回此时房间内说话的 openid，通过此事件可以判断用户是否说话，并展示声纹效果  | 应用侧维护通话成员列表 |
| ITMG_EVENT_ID_USER_NO_AUDIO  |                     有成员停止发送音频包，返回此时房间内停止说话的 openid                     | 应用侧维护通话成员列表 |

#### 示例代码

```java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_USER_UPDATE == type)
        {
		//更新成员状态
		int nEventID = data.getIntExtra("event_id", 0);
		String[] openIdList =data.getStringArrayExtra("user_list");
		 switch (nEventID)
 		    {
					case ITMG_EVENT_ID_USER_ENTER:
  			    //有成员进入房间
  			    break;
					case ITMG_EVENT_ID_USER_EXIT:
  			    //有成员退出房间
						break;
					case ITMG_EVENT_ID_USER_HAS_AUDIO:
						//有成员发送音频包
						break;
					case ITMG_EVENT_ID_USER_NO_AUDIO:
						//有成员停止发送音频包
						break;
					default:
						break;
 		    }
		}
}
```

#### Data 详情

| 消息                             |        Data         | 例子                          |
| -------------------------------- | :-----------------: | ----------------------------- |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | event_id; user_list | {"event_id":0,"user_list":""} |


### 房间中禁言某成员

将某个 ID 加入音频数据黑名单，即不接受某人的语音， 只对本端生效，不会影响其他端。返回值为 0 表示调用成功。例如 ：A、B、C 都在同一个房间开麦说话： 

- 如果 A 设置了 C 的黑名单， 则 A 只能听见 B 的声音。
- B 因为没有设置黑名单， 仍旧可以听见 A 和 C 的声音。
- C 同样因为没有设置黑名单， 可以听见 A 和 B 的声音。

此接口适用于在语音房间中将某用户禁言的场景。

#### 接口原型  

```java
public abstract int AddAudioBlackList(String openId);
```

| 参数   |  类型  | 含义              |
| ------ | :----: | ----------------- |
| openId | String | 需添加黑名单的用户 openid |

#### 示例代码  

```java
ITMGContext.GetInstance(this).GetAudioCtrl().AddAudioBlackList(openId);
```

### 移除禁言

将某个 Id 移除音频数据黑名单。返回值为0表示调用成功。

#### 接口原型  

```java
public abstract int RemoveAudioBlackList(String openId);
```

| 参数   | 类型  | 含义              |
| ------ | :----: | ----------------- |
| openId | String | 需移除黑名单的用户 openid |

#### 示例代码  

```java
ITMGContext.GetInstance(this).GetAudioCtrl().RemoveAudioBlackList(openId);
```



## 实时语音采集相关接口

- 初始化 SDK 之后进房，在房间中，才可以调用实时音频语音相关接口。
- 当用户界面单击打开/关闭麦克风/扬声器按钮时，建议采用 EnableMic 以及 EnableSpeaker 接口进行调用。
- 当用户进入实时语音房间，打开或者关闭采集设备，会伴随整个设备（采集及播放）重启，如果此时 App 正在播放背景音乐，那么背景音乐的播放也会被中断。利用控制上下行的方式来实现开关麦克风效果，不会中断播放设备。**具体调用方式为：在进房的时候调用 EnableAudioCaptureDevice(true) && EnableAudioPlayDevice(true) 一次，单击开关麦克风时只调用 EnableAudioSend/Recv 来控制音频流是否发送/接收**。


| 接口                        |       接口含义       |
| --------------------------- | :------------------: |
| EnableMic                   |      开关麦克风      |
| GetMicState                 |    获取麦克风状态    |
| EnableAudioCaptureDevice    |     开关采集设备     |
| IsAudioCaptureDeviceEnabled |   获取采集设备状态   |
| EnableAudioSend             |   打开关闭音频上行   |
| IsAudioSendEnabled          |   获取音频上行状态   |
| GetMicLevel                 |  获取实时麦克风音量  |
| GetSendStreamLevel          | 获取音频上行实时音量 |
| SetMicVolume                |    设置麦克风音量    |
| GetMicVolume                |    获取麦克风音量    |


[](id:EnableMic)	
### 开启或关闭麦克风

此接口用来开启关闭麦克风。加入房间默认不打开麦克风及扬声器。**EnableMic = EnableAudioCaptureDevice + EnableAudioSend**
**如果有使用伴奏的情况，请参考 [实时语音伴奏流程图](https://intl.cloud.tencent.com/document/product/607/31504) 进行调用。**

#### 接口原型  

```java
public abstract int EnableMic(boolean isEnabled);
```

| 参数     | 类型 | 含义                                                         |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled | boolean | 如果需要打开麦克风，则传入的参数为 true，如果关闭麦克风，则参数为 false |

#### 示例代码  

```
//打开麦克风
ITMGContext.GetInstance(this).GetAudioCtrl().EnableMic(true);
```

### 麦克风状态获取

此接口用于获取麦克风状态，返回值0为关闭麦克风状态，返回值1为打开麦克风状态。

#### 接口原型  

```
public abstract int GetMicState();
```

#### 示例代码  

```
int micState = ITMGContext.GetInstance(this).GetAudioCtrl().GetMicState();
```

### 开启或关闭采集设备

此接口用来开启/关闭采集设备。加入房间默认不打开设备。

- 只能在进房后调用此接口，退房会自动关闭设备。
- 在移动端，打开采集设备通常会伴随权限申请，音量类型调整等操作。

#### 接口原型  

```
public abstract int EnableAudioCaptureDevice(boolean isEnabled);
```

| 参数      |  类型   | 含义                                                         |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled | boolean | 如果需要打开采集设备，则传入的参数为 true，如果关闭采集设备，则参数为 false |

#### 示例代码

```
//打开采集设备
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### 采集设备状态获取

此接口用于采集设备状态获取。

#### 接口原型

```
public abstract boolean IsAudioCaptureDeviceEnabled();
```

#### 示例代码

```
bool IsAudioCaptureDevice = ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### 打开或关闭音频上行

此接口用于打开/关闭音频上行。如果采集设备已经打开，那么会发送采集到的音频数据。如果采集设备没有打开，那么仍旧无声。采集设备的打开关闭请参见接口 EnableAudioCaptureDevice。

#### 接口原型

```
public abstract int EnableAudioSend(boolean isEnabled);
```

| 参数      |  类型   | 含义                                                         |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled | boolean | 如果需要打开音频上行，则传入的参数为 true，如果关闭音频上行，则参数为 false |

#### 示例代码  

```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioSend(true);
```

### 音频上行状态获取

此接口用于音频上行状态获取。

#### 接口原型  

```
public abstract boolean IsAudioSendEnabled();
```

#### 示例代码  

```
bool IsAudioSend = ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioSendEnabled();
```

### 获取麦克风实时音量

此接口用于获取麦克风实时音量，返回值为 int 类型。建议20ms获取一次。值域为0 - 100，通过此接口可以获取到麦克风采集到的实时音量情况。

 

#### 接口原型  

```
public abstract int GetMicLevel();
```

#### 示例代码  

```
int micLevel = ITMGContext.GetInstance(this).GetAudioCtrl().GetMicLevel();
```

### 获取音频上行实时音量

此接口用于获取自己音频上行实时音量，返回值为 int 类型，取值范围为0 - 100。

 

#### 接口原型  

```
ITMGContext TMGAudioCtrl int GetSendStreamLevel()
```

#### 示例代码  

```
int Level = ITMGContext.GetInstance(this).GetAudioCtrl().GetSendStreamLevel();
```

### 设置麦克风软件音量

此接口用于设置麦克风的音量。参数 volume 用于设置麦克风的音量，相当于对采集的声音做衰减或增益。

 

#### 接口原型  

```
public abstract int SetMicVolume(int volume);
```

| 参数   | 类型 | 含义                                                         |
| ------ | :--: | ------------------------------------------------------------ |
| volume  | int  | 取值范围为 0-200，数值为0的时候表示静音，当数值为100的时候表示音量不增不减，默认数值为100。 |

#### 示例代码  

```
ITMGContext.GetInstance(this).GetAudioCtrl().SetMicVolume(volume);
```

### 获取麦克风软件音量

此接口用于获取麦克风的音量。返回值为一个int类型数值，返回值为101代表没调用过接口 SetMicVolume。

 

#### 接口原型  

```
public abstract int GetMicVolume();
```

#### 示例代码  

```
ITMGContext.GetInstance(this).GetAudioCtrl().GetMicVolume();
```

## 实时语音播放相关接口

| 接口                     |            接口含义            |
| ------------------------ | :----------------------------: |
| EnableSpeaker            |           开关扬声器           |
| GetSpeakerState          |         获取扬声器状态         |
| EnableAudioPlayDevice    |          开关播放设备          |
| IsAudioPlayDeviceEnabled |        获取播放设备状态        |
| EnableAudioRecv          |        打开关闭音频下行        |
| IsAudioRecvEnabled       |        获取音频下行状态        |
| GetSpeakerLevel          |       获取实时扬声器音量       |
| GetRecvStreamLevel       | 获取房间内其他成员下行实时音量 |
| SetSpeakerVolume         |         设置扬声器音量         |
| GetSpeakerVolume         |         获取扬声器音量         |

### [开启或关闭扬声器](id:EnableSpeaker)

此接口用于开启关闭扬声器。**EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv**
**如果有使用伴奏的情况，请参考 [实时语音伴奏流程图](https://intl.cloud.tencent.com/document/product/607/31504) 进行调用。**

#### 接口原型  

```
public abstract int EnableSpeaker(boolean isEnabled);
```

| 参数      | 类型 | 含义                                                         |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled | boolean | 如果需要关闭扬声器，则传入的参数为 false，如果打开扬声器，则参数为 true |

#### 示例代码  

```
//打开扬声器
ITMGContext.GetInstance(this).GetAudioCtrl().EnableSpeaker(true);
```

### 扬声器状态获取

此接口用于扬声器状态获取。返回值0为关闭扬声器状态，返回值1为打开扬声器状态。

#### 接口原型  

```
public abstract int GetSpeakerState();
```

#### 示例代码  

```
int micState = ITMGContext.GetInstance(this).GetAudioCtrl().GetSpeakerState();
```



### 开启或关闭播放设备

此接口用于开启关闭播放设备。

#### 接口原型  

```
public abstract int EnableAudioPlayDevice(boolean isEnabled);
```

| 参数      | 类型 | 含义                                                         |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled | boolean | 如果需要关闭播放设备，则传入的参数为 false，如果打开播放设备，则参数为 true |

#### 示例代码  

```
//打开播放设备
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioPlayDevice(true);
```

### 播放设备状态获取

此接口用于播放设备状态获取。

#### 接口原型

```
public abstract boolean IsAudioPlayDeviceEnabled();
```

#### 示例代码  

```
bool IsAudioPlayDevice = ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### 打开或关闭音频下行

此接口用于打开/关闭音频下行。如果播放设备已经打开，那么会播放房间里其他人的音频数据。如果播放设备没有打开，那么仍旧无声。播放设备的打开关闭参见接口请参见 EnableAudioPlayDevice。

#### 接口原型  

```
public abstract int EnableAudioRecv(boolean isEnabled);
```

| 参数      |  类型   | 含义                                                         |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled | boolean | 如果需要打开音频下行，则传入的参数为 true，如果关闭音频下行，则参数为 false |

#### 示例代码  

```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableAudioRecv(true);
```



### 音频下行状态获取

此接口用于音频下行状态获取。

#### 接口原型  

```
public abstract boolean IsAudioRecvEnabled();
```

#### 示例代码  

```
bool IsAudioRecv = ITMGContext.GetInstance(this).GetAudioCtrl().IsAudioRecvEnabled();
```

### 获取扬声器实时音量

此接口用于获取扬声器实时音量。返回值为 int 类型数值，表示扬声器实时音量。建议20ms获取一次。

#### 接口原型  

```
public abstract int GetSpeakerLevel();
```

#### 示例代码  

```
int SpeakLevel = ITMGContext.GetInstance(this).GetAudioCtrl().GetSpeakerLevel();
```

### 获取房间内其他成员下行实时音量

此接口用于获取房间内其他成员下行实时音量，返回值为 int 类型，取值范围为0 - 200。

#### 接口原型  

```
public abstract int GetRecvStreamLevel(String openId);
```

| 参数   |  类型  | 含义                 |
| ------ | :----: | -------------------- |
| openId | string | 房间其他成员的 openId |

#### 示例代码  

```
int Level = ITMGContext.GetInstance(this).GetAudioCtrl().GetRecvStreamLevel(openId);
```

### 动态设置房间内某成员音量

此接口用于设置房间内某成员的说话音量大小，此设置只在本端生效。

#### 接口原型  

```
public abstract int SetSpeakerVolumeByOpenID(String openId, int volume);
```

|参数   |类型   |含义   |
|----------|-------|-------|
|openId       |String *   |需要调节音量大小的OpenID|
|volume  |int        |百分比，建议[0-200]，其中100为默认值|

#### 示例代码

**执行语句**

```
// 将123333的声音压低到现在声音的80%
String strOpenID = "1233333";
int nOpenVolume = Integer.valueOf(80);
int nRet = ITMGContext.GetInstance(getActivity()).GetAudioCtrl().SetSpeakerVolumeByOpenID(strOpenID, nOpenVolume);
if (nRet != 0)
{
  // Toast error occured
}
else
{
  // Toast set successfully
}
```

### 获取设置的声音百分比

调用此接口获取SetSpeakerVolumeByOpenID设置的能量值

#### 接口原型

```
public abstract int GetSpeakerVolumeByOpenID(String openId);
```

|参数   |类型   |含义   |
|----------|-------|-------|
|openId       |String *   |需要调节音量大小的OpenID|


#### 返回值

接口返回 OpenID 设置的能量百分比， 默认返回100。

### 设置扬声器的音量

此接口用于设置扬声器的音量。

#### 接口原型  

```
public abstract int SetSpeakerVolume(int volume);
```

| 参数   | 类型 | 含义                 |
| ------ | :--: | -------------------- |
| volume | int  | 设置音量，范围0 - 200，当数值为0时，表示静音，当数值为100时，表示音量不增不减，默认数值为100。|

#### 示例代码  

```
int speVol = (int)(value * 100);ITMGContext.GetInstance(this).GetAudioCtrl().SetSpeakerVolume(volume);
```

### 获取扬声器的音量

此接口用于获取扬声器的音量。返回值为 int 类型数值，代表扬声器的音量，返回值为101代表没调用过接口 SetSpeakerVolume。
Level 是实时音量，Volume 是扬声器的音量，最终声音音量 =  Level × Volume %。例如实时音量是数值是100，此时 Volume 的数值是60，那么最终发出来的声音数值也是60。

#### 接口原型  

```
public abstract int GetSpeakerVolume();
```

#### 示例代码  

```
ITMGContext.GetInstance(this).GetAudioCtrl().GetSpeakerVolume();
```




## 高级 API

### 启动耳返

此接口用于启动耳返，需要 `EnableLoopBack + EnableSpeaker` 才可以听到自己声音。

#### 接口原型  

```
public abstract int EnableLoopBack(boolean enable);
```

| 参数   |  类型   | 含义         |
| ------ | :-----: | ------------ |
| enable | boolean | 设置是否启动 |

#### 示例代码  

```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableLoopBack(true);
```

### 获取用户房间音频类型

此接口用于获取用户房间音频类型，返回值为房间音频类型，返回值为0时代表获取用户房间音频类型发生错误，房间音频类型参考 EnterRoom 接口。

#### 接口原型  

```java
public abstract int GetRoomType();
```

#### 示例代码  

```java
ITMGContext.GetInstance(this).GetRoom().GetRoomType();
```

### 获取房间号
此接口用于获取实时语音房间号，只能在进房成功之后使用。返回值为 string 字符串。

#### 接口原型  

```
public abstract String GetRoomID();
```



### 修改用户房间音频类型

此接口用于修改用户房间音频类型，结果参见回调事件，事件类型为 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE。房间的音频类型由第一个进房的人确定，此后房间里有成员修改房间类型，将对此房间所有成员生效。

#### 接口原型  

```java
public abstract int ChangeRoomType(int nRoomType);
```

| 参数      | 类型 | 含义                                                  |
| --------- | :--: | ----------------------------------------------------- |
| nRoomType | int  | 房间切换成的目标类型，房间音频类型参考 EnterRoom 接口 |

#### 示例代码  

```java
ITMGContext.GetInstance(this).GetRoom().ChangeRoomType(nRoomType);
```

### 房间类型修改回调

房间类型设置完成后，回调的事件消息为 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE，返回的参数为 result、error_info 及 new_room_type，new_room_type 代表的信息如下，在 OnEvent 函数中对事件消息进行判断。

| 事件子类型                       | 代表参数 | 含义                                                         |
| -------------------------------- | :------: | ------------------------------------------------------------ |
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM |    1     | 表示在进房的过程中，自带的音频类型与房间不符合，被修改为所进入房间的音频类型。 |
| ITMG_ROOM_CHANGE_EVENT_START     |    2     | 表示已经在房间内，音频类型开始切换（例如调用 ChangeRoomType 接口后切换音频类型）。 |
| ITMG_ROOM_CHANGE_EVENT_COMPLETE  |    3     | 表示已经在房间，音频类型切换完成。                             |
| ITMG_ROOM_CHANGE_EVENT_REQUEST   |    4     | 表示房间成员调用 ChangeRoomType 接口，请求切换房间音频类型。   |

#### 示例代码  

```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE == type)        {		//对房间类型事件进行处理	 }}
```

#### Data 详情

| 消息                                  |                     Data                     | 例子                                                         |
| ------------------------------------- | :------------------------------------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE | result;error_info;new_room_type;subEventType | {"error_info":"","new_room_type":0,"subEventType":0,"result":0} |

### 房间通话质量监控事件

质量监控事件，在进房后触发，2秒回调一次，事件消息为 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY，返回的参数为 weight、loss 及 delay，代表的信息如下：

| 参数   | 类型   | 含义                                                         |
| ------ | ------ | ------------------------------------------------------------ |
| weight | int    | 范围是1 - 50，数值为50是音质评分极好，数值为1是音质评分很差，几乎不能使用，数值为0代表初始值，无含义。一般数值在30以下就可以提醒用户网络较差，建议切换网络。 |
| loss   | double | 上行丢包率。                                                 |
| delay  | int    | 音频触达延迟时间（ms）。                                     |

### 获取版本号

获取 SDK 版本号，用于分析。

#### 接口原型

```
public abstract String GetSDKVersion();
```

#### 示例代码  

```
ITMGContext.GetInstance(this).GetSDKVersion();
```

### 检查麦克风权限

返回麦克风权限状态。

#### 函数原型

```
public abstract ITMG_RECORD_PERMISSION  CheckMicPermission();
```

#### 参数含义

| 参数                          | 数值 | 含义                         |
| ----------------------------- | ---- | ---------------------------- |
| ITMG_PERMISSION_GRANTED       | 0    | 麦克风已授权                 |
| ITMG_PERMISSION_Denied        | 1    | 麦克风被禁用                 |
| ITMG_PERMISSION_NotDetermined | 2    | 尚未弹出权限框向用户申请权限 |
| ITMG_PERMISSION_ERROR         | 3    | 接口调用错误                 |

#### 示例代码  

```
ITMGContext.GetInstance(this).CheckMicPermission();
```

### 检查麦克风设备状态


#### 函数原型

```
public abstract ITMG_CHECK_MIC_STATUS CheckMic();
```

#### 返回值处理

| 返回值                               | 含义                | 处理                                                         |
| ------------------------------------ | ------------------- | ------------------------------------------------------------ |
| ITMG_CHECK_MIC_STATUS_AVAILABLE = 0   | 正常可用            | 无需处理                                                     |
| ITMG_CHECK_MIC_STATUS_NO_GRANTED = 2  | 未获得/拒绝授权权限 | 需要在打开麦克风之前获取下权限                               |
| ITMG_CHECK_MIC_STATUS_INVALID_MIC = 3 | 没有可用的设备      | 一般是 PC 设备上，没有可用的麦克风设备会报此错误，请提示插入耳机或麦克风 |
| ITMG_CHECK_MIC_STATUS_NOT_INIT = 5    | 没有初始化          | 在Init之后调用 EnableMic 接口                                |

### 设置打印日志等级

用于设置打印日志等级。建议保持默认等级。需要在 Init 之前调用。

#### 接口原型

```
public abstract int SetLogLevel(int levelWrite, int levelPrint);
```

#### 参数含义

| 参数       | 类型           | 含义                                                         |
| ---------- | -------------- | ------------------------------------------------------------ |
| levelWrite | ITMG_LOG_LEVEL | 设置写入日志的等级，TMG_LOG_LEVEL_NONE 表示不写入，默认为 TMG_LOG_LEVEL_INFO |
| levelPrint | ITMG_LOG_LEVEL | 设置打印日志的等级，TMG_LOG_LEVEL_NONE 表示不打印，默认为 TMG_LOG_LEVEL_ERROR |

ITMG_LOG_LEVEL 说明如下：

| ITMG_LOG_LEVEL        | 含义                 |
| --------------------- | -------------------- |
| TMG_LOG_LEVEL_NONE    | 不打印日志           |
| TMG_LOG_LEVEL_ERROR   | 打印错误日志（默认） |
| TMG_LOG_LEVEL_INFO    | 打印提示日志         |
| TMG_LOG_LEVEL_DEBUG   | 打印开发调试日志     |
| TMG_LOG_LEVEL_VERBOSE | 打印高频日志         |

#### 示例代码  

```
ITMGContext.GetInstance(this).SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```



### 设置打印日志路径

用于设置打印日志路径。默认路径为： /sdcard/Android/data/xxx.xxx.xxx/files。 需要在 Init 之前调用。

#### 接口原型

```
public abstract int SetLogPath(String logDir);
```

| 参数   |  类型  | 含义 |
| ------ | :----: | ---- |
| logDir | String | 路径 |

#### 示例代码  

```
ITMGContext.GetInstance(this).SetLogPath(path);
```

### 获取诊断信息

获取音视频通话的实时通话质量的相关信息。该接口主要用来查看实时通话质量、排查问题等，业务侧可以忽略。

#### 接口原型  

```
public abstract String GetQualityTips();
```

#### 示例代码  

```
ITMGContext.GetInstance(this).GetRoom().GetQualityTips();
```
## 回调消息


| 消息										|含义|Data                        | 例子                                                         |
| ----	|------| --- | -------------- |
|  ITMG_MAIN_EVENT_TYPE_ENTER_ROOM						| <div style="width: 150pt">进入音频房间消息			|result; error_info	| {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM						|退出音频房间消息			|result; error_info	| {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT					|房间因为网络等原因断开消息|result; error_info	| {"error_info":"waiting timeout, please check your network","result":0} |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE						|房间成员更新消息|user_list; event_id| {"event_id":1,"user_list":["0"]}                             |
| ITMG_MAIN_EVENT_TYPE_RECONNECT_START					|房间重连开始消息|result; error_info	| {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS				|房间重连成功消息|result; error_info	| {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_SWITCH_ROOM						|快速切换房间消息|result; error_info	| {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE					|房间状态切换消息|result; error_info; sub_event_type; new_room_type | {"error_info":"","new_room_type":0,"result":0}               |
| ITMG_MAIN_EVENT_TYPE_ROOM_SHARING_START				|开始跨房连麦消息|result;			| {"result":0} |
| ITMG_MAIN_EVENT_TYPE_ROOM_SHARING_STOP				|跨房连麦停止消息|result;			| {"result":0} |
| <div style="width: 250pt">ITMG_MAIN_EVENT_TYPE_SPEAKER_DEFAULT_DEVICE_CHANGED	|默认扬声器设备修改消息|result; error_info	| {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"扬声器 (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE				|新增扬声器设备消息|                result; error_info                 | {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"扬声器 (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE				|丢失扬声器设备消息| result; error_info                 | {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"扬声器 (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE			|新增麦克风设备消息|result; error_info                 | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"麦克风 (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE			|丢失麦克风设备消息|result; error_info                 | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"麦克风 (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_DEFAULT_DEVICE_CHANGED	|默认麦克风设备修改消息|result; error_info                 | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"麦克风 (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY		|房间质量消息|weight; loss; delay                | {"weight":5,"loss":0.1,"delay":1}                            |
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE		|语音消息录制完成消息|          result; file_path                 | {"file_path":"","result":0}                                  |
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE		|语音消息上传完成消息|result; file_path;file_id             | {"file_id":"","file_path":"","result":0}                     |
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE		|语音消息下载完成消息|result; file_path;file_id             | {"file_id":"","file_path":"","result":0}                     |
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE		|语音消息播放完成消息|result; file_path                 | {"file_path":"","result":0}                                  |
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE		|语音消息极速转文本完成消息|result; text;file_id                | {"file_id":"","text":"","result":0}                          |
|  <div style="width: 250pt">ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE|语音消息流式转文本完成消息|result; file_path; text;file_id          | {"file_id":"","file_path":","text":"","result":0}            |
|  <div style="width: 250pt">ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING |语音消息正在流式转文本中|result; file_path; text;file_id          | {"file_id":"","file_path":","text":"","result":0}            |
| ITMG_MAIN_EVNET_TYPE_PTT_TEXT2SPEECH_COMPLETE		|文本转语音完成消息|result; text;file_id                | {"file_id":"","text":"","result":0}                          |
| ITMG_MAIN_EVNET_TYPE_PTT_TRANSLATE_TEXT_COMPLETE	|文本翻译完成消息|result; text;file_id                | {"file_id":"","text":"","result":0}                          |
