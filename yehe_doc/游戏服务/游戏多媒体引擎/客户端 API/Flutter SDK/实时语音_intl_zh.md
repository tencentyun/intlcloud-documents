为方便 Flutter 开发者调试和接入腾讯云游戏多媒体引擎客户端 API，本文为您介绍适用于 Flutter 实时语音功能的开发接入技术文档。

## 使用 GME 重要事项

GME 提供实时语音服务、语音消息服务及转文本服务，使用 GME 服务都依赖 Init 和 Poll 等核心接口。

#### 重点提示
- 已完成 GME 应用创建，并获取 SDK AppID 和 Key。请参见 [服务开通指引](https://intl.cloud.tencent.com/document/product/607/10782)。

- 已开通 **GME 实时语音服务、语音消息服务以及转文本服务**。请参见 [服务开通指引](https://intl.cloud.tencent.com/document/product/607/10782)。

- GME 使用前请对工程进行配置，否则 SDK 不生效。

- GME 的接口调用成功后返回值为 GmeError.AV_OK，数值为 0。

- GME 的接口调用要在同一个线程下。

- GME 需要周期性的调用 Poll 接口触发事件回调。

- 错误码详情可参见 [错误码](https://intl.cloud.tencent.com/document/product/607/33223)。


## 接入 SDK

### 重要步骤

接入 SDK 重要流程如下：

![](https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg)
1. [初始化 GME](https://www.tencentcloud.com/document/product/607/53818)

2. [周期性调用 Poll 触发回调](https://www.tencentcloud.com/document/product/607/53818)

3. [进入实时语音房间](https://www.tencentcloud.com/document/product/607/53818)

4. [打开麦克风](https://www.tencentcloud.com/document/product/607/53818)

5. [打开扬声器](https://www.tencentcloud.com/document/product/607/53818)

6. [退出语音房间](https://www.tencentcloud.com/document/product/607/53818)

7. [反初始化 GME](https://www.tencentcloud.com/document/product/607/53818)


## 核心接口
<table>
<tr>
<td rowspan="1" colSpan="1" >接口</td>

<td rowspan="1" colSpan="1" >接口含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Init</td>

<td rowspan="1" colSpan="1" >初始化 GME</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Poll</td>

<td rowspan="1" colSpan="1" >触发事件回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Pause</td>

<td rowspan="1" colSpan="1" >系统暂停</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Resume</td>

<td rowspan="1" colSpan="1" >系统恢复</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Uninit</td>

<td rowspan="1" colSpan="1" >反初始化 GME</td>
</tr>
</table>


### 引用 GME 模块
``` bash
import 'package:gme/gme.dart';
import 'package:gme/gmeType.dart';
```

### 获取实例

在使用语音功能时，需要首先获取 GmeSDK 对象。
``` bash
ITMGContext context = ITMGContext.GetInstance();
```



### 初始化 SDK

未初始化前，SDK 处于未初始化阶段，**需要通过接口 Init 初始化 SDK**，才可以使用实时语音服务、语音消息服务及转文本服务。调用 Init 接口的线程必须于其他接口在同一线程,建议都在主线程调用接口。

#### 接口原型
``` bash
//class ITMGContext
Future<int> InitSDK(String appID, String openID)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sdkAppId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >来自 [腾讯云控制台](https://console.cloud.tencent.com/gamegme) 的 GME 服务提供的 AppID，获取请参见 [语音服务开通指引](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openID</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >openID 只支持int64 类型（转为 string 传入），规则由 App 开发者自行制定，App 内不重复即可。如需使用字符串作为 Openid 传入，可 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1) 联系开发者。</td>
</tr>
</table>


#### 返回值
<table>
<tr>
<td rowspan="1" colSpan="1" >返回值</td>

<td rowspan="1" colSpan="1" >处理</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GmeError.AV_OK= 0</td>

<td rowspan="1" colSpan="1" >初始化 SDK 成功</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >AV_ERR_SDK_NOT_FULL_UPDATE=7015</td>

<td rowspan="1" colSpan="1" >检查 SDK 文件是否完整，建议删除后重新导入 SDK</td>
</tr>
</table>


> **关于7015错误提示**
> 
> - 7015错误码是通过 md5 进行判断，在接入过程中若出现此错误，请根据提示检查 SDK 文件是否完整、SDK 文件版本是否一致。
> - 出现返回值 AV_ERR_SDK_NOT_FULL_UPDATE 时，此返回值**只有提示作用**，并不会造成初始化失败。
> - 由于第三方加固、Unity 打包机制等因素会影响库文件 md5，造成误判，所以**正式发布请在逻辑中忽略此错误**，并尽量不在 UI 中提示。


#### 示例代码
``` bash
string SDKAPPID3RD = "14000xxxxx";
string openId="10001";
int res = await ITMGContext.GetInstance().InitSDK(SDKAPPID3RD, openId);

if (ret != GmeError.AV_OK)
{
    print("Init SDK Error");
    return;
}
```

### 设置回调

接口类采用 Delegate 方法用于向应用程序发送回调通知。将回调函数注册给 SDK，用于接收回调的信息，需要在进房之前设置。

#### 函数原型及示例代码

设置回调，用于接收回调的信息，需要在进房之前设置。
``` bash
//在初始化 SDK 时候
ITMGContext.GetInstance().SetEvent(handleEventMsg);
//回调方法
void handleEventMsg(int eventType, String data) async {
    // enterRoom event
    print("AddDelegate3" + eventType.toString());
    switch (eventType) {
      case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
        //进房回调	
        }
        break;
      case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE:
        {
         //切换房间回调
        }
        break;
    }
}
```

### 触发事件回调

需要周期的调用 Poll 可以触发事件回调。Poll 是 GME 的消息泵，GME 需要周期性的调用 Poll 接口触发事件回调。如果没有调用 Poll ，将会导致整个 SDK 服务运行异常。详情请参见 [Sample Project](https://intl.cloud.tencent.com/document/product/607/18521)  中的 EnginePollHelper 文件。

> **务必周期性调用 Poll 接口**
> 

> 务必周期性调用 Poll 接口且在主线程调用，以免接口回调异常。
> 


#### 接口原型
``` bash
Future<void> Poll();
```

#### 示例代码
``` bash
  Future<void> pollTimer() async {_pollTimer = Timer.periodic(Duration(milliseconds: 100), (Timer timer) {
      ITMGContext.GetInstance().Poll();
    });
  }
```

### 系统暂停

当系统发生 Pause 事件时，需要同时通知引擎进行 Pause。例如在应用退后台时候（OnApplicationPause, isPause=True），如果不需要后台播放房间内声音，请调用 Pause 接口暂停整个 GME 服务。

#### 接口原型
``` bash
Future<int> Pause()
```

### 系统恢复

当系统发生 Resume 事件时，需要同时通知引擎进行 Resume。Resume 接口只恢复实时语音。

#### 接口原型
``` bash
Future<int> Resume()
```

### 反初始化 SDK

反初始化 SDK，进入未初始化状态。**如果游戏业务侧账号与 openid 是绑定的，那切换游戏账号需要反初始化 GME，再用新的 openid 初始化**。

#### 接口原型
``` bash
Future<int> Uninit()
```

## 实时语音房间相关接口

初始化之后，SDK 调用进房后进去了房间，才可以进行实时语音通话。
使用问题可参见 [实时语音相关问题](https://intl.cloud.tencent.com/document/product/607/39524)。

![](https://qcloudimg.tencent-cloud.cn/raw/02f98895d0b7bfe1bac774d5983289c1.jpg)
<table>
<tr>
<td rowspan="1" colSpan="1" >接口</td>

<td rowspan="1" colSpan="1" >接口含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GenAuthBuffer</td>

<td rowspan="1" colSpan="1" >本地鉴权计算</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnterRoom</td>

<td rowspan="1" colSpan="1" >加入房间</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ExitRoom</td>

<td rowspan="1" colSpan="1" >退出房间</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >IsRoomEntered</td>

<td rowspan="1" colSpan="1" >判断是否已经进入房间</td>
</tr>
</table>


### 本地鉴权计算

生成 AuthBuffer，用于相关功能的加密和鉴权，如正式发布请使用后台部署密钥，后台部署请参见 [鉴权密钥](https://intl.cloud.tencent.com/document/product/607/12218)。    

#### 接口原型
``` bash
Future<Uint8List> GenAuthBuffer(String appID, String roomID, String openID, String key)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >appID</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >来自腾讯云控制台的 AppID 号码。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >roomID</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >房间号，最大支持127字符。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openID</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >用户标识。与 Init 时候的 openID 相同。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >key</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >来自腾讯云 [控制台](https://console.cloud.tencent.com/gamegme) 的权限密钥。</td>
</tr>
</table>


#### 示例代码
``` bash
 Uint8List userSig = await ITMGContext.GetInstance().GenAuthBuffer(_editAppID.text, _editRoomID.text, _editOpenID.text, _editKey.text);
 int res = await ITMGContext.GetInstance().EnterRoom(_editRoomID.text, 1, userSig);
```

### 加入房间

用生成的鉴权信息进房，加入房间默认不打开麦克风及扬声器。

> **注意**
> 
> - 加入房间事件回调结果 result 为 0 代表进房成功，进房接口 EnterRoom 返回值为 0 不代表进房成功。
> - 房间的音频类型由第一个进房的人确定，此后房间里有成员修改房间类型，将对此房间所有成员生效。例如第一个进入房间的人使用的房间音频类型是流畅音质，第二个进房的是即使进房时候调用接口的音频类型参数是高清音质，进入房间之后也会变成流畅音质。需要有成员调用 ChangeRoomType 才会修改房间的音频类型。


#### 接口原型
``` bash
Future<int> EnterRoom(String roomID, int roomType, Uint8List authBuffer)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >roomId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >房间号，最大支持127字符</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >roomType</td>

<td rowspan="1" colSpan="1" >ITMGRoomType</td>

<td rowspan="1" colSpan="1" >房间类型，游戏建议使用  ITMG_ROOM_TYPE_FLUENCY。房间音频类型请参见 [音质选择](https://intl.cloud.tencent.com/document/product/607/18522)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >appKey</td>

<td rowspan="1" colSpan="1" >Uint8List</td>

<td rowspan="1" colSpan="1" >鉴权码</td>
</tr>
</table>


#### 示例代码
``` bash
int res = await ITMGContext.GetInstance().EnterRoom(_editRoomID.text, 1, authBuffer);
```

#### 加入房间事件回调

加入房间完成后会通过回调返回ITMG_MAIN_EVENT_TYPE_ENTER_ROOM事件类型返回进房结果，监听进房结果事件后进行处理。如果回调为成功，即此时进房成功，开始进行**计费**。

> **计费问题参考：**
> 
> - [购买指南。](https://intl.cloud.tencent.com/document/product/607/50009)
> - [计费相关问题。](https://intl.cloud.tencent.com/document/product/607/30255)
> - [使用实时语音后，如果客户端掉线了，是否还会继续计费？](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)


#### 示例代码
``` bash
//对事件进行监听：
void handleEventMsg(int eventType, String data) async {
  switch (eventType) {
      case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
      {
        //进房后续流程处理
      }
  }
}
ITMGContext.GetInstance().SetEvent(handleEventMsg);
```

#### Data 详情
<table>
<tr>
<td rowspan="1" colSpan="1" >消息</td>

<td rowspan="1" colSpan="1" >Data</td>

<td rowspan="1" colSpan="1" >例子</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_ENTER_ROOM</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"waiting timeout, please check your network","result":0}</td>
</tr>
</table>


如果断网，将会有断网的回调提示 `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT`，此时 SDK 会自动进行重连，回调是 `ITMG_MAIN_EVENT_TYPE_RECONNECT_START`，当重连成功时，会有 `ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS` 回调。

#### 错误码
<table>
<tr>
<td rowspan="1" colSpan="1" >错误码值</td>

<td rowspan="1" colSpan="1" >原因及建议方案</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >7006</td>

<td rowspan="1" colSpan="1" >鉴权失败原因：<br>- AppID 不存在或者错误<br>- authbuff 鉴权错误<br>- 鉴权过期 <br>- OpenId 不符合规范</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >7007</td>

<td rowspan="1" colSpan="1" >已经在其它房间</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >1001</td>

<td rowspan="1" colSpan="1" >已经在进房过程中，然后又重复了此操作。建议在进房回调返回之前不要再调用进房接口</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >1003</td>

<td rowspan="1" colSpan="1" >已经进房了在房间中，又调用一次进房接口</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >1101</td>

<td rowspan="1" colSpan="1" >确保已经初始化 SDK，确保 OpenId 是否符合规则，或者确保在同一线程调用接口，以及确保 Poll 接口正常调用</td>
</tr>
</table>


### 退出房间

通过调用此接口可以退出所在房间。这是一个异步接口，返回值为 AV_OK 的时候代表异步投递成功。如果应用中有退房后立即进房的场景，在接口调用流程上，开发者无需要等待 ExitRoom 的回调 RoomExitComplete 通知，只需直接调用接口。

#### 接口原型
``` bash
Future<int> ExitRoom()
```

#### 示例代码
``` bash
ITMGContext.GetInstance().ExitRoom();
```

#### 退出房间事件回调

退出房间完成后会有回调，消息为 ITMG_MAIN_EVENT_TYPE_EXIT_ROOM。示例代码如下：

#### 示例代码
``` bash
void handleEventMsg(int eventType, String data) async{
  switch (eventType) {
      case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
      {
      //退房后续进行处理
        break;
      }
  }
}
ITMGContext.GetInstance().SetEvent(handleEventMsg);
```

### 判断是否已经进入房间

通过调用此接口可以判断是否已经进入房间，返回值为 bool 类型。请勿在进房过程中调用。

#### 接口原型
``` bash
Future<bool> IsRoomEntered()
```

#### 示例代码
``` bash
bool res = await ITMGContext.GetInstance().IsRoomEntered();
```

## 房间内状态维护

此部分接口用于业务层显示说话成员、进退房成员，以及将房间内某成员禁言等功能。

![](https://main.qcloudimg.com/raw/33eecfcd9e18a361aa0b732ffd0fb7dd.png)
<table>
<tr>
<td rowspan="1" colSpan="1" >接口/通知</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_USER_UPDATE</td>

<td rowspan="1" colSpan="1" >成员状态变化通知</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >AddAudioBlackList</td>

<td rowspan="1" colSpan="1" >房间中禁言某成员</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >RemoveAudioBlackList</td>

<td rowspan="1" colSpan="1" >移除禁言</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >IsOpenIdInAudioBlackList</td>

<td rowspan="1" colSpan="1" >查询某openid是否被禁言</td>
</tr>
</table>


### 成员进房、说话状态通知事件
- 该事件适用于获取房间中说话的人并在 UI 中展示，以及有人进入、退出语音房间的一个通知。

- 该事件在状态变化才通知，状态不变化的情况下不通知。如需实时获取成员状态，请在业务层收到通知时缓存，事件消息为 ITMG_MAIN_EVNET_TYPE_USER_UPDATE，包含 event_id、count 及 openIdList，在 OnEvent 通知中对事件消息进行判断。

- 音频事件 EVENT_ID_ENDPOINT_NO_AUDIO 的通知有一个阈值，超过这个阈值才会发送通知。即本端两秒没采集到声音后， 房间其他成员才收到本端停止说话的通知。

- 音频事件只会返回成员说话状态，没有返回具体的音量。如需房间内成员具体音量可使用接口 GetVolumeById 进行获取。

<table>
<tr>
<td rowspan="1" colSpan="1" >event_id</td>

<td rowspan="1" colSpan="1" >含义</td>

<td rowspan="1" colSpan="1" >应用侧维护内容</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EVENT_ID_ENDPOINT_ENTER</td>

<td rowspan="1" colSpan="1" >有成员进入房间，返回此时进房的 openid</td>

<td rowspan="1" colSpan="1" >应用侧维护成员列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EVENT_ID_ENDPOINT_EXIT</td>

<td rowspan="1" colSpan="1" >有成员退出房间，返回此时退房的 openid</td>

<td rowspan="1" colSpan="1" >应用侧维护成员列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EVENT_ID_ENDPOINT_HAS_AUDIO</td>

<td rowspan="1" colSpan="1" >有成员发送音频包，返回此时房间内说话的 openid，通过此事件可以判断用户是否说话，并展示声纹效果</td>

<td rowspan="1" colSpan="1" >应用侧维护通话成员列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EVENT_ID_ENDPOINT_NO_AUDIO</td>

<td rowspan="1" colSpan="1" >有成员停止发送音频包，返回此时房间内停止说话的 openid</td>

<td rowspan="1" colSpan="1" >应用侧维护通话成员列表</td>
</tr>
</table>


#### 示例代码
``` bash
void handleEventMsg(int eventType, String data) async {
  if (eventType == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
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
}
```

### 房间中禁言某成员

将某个 ID 加入音频数据黑名单，即不接受某人的语音， 只对本端生效，不会影响其他端。返回值为 0 表示调用成功。例如 ：A、B、C 都在同一个房间开麦说话： 
- 如果 A 设置了 C 的黑名单， 则 A 只能听见 B 的声音。

- B 因为没有设置黑名单， 仍旧可以听见 A 和 C 的声音。

- C 同样因为没有设置黑名单， 可以听见 A 和 B 的声音。


   此接口适用于在语音房间中将某用户禁言的场景。


#### 接口原型
``` bash
Future<int> AddAudioBlackList(String openID) 
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openID</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >需添加黑名单的用户 openid</td>
</tr>
</table>


#### 示例代码
``` bash
res = await ITMGContext.GetInstance().GetAudioCtrl().AddAudioBlackList(_editRoomManagerID.text);
```

### 移除禁言

将某个 Id 移除音频数据黑名单。返回值为0表示调用成功。

#### 接口原型
``` bash
Future<int> RemoveAudioBlackList(String openID)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >需移除黑名单的 ID</td>
</tr>
</table>


#### 示例代码
``` bash
res = await ITMGContext.GetInstance().GetAudioCtrl().RemoveAudioBlackList(_editRoomManagerID.text);
```

## 实时语音采集相关接口
- 初始化 SDK 之后进房，在房间中，才可以调用实时音频语音相关接口。

- 当用户界面单击打开/关闭麦克风/扬声器按钮时，建议采用 EnableMic 以及 EnableSpeaker 接口进行调用。

- 当用户界面按住麦克风按钮时发言，放开按钮不发言，建议采用进房时候调用 EnableAudioCaptureDevice 一次，后续按住发言调用 EnableAudioSend 来实现。

<table>
<tr>
<td rowspan="1" colSpan="1" >接口</td>

<td rowspan="1" colSpan="1" >接口含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnableMic</td>

<td rowspan="1" colSpan="1" >开关麦克风</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetMicState</td>

<td rowspan="1" colSpan="1" >获取麦克风状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnableAudioCaptureDevice</td>

<td rowspan="1" colSpan="1" >开关采集设备</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >IsAudioCaptureDeviceEnabled</td>

<td rowspan="1" colSpan="1" >获取采集设备状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnableAudioSend</td>

<td rowspan="1" colSpan="1" >打开关闭音频上行</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >IsAudioSendEnabled</td>

<td rowspan="1" colSpan="1" >获取音频上行状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetMicLevel</td>

<td rowspan="1" colSpan="1" >获取实时麦克风音量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetSendStreamLevel</td>

<td rowspan="1" colSpan="1" >获取音频上行实时音量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SetMicVolume</td>

<td rowspan="1" colSpan="1" >设置麦克风音量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetMicVolume</td>

<td rowspan="1" colSpan="1" >获取麦克风音量</td>
</tr>
</table>




### 开启或关闭麦克风

此接口用来开启关闭麦克风。加入房间默认不打开麦克风及扬声器。**EnableMic = EnableAudioCaptureDevice + EnableAudioSend**

#### 接口原型
``` bash
Future<int> EnableMic(bool enable)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isEnabled</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >如果需要打开麦克风，则传入的参数为 true，如果关闭麦克风，则参数为 false</td>
</tr>
</table>


#### 示例代码
``` bash
//打开麦克风
int res = await ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```

### 麦克风状态获取

此接口用于获取麦克风状态，返回值0为关闭麦克风状态，返回值1为打开麦克风状态。

#### 接口原型
``` bash
Future<int> GetMicState()
```

#### 示例代码
``` bash
int micState = await ITMGContext.GetInstance().GetAudioCtrl().GetMicState();
```

### 开启或关闭采集设备

此接口用来开启/关闭采集设备。加入房间默认不打开设备。
- 只能在进房后调用此接口，退房会自动关闭设备。

- 在移动端，打开采集设备通常会伴随权限申请，音量类型调整等操作。


#### 接口原型
``` bash
Future<int> EnableAudioCaptureDevice(bool enable)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >如果需要打开采集设备，则传入的参数为 true，如果关闭采集设备，则参数为 false</td>
</tr>
</table>


#### 示例代码
``` bash
//打开采集设备
int res = await ITMGContext.GetInstance().GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### 采集设备状态获取

此接口用于采集设备状态获取。

#### 接口原型
``` bash
Future<bool> IsAudioCaptureDeviceEnabled()
```

#### 示例代码
``` bash
bool res = await ITMGContext.GetInstance().GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### 打开或关闭音频上行

此接口用于打开/关闭音频上行。如果采集设备已经打开，那么会发送采集到的音频数据。如果采集设备没有打开，那么仍旧无声。采集设备的打开关闭请参见接口 EnableAudioCaptureDevice。

#### 接口原型
``` bash
Future<int> EnableAudioSend(bool enable)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isEnabled</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >如果需要打开音频上行，则传入的参数为 true，如果关闭音频上行，则参数为 false</td>
</tr>
</table>


#### 示例代码
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().EnableAudioSend(isCheck);
```

### 音频上行状态获取

此接口用于音频上行状态获取。

#### 接口原型
``` bash
Future<bool> IsAudioSendEnabled() 
```

#### 示例代码
``` bash
bool IsAudioSend = await ITMGContext.GetInstance().GetAudioCtrl().IsAudioSendEnabled();
```

### 获取麦克风实时音量

此接口用于获取麦克风实时音量，返回值为 number 类型。建议20ms获取一次。值域为0 - 100，通过此接口可以获取到麦克风采集到的实时音量情况。

#### 接口原型
``` bash
Future<int> GetMicLevel()
```

#### 示例代码
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().GetMicLevel();
```

### 获取音频上行实时音量

此接口用于获取自己音频上行实时音量，返回值为 number 类型，取值范围为0 - 100。

#### 接口原型
``` bash
Future<int> GetSendStreamLevel()
```

#### 示例代码
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().GetSendStreamLevel();
```

### 设置麦克风软件音量

此接口用于设置麦克风的音量。参数 volume 用于设置麦克风的音量，相当于对采集的声音做衰减或增益。

#### 接口原型
``` bash
 Future<int> SetMicVolume(int volume)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >取值范围为 0-200，数值为0的时候表示静音，当数值为100的时候表示音量不增不减，默认数值为100。</td>
</tr>
</table>


#### 示例代码
``` bash
int volume = 100;
int res = await ITMGContext.GetInstance().GetAudioCtrl().SetMicVolume(volume);
```

### 获取麦克风软件音量

此接口用于获取麦克风的音量。返回值为一个number类型数值，返回值为101代表没调用过接口 SetMicVolume。

#### 接口原型
``` bash
Future<int> GetMicVolume()
```

#### 示例代码
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().GetMicVolume();
```

## 实时语音播放相关接口
<table>
<tr>
<td rowspan="1" colSpan="1" >接口</td>

<td rowspan="1" colSpan="1" >接口含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnableSpeaker</td>

<td rowspan="1" colSpan="1" >开关扬声器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetSpeakerState</td>

<td rowspan="1" colSpan="1" >获取扬声器状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnableAudioPlayDevice</td>

<td rowspan="1" colSpan="1" >开关播放设备</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >IsAudioPlayDeviceEnabled</td>

<td rowspan="1" colSpan="1" >获取播放设备状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >EnableAudioRecv</td>

<td rowspan="1" colSpan="1" >打开关闭音频下行</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >IsAudioRecvEnabled</td>

<td rowspan="1" colSpan="1" >获取音频下行状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetSpeakerLevel</td>

<td rowspan="1" colSpan="1" >获取实时扬声器音量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetRecvStreamLevel</td>

<td rowspan="1" colSpan="1" >获取房间内其他成员下行实时音量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SetSpeakerVolume</td>

<td rowspan="1" colSpan="1" >设置扬声器音量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GetSpeakerVolume</td>

<td rowspan="1" colSpan="1" >获取扬声器音量</td>
</tr>
</table>




### 开启或关闭扬声器

此接口用于开启关闭扬声器。**EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv**

#### 接口原型
``` bash
Future<int> EnableSpeaker(bool enable)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >bEnable</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >如果需要关闭扬声器，则传入的参数为 false，如果打开扬声器，则参数为 true</td>
</tr>
</table>


#### 示例代码
``` bash
//打开扬声器
await ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(isCheck);
```

### 扬声器状态获取

此接口用于扬声器状态获取。返回值0为关闭扬声器状态，返回值1为打开扬声器状态。

#### 接口原型
``` bash
Future<int> GetSpeakerState() 
```

#### 示例代码
``` bash
int spkState = await ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerState();
```

### 开启或关闭播放设备

此接口用于开启关闭播放设备。

#### 接口原型
``` bash
Future<int> EnableAudioPlayDevice(bool enable) 
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >如果需要关闭播放设备，则传入的参数为 false，如果打开播放设备，则参数为 true</td>
</tr>
</table>


#### 示例代码
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().EnableAudioPlayDevice(isCheck);
```

### 播放设备状态获取

此接口用于播放设备状态获取。

#### 接口原型
``` bash
Future<bool> IsAudioPlayDeviceEnabled()
```

#### 示例代码
``` bash
bool res = await ITMGContext.GetInstance().GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### 打开或关闭音频下行

此接口用于打开/关闭音频下行。如果播放设备已经打开，那么会播放房间里其他人的音频数据。如果播放设备没有打开，那么仍旧无声。播放设备的打开关闭参见接口请参见 EnableAudioPlayDevice。

#### 接口原型
``` bash
Future<int> EnableAudioRecv(bool enable)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isEnabled</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >如果需要打开音频下行，则传入的参数为 true，如果关闭音频下行，则参数为 false</td>
</tr>
</table>


#### 示例代码
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().EnableAudioRecv(isCheck);
```

### 音频下行状态获取

此接口用于音频下行状态获取。

#### 接口原型
``` bash
Future<bool> IsAudioRecvEnabled() 
```

#### 示例代码
``` bash
bool res = await ITMGContext.GetInstance().GetAudioCtrl().IsAudioRecvEnabled();
```

### 获取扬声器实时音量

此接口用于获取扬声器实时音量。返回值为 number 类型数值，表示扬声器实时音量。建议20ms获取一次。

#### 接口原型
``` bash
Future<int> GetSpeakerLevel()
```

#### 示例代码
``` bash
bool res = await ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerLevel();
```

### 获取房间内其他成员下行实时音量

此接口用于获取房间内其他成员下行实时音量，返回值为 number 类型，取值范围为0 - 200。

#### 接口原型
``` bash
Future<int> GetRecvStreamLevel(String openID)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >房间其他成员的openId</td>
</tr>
</table>


#### 示例代码
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().GetRecvStreamLevel(_editRoomManagerID.text);
```

### 动态设置房间内某成员音量

此接口用于设置房间内某成员的说话音量大小，此设置只在本端生效。

#### 接口原型
``` bash
Future<int> SetSpeakerVolumeByOpenID(String openId, int volume)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >需要调节音量大小的OpenID</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >百分比，建议[0-200]，其中100为默认值</td>
</tr>
</table>


#### 示例代码
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolumeByOpenID(_editRoomManagerID.text, 100);
```

### 获取设置的声音百分比

调用此接口获取 SetSpeakerVolumeByOpenID 设置的能量值

#### 接口原型
``` bash
Future<int> GetSpeakerVolumeByOpenID(String openId)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >openId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >需要调节音量大小的OpenID</td>
</tr>
</table>


#### 返回值

接口返回 OpenID 设置的能量百分比， 默认返回100。

#### 示例代码
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerVolumeByOpenID(_editRoomManagerID.text);
```

### 设置扬声器的音量

此接口用于设置扬声器的音量。

#### 接口原型
``` bash
Future<int> SetSpeakerVolume(int volume)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >设置音量，范围0 - 200，当数值为0时，表示静音，当数值为100时，表示音量不增不减，默认数值为100。</td>
</tr>
</table>


#### 示例代码
``` bash
int volume = value.toInt();
int res = await ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolume(volume);
```

### 获取扬声器的音量

此接口用于获取扬声器的音量。返回值为 number 类型数值，代表扬声器的音量，返回值为101代表没调用过接口 SetSpeakerVolume。
Level 是实时音量，Volume 是扬声器的音量，最终声音音量 =  Level × Volume %。例如实时音量是数值是100，此时 Volume 的数值是60，那么最终发出来的声音数值也是60。

#### 接口原型
``` bash
Future<int> GetSpeakerVolume() 
```

#### 示例代码
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerVolume();
```

## 高级 API

### 启动耳返

此接口用于启动耳返，需要 EnableLoopBack+EnableSpeaker 才可以听到自己声音。

#### 接口原型
``` bash
Future<int> EnableLoopBack(bool enable)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >bool</td>

<td rowspan="1" colSpan="1" >设置是否启动</td>
</tr>
</table>


#### 示例代码
``` bash
int res = await ITMGContext.GetInstance().GetAudioCtrl().EnableLoopBack(true);
```

### 获取用户房间音频类型

此接口用于获取用户房间音频类型，返回值为房间音频类型，返回值为0时代表获取用户房间音频类型发生错误，房间音频类型参考 EnterRoom 接口。

#### 接口原型
``` bash
Future<int> GetRoomType()
```

#### 示例代码
``` bash
int curType = await ITMGContext.GetInstance().GetRoom().GetRoomType();
```

### 房间类型修改

此接口用于修改用户房间音频类型，结果参见回调事件，事件类型为 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE。房间的音频类型由第一个进房的人确定，此后房间里有成员修改房间类型，将对此房间所有成员生效。

#### 接口原型
``` bash
Future<int> ChangeRoomType(int roomType)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >roomtype</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >房间切换成的目标类型，房间音频类型参考 EnterRoom 接口</td>
</tr>
</table>


#### 示例代码
``` bash
int res = await ITMGContext.GetInstance().GetRoom().ChangeRoomType(1);
```

#### 回调事件

房间类型设置完成后，回调的事件消息为 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE，返回的参数为 result、error_info 及 new_room_type，new_room_type 代表的信息如下，在 OnEvent 函数中对事件消息进行判断。
<table>
<tr>
<td rowspan="1" colSpan="1" >事件子类型</td>

<td rowspan="1" colSpan="1" >代表参数</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_ROOM_CHANGE_EVENT_ENTERROOM</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >表示在进房的过程中，自带的音频类型与房间不符合，被修改为所进入房间的音频类型</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_ROOM_CHANGE_EVENT_START</td>

<td rowspan="1" colSpan="1" >2</td>

<td rowspan="1" colSpan="1" >表示已经在房间内，音频类型开始切换（例如调用 ChangeRoomType 接口后切换音频类型 ）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_ROOM_CHANGE_EVENT_COMPLETE</td>

<td rowspan="1" colSpan="1" >3</td>

<td rowspan="1" colSpan="1" >表示已经在房间，音频类型切换完成</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_ROOM_CHANGE_EVENT_REQUEST</td>

<td rowspan="1" colSpan="1" >4</td>

<td rowspan="1" colSpan="1" >表示房间成员调用 ChangeRoomType 接口，请求切换房间音频类型</td>
</tr>
</table>


#### 示例代码
``` bash
case ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE:
  {
        //对房间类型事件进行处理
  }
  break;
```

### 房间通话质量监控事件

质量监控事件，此通知事件适用于监听网络质量，如果用户网络差的话，业务层将通过 UI 提醒用户切换网络。在进房后触发，事件2秒回调一次，事件消息为 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY，返回的参数为 weight、loss 及 delay，代表的信息如下：
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >weight</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >范围是1 - 50，数值为50是音质评分极好，数值为1是音质评分很差，几乎不能使用，数值为0代表初始值，无含义。一般数值在30以下就可以提醒用户网络较差，建议切换网络。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >loss</td>

<td rowspan="1" colSpan="1" >var</td>

<td rowspan="1" colSpan="1" >上行丢包率。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >delay</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >音频触达延迟时间（ms）。</td>
</tr>
</table>


### 获取版本号

获取 SDK 版本号，用于分析。

#### 接口原型
``` bash
Future<String> GetSDKVersion()
```

#### 示例代码
``` bash
_sdkVersions = await ITMGContext.GetInstance().GetSDKVersion();
```

### 设置应用名称和版本

该接口用于设置应用名称和版本

#### 接口原型
``` bash
Future<void> SetAppVersion(String appVersion)
```

#### 参数含义
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >appVersion</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >应用名称和版本</td>
</tr>
</table>


#### 示例代码
``` bash
await ITMGContext.GetInstance().SetAppVersion("gme V2.0.0");
```

### 设置打印日志等级

用于设置打印日志等级。建议保持默认等级。需要在 Init 之前调用。

#### 接口原型
``` bash
Future<int> SetLogLevel(int levelWrite, int levelPrint)
```

#### 参数含义
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >level</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >设置日志的等级，TMG_LOG_LEVEL_NONE 表示不写入，默认为 TMG_LOG_LEVEL_INFO</td>
</tr>
</table>


level 说明如下：
<table>
<tr>
<td rowspan="1" colSpan="1" >level</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_NONE</td>

<td rowspan="1" colSpan="1" >不打印日志</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_ERROR</td>

<td rowspan="1" colSpan="1" >打印错误日志（默认）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_INFO</td>

<td rowspan="1" colSpan="1" >打印提示日志</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_DEBUG</td>

<td rowspan="1" colSpan="1" >打印开发调试日志</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_VERBOSE</td>

<td rowspan="1" colSpan="1" >打印高频日志</td>
</tr>
</table>


#### 示例代码
``` bash
ITMGContext.GetInstance().SetLogLevel(ITMG_LOG_LEVEL.TMG_LOG_LEVEL_ERROR, ITMG_LOG_LEVEL.TMG_LOG_LEVEL_ERROR);
```

### 设置打印日志路径

用于设置打印日志路径。默认路径如下。需要在 Init 之前调用。

#### 接口原型
``` bash
Future<int> SetLogPath(String logDir)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >含义</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >logPath</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >路径</td>
</tr>
</table>


#### 示例代码
``` bash
String curPath = ""//自行设置路径
ITMGContext.GetInstance().SetLogPath(curPath);
```

### 获取诊断信息

获取音视频通话的实时通话质量的相关信息。该接口主要用来查看实时通话质量、排查问题等，业务侧可以忽略。

#### 接口原型
``` bash
Future<String> GetQualityTips()
```

#### 示例代码
``` bash
String curQualityTips = await ITMGContext.GetInstance().GetRoom().GetQualityTips();
```

### 回调消息
<table>
<tr>
<td rowspan="1" colSpan="1" >消息</td>

<td rowspan="1" colSpan="1" >含义</td>

<td rowspan="1" colSpan="1" >Data</td>

<td rowspan="1" colSpan="1" >例子｜</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_ENTER_ROOM</td>

<td rowspan="1" colSpan="1" >进入音频房间消息</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_EXIT_ROOM</td>

<td rowspan="1" colSpan="1" >退出音频房间消息</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT</td>

<td rowspan="1" colSpan="1" >房间因为网络等原因断开消息</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"waiting timeout, please check your network","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_USER_UPDATE</td>

<td rowspan="1" colSpan="1" >房间成员更新消息</td>

<td rowspan="1" colSpan="1" >user_list; event_id</td>

<td rowspan="1" colSpan="1" >{"event_id":1,"user_list":["0"]}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_RECONNECT_START</td>

<td rowspan="1" colSpan="1" >房间重连开始消息</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS</td>

<td rowspan="1" colSpan="1" >房间重连成功消息</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_SWITCH_ROOM</td>

<td rowspan="1" colSpan="1" >快速切换房间消息</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"error_info":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE</td>

<td rowspan="1" colSpan="1" >房间状态切换消息</td>

<td rowspan="1" colSpan="1" >result; error_info; sub_event_type; new_room_type</td>

<td rowspan="1" colSpan="1" >{"error_info":"","new_room_type":0,"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_ROOM_SHARING_START</td>

<td rowspan="1" colSpan="1" >开始跨房连麦消息</td>

<td rowspan="1" colSpan="1" >result;</td>

<td rowspan="1" colSpan="1" >{"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_ROOM_SHARING_STOP</td>

<td rowspan="1" colSpan="1" >跨房连麦停止消息</td>

<td rowspan="1" colSpan="1" >result;</td>

<td rowspan="1" colSpan="1" >{"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_SPEAKER_DEFAULT_DEVICE_CHANGED</td>

<td rowspan="1" colSpan="1" >默认扬声器设备修改消息</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"扬声器 (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE</td>

<td rowspan="1" colSpan="1" >新增扬声器设备消息</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"扬声器 (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE</td>

<td rowspan="1" colSpan="1" >丢失扬声器设备消息</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"扬声器 (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE</td>

<td rowspan="1" colSpan="1" >新增麦克风设备消息</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"麦克风 (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE</td>

<td rowspan="1" colSpan="1" >丢失麦克风设备消息</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"麦克风 (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_MIC_DEFAULT_DEVICE_CHANGED</td>

<td rowspan="1" colSpan="1" >默认麦克风设备修改消息</td>

<td rowspan="1" colSpan="1" >result; error_info</td>

<td rowspan="1" colSpan="1" >{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"麦克风 (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY</td>

<td rowspan="1" colSpan="1" >房间质量消息</td>

<td rowspan="1" colSpan="1" >weight; loss; delay</td>

<td rowspan="1" colSpan="1" >{"weight":5,"loss":0.1,"delay":1}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE</td>

<td rowspan="1" colSpan="1" >语音消息录制完成消息</td>

<td rowspan="1" colSpan="1" >result; file_path</td>

<td rowspan="1" colSpan="1" >{"file_path":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE</td>

<td rowspan="1" colSpan="1" >语音消息上传完成消息</td>

<td rowspan="1" colSpan="1" >result; file_path;file_id</td>

<td rowspan="1" colSpan="1" >{"file_id":"","file_path":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE</td>

<td rowspan="1" colSpan="1" >语音消息下载完成消息</td>

<td rowspan="1" colSpan="1" >result; file_path;file_id</td>

<td rowspan="1" colSpan="1" >{"file_id":"","file_path":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE</td>

<td rowspan="1" colSpan="1" >语音消息播放完成消息</td>

<td rowspan="1" colSpan="1" >result; file_path</td>

<td rowspan="1" colSpan="1" >{"file_path":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE</td>

<td rowspan="1" colSpan="1" >语音消息极速转文本完成消息</td>

<td rowspan="1" colSpan="1" >result; text;file_id</td>

<td rowspan="1" colSpan="1" >{"file_id":"","text":"","result":0}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE</td>

<td rowspan="1" colSpan="1" >语音消息流式转文本完成消息</td>

<td rowspan="1" colSpan="1" >result; file_path; text;file_id</td>

<td rowspan="1" colSpan="1" >{{"file_id":"","file_path":","text":"","result":0}}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING</td>

<td rowspan="1" colSpan="1" >语音消息正在流式转文本中</td>

<td rowspan="1" colSpan="1" >result; file_path; text;file_id</td>

<td rowspan="1" colSpan="1" >{{"file_id":"","file_path":","text":"","result":0}}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_TEXT2SPEECH_COMPLETE</td>

<td rowspan="1" colSpan="1" >文本转语音完成消息</td>

<td rowspan="1" colSpan="1" >result; text;file_id</td>

<td rowspan="1" colSpan="1" >{{"file_id":"","text":"","result":0}}</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ITMG_MAIN_EVNET_TYPE_PTT_TRANSLATE_TEXT_COMPLETE</td>

<td rowspan="1" colSpan="1" >文本翻译完成消息</td>

<td rowspan="1" colSpan="1" >result; text;file_id</td>

<td rowspan="1" colSpan="1" >{{"file_id":"","text":"","result":0}}</td>
</tr>
</table>
